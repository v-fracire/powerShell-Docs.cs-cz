---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC skriptu prostředků"
ms.openlocfilehash: d3e231d33a04fd8a018ffe2f3d51a15360e0d312
ms.sourcegitcommit: 60f06a06c2fce63024f3f4cbd7657b1dfe7fcb1a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/03/2018
---
# <a name="dsc-script-resource"></a><span data-ttu-id="69e7d-103">DSC skriptu prostředků</span><span class="sxs-lookup"><span data-stu-id="69e7d-103">DSC Script Resource</span></span>

 
> <span data-ttu-id="69e7d-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="69e7d-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="69e7d-105">**Skriptu** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke spuštění blocích skriptu prostředí Windows PowerShell na cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="69e7d-105">The **Script** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to run Windows PowerShell script blocks on target nodes.</span></span> <span data-ttu-id="69e7d-106">`Script` Prostředek má `GetScript`, `SetScript`, a `TestScript` vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="69e7d-106">The `Script` resource has `GetScript`, `SetScript`, and `TestScript` properties.</span></span> <span data-ttu-id="69e7d-107">Tyto vlastnosti musí být nastaven na skript bloky, které poběží na každý cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="69e7d-107">These properties should be set to script blocks that will run on each target node.</span></span> 

<span data-ttu-id="69e7d-108">`GetScript` Bloku skriptu by měla vrátit zatřiďovací tabulku představující stav aktuálního uzlu.</span><span class="sxs-lookup"><span data-stu-id="69e7d-108">The `GetScript` script block should return a hashtable representing the state of the current node.</span></span> <span data-ttu-id="69e7d-109">Zatřiďovací tabulky musí obsahovat jenom jeden klíč `Result` a hodnota musí být typu `String`.</span><span class="sxs-lookup"><span data-stu-id="69e7d-109">The hashtable must only contain one key `Result` and the value must be of type `String`.</span></span> <span data-ttu-id="69e7d-110">Není potřeba nic vrátit.</span><span class="sxs-lookup"><span data-stu-id="69e7d-110">It is not required to return anything.</span></span> <span data-ttu-id="69e7d-111">DSC nic se neděje s výstup tento blok skriptu.</span><span class="sxs-lookup"><span data-stu-id="69e7d-111">DSC doesn't do anything with the output of this script block.</span></span>

<span data-ttu-id="69e7d-112">`TestScript` Bloku skriptu měli zjistit, pokud má být změněn na aktuální uzel.</span><span class="sxs-lookup"><span data-stu-id="69e7d-112">The `TestScript` script block should determine if the current node needs to be modified.</span></span> <span data-ttu-id="69e7d-113">Měla by vrátit `$true` Pokud je aktuální uzel.</span><span class="sxs-lookup"><span data-stu-id="69e7d-113">It should return `$true` if the node is up-to-date.</span></span> <span data-ttu-id="69e7d-114">Měla by vrátit `$false` Pokud konfigurace uzlu je zastaralý a by měl být aktualizován `SetScript` bloku skriptu.</span><span class="sxs-lookup"><span data-stu-id="69e7d-114">It should return `$false` if the node's configuration is out-of-date and should be updated by the `SetScript` script block.</span></span> <span data-ttu-id="69e7d-115">`TestScript` Bloku skriptu je volána metodou DSC.</span><span class="sxs-lookup"><span data-stu-id="69e7d-115">The `TestScript` script block is called by DSC.</span></span>

<span data-ttu-id="69e7d-116">`SetScript` Bloku skriptu by měl změnit uzlu.</span><span class="sxs-lookup"><span data-stu-id="69e7d-116">The `SetScript` script block should modify the node.</span></span> <span data-ttu-id="69e7d-117">Je volána metodou DSC, pokud `TestScript` blokovat vrátit `$false`.</span><span class="sxs-lookup"><span data-stu-id="69e7d-117">It is called by DSC if the `TestScript` block return `$false`.</span></span>

<span data-ttu-id="69e7d-118">Pokud budete muset použít proměnné z vaší konfigurační skript v `GetScript`, `TestScript`, nebo `SetScript` bloky skriptu, použijte `$using:` oboru (dole najdete příklad).</span><span class="sxs-lookup"><span data-stu-id="69e7d-118">If you need to use variables from your configuration script in the `GetScript`, `TestScript`, or `SetScript` script blocks, use the `$using:` scope (see below for an example).</span></span>


