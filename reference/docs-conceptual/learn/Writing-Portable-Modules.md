---
ms.date: 12/14/2018
keywords: rutiny prostředí PowerShell
title: Vytváření přenosných moduly
ms.openlocfilehash: 38a93b5b030d58784b91292e2cd060b3a2c19a00
ms.sourcegitcommit: d396d0e4cfe3d279f399c17e7337380a31d373ac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/21/2018
ms.locfileid: "53747717"
---
# <a name="portable-modules"></a><span data-ttu-id="83d52-103">Přenosné moduly</span><span class="sxs-lookup"><span data-stu-id="83d52-103">Portable Modules</span></span>

<span data-ttu-id="83d52-104">Prostředí Windows PowerShell je určené pro [rozhraní .NET Framework][] při PowerShell Core je určené pro [.NET Core][].</span><span class="sxs-lookup"><span data-stu-id="83d52-104">Windows PowerShell is written for [.NET Framework][] while PowerShell Core is written for [.NET Core][].</span></span> <span data-ttu-id="83d52-105">Přenosné moduly jsou moduly, které fungují v prostředí Windows PowerShell a PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="83d52-105">Portable modules are modules that work in both Windows PowerShell and PowerShell Core.</span></span> <span data-ttu-id="83d52-106">Rozhraní .NET Framework a .NET Core jsou vysoce kompatibilní, existují rozdíly v dostupných rozhraní API mezi nimi.</span><span class="sxs-lookup"><span data-stu-id="83d52-106">While .NET Framework and .NET Core are highly compatible, there are differences in the available APIs between the two.</span></span> <span data-ttu-id="83d52-107">Také nejsou k dispozici v prostředí Windows PowerShell a PowerShell Core rozdíly v rozhraních API.</span><span class="sxs-lookup"><span data-stu-id="83d52-107">There are also differences in the APIs available in Windows PowerShell and PowerShell Core.</span></span> <span data-ttu-id="83d52-108">Moduly určena pro použití v obou prostředích musí mít na paměti tyto rozdíly.</span><span class="sxs-lookup"><span data-stu-id="83d52-108">Modules intended to be used in both environments need to be aware of these differences.</span></span>

## <a name="porting-an-existing-module"></a><span data-ttu-id="83d52-109">Přenesení existující modul</span><span class="sxs-lookup"><span data-stu-id="83d52-109">Porting an Existing Module</span></span>

### <a name="porting-a-pssnapin"></a><span data-ttu-id="83d52-110">Portování PSSnapIn</span><span class="sxs-lookup"><span data-stu-id="83d52-110">Porting a PSSnapIn</span></span>

<span data-ttu-id="83d52-111">Moduly Powershellu snapin (PSSnapIn) nejsou podporovány v prostředí PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="83d52-111">PowerShell SnapIns (PSSnapIn) aren't supported in PowerShell Core.</span></span> <span data-ttu-id="83d52-112">Je však triviální pro převod PSSnapIn modul prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83d52-112">However, it's trivial to convert a PSSnapIn to a PowerShell module.</span></span> <span data-ttu-id="83d52-113">Obvykle je PSSnapIn registrační kód v jediném souboru třídy, která je odvozena z [PSSnapIn][].</span><span class="sxs-lookup"><span data-stu-id="83d52-113">Typically, the PSSnapIn registration code is in a single source file of a class that derives from [PSSnapIn][].</span></span> <span data-ttu-id="83d52-114">Odebrat tento zdrojový soubor ze sestavení; už je nepotřebujete.</span><span class="sxs-lookup"><span data-stu-id="83d52-114">Remove this source file from the build; it's no longer needed.</span></span>

<span data-ttu-id="83d52-115">Použití [New-ModuleManifest][] vytvořit nový modul manifestu, který nahrazuje potřebu PSSnapIn registrační kód.</span><span class="sxs-lookup"><span data-stu-id="83d52-115">Use [New-ModuleManifest][] to create a new module manifest that replaces the need for the PSSnapIn registration code.</span></span> <span data-ttu-id="83d52-116">Některé z hodnot z PSSnapIn (například popis) lze opětovně použít v rámci manifestu modulu.</span><span class="sxs-lookup"><span data-stu-id="83d52-116">Some of the values from the PSSnapIn (such as Description) can be reused within the module manifest.</span></span>

