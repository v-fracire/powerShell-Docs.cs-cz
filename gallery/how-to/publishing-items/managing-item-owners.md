---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutiny, psgallery
title: Správa vlastníků položek
ms.openlocfilehash: 10d2a433253162847028e157b5bac47b23406469
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="managing-item-owners"></a><span data-ttu-id="c7c56-103">Správa vlastníků položek</span><span class="sxs-lookup"><span data-stu-id="c7c56-103">Managing item owners</span></span>

<span data-ttu-id="c7c56-104">Vlastnictví položky v galerii prostředí PowerShell je definována položka kdo publikoval do galerie.</span><span class="sxs-lookup"><span data-stu-id="c7c56-104">Ownership of an item in the PowerShell Gallery is defined by who published the item to the gallery.</span></span>
<span data-ttu-id="c7c56-105">V některých případech je potřeba spravovat nad rámec publikování počáteční položky, což znamená, že metadata vlastník musí být měnitelný při samotnou položku není tato metadata.</span><span class="sxs-lookup"><span data-stu-id="c7c56-105">Sometimes this metadata needs to be managed beyond the initial item publishing, which means the owner metadata needs to be mutable while the item itself is not.</span></span>

<span data-ttu-id="c7c56-106">Všechny položky vlastníky jsou partnerské uzly.</span><span class="sxs-lookup"><span data-stu-id="c7c56-106">All item owners are peers.</span></span>
<span data-ttu-id="c7c56-107">To znamená, že všechny položky vlastníka můžete publikovat novou verzi položky.</span><span class="sxs-lookup"><span data-stu-id="c7c56-107">This means any item owner can publish a new version of an item.</span></span> <span data-ttu-id="c7c56-108">Taky to znamená, že vlastník všechny položky můžete odebrat všechny ostatní položky vlastníka.</span><span class="sxs-lookup"><span data-stu-id="c7c56-108">It also means that any item owner can remove any other item owner.</span></span>
<span data-ttu-id="c7c56-109">Vlastník má další autority než ostatní vlastníky.</span><span class="sxs-lookup"><span data-stu-id="c7c56-109">No owner has more authority than other owners.</span></span>

## <a name="setting-an-items-initial-owner"></a><span data-ttu-id="c7c56-110">Nastavení počáteční vlastník položky</span><span class="sxs-lookup"><span data-stu-id="c7c56-110">Setting an Item's Initial Owner</span></span>

<span data-ttu-id="c7c56-111">Při publikování nové položky galerie prostředí PowerShell, vlastník počáteční definované uživatelem, který publikované položky.</span><span class="sxs-lookup"><span data-stu-id="c7c56-111">When a new item is published to PowerShell Gallery, the initial owner is defined by the user that published the item.</span></span> <span data-ttu-id="c7c56-112">To je určen, jejichž rozhraní API klíče v rutině modulu publikovat.</span><span class="sxs-lookup"><span data-stu-id="c7c56-112">This is determined by whose API key was used in the Publish-Module cmdlet.</span></span>

## <a name="adding-owners"></a><span data-ttu-id="c7c56-113">Přidání vlastníky</span><span class="sxs-lookup"><span data-stu-id="c7c56-113">Adding Owners</span></span>

<span data-ttu-id="c7c56-114">Jakmile položku se publikoval do Galerie prostředí PowerShell, je snadné pozvaným dalším uživatelům stane vlastníci položky.</span><span class="sxs-lookup"><span data-stu-id="c7c56-114">Once an item has been published to the PowerShell Gallery, it's easy to invite additional users to become owners of an item.</span></span>

