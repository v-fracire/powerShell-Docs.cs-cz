---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití rozšíření Tab
ms.assetid: c8730471-bf6a-43b8-ab1d-f9ef5a74f04e
ms.openlocfilehash: 3d047bf0691c8a304d7637aa50fba6ae99709a82
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404114"
---
# <a name="using-tab-expansion"></a><span data-ttu-id="b9513-103">Použití rozšíření Tab</span><span class="sxs-lookup"><span data-stu-id="b9513-103">Using Tab Expansion</span></span>

<span data-ttu-id="b9513-104">Příkazový řádek prostředí často poskytují způsob, jak, automatické dokončování názvů dlouhých souborů nebo příkazů urychlení položky příkazu a poskytuje.</span><span class="sxs-lookup"><span data-stu-id="b9513-104">Command-line shells often provide a way to complete the names of long files or commands automatically, speeding up command entry and providing .</span></span> <span data-ttu-id="b9513-105">Prostředí Windows PowerShell umožňuje zadat názvy souborů a názvy rutin stisknutím kombinace kláves **kartu** klíč.</span><span class="sxs-lookup"><span data-stu-id="b9513-105">Windows PowerShell allows you to fill in file names and cmdlet names by pressing the **Tab** key.</span></span>

> [!NOTE]
> <span data-ttu-id="b9513-106">Vnitřní funkce TabExpansion nebo TabExpansion2 řídí rozšíření TAB.</span><span class="sxs-lookup"><span data-stu-id="b9513-106">Tab expansion is controlled by the internal function TabExpansion or TabExpansion2.</span></span> <span data-ttu-id="b9513-107">Protože tato funkce může přepsat nebo upraví, této diskuse je návod k chování výchozí konfigurace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9513-107">Since this function can be modified or overridden, this discussion is a guide to the behavior of the default PowerShell configuration.</span></span>

<span data-ttu-id="b9513-108">Chcete-li automaticky vyplnit název souboru nebo cesta z dostupných voleb, zadejte část názvu a stiskněte klávesu **kartu** klíč.</span><span class="sxs-lookup"><span data-stu-id="b9513-108">To fill in a filename or path from the available choices automatically, type part of the name and press the **Tab** key.</span></span> <span data-ttu-id="b9513-109">Prostředí PowerShell bude automaticky rozbalte název tak, aby první shodu, kterou najde.</span><span class="sxs-lookup"><span data-stu-id="b9513-109">PowerShell will automatically expand the name to the first match that it finds.</span></span> <span data-ttu-id="b9513-110">Stisknutím klávesy **kartu** klíč bude opakovaně cyklicky procházet všechny dostupné možnosti.</span><span class="sxs-lookup"><span data-stu-id="b9513-110">Pressing the **Tab** key repeatedly will cycle through all of the available choices.</span></span>

<span data-ttu-id="b9513-111">Karta rozšíření názvy rutin se mírně liší.</span><span class="sxs-lookup"><span data-stu-id="b9513-111">The tab expansion of cmdlet names is slightly different.</span></span> <span data-ttu-id="b9513-112">Použití rozšíření tab na název rutiny, zadejte celý první část názvu (akce) a pomlčku, která ji následuje.</span><span class="sxs-lookup"><span data-stu-id="b9513-112">To use tab expansion on a cmdlet name, type the entire first part of the name (the verb) and the hyphen that follows it.</span></span> <span data-ttu-id="b9513-113">Můžete vyplnit informace pro částečné shody názvu.</span><span class="sxs-lookup"><span data-stu-id="b9513-113">You can fill in more of the name for a partial match.</span></span> <span data-ttu-id="b9513-114">Pokud zadáte například **get-co** a potom stiskněte klávesu **kartu** klíče, prostředí PowerShell se automaticky rozšíří na **Get-Command** rutiny (Všimněte si, že také změní velikost písmen posloupnost písmen na jejich běžného formuláře).</span><span class="sxs-lookup"><span data-stu-id="b9513-114">For example, if you type **get-co** and then press the **Tab** key, PowerShell will automatically expand this to the **Get-Command** cmdlet (notice that it also changes the case of letters to their standard form).</span></span> <span data-ttu-id="b9513-115">Pokud stisknete **kartu** klíče znovu, prostředí PowerShell nahradí to jenom další odpovídající název rutiny, **Get-Content**.</span><span class="sxs-lookup"><span data-stu-id="b9513-115">If you press **Tab** key again, PowerShell replaces this with the only other matching cmdlet name, **Get-Content**.</span></span>

<span data-ttu-id="b9513-116">Rozšíření tab můžete opakovaně použít na stejném řádku.</span><span class="sxs-lookup"><span data-stu-id="b9513-116">You can use tab expansion repeatedly on the same line.</span></span> <span data-ttu-id="b9513-117">Například můžete použít rozšíření tab na název **Get-Content** rutiny tak, že zadáte:</span><span class="sxs-lookup"><span data-stu-id="b9513-117">For example, you can use tab expansion on the name of the **Get-Content** cmdlet by entering:</span></span>

```
PS> Get-Con<Tab>
```

<span data-ttu-id="b9513-118">Po stisknutí klávesy **kartu** klíče, příkaz rozšíří na:</span><span class="sxs-lookup"><span data-stu-id="b9513-118">When you press the **Tab** key, the command expands to:</span></span>

```
PS> Get-Content
```

<span data-ttu-id="b9513-119">Potom můžete částečně zadejte cestu k souboru protokolu Active instalace a použití rozšíření tab znovu:</span><span class="sxs-lookup"><span data-stu-id="b9513-119">You can then partially specify the path to the Active Setup log file and use tab expansion again:</span></span>

```
PS> Get-Content c:\windows\acts<Tab>
```

<span data-ttu-id="b9513-120">Po stisknutí klávesy **kartu** klíče, příkaz rozšíří na:</span><span class="sxs-lookup"><span data-stu-id="b9513-120">When you press the **Tab** key, the command expands to:</span></span>

```
PS> Get-Content C:\windows\actsetup.log
```

> [!NOTE]
> <span data-ttu-id="b9513-121">Jedním z procesu rozšiřující karty omezení je, že jsou karty vždy interpretován jako pokusy o dokončení slova.</span><span class="sxs-lookup"><span data-stu-id="b9513-121">One limitation of the tab expansion process is that tabs are always interpreted as attempts to complete a word.</span></span> <span data-ttu-id="b9513-122">Pokud zkopírujete a vložíte příklady příkazů do konzoly Powershellu, ujistěte se, že ukázky neobsahuje karet; Pokud ano, mít nepředvídatelné výsledky a nebudou téměř jistě jste zamýšleli.</span><span class="sxs-lookup"><span data-stu-id="b9513-122">If you copy and paste command examples into a PowerShell console, make sure that the sample does not contain tabs; if it does, the results will be unpredictable and will almost certainly not be what you intended.</span></span>