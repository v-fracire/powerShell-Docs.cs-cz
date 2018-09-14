---
ms.date: 09/11/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Vytváří se účet Galerie prostředí PowerShell
ms.openlocfilehash: 08d18310d9e18b00bd9e22efcc552dfd29f8982c
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522822"
---
# <a name="creating-a-powershell-gallery-account"></a><span data-ttu-id="98b65-103">Vytváří se účet Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="98b65-103">Creating a PowerShell Gallery account</span></span>

<span data-ttu-id="98b65-104">Před publikováním nic v galerii prostředí PowerShell, musíte vytvořit účet Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98b65-104">You must create a PowerShell Gallery account before publishing anything to the PowerShell Gallery.</span></span>
<span data-ttu-id="98b65-105">Galerie prostředí PowerShell účty musí být propojený s účtem přihlášení povolený e-mail.</span><span class="sxs-lookup"><span data-stu-id="98b65-105">PowerShell Gallery accounts must be linked to an email-enabled login account.</span></span> <span data-ttu-id="98b65-106">Tento účet může být účet služby Azure Active Directory nebo Microsoft ID, jako jsou e-mailového účtu outlook.com nebo hotmail.com.</span><span class="sxs-lookup"><span data-stu-id="98b65-106">This account can be an Azure Active Directory account or a Microsoft ID, like an email account from outlook.com or hotmail.com.</span></span>

<span data-ttu-id="98b65-107">Pokud chcete vytvořit účet Galerie prostředí PowerShell, přejděte na [ https://PowerShellGallery.com ](https://PowerShellGallery.com) a klikněte na **přihlášení** jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="98b65-107">To create a PowerShell Gallery account, go to [https://PowerShellGallery.com](https://PowerShellGallery.com) and click on **Sign in** as shown in the following image.</span></span>

![Zaregistrujte nový účet](../../Images/CreateAccount-Register.png)

<span data-ttu-id="98b65-109">Chcete-li použít účet služby Azure Active Directory, vyberte **pracovního nebo školního účtu**a přihlaste se pomocí svého účtu.</span><span class="sxs-lookup"><span data-stu-id="98b65-109">To use an Azure Active Directory account, select **Work or School Account**, and sign in with your account.</span></span> <span data-ttu-id="98b65-110">Pokud chcete používat Microsoft ID, zvolte **osobní účet** a přihlaste se.</span><span class="sxs-lookup"><span data-stu-id="98b65-110">To use a Microsoft ID, choose **Personal Account** and sign in.</span></span>

<span data-ttu-id="98b65-111">V dalším kroku se výzva k vytvoření uživatelského jména v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98b65-111">Next, you are prompted to create a username for the PowerShell Gallery.</span></span> <span data-ttu-id="98b65-112">Seznamte se s podmínkami použití a zásadami ochrany osobních údajů, zadejte uživatelské jméno a potom klikněte na tlačítko **zaregistrovat**.</span><span class="sxs-lookup"><span data-stu-id="98b65-112">Review the Terms of Use and Privacy Policy, enter a username, and then click **Register**.</span></span>

> [!NOTE]
> <span data-ttu-id="98b65-113">Po vytvoření nelze změnit název účtu.</span><span class="sxs-lookup"><span data-stu-id="98b65-113">The account name cannot be changed once it is created.</span></span> <span data-ttu-id="98b65-114">Další informace najdete v tématu [Správa vlastníků položek](managing-item-owners.md).</span><span class="sxs-lookup"><span data-stu-id="98b65-114">For more information, see [Managing Item Owners](managing-item-owners.md).</span></span>

## <a name="recommended-practices-for-powershell-gallery-accounts"></a><span data-ttu-id="98b65-115">Doporučené postupy pro účty Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="98b65-115">Recommended practices for PowerShell Gallery accounts</span></span>

<span data-ttu-id="98b65-116">Je důležité, abyste aktivně monitorovat e-mailový účet, používat s vaším účtem Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98b65-116">It's important to actively monitor the email account used with your PowerShell Gallery account.</span></span> <span data-ttu-id="98b65-117">Veškerá komunikace s vlastníky položky galerie prostředí PowerShell je prostřednictvím této e-mailovou adresu.</span><span class="sxs-lookup"><span data-stu-id="98b65-117">All communication with owners of PowerShell Gallery items is through this email address.</span></span> <span data-ttu-id="98b65-118">Pokud provozní Galerie prostředí PowerShell tým nemůže kontaktovat vlastníka položky, nám může být nutné odstranit položku.</span><span class="sxs-lookup"><span data-stu-id="98b65-118">If the PowerShell Gallery Operations team is unable to contact an item owner, we may be required to delete an item.</span></span>

<span data-ttu-id="98b65-119">Organizace, které často publikují v galerii prostředí PowerShell vytvořit jedinečný účet externích pro tento účel.</span><span class="sxs-lookup"><span data-stu-id="98b65-119">Organizations that publish to the PowerShell Gallery often create a unique external account for that purpose.</span></span> <span data-ttu-id="98b65-120">Doporučujeme, abyste že použití předávání e-mailu přeposílat oznámení na adresu v rámci vaší organizace.</span><span class="sxs-lookup"><span data-stu-id="98b65-120">We recommend you use email forwarding to forward notifications to an address within your organization.</span></span>

<span data-ttu-id="98b65-121">Když více vlastníkům jsou spojeny s položkou, se všechny Galerie prostředí PowerShell oznámení odesílat pro všechny vlastníky.</span><span class="sxs-lookup"><span data-stu-id="98b65-121">When multiple owners are associated with an item, all PowerShell Gallery notifications are sent to all owners.</span></span> <span data-ttu-id="98b65-122">Další informace najdete v tématu [Správa vlastníků položek](managing-item-owners.md).</span><span class="sxs-lookup"><span data-stu-id="98b65-122">For more information, see [Managing Item Owners](managing-item-owners.md).</span></span>
