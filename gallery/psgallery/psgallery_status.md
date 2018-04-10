---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery
title: psgallery_status
ms.openlocfilehash: 08d09ce83b5133598152186e12fc8ced90c36a88
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
<a name="powershell-gallery-status"></a><span data-ttu-id="af6ec-103">Stav Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="af6ec-103">PowerShell Gallery Status</span></span>
=========================
## <a name="10102017---powershell-gallery-unavailable-for-2-hours-101017"></a><span data-ttu-id="af6ec-104">10/10/2017 - Galerie prostředí PowerShell, které jsou k dispozici další 2 hodiny 10/10/17</span><span class="sxs-lookup"><span data-stu-id="af6ec-104">10/10/2017 - PowerShell Gallery unavailable for 2 hours 10/10/17</span></span>

<span data-ttu-id="af6ec-105">__Souhrn dopad__: galerii prostředí PowerShell došlo období velmi vysokou latencí, což vede k nepřerušované připojení problémy, počínaje přibližně 17: 00 (PDT) 10/10/17.</span><span class="sxs-lookup"><span data-stu-id="af6ec-105">__Summary of Impact__: The PowerShell Gallery experienced a period of very high latency, resulting in intermittent connection issues, beginning approximately 5pm (PDT) 10/10/17.</span></span> <span data-ttu-id="af6ec-106">Při řešení problému, převedl webu do stavu offline 2 hodin od přibližně 22: 00 (PDT).</span><span class="sxs-lookup"><span data-stu-id="af6ec-106">While resolving the issue, the site was taken offline for 2 hours starting approximately 10pm (PDT).</span></span> <span data-ttu-id="af6ec-107">Webu byla obnovena krátce před půlnoc 10/10/2017.</span><span class="sxs-lookup"><span data-stu-id="af6ec-107">The site was restored shortly before midnight 10/10/2017.</span></span>

<span data-ttu-id="af6ec-108">__Příčina__: hlavní příčinu vysoké latenci je stále probíhá prozkoumat.</span><span class="sxs-lookup"><span data-stu-id="af6ec-108">__Root Cause__: The root cause of the high latency is still being investigated.</span></span>

<span data-ttu-id="af6ec-109">__Řešení__: webové služby musí být převedeny do režimu offline a obnovit Chcete-li primární problém vyřešit.</span><span class="sxs-lookup"><span data-stu-id="af6ec-109">__Resolution__: The web services had to be taken offline and restored in order to address the primary issue.</span></span>

<span data-ttu-id="af6ec-110">__Další kroky__: příčinu původní problém zkoumán.</span><span class="sxs-lookup"><span data-stu-id="af6ec-110">__Next Steps__: The root cause for the original issue is being investigated.</span></span>

## <a name="06012017---deploy-to-azure-automation-currently-unavailable"></a><span data-ttu-id="af6ec-111">01/06/2017 - nasazení do služby Azure Automation, které jsou nyní k dispozici</span><span class="sxs-lookup"><span data-stu-id="af6ec-111">06/01/2017 - Deploy to Azure Automation Currently Unavailable</span></span>

<span data-ttu-id="af6ec-112">__Souhrn dopad__: nasazení položek závislosti pro Azure Automation z Galerie prostředí PowerShell je nyní k dispozici.</span><span class="sxs-lookup"><span data-stu-id="af6ec-112">__Summary of Impact__: Deploying items with dependencies to Azure Automation from the PowerShell Gallery is currently unavailable.</span></span>  <span data-ttu-id="af6ec-113">Import položek z Galerie Powershellu z uvnitř Azure Automation je stále k dispozici.</span><span class="sxs-lookup"><span data-stu-id="af6ec-113">Importing items from the PowerShell Gallery from inside Azure Automation is still available.</span></span>

