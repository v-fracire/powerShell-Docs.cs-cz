---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Použít, Get a konfigurace v uzlu testů
ms.openlocfilehash: 41f8d2d75d3dd9621de615e7999c2690cb8ce44a
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403823"
---
# <a name="apply-get-and-test-configurations-on-a-node"></a>Použít, Get a konfigurace v uzlu testů

Tato příručka obsahuje pokyny pro práci s konfiguracemi na cílový uzel. Tato příručka je rozdělený do následujících kroků:

## <a name="apply-a-configuration"></a>Použití konfigurace

Pokud chcete použít a spravovat konfiguraci, musíte vygenerovat soubor "MOF". Následující kód bude představovat jednoduché konfigurace, který se použije v rámci tohoto průvodce.

```powershell
Configuration Sample
{
    # This will generate two .mof files, a localhost.mof, and a server02.mof
    Node localhost, server02
    {
        File SampleFile
        {
            DestinationPath = 'C:\Temp\temp.txt'
            Contents = 'This is a simple resource to show Configuration functionality on a Node.'
        }
    }
}

# The -OutputPath parameter is built into every Configuration automatically.
# The value of -OutputPath determines where the .mof file should be stored, once compiled.
Sample -OutputPath "C:\Temp\"
```

Kompilování tuto konfiguraci předá dva soubory ".mof".

```output
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a----       11/27/2018   7:29 AM     2.13KB localhost.mof
-a----       11/27/2018   7:29 AM     2.13KB server02.mof
```