<span data-ttu-id="83d52-117">`RootModule` Vlastnost v manifestu modulu musí být nastavena na název sestavení (dll) implementace rutiny.</span><span class="sxs-lookup"><span data-stu-id="83d52-117">The `RootModule` property in the module manifest should be set to the name of the assembly (dll) implementing the cmdlets.</span></span>

### <a name="the-net-portability-analyzer-aka-apiport"></a><span data-ttu-id="83d52-118">.NET Portability Analyzeru (neboli APIPort)</span><span class="sxs-lookup"><span data-stu-id="83d52-118">The .NET Portability Analyzer (aka APIPort)</span></span>

<span data-ttu-id="83d52-119">Na portu modulů napsaných pro prostředí Windows PowerShell pro práci s PowerShell Core, začněte s [.NET Portability Analyzeru][].</span><span class="sxs-lookup"><span data-stu-id="83d52-119">To port modules written for Windows PowerShell to work with PowerShell Core, start with the [.NET Portability Analyzer][].</span></span> <span data-ttu-id="83d52-120">Tento nástroj spusťte proti vaší zkompilovaného sestavení k určení, zda jsou kompatibilní s rozhraní .NET Framework, .NET Core a ostatní moduly .NET runtime rozhraní .NET API používaná v modulu.</span><span class="sxs-lookup"><span data-stu-id="83d52-120">Run this tool against your compiled assembly to determine if the .NET APIs used in the module are compatible with .NET Framework, .NET Core, and other .NET runtimes.</span></span> <span data-ttu-id="83d52-121">Pokud existují, návrh nástroje alternativní rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="83d52-121">The tool suggests alternate APIs if they exist.</span></span> <span data-ttu-id="83d52-122">V opačném případě budete muset přidat [kontroly za běhu][] a omezit funkce není k dispozici v konkrétní moduly runtime.</span><span class="sxs-lookup"><span data-stu-id="83d52-122">Otherwise, you may need to add [runtime checks][] and restrict capabilities not available in specific runtimes.</span></span>

## <a name="creating-a-new-module"></a><span data-ttu-id="83d52-123">Vytváří se nový modul</span><span class="sxs-lookup"><span data-stu-id="83d52-123">Creating a New Module</span></span>

<span data-ttu-id="83d52-124">Při vytváření nového modulu, doporučuje se použít [.NET CLI][].</span><span class="sxs-lookup"><span data-stu-id="83d52-124">If creating a new module, the recommendation is to use the [.NET CLI][].</span></span>

### <a name="installing-the-powershell-standard-module-template"></a><span data-ttu-id="83d52-125">Instalace šablony modulu prostředí PowerShell Standard</span><span class="sxs-lookup"><span data-stu-id="83d52-125">Installing the PowerShell Standard Module Template</span></span>

<span data-ttu-id="83d52-126">Po instalaci rozhraní příkazového řádku .NET je nainstalujte knihovny šablon pro generování jednoduchý modul prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83d52-126">Once the .NET CLI is installed, install a template library to generate a simple PowerShell module.</span></span>
<span data-ttu-id="83d52-127">Modul bude kompatibilní s Windows Powershellu, prostředí PowerShell Core, Windows, Linux a macOS.</span><span class="sxs-lookup"><span data-stu-id="83d52-127">The module will be compatible with Windows PowerShell, PowerShell Core, Windows, Linux, and macOS.</span></span>

<span data-ttu-id="83d52-128">Následující příklad ukazuje, jak nainstalovat šablony:</span><span class="sxs-lookup"><span data-stu-id="83d52-128">The following example shows how to install the template:</span></span>

```powershell
dotnet new -i Microsoft.PowerShell.Standard.Module.Template
```

