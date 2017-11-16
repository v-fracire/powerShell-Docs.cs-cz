---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Další užitečné skriptování objekty"
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: 8334d0b346e59dea3643a93bf52b780b361d1945
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="other-useful-scripting-objects"></a><span data-ttu-id="236ba-103">Další užitečné skriptování objekty</span><span class="sxs-lookup"><span data-stu-id="236ba-103">Other Useful Scripting Objects</span></span>
  <span data-ttu-id="236ba-104">Následující objekty poskytují další skriptovací funkce v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="236ba-104">The following objects provide additional scripting functionality in Windows PowerShell ISE.</span></span> <span data-ttu-id="236ba-105">Nejsou součástí **$psISE** hierarchie.</span><span class="sxs-lookup"><span data-stu-id="236ba-105">They are not part of the **$psISE** hierarchy.</span></span>

## <a name="useful-scripting-objects"></a><span data-ttu-id="236ba-106">Užitečné skriptování objekty</span><span class="sxs-lookup"><span data-stu-id="236ba-106">Useful Scripting objects</span></span>

### <a name="psunsupportedconsoleapplications"></a><span data-ttu-id="236ba-107">$psUnsupportedConsoleApplications</span><span class="sxs-lookup"><span data-stu-id="236ba-107">$psUnsupportedConsoleApplications</span></span>
 <span data-ttu-id="236ba-108">Existují určitá omezení na jak Windows PowerShell ISE komunikuje s konzolové aplikace.</span><span class="sxs-lookup"><span data-stu-id="236ba-108">There are some limitations on how Windows PowerShell ISE interacts with console applications.</span></span> <span data-ttu-id="236ba-109">Příkaz nebo skriptu pro automatizaci, která vyžaduje zásah uživatele nemusí fungovat způsob, jakým funguje z konzoly pro prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="236ba-109">A command or an automation script that requires user intervention might not work the way it works from the Windows PowerShell console.</span></span> <span data-ttu-id="236ba-110">Můžete chtít blokovat těchto příkazů nebo skriptů v podokně Windows PowerShell ISE příkaz spouštět.</span><span class="sxs-lookup"><span data-stu-id="236ba-110">You might want to block these commands or scripts from running in the Windows PowerShell ISE Command pane.</span></span> <span data-ttu-id="236ba-111">**$PsUnsupportedConsoleApplications** objekt udržuje seznam těchto příkazů.</span><span class="sxs-lookup"><span data-stu-id="236ba-111">The **$psUnsupportedConsoleApplications** object keeps a list of such commands.</span></span> <span data-ttu-id="236ba-112">Pokud se pokusíte spusťte příkazy v tomto seznamu, zobrazí zprávu, že nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="236ba-112">If you try to run the commands in this list, you get a message that they are not supported.</span></span> <span data-ttu-id="236ba-113">Následující skript přidá položku do seznamu.</span><span class="sxs-lookup"><span data-stu-id="236ba-113">The following script adds an entry to the list.</span></span>

```
# List the unsupported commands
psUnsupportedConsoleApplications
# Add a command to this list
psUnsupportedConsoleApplications.Add(“Mycommand”)
#Show the augmented list of commands
psUnsupportedConsoleApplications

```

### <a name="pslocalhelp"></a><span data-ttu-id="236ba-114">$psLocalHelp</span><span class="sxs-lookup"><span data-stu-id="236ba-114">$psLocalHelp</span></span>
 <span data-ttu-id="236ba-115">Toto je objekt slovník, který udržuje kontextová mapování mezi témata nápovědy a jejich přidružené odkazů v místním zkompilovaný soubor nápovědy HTML.</span><span class="sxs-lookup"><span data-stu-id="236ba-115">This is a dictionary object that maintains a context-sensitive mapping between Help topics and their associated links in the local compiled HTML Help file.</span></span> <span data-ttu-id="236ba-116">Slouží k vyhledání místní Nápověda pro příslušné téma.</span><span class="sxs-lookup"><span data-stu-id="236ba-116">It is used to locate the local Help for a particular topic.</span></span> <span data-ttu-id="236ba-117">Můžete přidat nebo odstranit témata z tohoto seznamu.</span><span class="sxs-lookup"><span data-stu-id="236ba-117">You can add or delete topics from this list.</span></span> <span data-ttu-id="236ba-118">Následující příklad kódu ukazuje několik příkladů páry klíč hodnota, které jsou obsaženy v **$psLocalHelp**.</span><span class="sxs-lookup"><span data-stu-id="236ba-118">The following code example shows some example key-value pairs that are contained in **$psLocalHelp**.</span></span>

