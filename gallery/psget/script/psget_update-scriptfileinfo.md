---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: Aktualizace ScriptFileInfo
ms.openlocfilehash: 3af12d2754b7b3c94ac63db8ca6a564c924a2bde
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="update-scriptfileinfo"></a><span data-ttu-id="3e758-103">Aktualizace ScriptFileInfo</span><span class="sxs-lookup"><span data-stu-id="3e758-103">Update-ScriptFileInfo</span></span>

<span data-ttu-id="3e758-104">Rutina aktualizace ScriptFileInfo umožňuje aktualizovat existující metadata souboru skriptu.</span><span class="sxs-lookup"><span data-stu-id="3e758-104">Update-ScriptFileInfo cmdlet lets you to update the existing script file metadata.</span></span>

## <a name="description"></a><span data-ttu-id="3e758-105">Popis</span><span class="sxs-lookup"><span data-stu-id="3e758-105">Description</span></span>

<span data-ttu-id="3e758-106">Rutinu Update-ScriptFileInfo aktualizuje informace o skriptu.</span><span class="sxs-lookup"><span data-stu-id="3e758-106">The Update-ScriptFileInfo cmdlet updates information for a script.</span></span>
- <span data-ttu-id="3e758-107">Rutina aktualizace ScriptFileInfo aktualizuje metadata souboru skriptu pouze v případě, že byla vytvořena pomocí rutiny New-ScriptFileInfo nebo mají platný PSScriptInfo komentář.</span><span class="sxs-lookup"><span data-stu-id="3e758-107">Update-ScriptFileInfo cmdlet updates the metadata of a script file only if it was created using New-ScriptFileInfo cmdlet or with valid PSScriptInfo comment.</span></span>
- <span data-ttu-id="3e758-108">Také můžete přidat do existující soubory skriptu, které nebyly vytvořeny pomocí rutiny New-ScriptFileInfo informací o souboru skriptu.</span><span class="sxs-lookup"><span data-stu-id="3e758-108">Also allows you to add the script file information to the existing script files which were not created using New-ScriptFileInfo cmdlet.</span></span>
- <span data-ttu-id="3e758-109">Pokud – Force, zkuste přidat metadata do existující soubor skriptu, který nebyl vytvořen pomocí rutiny New-ScriptFileInfo.</span><span class="sxs-lookup"><span data-stu-id="3e758-109">If –Force is specified, try to add the metadata to the existing script file which was not created using New-ScriptFileInfo cmdlet.</span></span>
- <span data-ttu-id="3e758-110">Pokud selže Test ScriptFileInfo k chybám analýzy po předřazení metadata skript k existujícímu souboru k chybě, bude vyvolána oznámením něco podobného jako "Nepodařilo se přidat metadata do existující soubor, můžete rutinu nové scriptfileinfo přidat metadata k existující soubor skriptu, který nebyl vytvořen pomocí rutiny New-ScriptFileInfo."</span><span class="sxs-lookup"><span data-stu-id="3e758-110">If Test-ScriptFileInfo fails with the parsing errors, after prepending the script metadata to the existing file, an error will be thrown saying something like "unable to add the metadata to the existing file, you can use the new-scriptfileinfo cmdlet to add the metadata to the existing script file which was not created using New-ScriptFileInfo cmdlet."</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="3e758-111">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="3e758-111">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Update-ScriptFileInfo -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="3e758-112">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="3e758-112">Cmdlet online help reference</span></span>

[<span data-ttu-id="3e758-113">Skript aktualizace</span><span class="sxs-lookup"><span data-stu-id="3e758-113">Update-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619793)

## <a name="example-commands"></a><span data-ttu-id="3e758-114">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="3e758-114">Example commands</span></span>

```powershell
# Use Update-ScriptFileInfo cmdlet to update the script metadata
Update-ScriptFileInfo -Path C:\ScriptSharingDemo\Demo-ScriptWithCompletePSScriptInfo.ps1 -Version 2.0

Test-ScriptFileInfo C:\ScriptSharingDemo\Demo-ScriptWithCompletePSScriptInfo.ps1

Version Name Author Description
------- ---- ------ -----------
2.0 Demo-ScriptWithComplet... manikb my new script file
```


### <a name="adding-the-script-metadata-to-the-existing-script-file"></a><span data-ttu-id="3e758-115">Přidání metadat skript k existujícímu souboru skriptu</span><span class="sxs-lookup"><span data-stu-id="3e758-115">Adding the script metadata to the existing script file</span></span>

