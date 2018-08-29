---
ms.date: 08/24/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC Script
ms.openlocfilehash: ef84239820a44aab2a028f7f0fe17653a851b72e
ms.sourcegitcommit: 59727f71dc204785a1bcdedc02716d8340a77aeb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2018
ms.locfileid: "43133889"
---
# <a name="dsc-script-resource"></a><span data-ttu-id="5f515-103">Prostředek DSC Script</span><span class="sxs-lookup"><span data-stu-id="5f515-103">DSC Script Resource</span></span>

> <span data-ttu-id="5f515-104">Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.x</span><span class="sxs-lookup"><span data-stu-id="5f515-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.x</span></span>

<span data-ttu-id="5f515-105">**Skript** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro spuštění bloky skriptu prostředí Windows PowerShell na cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="5f515-105">The **Script** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to run Windows PowerShell script blocks on target nodes.</span></span> <span data-ttu-id="5f515-106">**Skript** prostředků používá `GetScript`, `SetScript`, a `TestScript` vlastnosti, které obsahují bloky skriptu definujete k provedení odpovídající DSC stavu operace.</span><span class="sxs-lookup"><span data-stu-id="5f515-106">The **Script** resource uses `GetScript`, `SetScript`, and `TestScript` properties that contain script blocks you define to perform the corresponding DSC state operations.</span></span>

## <a name="syntax"></a><span data-ttu-id="5f515-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="5f515-107">Syntax</span></span>

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

> [!NOTE]
> <span data-ttu-id="5f515-108">`GetScript`, `TestScript`, A `SetScript` bloky jsou uloženy jako řetězce.</span><span class="sxs-lookup"><span data-stu-id="5f515-108">The `GetScript`, `TestScript`, and `SetScript` blocks are stored as strings.</span></span>

## <a name="properties"></a><span data-ttu-id="5f515-109">Properties</span><span class="sxs-lookup"><span data-stu-id="5f515-109">Properties</span></span>

|<span data-ttu-id="5f515-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="5f515-110">Property</span></span>|<span data-ttu-id="5f515-111">Popis</span><span class="sxs-lookup"><span data-stu-id="5f515-111">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="5f515-112">GetScript</span><span class="sxs-lookup"><span data-stu-id="5f515-112">GetScript</span></span>|<span data-ttu-id="5f515-113">Blok skriptu, který vrací aktuální stav tohoto uzlu.</span><span class="sxs-lookup"><span data-stu-id="5f515-113">A script block that returns the current state of the Node.</span></span>|
|<span data-ttu-id="5f515-114">SetScript</span><span class="sxs-lookup"><span data-stu-id="5f515-114">SetScript</span></span>|<span data-ttu-id="5f515-115">Blok skriptu, který používá DSC pro vynucování dodržování předpisů, pokud uzel není v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="5f515-115">A script block that DSC uses to enforce compliance when the Node is not in the desired state.</span></span>|
|<span data-ttu-id="5f515-116">TestScript</span><span class="sxs-lookup"><span data-stu-id="5f515-116">TestScript</span></span>|<span data-ttu-id="5f515-117">Blok skriptu, který určuje, zda je uzel v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="5f515-117">A script block that determines if the Node is in the desired state.</span></span>|
|<span data-ttu-id="5f515-118">Přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="5f515-118">Credential</span></span>| <span data-ttu-id="5f515-119">Určuje přihlašovací údaje používat pro spouštění tohoto skriptu, pokud se vyžadují přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="5f515-119">Indicates the credentials to use for running this script, if credentials are required.</span></span>|
|<span data-ttu-id="5f515-120">DependsOn</span><span class="sxs-lookup"><span data-stu-id="5f515-120">DependsOn</span></span>| <span data-ttu-id="5f515-121">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="5f515-121">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="5f515-122">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="5f515-122">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>

### <a name="getscript"></a><span data-ttu-id="5f515-123">GetScript</span><span class="sxs-lookup"><span data-stu-id="5f515-123">GetScript</span></span>