```output
  Restoring packages for C:\Users\Steve\.templateengine\dotnetcli\v2.1.302\scratch\restore.csproj...
  Installing Microsoft.PowerShell.Standard.Module.Template 0.1.3.
  Generating MSBuild file C:\Users\Steve\.templateengine\dotnetcli\v2.1.302\scratch\obj\restore.csproj.nuget.g.props.
  Generating MSBuild file C:\Users\Steve\.templateengine\dotnetcli\v2.1.302\scratch\obj\restore.csproj.nuget.g.targets.
  Restore completed in 1.66 sec for C:\Users\Steve\.templateengine\dotnetcli\v2.1.302\scratch\restore.csproj.

Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.
  -n, --name          The name for the output being created. If no name is specified, the name of the current directory is used.
  -o, --output        Location to place the generated output.
  -i, --install       Installs a source or a template pack.
  -u, --uninstall     Uninstalls a source or a template pack.
  --nuget-source      Specifies a NuGet source to use during install.
  --type              Filters templates based on available types. Predefined values are "project", "item" or "other".
  --force             Forces content to be generated even if it would change existing files.
  -lang, --language   Filters templates based on language and specifies the language of the template to create.


Templates                                         Short Name         Language          Tags
----------------------------------------------------------------------------------------------------------------------------
Console Application                               console            [C#], F#, VB      Common/Console
Class library                                     classlib           [C#], F#, VB      Common/Library
PowerShell Standard Module                        psmodule           [C#]              Library/PowerShell/Module
...
```

### <a name="creating-a-new-module-project"></a><span data-ttu-id="83d52-129">Vytvoření nového projektu modulu</span><span class="sxs-lookup"><span data-stu-id="83d52-129">Creating a New Module Project</span></span>

<span data-ttu-id="83d52-130">Po instalaci šablony můžete vytvořit nový projekt modulu prostředí PowerShell pomocí této šablony.</span><span class="sxs-lookup"><span data-stu-id="83d52-130">After the template is installed, you can create a new PowerShell module project using that template.</span></span> <span data-ttu-id="83d52-131">V tomto příkladu vzorový modul se nazývá "myModule".</span><span class="sxs-lookup"><span data-stu-id="83d52-131">In this example, the sample module is called 'myModule'.</span></span>

```
PS> mkdir myModule

    Directory: C:\Users\Steve

Mode LastWriteTime Length Name
---- ------------- ------ ----
d----- 8/3/2018 2:41 PM myModule

PS> cd myModule
PS C:\Users\Steve\myModule> dotnet new psmodule

The template "PowerShell Standard Module" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on C:\Users\Steve\myModule\myModule.csproj...
  Restoring packages for C:\Users\Steve\myModule\myModule.csproj...
  Installing PowerShellStandard.Library 5.1.0.
  Generating MSBuild file C:\Users\Steve\myModule\obj\myModule.csproj.nuget.g.props.
  Generating MSBuild file C:\Users\Steve\myModule\obj\myModule.csproj.nuget.g.targets.
  Restore completed in 1.76 sec for C:\Users\Steve\myModule\myModule.csproj.

Restore succeeded.
```

### <a name="building-the-module"></a><span data-ttu-id="83d52-132">Vytváření modulu</span><span class="sxs-lookup"><span data-stu-id="83d52-132">Building the Module</span></span>

<span data-ttu-id="83d52-133">Standardní příkazy rozhraní příkazového řádku .NET použijte k sestavení projektu.</span><span class="sxs-lookup"><span data-stu-id="83d52-133">Use standard .NET CLI commands to build the project.</span></span>

```powershell
dotnet build
```

```output
PS C:\Users\Steve\myModule> dotnet build
Microsoft (R) Build Engine version 15.7.179.6572 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 76.85 ms for C:\Users\Steve\myModule\myModule.csproj.
  myModule -> C:\Users\Steve\myModule\bin\Debug\netstandard2.0\myModule.dll

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:05.40
```

### <a name="testing-the-module"></a><span data-ttu-id="83d52-134">V modulu testování</span><span class="sxs-lookup"><span data-stu-id="83d52-134">Testing the Module</span></span>

<span data-ttu-id="83d52-135">Po sestavení v modulu, můžete importovat ho a spusťte rutinu vzorku.</span><span class="sxs-lookup"><span data-stu-id="83d52-135">After building the module, you can import it and execute the sample cmdlet.</span></span>

```powershell
ipmo .\bin\Debug\netstandard2.0\myModule.dll
Test-SampleCmdlet -?
Test-SampleCmdlet -FavoriteNumber 7 -FavoritePet Cat
```

