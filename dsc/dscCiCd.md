---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Vytváření kanál průběžnou integraci a průběžné nasazování pomocí DSC"
ms.openlocfilehash: 5f7583fb93b69bbe4103b34b79b3a859c9cee8a9
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="building-a-continuous-integration-and-continuous-deployment-pipeline-with-dsc"></a>Vytváření kanál průběžnou integraci a průběžné nasazování pomocí DSC

Tento příklad ukazuje, jak vytvořit kanál průběžné nasazování integrace/souvislý (CI/CD) pomocí prostředí PowerShell, DSC, Pester a Visual Studio Team Foundation Server (TFS).

Po vytvoření kanálu a nakonfigurovaný, můžete použít pro plně nasazení, konfiguraci a testování serveru DNS a přidružené záznamy hostitele. Tento proces simuluje první část kanál, který se použije ve vývojovém prostředí.

Kanál automatizované CI/CD umožňuje rychlejší aktualizace softwaru a spolehlivěji, zajistíte, že veškerý kód je testován a že je aktuální sestavení kódu vždy k dispozici.

## <a name="prerequisites"></a>Předpoklady

Pokud chcete použít v tomto příkladu, byste měli seznámit s následujícími službami:

- Koncepty CI CD. Odkaz na dobrý najdete na [modelu kanálu verze](http://aka.ms/thereleasepipelinemodelpdf).
- [Git](https://git-scm.com/) zdroj ovládacího prvku
- [Pester](https://github.com/pester/Pester) testování framework
- [Team Foundation Server](https://www.visualstudio.com/tfs/)

## <a name="what-you-will-need"></a>Co budete potřebovat

Pro sestavení a spuštění tohoto příkladu, budete potřebovat v prostředí s několika počítačích nebo virtuálních počítačů.

### <a name="client"></a>Client

Toto je počítač, kde, můžete to udělat všechny pracovní nastavení a spuštění v příkladu.

Klientský počítač musí být počítač se systémem Windows s nainstalované tyto položky:
- [Git](https://git-scm.com/)
- úložiště místní git naklonována ze https://github.com/PowerShell/Demo_CI
- textový editor, například [Visual Studio Code](https://code.visualstudio.com/)

### <a name="tfssrv1"></a>TFSSrv1

Počítač, který je hostitelem serveru TFS, kde můžete definovat vaše sestavení a verze.
Tento počítač musí mít [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) nainstalována.

### <a name="buildagent"></a>BuildAgent

Počítač, který spouští Windows sestavení agenta, který sestaví projekt.
Tento počítač musí mít Windows sestavení agent nainstalován a spuštěn.
V tématu [nasadit agenta v systému Windows](https://www.visualstudio.com/en-us/docs/build/actions/agents/v2-windows) pro pokyny, jak nainstalovat a spustit Windows sestavení agenta.

Musíte taky nainstalovat obě `xDnsServer` a `xNetworking` moduly DSC v tomto počítači.

### <a name="testagent1"></a>TestAgent1

Toto je počítač, který je nakonfigurovaný jako DNS server v tomto příkladu konfigurace DSC.
V počítači musí být spuštěn [systému Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).

### <a name="testagent2"></a>TestAgent2

Toto je počítač, který je hostitelem webu, který tento příklad konfiguruje.
V počítači musí být spuštěn [systému Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016). 

## <a name="add-the-code-to-tfs"></a>Přidejte kód do sady TFS

Začneme vytvoření úložiště Git v sadě TFS a importováním kód z místního úložiště v klientském počítači.
Pokud se úložiště Demo_CI nebyly již klonovat na klientském počítači, postupujte tak teď spuštěním následujícího příkazu git:

`git clone https://github.com/PowerShell/Demo_CI`

1. Na klientském počítači přejděte na server TFS ve webovém prohlížeči.
1. V sadě TFS [vytvoření nového týmového projektu](https://www.visualstudio.com/en-us/docs/setup-admin/create-team-project) s názvem Demo_CI.

    Ujistěte se, že **verzí** je nastaven na **Git**.
1. Na klientském počítači přidejte vzdálené úložiště, které jste právě vytvořili v sadě TFS pomocí následujícího příkazu:

    `git remote add tfs <YourTFSRepoURL>`

    Kde `<YourTFSRepoURL>` je adresa URL klonování k úložišti sady TFS, který jste vytvořili v předchozím kroku.

    Pokud si nejste jisti, kde se tato adresa URL, najdete v části [klonovat existující úložiště Git](https://www.visualstudio.com/en-us/docs/git/tutorial/clone).
1. Push kód z místního úložiště do úložiště TFS pomocí následujícího příkazu:

    `git push tfs --all`
1. Úložiště TFS vyplní kódem Demo_CI.

>**Poznámka:** kód v tomto příkladu používá `ci-cd-example` větve úložiště Git.
>Nezapomeňte zadat tuto větev jako výchozí větev ve vašem projektu sady TFS a aktivačních událostí CI/CD vytvoříte.

## <a name="understanding-the-code"></a>Pochopení kódu

Předtím, než vytvoříme kanály sestavení a nasazení, podíváme se na kód, abyste pochopili, co se děje.
Na klientském počítači otevřete svém oblíbeném textovém editoru a přejděte do kořenového úložiště Demo_CI Git.

### <a name="the-dsc-configuration"></a>Konfigurace DSC

Otevřete soubor `DNSServer.ps1` (z kořene místní úložiště Demo_CI `./InfraDNS/Configs/DNSServer.ps1`).

Tento soubor obsahuje konfigurace DSC, který slouží k nastavení serveru DNS. Tady je v celé jeho šíři:

```powershell
configuration DNSServer
{
    Import-DscResource -module 'xDnsServer','xNetworking', 'PSDesiredStateConfiguration'

    Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
    {
        WindowsFeature DNS
        {
            Ensure  = 'Present'
            Name    = 'DNS'
        }

        xDnsServerPrimaryZone $Node.zone
        {
            Ensure    = 'Present'
            Name      = $Node.Zone
            DependsOn = '[WindowsFeature]DNS'
        }

        foreach ($ARec in $Node.ARecords.keys) {
            xDnsRecord $ARec
            {
                Ensure    = 'Present'
                Name      = $ARec
                Zone      = $Node.Zone
                Type      = 'ARecord'
                Target    = $Node.ARecords[$ARec]
                DependsOn = '[WindowsFeature]DNS'
            }
        }

        foreach ($CName in $Node.CNameRecords.keys) {
            xDnsRecord $CName
            {
                Ensure    = 'Present'
                Name      = $CName
                Zone      = $Node.Zone
                Type      = 'CName'
                Target    = $Node.CNameRecords[$CName]
                DependsOn = '[WindowsFeature]DNS'
            }
        }
    }
}
```

Upozornění `Node` příkaz:

```powershell
Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
```

To vyhledá všechny uzly, které byly definovány tak, že má role `DNSServer` v [konfigurační data](configData.md), který je vytvořen `DevEnv.ps1` skriptu.

Definování uzly pomocí konfiguračních dat je důležité, pokud to položek konfigurace, protože uzel informace změní pravděpodobně mezi prostředími, a pomocí konfigurační data můžete snadno provádět změny uzlu informace beze změny kódu konfigurace.

V prvním bloku prostředků, konfigurace volá [WindowsFeature](windowsFeatureResource.md) zajistit, že je povolena funkce DNS. Bloky prostředků, které podle volání prostředky z [xDnsServer](https://github.com/PowerShell/xDnsServer) modulu Konfigurace primární zóna a záznamy DNS.

Všimněte si, že dva `xDnsRecord` bloky jsou uzavřen do `foreach` cykly, které iteraci v rámci pole v konfigurační data.
Znovu vytvoří konfigurační data `DevEnv.ps1` skript, který podíváme Další.

### <a name="configuration-data"></a>Konfigurační data

`DevEnv.ps1` Souboru (z kořene místní úložiště Demo_CI `./InfraDNS/DevEnv.ps1`) určuje konkrétní prostředí konfigurační data v zatřiďovací tabulky a pak předá tento zatřiďovací tabulky na volání `New-DscConfigurationDataDocument` funkce, která je definována v `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).

`DevEnv.ps1` Souboru:

```powershell
param(
    [parameter(Mandatory=$true)]
    [string]
    $OutputPath
)

Import-Module $PSScriptRoot\..\Assets\DscPipelineTools\DscPipelineTools.psd1 -Force

# Define Unit Test Environment
$DevEnvironment = @{
    Name                        = 'DevEnv';
    Roles = @(
        @{  Role                = 'DNSServer';
            VMName              = 'TestAgent1';
            Zone                = 'Contoso.com';
            ARecords            = @{'TFSSrv1'= '10.0.0.10';'Client'='10.0.0.15';'BuildAgent'='10.0.0.30';'TestAgent1'='10.0.0.40';'TestAgent2'='10.0.0.50'};
            CNameRecords        = @{'DNS' = 'TestAgent1.contoso.com'};
        }
    )
}

Return New-DscConfigurationDataDocument -RawEnvData $DevEnvironment -OutputPath $OutputPath
```

`New-DscConfigurationDataDocument` – Funkce (definované v `\Assets\DscPipelineTools\DscPipelineTools.psm1`) prostřednictvím kódu programu vytvoří dokument data konfigurace z zatřiďovací tabulky (data uzlu) a pole (bez uzlu data), které se předávají jako `RawEnvData` a `OtherEnvData` parametry.

V našem případě pouze `RawEnvData` parametr se používá.

### <a name="the-psake-build-script"></a>Skript psake sestavení

[Psake](https://github.com/psake/psake) skriptu definovaný v sestavení `Build.ps1` (z kořenového úložiště Demo_CI `./InfraDNS/Build.ps1`) definuje úlohy, které jsou součástí sestavení.
Také definuje, jaké úkoly, které každý úkol závisí na. Po vyvolání skriptu psake zajistí, že zadané úloze (nebo úloha s názvem `Default` Pokud není zadaný žádný) běží a že všechny závislosti také spustit (to je rekurzivní, takže závislosti závislosti spustit, a tak dále).

V tomto příkladu `Default` úloh je definován jako:

```powershell
Task Default -depends UnitTests
```

`Default` Úloha nemá žádnou implementaci sám sebe, ale má závislost na `CompileConfigs` úloh.
Výsledný řetězec závislostí zajistí, že jsou všechny úlohy ve skriptu buildu použít.

V tomto příkladu je skript psake vyvolat volání `Invoke-PSake` v `Initiate.ps1` soubor (umístěný v kořenovém úložišti Demo_CI):

```powershell
param(
    [parameter()]
    [ValidateSet('Build','Deploy')]
    [string]
    $fileName
)

#$Error.Clear()

Invoke-PSake $PSScriptRoot\InfraDNS\$fileName.ps1

<#if($Error.count)
{
    Throw "$fileName script failed. Check logs for failure details."
}
#>
```

Při vytváření definice sestavení pro náš příklad v sadě TFS, jsme se zadat soubor skriptu naše psake jako `fileName` parametr pro tento skript.

Skript sestavení definuje následující úlohy:

#### <a name="generateenvironmentfiles"></a>GenerateEnvironmentFiles

Spustí `DevEnv.ps1`, který generuje datový soubor konfigurace.

#### <a name="installmodules"></a>InstallModules

Nainstaluje moduly potřebnými konfigurace `DNSServer.ps1`.

#### <a name="scriptanalysis"></a>ScriptAnalysis

Volání [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).

#### <a name="unittests"></a>UnitTests

Spustí [Pester](https://github.com/pester/Pester/wiki) testování částí.

#### <a name="compileconfigs"></a>CompileConfigs

Zkompiluje konfigurace (`DNSServer.ps1`) do souboru MOF, pomocí konfiguračních dat vygenerovaných `GenerateEnvironmentFiles` úloh.

#### <a name="clean"></a>Clean

Vytvoří složek používaných pro tento příklad a odebere z předchozích spuštění žádné výsledky testů, souborů konfiguračních dat a modulů.

### <a name="the-psake-deploy-script"></a>Skript nasadit psake

[Psake](https://github.com/psake/psake) skript nasazení, které jsou definované v `Deploy.ps1` (z kořenového úložiště Demo_CI `./InfraDNS/Deploy.ps1`) definuje úlohy, které nasazení a spuštění konfigurace.

`Deploy.ps1`definuje následující úlohy:

#### <a name="deploymodules"></a>DeployModules

Spustí relaci prostředí PowerShell na `TestAgent1` a nainstaluje moduly obsahující prostředky DSC potřebné pro konfiguraci.

#### <a name="deployconfigs"></a>DeployConfigs

Volání [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration.md) můžete spustit konfiguraci `TestAgent1`.

#### <a name="integrationtests"></a>IntegrationTests

Spustí [Pester](https://github.com/pester/Pester/wiki) integrace testy.

#### <a name="acceptancetests"></a>AcceptanceTests

Spustí [Pester](https://github.com/pester/Pester/wiki) přijetí testy.

#### <a name="clean"></a>Clean

Odebere všechny moduly nainstalované v předchozích spuštění a zajišťuje, že složka výsledků testu existuje.

### <a name="test-scripts"></a>Testování skriptů

Přijetí, integrace a jednotky testů jsou definovány v skripty v `Tests` složky (z kořenového úložiště Demo_CI `./InfraDNS/Tests`), každou v souborech s názvem `DNSServer.tests.ps1` v jejich příslušné složky.

Použití skriptů test [Pester](https://github.com/pester/Pester/wiki) a [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntaxe.

#### <a name="unit-tests"></a>Testy jednotek

Jednotka testy konfigurací testů DSC, se ujistěte, že konfigurace bude provádět očekávané při spuštění.
Jednotka testování skript používá [Pester](https://github.com/pester/Pester/wiki).

#### <a name="integration-tests"></a>Integrace testů

Testy integrace otestovat konfiguraci systému a zajistit, že při integraci s ostatními součástmi, systém je nastaven podle očekávání. Tyto testy se spouštějí na cílovém uzlu po byl nakonfigurován s DSC.
Integrace zkušební skript používá kombinaci [Pester](https://github.com/pester/Pester/wiki) a [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntaxe.

#### <a name="acceptance-tests"></a>Přijetí testů

Přijetí testy testovací systém tak, aby se chová podle očekávání.
Například testy k zajištění, že vrací náležité informace, které při dotazu na webové stránce.
Tyto testy spustit z cílový uzel pro otestování skutečných scénářích vzdáleně.
Integrace zkušební skript používá kombinaci [Pester](https://github.com/pester/Pester/wiki) a [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntaxe.

## <a name="define-the-build"></a>Zadejte sestavení

Teď, když jsme nahrán kódu do sady TFS a podívat, jak funguje, nastavíme naše sestavení.

Zde jsme zaměříme pouze kroky sestavení, které přidáte do sestavení. Pokyny k vytvoření definice sestavení v sadě TFS najdete v tématu [vytvořit a fronty pro definici buildu](https://www.visualstudio.com/en-us/docs/build/define/create).

Vytvořte novou definici sestavení (vyberte **prázdný** šablony) s názvem "InfraDNS".
Přidáte že následující kroky vám sestavení definice:

- Skript prostředí PowerShell
- Publikování výsledků testů
- Kopírování souborů
- Publikování artefaktů

Po přidání tyto kroky sestavení, upravit vlastnosti každého kroku následujícím způsobem:

### <a name="powershell-script"></a>Skript prostředí PowerShell

1. Nastavte **typ** vlastnost `File Path`.
1. Nastavte **cestu ke skriptu** vlastnost `initiate.ps1`.
1. Přidat `-fileName build` k **argumenty** vlastnost.

Tento krok sestavení běží `initiate.ps1` souboru, který volá psake skriptu buildu.

### <a name="publish-test-results"></a>Publikování výsledků testů

1. Nastavit **testování výsledný formát** na`NUnit`
1. Nastavit **výsledky testu soubory** do`InfraDNS/Tests/Results/*.xml`
1. Nastavit **testování název běhu** k `Unit`.
1. Zajistěte, aby **možnosti řízení** **povoleno** a **vždy spustit** jsou obě vybrané.

Tento krok sestavení spustí testy jednotek ve skriptu Pester jsme se podívali na dříve a ukládá výsledky do `InfraDNS/Tests/Results/*.xml` složky.

### <a name="copy-files"></a>Kopírování souborů

1. Přidejte všechny následující řádky, které se **obsah**:

    ```
    initiate.ps1
    **\deploy.ps1
    **\Acceptance\**
    **\Integration\**
    ```

1. Nastavit **TargetFolder** na`$(Build.ArtifactStagingDirectory)\`

Tento krok zkopíruje sestavení a testů skriptů do pracovního adresáře, který lze publikovat, protože sestavení artefaktů dalším krokem.

### <a name="publish-artifact"></a>Publikování artefaktů

1. Nastavit **cestu k publikování** na`$(Build.ArtifactStagingDirectory)\`
1. Nastavit **artefaktů název** na`Deploy`
1. Nastavit **typu artefaktu** na`Server`
1. Vyberte `Enabled` v **řízení možností**

## <a name="enable-continuous-integration"></a>Povolit průběžnou integraci

Nyní nastavíme aktivační událost, která způsobí, že projekt sestavení kdykoli změnu se změnami do `ci-cd-example` větve úložiště git.

1. V sadě TFS, klikněte **sestavení a verze** karta
1. Vyberte `DNS Infra` definice sestavení a klikněte na tlačítko **upravit**
1. Klikněte **aktivační události** karta
1. Vyberte **průběžnou integraci (CI)**a vyberte `refs/heads/ci-cd-example` v rozevíracím seznamu firemní pobočky
1. Klikněte na tlačítko **Uložit** a potom **OK**

Nyní každé změně aktivačních událostí úložišti git sady TFS automatizované sestavení.

## <a name="create-the-release-definition"></a>Vytvořit definici verze

Umožňuje vytvořit definici verze tak, aby nasazení projektu do vývojového prostředí s každou změnami kódu.

K tomuto účelu přidání nové verze definice přidružené `InfraDNS` sestavení definice, které jste předtím vytvořili.
Je nutné vybrat **průběžné nasazování** tak, aby nové verze aktivuje vždy, když je dokončena nové sestavení.
([Postupy: práce s verzí definice](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)) a nakonfigurovat následujícím způsobem:

Přidáte následující kroky k definici verze:

- Skript prostředí PowerShell
- Publikování výsledků testů
- Publikování výsledků testů

Postup úpravy následujícím způsobem:

### <a name="powershell-script"></a>Skript prostředí PowerShell

1. Nastavte **cestu ke skriptu** do`$(Build.DefinitionName)\Deploy\initiate.ps1"`
1. Nastavte **argumenty** do`-fileName Deploy`

### <a name="first-publish-test-results"></a>Nejprve publikování výsledků testů

1. Vyberte `NUnit` pro **testovací výsledný formát** pole
1. Nastavte **testovací soubory výsledek** do`$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`
1. Nastavte **testování název běhu** na`Integration`
1. V části **možnosti řízení**, zkontrolujte **vždy spustit.**

### <a name="second-publish-test-results"></a>Druhý publikování výsledků testů

1. Vyberte `NUnit` pro **testovací výsledný formát** pole
1. Nastavte **testovací soubory výsledek** do`$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`
1. Nastavte **testování název běhu** na`Acceptance`
1. V části **možnosti řízení**, zkontrolujte **vždy spustit.**

## <a name="verify-your-results"></a>Zkontrolujte výsledky

Nyní, kdykoli nabízené změny `ci-cd-example` spustí větev do sady TFS, nové sestavení.
Sestavení se dokončí úspěšně, aktivuje se nové nasazení.

Výsledek nasazení můžete zkontrolovat otevřením prohlížeče v klientském počítači a přejdete na `www.contoso.com`.

## <a name="next-steps"></a>Další kroky

Tento příklad konfiguruje DNS server `TestAgent1` tak, aby adresa URL `www.contoso.com` přeloží na `TestAgent2`, ale ve skutečnosti Nenasazuje webu.
Kostru jak to udělat najdete v úložišti v části `WebApp` složky.
Zástupných procedur zadaná k vytvoření psake skripty, Pester testy a konfigurace DSC můžete použít k nasazení vlastního webu.







