---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Vylepšení DSC v WMF 5.1
ms.openlocfilehash: 32bdde6d43d17cc76c454fe10b00097753a9eebe
ms.sourcegitcommit: 2d9cf1ccb9a653db7726a408ebcb65530dcb1522
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/19/2018
ms.locfileid: "34309538"
---
# <a name="improvements-in-desired-state-configuration-dsc-in-wmf-51"></a>Vylepšení v požadované konfigurace stavu (DSC) v WMF 5.1

## <a name="dsc-class-resource-improvements"></a>Vylepšení prostředků DSC – třída

V WMF 5.1 vyřešili jsme následující známé problémy:

- Get-DscConfiguration může vrátit prázdné hodnoty (null) nebo chyby, pokud typ tabulky komplexní a hodnoty hash je vrácené funkcí Get() DSC prostředku založené na třídě.
- Get-DscConfiguration vrátí chybu, pokud se používá přihlašovací údaje RunAs konfigurace DSC.
- Na základě třídy prostředků nelze použít v konfiguraci složené.
- Spuštění DscConfiguration se zasekne, pokud na základě třídy prostředků má vlastnost vlastní typu.
- Na základě třídy prostředků nelze použít jako výhradní prostředek.

## <a name="dsc-resource-debugging-improvements"></a>Vylepšení ladění prostředek DSC

V WMF 5.0 ladicí program prostředí PowerShell se nezastavil v metodě založené na třídě prostředků (Get/Set nebo Test) přímo.
Ladicí program se zastaví v WMF 5.1 na metodu na základě třídy prostředků stejným způsobem jako u prostředků založených na MOF metody.

## <a name="dsc-pull-client-supports-tls-11-and-tls-12"></a>DSC vyžádání klient podporuje protokol TLS 1.1 a TLS 1.2

Dříve klient pro vyžádání obsahu DSC podporována pouze SSL3.0 a TLS1.0 přes připojení prostřednictvím protokolu HTTPS.
Při vynucené bezpečnější protokoly, by klient pro vyžádání obsahu přestane fungovat.
V 5.1 WMF klient vyžádání DSC už podporuje protokol SSL 3.0 a přidává podporu pro bezpečnější protokoly TLS 1.1 a TLS 1.2.

## <a name="improved-pull-server-registration"></a>Registrace serveru vylepšené vyžádání obsahu

V dřívějších verzích WMF souběžných registrace/reporting požadavky na server DSC za při použití databáze ESENT povede k LCM selhání k registraci nebo sestavy.
V takových případech protokolů událostí na serveru vyžádané replikace se chyba "Název Instance již používán."
Důvodem byla nezadají používá pro přístup k databázi ESENT ve scénáři s více procesy.
V 5.1 WMF tento problém byl opraven.
Souběžné registrace nebo generování sestav (zahrnující ESENT databáze), funguje bez potíží WMF 5.1.
Tento problém se vztahuje pouze na databázi ESENT a doporučení se netýká do databáze OLEDB.

## <a name="enable-circular-log-on-esent-database-instance"></a>Povolit cyklického protokolu ESENT instanci databáze

V eariler verzi DSC PullServer byly soubory protokolů databáze ESENT naplňování místa na disku becouse pullserver, které při vytváření instance databáze bez cyklické protokolování. V této verzi máte možnost řídit chování cyklické protokolování instanci pomocí souboru web.config pullserver. Ve výchozím nastavení CircularLogging nastavena na hodnotu TRUE.

```
<appSettings>
    <add key="dbprovider" value="ESENT" />
    <add key="dbconnectionstr" value="C:\Program Files\WindowsPowerShell\DscService\Devices.edb" />
    <add key="CheckpointDepthMaxKB" value="512" />
    <add key="UseCircularESENTLogs" value="TRUE" />
  </appSettings>
```

## <a name="pull-partial-configuration-naming-convention"></a>Zásady vytváření názvů částečné konfigurace pro vyžádání obsahu

