---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "Galerie prostředí powershell, rutiny, psgallery"
title: "Vytvoření účtu Galerie prostředí PowerShell"
ms.openlocfilehash: e21575320f220c1ba7ecd9bd464a814b3ebf49d9
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
## <a name="creating-a-powershell-gallery-account"></a><span data-ttu-id="e51d1-103">Vytvoření účtu Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e51d1-103">Creating a PowerShell Gallery Account</span></span>

<span data-ttu-id="e51d1-104">Před publikováním nic do Galerie prostředí PowerShell, je nutné vytvořit účet Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e51d1-104">A PowerShell Gallery account must be established before publishing anything to the PowerShell Gallery.</span></span> <span data-ttu-id="e51d1-105">Galerie prostředí PowerShell účty musí být propojena s povoleným e-mailu účtu Azure Active Directory nebo e-mailový účet Microsoft (s doménou outlook.com, hotmail.com, atd.)</span><span class="sxs-lookup"><span data-stu-id="e51d1-105">The PowerShell Gallery accounts must be linked to an Azure Active Directory email-enabled account, or a Microsoft email account (with a domain of outlook.com, hotmail.com, etc.)</span></span>

<span data-ttu-id="e51d1-106">Chcete-li vytvořit účet Galerie prostředí PowerShell, přejděte na https://PowerShellGallery.com a klikněte na "Register" (viz následující obrázek).</span><span class="sxs-lookup"><span data-stu-id="e51d1-106">To create a PowerShell Gallery account, go to https://PowerShellGallery.com and click on "Register" (see the image below).</span></span> 

![Zaregistrovat nový účet](./images/CreatingAccount-Register.png)

<span data-ttu-id="e51d1-108">Na další stránce Pokud chcete používat účet služby Azure Active Directory, vyberte "Pracovní nebo školní účet" a přihlaste se pomocí účtu.</span><span class="sxs-lookup"><span data-stu-id="e51d1-108">In the next page, to use an Azure Active Directory account, select "Work or School Account", and log in with your account.</span></span> <span data-ttu-id="e51d1-109">Použít účet Microsoft - například ten, který v doméně Hotmail.com nebo Outlook.com – zvolte "Osobní účet" a přihlaste se.</span><span class="sxs-lookup"><span data-stu-id="e51d1-109">To use a Microsoft account - such as one in a Hotmail.com or Outlook.com domain - choose "Personal Account", and log in.</span></span> 

<span data-ttu-id="e51d1-110">Jakmile jste přihlášení, vyzve k vytvoření uživatelské jméno pro galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e51d1-110">Once you have logged in, you will be prompted to create a username for the PowerShell Gallery.</span></span> <span data-ttu-id="e51d1-111">Přečtěte si podmínky použití a zásady ochrany osobních údajů, které jsou propojeny v, zadejte uživatelské jméno a potom kliknutím na tlačítko Registrovat.</span><span class="sxs-lookup"><span data-stu-id="e51d1-111">Review the Terms of Use and Privacy Policy that are linked in, enter a username, and then click Register.</span></span>

<span data-ttu-id="e51d1-112">Poznámka: Tento název účtu nelze změnit po vytvoření.</span><span class="sxs-lookup"><span data-stu-id="e51d1-112">Note: This account name cannot be changed once it is created.</span></span>  
<span data-ttu-id="e51d1-113">V tématu [Správa vlastníků položky](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/managing-item-owners) další podrobnosti týkající se to.</span><span class="sxs-lookup"><span data-stu-id="e51d1-113">See [Managing Item Owners](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/managing-item-owners) for additional details related to this.</span></span>

## <a name="recommended-practices-for-powershell-gallery-accounts"></a><span data-ttu-id="e51d1-114">Doporučené postupy pro účty Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e51d1-114">Recommended Practices for PowerShell Gallery Accounts</span></span>

<span data-ttu-id="e51d1-115">Je důležité, aby e-mailový účet, který používá s vaším účtem Galerie prostředí PowerShell aktivně sledovat.</span><span class="sxs-lookup"><span data-stu-id="e51d1-115">It is important that the email account used with your PowerShell Gallery account be actively monitored.</span></span>
<span data-ttu-id="e51d1-116">Všechny communiction s vlastníci položky galerie prostředí PowerShell je e-mailem na adresu spojenou s vaším účtem Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e51d1-116">All communiction with owners of PowerShell Gallery items is through the email using the address associated with your PowerShell Gallery account.</span></span>
<span data-ttu-id="e51d1-117">Pokud jsme nelze kontaktovat vlastníka položek, může být provozní tým nutné odstranit položku za určitých okolností.</span><span class="sxs-lookup"><span data-stu-id="e51d1-117">If we are unable to contact an item owner, the Operations team may be required to delete an item under some circumstances.</span></span>

<span data-ttu-id="e51d1-118">Organizace, které často publikovat do Galerie prostředí PowerShell vytvořit jedinečný účet pro tento účel v Outlook.com nebo jiné domény, účet Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e51d1-118">Organizations that publish to the PowerShell Gallery often create a unique account for that purpose in Outlook.com, or another Microsoft account domain.</span></span>
<span data-ttu-id="e51d1-119">V mnoha případech není pravidelně sledovat tento účet.</span><span class="sxs-lookup"><span data-stu-id="e51d1-119">In many cases that account is not regularly monitored.</span></span> <span data-ttu-id="e51d1-120">Osvědčeným postupem je v takovém případě používat předávání Outlook k odesílání e-mailu na jiný účet, obvykle jednu v rámci organizace, které se budou monitorovat pomocí položky vlastníka/vlastníků.</span><span class="sxs-lookup"><span data-stu-id="e51d1-120">A best practice in that case is to use Outlook Forwarding to send email to another account, typically one within the organization, that will be monitored by the item owner(s).</span></span>

<span data-ttu-id="e51d1-121">Pokud existují více vlastníky přidružený k položce, bude veškerá komunikace, které pocházejí z Galerie Powershellu přejděte na všechny vlastníky.</span><span class="sxs-lookup"><span data-stu-id="e51d1-121">If there are multiple owners associated with an item, all communications that come from the PowerShell Gallery will go to all owners.</span></span>
<span data-ttu-id="e51d1-122">V tématu [Správa vlastníků položky](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/managing-item-owners) další podrobnosti o přidání vlastníky k položce.</span><span class="sxs-lookup"><span data-stu-id="e51d1-122">See [Managing Item Owners](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/managing-item-owners) for additional details on adding owners to an item.</span></span> 