```output
PS C:\Users\Steve\myModule> ipmo .\bin\Debug\netstandard2.0\myModule.dll
PS C:\Users\Steve\myModule> Test-SampleCmdlet -?

NAME
    Test-SampleCmdlet

SYNTAX
    Test-SampleCmdlet [-FavoriteNumber] <int> [[-FavoritePet] {Cat | Dog | Horse}] [<CommonParameters>]


ALIASES
    None


REMARKS
    None


PS C:\Users\Steve\myModule> Test-SampleCmdlet -FavoriteNumber 7 -FavoritePet Cat

FavoriteNumber FavoritePet
-------------- -----------
             7 Cat
```

<span data-ttu-id="83d52-136">Následující části popisují podrobně některé z technologií používaných touto šablonou.</span><span class="sxs-lookup"><span data-stu-id="83d52-136">The following sections describe in detail some of the technologies used by this template.</span></span>

## <a name="net-standard-library"></a><span data-ttu-id="83d52-137">Knihovna .NET standard</span><span class="sxs-lookup"><span data-stu-id="83d52-137">.NET Standard Library</span></span>

<span data-ttu-id="83d52-138">[.NET standard][] je formální specifikaci rozhraní API pro .NET, které jsou k dispozici ve všech implementace .NET.</span><span class="sxs-lookup"><span data-stu-id="83d52-138">[.NET Standard][] is a formal specification of .NET APIs that are available in all .NET implementations.</span></span> <span data-ttu-id="83d52-139">Spravovaného kódu, které cílí na .NET Standard pracuje s verzemi rozhraní .NET Framework a .NET Core, které jsou kompatibilní s touto verzí rozhraní .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="83d52-139">Managed code targeting .NET Standard works with the .NET Framework and .NET Core versions that are compatible with that version of the .NET Standard.</span></span>

> [!NOTE]
> <span data-ttu-id="83d52-140">Přestože rozhraní API můžou existovat v .NET Standard, může vyvolat implementace rozhraní API v .NET Core `PlatformNotSupportedException` za běhu, takže k ověření kompatibility s Windows Powershellem a PowerShell Core, nejlepším postupem je ke spuštění testů pro modul v obou prostředích.</span><span class="sxs-lookup"><span data-stu-id="83d52-140">Although an API may exist in .NET Standard, the API implementation in .NET Core may throw a `PlatformNotSupportedException` at runtime, so to verify compatibility with Windows PowerShell and PowerShell Core, the best practice is to run tests for your module within both environments.</span></span>
> <span data-ttu-id="83d52-141">Pokud modul má být multiplatformní také Spusťte testy na Linuxu a macOS.</span><span class="sxs-lookup"><span data-stu-id="83d52-141">Also run tests on Linux and macOS if your module is intended to be cross-platform.</span></span>

<span data-ttu-id="83d52-142">Cílení na .NET Standard pomáhá zajistit, že jak vyvíjí modul nekompatibilních rozhraní API není omylem představení do modulu.</span><span class="sxs-lookup"><span data-stu-id="83d52-142">Targeting .NET Standard helps ensure that, as the module evolves, incompatible APIs don't accidentally get introduced into the module.</span></span> <span data-ttu-id="83d52-143">Nekompatibility jsou zjištěné v době kompilace místo modulu runtime.</span><span class="sxs-lookup"><span data-stu-id="83d52-143">Incompatibilities are discovered at compile time instead of runtime.</span></span>

<span data-ttu-id="83d52-144">Však není nutné, aby cílový .NET Standard pro modul pro práci s prostředí Windows PowerShell a PowerShell Core, za předpokladu, použijte kompatibilní rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="83d52-144">However, it isn't required to target .NET Standard for a module to work with both Windows PowerShell and PowerShell Core, as long as you use compatible APIs.</span></span> <span data-ttu-id="83d52-145">Intermediate Language (IL) není kompatibilní mezi dva moduly runtime.</span><span class="sxs-lookup"><span data-stu-id="83d52-145">The Intermediate Language (IL) is compatible between the two runtimes.</span></span> <span data-ttu-id="83d52-146">Můžete cílit rozhraní .NET Framework 4.6.1, které je kompatibilní s rozhraním .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="83d52-146">You can target .NET Framework 4.6.1, which is compatible with .NET Standard 2.0.</span></span> <span data-ttu-id="83d52-147">Pokud nepoužíváte rozhraní API mimo rozhraní .NET Standard 2.0, pak modul funguje pomocí prostředí PowerShell Core 6 bez opětovnou kompilaci.</span><span class="sxs-lookup"><span data-stu-id="83d52-147">If you don't use APIs outside of .NET Standard 2.0, then your module works with PowerShell Core 6 without recompilation.</span></span>

