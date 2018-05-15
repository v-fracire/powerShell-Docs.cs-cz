---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery
title: Vynětí položek ze seznamu
ms.openlocfilehash: 35dcd283ddace5aec62d692b0ede12ae0bada765
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="unlisting-items"></a><span data-ttu-id="bdd6d-103">Vynětí položek ze seznamu</span><span class="sxs-lookup"><span data-stu-id="bdd6d-103">Unlisting items</span></span>

<span data-ttu-id="bdd6d-104">**Proč je odebrání položky z Galerie prostředí PowerShell, nejsou viditelné jako možnost?**</span><span class="sxs-lookup"><span data-stu-id="bdd6d-104">**Why is removing an item from PowerShell Gallery not exposed as an option?**</span></span>

<span data-ttu-id="bdd6d-105">Galerie prostředí PowerShell nepodporuje uživatele trvale odstranit jejich položky.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-105">The PowerShell Gallery does not support users permanently deleting their items.</span></span>
<span data-ttu-id="bdd6d-106">To umožňuje ostatním uživatelům trvat závislosti na vaší položky bez obav o možných zalomení v budoucnu.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-106">This enables others to take dependencies on your items without worrying about possible breaks in the future.</span></span>
<span data-ttu-id="bdd6d-107">Například pokud modul Pester závisí na modulu Azure a Azure, odebere se z galerie, pak uživatel může už používá modul Pester.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-107">For example, if the Pester module depends on the Azure module and the Azure module is removed from the gallery, then user can no longer uses the Pester module.</span></span>

<span data-ttu-id="bdd6d-108">Místo odebírání položku, ale můžete můžete unlist ho místo.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-108">Instead of removing an item, however, you can unlist it instead.</span></span>

<span data-ttu-id="bdd6d-109">**Jaké jsou unlisting položku v galerii prostředí PowerShell se?**</span><span class="sxs-lookup"><span data-stu-id="bdd6d-109">**What does unlisting an item on PowerShell Gallery do?**</span></span>

<span data-ttu-id="bdd6d-110">Unlisting položku jako je například modul nebo skriptu v galerii prostředí PowerShell ji odeberte z karty položky. Kromě toho nebude neuvedené položky zjistitelný pomocí panelu vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-110">Unlisting an item such as module or script on PowerShell Gallery will remove it from the Items tab. In addition, unlisted items will not be discoverable using the search bar.</span></span>
<span data-ttu-id="bdd6d-111">Jediný způsob, jak stáhnout neuvedené položku je zadejte přesně název a verzi položky.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-111">The only way to download an unlisted item is to specify the exact name and version of the item.</span></span>
<span data-ttu-id="bdd6d-112">Z tohoto důvodu nebude unlisting položku Rozdělit další moduly nebo skripty, které jsou na ní závislé.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-112">Because of this, the unlisting of an item will not break other modules or scripts that depend on it.</span></span>

<span data-ttu-id="bdd6d-113">Chcete-li unlist vaší položky, naleznete na stránce Podrobnosti položky a vyberte Odstranit položku.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-113">To unlist your item, visit the item details page and select 'Delete Item'.</span></span> <span data-ttu-id="bdd6d-114">Zrušte zaškrtnutí políčka 'uvedené a klikněte na tlačítko Uložit.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-114">Uncheck the 'Listed' checkbox, and click Save.</span></span>

<span data-ttu-id="bdd6d-115">**Jak můžete odebrat položku?**</span><span class="sxs-lookup"><span data-stu-id="bdd6d-115">**How can I remove an item?**</span></span>

<span data-ttu-id="bdd6d-116">Pokud dojde k scénář, kde je nutné odstranění položky, obraťte se na správce Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-116">If you experience a scenario where item deletion is necessary, contact the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="bdd6d-117">Platný odstranění scénáře jsou:</span><span class="sxs-lookup"><span data-stu-id="bdd6d-117">Valid deletion scenarios are:</span></span>
- <span data-ttu-id="bdd6d-118">Problémy věci porušení autorských práv.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-118">Issues of copyright infringement.</span></span>
- <span data-ttu-id="bdd6d-119">Položka obsahuje potenciálně nebezpečný obsah.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-119">Item contains potentially harmful content.</span></span>
- <span data-ttu-id="bdd6d-120">Položka obsahuje citlivá data.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-120">Item contains sensitive data.</span></span>

<span data-ttu-id="bdd6d-121">Odeslání odstranit položku požadavku na správcům Galerie prostředí PowerShell, navštivte stránku s podrobnostmi položky na a vyberte obraťte se na podporu.</span><span class="sxs-lookup"><span data-stu-id="bdd6d-121">To submit a Delete Item Request to the PowerShell Gallery Administrators, visit your item's detail page and select Contact Support.</span></span>