<span data-ttu-id="5f515-124">DSC nepoužívá výstup z `GetScript`.</span><span class="sxs-lookup"><span data-stu-id="5f515-124">DSC does not use the output from `GetScript`.</span></span> <span data-ttu-id="5f515-125">[Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) spustí rutinu `GetScript` načíst aktuální stav uzlu.</span><span class="sxs-lookup"><span data-stu-id="5f515-125">The [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) cmdlet executes the `GetScript` to retrieve a node's current state.</span></span> <span data-ttu-id="5f515-126">Návratová hodnota není zapotřebí ve směru z `GetScript`.</span><span class="sxs-lookup"><span data-stu-id="5f515-126">A return value is not required from `GetScript`.</span></span> <span data-ttu-id="5f515-127">Pokud zadáte návratovou hodnotu, musí být `hashtable` obsahující **výsledek** klíč, jehož hodnota je `String`.</span><span class="sxs-lookup"><span data-stu-id="5f515-127">If you specify a return value, it must be a `hashtable` containing a **Result** key whose value is a `String`.</span></span>

### <a name="testscript"></a><span data-ttu-id="5f515-128">TestScript</span><span class="sxs-lookup"><span data-stu-id="5f515-128">TestScript</span></span>

<span data-ttu-id="5f515-129">`TestScript` Provádí DSC k určení, zda `SetScript` by se měl spustit.</span><span class="sxs-lookup"><span data-stu-id="5f515-129">The `TestScript` is executed by DSC to determine if the `SetScript` should be run.</span></span> <span data-ttu-id="5f515-130">Pokud `TestScript` vrátí `$false`, provede DSC `SetScript` Chcete-li převést uzel zpět do požadovaného stavu.</span><span class="sxs-lookup"><span data-stu-id="5f515-130">If the `TestScript` returns `$false`, DSC executes the `SetScript` to bring the node back to the desired state.</span></span> <span data-ttu-id="5f515-131">Musí vrátit `boolean` hodnotu.</span><span class="sxs-lookup"><span data-stu-id="5f515-131">It must return a `boolean` value.</span></span> <span data-ttu-id="5f515-132">Výsledkem `$true` označuje, zda je uzel kompatibilní a `SetScript` by neměla provést.</span><span class="sxs-lookup"><span data-stu-id="5f515-132">A result of `$true` indicates that the node is compliant and `SetScript` should not executed.</span></span>

<span data-ttu-id="5f515-133">[Test-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Test-DscConfiguration) spustí rutinu `TestScript` načíst dodržování předpisů uzly s **skript** prostředky.</span><span class="sxs-lookup"><span data-stu-id="5f515-133">The [Test-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Test-DscConfiguration) cmdlet, executes the `TestScript` to retrieve the nodes compliance with the  **Script** resources.</span></span> <span data-ttu-id="5f515-134">V takovém případě však `SetScript` nespustí, bez ohledu na to, co `TestScript` blokovat vrátí.</span><span class="sxs-lookup"><span data-stu-id="5f515-134">However, in this case, the `SetScript` does not run, no matter what the `TestScript` block returns.</span></span>

> [!NOTE]
> <span data-ttu-id="5f515-135">Veškerý výstup z vaší `TestScript` je součástí jeho návratovou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="5f515-135">All output from your `TestScript` is part of its return value.</span></span> <span data-ttu-id="5f515-136">Prostředí PowerShell interpretuje nepotlačená výstup jako nenulová, což znamená, že vaše `TestScript` vrátí `$true` bez ohledu na stav vašeho uzlu.</span><span class="sxs-lookup"><span data-stu-id="5f515-136">PowerShell interprets unsuppressed output as non-zero, which means that your `TestScript` will return `$true` regardless of your node's state.</span></span>
> <span data-ttu-id="5f515-137">Výsledkem nepředvídatelné výsledky, počet falešně pozitivních výsledků a způsobí, že potíže při odstraňování problémů.</span><span class="sxs-lookup"><span data-stu-id="5f515-137">This results in unpredictable results, false positives, and causes difficulty during troubleshooting.</span></span>

### <a name="setscript"></a><span data-ttu-id="5f515-138">SetScript</span><span class="sxs-lookup"><span data-stu-id="5f515-138">SetScript</span></span>

