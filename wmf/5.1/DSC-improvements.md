---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Vylepšení DSC ve WMF 5.1
ms.openlocfilehash: 92f82d62550e105a187fd7c0c58b49367c646a7e
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523018"
---
# <a name="improvements-in-desired-state-configuration-dsc-in-wmf-51"></a>Vylepšení Desired State Configuration (DSC) ve WMF 5.1

## <a name="dsc-class-resource-improvements"></a>Vylepšení prostředků třídy DSC

Ve WMF 5.1 jsme vyřešili následující známé problémy:

- Get-DscConfiguration může vrátit prázdné hodnoty (null) nebo chyby, pokud je typ tabulky komplexní a hodnoty hash vrácená funkcí Get() prostředku DSC založené na třídě.
- Get-DscConfiguration vrátí chybu, pokud se přihlašovací údaje Spustit jako se používá v konfiguraci DSC.
- Založené na třídě prostředků nelze použít v složené konfiguraci.
- Start-DscConfiguration přestane reagovat, pokud má vlastnost vlastní typ založené na třídě prostředků.
- Založené na třídě prostředků nelze použít jako výhradní prostředků.

## <a name="dsc-resource-debugging-improvements"></a>Vylepšení ladění prostředků DSC

Ve WMF 5.0 ladicí program Powershellu se nezastavil u metody založené na třídě prostředků (Get/Set/Test) přímo.
Ladicí program se zastaví ve WMF 5.1 u metody založené na třídě prostředků stejným způsobem jako u metody založené na souboru MOF prostředky.

## <a name="dsc-pull-client-supports-tls-11-and-tls-12"></a>DSC o přijetí změn klient podporuje protokol TLS 1.1 a TLS 1.2

Dříve DSC načítacího klienta podporuje jenom SSL3.0 a protokol TLS 1.0 prostřednictvím připojení prostřednictvím protokolu HTTPS.
Při vynucené bezpečnější protokoly by načítacího klienta přestane fungovat.
Ve WMF 5.1 DSC načítacího klienta už podporuje protokol SSL 3.0 a přidává podporu pro bezpečnější protokoly TLS 1.1 a TLS 1.2.

## <a name="improved-pull-server-registration"></a>Registrace serveru Vylepšený o přijetí změn

V dřívějších verzích WMF souběžných registrací/reporting požadavků na serveru vyžádané replikace DSC při používání databáze ESENT povede k LCM selhání registrace a/nebo sestavy.
V takovém případě protokolů událostí na serveru vyžádané replikace obsahuje chybu "Název Instance již používán."
Důvodem byla nesprávné způsob, jak získat přístup k databázi ESENT ve scénáři s více procesy.
Ve WMF 5.1 Tento problém vyřešen.
Souběžných registrací nebo vytváření sestav (zahrnující ESENT databáze) funguje bez problémů ve WMF 5.1.
Tento problém se vztahuje pouze na databázi ESENT a se nedá použít u databáze OLEDB.

## <a name="enable-circular-log-on-esent-database-instance"></a>Povolit cyklického protokolu v instanci databáze ESENT

Ve verzi eariler DSC PullServer byly soubory protokolů databáze ESENT zaplnění místa na disku becouse pullserver, které při vytváření instance databáze bez cyklické protokolování. V této verzi máte možnost řídit chování instance pomocí souboru web.config pullserver cyklické protokolování. Ve výchozím nastavení je CircularLogging nastavena na hodnotu TRUE.

```
<appSettings>
    <add key="dbprovider" value="ESENT" />
    <add key="dbconnectionstr" value="C:\Program Files\WindowsPowerShell\DscService\Devices.edb" />
    <add key="CheckpointDepthMaxKB" value="512" />
    <add key="UseCircularESENTLogs" value="TRUE" />
  </appSettings>
```

## <a name="pull-partial-configuration-naming-convention"></a>O přijetí změn zásady vytváření názvů částečné konfigurace

V předchozí verzi zásady vytváření názvů pro částečné konfigurace bylo, že název souboru MOF v serveru nebo služby o přijetí změn by měl odpovídat názvu konfigurace částečné zadaný v nastavení místního configuration manager, které pak musí odpovídat Název konfigurace vložený do souboru MOF.

Zobrazit snímky níže:

- Místní konfigurační nastavení, která definuje částečné konfigurace, který uzel může přijímat.

![Ukázka metaconfiguration](../images/MetaConfigPartialOne.png)

- Ukázková definice částečné konfigurace

```powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

- "ConfigurationName" vložen do generovaného souboru MOF.

![Ukázkový soubor generovaný soubor mof](../images/PartialGeneratedMof.png)

- Název souboru v úložišti o přijetí změn konfigurace.

![Název souboru v úložišti konfigurace.](../images/PartialInConfigRepository.png)

Název služby Azure Automation generované soubory MOF jako `<ConfigurationName>.<NodeName>.mof`.
Konfigurace níže tak kompiluje PartialOne.localhost.mof.

Kvůli tomu bylo možné pro akce pull, jedna částečná konfigurace ze služby Azure Automation.

```powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

