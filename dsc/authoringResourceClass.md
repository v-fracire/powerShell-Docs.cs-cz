---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Psaní vlastních prostředků DSC s třídami, prostředí PowerShell"
ms.openlocfilehash: 6e482f45c7d09898d46de20f43dcf16ecf3da7da
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="writing-a-custom-dsc-resource-with-powershell-classes"></a><span data-ttu-id="066de-103">Psaní vlastních prostředků DSC s třídami, prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="066de-103">Writing a custom DSC resource with PowerShell classes</span></span>

> <span data-ttu-id="066de-104">Platí pro: Windows prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="066de-104">Applies To: Windows Windows PowerShell 5.0</span></span>

<span data-ttu-id="066de-105">Se zavedením prostředí PowerShell tříd v prostředí Windows PowerShell 5.0 můžete teď určit prostředek DSC vytvořením třídy.</span><span class="sxs-lookup"><span data-stu-id="066de-105">With the introduction of PowerShell classes in Windows PowerShell 5.0, you can now define a DSC resource by creating a class.</span></span> <span data-ttu-id="066de-106">Třída definuje schéma a provádění prostředku, takže není nutné vytvořit samostatný soubor MOF.</span><span class="sxs-lookup"><span data-stu-id="066de-106">The class defines both the schema and the implementation of the resource, so there is no need to create a separate MOF file.</span></span> <span data-ttu-id="066de-107">Struktura složek na základě třídy prostředku je také jednodušší, protože **DSCResources** složka není nezbytné.</span><span class="sxs-lookup"><span data-stu-id="066de-107">The folder structure for a class-based resource is also simpler, because a **DSCResources** folder is not necessary.</span></span>

