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
# <a name="portable-modules"></a>Přenosné moduly

Prostředí Windows PowerShell je určené pro [rozhraní .NET Framework][] při PowerShell Core je určené pro [.NET Core][]. Přenosné moduly jsou moduly, které fungují v prostředí Windows PowerShell a PowerShell Core. Rozhraní .NET Framework a .NET Core jsou vysoce kompatibilní, existují rozdíly v dostupných rozhraní API mezi nimi. Také nejsou k dispozici v prostředí Windows PowerShell a PowerShell Core rozdíly v rozhraních API. Moduly určena pro použití v obou prostředích musí mít na paměti tyto rozdíly.

## <a name="porting-an-existing-module"></a>Přenesení existující modul

### <a name="porting-a-pssnapin"></a>Portování PSSnapIn

Moduly Powershellu snapin (PSSnapIn) nejsou podporovány v prostředí PowerShell Core. Je však triviální pro převod PSSnapIn modul prostředí PowerShell. Obvykle je PSSnapIn registrační kód v jediném souboru třídy, která je odvozena z [PSSnapIn][]. Odebrat tento zdrojový soubor ze sestavení; už je nepotřebujete.

Použití [New-ModuleManifest][] vytvořit nový modul manifestu, který nahrazuje potřebu PSSnapIn registrační kód. Některé z hodnot z PSSnapIn (například popis) lze opětovně použít v rámci manifestu modulu.

`RootModule` Vlastnost v manifestu modulu musí být nastavena na název sestavení (dll) implementace rutiny.

### <a name="the-net-portability-analyzer-aka-apiport"></a>.NET Portability Analyzeru (neboli APIPort)

Na portu modulů napsaných pro prostředí Windows PowerShell pro práci s PowerShell Core, začněte s [.NET Portability Analyzeru][]. Tento nástroj spusťte proti vaší zkompilovaného sestavení k určení, zda jsou kompatibilní s rozhraní .NET Framework, .NET Core a ostatní moduly .NET runtime rozhraní .NET API používaná v modulu. Pokud existují, návrh nástroje alternativní rozhraní API. V opačném případě budete muset přidat [kontroly za běhu][] a omezit funkce není k dispozici v konkrétní moduly runtime.

## <a name="creating-a-new-module"></a>Vytváří se nový modul

Při vytváření nového modulu, doporučuje se použít [.NET CLI][].

### <a name="installing-the-powershell-standard-module-template"></a>Instalace šablony modulu prostředí PowerShell Standard

Po instalaci rozhraní příkazového řádku .NET je nainstalujte knihovny šablon pro generování jednoduchý modul prostředí PowerShell.
Modul bude kompatibilní s Windows Powershellu, prostředí PowerShell Core, Windows, Linux a macOS.

Následující příklad ukazuje, jak nainstalovat šablony:

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

### <a name="creating-a-new-module-project"></a>Vytvoření nového projektu modulu

Po instalaci šablony můžete vytvořit nový projekt modulu prostředí PowerShell pomocí této šablony. V tomto příkladu vzorový modul se nazývá "myModule".

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

### <a name="building-the-module"></a>Vytváření modulu

Standardní příkazy rozhraní příkazového řádku .NET použijte k sestavení projektu.

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

### <a name="testing-the-module"></a>V modulu testování

Po sestavení v modulu, můžete importovat ho a spusťte rutinu vzorku.

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

Následující části popisují podrobně některé z technologií používaných touto šablonou.

## <a name="net-standard-library"></a>Knihovna .NET standard

[.NET standard][] je formální specifikaci rozhraní API pro .NET, které jsou k dispozici ve všech implementace .NET. Spravovaného kódu, které cílí na .NET Standard pracuje s verzemi rozhraní .NET Framework a .NET Core, které jsou kompatibilní s touto verzí rozhraní .NET Standard.

> [!NOTE]
> Přestože rozhraní API můžou existovat v .NET Standard, může vyvolat implementace rozhraní API v .NET Core `PlatformNotSupportedException` za běhu, takže k ověření kompatibility s Windows Powershellem a PowerShell Core, nejlepším postupem je ke spuštění testů pro modul v obou prostředích.
> Pokud modul má být multiplatformní také Spusťte testy na Linuxu a macOS.

Cílení na .NET Standard pomáhá zajistit, že jak vyvíjí modul nekompatibilních rozhraní API není omylem představení do modulu. Nekompatibility jsou zjištěné v době kompilace místo modulu runtime.