Ve WMF 5.1 částečné konfigurace v serveru nebo služby o přijetí změn může mít název jako `<ConfigurationName>.<NodeName>.mof`.
Kromě toho pokud počítač s konfigurací jedné z o přijetí změn táhne server nebo služba potom konfiguračního souboru v úložišti konfigurace serveru o přijetí změn může mít libovolný název souboru.
Pojmenování díky této flexibilitě vám umožní spravovat uzly částečně ve službě Azure Automation, kde některé konfigurace pro uzel pochází z Azure Automation DSC a s částečnou konfigurací, které spravujete místně.

Metaconfiguration níže nastaví uzel za spravované obě služby místně i ve službě Azure Automation.

```powershell
[DscLocalConfigurationManager()]
Configuration RegistrationMetaConfig
{
    Settings
    {
        RefreshFrequencyMins = 30
        RefreshMode = "PULL"
    }

    ConfigurationRepositoryWeb web
    {
        ServerURL =  $endPoint
        RegistrationKey = $registrationKey
        ConfigurationNames = $configurationName
    }

    # Partial configuration managed by Azure Automation service.
    PartialConfiguration PartialConfigurationManagedByAzureAutomation
    {
        ConfigurationSource = "[ConfigurationRepositoryWeb]Web"
    }

    # This partial configuration is managed locally.
    PartialConfiguration OnPremisesConfig
    {
        RefreshMode = "PUSH"
        ExclusiveResources = @("Script")
    }

}

RegistrationMetaConfig
Set-DscLocalConfigurationManager -Path .\RegistrationMetaConfig -Verbose
```

## <a name="using-psdscrunascredential-with-dsc-composite-resources"></a>Pomocí PsDscRunAsCredential složené prostředky DSC