<span data-ttu-id="066de-108">V prostředek DSC založené na třídě schématu je definován jako vlastnosti třídy, které lze upravit atributy pro určení typu vlastnost...</span><span class="sxs-lookup"><span data-stu-id="066de-108">In a class-based DSC resource, the schema is defined as properties of the class which can be modified with attributes to specify the property type..</span></span> <span data-ttu-id="066de-109">Prostředek je implementováno modulem **Get()**, **Set()**, a **Test()** metody (ekvivalentní **Get-TargetResource**, **Set-TargetResource**, a **Test TargetResource** funkcí v zdroje skriptu.</span><span class="sxs-lookup"><span data-stu-id="066de-109">The resource is implemented by **Get()**, **Set()**, and **Test()** methods (equivalent to the **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions in a script resource.</span></span>

<span data-ttu-id="066de-110">V tomto tématu, vytvoříme jednoduchý prostředek s názvem **FileResource** , spravuje soubor v zadané cestě.</span><span class="sxs-lookup"><span data-stu-id="066de-110">In this topic, we will create a simple resource named **FileResource** that manages a file in a specified path.</span></span>

<span data-ttu-id="066de-111">Další informace o prostředcích DSC najdete v tématu [sestavení vlastní Windows PowerShell požadovaného stavu konfigurace prostředků](authoringResource.md)</span><span class="sxs-lookup"><span data-stu-id="066de-111">For more information about DSC resources, see [Build Custom Windows PowerShell Desired State Configuration Resources](authoringResource.md)</span></span>

><span data-ttu-id="066de-112">**Poznámka:** obecné kolekce nepodporuje prostředky založené na třídě.</span><span class="sxs-lookup"><span data-stu-id="066de-112">**Note:** Generic collections are not supported in class-based resources.</span></span>

## <a name="folder-structure-for-a-class-resource"></a><span data-ttu-id="066de-113">Struktura složek pro prostředek – třída</span><span class="sxs-lookup"><span data-stu-id="066de-113">Folder structure for a class resource</span></span>

<span data-ttu-id="066de-114">Chcete-li implementovat vlastní prostředek DSC s třídou prostředí PowerShell, vytvořte následující strukturu složek.</span><span class="sxs-lookup"><span data-stu-id="066de-114">To implement a DSC custom resource with a PowerShell class, create the following folder structure.</span></span> <span data-ttu-id="066de-115">Je třída definovaná v **MyDscResource.psm1** a manifestu modulu je definována v **MyDscResource.psd1**.</span><span class="sxs-lookup"><span data-stu-id="066de-115">The class is defined in **MyDscResource.psm1** and the module manifest is defined in **MyDscResource.psd1**.</span></span>

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResource (folder)
        |- MyDscResource.psm1 
           MyDscResource.psd1 
```

## <a name="create-the-class"></a><span data-ttu-id="066de-116">Vytvoření třídy</span><span class="sxs-lookup"><span data-stu-id="066de-116">Create the class</span></span>

<span data-ttu-id="066de-117">Class – klíčové slovo použijete pro vytvoření třídy prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="066de-117">You use the class keyword to create a PowerShell class.</span></span> <span data-ttu-id="066de-118">Chcete-li určit, že třída je prostředek DSC, použijte **DscResource()** atribut.</span><span class="sxs-lookup"><span data-stu-id="066de-118">To specify that a class is a DSC resource, use the **DscResource()** attribute.</span></span> <span data-ttu-id="066de-119">Název třídy je název prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="066de-119">The name of the class is the name of the DSC resource.</span></span>

```powershell
[DscResource()]
class FileResource {
}
```

### <a name="declare-properties"></a><span data-ttu-id="066de-120">Deklarování vlastností</span><span class="sxs-lookup"><span data-stu-id="066de-120">Declare properties</span></span>

<span data-ttu-id="066de-121">Schéma prostředků DSC je definován jako vlastnosti třídy.</span><span class="sxs-lookup"><span data-stu-id="066de-121">The DSC resource schema is defined as properties of the class.</span></span> <span data-ttu-id="066de-122">Jsme deklarovat tři vlastnosti následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="066de-122">We declare three properties as follows.</span></span>

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

<span data-ttu-id="066de-123">Všimněte si, že jsou upraveny vlastnosti podle atributů.</span><span class="sxs-lookup"><span data-stu-id="066de-123">Notice that the properties are modified by attributes.</span></span> <span data-ttu-id="066de-124">Význam atributy vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="066de-124">The meaning of the attributes is as follows:</span></span>

- <span data-ttu-id="066de-125">**DscProperty(Key)**: vlastnost se vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="066de-125">**DscProperty(Key)**: The property is required.</span></span> <span data-ttu-id="066de-126">Vlastnost je klíč.</span><span class="sxs-lookup"><span data-stu-id="066de-126">The property is a key.</span></span> <span data-ttu-id="066de-127">Hodnoty všech vlastností označené jako klíče musí zkombinovat k jednoznačné identifikaci instance prostředku v rámci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="066de-127">The values of all properties marked as keys must combine to uniquely identify a resource instance within a configuration.</span></span>
- <span data-ttu-id="066de-128">**DscProperty(Mandatory)**: vlastnost se vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="066de-128">**DscProperty(Mandatory)**: The property is required.</span></span>
- <span data-ttu-id="066de-129">**DscProperty(NotConfigurable)**: vlastnost je jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="066de-129">**DscProperty(NotConfigurable)**: The property is read-only.</span></span> <span data-ttu-id="066de-130">Vlastnosti, které jsou označené jako tento atribut nelze nastavit konfigurace, ale jsou nenaplnil **Get()** metoda, pokud jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="066de-130">Properties marked with this attribute cannot be set by a configuration, but are populated by the **Get()** method when present.</span></span>
- <span data-ttu-id="066de-131">**DscProperty()**: vlastnost je možné konfigurovat, ale není nutné.</span><span class="sxs-lookup"><span data-stu-id="066de-131">**DscProperty()**: The property is configurable, but it is not required.</span></span>

<span data-ttu-id="066de-132">**$Path** a **$SourcePath** vlastnosti jsou oba řetězce.</span><span class="sxs-lookup"><span data-stu-id="066de-132">The **$Path** and **$SourcePath** properties are both strings.</span></span> <span data-ttu-id="066de-133">**$CreationTime** je [data a času](https://technet.microsoft.com/en-us/library/system.datetime.aspx) vlastnost.</span><span class="sxs-lookup"><span data-stu-id="066de-133">The **$CreationTime** is a [DateTime](https://technet.microsoft.com/en-us/library/system.datetime.aspx) property.</span></span> <span data-ttu-id="066de-134">**$Ensure** vlastnost je typ výčtu definované následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="066de-134">The **$Ensure** property is an enumeration type, defined as follows.</span></span>

```powershell
enum Ensure 
{ 
    Absent 
    Present 
}
```

### <a name="implementing-the-methods"></a><span data-ttu-id="066de-135">Implementace metody</span><span class="sxs-lookup"><span data-stu-id="066de-135">Implementing the methods</span></span>

<span data-ttu-id="066de-136">**Get()**, **Set()**, a **Test()** metody jsou obdobou **Get-TargetResource**, **Set-TargetResource** , a **Test TargetResource** funkcí v zdroje skriptu.</span><span class="sxs-lookup"><span data-stu-id="066de-136">The **Get()**, **Set()**, and **Test()** methods are analogous to the **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions in a script resource.</span></span>

<span data-ttu-id="066de-137">Tento kód také obsahuje funkci CopyFile() pomocné funkce, která zkopíruje soubor z **$SourcePath** k **$Path**.</span><span class="sxs-lookup"><span data-stu-id="066de-137">This code also includes the CopyFile() function, a helper function that copies the file from **$SourcePath** to **$Path**.</span></span> 

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

### <a name="the-complete-file"></a><span data-ttu-id="066de-138">Dokončení souboru</span><span class="sxs-lookup"><span data-stu-id="066de-138">The complete file</span></span>
<span data-ttu-id="066de-139">Dokončení třídy soubor odpovídá.</span><span class="sxs-lookup"><span data-stu-id="066de-139">The complete class file follows.</span></span>

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


## <a name="create-a-manifest"></a><span data-ttu-id="066de-140">Vytvoření manifestu</span><span class="sxs-lookup"><span data-stu-id="066de-140">Create a manifest</span></span>

<span data-ttu-id="066de-141">Pokud chcete zpřístupnit prostředek založené na třídě modul DSC, je nutné zahrnout **DscResourcesToExport** příkaz v souboru manifestu, který se dá pokyn modulu exportovat prostředku.</span><span class="sxs-lookup"><span data-stu-id="066de-141">To make a class-based resource available to the DSC engine, you must include a **DscResourcesToExport** statement in the manifest file that instructs the module to export the resource.</span></span> <span data-ttu-id="066de-142">Naše manifest vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="066de-142">Our manifest looks like this:</span></span>

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

## <a name="test-the-resource"></a><span data-ttu-id="066de-143">Testování prostředku</span><span class="sxs-lookup"><span data-stu-id="066de-143">Test the resource</span></span>

<span data-ttu-id="066de-144">Po uložení třídy a souborů manifestu ve struktuře složky, jak bylo popsáno dříve, můžete vytvořit konfigurace, které používá nový prostředek.</span><span class="sxs-lookup"><span data-stu-id="066de-144">After saving the class and manifest files in the folder structure as described earlier, you can create a configuration that uses the new resource.</span></span> <span data-ttu-id="066de-145">Informace o tom, jak spustit konfigurace DSC najdete v tématu [přijetí konfigurace](enactingConfigurations.md).</span><span class="sxs-lookup"><span data-stu-id="066de-145">For information about how to run a DSC configuration, see [Enacting configurations](enactingConfigurations.md).</span></span> <span data-ttu-id="066de-146">Následující konfigurace bude zkontrolujte, jestli soubor v `c:\test\test.txt` existuje a pokud ne, zkopíruje soubor z `c:\test.txt` (byste měli vytvořit `c:\test.txt` před spuštěním konfigurace).</span><span class="sxs-lookup"><span data-stu-id="066de-146">The following configuration will check to see whether the file at `c:\test\test.txt` exists, and, if not, copies the file from `c:\test.txt` (you should create `c:\test.txt` before you run the configuration).</span></span>

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

## <a name="supporting-psdscrunascredential"></a><span data-ttu-id="066de-147">Podpora PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="066de-147">Supporting PsDscRunAsCredential</span></span>

><span data-ttu-id="066de-148">**Poznámka:** **PsDscRunAsCredential** je podporována v prostředí PowerShell 5.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="066de-148">**Note:** **PsDscRunAsCredential** is supported in PowerShell 5.0 and later.</span></span>

<span data-ttu-id="066de-149">**PsDscRunAsCredential** vlastnost lze použít v [konfigurace DSC](configurations.md) prostředků bloku určí prostředek by měl být spuštění pod zadanou sadu přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="066de-149">The **PsDscRunAsCredential** property can be used in [DSC configurations](configurations.md) resource block to specify that the resource should be run under a specified set of credentials.</span></span>
<span data-ttu-id="066de-150">Další informace najdete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="066de-150">For more information, see [Running DSC with user credentials](runAsUser.md).</span></span>

### <a name="require-or-disallow-psdscrunascredential-for-your-resource"></a><span data-ttu-id="066de-151">Povolení nebo zakázání PsDscRunAsCredential prostředku</span><span class="sxs-lookup"><span data-stu-id="066de-151">Require or disallow PsDscRunAsCredential for your resource</span></span>

<span data-ttu-id="066de-152">**DscResource()** atribut přebírá volitelný parametr **RunAsCredential**.</span><span class="sxs-lookup"><span data-stu-id="066de-152">The **DscResource()** attribute takes an optional parameter **RunAsCredential**.</span></span>
<span data-ttu-id="066de-153">Tento parametr má jednu ze tří hodnot:</span><span class="sxs-lookup"><span data-stu-id="066de-153">This parameter takes one of three values:</span></span>

- <span data-ttu-id="066de-154">`Optional`**PsDscRunAsCredential** pro konfigurace, které volají tento prostředek je volitelný.</span><span class="sxs-lookup"><span data-stu-id="066de-154">`Optional` **PsDscRunAsCredential** is optional for configurations that call this resource.</span></span> <span data-ttu-id="066de-155">Tato hodnota je výchozí.</span><span class="sxs-lookup"><span data-stu-id="066de-155">This is the default value.</span></span>
- <span data-ttu-id="066de-156">`Mandatory`**PsDscRunAsCredential** musí používat pro všechny konfigurace, který volá tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="066de-156">`Mandatory` **PsDscRunAsCredential** must be used for any configuration that calls this resource.</span></span>
- <span data-ttu-id="066de-157">`NotSupported`Konfigurace, které volají tento prostředek nelze použít **PsDscRunAsCredential**.</span><span class="sxs-lookup"><span data-stu-id="066de-157">`NotSupported` Configurations that call this resource cannot use **PsDscRunAsCredential**.</span></span>
- <span data-ttu-id="066de-158">`Default`Stejné jako `Optional`.</span><span class="sxs-lookup"><span data-stu-id="066de-158">`Default` Same as `Optional`.</span></span>

<span data-ttu-id="066de-159">Například následující atribut použít k určení, že vlastní prostředek nepodporuje použití **PsDscRunAsCredential**:</span><span class="sxs-lookup"><span data-stu-id="066de-159">For example, use the following attribute to specify that your custom resource does not support using **PsDscRunAsCredential**:</span></span>

```powershell
[DscResource(RunAsCredential=NotSupported)]
class FileResource {
}
```

### <a name="access-the-user-context"></a><span data-ttu-id="066de-160">Přístup k kontext uživatele</span><span class="sxs-lookup"><span data-stu-id="066de-160">Access the user context</span></span>

<span data-ttu-id="066de-161">Pro přístup k kontext uživatele z v rámci vlastní prostředek, můžete použít automatické proměnné `$global:PsDscContext`.</span><span class="sxs-lookup"><span data-stu-id="066de-161">To access the user context from within a custom resource, you can use the automatic variable `$global:PsDscContext`.</span></span>

<span data-ttu-id="066de-162">Například následující kód zapíše kontextu uživatele, pod kterým běží prostředku do datového proudu podrobný výstup:</span><span class="sxs-lookup"><span data-stu-id="066de-162">For example the following code would write the user context under which the resource is running to the verbose output stream:</span></span>

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $global:PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a><span data-ttu-id="066de-163">Viz také</span><span class="sxs-lookup"><span data-stu-id="066de-163">See Also</span></span>
### <a name="concepts"></a><span data-ttu-id="066de-164">Koncepty</span><span class="sxs-lookup"><span data-stu-id="066de-164">Concepts</span></span>
[<span data-ttu-id="066de-165">Sestavení vlastní Windows PowerShell Desired State Configuration prostředky</span><span class="sxs-lookup"><span data-stu-id="066de-165">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)

