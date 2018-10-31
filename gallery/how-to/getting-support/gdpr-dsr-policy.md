---
ms.date: 03/27/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, psgallery GDPR
title: Dodržování předpisů GDPR Galerie prostředí PowerShell
ms.openlocfilehash: fb1191d8a1cd12d5994e41238c384eb504d0c261
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002646"
---
# <a name="powershell-gallery-gdpr-compliance"></a><span data-ttu-id="e13bd-103">Dodržování předpisů GDPR Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13bd-103">PowerShell Gallery GDPR compliance</span></span>

## <a name="overview"></a><span data-ttu-id="e13bd-104">Přehled</span><span class="sxs-lookup"><span data-stu-id="e13bd-104">Overview</span></span>

<span data-ttu-id="e13bd-105">V květnu 2018 zákony Evropské ochrany osobních údajů, obecného Protection Regulation (GDPR), vstoupily v platnost.</span><span class="sxs-lookup"><span data-stu-id="e13bd-105">In May 2018, a European privacy law, the General Data Protection Regulation (GDPR), took effect.</span></span>
<span data-ttu-id="e13bd-106">GDPR ukládá nová pravidla pro společnosti, státních úřadů, – neziskové organizace a jinými organizacemi, že nabídka zboží a služby lidem v Evropské unii (EU) nebo které shromažďovat a analyzovat data svázaná s pobytem v EU.</span><span class="sxs-lookup"><span data-stu-id="e13bd-106">The GDPR imposes new rules on companies, government agencies, non-profits, and other organizations that offer goods and services to people in the European Union (EU), or that collect and analyze data tied to EU residents.</span></span>
<span data-ttu-id="e13bd-107">GDPR se vztahuje bez ohledu na to, kde se nachází.</span><span class="sxs-lookup"><span data-stu-id="e13bd-107">The GDPR applies no matter where you are located.</span></span>

> [!NOTE]
> <span data-ttu-id="e13bd-108">Tento článek popisuje kroky pro odstranění osobních údajů z Galerie prostředí PowerShell a slouží k podpoře vaší povinností v GDPR.</span><span class="sxs-lookup"><span data-stu-id="e13bd-108">This article provides steps for how to delete personal data from the PowerShell Gallery and can be used to support your obligations under the GDPR.</span></span> <span data-ttu-id="e13bd-109">Pokud potřebujete obecné informace o podle nařízení GDPR, najdete v článku [GDPR část Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).</span><span class="sxs-lookup"><span data-stu-id="e13bd-109">If you’re looking for general info about GDPR, see the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).</span></span>

## <a name="personally-identifiable-data"></a><span data-ttu-id="e13bd-110">Osobně identifikovatelných dat</span><span class="sxs-lookup"><span data-stu-id="e13bd-110">Personally identifiable data</span></span>

<span data-ttu-id="e13bd-111">Galerie prostředí PowerShell se ukládají následující informace, který může zadat uživatele, které mohou obsahovat osobní údaje:</span><span class="sxs-lookup"><span data-stu-id="e13bd-111">The PowerShell Gallery stores the following information that may be provided by users, which may contain personal information:</span></span>

- <span data-ttu-id="e13bd-112">Účet Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13bd-112">PowerShell Gallery account</span></span>
- <span data-ttu-id="e13bd-113">Balíčky, které jsou publikované v galerii prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13bd-113">Packages published to the PowerShell Gallery</span></span>
- <span data-ttu-id="e13bd-114">E-mailové korespondence s týmem Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13bd-114">Email correspondence with the PowerShell Gallery team</span></span>

