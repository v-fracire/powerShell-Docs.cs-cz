---
ms.date: 09/10/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Správa klíčů rozhraní API
ms.openlocfilehash: 954eb27c25babdb8efe50c13caf5f2d287c6b3e3
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002509"
---
# <a name="managing-api-keys"></a><span data-ttu-id="84f4b-103">Správa klíčů rozhraní API</span><span class="sxs-lookup"><span data-stu-id="84f4b-103">Managing API keys</span></span>

<span data-ttu-id="84f4b-104">Galerie prostředí PowerShell podporuje vytváření více klíčů rozhraní API pro podporu rozsahu publikování požadavky.</span><span class="sxs-lookup"><span data-stu-id="84f4b-104">The PowerShell Gallery supports creating multiple API keys to support a range of publishing requirements.</span></span> <span data-ttu-id="84f4b-105">Klíč rozhraní API můžete použít na jeden nebo více balíčků, udělí zvláštní oprávnění a má datum vypršení platnosti.</span><span class="sxs-lookup"><span data-stu-id="84f4b-105">An API key can apply to one or more packages, grants specific privileges, and has an expiration date.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84f4b-106">Uživatelé, kteří publikují do Galerie prostředí PowerShell před zavedením s vymezeným oborem klíče rozhraní API budou mít "API key úplný přístup".</span><span class="sxs-lookup"><span data-stu-id="84f4b-106">Users who published to the PowerShell Gallery prior to the introduction of scoped API keys will have a "Full access API key".</span></span> <span data-ttu-id="84f4b-107">Vylepšení zabezpečení integrované s vymezeným oborem klíče rozhraní API není nutné úplné přístupové klíče.</span><span class="sxs-lookup"><span data-stu-id="84f4b-107">The full access keys do not have the security improvements built into scoped API keys.</span></span> <span data-ttu-id="84f4b-108">Úplné přístupové klávesy nikdy vyprší platnost a platí pro všechno, co vlastněné uživatelem.</span><span class="sxs-lookup"><span data-stu-id="84f4b-108">The full access keys never expires and apply to everything owned by the user.</span></span> <span data-ttu-id="84f4b-109">Pokud odstraníte tento klíč, nemůže být obnovena.</span><span class="sxs-lookup"><span data-stu-id="84f4b-109">If you delete this key, it cannot be recreated.</span></span>

<span data-ttu-id="84f4b-110">Následující obrázek ukazuje možnosti dostupné při vytváření oboru klíč rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="84f4b-110">The following image shows the options available when creating a scoped API key.</span></span>

![Vytvoření klíče rozhraní API](../../Images/PSGallery_KeyScoped.png)

<span data-ttu-id="84f4b-112">V tomto příkladu jsme vytvořili klíč rozhraní API s názvem **AzureRMDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="84f4b-112">In this example, we created an API key named **AzureRMDataFactory**.</span></span> <span data-ttu-id="84f4b-113">Tato hodnota klíče je možné tak, aby nabízel balíčků s názvy, které začínají řetězcem "AzureRM.DataFactory" a je platný 365 dní.</span><span class="sxs-lookup"><span data-stu-id="84f4b-113">This key value can be used to push packages with names that begin with 'AzureRM.DataFactory' and is valid for 365 days.</span></span> <span data-ttu-id="84f4b-114">Toto je typický scénář, když pracují různé týmy v rámci stejné organizace na různých balíčcích.</span><span class="sxs-lookup"><span data-stu-id="84f4b-114">This is a typical scenario when different teams within the same organization work on different packages.</span></span> <span data-ttu-id="84f4b-115">Členové týmu mají klíč, který udělí oprávnění pro konkrétní balíček, který pracují na.</span><span class="sxs-lookup"><span data-stu-id="84f4b-115">The members of the team have a key that grants them privileges for the specific package they work on.</span></span>
<span data-ttu-id="84f4b-116">Hodnota vypršení platnosti brání použití zastaralé či zapomenutí klíčů.</span><span class="sxs-lookup"><span data-stu-id="84f4b-116">The expiration value prevents the use of stale or forgotten keys.</span></span>

## <a name="using-glob-patterns"></a><span data-ttu-id="84f4b-117">Pomocí glob vzory</span><span class="sxs-lookup"><span data-stu-id="84f4b-117">Using glob patterns</span></span>