## <a name="powershell-standard-library"></a><span data-ttu-id="83d52-148">Prostředí PowerShell standardní knihovny</span><span class="sxs-lookup"><span data-stu-id="83d52-148">PowerShell Standard Library</span></span>

<span data-ttu-id="83d52-149">[Standardní prostředí PowerShell][] knihovna je formální specifikaci dostupný ve všech verzích Powershellu větší než nebo rovna verzi tohoto standardní rozhraní API Powershellu.</span><span class="sxs-lookup"><span data-stu-id="83d52-149">The [PowerShell Standard][] library is a formal specification of PowerShell APIs available in all PowerShell versions greater than or equal to the version of that standard.</span></span>

<span data-ttu-id="83d52-150">Například [standardní prostředí PowerShell 5.1][] je kompatibilní s Windows PowerShell 5.1 a Windows Powershellu 6.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="83d52-150">For example, [PowerShell Standard 5.1][] is compatible with both Windows PowerShell 5.1 and PowerShell Core 6.0 or newer.</span></span>

<span data-ttu-id="83d52-151">Doporučujeme, abyste že kompilace modulu pomocí prostředí PowerShell standardní knihovny.</span><span class="sxs-lookup"><span data-stu-id="83d52-151">We recommend you compile your module using PowerShell Standard Library.</span></span> <span data-ttu-id="83d52-152">Knihovny zajistí, že rozhraní API, jsou k dispozici a implementováno ve Windows Powershellu a PowerShell Core 6.</span><span class="sxs-lookup"><span data-stu-id="83d52-152">The library ensures the APIs are available and implemented in both Windows PowerShell and PowerShell Core 6.</span></span>
<span data-ttu-id="83d52-153">Standardní prostředí PowerShell má být vždy předává kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="83d52-153">PowerShell Standard is intended to always be forwards-compatible.</span></span> <span data-ttu-id="83d52-154">Modul vytvořené pomocí prostředí PowerShell 5.1 standardní knihovny bude vždy kompatibilní s budoucí verze prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83d52-154">A module built using PowerShell Standard Library 5.1 will always be compatible with future versions of PowerShell.</span></span>

## <a name="module-manifest"></a><span data-ttu-id="83d52-155">Manifestu modulu</span><span class="sxs-lookup"><span data-stu-id="83d52-155">Module Manifest</span></span>

### <a name="indicating-compatibility-with-windows-powershell-and-powershell-core"></a><span data-ttu-id="83d52-156">O kompatibilitě s Windows Powershellem a PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="83d52-156">Indicating Compatibility With Windows PowerShell and PowerShell Core</span></span>

<span data-ttu-id="83d52-157">Po ověření, že používá modul prostředí Windows PowerShell a PowerShell Core manifestu modulu explicitně uvádět kompatibility s použitím [CompatiblePSEditions][] vlastnost.</span><span class="sxs-lookup"><span data-stu-id="83d52-157">After validating that your module works with both Windows PowerShell and PowerShell Core, the module manifest should explicitly indicate compatibility by using the [CompatiblePSEditions][] property.</span></span> <span data-ttu-id="83d52-158">Hodnota `Desktop` znamená, že modul je kompatibilní s prostředím Windows PowerShell při hodnotu `Core` znamená, že modul je kompatibilní s PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="83d52-158">A value of `Desktop` means that the module is compatible with Windows PowerShell, while a value of `Core` means that the module is compatible with PowerShell Core.</span></span> <span data-ttu-id="83d52-159">Včetně `Desktop` a `Core` znamená, že modul je kompatibilní s Windows Powershellu a PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="83d52-159">Including both `Desktop` and `Core` means that the module is compatible with both Windows PowerShell and PowerShell Core.</span></span>

