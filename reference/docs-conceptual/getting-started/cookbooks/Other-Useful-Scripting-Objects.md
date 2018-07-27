---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Další užitečné skriptovací objekty
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: 04e94f858b568928b3910dd0ee85a912a6afc264
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268496"
---
# <a name="other-useful-scripting-objects"></a><span data-ttu-id="6be51-103">Další užitečné skriptovací objekty</span><span class="sxs-lookup"><span data-stu-id="6be51-103">Other Useful Scripting Objects</span></span>

<span data-ttu-id="6be51-104">Následující objekty poskytují další funkce skriptování v prostředí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6be51-104">The following objects provide additional scripting functionality in Windows PowerShell ISE.</span></span> <span data-ttu-id="6be51-105">Nejsou součástí **$psISE** hierarchie.</span><span class="sxs-lookup"><span data-stu-id="6be51-105">They are not part of the **$psISE** hierarchy.</span></span>

## <a name="useful-scripting-objects"></a><span data-ttu-id="6be51-106">Užitečné objekty skriptování</span><span class="sxs-lookup"><span data-stu-id="6be51-106">Useful Scripting objects</span></span>

### <a name="psunsupportedconsoleapplications"></a><span data-ttu-id="6be51-107">$psUnsupportedConsoleApplications</span><span class="sxs-lookup"><span data-stu-id="6be51-107">$psUnsupportedConsoleApplications</span></span>

<span data-ttu-id="6be51-108">Existují určitá omezení pro interakci Windows PowerShell ISE pomocí konzolové aplikace.</span><span class="sxs-lookup"><span data-stu-id="6be51-108">There are some limitations on how Windows PowerShell ISE interacts with console applications.</span></span> <span data-ttu-id="6be51-109">Příkaz nebo automatizační skript, který vyžaduje zásah uživatele nemusí fungovat způsob, jakým funguje v konzole Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="6be51-109">A command or an automation script that requires user intervention might not work the way it works from the Windows PowerShell console.</span></span> <span data-ttu-id="6be51-110">Můžete chtít blokovat útoky DoS tyto příkazy nebo skripty v aplikaci Windows PowerShell ISE příkazového podokna.</span><span class="sxs-lookup"><span data-stu-id="6be51-110">You might want to block these commands or scripts from running in the Windows PowerShell ISE Command pane.</span></span> <span data-ttu-id="6be51-111">**$PsUnsupportedConsoleApplications** objektu udržuje seznam těchto příkazů.</span><span class="sxs-lookup"><span data-stu-id="6be51-111">The **$psUnsupportedConsoleApplications** object keeps a list of such commands.</span></span> <span data-ttu-id="6be51-112">Pokud se pokusíte spustit příkazy v tomto seznamu, dostanete zprávu, že se nepodporují.</span><span class="sxs-lookup"><span data-stu-id="6be51-112">If you try to run the commands in this list, you get a message that they are not supported.</span></span> <span data-ttu-id="6be51-113">Následující skript přidá položku do seznamu.</span><span class="sxs-lookup"><span data-stu-id="6be51-113">The following script adds an entry to the list.</span></span>

```powershell
# List the unsupported commands
$psUnsupportedConsoleApplications

# Add a command to this list
$psUnsupportedConsoleApplications.Add('Mycommand')

# Show the augmented list of commands
$psUnsupportedConsoleApplications
```

### <a name="pslocalhelp"></a><span data-ttu-id="6be51-114">$psLocalHelp</span><span class="sxs-lookup"><span data-stu-id="6be51-114">$psLocalHelp</span></span>

<span data-ttu-id="6be51-115">Toto je objekt slovníku, který udržuje kontextové mapování mezi témata nápovědy a souvisejících odkazů v místním zkompilovaný soubor nápovědy HTML.</span><span class="sxs-lookup"><span data-stu-id="6be51-115">This is a dictionary object that maintains a context-sensitive mapping between Help topics and their associated links in the local compiled HTML Help file.</span></span> <span data-ttu-id="6be51-116">Používá se k vyhledání místní nápovědu pro určité téma.</span><span class="sxs-lookup"><span data-stu-id="6be51-116">It is used to locate the local Help for a particular topic.</span></span> <span data-ttu-id="6be51-117">Můžete přidat nebo odstranit témata z tohoto seznamu.</span><span class="sxs-lookup"><span data-stu-id="6be51-117">You can add or delete topics from this list.</span></span> <span data-ttu-id="6be51-118">Následující příklad kódu ukazuje příklad páry klíč hodnota, které jsou obsaženy v `$psLocalHelp`.</span><span class="sxs-lookup"><span data-stu-id="6be51-118">The following code example shows some example key-value pairs that are contained in `$psLocalHelp`.</span></span>

```powershell
# See the local help map
$psLocalHelp | Format-List
```

```output
Key   : Add-Computer
Value : WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm

Key   : Add-Content
Value : WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm
```

<span data-ttu-id="6be51-119">Následující skript přidá položku do seznamu.</span><span class="sxs-lookup"><span data-stu-id="6be51-119">The following script adds an entry to the list.</span></span>

```powershell
$psLocalHelp.Add("get-myNoun", "c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a><span data-ttu-id="6be51-120">$psOnlineHelp</span><span class="sxs-lookup"><span data-stu-id="6be51-120">$psOnlineHelp</span></span>

<span data-ttu-id="6be51-121">Toto je objekt slovníku, který udržuje kontextové mapování mezi názvy témat témat nápovědy a jejich přidružené externí adresy URL.</span><span class="sxs-lookup"><span data-stu-id="6be51-121">This is a dictionary object that maintains a context-sensitive mapping between topic titles of Help topics and their associated external URLs.</span></span> <span data-ttu-id="6be51-122">Používá se k vyhledejte v nápovědě k určitému tématu na webu.</span><span class="sxs-lookup"><span data-stu-id="6be51-122">It is used to locate the Help for a particular topic on the web.</span></span> <span data-ttu-id="6be51-123">Můžete přidat nebo odstranit témata z tohoto seznamu.</span><span class="sxs-lookup"><span data-stu-id="6be51-123">You can add or delete topics from this list.</span></span>

```powershell
$psOnlineHelp | Format-List
```

```output
Key   : Add-Computer
Value : http://go.microsoft.com/fwlink/p/?LinkID=135194

Key   : Add-Content
Value : http://go.microsoft.com/fwlink/p/?LinkID=113278
```

<span data-ttu-id="6be51-124">Následující skript přidá položku do seznamu.</span><span class="sxs-lookup"><span data-stu-id="6be51-124">The following script adds an entry to the list.</span></span>

```powershell
$psOnlineHelp.Add("get-myNoun", "http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a><span data-ttu-id="6be51-125">Viz také</span><span class="sxs-lookup"><span data-stu-id="6be51-125">See Also</span></span>

[<span data-ttu-id="6be51-126">Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="6be51-126">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)