V předchozí verzi, zásady vytváření názvů pro částečné konfigurace byla, název souboru MOF v služba nebo server vyžádané replikace musí shodovat s názvem částečné konfigurace zadaný v nastavení správce místní konfigurace, která zase musí odpovídat Název konfigurace vložených v souboru MOF.

Najdete níže snímky:

- Místní konfigurační nastavení, která definuje konfiguraci částečné uzlu je povoleno přijímat.

![Ukázka metakonfiguraci](../images/MetaConfigPartialOne.png)

- Ukázka definice částečné konfigurace

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

- 'ConfigurationName' vložený vygenerovaný soubor MOF.

![Ukázkový soubor generovaný mof](../images/PartialGeneratedMof.png)

- Název souboru v úložišti konfigurace vyžádání obsahu

![Název souboru v úložišti konfigurace](../images/PartialInConfigRepository.png)

Název služby Azure Automation generované soubory MOF jako `<ConfigurationName>.<NodeName>.mof`.
Konfigurace níže tak zkompiluje do PartialOne.localhost.mof.

Z tohoto důvodu bylo možné na vyžádání, jednu konfiguraci částečné ze služby Azure Automation.

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

V WMF 5.1, může mít jako název částečné konfigurace v rámci serveru nebo služby z vlastního `<ConfigurationName>.<NodeName>.mof`.
Navíc pokud je počítač se stahování konfigurací jedné z vyžádání služba nebo server pak konfigurační soubor na vyžádání obsahu server konfigurace úložiště může mít libovolný název souboru.
Tato pojmenování flexibilitu vám umožní spravovat uzly částečně službou Azure Automation, kde některé konfigurace pro váš uzel pochází z Azure Automation DSC a částečné konfigurace, které můžete spravovat místně.

Metakonfiguraci níže nastaví uzlu jako spravované obě služby místně a také pomocí Azure Automation.

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