> [!NOTE]
> <span data-ttu-id="83d52-160">`Core` neznamená automaticky, že modul je kompatibilní s Windows, Linux a macOS.</span><span class="sxs-lookup"><span data-stu-id="83d52-160">`Core` does not automatically mean that the module is compatible with Windows, Linux, and macOS.</span></span>
> <span data-ttu-id="83d52-161">**CompatiblePSEditions** vlastnost byla zavedena v prostředí PowerShell verze 5.</span><span class="sxs-lookup"><span data-stu-id="83d52-161">The **CompatiblePSEditions** property was introduced in PowerShell v5.</span></span> <span data-ttu-id="83d52-162">Modul manifestů, které používají **CompatiblePSEditions** vlastnost nepodaří načíst v verze starší než verze 5 prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83d52-162">Module manifests that use the **CompatiblePSEditions** property fail to load in versions prior to PowerShell v5.</span></span>

### <a name="indicating-os-compatibility"></a><span data-ttu-id="83d52-163">Označující Kompatibilita operačního systému</span><span class="sxs-lookup"><span data-stu-id="83d52-163">Indicating OS Compatibility</span></span>

<span data-ttu-id="83d52-164">Nejprve ověřte, že modul funguje v Linuxu a macOS.</span><span class="sxs-lookup"><span data-stu-id="83d52-164">First, validate that your module works on Linux and macOS.</span></span> <span data-ttu-id="83d52-165">V dalším kroku určit kompatibilitu s těmito operačními systémy v manifestu modulu.</span><span class="sxs-lookup"><span data-stu-id="83d52-165">Next, indicate compatibility with those operating systems in the module manifest.</span></span> <span data-ttu-id="83d52-166">To usnadňuje uživatelům najít modul pro jejich operačního systému, pokud je publikovaná [Galerie prostředí PowerShell][].</span><span class="sxs-lookup"><span data-stu-id="83d52-166">This makes it easier for users to find your module for their operating system when published to the [PowerShell Gallery][].</span></span>

<span data-ttu-id="83d52-167">V manifestu modulu `PrivateData` má vlastnost `PSData` dílčí vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="83d52-167">Within the module manifest, the `PrivateData` property has a `PSData` sub-property.</span></span> <span data-ttu-id="83d52-168">Volitelný `Tags` vlastnost `PSData` přijímá pole hodnot, které se zobrazí v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83d52-168">The optional `Tags` property of `PSData` takes an array of values that show up in PowerShell Gallery.</span></span> <span data-ttu-id="83d52-169">Galerie prostředí PowerShell podporuje následující hodnoty kompatibility:</span><span class="sxs-lookup"><span data-stu-id="83d52-169">The PowerShell Gallery supports the following compatibility values:</span></span>

| <span data-ttu-id="83d52-170">Značka</span><span class="sxs-lookup"><span data-stu-id="83d52-170">Tag</span></span>               | <span data-ttu-id="83d52-171">Popis</span><span class="sxs-lookup"><span data-stu-id="83d52-171">Description</span></span>                                |
|-------------------|--------------------------------------------|
| <span data-ttu-id="83d52-172">PSEdition_Core</span><span class="sxs-lookup"><span data-stu-id="83d52-172">PSEdition_Core</span></span>    | <span data-ttu-id="83d52-173">Kompatibilní s PowerShell Core 6</span><span class="sxs-lookup"><span data-stu-id="83d52-173">Compatible with PowerShell Core 6</span></span>          |
| <span data-ttu-id="83d52-174">PSEdition_Desktop</span><span class="sxs-lookup"><span data-stu-id="83d52-174">PSEdition_Desktop</span></span> | <span data-ttu-id="83d52-175">Kompatibilní s prostředím Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="83d52-175">Compatible with Windows PowerShell</span></span>         |
| <span data-ttu-id="83d52-176">Windows</span><span class="sxs-lookup"><span data-stu-id="83d52-176">Windows</span></span>           | <span data-ttu-id="83d52-177">Kompatibilní s Windows</span><span class="sxs-lookup"><span data-stu-id="83d52-177">Compatible with Windows</span></span>                    |
| <span data-ttu-id="83d52-178">Linux</span><span class="sxs-lookup"><span data-stu-id="83d52-178">Linux</span></span>             | <span data-ttu-id="83d52-179">Kompatibilní s Linuxem (žádné konkrétní distribuce)</span><span class="sxs-lookup"><span data-stu-id="83d52-179">Compatible with Linux (no specific distro)</span></span> |
| <span data-ttu-id="83d52-180">macOS</span><span class="sxs-lookup"><span data-stu-id="83d52-180">macOS</span></span>             | <span data-ttu-id="83d52-181">Kompatibilní s macOS</span><span class="sxs-lookup"><span data-stu-id="83d52-181">Compatible with macOS</span></span>                      |