<span data-ttu-id="af6ec-114">__Hlavní příčinu__: položky, které mají závislosti na jiných a byla předtím nasadili do Azure Automation, nebude nasazen do Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="af6ec-114">__Root Cause__: Items that have dependencies on others, and have been previously deployed to Azure Automation, will not be deployed to Azure Automation.</span></span> <span data-ttu-id="af6ec-115">Technici určili problém s způsob generování šablon ARM pro položky s závislosti pro nasazení do Azure Automation funkce.</span><span class="sxs-lookup"><span data-stu-id="af6ec-115">Engineers have identified an issue with how ARM templates are generated for items with dependencies for the Deploy to Azure Automation functionality.</span></span>

<span data-ttu-id="af6ec-116">__Řešení__: technici pracují k vyřešení problému.</span><span class="sxs-lookup"><span data-stu-id="af6ec-116">__Resolution__: Engineers are working to resolve issue.</span></span>  <span data-ttu-id="af6ec-117">Aktuální řešení pro uživatele je importovat položky z Galerie Powershellu z uvnitř Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="af6ec-117">The current workaround for users is to import the item from the PowerShell Gallery from inside Azure Automation.</span></span>

<span data-ttu-id="af6ec-118">__Další kroky__: technici vydá opravu za chvíli.</span><span class="sxs-lookup"><span data-stu-id="af6ec-118">__Next Steps__: Engineers will release the fix shortly.</span></span>  <span data-ttu-id="af6ec-119">Do té doby použijte prosím doporučená řešení.</span><span class="sxs-lookup"><span data-stu-id="af6ec-119">In the meantime, please use the recommended workaround.</span></span>


## <a name="04112017---users-unable-to-log-in-with-azure-active-directory-aad-accounts"></a><span data-ttu-id="af6ec-120">04/11/2017 - uživatele nelze se přihlásit účty Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="af6ec-120">04/11/2017 - Users unable to log in with Azure Active Directory (AAD) accounts</span></span>

<span data-ttu-id="af6ec-121">__Souhrn dopad__: někteří uživatelé nemohli k přihlášení do Galerie prostředí PowerShell pomocí účty Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af6ec-121">__Summary of Impact__: Some users were unable to log in to the PowerShell Gallery using Azure AD Accounts.</span></span>

<span data-ttu-id="af6ec-122">__Hlavní příčinu__: během aktualizace bezpečněji spolupracovat s AAD, nebyla provedena změna nastavení.</span><span class="sxs-lookup"><span data-stu-id="af6ec-122">__Root Cause__: During an update to interact more securely with AAD, a setting change was missed.</span></span>
<span data-ttu-id="af6ec-123">Testování provádí ověření změny nejsou zahrnuty některé typy účtů AAD, aby nasazení pokračovalo.</span><span class="sxs-lookup"><span data-stu-id="af6ec-123">The testing done to validate the change did not include certain types of AAD accounts, so the deployment proceeded.</span></span>

<span data-ttu-id="af6ec-124">__Řešení__: technici identifikovat chybějící nastavení a byl problém odstraněn.</span><span class="sxs-lookup"><span data-stu-id="af6ec-124">__Resolution__: Engineers identified the missing setting and corrected the problem.</span></span>

<span data-ttu-id="af6ec-125">__Další kroky__: jsme se změnou našich testech zahrnout širší sadě typy účtů AAD.</span><span class="sxs-lookup"><span data-stu-id="af6ec-125">__Next Steps__: We will be modifying our testing to include a broader set of AAD account types.</span></span>

## <a name="03272017---resolved-unable-to-see-individual-module-and-script-pages"></a><span data-ttu-id="af6ec-126">VYŘEŠIT 03/27/2017 -: nelze zobrazit jednotlivé stránky modulu a skriptu</span><span class="sxs-lookup"><span data-stu-id="af6ec-126">03/27/2017 - RESOLVED: Unable to see individual module and script pages</span></span>