Jsme doplnili podporu pro používání [ *PsDscRunAsCredential* ](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) s DSC [složené](https://msdn.microsoft.com/en-us/powershell/dsc/authoringresourcecomposite) prostředky.

Teď můžete zadat hodnotu pro PsDscRunAsCredential při použití složené prostředků v konfiguraci.
-Li zadána, všechny prostředky spustit uvnitř složené prostředků jako uživatel RunAs.
Volá-li prostředek složené jiný prostředek složený, všechny její prostředky jsou provést, protože uživatele RunAs.
Pověření spustit jako rozšířeny všechny úrovně hierarchie složené prostředků.
Pokud žádný prostředek uvnitř složené prostředků určuje vlastní hodnotu pro PsDscRunAsCredential, výsledky sloučení chyby při kompilaci konfigurace.

Tento příklad ukazuje použití se [WindowsFeatureSet](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_newresources) složené prostředků, které jsou součástí modulu PSDesiredStateConfiguration.

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

## <a name="dsc-module-and-configuration-signing-validations"></a>Modul DSC a podepisování ověření konfigurace

V DSC konfigurace a moduly jsou distribuovány do spravovaných počítačů z načítacího serveru.
Pokud ohrožení zabezpečení serveru vyžádané replikace útočník může potenciálně upravit konfigurace a modulů na tomto serveru a jeho distribuován do všech spravovaných uzlech, ohrožení všechny z nich.

V WMF 5.1, podporuje ověření digitálních podpisů v katalogu a konfigurace DSC (. Soubory MOF).
Tato funkce nebude uzly spuštěn konfigurace nebo modul soubory nejsou podepsány důvěryhodným podepisující osoba nebo které mají bylo manipulováno po byly podepsány důvěryhodným podepisující osoba.

### <a name="how-to-sign-configuration-and-module"></a>Postup konfigurace přihlášení a modulu

***
* Konfigurační soubory (. Soubory MOF): existující rutiny prostředí PowerShell [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) je rozšířeno pro podporu podepisování souborů MOF.
* Moduly: Podepisování modulů se provádí podepisování katalogu modul odpovídající pomocí následujících kroků:
    1. Vytvořte soubor katalogu: soubor katalogu obsahuje kolekci kryptografické hodnoty hash nebo kryptografické otisky.
       Každý kryptografický otisk odpovídá souboru, který je součástí modulu.
       K dispozici novou rutinu [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), byl přidán do povolit uživatelům vytvářet soubor katalogu pro jejich modul.
    2. Podepsání souboru katalogu: použití [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) k podepsání souboru katalogu.
    3. Umístěte soubor katalogu naleznete ve složce modulu.
Podle konvence třeba modul katalogu soubor uložit ve složce modulu se stejným názvem jako modul.

### <a name="localconfigurationmanager-settings-to-enable-signing-validations"></a>LocalConfigurationManager nastavení pro povolení podpisový ověření

#### <a name="pull"></a>Pro vyžádání obsahu

LocalConfigurationManager uzlu provede podpisový ověření modulů a na základě aktuální nastavení konfigurace.
Ověření podpisu je ve výchozím nastavení zakázané.
Ověření podpisu můžete povolit přidáním 'SignatureValidation' blok k definici meta konfigurace uzlu jako uvedené níže:

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

Nastavení výše metakonfiguraci na uzlu umožňuje ověření podpisu stažené konfigurace a moduly.
Správce místní konfigurace provede následující kroky k ověření digitálních podpisů.

1. Ověření podpisu na konfigurační soubor (. MOF) je platná.
   Používá rutinu prostředí PowerShell [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), což je rozšířená v 5.1 pro podporu ověřování podpisu MOF.
2. Ověřte, že certifikační autority, která oprávnění podepisující je důvěryhodný.
3. Stáhněte si modul nebo prostředků závislosti konfigurace do dočasného umístění.
4. Ověření podpisu katalogu zahrnuty do vnitřní modul.
    * Najít `<moduleName>.cat` souboru a ověřte jeho podpis pomocí rutiny [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).
    * Ověřte, že certifikační autorita, která ověření podpisu je důvěryhodný.
    * Ověřte obsah moduly nikdo neoprávněně pomocí nové rutiny [Test FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).
5. Instalace modulu pro $env: ProgramFiles\WindowsPowerShell\Modules\
6. Konfigurace procesů

> Poznámka: Ověřování podpisu v modulu katalogu a konfigurace se provádí pouze při použití konfigurace systému poprvé, nebo pokud je modul stáhli a nainstalovali.
Spustí konzistence neověřují podpis Current.mof nebo jeho závislé součásti modulu.
Pokud ověření došlo k chybě v jakékoli fázi, například pokud konfigurace načtený z je vyžádání obsahu server bez znaménka, pak ukončí zpracování konfigurace s následující chybou a jsou odstraněny všechny dočasné soubory.

![Ukázková konfigurace výstupní chyby](../images/PullUnsignedConfigFail.png)

Podobně stahování modulu, jehož katalogu není podepsané má za následek následující chybě:

![Ukázka modul výstupní chyby](../images/PullUnisgnedCatalog.png)

#### <a name="push"></a>Push

Konfigurace doručit pomocí nabízené instalace může být úmyslně poškozena úrovni jeho zdroje před jeho doručit do uzlu.
Správce místní konfigurace se provádí podobným způsobem ověření podpisu pro stisknutí nebo publikované konfigurace.
Níže je kompletní příklad, jak ověřit podpis nabízená instalace.

- Povolte ověřování podpisu na uzlu.

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

- Vytvořte vzorový konfigurační soubor.

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

- Zkuste, když zavedete nepodepsané konfiguračního souboru uzlu.

```powershell
Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
```

![ErrorUnsignedMofPushed](../images/PushUnsignedMof.png)

- Zaregistrujte konfiguračního souboru pomocí certifikátu pro podepisování kódu.

![SignMofFile](../images/SignMofFile.png)

- Zkuste vkládání podepsaného souboru MOF.

![SignMofFile](../images/PushSignedMof.png)