<span data-ttu-id="84f4b-118">Pokud pracujete ve více balíčků, můžete použít vzorů podpory zástupných znaků tak, aby odpovídaly více balíčků jako skupinu.</span><span class="sxs-lookup"><span data-stu-id="84f4b-118">If you work on multiple packages, you can use globbing patterns to match multiple packages as a group.</span></span> <span data-ttu-id="84f4b-119">Oprávnění ke klíči rozhraní API platí pro všechny nové balíčky pro odpovídající vzoru glob.</span><span class="sxs-lookup"><span data-stu-id="84f4b-119">API key permissions apply to all new packages matching the glob pattern.</span></span> <span data-ttu-id="84f4b-120">Například v předchozím příkladu používá **Glob vzor** hodnotu "AzureRM.DataFactory\*".</span><span class="sxs-lookup"><span data-stu-id="84f4b-120">For example, the previous example uses a **Glob Pattern** value of 'AzureRM.DataFactory\*'.</span></span> <span data-ttu-id="84f4b-121">Můžete odeslat balíček s názvem pomocí tohoto klíče, protože balíček shoduje se vzorem glob AzureRm.DataFactoryV2.Netcore.</span><span class="sxs-lookup"><span data-stu-id="84f4b-121">You can push a package named 'AzureRm.DataFactoryV2.Netcore' using this key since the package matches the glob pattern.</span></span>

## <a name="create-api-keys-securely"></a><span data-ttu-id="84f4b-122">Vytvořte bezpečně klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="84f4b-122">Create API keys securely</span></span>

<span data-ttu-id="84f4b-123">Pro zabezpečení nově vytvořený hodnotu klíče se nikdy zobrazí na obrazovce a je dostupná jenom při tlačítka pro kopírování, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="84f4b-123">For security, a newly created key value is never shown on the screen and is only available with the Copy button, as shown below.</span></span>

![Získání nové hodnoty klíče rozhraní API](../../Images/PSGallery_CopyCreatedKey.png)

> [!IMPORTANT]
> <span data-ttu-id="84f4b-125">Kopírovat můžete pouze hodnotu klíče rozhraní API ihned po vytvoření nebo aktualizaci.</span><span class="sxs-lookup"><span data-stu-id="84f4b-125">You can only copy the API key value immediately after creating or refreshing it.</span></span> <span data-ttu-id="84f4b-126">Se nezobrazí a nebudete mít přístup znovu po aktualizaci stránky.</span><span class="sxs-lookup"><span data-stu-id="84f4b-126">It will not be displayed, and will not be accessible again after the page is refreshed.</span></span> <span data-ttu-id="84f4b-127">Pokud ztratíte hodnota klíče, musíte použít znovu vygenerovat klíč a zkopírujte klíč, až se znovu vygeneroval.</span><span class="sxs-lookup"><span data-stu-id="84f4b-127">If you lose the key value, you must use Regenerate, and copy the key after it is regenerated.</span></span>

## <a name="key-permissions-and-expiration"></a><span data-ttu-id="84f4b-128">Oprávnění ke klíči a vypršení platnosti</span><span class="sxs-lookup"><span data-stu-id="84f4b-128">Key permissions and expiration</span></span>

<span data-ttu-id="84f4b-129">S vymezeným oborem klíče rozhraní API můžete přiřadit některé z těchto oprávnění:</span><span class="sxs-lookup"><span data-stu-id="84f4b-129">Scoped API keys can assign any of the following permissions:</span></span>

- <span data-ttu-id="84f4b-130">Vložit nové balíčky</span><span class="sxs-lookup"><span data-stu-id="84f4b-130">Push new packages</span></span>
- <span data-ttu-id="84f4b-131">Vložit nový nebo aktualizovat balíčky</span><span class="sxs-lookup"><span data-stu-id="84f4b-131">Push new or update packages</span></span>
- <span data-ttu-id="84f4b-132">Vyjmutí ze seznamu balíčků</span><span class="sxs-lookup"><span data-stu-id="84f4b-132">Unlist packages</span></span>

<span data-ttu-id="84f4b-133">Každý nový klíč má vypršení platnosti.</span><span class="sxs-lookup"><span data-stu-id="84f4b-133">Every new key has an expiration.</span></span> <span data-ttu-id="84f4b-134">Ve dnech se měří hodnota vypršení platnosti.</span><span class="sxs-lookup"><span data-stu-id="84f4b-134">The expiration value is measured in days.</span></span> <span data-ttu-id="84f4b-135">Možné hodnoty pro vypršení platnosti jsou:</span><span class="sxs-lookup"><span data-stu-id="84f4b-135">The possible values for expiration are:</span></span>

- <span data-ttu-id="84f4b-136">1 den</span><span class="sxs-lookup"><span data-stu-id="84f4b-136">1 day</span></span>
- <span data-ttu-id="84f4b-137">90 dnů</span><span class="sxs-lookup"><span data-stu-id="84f4b-137">90 days</span></span>
- <span data-ttu-id="84f4b-138">180 dnů</span><span class="sxs-lookup"><span data-stu-id="84f4b-138">180 days</span></span>
- <span data-ttu-id="84f4b-139">270 dní</span><span class="sxs-lookup"><span data-stu-id="84f4b-139">270 days</span></span>
- <span data-ttu-id="84f4b-140">365 dnů (výchozí)</span><span class="sxs-lookup"><span data-stu-id="84f4b-140">365 days (default)</span></span>

