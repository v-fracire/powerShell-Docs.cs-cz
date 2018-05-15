---
ms.date: 03/27/2018
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, psgallery, GDPR
title: Dodržování předpisů GDPR Galerie prostředí PowerShell
ms.openlocfilehash: 0a9e76325a2a5cf8f509e1a6317c8ed88d133f1d
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="powershell-gallery-gdpr-compliance"></a><span data-ttu-id="ea392-103">Dodržování předpisů GDPR Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea392-103">PowerShell Gallery GDPR compliance</span></span>

## <a name="overview"></a><span data-ttu-id="ea392-104">Přehled</span><span class="sxs-lookup"><span data-stu-id="ea392-104">Overview</span></span>

<span data-ttu-id="ea392-105">V květnu 2018 zákonem Evropského ochrany osobních údajů, obecné Data Protection nařízení (GDPR), se projeví.</span><span class="sxs-lookup"><span data-stu-id="ea392-105">In May 2018, a European privacy law, the General Data Protection Regulation (GDPR), takes effect.</span></span>
<span data-ttu-id="ea392-106">GDPR ukládá nové pravidel na společnosti, organizace státní správy, bez zisku a organizace nabídka zboží a služeb na osoby ve Evropské unie (EU), nebo že shromažďovat a analyzovat data svázané s obyvatele Evropské unie.</span><span class="sxs-lookup"><span data-stu-id="ea392-106">The GDPR imposes new rules on companies, government agencies, non-profits, and other organizations that offer goods and services to people in the European Union (EU), or that collect and analyze data tied to EU residents.</span></span>
<span data-ttu-id="ea392-107">GDPR platí bez ohledu na to, kde se nacházíte.</span><span class="sxs-lookup"><span data-stu-id="ea392-107">The GDPR applies no matter where you are located.</span></span>

> [!NOTE]
> <span data-ttu-id="ea392-108">Tento článek popisuje kroky pro odstranění osobní data z Galerie prostředí PowerShell a slouží k podpoře vaší povinností podle GDPR.</span><span class="sxs-lookup"><span data-stu-id="ea392-108">This article provides steps for how to delete personal data from the PowerShell Gallery and can be used to support your obligations under the GDPR.</span></span> <span data-ttu-id="ea392-109">Pokud hledáte obecné informace o GDPR, přečtěte si téma [GDPR části portálu služby důvěřovat](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).</span><span class="sxs-lookup"><span data-stu-id="ea392-109">If you’re looking for general info about GDPR, see the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).</span></span>

## <a name="personally-identifiable-data"></a><span data-ttu-id="ea392-110">Identifikovatelné osobní údaje</span><span class="sxs-lookup"><span data-stu-id="ea392-110">Personally identifiable data</span></span>

<span data-ttu-id="ea392-111">Galerie prostředí PowerShell se ukládají následující informace, které může poskytovat uživatelům, které můžou obsahovat osobní informace:</span><span class="sxs-lookup"><span data-stu-id="ea392-111">The PowerShell Gallery stores the following information that may be provided by users, which may contain personal information:</span></span>

* <span data-ttu-id="ea392-112">Účet Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea392-112">PowerShell Gallery account</span></span>
* <span data-ttu-id="ea392-113">Položky, které jsou publikovány do Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea392-113">Items published to the PowerShell Gallery</span></span>
* <span data-ttu-id="ea392-114">E-mailové korespondence s týmem Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea392-114">Email correspondence with the PowerShell Gallery team</span></span>

<span data-ttu-id="ea392-115">Většina uživatelů nevytvářejte účet Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea392-115">Most users do not create a PowerShell Gallery account.</span></span>
<span data-ttu-id="ea392-116">Účet se nevyžaduje, pokud chcete publikovat položku nebo použít funkci "Obraťte se na vlastníka" v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea392-116">An account is not required unless you are going to publish an item or use the "Contact Owner" feature in the PowerShell Gallery.</span></span>
<span data-ttu-id="ea392-117">Kromě e-mailové korespondence iniciováno uživatelem Galerie prostředí PowerShell neukládá identifikovatelné osobní údaje pro uživatele, kteří ještě nevytvořili účet.</span><span class="sxs-lookup"><span data-stu-id="ea392-117">Other than email correspondence initiated by the user, the PowerShell Gallery does not store personally identifiable data for users who have not created an account.</span></span>