Chcete-li použít konfiguraci, použijte [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny. `-Path` Parametr určuje adresář, kde jsou uloženy soubory ".mof". Pokud ne `-Computername` není zadána, `Start-DSCConfiguration` se pokusí použít každou konfiguraci názvu počítače určeném názvem souboru ".mof" (\<computername\>MOF). Zadejte `-Verbose` k `Start-DSCConfiguration` zobrazíte podrobnější výstup.

```powershell
Start-DSCConfiguration -Path C:\Temp\ -Verbose
```

Pokud `-Wait` není zadán, se zobrazí jedna úloha vytvořena. Vytvořená úloha bude mít jednu **ChildJob** pro každý soubor ".mof" zpracovány `Start-DSCConfiguration`.

```output
Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
45     Job45           Configuratio... Running       True            localhost,server02   Start-DSCConfiguration...
```

Pokud je konfigurace trvá příliš dlouho a chcete ji zastavit, můžete použít [Stop-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Stop-DscConfiguration) zastavení aplikace v místním uzlu.

```powershell
Stop-DSCConfiguration -Force
```

Jakmile budete hotovi, můžete zobrazit stav úlohy prostřednictvím úlohy objekt vrácený rutinou [Get-Job](/powershell/module/microsoft.powershell.core/get-job).

```powershell
$job = Get-Job
$job.ChildJobs
```

```output
Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
49     Job49           Configuratio... Completed     True            localhost            Start-DSCConfiguration...
50     Job50           Configuratio... Completed     True            server02             Start-DSCConfiguration...
```

Zobrazíte **Verbose** výstup, zobrazíte pomocí následujících příkazů **Verbose** datového proudu pro každou **ChildJob**. Další informace o úloh Powershellu najdete v tématu [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs).

```powershell
# View the verbose output of the localhost job using array indexing.
$job.ChildJobs[0].Verbose
```

```output
Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendConfigurationApply,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
An LCM method call arrived from computer SERVER01 with user sid S-1-5-21-124525095-708259637-1543119021-1282804.
[SERVER01]: LCM:  [ Start  Set      ]
[SERVER01]: LCM:  [ Start  Resource ]  [[File]SampleFile]
[SERVER01]: LCM:  [ Start  Test     ]  [[File]SampleFile]
[SERVER01]:                            [[File]SampleFile] The destination object was found and no action is required.
[SERVER01]: LCM:  [ End    Test     ]  [[File]SampleFile]  in 0.0370 seconds.
[SERVER01]: LCM:  [ Skip   Set      ]  [[File]SampleFile]
[SERVER01]: LCM:  [ End    Resource ]  [[File]SampleFile]
[SERVER01]: LCM:  [ End    Set      ]
[SERVER01]: LCM:  [ End    Set      ]    in  0.2400 seconds.
Operation 'Invoke CimMethod' complete.
```

V Powershellu 5.0 `-UseExisting` parametr byl přidán do `Start-DSCConfiguration`. Zadáním `-UseExisting`, dáte pokyn, aby se rutina mohla používat existující konfigurace použité místo určený `-Path` parametru.

```powershell
Start-DSCConfiguration -UseExisting -Verbose -Wait
```

## <a name="test-a-configuration"></a>Testování konfigurace

Můžete otestovat aktuálně použité pomocí konfigurace [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration). `Test-DSCConfiguration` Vrátí `True` Pokud uzel je v souladu, a `False` nesplnění.

```powershell
Test-DSCConfiguration
```

V Powershellu 5.0 `-Detailed` parametr byl přidán, která vrací objekt s kolekcí pro **ResourcesInDesiredState** a **ResourcesNotInDesiredState**

```powershell
Test-DSCConfiguration -Detailed
```

Od v Powershellu 5.0 můžete otestovat konfiguraci bez jeho použití. `-ReferenceConfiguration` Parametr přijímá cesty ".mof" soubor pro test uzlu, u. Ne **nastavit** jsou akcí provedených vůči uzlu. V Powershellu 4.0 existují řešení v oblasti testování konfigurace bez jeho použití, ale nejsou popsány zde.

## <a name="get-configuration-values"></a>Získání hodnoty konfigurace

[Get-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) rutina vrací aktuální hodnoty pro všechny nakonfigurované prostředky v aktuálně použité konfigurace.

```powershell
Get-DSCConfiguration
```

Výstup z naše ukázka konfigurace by vypadalo takto úspěšně použila.

```output
ConfigurationName    : Sample
DependsOn            :
ModuleName           : PSDesiredStateConfiguration
ModuleVersion        :
PsDscRunAsCredential :
ResourceId           : [File]SampleFile
SourceInfo           :
Attributes           : {archive}
Checksum             :
Contents             :
CreatedDate          : 11/27/2018 7:16:06 AM
Credential           :
DestinationPath      : C:\Temp\temp.txt
Ensure               : present
Force                :
MatchSource          :
ModifiedDate         : 11/27/2018 7:16:06 AM
Recurse              :
Size                 : 75
SourcePath           :
SubItems             :
Type                 : file
PSComputerName       :
CimClassName         : MSFT_FileDirectoryConfiguration
```

## <a name="get-configuration-status"></a>Získat stav konfigurace

V Powershellu 5.0 [Get-DSCConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus) rutina umožňuje zobrazit historii konfigurace použité k uzlu. PowerShell DSC uchovává informace o poslední {{N}} konfigurace použité v **Push** nebo **o přijetí změn** režimu. Jedná se o některý *konzistence* proveden LCM kontroly. Ve výchozím nastavení `Get-DSCConfigurationStatus` zobrazuje jenom poslední položka historie.

```powershell
Get-DSCConfigurationStatus
```

```output
Status     StartDate                 Type            Mode  RebootRequested      NumberOfResources
------     ---------                 ----            ----  ---------------      -----------------
Success    11/27/2018 7:18:40 AM     Consistency     PUSH  False                1
```

Použití `-All` parametr zobrazíte historii všech stav konfigurace.

> [!NOTE]
> Výstup je zkrácen pro zkrácení.

```powershell
Get-DSCConfigurationStatus -All
```

```output
Status     StartDate                 Type            Mode  RebootRequested      NumberOfResources
------     ---------                 ----            ----  ---------------      -----------------
Success    11/27/2018 7:18:40 AM     Consistency     PUSH  False                1
Success    11/27/2018 7:16:06 AM     Initial         PUSH  False                1
Success    11/27/2018 7:04:53 AM     Initial         PUSH  False                1
Success    11/27/2018 7:03:45 AM     Consistency     PUSH  False                2
Success    11/27/2018 7:03:40 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:48:40 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:33:44 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:33:40 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:18:40 AM     Consistency     PUSH  False                2
Success    11/27/2018 6:03:44 AM     Consistency     PUSH  False                2
```

## <a name="manage-configuration-documents"></a>Správa konfigurace dokumentů

Práce s konfigurační uzel spravuje LCM **konfigurace dokumenty**. Tyto soubory ".mof" jsou umístěny v adresáři "C:\Windows\System32\Configuration".

V Powershellu 5.0 [odebrat DSCConfigurationDocument](/powershell/module/PSDesiredStateConfiguration/Remove-DscConfigurationDocument) slouží k odebrání souborů ".mof" zastavení kontroly konzistence budoucí nebo odeberte konfiguraci, která obsahuje chyby při použití. `-Stage` Parametrů můžete zadat soubor "MOF", který chcete odebrat.

```powershell
Remove-DSCConfigurationDocument -Stage Current
```

> [!NOTE]
> V Powershellu 4.0, můžete odebrat tyto soubory ".mof" přímo pomocí [Remove-Item](/powershell/module/microsoft.powershell.management/remove-item).

## <a name="publish-configurations"></a>Konfigurace publikování

V Powershellu 5.0 [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) rutina byla přidána. Tato rutina umožňuje publikování souboru ".mof" na vzdálených počítačích, bez jeho použití.

```powershell
Publish-DscConfiguration -Path '$home\WebServer' -ComputerName "ContosoWebServer" -Credential (get-credential Contoso\webadministrator)
```

## <a name="see-also"></a>Viz taky

- [Získání, testu a nastavení](../resources/get-test-set.md)