Přidali jsme podporu pro používání [ *PsDscRunAsCredential* ](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) s DSC [složené](https://msdn.microsoft.com/powershell/dsc/authoringresourcecomposite) prostředky.

Nyní můžete zadat hodnotu pro PsDscRunAsCredential při použití složené prostředky uvnitř konfigurace.
-Li zadána, spustit všechny prostředky uvnitř složených prostředků jako uživatele RunAs.
Volá-li složený prostředek jiný složený prostředek, všechny její prostředky jsou spouštěny, jako uživatele RunAs.
Pověření spustit jako se rozšíří na libovolné úrovni hierarchie složených prostředků.
Pokud prostředek uvnitř složených prostředků určuje jeho vlastní hodnotě. pro PsDscRunAsCredential, Chyba sloučení výsledků během kompilace konfigurace.

Tento příklad ukazuje použití s [WindowsFeatureSet](https://msdn.microsoft.com/powershell/wmf/dsc_newresources) složených prostředků zahrnuté v modulu PSDesiredStateConfiguration.

```powershell
Configuration InstallWindowsFeature
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        WindowsFeatureSet features
        {
            Name = @("Telnet-Client","SNMP-Service")
            Ensure = "Present"
            IncludeAllSubFeature = $true
            PsDscRunAsCredential = Get-Credential
        }
    }
}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost'
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}

InstallWindowsFeature -ConfigurationData $configData
```

## <a name="dsc-module-and-configuration-signing-validations"></a>Modul DSC a konfiguraci podepisování ověření

V DSC, konfigurace a moduly jsou rozděleny do spravovaných počítačů ze serveru vyžádané replikace.
Pokud dojde k narušení serveru vyžádané replikace útočník potenciálně upravit konfigurace a moduly na tomto serveru a byl distribuován do všech spravovaných uzlů, tím bylo narušeno všechny z nich.

Ve WMF 5.1 podporuje ověřují digitální podpisy v katalogu a konfigurace DSC (. Soubory MOF).
Tato funkce zabraňuje uzly provádění konfigurace nebo modul soubory nejsou podepsány důvěryhodným podepisující osoba nebo který bylo pravděpodobně úmyslně po byly podepsány důvěryhodným podepisující osoba.

### <a name="how-to-sign-configuration-and-module"></a>Jak zaregistrovat modul a konfigurace

***
* Konfigurační soubory (. Soubory MOF): existující rutiny Powershellu [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) je rozšířeno pro podporu podepisování souborů MOF.
* Moduly: Podepisování modulů se provádí po přihlášení odpovídající modulu katalogu pomocí následujících kroků:
    1. Vytvořte soubor katalogu: soubor katalogu obsahuje kolekci kryptografické hodnoty hash nebo kryptografické otisky.
       Každý kryptografický otisk odpovídá souboru, který je součástí modulu.
       Nová rutina [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), byl přidán do povolí uživatelům vytvářet soubor katalogu pro jejich modulu.
    2. Podepsat soubor katalogu: použití [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) k podepsání souboru katalogu.
    3. Umístěte soubor katalogu ve složce modulu.
Podle konvence modulu katalogu má být umístěn ve složce modulu se stejným názvem jako modul.

### <a name="localconfigurationmanager-settings-to-enable-signing-validations"></a>LocalConfigurationManager nastavení pro povolení ověření podpisu

#### <a name="pull"></a>O přijetí změn

LocalConfigurationManager uzel provádí podpisový ověření modulů a konfigurací na základě aktuální nastavení.
Ověření podpisu je ve výchozím nastavení zakázána.
Ověření podpisu je povolit tak, že přidáte blok "SignatureValidation" definici meta konfigurace typu uzlu jak je znázorněno níže:

```powershell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PULL'
    }

    ConfigurationRepositoryWeb pullserver{
      ConfigurationNames = 'sql'
      ServerURL = 'http://localhost:8080/PSDSCPullServer/PSDSCPullServer.svc'
      AllowUnsecureConnection = $true
      RegistrationKey = 'd6750ff1-d8dd-49f7-8caf-7471ea9793fc' # Replace this with correct registration key.
    }
    SignatureValidation validations{
        # If the TrustedStorePath property is provided then LCM will use the custom path. Otherwise, the LCM will use default trusted store path (Cert:\LocalMachine\DSCStore) to find the signing certificate.
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType = 'Configuration','Module'         # This is a list of DSC artifacts, for which LCM need to verify their digital signature before executing them on the node.
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
```

V uzlu nastavení výše metaconfiguration umožňuje ověřit podpis staženého konfigurace a moduly.
Local Configuration Manageru provede následující kroky k ověření digitálních podpisů.

1. Ověření podpisu pro soubor konfigurace (. Platnost MOF).
   Použije rutinu prostředí PowerShell [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), což je rozšířená 5.1 pro podporu ověřování podpisu MOF.
2. Ověřte, že certifikační autorita, která oprávnění podpisu je důvěryhodný.
3. Stáhněte si závislosti modulu nebo prostředek konfigurace do dočasného umístění.
4. Ověření podpisu katalogu, zahrnuty uvnitř modulu.
    * Najít `<moduleName>.cat` souboru a ověření jeho podpisu pomocí rutiny [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).
    * Ověřte, že certifikační autorita, která ověření podpisu je důvěryhodný.
    * Ověřte obsah moduly nikdo neoprávněně nemanipuloval pomocí nové rutiny [testovací FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).
5. Install-Module k $env: ProgramFiles\WindowsPowerShell\Modules\
6. Konfigurace procesu

> Poznámka: Ověření podpisu v modulu katalogu a konfigurace se provádí pouze při použití konfigurace k systému poprvé nebo když je stažen a nainstalován modul.
Spuštění konzistence nelze ověřit podpis Current.mof nebo jeho závislosti modulu.
Pokud ověření se nezdařilo v jakékoli fázi, například pokud konfigurace získaných z serveru vyžádané replikace je bez znaménka, pak zpracování konfigurace skončí s chybou je uvedeno níže a se odstraní všechny dočasné soubory.

![Konfigurace výstupu Chyba vzorku](../images/PullUnsignedConfigFail.png)

Obdobně souhrnné informace modulu, jehož katalog není podepsaný za následek následující chybě:

![Ukázka chyby výstupu modulu](../images/PullUnisgnedCatalog.png)

#### <a name="push"></a>nabízených oznámení

Předtím, než se doručí do uzlu, může být úmyslně konfigurace doručit pomocí nabízené instalace v jejich zdroji.
Místní Configuration Manager provádí podobným způsobem ověření podpisu pro vložené nebo publikované konfigurace.
Níže je úplný Příklad ověření podpisu pro nabízené oznámení.

- Povolení ověření podpisu na uzlu.

```powershell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PUSH'
    }
    SignatureValidation validations{
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType =  'Configuration','Module'
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
```

- Vytvořte ukázkový konfigurační soubor.

```powershell
# Sample configuration
Configuration Test
{

    File foo
    {
        DestinationPath =  "$env:TEMP\signingTest.txt"
        Contents = "ABC"
    }
}
Test
```

- Zkuste doručením (push) bez znaménka konfiguračního souboru uzlu.

```powershell
Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
```

![ErrorUnsignedMofPushed](../images/PushUnsignedMof.png)

- Podepište konfigurační soubor pomocí certifikátu pro podepisování kódu.

![SignMofFile](../images/SignMofFile.png)

- Zkuste nahráním podepsaného souboru MOF.

![SignMofFile](../images/PushSignedMof.png)