<span data-ttu-id="ea392-118">Uživatelé, kteří vytvořit účet Galerie prostředí PowerShell můžete publikovat položky galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea392-118">Users who create a PowerShell Gallery account can publish items to the PowerShell Gallery.</span></span>
<span data-ttu-id="ea392-119">Tyto položky se měl kódu PowerShell, ale může obsahovat další informace, včetně osobních údajů.</span><span class="sxs-lookup"><span data-stu-id="ea392-119">Those items are expected to be PowerShell code, but may contain other information including personal information.</span></span>
<span data-ttu-id="ea392-120">Níže uvedené informace se zobrazí, jak můžete získat všechny položky jste publikovali do Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea392-120">The information below will show how you can get all the items you have published to the PowerShell Gallery.</span></span>

## <a name="dsr-export-of-powershell-gallery-data"></a><span data-ttu-id="ea392-121">DSR Export dat Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea392-121">DSR Export of PowerShell Gallery Data</span></span>

<span data-ttu-id="ea392-122">Následující části popisují, jak Galerie prostředí PowerShell podporuje požadavky na data subjektu (DSR), tím, že vysvětlí, jak exportovat informace uložené v galerii prostředí PowerShell a jak požádat o odstranění těchto informací.</span><span class="sxs-lookup"><span data-stu-id="ea392-122">The following sections describe how the PowerShell Gallery supports data subject requests (DSR), by explaining how to export information stored in the PowerShell Gallery, and how to request deletion of this information.</span></span>

### <a name="email"></a><span data-ttu-id="ea392-123">E-mail</span><span class="sxs-lookup"><span data-stu-id="ea392-123">Email</span></span>

<span data-ttu-id="ea392-124">E-mailové korespondence může obsahovat žádné z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="ea392-124">Email correspondence may include any of the following:</span></span>

