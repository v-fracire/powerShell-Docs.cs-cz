---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Vynětí balíčky
ms.openlocfilehash: fb66fd23dae1d4640056a764c31426f61f56d910
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004019"
---
# <a name="unlisting-packages"></a><span data-ttu-id="13f09-103">Unlisting balíčky</span><span class="sxs-lookup"><span data-stu-id="13f09-103">Unlisting Packages</span></span>

<span data-ttu-id="13f09-104">**Proč je odebrat balíček z Galerie prostředí PowerShell, nejsou viditelné jako možnost?**</span><span class="sxs-lookup"><span data-stu-id="13f09-104">**Why is removing a package from PowerShell Gallery not exposed as an option?**</span></span>

<span data-ttu-id="13f09-105">Galerie prostředí PowerShell nepodporuje uživatelů se odstraňuje natrvalo své balíčky.</span><span class="sxs-lookup"><span data-stu-id="13f09-105">The PowerShell Gallery does not support users permanently deleting their packages.</span></span>
<span data-ttu-id="13f09-106">To umožňuje ostatním uživatelům provádět závislosti na své balíčky bez starostí o možných konce v budoucnu.</span><span class="sxs-lookup"><span data-stu-id="13f09-106">This enables others to take dependencies on your packages without worrying about possible breaks in the future.</span></span>
<span data-ttu-id="13f09-107">Například pokud modulu Pester závisí na modulu Azure a Azure, odebere se z galerie, pak uživatel může již používá modul Pester.</span><span class="sxs-lookup"><span data-stu-id="13f09-107">For example, if the Pester module depends on the Azure module and the Azure module is removed from the gallery, then user can no longer uses the Pester module.</span></span>

<span data-ttu-id="13f09-108">Místo aby odebrala balíček, ale můžete můžete vyjmutí ze seznamu jej místo toho.</span><span class="sxs-lookup"><span data-stu-id="13f09-108">Instead of removing an package, however, you can unlist it instead.</span></span>

<span data-ttu-id="13f09-109">**Co dělá vynětí balíček v galerii prostředí PowerShell dělat?**</span><span class="sxs-lookup"><span data-stu-id="13f09-109">**What does unlisting a package on PowerShell Gallery do?**</span></span>

<span data-ttu-id="13f09-110">Vynětí balíčku, například modul nebo skript ve galerii prostředí PowerShell, bude odebrat z karty balíčky. Kromě toho nesmí být neuvedené v seznamu balíčků zjistitelné pomocí panelu hledání.</span><span class="sxs-lookup"><span data-stu-id="13f09-110">Unlisting a package such as module or script on PowerShell Gallery will remove it from the Packages tab. In addition, unlisted packages will not be discoverable using the search bar.</span></span>
<span data-ttu-id="13f09-111">Jediný způsob, jak si stáhnout balíček neuvedené v seznamu je zadat přesný název a verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="13f09-111">The only way to download an unlisted package is to specify the exact name and version of the package.</span></span>
<span data-ttu-id="13f09-112">Z tohoto důvodu vynětí balíčku nebudou přerušeny. Další moduly nebo skripty, které jsou na ní závislé.</span><span class="sxs-lookup"><span data-stu-id="13f09-112">Because of this, the unlisting of an package will not break other modules or scripts that depend on it.</span></span>

<span data-ttu-id="13f09-113">Vyjmutí ze seznamu vašeho balíčku, najdete na stránce podrobností balíčku a vyberte možnost "odstranit modul.</span><span class="sxs-lookup"><span data-stu-id="13f09-113">To unlist your package, visit the package details page and select 'Delete Module'.</span></span> <span data-ttu-id="13f09-114">Zrušte zaškrtnutí políčka "Uvedené" a klikněte na Uložit.</span><span class="sxs-lookup"><span data-stu-id="13f09-114">Uncheck the 'Listed' checkbox, and click Save.</span></span>

<span data-ttu-id="13f09-115">**Jak můžete balíček odstranit?**</span><span class="sxs-lookup"><span data-stu-id="13f09-115">**How can I remove an package?**</span></span>

<span data-ttu-id="13f09-116">Pokud máte scénáře, kdy je nezbytné odstranění balíčku, obraťte se na správce Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13f09-116">If you experience a scenario where package deletion is necessary, contact the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="13f09-117">Platný odstranění scénáře jsou:</span><span class="sxs-lookup"><span data-stu-id="13f09-117">Valid deletion scenarios are:</span></span>
- <span data-ttu-id="13f09-118">Problémy porušení autorských práv.</span><span class="sxs-lookup"><span data-stu-id="13f09-118">Issues of copyright infringement.</span></span>
- <span data-ttu-id="13f09-119">Balíček obsahuje potenciálně škodlivý obsah.</span><span class="sxs-lookup"><span data-stu-id="13f09-119">Package contains potentially harmful content.</span></span>
- <span data-ttu-id="13f09-120">Balíček obsahuje citlivé údaje.</span><span class="sxs-lookup"><span data-stu-id="13f09-120">Package contains sensitive data.</span></span>

<span data-ttu-id="13f09-121">Odeslat odstranit balíček požadavek správcům Galerie prostředí PowerShell, navštivte stránku s podrobnostmi balíčku a vyberte obraťte se na podporu.</span><span class="sxs-lookup"><span data-stu-id="13f09-121">To submit a Delete Package Request to the PowerShell Gallery Administrators, visit your package's detail page and select Contact Support.</span></span>
