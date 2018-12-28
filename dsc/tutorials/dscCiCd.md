---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Vytváření procesních toků pro průběžnou integraci a průběžné nasazování s DSC
ms.openlocfilehash: c305d9bc7e0f8c659129b5a20d0b7e8b34d09ba8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403824"
---
# <a name="building-a-continuous-integration-and-continuous-deployment-pipeline-with-dsc"></a>Vytváření procesních toků pro průběžnou integraci a průběžné nasazování s DSC

Tento příklad ukazuje, jak vytvořit kanál průběžné integrace a průběžného nasazování (CI/CD) s použitím prostředí PowerShell, DSC, Pester a Visual Studio Team Foundation Server (TFS).

Po vytvoření kanálu a nakonfigurované, můžete použít plně nasazení, testování a konfigurace serveru DNS a související záznamy hostitele.
Tento proces simuluje první část kanál, který se použije ve vývojovém prostředí.

Automatizovaný kanál CI/CD vám pomůže aktualizovat software rychleji a spolehlivěji, zajištění, že je testován veškerý kód, a zda je aktuální sestavení kódu vždy k dispozici.

## <a name="prerequisites"></a>Předpoklady

Chcete-li použít tento příklad, měli seznámit s následujícími možnostmi:

- Koncepty CI-CD. Najdete vhodné reference na [The Model kanálu verze](http://aka.ms/thereleasepipelinemodelpdf).
- [Git](https://git-scm.com/) správy zdrojového kódu
- [Pester](https://github.com/pester/Pester) testování
- [Team Foundation Server](https://www.visualstudio.com/tfs/)

## <a name="what-you-will-need"></a>Co budete potřebovat

Sestavit a spustit tento příklad, musíte v prostředí s několika počítačích nebo virtuálních počítačů.

### <a name="client"></a>Client

Toto je počítač, kde budete používat všechnu práci, nastavení a spuštění příkladu.

Klientský počítač musí být počítač Windows s nainstalované tyto položky:

- [Git](https://git-scm.com/)
- naklonovat místního úložiště git z https://github.com/PowerShell/Demo_CI
- textový editor, například [Visual Studio Code](https://code.visualstudio.com/)

### <a name="tfssrv1"></a>TFSSrv1

Počítač, který je hostitelem serveru TFS, kde bude definici sestavení a vydání.
Tento počítač musí mít [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) nainstalované.

### <a name="buildagent"></a>BuildAgent

Počítač, na kterém běží Windows agenta sestavení, sestavení projektu.
Tento počítač musí mít Windows nainstalovaný a spuštěný agent sestavení.
Zobrazit [nasazení agenta ve Windows](/azure/devops/pipelines/agents/v2-windows) pro agenta sestavení pokyny o tom, jak nainstalovat a spustit Windows.

Budete také muset nainstalovat i `xDnsServer` a `xNetworking` moduly DSC na tomto počítači.

### <a name="testagent1"></a>TestAgent1

To je počítač, který je nakonfigurovaný jako DNS server konfigurací DSC v tomto příkladu.
Počítači musí běžet [Windows serveru 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).

### <a name="testagent2"></a>TestAgent2

Toto je počítač, který je hostitelem webu, který tento příklad konfiguruje.
Počítači musí běžet [Windows serveru 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).

## <a name="add-the-code-to-tfs"></a>Přidejte kód do TFS

Začneme vytváření úložiště Git v sadě TFS a import kód ze svého místního úložiště na klientském počítači.
Pokud nebyly již naklonované úložiště Demo_CI na klientském počítači, proveďte to teď spuštěním následujícího příkazu git:

`git clone https://github.com/PowerShell/Demo_CI`

1. Na klientském počítači přejděte na server TFS ve webovém prohlížeči.
1. V sadě TFS [vytvořte nový týmový projekt](/azure/devops/organizations/projects/create-project) s názvem Demo_CI.

   Ujistěte se, že **verzí** je nastavena na **Git**.
1. Na klientském počítači přidejte vzdálené úložiště, které jste právě vytvořili na serveru TFS pomocí následujícího příkazu:

   `git remote add tfs <YourTFSRepoURL>`

   Kde `<YourTFSRepoURL>` je adresa URL klonování k TFS úložiště, kterou jste vytvořili v předchozím kroku.

   Pokud si nejste jisti, kde najít tuto adresu URL, najdete v článku [Naklonovat existující úložiště Git](/azure/devops/repos/git/clone).
1. Vložit kód ze svého místního úložiště do vašeho úložiště TFS pomocí následujícího příkazu:

   `git push tfs --all`
1. Úložiště TFS naplní Demo_CI kódu.

> [!NOTE]
> V tomto příkladu kódu v `ci-cd-example` větve úložiště Git.
> Nezapomeňte zadat tuto větev jako výchozí větev ve vašem projektu TFS a pro aktivační události CI/CD, který vytvoříte.

## <a name="understanding-the-code"></a>Porozumění kódu

Než vytvoříme kanály sestavení a nasazení, Pojďme se podívat na některé z kódu pochopit, co se děje.
Na klientském počítači otevřete oblíbený textový editor a přejděte do kořenového adresáře úložiště Demo_CI Git.

### <a name="the-dsc-configuration"></a>Konfigurace DSC

Otevřete soubor `DNSServer.ps1` (z kořenového adresáře místního úložiště Demo_CI `./InfraDNS/Configs/DNSServer.ps1`).

Tento soubor obsahuje konfiguraci DSC, která slouží k nastavení serveru DNS. Tady je v celém rozsahu:

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

Všimněte si, že `Node` – příkaz:

```powershell
Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
```

To najde všechny uzly, které byly definovány jako s rolí `DNSServer` v [konfigurační data](../configurations/configData.md), který je vytvořen `DevEnv.ps1` skriptu.

Další informace o `Where` metoda [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)

Definování uzly pomocí konfiguračních dat je důležité při provádění položky konfigurace, protože informace o uzlu se pravděpodobně změní mezi prostředími a pomocí konfigurační data můžete snadno změnit informace o uzlu beze změny kódu konfigurace.

V prvním bloku prostředek konfigurace volá **WindowsFeature** zajistit, že je povolena funkce DNS.
Bloky prostředků, které následují volání zdroje z [xDnsServer](https://github.com/PowerShell/xDnsServer) modulu, který chcete konfigurovat zóny a záznamy DNS.

Všimněte si, že dva `xDnsRecord` bloky jsou zabaleny v `foreach` smyček, které iteraci přes pole v konfiguračních datech.
Znovu vytvoří konfigurační data `DevEnv.ps1` skript, který se podíváme na další.

### <a name="configuration-data"></a>Konfigurační data

`DevEnv.ps1` Souboru (z kořenového adresáře místního úložiště Demo_CI `./InfraDNS/DevEnv.ps1`) určuje specifických pro prostředí konfigurační data v zatřiďovací tabulku a pak předá tento zatřiďovací tabulky na volání `New-DscConfigurationDataDocument` funkce, která je definována v `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).

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

`New-DscConfigurationDataDocument` – Funkce (definované v `\Assets\DscPipelineTools\DscPipelineTools.psm1`) prostřednictvím kódu programu vytvoří konfigurační data dokumentu z zatřiďovací tabulky (data uzlu) a pole (data bez uzlu), které jsou předány jako `RawEnvData` a `OtherEnvData` parametry.

V našem případě pouze `RawEnvData` parametr se používá.

### <a name="the-psake-build-script"></a>Skript sestavení psake

[Psake](https://github.com/psake/psake) skript definovaný v sestavení `Build.ps1` (z kořenového adresáře úložiště Demo_CI `./InfraDNS/Build.ps1`) definuje úlohy, které jsou součástí sestavení.
Definuje také další úlohy, které každý úkol závisí.
Po vyvolání skriptu psake zajišťuje, že zadanou úlohu (nebo úloha s názvem `Default` Pokud není zadaný žádný) běží a že všechny závislosti také spustit (to je rekurzivní, tak, aby závislosti závislosti spouštět, a tak dále).

V tomto příkladu `Default` úkolu je definován jako:

```powershell
Task Default -depends UnitTests
```

`Default` Úloha nemá žádnou implementaci samotný, ale má závislost na `CompileConfigs` úloh.
Výsledný řetězec závislostí zajistí, že jsou spuštěny všechny úlohy ve skriptu buildu.

V tomto příkladu je skript psake vyvolána voláním `Invoke-PSake` v `Initiate.ps1` soubor (umístěný v kořenovém adresáři úložiště Demo_CI):

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

Když jsme v našem příkladu na serveru TFS vytvořte definici sestavení, jsme poskytne naše psake soubor skriptu jako `fileName` parametr pro tento skript.

Skript sestavení definuje následující úlohy:

#### <a name="generateenvironmentfiles"></a>GenerateEnvironmentFiles

Spuštění `DevEnv.ps1`, který generuje soubor konfiguračních dat.

#### <a name="installmodules"></a>InstallModules

Nainstaluje moduly potřebnými konfigurace `DNSServer.ps1`.

#### <a name="scriptanalysis"></a>ScriptAnalysis

Volání [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).

#### <a name="unittests"></a>UnitTests

Spuštění [Pester](https://github.com/pester/Pester/wiki) testování částí.

#### <a name="compileconfigs"></a>CompileConfigs

Zkompiluje konfiguraci (`DNSServer.ps1`) do souboru MOF pomocí konfiguračních dat generovaných `GenerateEnvironmentFiles` úloh.

#### <a name="clean"></a>Clean

Vytvoří složek používaných pro příklad a odebere všechny výsledky testů, soubory konfiguračních dat a moduly z předchozích spuštění.

### <a name="the-psake-deploy-script"></a>Skript nasadit psake

[Psake](https://github.com/psake/psake) skript nasazení, které jsou definovány v `Deploy.ps1` (z kořenového adresáře úložiště Demo_CI `./InfraDNS/Deploy.ps1`) definuje úlohy, které nasadit a spustit konfiguraci.

`Deploy.ps1` definuje následující úlohy:

#### <a name="deploymodules"></a>DeployModules

Spustí relaci prostředí PowerShell na `TestAgent1` a nainstaluje moduly obsahují prostředky DSC vyžadované pro konfiguraci.

#### <a name="deployconfigs"></a>DeployConfigs

Volání [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny spustit konfiguraci v `TestAgent1`.

#### <a name="integrationtests"></a>IntegrationTests

Spuštění [Pester](https://github.com/pester/Pester/wiki) integrační testy.

#### <a name="acceptancetests"></a>AcceptanceTests

Spuštění [Pester](https://github.com/pester/Pester/wiki) předávací testy.

#### <a name="clean"></a>Clean

Odebere všechny moduly nainstalované v předchozí běhy a zajistí, že existuje složka výsledků testu.

### <a name="test-scripts"></a>Testování skriptů

Přijetí, integrace a testy jednotek, které jsou definovány ve skriptech v `Tests` složky (z kořenového adresáře úložiště Demo_CI `./InfraDNS/Tests`), každá do souborů s názvem `DNSServer.tests.ps1` v jejich příslušné složky.

Testovací skripty použití [Pester](https://github.com/pester/Pester/wiki) a [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntaxe.

#### <a name="unit-tests"></a>Testy jednotek

Konfigurace testů DSC samy o sobě Ujistěte se, že konfigurace provedete, co se očekává při spuštění testování částí.
Skript používá test jednotky [Pester](https://github.com/pester/Pester/wiki).

#### <a name="integration-tests"></a>Integrační testy

Integrační testy otestovat konfiguraci systému a zajistit tak, že při integraci s ostatními součástmi, systém je nakonfigurován podle očekávání. Tyto testy se spouštějí na cílovém uzlu po dokončení konfigurace pomocí DSC.
Tento skript test integrace využívá kombinaci [Pester](https://github.com/pester/Pester/wiki) a [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntaxe.

#### <a name="acceptance-tests"></a>Předávací testy

Akceptační testy otestovat systém a ujistěte se, že se chová podle očekávání.
Například testy k zajištění, že se že vrátí správné informace při dotazu na webové stránce.
Tyto testy vzdáleně spouštět z cílového uzlu účely otestování scénářů reálného světa.
Tento skript test integrace využívá kombinaci [Pester](https://github.com/pester/Pester/wiki) a [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntaxe.

## <a name="define-the-build"></a>Definice sestavení

Teď, když jsme na server TFS odeslána našeho kódu a prohlédli jste si ho nemá, nadefinujeme našich sestavení.

Tady zaměříme jenom kroky sestavení, které přidáte do sestavení. Pokyny o tom, jak vytvořit definici sestavení v TFS naleznete v tématu [Create a queue definici sestavení](/azure/devops/pipelines/get-started-designer).

Vytvoření nové definice sestavení (vyberte **prázdný** šablony) s názvem "InfraDNS".
Přidáte že následující kroky vám definice sestavení:

- Skript prostředí PowerShell
- Publikování výsledků testů
- Kopírování souborů
- Publikování artefaktů

Po přidání tyto kroky sestavení, upravte vlastnosti každého kroku následujícím způsobem:

### <a name="powershell-script"></a>Skript prostředí PowerShell

1. Nastavte **typ** vlastnost `File Path`.
1. Nastavte **cesta ke skriptu** vlastnost `initiate.ps1`.
1. Přidat `-fileName build` k **argumenty** vlastnost.

Tento krok sestavení běží `initiate.ps1` soubor, který volá psake skript sestavení.

### <a name="publish-test-results"></a>Publikování výsledků testů

1. Nastavte **testování výsledku formátu** do `NUnit`
1. Nastavte **soubory výsledků testu** do `InfraDNS/Tests/Results/*.xml`
1. Nastavte **název testovacího běhu** k `Unit`.
1. Ujistěte se, že **možnosti ovládání** **povoleno** a **vždycky spouštět** jsou oba zaškrtnuto.

Tento krok sestavení spustí testy jednotek ve skriptu Pester jsme se podívali na dříve a ukládá výsledky `InfraDNS/Tests/Results/*.xml` složky.

### <a name="copy-files"></a>Kopírování souborů

1. Přidejte následující řádky do **obsah**:

   ```
   initiate.ps1
   **\deploy.ps1
   **\Acceptance\**
   **\Integration\**
   ```

1. Nastavte **TargetFolder** do `$(Build.ArtifactStagingDirectory)\`

Zkopíruje tento krok sestavení a testovací skripty do pracovního adresáře tak, lze publikovat, protože artefaktů sestavení na další krok.

### <a name="publish-artifact"></a>Publikování artefaktů

1. Nastavte **cesta k publikování** do `$(Build.ArtifactStagingDirectory)\`
1. Nastavte **název artefaktu** do `Deploy`
1. Nastavte **Typ artefaktu** do `Server`
1. Vyberte `Enabled` v **možnosti ovládání**

## <a name="enable-continuous-integration"></a>Povolit průběžnou integraci

Teď nastavíme triggeru, který způsobí, že projekt k sestavení kdykoli změnu se změnami do `ci-cd-example` větve úložiště git.

1. V sadě TFS, klikněte na tlačítko **sestavení a vydání** kartu
1. Vyberte `DNS Infra` definice sestavení a klikněte na tlačítko **upravit**
1. Klikněte na tlačítko **triggery** kartu
1. Vyberte **kontinuální integrace (CI)** a vyberte `refs/heads/ci-cd-example` v rozevíracím seznamu větve
1. Klikněte na tlačítko **Uložit** a potom **OK**

Nyní jakékoli změny v aktivační události git úložiště TFS automatické sestavení.

## <a name="create-the-release-definition"></a>Vytvoření definice verze

Pojďme vytvořit definici vydané verze, tak, že projekt je nasazen do vývojového prostředí s každou kód vrácení se změnami.

Provedete to tak, přidejte novou definici verze přidružené k `InfraDNS` jste předtím vytvořili definice sestavení.
Je potřeba vybrat možnost **průběžné nasazování** tak, aby se nová verze se aktivuje vždy nového sestavení se dokončí.
([Jak: Práce s definic vydané verze](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)) a nakonfigurujte následujícím způsobem:

Přidejte do definice vydané verze následující kroky:

- Skript prostředí PowerShell
- Publikování výsledků testů
- Publikování výsledků testů

Postup úpravy následujícím způsobem:

### <a name="powershell-script"></a>Skript prostředí PowerShell

1. Nastavte **cesta ke skriptu** pole `$(Build.DefinitionName)\Deploy\initiate.ps1"`
1. Nastavte **argumenty** pole `-fileName Deploy`

### <a name="first-publish-test-results"></a>Nejprve publikovat výsledky testů

1. Vyberte `NUnit` pro **formát výsledku testu** pole
1. Nastavte **soubory s výsledky testu** pole `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`
1. Nastavte **název testovacího běhu** do `Integration`
1. V části **možnosti ovládání**, zkontrolujte **vždycky spouštět**

### <a name="second-publish-test-results"></a>Za druhé publikovat výsledky testů

1. Vyberte `NUnit` pro **formát výsledku testu** pole
1. Nastavte **soubory s výsledky testu** pole `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`
1. Nastavte **název testovacího běhu** do `Acceptance`
1. V části **možnosti ovládání**, zkontrolujte **vždycky spouštět**

## <a name="verify-your-results"></a>Zkontrolujte výsledky

Teď, když odešlete změny `ci-cd-example` větve na server TFS, nové sestavení spustí.
Pokud se sestavení úspěšně dokončí, se aktivuje nové nasazení.

Výsledek nasazení můžete zkontrolovat otevřením prohlížeče v klientském počítači a přejdete na `www.contoso.com`.

## <a name="next-steps"></a>Další kroky

Tento příklad konfiguruje DNS server `TestAgent1` tak, aby adresa URL `www.contoso.com` přeloží na `TestAgent2`, ale ve skutečnosti Nenasazuje webu.
Kostru to udělat najdete v úložišti v rámci `WebApp` složky.
Můžete použít zástupné procedury, chcete-li vytvořit skripty psake Pester testy a konfigurace DSC k dispozici pro nasazení svůj vlastní web.
