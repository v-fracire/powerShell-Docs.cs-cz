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
# <a name="apply-get-and-test-configurations-on-a-node"></a><span data-ttu-id="6bbc0-103">Použít, Get a konfigurace v uzlu testů</span><span class="sxs-lookup"><span data-stu-id="6bbc0-103">Apply, Get, and Test Configurations on a Node</span></span>

<span data-ttu-id="6bbc0-104">Tato příručka obsahuje pokyny pro práci s konfiguracemi na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-104">This guide will show you how to work with Configurations on a target Node.</span></span> <span data-ttu-id="6bbc0-105">Tato příručka je rozdělený do následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="6bbc0-105">This guide is broken up into the following steps:</span></span>

## <a name="apply-a-configuration"></a><span data-ttu-id="6bbc0-106">Použití konfigurace</span><span class="sxs-lookup"><span data-stu-id="6bbc0-106">Apply a Configuration</span></span>

<span data-ttu-id="6bbc0-107">Pokud chcete použít a spravovat konfiguraci, musíte vygenerovat soubor "MOF".</span><span class="sxs-lookup"><span data-stu-id="6bbc0-107">In order to apply and manage a Configuration, we need to generate a ".mof" file.</span></span> <span data-ttu-id="6bbc0-108">Následující kód bude představovat jednoduché konfigurace, který se použije v rámci tohoto průvodce.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-108">The following code will represent a simple Configuration that will be used throughout this guide.</span></span>

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

<span data-ttu-id="6bbc0-109">Kompilování tuto konfiguraci předá dva soubory ".mof".</span><span class="sxs-lookup"><span data-stu-id="6bbc0-109">Compiling this configuration will yield two ".mof" files.</span></span>

```output
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a----       11/27/2018   7:29 AM     2.13KB localhost.mof
-a----       11/27/2018   7:29 AM     2.13KB server02.mof
```

