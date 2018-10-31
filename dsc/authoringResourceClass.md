---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Psaní vlastních prostředků DSC pomocí tříd Powershellu
ms.openlocfilehash: a8f08323f2cced8a17de4224bea94a54ba5ef0cd
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2018
ms.locfileid: "50226079"
---
# <a name="writing-a-custom-dsc-resource-with-powershell-classes"></a>Psaní vlastních prostředků DSC pomocí tříd Powershellu

> Platí pro: Windows PowerShell 5.0

Se zavedením tříd Powershellu ve Windows Powershellu 5.0 je možnost definovat prostředek DSC tak, že vytvoříte třídu. Třída definuje schéma a provádění prostředku, takže není nutné vytvořit samostatný soubor MOF. Struktura složek pro prostředek založené na třídě je také jednodušší, protože **DSCResources** složka není nezbytné.

V založené na třídě prostředků DSC schéma je definován jako vlastnosti třídy, která se dají upravovat pomocí atributů k určení typu vlastnosti... Prostředek je implementováno **Get()**, **Set()**, a **Test()** metody (odpovídá **Get-TargetResource**, **Set-TargetResource**, a **testovací TargetResource** funkcí ve skriptu prostředků.

V tomto tématu vytvoříme jednoduchou prostředek s názvem **FileResource** , který spravuje souboru v zadané cestě.

Další informace o prostředcích DSC najdete v tématu [vytvářet vlastní Windows PowerShell Desired State Configuration prostředky](authoringResource.md)

>**Poznámka:** nejsou podporovány obecné kolekce v založené na třídě prostředků.

## <a name="folder-structure-for-a-class-resource"></a>Struktura složek pro prostředek třídy

K implementaci vlastní prostředek DSC Powershellu Class, vytvořte následující strukturu složek. Je třída definovaná v **MyDscResource.psm1** a manifest modul je definované v **MyDscResource.psd1**.

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResource (folder)
        |- MyDscResource.psm1
           MyDscResource.psd1
```

## <a name="create-the-class"></a>Vytvoření třídy

Class – klíčové slovo použijete k vytvoření třídy prostředí PowerShell. Chcete-li určit, že třída je prostředek DSC, použijte **DscResource()** atribut. Název třídy je název prostředku DSC.

```powershell
[DscResource()]
class FileResource {
}
```

### <a name="declare-properties"></a>Deklarace vlastnosti

Schéma prostředků DSC je definován jako vlastnosti třídy. Můžeme deklarovat tři vlastnosti následujícím způsobem.

```powershell
[DscProperty(Key)]
[string]$Path

[DscProperty(Mandatory)]
[Ensure] $Ensure

[DscProperty(Mandatory)]
[string] $SourcePath

[DscProperty(NotConfigurable)]
[Nullable[datetime]] $CreationTime
```

Všimněte si, že jsou upraveny vlastnosti Description atributy. Význam atributy vypadá takto:

- **DscProperty(Key)**: vlastnost je povinný. Vlastnost je klíč. Hodnoty všech vlastností označený jako obsahující kombinaci kláves k jednoznačné identifikaci instance prostředku v rámci konfigurace.
- **DscProperty(Mandatory)**: vlastnost je povinný.
- **DscProperty(NotConfigurable)**: vlastnost je jen pro čtení. Vlastnosti označené tento atribut nemůže nastavit konfiguraci, ale jsou vyplněn **Get()** metodu, pokud je k dispozici.
- **DscProperty()**: vlastnost je možné konfigurovat, ale není nutné.

**$Path** a **$SourcePath** vlastnosti jsou obou řetězců. **$CreationTime** je [data a času](https://technet.microsoft.com/library/system.datetime.aspx) vlastnost. **$Ensure** vlastnost je typ výčtu, definovaná následujícím způsobem.

```powershell
enum Ensure
{
    Absent
    Present
}
```

### <a name="implementing-the-methods"></a>Implementace metody

**Get()**, **Set()**, a **Test()** metody jsou obdobou **Get-TargetResource**, **Set TargetResource** , a **testovací TargetResource** funkcí ve skriptu prostředků.

Tento kód také zahrnuje funkci CopyFile() pomocná funkce, která zkopíruje soubor z **$SourcePath** k **$Path**.

```powershell

    <#
        This method is equivalent of the Set-TargetResource script function.
        It sets the resource to the desired state.
    #>
    [void] Set()
    {
        $fileExists = $this.TestFilePath($this.Path)

        if ($this.ensure -eq [Ensure]::Present)
        {
            if(-not $fileExists)
            {
                $this.CopyFile()
            }
        }
        else
        {
            if ($fileExists)
            {
                Write-Verbose -Message "Deleting the file $($this.Path)"
                Remove-Item -LiteralPath $this.Path -Force
            }
        }
    }

    <#
        This method is equivalent of the Test-TargetResource script function.
        It should return True or False, showing whether the resource
        is in a desired state.
    #>
    [bool] Test()
    {
        $present = $this.TestFilePath($this.Path)

        if ($this.Ensure -eq [Ensure]::Present)
        {
            return $present
        }
        else
        {
            return -not $present
        }
    }

    <#
        This method is equivalent of the Get-TargetResource script function.
        The implementation should use the keys to find appropriate resources.
        This method returns an instance of this class with the updated key
         properties.
    #>
    [FileResource] Get()
    {
        $present = $this.TestFilePath($this.Path)

        if ($present)
        {
            $file = Get-ChildItem -LiteralPath $this.Path
            $this.CreationTime = $file.CreationTime
            $this.Ensure = [Ensure]::Present
        }
        else
        {
            $this.CreationTime = $null
            $this.Ensure = [Ensure]::Absent
        }

        return $this
    }

    <#
        Helper method to check if the file exists and it is file
    #>
    [bool] TestFilePath([string] $location)
    {
        $present = $true

        $item = Get-ChildItem -LiteralPath $location -ErrorAction Ignore

        if ($item -eq $null)
        {
            $present = $false
        }
        elseif ($item.PSProvider.Name -ne "FileSystem")
        {
            throw "Path $($location) is not a file path."
        }
        elseif ($item.PSIsContainer)
        {
            throw "Path $($location) is a directory path."
        }

        return $present
    }

    <#
        Helper method to copy file from source to path
    #>
    [void] CopyFile()
    {
        if (-not $this.TestFilePath($this.SourcePath))
        {
            throw "SourcePath $($this.SourcePath) is not found."
        }

        [System.IO.FileInfo] $destFileInfo = New-Object -TypeName System.IO.FileInfo($this.Path)

        if (-not $destFileInfo.Directory.Exists)
        {
            Write-Verbose -Message "Creating directory $($destFileInfo.Directory.FullName)"

            <#
                Use CreateDirectory instead of New-Item to avoid code
                to handle the non-terminating error
            #>
            [System.IO.Directory]::CreateDirectory($destFileInfo.Directory.FullName)
        }

        if (Test-Path -LiteralPath $this.Path -PathType Container)
        {
            throw "Path $($this.Path) is a directory path"
        }

        Write-Verbose -Message "Copying $($this.SourcePath) to $($this.Path)"

        # DSC engine catches and reports any error that occurs
        Copy-Item -LiteralPath $this.SourcePath -Destination $this.Path -Force
    }
```

### <a name="the-complete-file"></a>Celý
Následující soubor úplné třídy.

```powershell
enum Ensure
{
    Absent
    Present
}

<#
   This resource manages the file in a specific path.
   [DscResource()] indicates the class is a DSC resource
#>

[DscResource()]
class FileResource
{
    <#
       This property is the fully qualified path to the file that is
       expected to be present or absent.

       The [DscProperty(Key)] attribute indicates the property is a
       key and its value uniquely identifies a resource instance.
       Defining this attribute also means the property is required
       and DSC will ensure a value is set before calling the resource.

       A DSC resource must define at least one key property.
    #>
    [DscProperty(Key)]
    [string]$Path

    <#
        This property indicates if the settings should be present or absent
        on the system. For present, the resource ensures the file pointed
        to by $Path exists. For absent, it ensures the file point to by
        $Path does not exist.

        The [DscProperty(Mandatory)] attribute indicates the property is
        required and DSC will guarantee it is set.

        If Mandatory is not specified or if it is defined as
        Mandatory=$false, the value is not guaranteed to be set when DSC
        calls the resource.  This is appropriate for optional properties.
    #>
    [DscProperty(Mandatory)]
    [Ensure] $Ensure

    <#
       This property defines the fully qualified path to a file that will
       be placed on the system if $Ensure = Present and $Path does not
        exist.

       NOTE: This property is required because [DscProperty(Mandatory)] is
        set.
    #>
    [DscProperty(Mandatory)]
    [string] $SourcePath

    <#
       This property reports the file's create timestamp.

       [DscProperty(NotConfigurable)] attribute indicates the property is
       not configurable in DSC configuration.  Properties marked this way
       are populated by the Get() method to report additional details
       about the resource when it is present.

    #>
    [DscProperty(NotConfigurable)]
    [Nullable[datetime]] $CreationTime

    <#
        This method is equivalent of the Set-TargetResource script function.
        It sets the resource to the desired state.
    #>
    [void] Set()
    {
        $fileExists = $this.TestFilePath($this.Path)
        if ($this.ensure -eq [Ensure]::Present)
        {
            if (-not $fileExists)
            {
                $this.CopyFile()
            }
        }
        else
        {
            if ($fileExists)
            {
                Write-Verbose -Message "Deleting the file $($this.Path)"
                Remove-Item -LiteralPath $this.Path -Force
            }
        }
    }

    <#
        This method is equivalent of the Test-TargetResource script function.
        It should return True or False, showing whether the resource
        is in a desired state.
    #>
    [bool] Test()
    {
        $present = $this.TestFilePath($this.Path)

        if ($this.Ensure -eq [Ensure]::Present)
        {
            return $present
        }
        else
        {
            return -not $present
        }
    }

    <#
        This method is equivalent of the Get-TargetResource script function.
        The implementation should use the keys to find appropriate resources.
        This method returns an instance of this class with the updated key
         properties.
    #>
    [FileResource] Get()
    {
        $present = $this.TestFilePath($this.Path)

        if ($present)
        {
            $file = Get-ChildItem -LiteralPath $this.Path
            $this.CreationTime = $file.CreationTime
            $this.Ensure = [Ensure]::Present
        }
        else
        {
            $this.CreationTime = $null
            $this.Ensure = [Ensure]::Absent
        }

        return $this
    }

    <#
        Helper method to check if the file exists and it is file
    #>
    [bool] TestFilePath([string] $location)
    {
        $present = $true

        $item = Get-ChildItem -LiteralPath $location -ea Ignore
        if ($item -eq $null)
        {
            $present = $false
        }
        elseif ($item.PSProvider.Name -ne "FileSystem")
        {
            throw "Path $($location) is not a file path."
        }
        elseif ($item.PSIsContainer)
        {
            throw "Path $($location) is a directory path."
        }

        return $present
    }

    <#
        Helper method to copy file from source to path
    #>
    [void] CopyFile()
    {
        if (-not $this.TestFilePath($this.SourcePath))
        {
            throw "SourcePath $($this.SourcePath) is not found."
        }

        [System.IO.FileInfo] $destFileInfo = new-object System.IO.FileInfo($this.Path)
        if (-not $destFileInfo.Directory.Exists)
        {
            Write-Verbose -Message "Creating directory $($destFileInfo.Directory.FullName)"

            <#
                Use CreateDirectory instead of New-Item to avoid code
                 to handle the non-terminating error
            #>
            [System.IO.Directory]::CreateDirectory($destFileInfo.Directory.FullName)
        }

        if (Test-Path -LiteralPath $this.Path -PathType Container)
        {
            throw "Path $($this.Path) is a directory path"
        }

        Write-Verbose -Message "Copying $($this.SourcePath) to $($this.Path)"

        # DSC engine catches and reports any error that occurs
        Copy-Item -LiteralPath $this.SourcePath -Destination $this.Path -Force
    }
} # This module defines a class for a DSC "FileResource" provider.
```


## <a name="create-a-manifest"></a>Vytvoření manifestu

Chcete-li zpřístupnit prostředek založené na třídě modulu DSC, musíte zahrnout **DscResourcesToExport** prohlášení v souboru manifestu, který dává pokyn modul k exportu prostředku. Naše manifestu vypadá takto:

```powershell
@{

# Script module or binary module file associated with this manifest.
RootModule = 'MyDscResource.psm1'

DscResourcesToExport = 'FileResource'

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = '81624038-5e71-40f8-8905-b1a87afe22d7'

# Author of this module
Author = 'Microsoft Corporation'

# Company or vendor of this module
CompanyName = 'Microsoft Corporation'

# Copyright statement for this module
Copyright = '(c) 2014 Microsoft. All rights reserved.'

# Description of the functionality provided by this module
# Description = ''

# Minimum version of the Windows PowerShell engine required by this module
PowerShellVersion = '5.0'

# Name of the Windows PowerShell host required by this module
# PowerShellHostName = ''
}
```

## <a name="test-the-resource"></a>Testovací prostředek

Po uložení třídy a soubory manifestu ve struktuře složek, jak je popsáno výše, můžete vytvořit konfiguraci, která využívá nový prostředek. Informace o tom, jak spustit konfiguraci DSC, naleznete v tématu [přijetí konfigurace](enactingConfigurations.md). Následující konfigurace zkontroluje, jestli soubor v `c:\test\test.txt` existuje a pokud ne, zkopíruje soubor z `c:\test.txt` (byste měli vytvořit `c:\test.txt` předtím, než spustíte konfiguraci).

```powershell
Configuration Test
{
    Import-DSCResource -module MyDscResource
    FileResource file
    {
        Path = "C:\test\test.txt"
        SourcePath = "c:\test.txt"
        Ensure = "Present"
    }
}
Test
Start-DscConfiguration -Wait -Force Test
```

## <a name="supporting-psdscrunascredential"></a>Podpora PsDscRunAsCredential

>**Poznámka:** **PsDscRunAsCredential** je podporován v Powershellu 5.0 a novějším.

**PsDscRunAsCredential** vlastnost lze použít v [konfigurací DSC](configurations.md) prostředků bloku k určení, prostředku by měl být spuštěny pod zadanou sadu přihlašovacích údajů.
Další informace najdete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).

### <a name="require-or-disallow-psdscrunascredential-for-your-resource"></a>Povolení nebo zakázání PsDscRunAsCredential pro prostředek

**DscResource()** atribut přebírá volitelný parametr **RunAsCredential**.
Tento parametr má jednu ze tří hodnot:

- `Optional` **PsDscRunAsCredential** je volitelné konfigurace, které volají tento prostředek. Tato hodnota je výchozí.
- `Mandatory` **PsDscRunAsCredential** musí být použito pro všechny konfigurace, který volá tento prostředek.
- `NotSupported` Nelze použít konfigurace, které volají tento prostředek **PsDscRunAsCredential**.
- `Default` Stejné jako `Optional`.

Například následující atribut můžete zadat vlastní prostředek nepodporuje použití **PsDscRunAsCredential**:

```powershell
[DscResource(RunAsCredential=NotSupported)]
class FileResource {
}
```

### <a name="access-the-user-context"></a>Přístup k kontextu uživatele

Pro přístup k uživatelský kontext z v rámci vlastní prostředek, můžete použít automatické proměnné `$global:PsDscContext`.

Například následující kód by zápisu uživatelský kontext, ve kterém prostředek běží podrobné výstupního datového proudu:

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $global:PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a>Viz také
### <a name="concepts"></a>Koncepty
[Vlastní Windows PowerShell Desired State Configuration prostředky sestavení](authoringResource.md)