<span data-ttu-id="e13bd-115">Většina uživatelů, nevytvářejte účet Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e13bd-115">Most users do not create a PowerShell Gallery account.</span></span>
<span data-ttu-id="e13bd-116">Účet není povinný, pokud se chystáte publikovat balíček nebo použít funkci "Kontaktujte vlastníka" v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e13bd-116">An account is not required unless you are going to publish a package or use the "Contact Owner" feature in the PowerShell Gallery.</span></span>
<span data-ttu-id="e13bd-117">Galerie prostředí PowerShell než e-mailové korespondence iniciované příslušným uživatelem, neukládá identifikovatelné osobní údaje pro uživatele, kteří ještě nevytvořili účet.</span><span class="sxs-lookup"><span data-stu-id="e13bd-117">Other than email correspondence initiated by the user, the PowerShell Gallery does not store personally identifiable data for users who have not created an account.</span></span>

<span data-ttu-id="e13bd-118">Uživatele, kteří vytvářejí účet Galerie prostředí PowerShell můžete publikovat balíčky do Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e13bd-118">Users who create a PowerShell Gallery account can publish packages to the PowerShell Gallery.</span></span>
<span data-ttu-id="e13bd-119">Tyto balíčky jsou očekávány kódu Powershellu, ale může obsahovat další informace, včetně osobních údajů.</span><span class="sxs-lookup"><span data-stu-id="e13bd-119">Those packages are expected to be PowerShell code, but may contain other information including personal information.</span></span>
<span data-ttu-id="e13bd-120">Níže uvedené informace se zobrazí, jak získat všechny balíčky jste publikovali v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e13bd-120">The information below will show how you can get all the packages you have published to the PowerShell Gallery.</span></span>

## <a name="dsr-export-of-powershell-gallery-data"></a><span data-ttu-id="e13bd-121">Export PSÚ dat Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13bd-121">DSR Export of PowerShell Gallery Data</span></span>

<span data-ttu-id="e13bd-122">Následující části popisují, jak v galerii prostředí PowerShell podporuje žádosti údajů (PSÚ), tak s vysvětlením, jak exportovat informace uložené v galerii prostředí PowerShell a jak požádat o odstranění těchto informací.</span><span class="sxs-lookup"><span data-stu-id="e13bd-122">The following sections describe how the PowerShell Gallery supports data subject requests (DSR), by explaining how to export information stored in the PowerShell Gallery, and how to request deletion of this information.</span></span>

### <a name="email"></a><span data-ttu-id="e13bd-123">E-mail</span><span class="sxs-lookup"><span data-stu-id="e13bd-123">Email</span></span>

<span data-ttu-id="e13bd-124">E-mailové korespondence může obsahovat žádný z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="e13bd-124">Email correspondence may include any of the following:</span></span>