* <span data-ttu-id="ea392-125">E-mailu odeslaného na vlastníky Galerie prostředí PowerShell položky Pokud analýza kódu kontrol zjistil potíže s libovolnou položku, kterou jste publikovali do Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea392-125">Email sent to the owners of PowerShell Gallery items if the code analysis scans detected an issue with any item they have published to the PowerShell Gallery</span></span>
* <span data-ttu-id="ea392-126">Každý, kdo posílá týmem Galerie prostředí PowerShell pomocí e-mailovou adresu na stránce "Kontaktujte nás" e-mailu (cgadmin@microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="ea392-126">Email sent by anyone to the PowerShell Gallery team using the email address in the "Contact Us" page (cgadmin@microsoft.com)</span></span>
* <span data-ttu-id="ea392-127">Registrované uživatele, kteří používají funkce "Obraťte se na vlastníka" v galerii prostředí PowerShell k odesílání e-mailu vlastníka položky v galerii prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea392-127">Registered users who use the "Contact Owner" feature in the PowerShell Gallery to send email to the owner of an item in the PowerShell Gallery</span></span>

<span data-ttu-id="ea392-128">E-maily odesílané do Galerie prostředí PowerShell nebo mít zásady uchovávání informací 90 dní pro podporu vyšetřování možné zabezpečení by měl škodlivý kód zjištěných v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea392-128">Emails sent by or to the PowerShell Gallery have a retention policy of 90 days to support possible security investigations should malicious code be discovered on the PowerShell Gallery.</span></span>
<span data-ttu-id="ea392-129">E-mailů jsou zásadami odstraněny po 90 dnech.</span><span class="sxs-lookup"><span data-stu-id="ea392-129">Emails are deleted by policy after 90 days.</span></span>

<span data-ttu-id="ea392-130">Může požádat o kopie všechny e-maily odesílané do nebo z e-mailovou adresu a Galerie prostředí PowerShell v rámci předchozích 90 dnů.</span><span class="sxs-lookup"><span data-stu-id="ea392-130">You may request copies of all emails sent to or from your email address and the PowerShell Gallery within the previous 90 days.</span></span>
<span data-ttu-id="ea392-131">Požádat o tato korespondence, pošlete e-mail na cgadmin@microsoft.com, s názvem: "DSR žádost o e-mailů týkajících se k tomuto účtu".</span><span class="sxs-lookup"><span data-stu-id="ea392-131">To request this correspondence, send an email to cgadmin@microsoft.com, with the title: "DSR Request for emails relating to this account".</span></span>
<span data-ttu-id="ea392-132">V textu zprávy, jaké informace, které jste požádali o stavu (například: pošlete prosím všechny e-maily odesílané nebo přijímané z této e-mailovou adresu.) Všechny e-mailů zahrnující e-mailovou adresu do 90 dnů od žádosti budou odeslány do 7 dnů firmy.</span><span class="sxs-lookup"><span data-stu-id="ea392-132">In the body of the message, state what information you are requesting (for example: Please send all emails sent to or received from this email address.) All emails involving your email address within 90 days of the request will be sent within 7 business days.</span></span>

### <a name="powershell-gallery-account-information"></a><span data-ttu-id="ea392-133">Informace o účtu Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea392-133">PowerShell Gallery Account Information</span></span>

<span data-ttu-id="ea392-134">Pokud jste vytvořili účet Galerie prostředí PowerShell, můžete najít všechny osobní informace, která byla uložena v galerii prostředí PowerShell provedením následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="ea392-134">If you have created a PowerShell Gallery account, you can find all personal information that has been stored in PowerShell Gallery by taking the following steps:</span></span>

1. <span data-ttu-id="ea392-135">Přihlaste se k Galerie prostředí PowerShell, a potom klikněte na své uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="ea392-135">Sign in to the PowerShell Gallery, then click on your username</span></span>
2. <span data-ttu-id="ea392-136">Na další stránku, zobrazí se stránku účtu, který zobrazuje e-mailovou adresu, použité pro účet Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea392-136">The next page displayed is the Account page, which shows the email address used for the PowerShell Gallery account</span></span>

<span data-ttu-id="ea392-137">Pokud jste vytvořili více než jeden účet v galerii prostředí PowerShell, musíte tento postup opakujte pro každý účet.</span><span class="sxs-lookup"><span data-stu-id="ea392-137">If you have created more than one account in the PowerShell Gallery, you will need to repeat these steps for each account.</span></span>

### <a name="items-in-the-powershell-gallery"></a><span data-ttu-id="ea392-138">Položky v galerii prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea392-138">Items in the PowerShell Gallery</span></span>

<span data-ttu-id="ea392-139">Pro usnadnění Export položky, které jsou publikovány do Galerie prostředí PowerShell, jsme publikovali skriptu "GetPSGalleryItemsForAuthor" do Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea392-139">To facilitate exporting items published to the PowerShell Gallery, we have published the script "GetPSGalleryItemsForAuthor" to the PowerShell Gallery.</span></span>
<span data-ttu-id="ea392-140">Tento skript exportuje kopii každé verzi každá položka vložena Galerie prostředí PowerShell založený na informacích Autor uložená v položce.</span><span class="sxs-lookup"><span data-stu-id="ea392-140">This script exports a copy of every version of every item put into the PowerShell Gallery based on the author information stored in the item.</span></span>

> [!NOTE]
> <span data-ttu-id="ea392-141">Autor je uložený v manifestu položky při publikování vaší položky.</span><span class="sxs-lookup"><span data-stu-id="ea392-141">The Author is stored in the item manifest when you publish your item.</span></span>
> <span data-ttu-id="ea392-142">Není zaručeno, že autor se stejnou identitou jako účet, který používáte v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea392-142">There is no guarantee that the Author is the same identity as the account you use in the PowerShell Gallery.</span></span>
> <span data-ttu-id="ea392-143">Pokud použijete jinou hodnotu v poli autora, musíte zadat tuto hodnotu, při použití tohoto skriptu.</span><span class="sxs-lookup"><span data-stu-id="ea392-143">If you use some other value in the Author field, you will need to supply that value when using this script.</span></span>

<span data-ttu-id="ea392-144">Skript může stáhnout pomocí následujícího příkazu Powershellu:</span><span class="sxs-lookup"><span data-stu-id="ea392-144">You may download the script by using the following PowerShell command:</span></span>

```powershell
Save-Script GetPSGalleryItemsForAuthor -path <local folder location> -repository psgallery
```

<span data-ttu-id="ea392-145">Když pak spustíte skript přímo, spuštěním následujících příkazů prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ea392-145">You can then run the script directly, by running the following PowerShell commands:</span></span>

```powershell
cd <local folder location >
.\GetPSGalleryItemsForAuthor.ps1
```

<span data-ttu-id="ea392-146">Zobrazí se výzva k zadání autora a složku ve vašem systému místo položky, které chcete uložit.</span><span class="sxs-lookup"><span data-stu-id="ea392-146">You will be prompted to supply the Author and a folder on your system where you want the items to be saved.</span></span>

## <a name="deleting-personal-data-from-the-powershell-gallery"></a><span data-ttu-id="ea392-147">Odstranění osobní Data z Galerie Powershellu</span><span class="sxs-lookup"><span data-stu-id="ea392-147">Deleting Personal Data From The PowerShell Gallery</span></span>

<span data-ttu-id="ea392-148">Pokud chcete odstranit účet Galerie prostředí PowerShell nebo libovolnou položku, kterou vlastníte v galerii prostředí PowerShell, odesílat e-mailu cgadmin@microsoft.com s názvem: "GDPR žádost pro položky vztahující se k tomuto účtu".</span><span class="sxs-lookup"><span data-stu-id="ea392-148">To delete your PowerShell Gallery account or any item you own in the PowerShell Gallery, send email to cgadmin@microsoft.com with the title: "GDPR Request for items relating to this account".</span></span>
<span data-ttu-id="ea392-149">V těle zprávy o stavu informacích chcete odstraněné.</span><span class="sxs-lookup"><span data-stu-id="ea392-149">In the body of the message state what information you want deleted.</span></span> <span data-ttu-id="ea392-150">Příklad:</span><span class="sxs-lookup"><span data-stu-id="ea392-150">For example:</span></span>

* <span data-ttu-id="ea392-151">Odstraňte prosím verze x.y.z "název položky" Moje položky</span><span class="sxs-lookup"><span data-stu-id="ea392-151">Please delete version x.y.z of my item "item name"</span></span>
* <span data-ttu-id="ea392-152">Odstraňte všechny verze "název položky" Moje položky</span><span class="sxs-lookup"><span data-stu-id="ea392-152">Please delete all versions of my item "item name"</span></span>
* <span data-ttu-id="ea392-153">Odstraňte Můj účet Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea392-153">Please delete my PowerShell Gallery account</span></span>

<span data-ttu-id="ea392-154">Správci Galerie prostředí PowerShell odpovíte do 7 dnů firmy.</span><span class="sxs-lookup"><span data-stu-id="ea392-154">The PowerShell Gallery administrators will reply within 7 business days.</span></span>
<span data-ttu-id="ea392-155">Do 30 dní po odeslání žádosti se odstraní vybrané položky.</span><span class="sxs-lookup"><span data-stu-id="ea392-155">The items specified will be deleted within 30 days after the request is sent.</span></span>
