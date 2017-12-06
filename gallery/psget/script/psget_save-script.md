---
ms.date: 2017-10-17
contributor: keithb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: "Uložení skriptu"
ms.openlocfilehash: b54e8ba074b7cadd52df781c9021332ccc90f9fd
ms.sourcegitcommit: 58371abe9db4b9a0e4e1eb82d39a9f9e187355f9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/05/2017
---
# <a name="save-script"></a><span data-ttu-id="8f2bf-103">Uložení skriptu</span><span class="sxs-lookup"><span data-stu-id="8f2bf-103">Save-Script</span></span>

<span data-ttu-id="8f2bf-104">Umožňuje uložit skript rutiny a projděte si soubor skriptu uložením do zadaného umístění.</span><span class="sxs-lookup"><span data-stu-id="8f2bf-104">Save-Script cmdlet lets you to review the script file by saving it to a specified location.</span></span>

## <a name="description"></a><span data-ttu-id="8f2bf-105">Popis</span><span class="sxs-lookup"><span data-stu-id="8f2bf-105">Description</span></span>

<span data-ttu-id="8f2bf-106">Uložení skriptu rutina uloží zadaný skript.</span><span class="sxs-lookup"><span data-stu-id="8f2bf-106">The Save-Script cmdlet saves the specified script.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="8f2bf-107">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="8f2bf-107">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Save-Script -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="8f2bf-108">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="8f2bf-108">Cmdlet online help reference</span></span>

[<span data-ttu-id="8f2bf-109">Uložení skriptu</span><span class="sxs-lookup"><span data-stu-id="8f2bf-109">Save-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619786)

## <a name="example-commands"></a><span data-ttu-id="8f2bf-110">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="8f2bf-110">Example commands</span></span>

### <a name="example-1-save-a-script-from-a-repository"></a><span data-ttu-id="8f2bf-111">Příklad 1: Uložte skript z úložiště</span><span class="sxs-lookup"><span data-stu-id="8f2bf-111">Example 1: Save a script from a repository</span></span>
<span data-ttu-id="8f2bf-112">Tento příkaz uloží nejnovější verzi skriptu Fabrikam-ClientScript z GalleryINT úložiště do místní složky C:\ScriptSharingDemo</span><span class="sxs-lookup"><span data-stu-id="8f2bf-112">This command saves the latest version of the script Fabrikam-ClientScript from GalleryINT repository to the local folder C:\ScriptSharingDemo</span></span>

```powershell
Save-Script -Name Fabrikam-ClientScript -Repository GalleryINT -Path C:\ScriptSharingDemo
```

### <a name="example-2-save-a-version-of-a-script-by-piping-from-the-find-script-cmdlet"></a><span data-ttu-id="8f2bf-113">Příklad 2: Uložení verze skriptu pomocí zřetězení z rutiny najít skriptu</span><span class="sxs-lookup"><span data-stu-id="8f2bf-113">Example 2: Save a version of a script by piping from the Find-Script cmdlet</span></span>

<span data-ttu-id="8f2bf-114">První příkaz vyhledá verzi 1.5 Fabrikam ClientScript z úložiště GalleryINT a uloží ji do složky C:\ScriptSharingDemo</span><span class="sxs-lookup"><span data-stu-id="8f2bf-114">The first command finds version 1.5 of Fabrikam-ClientScript from the repository GalleryINT and saves it to the folder C:\ScriptSharingDemo</span></span>

<span data-ttu-id="8f2bf-115">V druhém příkazu ověří metadata uložený skript.</span><span class="sxs-lookup"><span data-stu-id="8f2bf-115">The second command validates the saved script metadata.</span></span>

```powershell
Find-Script -Name Fabrikam-ClientScript -Repository GalleryINT -RequiredVersion 1.5 | Save-Script -Path C:\\ScriptSharingDemo
Test-ScriptFileInfo C:\\ScriptSharingDemo\\Fabrikam-ClientScript.ps1

Version Name Author Description
------- ---- ------ -----------
1.5 Fabrikam-ClientScript manikb Description for the Fabrikam-ClientScript script
```

### <a name="example-3-save-a-prerelease-version-of-a-script-from-a-repository"></a><span data-ttu-id="8f2bf-116">Příklad 3: Uložení předprodejní verze skriptu z úložiště</span><span class="sxs-lookup"><span data-stu-id="8f2bf-116">Example 3: Save a prerelease version of a script from a repository</span></span>
<span data-ttu-id="8f2bf-117">Tento příkaz uloží nejnovější verzi skriptu Fabrikam-ClientScript z GalleryINT úložiště do místní složky C:\ScriptSharingDemo</span><span class="sxs-lookup"><span data-stu-id="8f2bf-117">This command saves the latest version of the script Fabrikam-ClientScript from GalleryINT repository to the local folder C:\ScriptSharingDemo</span></span>

```powershell
Save-Script -Name Fabrikam-ClientScript -Path C:\ScriptSharingDemo -AllowPrerelease
```