- <span data-ttu-id="e13bd-125">E-mailu odeslaného pro vlastníky Galerie prostředí PowerShell balíčky, pokud analýza kódu vyhledá zjistili potíže v balíčcích, které jste publikovali v galerii prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13bd-125">Email sent to the owners of PowerShell Gallery packages if the code analysis scans detected an issue with any package they have published to the PowerShell Gallery</span></span>
- <span data-ttu-id="e13bd-126">E-mailu odeslaného kdokoli v týmu Galerie prostředí PowerShell pomocí e-mailovou adresu v stránky "Kontaktujte nás" [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="e13bd-126">Email sent by anyone to the PowerShell Gallery team using the email address in the "Contact Us" page [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com)</span></span>
- <span data-ttu-id="e13bd-127">Registrovaný uživatelů, kteří používají funkci "Kontaktujte vlastníka" v galerii prostředí PowerShell k odesílání e-mailu vlastníka balíčku v galerii prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13bd-127">Registered users who use the "Contact Owner" feature in the PowerShell Gallery to send email to the owner of a package in the PowerShell Gallery</span></span>

<span data-ttu-id="e13bd-128">E-mailů podle nebo v galerii prostředí PowerShell mají zásady uchovávání 90 dnů pro podporu možné bezpečnostní vyšetřování by měl škodlivý kód nalezených v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e13bd-128">Emails sent by or to the PowerShell Gallery have a retention policy of 90 days to support possible security investigations should malicious code be discovered on the PowerShell Gallery.</span></span>
<span data-ttu-id="e13bd-129">E-maily se odstraní podle zásad po 90 dnech.</span><span class="sxs-lookup"><span data-stu-id="e13bd-129">Emails are deleted by policy after 90 days.</span></span>

<span data-ttu-id="e13bd-130">Může vyžadovat zkopíruje všechny e-maily odesílané do nebo z e-mailovou adresu a Galerie prostředí PowerShell v rámci za předchozích 90 dnů.</span><span class="sxs-lookup"><span data-stu-id="e13bd-130">You may request copies of all emails sent to or from your email address and the PowerShell Gallery within the previous 90 days.</span></span>
<span data-ttu-id="e13bd-131">Žádost o tuto komunikaci, pošlete e-mailu [ cgadmin@microsoft.com ](mailto:cgadmin@microsoft.com), s názvem: "Žádost PSÚ ohledně e-mailů týkajících se k tomuto účtu".</span><span class="sxs-lookup"><span data-stu-id="e13bd-131">To request this correspondence, send an email to [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com), with the title: "DSR Request for emails relating to this account".</span></span>
<span data-ttu-id="e13bd-132">V textu zprávy, jaké informace, které jste požádali stavu (například: odešlete všechny e-maily odesílané nebo přijímané z tohoto e-mailovou adresu.) Všechny e-mailů týkajících se e-mailovou adresu do 90 dnů od žádosti se odešlou do 7 pracovních dnů.</span><span class="sxs-lookup"><span data-stu-id="e13bd-132">In the body of the message, state what information you are requesting (for example: Please send all emails sent to or received from this email address.) All emails involving your email address within 90 days of the request will be sent within 7 business days.</span></span>

### <a name="powershell-gallery-account-information"></a><span data-ttu-id="e13bd-133">Informace o účtu Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13bd-133">PowerShell Gallery Account Information</span></span>

<span data-ttu-id="e13bd-134">Pokud jste vytvořili účet Galerie prostředí PowerShell, můžete najít všechny osobní informace, které jsou uložená v galerii prostředí PowerShell pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="e13bd-134">If you have created a PowerShell Gallery account, you can find all personal information that has been stored in PowerShell Gallery by taking the following steps:</span></span>

1. <span data-ttu-id="e13bd-135">Přihlaste se v galerii prostředí PowerShell a potom klikněte na své uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="e13bd-135">Sign in to the PowerShell Gallery, then click on your username</span></span>
2. <span data-ttu-id="e13bd-136">Na další stránku, zobrazí se na stránku účtu, který zobrazuje e-mailovou adresu použije pro účet Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13bd-136">The next page displayed is the Account page, which shows the email address used for the PowerShell Gallery account</span></span>

<span data-ttu-id="e13bd-137">Pokud vytvoříte více než jeden účet v galerii prostředí PowerShell, musíte tento postup opakujte pro každý účet.</span><span class="sxs-lookup"><span data-stu-id="e13bd-137">If you have created more than one account in the PowerShell Gallery, you will need to repeat these steps for each account.</span></span>

### <a name="packages-in-the-powershell-gallery"></a><span data-ttu-id="e13bd-138">Balíčky v galerii prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13bd-138">Packages in the PowerShell Gallery</span></span>

<span data-ttu-id="e13bd-139">Pro usnadnění export balíčky, které jsou publikované v galerii prostředí PowerShell, jsme publikovali skriptu "GetPSGalleryItemsForAuthor" v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e13bd-139">To facilitate exporting packages published to the PowerShell Gallery, we have published the script "GetPSGalleryItemsForAuthor" to the PowerShell Gallery.</span></span>
<span data-ttu-id="e13bd-140">Tento skript exportuje kopie každé verze každého balíčku do Galerie prostředí PowerShell na základě Autor informací uložených v balíčku.</span><span class="sxs-lookup"><span data-stu-id="e13bd-140">This script exports a copy of every version of every package put into the PowerShell Gallery based on the author information stored in the package.</span></span>

> [!NOTE]
> <span data-ttu-id="e13bd-141">Autor se ukládají v manifestu balíčku, když publikujete balíček.</span><span class="sxs-lookup"><span data-stu-id="e13bd-141">The Author is stored in the package manifest when you publish your package.</span></span>
> <span data-ttu-id="e13bd-142">Není zaručeno, že autor se stejnou identitou jako účet, který použijete v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e13bd-142">There is no guarantee that the Author is the same identity as the account you use in the PowerShell Gallery.</span></span>
> <span data-ttu-id="e13bd-143">Pokud použijete jinou hodnotu v poli Autor, je potřeba zadat tuto hodnotu při použití tohoto skriptu.</span><span class="sxs-lookup"><span data-stu-id="e13bd-143">If you use some other value in the Author field, you will need to supply that value when using this script.</span></span>

<span data-ttu-id="e13bd-144">Skript může stáhnout pomocí následujícího příkazu Powershellu:</span><span class="sxs-lookup"><span data-stu-id="e13bd-144">You may download the script by using the following PowerShell command:</span></span>

```powershell
Save-Script Get-repository psgallery
```

<span data-ttu-id="e13bd-145">Potom spustíte skript přímo, spuštěním následujících příkazů Powershellu:</span><span class="sxs-lookup"><span data-stu-id="e13bd-145">You can then run the script directly, by running the following PowerShell commands:</span></span>

```powershell
# cd <local folder location>
.\GetPSGalleryItemsForAuthor.ps1
```

<span data-ttu-id="e13bd-146">Zobrazí výzva k zadání jeho autorovi a složku ve vašem systému, požadované balíčky, které se má uložit.</span><span class="sxs-lookup"><span data-stu-id="e13bd-146">You will be prompted to supply the Author and a folder on your system where you want the packages to be saved.</span></span>

## <a name="deleting-personal-data-from-the-powershell-gallery"></a><span data-ttu-id="e13bd-147">Odstranění osobní údaje z Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13bd-147">Deleting Personal Data From The PowerShell Gallery</span></span>

<span data-ttu-id="e13bd-148">Chcete-li odstranit svůj účet Galerie prostředí PowerShell nebo všechny balíčky, které vlastníte v galerii prostředí PowerShell, pošlete e-mail na adresu cgadmin@microsoft.com s názvem: "Žádosti GDPR o položky vztahující se k tomuto účtu".</span><span class="sxs-lookup"><span data-stu-id="e13bd-148">To delete your PowerShell Gallery account or any package you own in the PowerShell Gallery, send email to cgadmin@microsoft.com with the title: "GDPR Request for items relating to this account".</span></span>
<span data-ttu-id="e13bd-149">V těle zprávy o stavu jaké informace chcete odstraněné.</span><span class="sxs-lookup"><span data-stu-id="e13bd-149">In the body of the message state what information you want deleted.</span></span> <span data-ttu-id="e13bd-150">Příklad:</span><span class="sxs-lookup"><span data-stu-id="e13bd-150">For example:</span></span>

- <span data-ttu-id="e13bd-151">Odstraňte prosím verze x.y.z Můj balíček "název balíčku"</span><span class="sxs-lookup"><span data-stu-id="e13bd-151">Please delete version x.y.z of my package "package name"</span></span>
- <span data-ttu-id="e13bd-152">Odstraňte prosím všechny verze balíčku "název balíčku"</span><span class="sxs-lookup"><span data-stu-id="e13bd-152">Please delete all versions of my package "package name"</span></span>
- <span data-ttu-id="e13bd-153">Odstraňte prosím svůj účet Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e13bd-153">Please delete my PowerShell Gallery account</span></span>

<span data-ttu-id="e13bd-154">Správci Galerie prostředí PowerShell odpovíte do 7 pracovních dnů.</span><span class="sxs-lookup"><span data-stu-id="e13bd-154">The PowerShell Gallery administrators will reply within 7 business days.</span></span>
<span data-ttu-id="e13bd-155">Do 30 dní po odeslání žádosti se odstraní balíčky zadané.</span><span class="sxs-lookup"><span data-stu-id="e13bd-155">The packages specified will be deleted within 30 days after the request is sent.</span></span>
