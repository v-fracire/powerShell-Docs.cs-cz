---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Správa vlastníků balíčku
ms.openlocfilehash: 5cf26a7195ac446177cbb7f3a055e8e0a78569cc
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004033"
---
# <a name="managing-package-owners"></a><span data-ttu-id="8cdd4-103">Správa vlastníků balíčku</span><span class="sxs-lookup"><span data-stu-id="8cdd4-103">Managing package owners</span></span>

<span data-ttu-id="8cdd4-104">Vlastnictví balíčku v galerii prostředí PowerShell je definována vydavatele balíček do galerie.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-104">Ownership of a package in the PowerShell Gallery is defined by who published the package to the gallery.</span></span>
<span data-ttu-id="8cdd4-105">Tato metadata je někdy potřeba spravovat nad rámec počáteční balíček publikování, což znamená, že vlastník metadat musí být Měnitelná při samotném balíčku není.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-105">Sometimes this metadata needs to be managed beyond the initial package publishing, which means the owner metadata needs to be mutable while the package itself is not.</span></span>

<span data-ttu-id="8cdd4-106">Všechny vlastníky balíčku se partnerské uzly.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-106">All package owners are peers.</span></span>
<span data-ttu-id="8cdd4-107">To znamená, že všechny vlastníka balíčku můžete publikovat novou verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-107">This means any package owner can publish a new version of an package.</span></span> <span data-ttu-id="8cdd4-108">Také znamená, že všechny vlastníka balíčku můžete odebrat ostatní vlastníka balíčku.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-108">It also means that any package owner can remove any other package owner.</span></span>
<span data-ttu-id="8cdd4-109">Žádný vlastník má více oprávnění než další vlastníky.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-109">No owner has more authority than other owners.</span></span>

## <a name="setting-a-packages-initial-owner"></a><span data-ttu-id="8cdd4-110">Nastavení původního vlastníka balíčku</span><span class="sxs-lookup"><span data-stu-id="8cdd4-110">Setting a Package's Initial Owner</span></span>

<span data-ttu-id="8cdd4-111">Při publikování nového balíčku do Galerie prostředí PowerShell původního vlastníka je definovaný uživatelem, která publikuje balíček.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-111">When a new package is published to PowerShell Gallery, the initial owner is defined by the user that published the package.</span></span> <span data-ttu-id="8cdd4-112">To je určen, rozhraním API, jejichž klíč použila rutinu Publish-Module.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-112">This is determined by whose API key was used in the Publish-Module cmdlet.</span></span>

## <a name="adding-owners"></a><span data-ttu-id="8cdd4-113">Přidávají se vlastníci</span><span class="sxs-lookup"><span data-stu-id="8cdd4-113">Adding Owners</span></span>

<span data-ttu-id="8cdd4-114">Jakmile balíčku se publikoval do Galerie prostředí PowerShell, velmi snadno pozvat další uživatele se vlastníky balíčku.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-114">Once a package has been published to the PowerShell Gallery, it's easy to invite additional users to become owners of a package.</span></span>