1. <span data-ttu-id="c7c56-115">[Přihlaste se](https://powershellgallery.com/users/account/LogOn) do Galerie prostředí PowerShell pomocí účtu, který je vlastníkem aktuální položky.</span><span class="sxs-lookup"><span data-stu-id="c7c56-115">[Log on](https://powershellgallery.com/users/account/LogOn) to the PowerShell Gallery with the account that is the current owner of an item.</span></span>
2. <span data-ttu-id="c7c56-116">Přejděte na stránku položku na kartě "položky, hledání nebo kliknutím na své uživatelské jméno a potom [ **spravovat Moje položky**](https://www.powershellgallery.com/account/Packages).</span><span class="sxs-lookup"><span data-stu-id="c7c56-116">Navigate to an item page using the 'Items' tab, searching, or clicking your username and then [**Manage My Items**](https://www.powershellgallery.com/account/Packages).</span></span>
3. <span data-ttu-id="c7c56-117">Při přihlášení se jako vlastník položky, je na levé straně klikněte na odkaz Spravovat vlastníky.</span><span class="sxs-lookup"><span data-stu-id="c7c56-117">When logged on as an item's owner, there is a 'Manage Owners' link on the left side to click.</span></span>
4. <span data-ttu-id="c7c56-118">Zadejte uživatelské jméno osoby, k přidání jako vlastníka a klikněte na tlačítko "Přidat".</span><span class="sxs-lookup"><span data-stu-id="c7c56-118">Enter the username of the person to add as an owner and click 'Add'.</span></span>
5. <span data-ttu-id="c7c56-119">E-mailu se pak posílají do nové spoluvlastník jako Pozvánka se vlastníkem položku.</span><span class="sxs-lookup"><span data-stu-id="c7c56-119">An email is then sent to the new co-owner, as an invitation to become an owner of an item.</span></span>
6. <span data-ttu-id="c7c56-120">Jakmile tento uživatel klikne na odkaz, nejsou úplné spoluvlastník s plnou kontrolu nad položku, včetně možnosti odstranit další uživatele jako vlastníci.</span><span class="sxs-lookup"><span data-stu-id="c7c56-120">Once that user clicks the link, they are a full co-owner with full control over an item, including the ability to remove other users as owners.</span></span>

<span data-ttu-id="c7c56-121">**Poznámka:**: dokud nový vlastník potvrdí vlastnictví, jejich *nikoli* uveden jako vlastníka položky.</span><span class="sxs-lookup"><span data-stu-id="c7c56-121">**NOTE**: Until the new owner confirms ownership, they *will not* be listed as an owner of an item.</span></span>
<span data-ttu-id="c7c56-122">Při zobrazení **Spravovat vlastníky** stránky, zobrazí se položka "čekající na schválení" v aktuální vlastníky.</span><span class="sxs-lookup"><span data-stu-id="c7c56-122">When viewing the **Manage Owners** page, you will see a "pending approval" entry in the current owners.</span></span>
<span data-ttu-id="c7c56-123">Tuto pozvánku lze odebrat; stejně jako ostatní vlastníků lze odebrat.</span><span class="sxs-lookup"><span data-stu-id="c7c56-123">That invitation can be removed; just as other owners can be removed.</span></span>
<span data-ttu-id="c7c56-124">Tento proces pozvánek zabrání uživatelům v nesprávně jako vlastníci jejich položek přidávání jiných uživatelů.</span><span class="sxs-lookup"><span data-stu-id="c7c56-124">This process of invitations prevents users from falsely adding other users as owners of their items.</span></span>

<span data-ttu-id="c7c56-125">Upozorňujeme, že metadata "Autoři" je čistě volného tvaru textu. jsou ovládaná pouze "vlastníci".</span><span class="sxs-lookup"><span data-stu-id="c7c56-125">Note that the "Authors" metadata is purely freeform text; only "Owners" are controlled.</span></span>


## <a name="removing-owners"></a><span data-ttu-id="c7c56-126">Odebrání vlastníky</span><span class="sxs-lookup"><span data-stu-id="c7c56-126">Removing Owners</span></span>

<span data-ttu-id="c7c56-127">Pokud má více vlastníky, položku a jedna je potřeba odstranit, proces je jednoduchý:</span><span class="sxs-lookup"><span data-stu-id="c7c56-127">When an item has multiple owners and one needs to be removed, the process is simple:</span></span>

1. <span data-ttu-id="c7c56-128">[Přihlaste se](https://powershellgallery.com/users/account/LogOn) do Galerie prostředí PowerShell pomocí účtu, který je vlastníkem aktuální položky;</span><span class="sxs-lookup"><span data-stu-id="c7c56-128">[Log on](https://powershellgallery.com/users/account/LogOn) to PowerShell Gallery with the account that is the current owner of an item;</span></span>
2. <span data-ttu-id="c7c56-129">Přejděte na stránku položek pomocí karty položek, hledání nebo kliknutím na své uživatelské jméno a potom [ **spravovat Moje položky**](https://www.powershellgallery.com/account/Packages).</span><span class="sxs-lookup"><span data-stu-id="c7c56-129">Navigate to an item page using the Items tab, searching, or clicking your username and then [**Manage My Items**](https://www.powershellgallery.com/account/Packages).</span></span>
3. <span data-ttu-id="c7c56-130">Při přihlášení se jako vlastník položky, je Spravovat vlastníky odkaz na levé straně klikněte na;</span><span class="sxs-lookup"><span data-stu-id="c7c56-130">When logged on as an item's owner, there is a 'Manage Owners' link on the left side to click;</span></span>
4. <span data-ttu-id="c7c56-131">Klikněte na odkaz "Odebrat" vedle vlastník odeberou.</span><span class="sxs-lookup"><span data-stu-id="c7c56-131">Click the 'remove' link next to the owner to be removed.</span></span>



## <a name="transferring-item-ownership"></a><span data-ttu-id="c7c56-132">Převedení vlastnictví položky</span><span class="sxs-lookup"><span data-stu-id="c7c56-132">Transferring Item Ownership</span></span>

<span data-ttu-id="c7c56-133">V některých případech nám získat žádosti o podporu pro přenos položky vlastnictví z jednoho uživatele do jiného, ale můžete provést téměř vždy sobě.</span><span class="sxs-lookup"><span data-stu-id="c7c56-133">We sometimes get support requests to transfer item ownership from one user to another, but you can almost always accomplish this yourself.</span></span>
<span data-ttu-id="c7c56-134">Převedení vlastnictví z jednoho uživatele je jednoduše kombinací tyto dvě funkce výše.</span><span class="sxs-lookup"><span data-stu-id="c7c56-134">Transferring ownership from one user to another is simply a combination of the two features above.</span></span>

1. <span data-ttu-id="c7c56-135">Aktuální vlastník žádostí nového uživatele se spoluvlastník a nový uživatel přijme podmínky pozvání;</span><span class="sxs-lookup"><span data-stu-id="c7c56-135">The current owner invites the new user to become a co-owner and the new user accepts the invite;</span></span>
2. <span data-ttu-id="c7c56-136">Nový uživatel odebere staré uživatele ze seznamu vlastníků.</span><span class="sxs-lookup"><span data-stu-id="c7c56-136">The new user removes the old user from the list of owners.</span></span>

<span data-ttu-id="c7c56-137">Tento požadavek zase pod několik forms ale proces funguje stejně.</span><span class="sxs-lookup"><span data-stu-id="c7c56-137">This request has come in under a couple forms but the process works the same.</span></span>

- <span data-ttu-id="c7c56-138">Vlastnictví položky se mění z jedné vývojáře do jiného</span><span class="sxs-lookup"><span data-stu-id="c7c56-138">The item ownership is changing from one developer to another</span></span>
- <span data-ttu-id="c7c56-139">Položka byla omylem publikována pomocí nesprávného účtu</span><span class="sxs-lookup"><span data-stu-id="c7c56-139">The item was accidentally published using the wrong account</span></span>


## <a name="orphaned-items"></a><span data-ttu-id="c7c56-140">Osamocené položky</span><span class="sxs-lookup"><span data-stu-id="c7c56-140">Orphaned Items</span></span>

<span data-ttu-id="c7c56-141">Došlo k jedné posledním scénáři, ale není tolikrát, kolikrát.</span><span class="sxs-lookup"><span data-stu-id="c7c56-141">One last scenario has occurred, but not many times.</span></span>
<span data-ttu-id="c7c56-142">Položky se staly osamocené položky a jenom vlastník účtu položky nelze použít k přidání nové vlastníky.</span><span class="sxs-lookup"><span data-stu-id="c7c56-142">Items have become orphans and the only item owner account cannot be used to add new owners.</span></span>
<span data-ttu-id="c7c56-143">Zde je několik příkladů tohoto scénáře:</span><span class="sxs-lookup"><span data-stu-id="c7c56-143">Here are some examples of this scenario:</span></span>

- <span data-ttu-id="c7c56-144">Účet vlastníka souvisí s e-mailovou adresu, která už existuje a uživatel zapomene své heslo</span><span class="sxs-lookup"><span data-stu-id="c7c56-144">The owner's account is associated with an email address that no longer exists and the user has forgotten their password</span></span>
- <span data-ttu-id="c7c56-145">Registrovaný vlastník opustil společnost, která vytváří položky a nelze získat přístup k aktualizaci položky vlastnictví</span><span class="sxs-lookup"><span data-stu-id="c7c56-145">The registered owner has left the company that produces the item and cannot be reached to update the item ownership</span></span>
- <span data-ttu-id="c7c56-146">Z důvodu chyb, který má vliv pouze několik položek položka je nějakým způsobem ownerless na Galerie</span><span class="sxs-lookup"><span data-stu-id="c7c56-146">Due to a bug that has only affected a handful of items, the item is somehow ownerless on the gallery</span></span>

<span data-ttu-id="c7c56-147">Správci Galerie prostředí PowerShell můžete přístup k Spravovat vlastníky odkazu pro libovolnou položku.</span><span class="sxs-lookup"><span data-stu-id="c7c56-147">The PowerShell Gallery Administrators can access the 'Manage Owners' link for any item.</span></span>
<span data-ttu-id="c7c56-148">Pokud jste jeho oprávněný vlastník položku a nemůže kontaktovat aktuální vlastník pro získání vlastnictví oprávnění, pak použijte odkaz 'Oznámení zneužití' v galerii k dosažení správci Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7c56-148">If you are the rightful owner of a item and cannot reach the current owner to gain ownership permissions, then use the 'Report Abuse' link on the gallery to reach the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="c7c56-149">Nemůžeme se potom postupujte podle procesu ověřit vlastnictví položky.</span><span class="sxs-lookup"><span data-stu-id="c7c56-149">We will then follow a process to verify your ownership of the item.</span></span>
<span data-ttu-id="c7c56-150">Pokud jsme určit, že by měla být vlastníkem položky, jsme použije Spravovat vlastníky odkaz pro položku označována a poslat pozvání k vlastníka.</span><span class="sxs-lookup"><span data-stu-id="c7c56-150">If we determine you should be an owner of the item, we will use the 'Manage Owners' link for the item ourselves and send you the invite to become an owner.</span></span>
<span data-ttu-id="c7c56-151">Pouze Uděláme to po ověření, že by měl být vlastníka a pro tento proces se liší podle okolností.</span><span class="sxs-lookup"><span data-stu-id="c7c56-151">We will only do this after verifying that you should be an owner and the process for this varies by circumstances.</span></span>
<span data-ttu-id="c7c56-152">Častým použijeme adresy URL projektu položky najít způsob, jak obraťte se na vlastníka projektu, ale můžeme také používat Twitter, e-mailu nebo jiným způsobem pro kontaktování vlastníka projektu.</span><span class="sxs-lookup"><span data-stu-id="c7c56-152">Often times, we will use the item's Project URL to find a way to contact the project owner, but we may also use Twitter, Email, or other means for contacting the project owner.</span></span>