```powershell
PS C:\WINDOWS\system32> New-ScriptFileInfo -Description "Script file description." -PassThru

<#PSScriptInfo

.VERSION 1.0

.GUID 1cfd45e7-4219-4cd2-af21-d8577476be09

.AUTHOR manikb

.COMPANYNAME

.COPYRIGHT

.TAGS

.LICENSEURI

.PROJECTURI

.ICONURI

.EXTERNALMODULEDEPENDENCIES

.REQUIREDSCRIPTS

.EXTERNALSCRIPTDEPENDENCIES

.RELEASENOTES


#>

<#

.DESCRIPTION
Script file description.

#>
Param()


PS C:\WINDOWS\system32> $content = @'
   Function foo
   {
   "Foo"
   }
>>
   Foo
'@

PS C:\WINDOWS\system32>
PS C:\WINDOWS\system32> Set-Content -Value $content -Path C:\temp\ScriptFileWithoutMetadata.ps1 -Force
PS C:\WINDOWS\system32> Test-ScriptFileInfo c:\temp\ScriptFileWithoutMetadata.ps1
Test-ScriptFileInfo : PSScriptInfo is not specified in the script file 'C:\temp\ScriptFileWithoutMetadata.ps1', use the Update-ScriptFileInfo with -Force 
or New-ScriptFileInfo cmdlet to add the PSScriptInfo to the script file.
At line:1 char:1
+ Test-ScriptFileInfo c:\temp\ScriptFileWithoutMetadata.ps1
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (C:\temp\ScriptFileWithoutMetadata.ps1:String) [Test-ScriptFileInfo], ArgumentException
    + FullyQualifiedErrorId : MissingPSScriptInfo,Test-ScriptFileInfo

PS C:\WINDOWS\system32> # Should Fail
PS C:\WINDOWS\system32> Update-ScriptFileInfo c:\temp\ScriptFileWithoutMetadata.ps1
Test-ScriptFileInfo : PSScriptInfo is not specified in the script file 'C:\temp\ScriptFileWithoutMetadata.ps1', use the Update-ScriptFileInfo with -Force 
or New-ScriptFileInfo cmdlet to add the PSScriptInfo to the script file.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:4704 char:29
+ ...      $psscriptInfo = Test-ScriptFileInfo -LiteralPath $scriptFilePath
+                          ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (C:\temp\ScriptFileWithoutMetadata.ps1:String) [Test-ScriptFileInfo], ArgumentException
    + FullyQualifiedErrorId : MissingPSScriptInfo,Test-ScriptFileInfo

PS C:\WINDOWS\system32> # Should Fail
PS C:\WINDOWS\system32> Update-ScriptFileInfo c:\temp\ScriptFileWithoutMetadata.ps1 -Force
Update-ScriptFileInfo : Description parameter is missing for adding the metadata to script file. Try again after specifying the description.
At line:1 char:1
+ Update-ScriptFileInfo c:\temp\ScriptFileWithoutMetadata.ps1 -Force
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Update-ScriptFileInfo], ArgumentException
    + FullyQualifiedErrorId : DescriptionParameterIsMissingForAddingTheScriptFileInfo,Update-ScriptFileInfo

PS C:\WINDOWS\system32> Update-ScriptFileInfo c:\temp\ScriptFileWithoutMetadata.ps1 -Force -Description "Temp script file."
PS C:\WINDOWS\system32> Test-ScriptFileInfo c:\temp\ScriptFileWithoutMetadata.ps1

Version    Name                      Author               Description
-------    ----                      ------               -----------
1.0        ScriptFileWithoutMetadata manikb               Temp script file.


PS C:\WINDOWS\system32> Get-Content c:\temp\ScriptFileWithoutMetadata.ps1

<#PSScriptInfo

.VERSION 1.0

.GUID 855821be-811c-4eb1-a7a7-afd6081be175

.AUTHOR manikb

.COMPANYNAME

.COPYRIGHT

.TAGS

.LICENSEURI

.PROJECTURI

.ICONURI

.EXTERNALMODULEDEPENDENCIES

.REQUIREDSCRIPTS

.EXTERNALSCRIPTDEPENDENCIES

.RELEASENOTES


#>

<#

.DESCRIPTION
Temp script file.

#>

Param()


Function foo
{
"Foo"
}

Foo

```

