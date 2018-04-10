---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: Test-ScriptFileInfo
ms.openlocfilehash: 56f75007be6e952572aaed7942a1e8714d4104b0
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="test-scriptfileinfo"></a><span data-ttu-id="208fa-103">Test-ScriptFileInfo</span><span class="sxs-lookup"><span data-stu-id="208fa-103">Test-ScriptFileInfo</span></span>

<span data-ttu-id="208fa-104">Ověří blok komentáře metadata souboru skriptu.</span><span class="sxs-lookup"><span data-stu-id="208fa-104">Validates the metadata comment block of a script file.</span></span>

## <a name="description"></a><span data-ttu-id="208fa-105">Popis</span><span class="sxs-lookup"><span data-stu-id="208fa-105">Description</span></span>

<span data-ttu-id="208fa-106">Rutina Test-ScriptFileInfo ověří blok komentáře na začátku skriptu, který bude publikována s rutinu Publish-skriptu.</span><span class="sxs-lookup"><span data-stu-id="208fa-106">The Test-ScriptFileInfo cmdlet validates the comment block at the beginning of a script that will be published with the Publish-Script cmdlet.</span></span>
<span data-ttu-id="208fa-107">Pokud blok komentáře metadat došlo k chybě, tato rutina vrátí informace o kterém se nachází chyba nebo jak opravte ho.</span><span class="sxs-lookup"><span data-stu-id="208fa-107">If the metadata comment block has an error, this cmdlet returns information about where the error is located or how to correct it.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="208fa-108">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="208fa-108">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Test-ScriptFileInfo -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="208fa-109">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="208fa-109">Cmdlet online help reference</span></span>

[<span data-ttu-id="208fa-110">Test-ScriptFileInfo</span><span class="sxs-lookup"><span data-stu-id="208fa-110">Test-ScriptFileInfo</span></span>](http://go.microsoft.com/fwlink/?LinkId=619791)

## <a name="example-commands"></a><span data-ttu-id="208fa-111">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="208fa-111">Example commands</span></span>
```powershell
# Create a new script file with minimum required metadata values
New-ScriptFileInfo -Path C:\ScriptSharingDemo\Demo-Script.ps1 -Description "Script file description goes here"

Get-Content -Path C:\ScriptSharingDemo\Demo-Script.ps1
<#PSScriptInfo
.VERSION 1.0
.GUID 926b47c3-6af2-4b18-b6f5-8b813a9e93ab
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
Script file description goes here
#>
Param()

# Validate and get the script metadata
Test-ScriptFileInfo -Path C:\ScriptSharingDemo\Demo-Script.ps1
Version Name Author Description
------- ---- ------ -----------
1.0 Demo-Script manikb Script file description goes here

# This command tests the script file Test-Runbook.ps1 and uses the pipeline operator to pass the results to the Format-List cmdlet to format the results.
Test-ScriptFileInfo -Path D:\code\Test-Runbook.ps1 | Format-List *

# This command tests the script file Hello-World.ps1, which has no metadata associated with it.
Test-ScriptFileInfo -Path C:\code\Hello-World.ps1
Test-ScriptFileInfo : PSScriptInfo is not specified in the script file 'C:\code\Hello-World.ps1'. You can use the Update-ScriptFileInfo with -Force or New-ScriptFileInfo cmdlet to add the PSScriptInfo to the script file.
At line:1 char:1
+ Test-ScriptFileInfo -Path C:\code\Hello-World.ps1
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (C:\code\Hello-World.ps1:String) [Test-ScriptFileInfo], ArgumentException
    + FullyQualifiedErrorId : MissingPSScriptInfo,Test-ScriptFileInfo

```