<span data-ttu-id="af6ec-127">__Souhrn dopad__: přímé odkazy na jednotlivých stránkách modulu a skriptu na https://www.powershellgallery.com bylo přerušeno.</span><span class="sxs-lookup"><span data-stu-id="af6ec-127">__Summary of Impact__: Direct links to individual module and script pages on https://www.powershellgallery.com were broken.</span></span> <span data-ttu-id="af6ec-128">To se ohlásil přes všechny oblasti.</span><span class="sxs-lookup"><span data-stu-id="af6ec-128">This was being reported across all the regions.</span></span> <span data-ttu-id="af6ec-129">To negativní vliv na některé z rutiny PowerShellGet ie., nainstalujte modul, skript aktualizace, publikování-Module skriptu instalace, aktualizace-Module publikování-Scirpt dál fungovat.</span><span class="sxs-lookup"><span data-stu-id="af6ec-129">This did not impact any of the PowerShellGet cmdlets ie., Install-Module, Install-Script, Update-Module, Update-Script, Publish-Module, Publish-Scirpt continued to work.</span></span>

<span data-ttu-id="af6ec-130">__Příčina__: technici označený příčinu problému přináší až sociálních médií tlačítka jako je Facebook na stránku.</span><span class="sxs-lookup"><span data-stu-id="af6ec-130">__Root Cause__: Engineers identified the cause as an issue bringing up social media buttons like Facebook onto the page.</span></span>

<span data-ttu-id="af6ec-131">__Řešení__: technici opraven problém zakázání informace o počtu Facebook.</span><span class="sxs-lookup"><span data-stu-id="af6ec-131">__Resolution__: Engineers fixed the problem by disabling the Facebook count information.</span></span>

<span data-ttu-id="af6ec-132">__Další kroky__: jsme otevřít interní sledování problém opravit naše využití rozhraní API sítě Facebook.</span><span class="sxs-lookup"><span data-stu-id="af6ec-132">__Next Steps__: We opened an internal tracking issue to fix our usage of Facebook API.</span></span>

## <a name="12152016---unable-to-send-emails-via-powershellgallery-website"></a><span data-ttu-id="af6ec-133">12/15/2016 - nelze odeslat e-mailů prostřednictvím PowerShellGallery webu</span><span class="sxs-lookup"><span data-stu-id="af6ec-133">12/15/2016 - Unable to send emails via PowerShellGallery website</span></span>

<span data-ttu-id="af6ec-134">__Souhrn dopad__: až 12, 13/2016 15 12. 2016, nebyly přijaty žádné zprávy odeslané přes kontaktujte vlastníky, Spravovat vlastníky, obraťte se na podporu nebo oznámení zneužití správci Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af6ec-134">__Summary of Impact__: Between 12/13/2016 and 12/15/2016, any messages sent via Contact Owners, Manage Owners, Contact Support, or Report Abuse were not received by the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="af6ec-135">__Příčina__: technici označený příčinu chyby ověřování se serverem SMTP.</span><span class="sxs-lookup"><span data-stu-id="af6ec-135">__Root Cause__: Engineers identified the cause as an authentication issue with the SMTP server.</span></span>
<span data-ttu-id="af6ec-136">__Řešení__: technici byli schopni vyřešit problém s ověřováním a obnovte připojení k serveru SMTP.</span><span class="sxs-lookup"><span data-stu-id="af6ec-136">__Resolution__: Engineers were able to resolve the authentication issue and restore connection to the SMTP server.</span></span>
<span data-ttu-id="af6ec-137">__Další kroky__: Pokud jste použili kontaktujte vlastníky, Spravovat vlastníky, obraťte se na podporu nebo oznámení zneužití odkazy k odesílání e-mailu cgadmin@microsoft.com během této doby a jsme neodpověděli, zkuste to prosím znovu.</span><span class="sxs-lookup"><span data-stu-id="af6ec-137">__Next Steps__: If you used the Contact Owners, Manage Owners, Contact Support, or Report Abuse links to send mail to cgadmin@microsoft.com during this time and we have not responded, please try again.</span></span> <span data-ttu-id="af6ec-138">Omlouváme se za nepříjemnosti.</span><span class="sxs-lookup"><span data-stu-id="af6ec-138">We apologize for the inconvenience.</span></span>