## <a name="syntax"></a><span data-ttu-id="69e7d-119">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="69e7d-119">Syntax</span></span>

```
Script [string] #ResourceName
{
    GetScript = [string]
    SetScript = [string]
    TestScript = [string]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="69e7d-120">Properties</span><span class="sxs-lookup"><span data-stu-id="69e7d-120">Properties</span></span>

|  <span data-ttu-id="69e7d-121">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="69e7d-121">Property</span></span>  |  <span data-ttu-id="69e7d-122">Popis</span><span class="sxs-lookup"><span data-stu-id="69e7d-122">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="69e7d-123">GetScript</span><span class="sxs-lookup"><span data-stu-id="69e7d-123">GetScript</span></span>| <span data-ttu-id="69e7d-124">Poskytuje blok skriptu prostředí Windows PowerShell, který je spuštěn při vyvolání [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="69e7d-124">Provides a block of Windows PowerShell script that runs when you invoke the [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx) cmdlet.</span></span> <span data-ttu-id="69e7d-125">Tento blok musí vracet zatřiďovací tabulku.</span><span class="sxs-lookup"><span data-stu-id="69e7d-125">This block must return a hashtable.</span></span> <span data-ttu-id="69e7d-126">Zatřiďovací tabulky musí obsahovat jenom jeden klíč **výsledek** a hodnota musí být typu **řetězec**.</span><span class="sxs-lookup"><span data-stu-id="69e7d-126">The hashtable must only contain one key **Result** and the value must be of type **String**.</span></span>| 
| <span data-ttu-id="69e7d-127">SetScript</span><span class="sxs-lookup"><span data-stu-id="69e7d-127">SetScript</span></span>| <span data-ttu-id="69e7d-128">Poskytuje blok skriptu prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69e7d-128">Provides a block of Windows PowerShell script.</span></span> <span data-ttu-id="69e7d-129">Při vyvolání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny **TestScript** bloku spustí první.</span><span class="sxs-lookup"><span data-stu-id="69e7d-129">When you invoke the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, the **TestScript** block runs first.</span></span> <span data-ttu-id="69e7d-130">Pokud **TestScript** blokovat vrátí **$false**, **SetScript** bloku se spustí.</span><span class="sxs-lookup"><span data-stu-id="69e7d-130">If the **TestScript** block returns **$false**, the **SetScript** block will run.</span></span> <span data-ttu-id="69e7d-131">Pokud **TestScript** blokovat vrátí **$true**, **SetScript** bloku se nespustí.</span><span class="sxs-lookup"><span data-stu-id="69e7d-131">If the **TestScript** block returns **$true**, the **SetScript** block will not run.</span></span>| 
| <span data-ttu-id="69e7d-132">TestScript</span><span class="sxs-lookup"><span data-stu-id="69e7d-132">TestScript</span></span>| <span data-ttu-id="69e7d-133">Poskytuje blok skriptu prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69e7d-133">Provides a block of Windows PowerShell script.</span></span> <span data-ttu-id="69e7d-134">Při vyvolání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) spuštění rutiny, tento blok.</span><span class="sxs-lookup"><span data-stu-id="69e7d-134">When you invoke the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, this block runs.</span></span> <span data-ttu-id="69e7d-135">Vrátí-li **$false**, spustí SetScript bloku.</span><span class="sxs-lookup"><span data-stu-id="69e7d-135">If it returns **$false**, the SetScript block will run.</span></span> <span data-ttu-id="69e7d-136">Vrátí-li **$true**, SetScript bloku se nespustí.</span><span class="sxs-lookup"><span data-stu-id="69e7d-136">If it returns **$true**, the SetScript block will not run.</span></span> <span data-ttu-id="69e7d-137">**TestScript** bloku poběží i v případě vyvolání [Test DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="69e7d-137">The **TestScript** block also runs when you invoke the [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) cmdlet.</span></span> <span data-ttu-id="69e7d-138">V takovém případě však **SetScript** bloku nebude spouštět, bez ohledu na to, co hodnotu TestScript blokovat vrátí.</span><span class="sxs-lookup"><span data-stu-id="69e7d-138">However, in this case, the **SetScript** block will not run, no matter what value the TestScript block returns.</span></span> <span data-ttu-id="69e7d-139">**TestScript** bloku musí vracet hodnotu True, pokud skutečné konfigurace odpovídá aktuální konfigurace požadovaného stavu a na hodnotu False, pokud neodpovídá.</span><span class="sxs-lookup"><span data-stu-id="69e7d-139">The **TestScript** block must return True if the actual configuration matches the current desired state configuration, and False if it does not match.</span></span> <span data-ttu-id="69e7d-140">(Aktuální konfigurace požadovaného stavu je poslední konfigurace použity na uzlu, který používá DSC.)</span><span class="sxs-lookup"><span data-stu-id="69e7d-140">(The current desired state configuration is the last configuration enacted on the node that is using DSC.)</span></span>| 
| <span data-ttu-id="69e7d-141">přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="69e7d-141">Credential</span></span>| <span data-ttu-id="69e7d-142">Určuje pověření sloužící ke spuštění tohoto skriptu, pokud je třeba zadat pověření.</span><span class="sxs-lookup"><span data-stu-id="69e7d-142">Indicates the credentials to use for running this script, if credentials are required.</span></span>| 
| <span data-ttu-id="69e7d-143">dependsOn</span><span class="sxs-lookup"><span data-stu-id="69e7d-143">DependsOn</span></span>| <span data-ttu-id="69e7d-144">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="69e7d-144">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="69e7d-145">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba **ResourceName** a její typ je **ResourceType**, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="69e7d-145">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>

## <a name="example-1"></a><span data-ttu-id="69e7d-146">Příklad 1</span><span class="sxs-lookup"><span data-stu-id="69e7d-146">Example 1</span></span>
```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script ScriptExample
    {
        SetScript = 
        { 
            $sw = New-Object System.IO.StreamWriter("C:\TempFolder\TestFile.txt")
            $sw.WriteLine("Some sample string")
            $sw.Close()
        }
        TestScript = { Test-Path "C:\TempFolder\TestFile.txt" }
        GetScript = { @{ Result = (Get-Content C:\TempFolder\TestFile.txt) } }          
    }
}
```

## <a name="example-2"></a><span data-ttu-id="69e7d-147">Příklad 2</span><span class="sxs-lookup"><span data-stu-id="69e7d-147">Example 2</span></span>
```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script UpdateConfigurationVersion
    {
        GetScript = { 
            $currentVersion = Get-Content (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
            return @{ 'Result' = "$currentVersion" }
        }          
        TestScript = { 
            $state = $GetScript
            if( $state['Result'] -eq $using:version )
            {
                Write-Verbose -Message ('{0} -eq {1}' -f $state['Result'],$using:version)
                return $true
            }
            Write-Verbose -Message ('Version up-to-date: {0}' -f $using:version)
            return $false
        }
        SetScript = { 
            $using:version | Set-Content -Path (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
        }
    }
}
```

<span data-ttu-id="69e7d-148">Tento prostředek je zapisování konfigurace do textového souboru.</span><span class="sxs-lookup"><span data-stu-id="69e7d-148">This resource is writing the configuration's version to a text file.</span></span> <span data-ttu-id="69e7d-149">Tato verze je dostupná v klientském počítači, ale není na všech uzlech, tak musí být předán ke každému `Script` blocích skriptu prostředku v prostředí PowerShell na `using` oboru.</span><span class="sxs-lookup"><span data-stu-id="69e7d-149">This version is available on the client computer, but isn't on any of the nodes, so it has to be passed to each of the `Script` resource's script blocks with PowerShell's `using` scope.</span></span> <span data-ttu-id="69e7d-150">Při generování uzlu MOF souboru, hodnota `$version` proměnnou je pro čtení z textového souboru v klientském počítači.</span><span class="sxs-lookup"><span data-stu-id="69e7d-150">When generating the node's MOF file, the value of the `$version` variable is read from a text file on the client computer.</span></span> <span data-ttu-id="69e7d-151">Nahradí DSC `$using:version` proměnné v každý skript blokovat s hodnotou `$version` proměnné.</span><span class="sxs-lookup"><span data-stu-id="69e7d-151">DSC replaces the `$using:version` variables in each script block with the value of the `$version` variable.</span></span>