```
# See the local help map
$psLocalHelp | Format-List

```

### <a name="sample-output"></a><span data-ttu-id="236ba-119">Ukázkový výstup</span><span class="sxs-lookup"><span data-stu-id="236ba-119">Sample Output</span></span>

|||
|-|-|
|<span data-ttu-id="236ba-120">Klíč: Počítač</span><span class="sxs-lookup"><span data-stu-id="236ba-120">Key : Add-Computer</span></span>|<span data-ttu-id="236ba-121">Hodnota: WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm</span><span class="sxs-lookup"><span data-stu-id="236ba-121">Value : WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm</span></span>|
|<span data-ttu-id="236ba-122">Klíč: Obsah</span><span class="sxs-lookup"><span data-stu-id="236ba-122">Key : Add-Content</span></span>|<span data-ttu-id="236ba-123">Hodnota: WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm</span><span class="sxs-lookup"><span data-stu-id="236ba-123">Value : WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm</span></span>|

 <span data-ttu-id="236ba-124">Následující skript přidá položku do seznamu.</span><span class="sxs-lookup"><span data-stu-id="236ba-124">The following script adds an entry to the list.</span></span>

```
$psLocalHelp.Add("get-myNoun","c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a><span data-ttu-id="236ba-125">$psOnlineHelp</span><span class="sxs-lookup"><span data-stu-id="236ba-125">$psOnlineHelp</span></span>
 <span data-ttu-id="236ba-126">Toto je objekt slovník, který udržuje kontextová mapování mezi názvy témat témat nápovědy a jejich přidružené externí adresy URL.</span><span class="sxs-lookup"><span data-stu-id="236ba-126">This is a dictionary object that maintains a context-sensitive mapping between topic titles of Help topics and their associated external URLs.</span></span> <span data-ttu-id="236ba-127">Slouží k vyhledejte v nápovědě k příslušné téma na webu.</span><span class="sxs-lookup"><span data-stu-id="236ba-127">It is used to locate the Help for a particular topic on the web.</span></span> <span data-ttu-id="236ba-128">Můžete přidat nebo odstranit témata z tohoto seznamu.</span><span class="sxs-lookup"><span data-stu-id="236ba-128">You can add or delete topics from this list.</span></span>

```
$psOnlineHelp | Format-List

```

### <a name="sample-output"></a><span data-ttu-id="236ba-129">Ukázkový výstup</span><span class="sxs-lookup"><span data-stu-id="236ba-129">Sample Output</span></span>

|||
|-|-|
|<span data-ttu-id="236ba-130">Klíč: Počítač</span><span class="sxs-lookup"><span data-stu-id="236ba-130">Key : Add-Computer</span></span>|<span data-ttu-id="236ba-131">Hodnota: http://go.microsoft.com/fwlink/p/?LinkID=135194</span><span class="sxs-lookup"><span data-stu-id="236ba-131">Value : http://go.microsoft.com/fwlink/p/?LinkID=135194</span></span>|
|<span data-ttu-id="236ba-132">Klíč: Obsah</span><span class="sxs-lookup"><span data-stu-id="236ba-132">Key : Add-Content</span></span>|<span data-ttu-id="236ba-133">Hodnota: http://go.microsoft.com/fwlink/p/?LinkID=113278</span><span class="sxs-lookup"><span data-stu-id="236ba-133">Value : http://go.microsoft.com/fwlink/p/?LinkID=113278</span></span>|

 <span data-ttu-id="236ba-134">Následující skript přidá položku do seznamu.</span><span class="sxs-lookup"><span data-stu-id="236ba-134">The following script adds an entry to the list.</span></span>

```
$psOnlineHelp.Add("get-myNoun","http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a><span data-ttu-id="236ba-135">Viz také</span><span class="sxs-lookup"><span data-stu-id="236ba-135">See Also</span></span>
- [<span data-ttu-id="236ba-136">ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="236ba-136">The Windows PowerShell ISE Scripting Object Model</span></span>](../../core-powershell/ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md)

  