Však není nutné, aby cílový .NET Standard pro modul pro práci s prostředí Windows PowerShell a PowerShell Core, za předpokladu, použijte kompatibilní rozhraní API. Intermediate Language (IL) není kompatibilní mezi dva moduly runtime. Můžete cílit rozhraní .NET Framework 4.6.1, které je kompatibilní s rozhraním .NET Standard 2.0. Pokud nepoužíváte rozhraní API mimo rozhraní .NET Standard 2.0, pak modul funguje pomocí prostředí PowerShell Core 6 bez opětovnou kompilaci.

## <a name="powershell-standard-library"></a>Prostředí PowerShell standardní knihovny

[Standardní prostředí PowerShell][] knihovna je formální specifikaci dostupný ve všech verzích Powershellu větší než nebo rovna verzi tohoto standardní rozhraní API Powershellu.

Například [standardní prostředí PowerShell 5.1][] je kompatibilní s Windows PowerShell 5.1 a Windows Powershellu 6.0 nebo novější.

Doporučujeme, abyste že kompilace modulu pomocí prostředí PowerShell standardní knihovny. Knihovny zajistí, že rozhraní API, jsou k dispozici a implementováno ve Windows Powershellu a PowerShell Core 6.
Standardní prostředí PowerShell má být vždy předává kompatibilní. Modul vytvořené pomocí prostředí PowerShell 5.1 standardní knihovny bude vždy kompatibilní s budoucí verze prostředí PowerShell.

## <a name="module-manifest"></a>Manifestu modulu

### <a name="indicating-compatibility-with-windows-powershell-and-powershell-core"></a>O kompatibilitě s Windows Powershellem a PowerShell Core

Po ověření, že používá modul prostředí Windows PowerShell a PowerShell Core manifestu modulu explicitně uvádět kompatibility s použitím [CompatiblePSEditions][] vlastnost. Hodnota `Desktop` znamená, že modul je kompatibilní s prostředím Windows PowerShell při hodnotu `Core` znamená, že modul je kompatibilní s PowerShell Core. Včetně `Desktop` a `Core` znamená, že modul je kompatibilní s Windows Powershellu a PowerShell Core.

> [!NOTE]
> `Core` neznamená automaticky, že modul je kompatibilní s Windows, Linux a macOS.
> **CompatiblePSEditions** vlastnost byla zavedena v prostředí PowerShell verze 5. Modul manifestů, které používají **CompatiblePSEditions** vlastnost nepodaří načíst v verze starší než verze 5 prostředí PowerShell.

### <a name="indicating-os-compatibility"></a>Označující Kompatibilita operačního systému

Nejprve ověřte, že modul funguje v Linuxu a macOS. V dalším kroku určit kompatibilitu s těmito operačními systémy v manifestu modulu. To usnadňuje uživatelům najít modul pro jejich operačního systému, pokud je publikovaná [Galerie prostředí PowerShell][].

V manifestu modulu `PrivateData` má vlastnost `PSData` dílčí vlastnosti. Volitelný `Tags` vlastnost `PSData` přijímá pole hodnot, které se zobrazí v galerii prostředí PowerShell. Galerie prostředí PowerShell podporuje následující hodnoty kompatibility:

| Značka               | Popis                                |
|-------------------|--------------------------------------------|
| PSEdition_Core    | Kompatibilní s PowerShell Core 6          |
| PSEdition_Desktop | Kompatibilní s prostředím Windows PowerShell         |
| Windows           | Kompatibilní s Windows                    |
| Linux             | Kompatibilní s Linuxem (žádné konkrétní distribuce) |
| macOS             | Kompatibilní s macOS                      |

Příklad:

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
[.NET core]: /dotnet/core/
[PSSnapIn]: /dotnet/api/system.management.automation.pssnapin
[New-ModuleManifest]: /powershell/module/microsoft.powershell.core/new-modulemanifest
[kontroly za běhu]: /dotnet/api/system.runtime.interopservices.runtimeinformation.frameworkdescription#System_Runtime_InteropServices_RuntimeInformation_FrameworkDescription
[.NET CLI]: /dotnet/core/tools/?tabs=netcore2x
[.NET standard]: /dotnet/standard/net-standard
[Standardní prostředí PowerShell]: https://github.com/PowerShell/PowerShellStandard
[Standardní prostředí PowerShell 5.1]: https://www.nuget.org/packages/PowerShellStandard.Library/5.1.0
[Galerie prostředí PowerShell]: https://www.powershellgallery.com
[.NET portability Analyzeru]: https://github.com/Microsoft/dotnet-apiport
[CompatiblePSEditions]: /powershell/gallery/concepts/module-psedition-support