<span data-ttu-id="6bbc0-110">Chcete-li použít konfiguraci, použijte [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-110">To apply a Configuration, use the [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span> <span data-ttu-id="6bbc0-111">`-Path` Parametr určuje adresář, kde jsou uloženy soubory ".mof".</span><span class="sxs-lookup"><span data-stu-id="6bbc0-111">The `-Path` parameter specifies a directory where ".mof" files reside.</span></span> <span data-ttu-id="6bbc0-112">Pokud ne `-Computername` není zadána, `Start-DSCConfiguration` se pokusí použít každou konfiguraci názvu počítače určeném názvem souboru ".mof" (\<computername\>MOF).</span><span class="sxs-lookup"><span data-stu-id="6bbc0-112">If no `-Computername` is specified, `Start-DSCConfiguration` will attempt to apply each Configuration to the computer name specified by the name of the '.mof' file (\<computername\>.mof).</span></span> <span data-ttu-id="6bbc0-113">Zadejte `-Verbose` k `Start-DSCConfiguration` zobrazíte podrobnější výstup.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-113">Specify `-Verbose` to `Start-DSCConfiguration` to see more verbose output.</span></span>

```powershell
Start-DSCConfiguration -Path C:\Temp\ -Verbose
```

<span data-ttu-id="6bbc0-114">Pokud `-Wait` není zadán, se zobrazí jedna úloha vytvořena.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-114">If `-Wait` is not specified, you see one job created.</span></span> <span data-ttu-id="6bbc0-115">Vytvořená úloha bude mít jednu **ChildJob** pro každý soubor ".mof" zpracovány `Start-DSCConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-115">The job created will have one **ChildJob** for each ".mof" file processed by `Start-DSCConfiguration`.</span></span>

```output
Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
45     Job45           Configuratio... Running       True            localhost,server02   Start-DSCConfiguration...
```

<span data-ttu-id="6bbc0-116">Pokud je konfigurace trvá příliš dlouho a chcete ji zastavit, můžete použít [Stop-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Stop-DscConfiguration) zastavení aplikace v místním uzlu.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-116">If a Configuration is taking a long time and you want to stop it, you can use [Stop-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Stop-DscConfiguration) to stop application on the local Node.</span></span>

```powershell
Stop-DSCConfiguration -Force
```

<span data-ttu-id="6bbc0-117">Jakmile budete hotovi, můžete zobrazit stav úlohy prostřednictvím úlohy objekt vrácený rutinou [Get-Job](/powershell/module/microsoft.powershell.core/get-job).</span><span class="sxs-lookup"><span data-stu-id="6bbc0-117">Once complete, you can view the status of the jobs through the job object returned by [Get-Job](/powershell/module/microsoft.powershell.core/get-job).</span></span>

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

<span data-ttu-id="6bbc0-118">Zobrazíte **Verbose** výstup, zobrazíte pomocí následujících příkazů **Verbose** datového proudu pro každou **ChildJob**.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-118">To see the **Verbose** output, use the following commands to view the **Verbose** stream for each **ChildJob**.</span></span> <span data-ttu-id="6bbc0-119">Další informace o úloh Powershellu najdete v tématu [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs).</span><span class="sxs-lookup"><span data-stu-id="6bbc0-119">For more about PowerShell jobs, see [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs).</span></span>

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

<span data-ttu-id="6bbc0-120">V Powershellu 5.0 `-UseExisting` parametr byl přidán do `Start-DSCConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-120">Beginning in PowerShell 5.0, the `-UseExisting` parameter was added to `Start-DSCConfiguration`.</span></span> <span data-ttu-id="6bbc0-121">Zadáním `-UseExisting`, dáte pokyn, aby se rutina mohla používat existující konfigurace použité místo určený `-Path` parametru.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-121">By specifying `-UseExisting`, you instruct the cmdlet to use the existing applied Configuration instead of one specified by the `-Path` parameter.</span></span>

```powershell
Start-DSCConfiguration -UseExisting -Verbose -Wait
```

## <a name="test-a-configuration"></a><span data-ttu-id="6bbc0-122">Testování konfigurace</span><span class="sxs-lookup"><span data-stu-id="6bbc0-122">Test a Configuration</span></span>

<span data-ttu-id="6bbc0-123">Můžete otestovat aktuálně použité pomocí konfigurace [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration).</span><span class="sxs-lookup"><span data-stu-id="6bbc0-123">You can test a currently applied Configuration using [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration).</span></span> <span data-ttu-id="6bbc0-124">`Test-DSCConfiguration` Vrátí `True` Pokud uzel je v souladu, a `False` nesplnění.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-124">`Test-DSCConfiguration` will return `True` if the Node is compliant, and `False` if it is not.</span></span>

```powershell
Test-DSCConfiguration
```

<span data-ttu-id="6bbc0-125">V Powershellu 5.0 `-Detailed` parametr byl přidán, která vrací objekt s kolekcí pro **ResourcesInDesiredState** a **ResourcesNotInDesiredState**</span><span class="sxs-lookup"><span data-stu-id="6bbc0-125">Beginning in PowerShell 5.0, the `-Detailed` parameter was added which returns an object with collections for **ResourcesInDesiredState** and **ResourcesNotInDesiredState**</span></span>

```powershell
Test-DSCConfiguration -Detailed
```

<span data-ttu-id="6bbc0-126">Od v Powershellu 5.0 můžete otestovat konfiguraci bez jeho použití.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-126">Beginning in PowerShell 5.0 you can test a Configuration without applying it.</span></span> <span data-ttu-id="6bbc0-127">`-ReferenceConfiguration` Parametr přijímá cesty ".mof" soubor pro test uzlu, u.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-127">The `-ReferenceConfiguration` parameter accepts the path of a ".mof" file to test the Node against.</span></span> <span data-ttu-id="6bbc0-128">Ne **nastavit** jsou akcí provedených vůči uzlu.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-128">No **Set** actions are taken against the Node.</span></span> <span data-ttu-id="6bbc0-129">V Powershellu 4.0 existují řešení v oblasti testování konfigurace bez jeho použití, ale nejsou popsány zde.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-129">In PowerShell 4.0, there are workarounds to test a Configuration without applying it, but they are not discussed here.</span></span>

## <a name="get-configuration-values"></a><span data-ttu-id="6bbc0-130">Získání hodnoty konfigurace</span><span class="sxs-lookup"><span data-stu-id="6bbc0-130">Get Configuration Values</span></span>

<span data-ttu-id="6bbc0-131">[Get-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) rutina vrací aktuální hodnoty pro všechny nakonfigurované prostředky v aktuálně použité konfigurace.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-131">The [Get-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) cmdlet returns the current values for any configured resources in the currently applied Configuration.</span></span>

```powershell
Get-DSCConfiguration
```

<span data-ttu-id="6bbc0-132">Výstup z naše ukázka konfigurace by vypadalo takto úspěšně použila.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-132">Output from our sample Configuration would look like this if applied successfully.</span></span>

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

## <a name="get-configuration-status"></a><span data-ttu-id="6bbc0-133">Získat stav konfigurace</span><span class="sxs-lookup"><span data-stu-id="6bbc0-133">Get Configuration Status</span></span>

<span data-ttu-id="6bbc0-134">V Powershellu 5.0 [Get-DSCConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus) rutina umožňuje zobrazit historii konfigurace použité k uzlu.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-134">Beginning in PowerShell 5.0 the [Get-DSCConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus) cmdlet allows you to see the history of applied Configurations to the node.</span></span> <span data-ttu-id="6bbc0-135">PowerShell DSC uchovává informace o poslední {{N}} konfigurace použité v **Push** nebo **o přijetí změn** režimu.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-135">PowerShell DSC keeps track of the last {{N}} Configurations applied in **Push** or **Pull** mode.</span></span> <span data-ttu-id="6bbc0-136">Jedná se o některý *konzistence* proveden LCM kontroly.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-136">This includes any *consistency* checks executed by the LCM.</span></span> <span data-ttu-id="6bbc0-137">Ve výchozím nastavení `Get-DSCConfigurationStatus` zobrazuje jenom poslední položka historie.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-137">By default, `Get-DSCConfigurationStatus` shows you the last history entry only.</span></span>

```powershell
Get-DSCConfigurationStatus
```

```output
Status     StartDate                 Type            Mode  RebootRequested      NumberOfResources
------     ---------                 ----            ----  ---------------      -----------------
Success    11/27/2018 7:18:40 AM     Consistency     PUSH  False                1
```

<span data-ttu-id="6bbc0-138">Použití `-All` parametr zobrazíte historii všech stav konfigurace.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-138">Use the `-All` parameter to see all Configuration Status history.</span></span>

> [!NOTE]
> <span data-ttu-id="6bbc0-139">Výstup je zkrácen pro zkrácení.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-139">Output is truncated for brevity.</span></span>

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

## <a name="manage-configuration-documents"></a><span data-ttu-id="6bbc0-140">Správa konfigurace dokumentů</span><span class="sxs-lookup"><span data-stu-id="6bbc0-140">Manage Configuration Documents</span></span>

<span data-ttu-id="6bbc0-141">Práce s konfigurační uzel spravuje LCM **konfigurace dokumenty**.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-141">The LCM manages the Configuration of the Node by working with **Configuration Documents**.</span></span> <span data-ttu-id="6bbc0-142">Tyto soubory ".mof" jsou umístěny v adresáři "C:\Windows\System32\Configuration".</span><span class="sxs-lookup"><span data-stu-id="6bbc0-142">These ".mof" files reside in the "C:\Windows\System32\Configuration" directory.</span></span>

<span data-ttu-id="6bbc0-143">V Powershellu 5.0 [odebrat DSCConfigurationDocument](/powershell/module/PSDesiredStateConfiguration/Remove-DscConfigurationDocument) slouží k odebrání souborů ".mof" zastavení kontroly konzistence budoucí nebo odeberte konfiguraci, která obsahuje chyby při použití.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-143">Beginning in PowerShell 5.0 the [Remove-DSCConfigurationDocument](/powershell/module/PSDesiredStateConfiguration/Remove-DscConfigurationDocument) allows you to remove the ".mof" files to stop future consistency checks or remove a Configuration that has errors when applied.</span></span> <span data-ttu-id="6bbc0-144">`-Stage` Parametrů můžete zadat soubor "MOF", který chcete odebrat.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-144">The `-Stage` parameter allows you to specify which ".mof" file you want to remove.</span></span>

```powershell
Remove-DSCConfigurationDocument -Stage Current
```

> [!NOTE]
> <span data-ttu-id="6bbc0-145">V Powershellu 4.0, můžete odebrat tyto soubory ".mof" přímo pomocí [Remove-Item](/powershell/module/microsoft.powershell.management/remove-item).</span><span class="sxs-lookup"><span data-stu-id="6bbc0-145">In PowerShell 4.0, you can still remove these ".mof" files directly using [Remove-Item](/powershell/module/microsoft.powershell.management/remove-item).</span></span>

## <a name="publish-configurations"></a><span data-ttu-id="6bbc0-146">Konfigurace publikování</span><span class="sxs-lookup"><span data-stu-id="6bbc0-146">Publish Configurations</span></span>

<span data-ttu-id="6bbc0-147">V Powershellu 5.0 [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) rutina byla přidána.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-147">Beginning in PowerShell 5.0, the [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) cmdlet was added.</span></span> <span data-ttu-id="6bbc0-148">Tato rutina umožňuje publikování souboru ".mof" na vzdálených počítačích, bez jeho použití.</span><span class="sxs-lookup"><span data-stu-id="6bbc0-148">This cmdlet allows you to publish a ".mof" file to remote computers, without applying it.</span></span>

```powershell
Publish-DscConfiguration -Path '$home\WebServer' -ComputerName "ContosoWebServer" -Credential (get-credential Contoso\webadministrator)
```

## <a name="see-also"></a><span data-ttu-id="6bbc0-149">Viz taky</span><span class="sxs-lookup"><span data-stu-id="6bbc0-149">See also</span></span>

- [<span data-ttu-id="6bbc0-150">Získání, testu a nastavení</span><span class="sxs-lookup"><span data-stu-id="6bbc0-150">Get, Test, and Set</span></span>](../resources/get-test-set.md)