<span data-ttu-id="83d52-182">Příklad:</span><span class="sxs-lookup"><span data-stu-id="83d52-182">Example:</span></span>

```powershell
@{
    GUID = "4ae9fd46-338a-459c-8186-07f910774cb8"
    Author = "Microsoft Corporation"
    CompanyName = "Microsoft Corporation"
    Copyright = "(C) Microsoft Corporation. All rights reserved."
    HelpInfoUri = "https://go.microsoft.com/fwlink/?linkid=855962"
    ModuleVersion = "1.2.4"
    PowerShellVersion = "3.0"
    ClrVersion = "4.0"
    RootModule = "PackageManagement.psm1"
    Description = 'PackageManagement (a.k.a. OneGet) is a new way to discover and install software packages from around the web.
 It is a manager or multiplexer of existing package managers (also called package providers) that unifies Windows package management with a single Windows PowerShell interface. With PackageManagement, you can do the following.
  - Manage a list of software repositories in which packages can be searched, acquired and installed
  - Discover software packages
  - Seamlessly install, uninstall, and inventory packages from one or more software repositories'

    CmdletsToExport = @(
        'Find-Package',
        'Get-Package',
        'Get-PackageProvider',
        'Get-PackageSource',
        'Install-Package',
        'Import-PackageProvider'
        'Find-PackageProvider'
        'Install-PackageProvider'
        'Register-PackageSource',
        'Set-PackageSource',
        'Unregister-PackageSource',
        'Uninstall-Package'
        'Save-Package'
    )

    FormatsToProcess  = @('PackageManagement.format.ps1xml')

    PrivateData = @{
        PSData = @{
            Tags = @('PackageManagement', 'PSEdition_Core', 'PSEdition_Desktop', 'Windows', 'Linux', 'macOS')
            ProjectUri = 'https://oneget.org'
        }
    }
}
```

<!-- reference links -->
[Rozhraní .NET framework]: /dotnet/framework/
[.NET Framework]: /dotnet/framework/
[.NET core]: /dotnet/core/
[.NET Core]: /dotnet/core/
[PSSnapIn]: /dotnet/api/system.management.automation.pssnapin
[New-ModuleManifest]: /powershell/module/microsoft.powershell.core/new-modulemanifest
[kontroly za běhu]: /dotnet/api/system.runtime.interopservices.runtimeinformation.frameworkdescription#System_Runtime_InteropServices_RuntimeInformation_FrameworkDescription
[runtime checks]: /dotnet/api/system.runtime.interopservices.runtimeinformation.frameworkdescription#System_Runtime_InteropServices_RuntimeInformation_FrameworkDescription
[.NET CLI]: /dotnet/core/tools/?tabs=netcore2x
[.NET standard]: /dotnet/standard/net-standard
[.NET Standard]: /dotnet/standard/net-standard
[Standardní prostředí PowerShell]: https://github.com/PowerShell/PowerShellStandard
[PowerShell Standard]: https://github.com/PowerShell/PowerShellStandard
[Standardní prostředí PowerShell 5.1]: https://www.nuget.org/packages/PowerShellStandard.Library/5.1.0
[PowerShell Standard 5.1]: https://www.nuget.org/packages/PowerShellStandard.Library/5.1.0
[Galerie prostředí PowerShell]: https://www.powershellgallery.com
[PowerShell Gallery]: https://www.powershellgallery.com
[.NET portability Analyzeru]: https://github.com/Microsoft/dotnet-apiport
[.NET Portability Analyzer]: https://github.com/Microsoft/dotnet-apiport
[CompatiblePSEditions]: /powershell/gallery/concepts/module-psedition-support