<span data-ttu-id="5f515-139">`SetScript` Upraví uzel, který má enfore požadovaného stavu.</span><span class="sxs-lookup"><span data-stu-id="5f515-139">The `SetScript` modifies the node to enfore the desired state.</span></span> <span data-ttu-id="5f515-140">Je volána metodou DSC, pokud `TestScript` skript vrátí bloku `$false`.</span><span class="sxs-lookup"><span data-stu-id="5f515-140">It is called by DSC if the `TestScript` script block returns `$false`.</span></span> <span data-ttu-id="5f515-141">`SetScript` By měl mít žádnou návratovou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="5f515-141">The `SetScript` should have no return value.</span></span>

## <a name="examples"></a><span data-ttu-id="5f515-142">Příklady</span><span class="sxs-lookup"><span data-stu-id="5f515-142">Examples</span></span>

### <a name="example-1-write-sample-text-using-a-script-resource"></a><span data-ttu-id="5f515-143">Příklad 1: Zápis textu vzorku pomocí skriptu prostředků</span><span class="sxs-lookup"><span data-stu-id="5f515-143">Example 1: Write sample text using a Script resource</span></span>

<span data-ttu-id="5f515-144">V tomto příkladu ověřuje existenci `C:\TempFolder\TestFile.txt` na každém uzlu.</span><span class="sxs-lookup"><span data-stu-id="5f515-144">This example tests for the existence of `C:\TempFolder\TestFile.txt` on each node.</span></span> <span data-ttu-id="5f515-145">Pokud neexistuje, vytvoří pomocí `SetScript`.</span><span class="sxs-lookup"><span data-stu-id="5f515-145">If it does not exist, it creates it using the `SetScript`.</span></span> <span data-ttu-id="5f515-146">`GetScript` Vrátí obsah souboru a jeho návratovou hodnotu není používán.</span><span class="sxs-lookup"><span data-stu-id="5f515-146">The `GetScript` returns the contents of the file, and its return value is not used.</span></span>

```powershell
Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Node localhost
    {
        Script ScriptExample
        {
            SetScript = {
                $sw = New-Object System.IO.StreamWriter("C:\TempFolder\TestFile.txt")
                $sw.WriteLine("Some sample string")
                $sw.Close()
            }
            TestScript = { Test-Path "C:\TempFolder\TestFile.txt" }
            GetScript = { @{ Result = (Get-Content C:\TempFolder\TestFile.txt) } }
        }
    }
}
```

### <a name="example-2-compare-version-information-using-a-script-resource"></a><span data-ttu-id="5f515-147">Příklad 2: Porovnání informace o verzi použitím skriptu prostředků</span><span class="sxs-lookup"><span data-stu-id="5f515-147">Example 2: Compare version information using a Script resource</span></span>

<span data-ttu-id="5f515-148">Tento příklad načte *kompatibilní* informace o verzi z textového souboru na vývojovém počítači a uloží jej do `$version` proměnné.</span><span class="sxs-lookup"><span data-stu-id="5f515-148">This example retrieves the *compliant* version information from a text file on the authoring computer and stores it in the `$version` variable.</span></span> <span data-ttu-id="5f515-149">Při generování souboru MOF uzlu DSC nahradí `$using:version` blokovat proměnné do každého skriptu s hodnotou `$version` proměnné.</span><span class="sxs-lookup"><span data-stu-id="5f515-149">When generating the node's MOF file, DSC replaces the `$using:version` variables in each script block with the value of the `$version` variable.</span></span> <span data-ttu-id="5f515-150">Během provádění *kompatibilní* verze je uložený v textovém souboru na každém uzlu a porovnání a aktualizovat na další spuštění.</span><span class="sxs-lookup"><span data-stu-id="5f515-150">During execution, the *compliant* version is stored in a text file on each Node and compared and updated on subsequent executions.</span></span>

```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Node localhost
    {
        Script UpdateConfigurationVersion
        {
            GetScript = {
                $currentVersion = Get-Content (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
                return @{ 'Result' = "$currentVersion" }
            }
            TestScript = {
                # Create and invoke a scriptblock using the $GetScript automatic variable, which contains a string representation of the GetScript.
                $state = [scriptblock]::Create($GetScript).Invoke()

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
}
```