## <a name="8102016---resolved-unable-to-send-emails-to-cgadminmicrosoftcom"></a><span data-ttu-id="af6ec-139">8/10/2016 - přeložit: nebylo možné odeslat e-mailů cgadmin@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="af6ec-139">8/10/2016 - Resolved: Unable to send emails to cgadmin@microsoft.com</span></span>

<span data-ttu-id="af6ec-140">__Souhrn dopad__: mezi 8/5/2016 a 8/10/2016 zákazníci nemohli odesílat e-mailů cgadmin@microsoft.com, nebo použijte funkci kontaktujte nás.</span><span class="sxs-lookup"><span data-stu-id="af6ec-140">__Summary of Impact__: Between 8/5/2016 and 8/10/2016, customers were unable to send emails to cgadmin@microsoft.com, or use the Contact Us feature.</span></span>
<span data-ttu-id="af6ec-141">__Příčina__: technici označený příčinu změna konfigurace e-mailového účtu.</span><span class="sxs-lookup"><span data-stu-id="af6ec-141">__Root Cause__: Engineers identified the cause as a configuration change of the email account.</span></span>
<span data-ttu-id="af6ec-142">__Řešení__: technici práce na incidentu k vyřešení problému konfigurace.</span><span class="sxs-lookup"><span data-stu-id="af6ec-142">__Resolution__: Engineers worked to resolve the configuration issue.</span></span>
<span data-ttu-id="af6ec-143">__Další kroky__: Pokud můžete použít odkaz kontaktujte nás nebo odeslat e-mailu cgadmin@microsoft.com během této doby a jsme neodpověděli, zkuste to prosím znovu.</span><span class="sxs-lookup"><span data-stu-id="af6ec-143">__Next Steps__: If you used the Contact Us link or sent mail to cgadmin@microsoft.com during this time and we have not responded, please try again.</span></span> <span data-ttu-id="af6ec-144">Děkujeme vám za trpělivost.</span><span class="sxs-lookup"><span data-stu-id="af6ec-144">Thank you for your patience.</span></span>



## <a name="7132016---download-items-failed"></a><span data-ttu-id="af6ec-145">13/7/2016 – stažení položky se nezdařilo</span><span class="sxs-lookup"><span data-stu-id="af6ec-145">7/13/2016 - Download Items Failed</span></span>

<span data-ttu-id="af6ec-146">__Souhrn dopad__: mezi 7/11. dubna 2016 a 13 7. 2016 podmnožinu zákazníkům došlo problémy stahování položky z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af6ec-146">__Summary of Impact__: Between 7/11/2016 and 7/13/2016, a subset of customers experienced issues downloading items from the PowerShell Gallery.</span></span> <span data-ttu-id="af6ec-147">Tento problém pravděpodobně sám označované v následující chybovou zprávu vrácenou z instalace – modul nebo instalační skript a uložit modulu nebo Save-skriptu:</span><span class="sxs-lookup"><span data-stu-id="af6ec-147">The issue likely manifested itself in the following error message returned from Install-Module/Install-Script and Save-Module/Save-Script:</span></span>

```powershell
PS C:\> Install-Module xStorage
PackageManagement\Install-Package : Package 'xStorage' failed to be installed because:
End of Central Directory record could not be found. At C:\Program
Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1375 char:21 + ...
$null = PackageManagement\Install-Package @PSBoundParameters +
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ + CategoryInfo : InvalidResult:
(xStorage:String) [Install-Package], Exception + FullyQualifiedErrorId : Package '{0}'
failed to be installed because: {1},Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage
```

