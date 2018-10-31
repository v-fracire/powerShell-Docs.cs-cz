---
ms.date: 09/11/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Vytváří se účet Galerie prostředí PowerShell
ms.openlocfilehash: e4cf73edb03267cff6bbcc0cf3b754225e45be9f
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004016"
---
# <a name="creating-a-powershell-gallery-account"></a><span data-ttu-id="3584e-103">Vytváří se účet Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="3584e-103">Creating a PowerShell Gallery account</span></span>

<span data-ttu-id="3584e-104">Před publikováním nic v galerii prostředí PowerShell, musíte vytvořit účet Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3584e-104">You must create a PowerShell Gallery account before publishing anything to the PowerShell Gallery.</span></span>
<span data-ttu-id="3584e-105">Galerie prostředí PowerShell účty musí být propojený s účtem přihlášení povolený e-mail.</span><span class="sxs-lookup"><span data-stu-id="3584e-105">PowerShell Gallery accounts must be linked to an email-enabled login account.</span></span> <span data-ttu-id="3584e-106">Tento účet může být účet služby Azure Active Directory nebo Microsoft ID, jako jsou e-mailového účtu outlook.com nebo hotmail.com.</span><span class="sxs-lookup"><span data-stu-id="3584e-106">This account can be an Azure Active Directory account or a Microsoft ID, like an email account from outlook.com or hotmail.com.</span></span>

<span data-ttu-id="3584e-107">Pokud chcete vytvořit účet Galerie prostředí PowerShell, přejděte na [ https://PowerShellGallery.com ](https://PowerShellGallery.com) a klikněte na **přihlášení** jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="3584e-107">To create a PowerShell Gallery account, go to [https://PowerShellGallery.com](https://PowerShellGallery.com) and click on **Sign in** as shown in the following image.</span></span>

![Zaregistrujte nový účet](../../Images/CreateAccount-Register.png)

<span data-ttu-id="3584e-109">Chcete-li použít účet služby Azure Active Directory, vyberte **pracovního nebo školního účtu**a přihlaste se pomocí svého účtu.</span><span class="sxs-lookup"><span data-stu-id="3584e-109">To use an Azure Active Directory account, select **Work or School Account**, and sign in with your account.</span></span> <span data-ttu-id="3584e-110">Pokud chcete používat Microsoft ID, zvolte **osobní účet** a přihlaste se.</span><span class="sxs-lookup"><span data-stu-id="3584e-110">To use a Microsoft ID, choose **Personal Account** and sign in.</span></span>

<span data-ttu-id="3584e-111">V dalším kroku se výzva k vytvoření uživatelského jména v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3584e-111">Next, you are prompted to create a username for the PowerShell Gallery.</span></span> <span data-ttu-id="3584e-112">Seznamte se s podmínkami použití a zásadami ochrany osobních údajů, zadejte uživatelské jméno a potom klikněte na tlačítko **zaregistrovat**.</span><span class="sxs-lookup"><span data-stu-id="3584e-112">Review the Terms of Use and Privacy Policy, enter a username, and then click **Register**.</span></span>

> [!NOTE]
> <span data-ttu-id="3584e-113">Po vytvoření nelze změnit název účtu.</span><span class="sxs-lookup"><span data-stu-id="3584e-113">The account name cannot be changed once it is created.</span></span> <span data-ttu-id="3584e-114">Další informace najdete v tématu [Správa vlastníků balíčku](managing-package-owners.md).</span><span class="sxs-lookup"><span data-stu-id="3584e-114">For more information, see [Managing Package Owners](managing-package-owners.md).</span></span>

## <a name="recommended-practices-for-powershell-gallery-accounts"></a><span data-ttu-id="3584e-115">Doporučené postupy pro účty Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="3584e-115">Recommended practices for PowerShell Gallery accounts</span></span>

<span data-ttu-id="3584e-116">Je důležité, abyste aktivně monitorovat e-mailový účet, používat s vaším účtem Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3584e-116">It's important to actively monitor the email account used with your PowerShell Gallery account.</span></span> <span data-ttu-id="3584e-117">Veškerá komunikace s vlastníky balíčky Galerie prostředí PowerShell je prostřednictvím této e-mailovou adresu.</span><span class="sxs-lookup"><span data-stu-id="3584e-117">All communication with owners of PowerShell Gallery packages is through this email address.</span></span> <span data-ttu-id="3584e-118">Pokud provozní Galerie prostředí PowerShell tým nemůže kontaktovat vlastníka balíčku, nám může být nutné odstranit balíček.</span><span class="sxs-lookup"><span data-stu-id="3584e-118">If the PowerShell Gallery Operations team is unable to contact a package owner, we may be required to delete a package.</span></span>

<span data-ttu-id="3584e-119">Organizace, které často publikují v galerii prostředí PowerShell vytvořit jedinečný účet externích pro tento účel.</span><span class="sxs-lookup"><span data-stu-id="3584e-119">Organizations that publish to the PowerShell Gallery often create a unique external account for that purpose.</span></span> <span data-ttu-id="3584e-120">Doporučujeme, abyste že použití předávání e-mailu přeposílat oznámení na adresu v rámci vaší organizace.</span><span class="sxs-lookup"><span data-stu-id="3584e-120">We recommend you use email forwarding to forward notifications to an address within your organization.</span></span>

<span data-ttu-id="3584e-121">Když více vlastníkům jsou spojeny s balíčkem, se všechny Galerie prostředí PowerShell oznámení odesílat pro všechny vlastníky.</span><span class="sxs-lookup"><span data-stu-id="3584e-121">When multiple owners are associated with a package, all PowerShell Gallery notifications are sent to all owners.</span></span> <span data-ttu-id="3584e-122">Další informace najdete v tématu [Správa vlastníků balíčku](managing-package-owners.md).</span><span class="sxs-lookup"><span data-stu-id="3584e-122">For more information, see [Managing Package Owners](managing-package-owners.md).</span></span>