1. <span data-ttu-id="8cdd4-115">[Přihlaste se na](https://powershellgallery.com/users/account/LogOn) v galerii prostředí PowerShell pomocí účtu, který je aktuální vlastník balíčku.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-115">[Log on](https://powershellgallery.com/users/account/LogOn) to the PowerShell Gallery with the account that is the current owner of a package.</span></span>
2. <span data-ttu-id="8cdd4-116">Přejděte na stránku balíčku na kartě "Položky", hledání nebo kliknutím na své uživatelské jméno a potom [ **spravovat Moje balíčky**](https://www.powershellgallery.com/account/Packages).</span><span class="sxs-lookup"><span data-stu-id="8cdd4-116">Navigate to a package page using the 'Items' tab, searching, or clicking your username and then [**Manage My Packages**](https://www.powershellgallery.com/account/Packages).</span></span>
3. <span data-ttu-id="8cdd4-117">Po přihlášení se jako vlastník balíčku, je na levé straně klikněte na odkaz Spravovat vlastníky.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-117">When logged on as an package's owner, there is a 'Manage Owners' link on the left side to click.</span></span>
4. <span data-ttu-id="8cdd4-118">Zadejte uživatelské jméno osoby, které chcete přidat jako vlastníka a klikněte na tlačítko 'Přidat'.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-118">Enter the username of the person to add as an owner and click 'Add'.</span></span>
5. <span data-ttu-id="8cdd4-119">E-mailu se pak posílají do nové spoluvlastník jako pozvánku k vlastníka balíčku.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-119">An email is then sent to the new co-owner, as an invitation to become an owner of a package.</span></span>
6. <span data-ttu-id="8cdd4-120">Jakmile se tento uživatel klikne na odkaz, jsou úplné spoluvlastník s úplnou kontrolou nad balíček, včetně možnosti odebírat další uživatele jako vlastníky.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-120">Once that user clicks the link, they are a full co-owner with full control over a package, including the ability to remove other users as owners.</span></span>

<span data-ttu-id="8cdd4-121">**Poznámka:**: dokud nový vlastník potvrdí vlastnictví, jejich *nebudou* uvedení jako vlastníci balíčku.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-121">**NOTE**: Until the new owner confirms ownership, they *will not* be listed as an owner of a package.</span></span>
<span data-ttu-id="8cdd4-122">Při prohlížení **Spravovat vlastníky** stránky, zobrazí se položka "čekající na schválení" aktuální vlastníky.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-122">When viewing the **Manage Owners** page, you will see a "pending approval" entry in the current owners.</span></span>
<span data-ttu-id="8cdd4-123">Je možné odebrat tuto pozvánku; stejně jako další vlastníky je možné odebrat.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-123">That invitation can be removed; just as other owners can be removed.</span></span>
<span data-ttu-id="8cdd4-124">Tento proces pozvánky zabraňuje uživatelům falešně přidávání jiných uživatelů jako vlastníky své balíčky.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-124">This process of invitations prevents users from falsely adding other users as owners of their packages.</span></span>

<span data-ttu-id="8cdd4-125">Mějte na paměti, že metadata "Autoři" je čistě volný text; pouze vlastníci"" jsou řízeny.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-125">Note that the "Authors" metadata is purely freeform text; only "Owners" are controlled.</span></span>


## <a name="removing-owners"></a><span data-ttu-id="8cdd4-126">Odebrat vlastníky</span><span class="sxs-lookup"><span data-stu-id="8cdd4-126">Removing Owners</span></span>

<span data-ttu-id="8cdd4-127">Když balíček obsahuje více vlastníkům a jeden je potřeba odebrat, tento proces je prostý:</span><span class="sxs-lookup"><span data-stu-id="8cdd4-127">When a package has multiple owners and one needs to be removed, the process is simple:</span></span>

1. <span data-ttu-id="8cdd4-128">[Přihlaste se na](https://powershellgallery.com/users/account/LogOn) galerii prostředí PowerShell pomocí účtu, který je aktuální vlastník balíčku.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-128">[Log on](https://powershellgallery.com/users/account/LogOn) to PowerShell Gallery with the account that is the current owner of a package;</span></span>
2. <span data-ttu-id="8cdd4-129">Přejděte na stránku balíčku na kartě balíčky, hledání nebo kliknutím na své uživatelské jméno a potom [ **spravovat Moje balíčky**](https://www.powershellgallery.com/account/Packages).</span><span class="sxs-lookup"><span data-stu-id="8cdd4-129">Navigate to a package page using the Packages tab, searching, or clicking your username and then [**Manage My Packages**](https://www.powershellgallery.com/account/Packages).</span></span>
3. <span data-ttu-id="8cdd4-130">Po přihlášení se jako vlastník balíčku, je na levé straně klikněte na tlačítko; Spravovat vlastníky odkaz</span><span class="sxs-lookup"><span data-stu-id="8cdd4-130">When logged on as a package's owner, there is a 'Manage Owners' link on the left side to click;</span></span>
4. <span data-ttu-id="8cdd4-131">Klikněte na odkaz "Odebrat" vedle vlastníka k odebrání.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-131">Click the 'remove' link next to the owner to be removed.</span></span>



## <a name="transferring-package-ownership"></a><span data-ttu-id="8cdd4-132">Přenos vlastnictví balíčku</span><span class="sxs-lookup"><span data-stu-id="8cdd4-132">Transferring Package Ownership</span></span>

<span data-ttu-id="8cdd4-133">Někdy získáme žádosti o podporu pro přenos vlastnictví balíčku z jednoho uživatele do jiného, ale můžete téměř vždy provést sami.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-133">We sometimes get support requests to transfer package ownership from one user to another, but you can almost always accomplish this yourself.</span></span>
<span data-ttu-id="8cdd4-134">Přenosu vlastnictví z jednoho uživatele je jednoduše kombinace obou funkcí výše.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-134">Transferring ownership from one user to another is simply a combination of the two features above.</span></span>

1. <span data-ttu-id="8cdd4-135">Aktuální vlastník vyzývá nového uživatele, aby se spoluvlastník a nový uživatel přijme pozvánku;</span><span class="sxs-lookup"><span data-stu-id="8cdd4-135">The current owner invites the new user to become a co-owner and the new user accepts the invite;</span></span>
2. <span data-ttu-id="8cdd4-136">Nový uživatel odebere staré uživatele ze seznamu vlastníků.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-136">The new user removes the old user from the list of owners.</span></span>

<span data-ttu-id="8cdd4-137">Tento požadavek má spadají několika formuláře, ale proces funguje stejně.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-137">This request has come in under a couple forms but the process works the same.</span></span>

- <span data-ttu-id="8cdd4-138">Vlastnictví balíčku se mění z jeden vývojář na jiný</span><span class="sxs-lookup"><span data-stu-id="8cdd4-138">The package ownership is changing from one developer to another</span></span>
- <span data-ttu-id="8cdd4-139">Balíček byl náhodnému publikování pomocí k nesprávnému účtu.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-139">The package was accidentally published using the wrong account</span></span>


## <a name="orphaned-packages"></a><span data-ttu-id="8cdd4-140">Osamocené balíčky</span><span class="sxs-lookup"><span data-stu-id="8cdd4-140">Orphaned Packages</span></span>

<span data-ttu-id="8cdd4-141">Došlo k poslední jeden scénář, ale ne mnohokrát.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-141">One last scenario has occurred, but not many times.</span></span>
<span data-ttu-id="8cdd4-142">Balíčky se staly osamocené položky a pouze vlastník účtu balíčku nelze použít k přidání novým vlastníkům.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-142">Packages have become orphans and the only package owner account cannot be used to add new owners.</span></span>
<span data-ttu-id="8cdd4-143">Tady je několik příkladů tohoto scénáře:</span><span class="sxs-lookup"><span data-stu-id="8cdd4-143">Here are some examples of this scenario:</span></span>

- <span data-ttu-id="8cdd4-144">Vlastníka účtu je spojen s e-mailovou adresu, která už existuje a uživatel zapomněl svoje heslo</span><span class="sxs-lookup"><span data-stu-id="8cdd4-144">The owner's account is associated with an email address that no longer exists and the user has forgotten their password</span></span>
- <span data-ttu-id="8cdd4-145">Registrovaný vlastník opustil společnost, která vytvoří balíček a je nedostupné k aktualizaci balíčku vlastnictví</span><span class="sxs-lookup"><span data-stu-id="8cdd4-145">The registered owner has left the company that produces the package and cannot be reached to update the package ownership</span></span>
- <span data-ttu-id="8cdd4-146">Kvůli chybě, která má vliv jenom na několik balíčků balíček je nějakým způsobem ownerless v galerii</span><span class="sxs-lookup"><span data-stu-id="8cdd4-146">Due to a bug that has only affected a handful of packages, the package is somehow ownerless on the gallery</span></span>

<span data-ttu-id="8cdd4-147">Správci Galerie prostředí PowerShell můžete přistupovat k Spravovat vlastníky propojení pro všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-147">The PowerShell Gallery Administrators can access the 'Manage Owners' link for any package.</span></span>
<span data-ttu-id="8cdd4-148">Pokud jsou právoplatného vlastníka balíčku a kontaktovat aktuálního vlastníka k získání vlastnictví oprávnění, použijte odkaz "Ohlášení zneužití" v galerii k dosažení správci Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-148">If you are the rightful owner of a package and cannot reach the current owner to gain ownership permissions, then use the 'Report Abuse' link on the gallery to reach the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="8cdd4-149">Pak budeme postupovat procesu ověřit vlastnictví balíčku.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-149">We will then follow a process to verify your ownership of the package.</span></span>
<span data-ttu-id="8cdd4-150">Pokud vyhodnotíme, že by měl být vlastníka balíčku, budeme používali odkaz Spravovat vlastníky pro tento balíček a odeslat pozvánku pro stát vlastníkem.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-150">If we determine you should be an owner of the package, we will use the 'Manage Owners' link for the package ourselves and send you the invite to become an owner.</span></span>
<span data-ttu-id="8cdd4-151">Pouze Uděláme to po ověření, že by měl být vlastníkem a tento proces se liší podle okolností.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-151">We will only do this after verifying that you should be an owner and the process for this varies by circumstances.</span></span>
<span data-ttu-id="8cdd4-152">Častým použije adresu URL projektu daného balíčku hledal způsob, jak se obraťte na správce projektu, ale můžeme také používat Twitter, e-mailu nebo jiným způsobem pro kontaktování Vlastník projektu.</span><span class="sxs-lookup"><span data-stu-id="8cdd4-152">Often times, we will use the package's Project URL to find a way to contact the project owner, but we may also use Twitter, Email, or other means for contacting the project owner.</span></span>
