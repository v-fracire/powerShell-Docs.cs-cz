---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: "Uložení skriptu"
ms.openlocfilehash: 7b692d33e3f86a89505b8d37c0da4177f3dff2c2
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="save-script"></a><span data-ttu-id="53250-103">Uložení skriptu</span><span class="sxs-lookup"><span data-stu-id="53250-103">Save-Script</span></span>

<span data-ttu-id="53250-104">Umožňuje uložit skript rutiny a projděte si soubor skriptu uložením do zadaného umístění.</span><span class="sxs-lookup"><span data-stu-id="53250-104">Save-Script cmdlet lets you to review the script file by saving it to a specified location.</span></span>

## <a name="description"></a><span data-ttu-id="53250-105">Popis</span><span class="sxs-lookup"><span data-stu-id="53250-105">Description</span></span>

<span data-ttu-id="53250-106">Uložení skriptu rutina uloží zadaný skript.</span><span class="sxs-lookup"><span data-stu-id="53250-106">The Save-Script cmdlet saves the specified script.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="53250-107">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="53250-107">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Save-Script -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="53250-108">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="53250-108">Cmdlet online help reference</span></span>

[<span data-ttu-id="53250-109">Uložení skriptu</span><span class="sxs-lookup"><span data-stu-id="53250-109">Save-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619786)

## <a name="example-commands"></a><span data-ttu-id="53250-110">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="53250-110">Example commands</span></span>

### <a name="example-1-save-a-script-from-a-repository"></a><span data-ttu-id="53250-111">Příklad 1: Uložte skript z úložiště</span><span class="sxs-lookup"><span data-stu-id="53250-111">Example 1: Save a script from a repository</span></span>
<span data-ttu-id="53250-112">Tento příkaz uloží nejnovější verzi skriptu Fabrikam-ClientScript z GalleryINT úložiště do místní složky C:\ScriptSharingDemo</span><span class="sxs-lookup"><span data-stu-id="53250-112">This command saves the latest version of the script Fabrikam-ClientScript from GalleryINT repository to the local folder C:\ScriptSharingDemo</span></span>

```powershell
Save-Script -Name Fabrikam-ClientScript -Repository GalleryINT -Path C:\ScriptSharingDemo
```

### <a name="example-2-save-a-version-of-a-script-by-piping-from-the-find-script-cmdlet"></a><span data-ttu-id="53250-113">Příklad 2: Uložení verze skriptu pomocí zřetězení z rutiny najít skriptu</span><span class="sxs-lookup"><span data-stu-id="53250-113">Example 2: Save a version of a script by piping from the Find-Script cmdlet</span></span>

<span data-ttu-id="53250-114">První příkaz vyhledá verzi 1.5 Fabrikam ClientScript z úložiště GalleryINT a uloží ji do složky C:\ScriptSharingDemo</span><span class="sxs-lookup"><span data-stu-id="53250-114">The first command finds version 1.5 of Fabrikam-ClientScript from the repository GalleryINT and saves it to the folder C:\ScriptSharingDemo</span></span>

<span data-ttu-id="53250-115">V druhém příkazu ověří metadata uložený skript.</span><span class="sxs-lookup"><span data-stu-id="53250-115">The second command validates the saved script metadata.</span></span>

```powershell
Find-Script -Name Fabrikam-ClientScript -Repository GalleryINT -RequiredVersion 1.5 | Save-Script -Path C:\\ScriptSharingDemo
Test-ScriptFileInfo C:\\ScriptSharingDemo\\Fabrikam-ClientScript.ps1

Version Name Author Description
------- ---- ------ -----------
1.5 Fabrikam-ClientScript manikb Description for the Fabrikam-ClientScript script
```