<span data-ttu-id="af6ec-148">__Předběžný hlavní příčinu__: technici zjistila problém s obsahu doručit síť (CDN) Azure, který byl nasazen do Galerie prostředí PowerShell na 7/11. dubna 2016.</span><span class="sxs-lookup"><span data-stu-id="af6ec-148">__Preliminary root cause__: Engineers identified an issue with Azure Content Deliver Network (CDN), which was deployed to the PowerShell Gallery on 7/11/2016.</span></span>
<span data-ttu-id="af6ec-149">__Zmírnění dopadů__: technici zakázáno Azure CDN v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af6ec-149">__Mitigation__: Engineers disabled Azure CDN in the PowerShell Gallery.</span></span>
<span data-ttu-id="af6ec-150">__Další kroky__: prozkoumat základní příčiny a vývoj řešení, aby se zabránilo budoucna.</span><span class="sxs-lookup"><span data-stu-id="af6ec-150">__Next Steps__: Investigate the underlying root cause and developing a solution to prevent future occurrences.</span></span>


## <a name="5192016---download-items-failed"></a><span data-ttu-id="af6ec-151">5/19. ledna 2016 - stažení položky se nezdařilo</span><span class="sxs-lookup"><span data-stu-id="af6ec-151">5/19/2016 - Download Items Failed</span></span>
<span data-ttu-id="af6ec-152">__Souhrn dopad__: mezi 5/17/2016 a 5/19. ledna 2016, podmnožinu zákazníkům došlo problémy stahování položky z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af6ec-152">__Summary of Impact__: Between 5/17/2016 and 5/19/2016, a subset of customers experienced issues downloading items from the PowerShell Gallery.</span></span> <span data-ttu-id="af6ec-153">Tento problém pravděpodobně sám označované v následující chybovou zprávu vrácenou z instalace – modul nebo instalační skript a uložit modulu nebo Save-skriptu:</span><span class="sxs-lookup"><span data-stu-id="af6ec-153">The issue likely manifested itself in the following error message returned from Install-Module/Install-Script and Save-Module/Save-Script:</span></span>

```powershell
VERBOSE: Hash for package 'AzureRM.OperationalInsights' does not match hash provided from the server.
VERBOSE: InstallPackageLocal' - name='AzureRM.OperationalInsights', version='1.0.8',
destination='C:\Users\jbritt\AppData\Local\Temp\2\1741355729'
WARNING: Package 'AzureRM.OperationalInsights' failed to be installed because:
End of Central Directory record could not be found.
WARNING: Dependent Package 'AzureRM.OperationalInsights' failed to install.
WARNING: Package 'AzureRM' failed to install.
VERBOSE: Module 'AzureRM.Network' was saved successfully.
VERBOSE: Saving the dependency module 'AzureRM.NotificationHubs' with version '1.0.8' for the
module 'AzureRM'.
VERBOSE: Module 'AzureRM.NotificationHubs' was saved successfully.
PackageManagement\Save-Package : Unable to save the module 'AzureRM'. At C:\Program
Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1187 char:21 +
$null = PackageManagement\Save-Package @PSBoundParameters +
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ +
CategoryInfo : InvalidOperation: (Microsoft.Power...ets.SavePackage:SavePackage)
[Save-Package], Exception + FullyQualifiedErrorId : ProviderFailToDownloadFile,
Microsoft.PowerShell.PackageManagement.Cmdlets.SavePackage
```

<span data-ttu-id="af6ec-154">__Předběžný hlavní příčinu__: technici identifikovat výpadku v rámci příslušného zprostředkovatele z obsahu doručit síť (CDN) Azure, který byl nasazen do Galerie prostředí PowerShell 5/17/2016.</span><span class="sxs-lookup"><span data-stu-id="af6ec-154">__Preliminary root cause__: Engineers identified an outage in the underlying provider of Azure Content Deliver Network (CDN), which was deployed to the PowerShell Gallery on 5/17/2016.</span></span>
<span data-ttu-id="af6ec-155">__Zmírnění dopadů__: technici zakázáno Azure CDN v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af6ec-155">__Mitigation__: Engineers disabled Azure CDN in the PowerShell Gallery.</span></span>
<span data-ttu-id="af6ec-156">__Další kroky__: prozkoumat základní příčiny a vývoj řešení, aby se zabránilo budoucna.</span><span class="sxs-lookup"><span data-stu-id="af6ec-156">__Next Steps__: Investigate the underlying root cause and developing a solution to prevent future occurrences.</span></span>