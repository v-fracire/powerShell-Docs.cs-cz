---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Psaní vlastních prostředků DSC s třídami, prostředí PowerShell
ms.openlocfilehash: f2500bfb41302cbeaf3cb9d23b843f26f01c1d5b
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189461"
---
# <a name="writing-a-custom-dsc-resource-with-powershell-classes"></a>Psaní vlastních prostředků DSC s třídami, prostředí PowerShell

> Platí pro: Windows prostředí Windows PowerShell 5.0

Se zavedením prostředí PowerShell tříd v prostředí Windows PowerShell 5.0 můžete teď určit prostředek DSC vytvořením třídy. Třída definuje schéma a provádění prostředku, takže není nutné vytvořit samostatný soubor MOF. Struktura složek na základě třídy prostředku je také jednodušší, protože **DSCResources** složka není nezbytné.

V prostředek DSC založené na třídě schématu je definován jako vlastnosti třídy, které lze upravit atributy pro určení typu vlastnost... Prostředek je implementováno modulem **Get()**, **Set()**, a **Test()** metody (ekvivalentní **Get-TargetResource**, **Set-TargetResource**, a **Test TargetResource** funkcí v zdroje skriptu.

V tomto tématu, vytvoříme jednoduchý prostředek s názvem **FileResource** , spravuje soubor v zadané cestě.

Další informace o prostředcích DSC najdete v tématu [sestavení vlastní Windows PowerShell požadovaného stavu konfigurace prostředků](authoringResource.md)

>**Poznámka:** obecné kolekce nepodporuje prostředky založené na třídě.

## <a name="folder-structure-for-a-class-resource"></a>Struktura složek pro prostředek – třída

Chcete-li implementovat vlastní prostředek DSC s třídou prostředí PowerShell, vytvořte následující strukturu složek. Je třída definovaná v **MyDscResource.psm1** a manifestu modulu je definována v **MyDscResource.psd1**.

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResource (folder)
        |- MyDscResource.psm1
           MyDscResource.psd1
```

## <a name="create-the-class"></a>Vytvoření třídy

Class – klíčové slovo použijete pro vytvoření třídy prostředí PowerShell. Chcete-li určit, že třída je prostředek DSC, použijte **DscResource()** atribut. Název třídy je název prostředek DSC.

```powershell
[DscResource()]
class FileResource {
}
```

### <a name="declare-properties"></a>Deklarování vlastností

Schéma prostředků DSC je definován jako vlastnosti třídy. Jsme deklarovat tři vlastnosti následujícím způsobem.

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

Všimněte si, že jsou upraveny vlastnosti podle atributů. Význam atributy vypadá takto:

- **DscProperty(Key)**: vlastnost se vyžaduje. Vlastnost je klíč. Hodnoty všech vlastností označené jako klíče musí zkombinovat k jednoznačné identifikaci instance prostředku v rámci konfigurace.
- **DscProperty(Mandatory)**: vlastnost se vyžaduje.
- **DscProperty(NotConfigurable)**: vlastnost je jen pro čtení. Vlastnosti, které jsou označené jako tento atribut nelze nastavit konfigurace, ale jsou nenaplnil **Get()** metoda, pokud jsou k dispozici.
- **DscProperty()**: vlastnost je možné konfigurovat, ale není nutné.

**$Path** a **$SourcePath** vlastnosti jsou oba řetězce. **$CreationTime** je [data a času](https://technet.microsoft.com/library/system.datetime.aspx) vlastnost. **$Ensure** vlastnost je typ výčtu definované následujícím způsobem.

```powershell
enum Ensure
{
    Absent
    Present
}
```

### <a name="implementing-the-methods"></a>Implementace metody

**Get()**, **Set()**, a **Test()** metody jsou obdobou **Get-TargetResource**, **Set-TargetResource** , a **Test TargetResource** funkcí v zdroje skriptu.

Tento kód také obsahuje funkci CopyFile() pomocné funkce, která zkopíruje soubor z **$SourcePath** k **$Path**.

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

### <a name="the-complete-file"></a>Dokončení souboru
Dokončení třídy soubor odpovídá.

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

Pokud chcete zpřístupnit prostředek založené na třídě modul DSC, je nutné zahrnout **DscResourcesToExport** příkaz v souboru manifestu, který se dá pokyn modulu exportovat prostředku. Naše manifest vypadá takto:

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

## <a name="test-the-resource"></a>Testování prostředku

Po uložení třídy a souborů manifestu ve struktuře složky, jak bylo popsáno dříve, můžete vytvořit konfigurace, které používá nový prostředek. Informace o tom, jak spustit konfigurace DSC najdete v tématu [přijetí konfigurace](enactingConfigurations.md). Následující konfigurace bude zkontrolujte, jestli soubor v `c:\test\test.txt` existuje a pokud ne, zkopíruje soubor z `c:\test.txt` (byste měli vytvořit `c:\test.txt` před spuštěním konfigurace).

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

>**Poznámka:** **PsDscRunAsCredential** je podporována v prostředí PowerShell 5.0 nebo novější.

**PsDscRunAsCredential** vlastnost lze použít v [konfigurace DSC](configurations.md) prostředků bloku určí prostředek by měl být spuštění pod zadanou sadu přihlašovacích údajů.
Další informace najdete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).

### <a name="require-or-disallow-psdscrunascredential-for-your-resource"></a>Povolení nebo zakázání PsDscRunAsCredential prostředku

**DscResource()** atribut přebírá volitelný parametr **RunAsCredential**.
Tento parametr má jednu ze tří hodnot:

- `Optional` **PsDscRunAsCredential** pro konfigurace, které volají tento prostředek je volitelný. Tato hodnota je výchozí.
- `Mandatory` **PsDscRunAsCredential** musí používat pro všechny konfigurace, který volá tento prostředek.
- `NotSupported` Konfigurace, které volají tento prostředek nelze použít **PsDscRunAsCredential**.
- `Default` Stejné jako `Optional`.

Například následující atribut použít k určení, že vlastní prostředek nepodporuje použití **PsDscRunAsCredential**:

```powershell
[DscResource(RunAsCredential=NotSupported)]
class FileResource {
}
```

### <a name="access-the-user-context"></a>Přístup k kontext uživatele

Pro přístup k kontext uživatele z v rámci vlastní prostředek, můžete použít automatické proměnné `$global:PsDscContext`.

Například následující kód zapíše kontextu uživatele, pod kterým běží prostředku do datového proudu podrobný výstup:

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $global:PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a>Viz také
### <a name="concepts"></a>Koncepty
[Sestavení vlastní Windows PowerShell Desired State Configuration prostředky](authoringResource.md)