<span data-ttu-id="84f4b-141">Tato nastavení nelze změnit po vytvoření klíče.</span><span class="sxs-lookup"><span data-stu-id="84f4b-141">These settings cannot be changed once the key is created.</span></span> <span data-ttu-id="84f4b-142">Nelze vytvořit nový klíč, který nikdy nevyprší.</span><span class="sxs-lookup"><span data-stu-id="84f4b-142">You cannot create a new key that never expires.</span></span>

## <a name="editing-and-deleting-existing-api-keys"></a><span data-ttu-id="84f4b-143">Úpravy a odstranění existující klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="84f4b-143">Editing and deleting existing API keys</span></span>

<span data-ttu-id="84f4b-144">Můžete změnit některá nastavení existujícího klíče.</span><span class="sxs-lookup"><span data-stu-id="84f4b-144">You can change some settings of an existing key.</span></span> <span data-ttu-id="84f4b-145">Jak již bylo uvedeno výše nelze změnit obor zabezpečení pro existující klíč rozhraní API nebo změnit vypršení platnosti.</span><span class="sxs-lookup"><span data-stu-id="84f4b-145">As previously noted, you cannot modify the security scope for an existing API key or change the expiration.</span></span> <span data-ttu-id="84f4b-146">Změnit možnosti můžete vidět na následujícím snímku obrazovky:</span><span class="sxs-lookup"><span data-stu-id="84f4b-146">The changeable options are shown in the following screenshot:</span></span>

![Získání nové hodnoty klíče rozhraní API](../../Images/PSGallery_EditAPIKey.png)

<span data-ttu-id="84f4b-148">Chcete-li změnit balíčky řídí klíč, můžete zvolit jednotlivé balíčky ze seznamu nebo změnit glob vzor.</span><span class="sxs-lookup"><span data-stu-id="84f4b-148">To change the packages controlled by a key, you can choose individual packages from the list or change the glob pattern.</span></span>

<span data-ttu-id="84f4b-149">Kliknutím na **znovu vygenerovat** vytvoří novou hodnotu klíče.</span><span class="sxs-lookup"><span data-stu-id="84f4b-149">Clicking **Regenerate** creates a new key value.</span></span> <span data-ttu-id="84f4b-150">Stejně jako při původně vytvořil klíč, je třeba **kopírování** hodnotu klíče ihned po jeho aktualizace.</span><span class="sxs-lookup"><span data-stu-id="84f4b-150">Just like when you initially created the key, you must **Copy** the key value immediately after updating it.</span></span> <span data-ttu-id="84f4b-151">**Kopírování** možnost není k dispozici po opuštění této stránky.</span><span class="sxs-lookup"><span data-stu-id="84f4b-151">The **Copy** option is not available once you leave this page.</span></span>

<span data-ttu-id="84f4b-152">Kliknutím na **odstranit** zobrazí potvrzovací zpráva.</span><span class="sxs-lookup"><span data-stu-id="84f4b-152">Clicking **Delete** displays a confirmation message.</span></span> <span data-ttu-id="84f4b-153">Po odstranění klíče nepoužitelné.</span><span class="sxs-lookup"><span data-stu-id="84f4b-153">Once a key is deleted, it will be unusable.</span></span>

## <a name="key-expiration"></a><span data-ttu-id="84f4b-154">Vypršení platnosti klíče</span><span class="sxs-lookup"><span data-stu-id="84f4b-154">Key expiration</span></span>

<span data-ttu-id="84f4b-155">Deset dní před vypršením platnosti, galerie prostředí PowerShell odešle e-mail s upozorněním držitele účtu, klíč rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="84f4b-155">Ten days before the expiration, the PowerShell Gallery sends a warning email the account holder of the API key.</span></span> <span data-ttu-id="84f4b-156">Po vypršení platnosti klíčem nepoužitelné.</span><span class="sxs-lookup"><span data-stu-id="84f4b-156">After expiration, the key is unusable.</span></span> <span data-ttu-id="84f4b-157">Upozornění se zobrazí v horní části stránky správy klíčů rozhraní API, zobrazení, které klíče už nejsou platné.</span><span class="sxs-lookup"><span data-stu-id="84f4b-157">A warning message is displayed at the top of the API key management page showing which keys are no longer valid.</span></span> <span data-ttu-id="84f4b-158">Můžete generovat nové hodnoty klíče.</span><span class="sxs-lookup"><span data-stu-id="84f4b-158">You can generate a new key value.</span></span>
