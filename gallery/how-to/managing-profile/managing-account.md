---
ms.date: 09/05/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Nastavení účtu galerie PowerShellu
ms.openlocfilehash: ebe784ec5aae5ff3a4d444d12a168ef38aaef65f
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002782"
---
# <a name="powershell-gallery-account-settings"></a><span data-ttu-id="d512d-103">Nastavení účtu galerie PowerShellu</span><span class="sxs-lookup"><span data-stu-id="d512d-103">PowerShell Gallery Account Settings</span></span>

<span data-ttu-id="d512d-104">Váš účet Galerie prostředí PowerShell je veřejně viditelný název, který je propojený s identitou.</span><span class="sxs-lookup"><span data-stu-id="d512d-104">Your PowerShell Gallery account is a publicly visible name that is linked to an identity.</span></span> <span data-ttu-id="d512d-105">Tato identita je buď Microsoft ID, jako je třeba `user@hotmail.com` nebo `user@outlook.com`, nebo účet Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="d512d-105">That identity is either a Microsoft ID, like `user@hotmail.com` or `user@outlook.com`, or an Azure Active Directory (AAD) account.</span></span>

<span data-ttu-id="d512d-106">Galerie prostředí PowerShell poskytuje následující nastavení účtu:</span><span class="sxs-lookup"><span data-stu-id="d512d-106">The PowerShell Gallery provides the following account settings:</span></span>

- <span data-ttu-id="d512d-107">E-mailový účet spojený s vaším účtem Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="d512d-107">The email account associated with your PowerShell Gallery account</span></span>
- <span data-ttu-id="d512d-108">Možnosti e-mailových oznámení odeslané z Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="d512d-108">Options for email notifications sent from the PowerShell Gallery</span></span>
- <span data-ttu-id="d512d-109">Uživatelský účet spojený s vaším účtem Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="d512d-109">The user account associated with your PowerShell Gallery account</span></span>
- <span data-ttu-id="d512d-110">Obrázek spojené s vaším účtem Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="d512d-110">The picture associated with your PowerShell Gallery account</span></span>

## <a name="email-address"></a><span data-ttu-id="d512d-111">E-mailová adresa</span><span class="sxs-lookup"><span data-stu-id="d512d-111">Email address</span></span>

<span data-ttu-id="d512d-112">E-mailová adresa je cílem pro oznámení Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d512d-112">The email address is the destination for PowerShell Gallery notifications.</span></span> <span data-ttu-id="d512d-113">Nemusí se shodovat s účtem přihlášení.</span><span class="sxs-lookup"><span data-stu-id="d512d-113">It does not have to match the login account.</span></span> <span data-ttu-id="d512d-114">Můžete použít libovolné e-mailový účet, ke kterým máte přístup.</span><span class="sxs-lookup"><span data-stu-id="d512d-114">You may use any email account you have access to.</span></span> <span data-ttu-id="d512d-115">E-mailová adresa zadaná v galerii prostředí PowerShell nikdy nesmí přímo ostatním uživatelům.</span><span class="sxs-lookup"><span data-stu-id="d512d-115">Your email address is never directly provided by the PowerShell Gallery to other users.</span></span>

![Změna e-mailovou adresu](../../Images/PSGallery_AcccountEmailAddress.png)

<span data-ttu-id="d512d-117">Po zadání nové e-mailová adresa se v galerii prostředí PowerShell odešle e-mailu ověřovací k této adrese.</span><span class="sxs-lookup"><span data-stu-id="d512d-117">When you enter a new email address, the PowerShell Gallery sends a verification mail to that address.</span></span> <span data-ttu-id="d512d-118">Ověření e-mailu obsahuje odkaz zpět do Galerie prostředí PowerShell, dokončete proces změn.</span><span class="sxs-lookup"><span data-stu-id="d512d-118">The verification mail contains a link back to the PowerShell Gallery to complete the change process.</span></span> <span data-ttu-id="d512d-119">Až do dokončení procesu ověření se všechna oznámení odeslané na adresu předchozí.</span><span class="sxs-lookup"><span data-stu-id="d512d-119">Until you complete the verification process, all notifications are sent to the previous address.</span></span>

## <a name="email-notifications"></a><span data-ttu-id="d512d-120">E-mailových oznámení</span><span class="sxs-lookup"><span data-stu-id="d512d-120">Email notifications</span></span>

<span data-ttu-id="d512d-121">Galerie prostředí PowerShell poskytuje následující možnosti oznámení:</span><span class="sxs-lookup"><span data-stu-id="d512d-121">PowerShell Gallery provides the following notification options:</span></span>

- <span data-ttu-id="d512d-122">Uživatelé mě mohli kontaktovat v galerii prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="d512d-122">Users can contact me through the PowerShell Gallery</span></span>
- <span data-ttu-id="d512d-123">Upozornit, když se balíček převede v galerii prostředí PowerShell pomocí svého účtu</span><span class="sxs-lookup"><span data-stu-id="d512d-123">Notify me when an package is pushed to the PowerShell Gallery using my account</span></span>

![Změna e-mailovou adresu](../../Images/PSGallery_AccountEmailOptions.png)

<span data-ttu-id="d512d-125">Důležité oznámení z Galerie prostředí PowerShell nejdou zakázat, jak je uvedeno na stránce.</span><span class="sxs-lookup"><span data-stu-id="d512d-125">As noted on the page, critical notifications from the PowerShell Gallery can't be disabled.</span></span>
<span data-ttu-id="d512d-126">Patří k nim:</span><span class="sxs-lookup"><span data-stu-id="d512d-126">These include:</span></span>

- <span data-ttu-id="d512d-127">Upozornění zabezpečení</span><span class="sxs-lookup"><span data-stu-id="d512d-127">Security notifications</span></span>
- <span data-ttu-id="d512d-128">Účet správy oznámení z Galerie prostředí PowerShell správce</span><span class="sxs-lookup"><span data-stu-id="d512d-128">Account management notifications from PowerShell Gallery administrators</span></span>
- <span data-ttu-id="d512d-129">Oznámení o testy spouštět pomocí Galerie prostředí PowerShell pro odesílání, které jste provedli</span><span class="sxs-lookup"><span data-stu-id="d512d-129">Notifications about the tests run by the PowerShell Gallery for submissions you have made</span></span>

## <a name="change-your-login-account"></a><span data-ttu-id="d512d-130">Změnit přihlašovací účet</span><span class="sxs-lookup"><span data-stu-id="d512d-130">Change your login account</span></span>

<span data-ttu-id="d512d-131">Chcete-li změnit přihlašovací účet, musíte být přihlášeni pomocí aktuálního účtu.</span><span class="sxs-lookup"><span data-stu-id="d512d-131">To change the login account, you must be signed in with the current account.</span></span> <span data-ttu-id="d512d-132">K dokončení změny použijte následující postup.</span><span class="sxs-lookup"><span data-stu-id="d512d-132">Use the following steps to complete the change.</span></span>

![Nastavení účtu přihlášení](../../Images/PSGallery_LoginAccountSettings.png)

1. <span data-ttu-id="d512d-134">Klikněte na **změnit účet**.</span><span class="sxs-lookup"><span data-stu-id="d512d-134">Click on **Change Account**.</span></span> <span data-ttu-id="d512d-135">Automaticky otevírané okno vysvětluje, že změna přihlášení účtu vztahuje na všechna použití daného účtu v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d512d-135">A pop-up window explains that changing the login account applies to all uses of that account in the PowerShell Gallery.</span></span> <span data-ttu-id="d512d-136">Přečtěte si informace a pak klikněte na **OK** pokračujte.</span><span class="sxs-lookup"><span data-stu-id="d512d-136">Review the information, then click **OK** to continue.</span></span>

   ![Nastavení účtu přihlášení](../../Images/PSGallery_LoginAccountChange-1.png)

2. <span data-ttu-id="d512d-138">Zobrazí se výzva k přihlášení pomocí _nový účet_.</span><span class="sxs-lookup"><span data-stu-id="d512d-138">You are then prompted to sign in using the _new account_.</span></span>

   ![Nastavení účtu přihlášení](../../Images/PSGallery_LoginAccountChange-2.png)

3. <span data-ttu-id="d512d-140">Po kliknutí na **Další**, zobrazí se zpráva, že jste přihlášeni pomocí aktuálního účtu.</span><span class="sxs-lookup"><span data-stu-id="d512d-140">When you click **Next**, you see a message that you are signed in using the current account.</span></span>
   <span data-ttu-id="d512d-141">Klikněte na tlačítko **přihlásit na více instancí a přihlaste se pomocí jiného účtu**.</span><span class="sxs-lookup"><span data-stu-id="d512d-141">Click **Sign out and sign in with a different account**.</span></span>

   ![Nastavení účtu přihlášení](../../Images/PSGallery_LoginAccountChange-3.png)

4. <span data-ttu-id="d512d-143">Zadejte heslo pro nový účet.</span><span class="sxs-lookup"><span data-stu-id="d512d-143">Enter the password of the new account.</span></span> <span data-ttu-id="d512d-144">Po zadání hesla, budete přesměrováni zpět na stránku nastavení účtu znázorňující, že účet přihlášení byl aktualizován.</span><span class="sxs-lookup"><span data-stu-id="d512d-144">After entering the password, you are returned to the Account Settings page showing you that the login account has been updated.</span></span>


## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="d512d-145">Povolení dvoufaktorového ověřování (2FA)</span><span class="sxs-lookup"><span data-stu-id="d512d-145">Enable Two-Factor Authentication (2FA)</span></span>

<span data-ttu-id="d512d-146">Dvoufaktorové ověřování doporučujeme pro všechny uživatele, kteří ručně publikovat v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d512d-146">Two-factor authentication is recommended for all users who publish manually to the PowerShell Gallery.</span></span> <span data-ttu-id="d512d-147">Pokud chcete povolit dvoufaktorové ověřování, přihlašovací účet musí mít alespoň dva typy ověřování zaregistrovaný.</span><span class="sxs-lookup"><span data-stu-id="d512d-147">To enable two-factor authentication, the login account must have at least two forms of authentication registered.</span></span> <span data-ttu-id="d512d-148">Jeden je heslo a může být jiné:</span><span class="sxs-lookup"><span data-stu-id="d512d-148">One is a password and the other forms can be:</span></span>

- <span data-ttu-id="d512d-149">Telefonní číslo, které můžou přijímat textové zprávy</span><span class="sxs-lookup"><span data-stu-id="d512d-149">A phone number that can receive text messages</span></span>
- <span data-ttu-id="d512d-150">Registrovaný ověřovací aplikace, jako je například Microsoft Authenticator pro váš mobilní telefon</span><span class="sxs-lookup"><span data-stu-id="d512d-150">A registered authenticator application, such as Microsoft Authenticator for your mobile phone</span></span>

<span data-ttu-id="d512d-151">Tyto formy ověřování musí být nakonfigurován v informace o vašem účtu AAD nebo v nastavení zabezpečení ID účtu Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d512d-151">These forms of authentication must be configured in your AAD account information or in your Microsoft ID Account Security settings.</span></span>

<span data-ttu-id="d512d-152">Jakmile povolíte službu 2FA, musíte se ověřit pomocí nakonfigurovaného formy ověřování pokaždé, když se přihlásíte do Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d512d-152">Once 2FA is enabled, you are required to authenticate using the configured forms of authentication every time you sign in to the PowerShell Gallery.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d512d-153">Povolení dvoufaktorového ověřování pro galerii prostředí PowerShell nevyžaduje, abyste zapnuli 2FA pro všechny výskyty přihlašovací účet.</span><span class="sxs-lookup"><span data-stu-id="d512d-153">Enabling two-factor authentication for the PowerShell Gallery site does not require you to enable 2FA for all uses of your login account.</span></span> <span data-ttu-id="d512d-154">Další informace najdete v tématu [o dvoustupňovém ověřování](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span><span class="sxs-lookup"><span data-stu-id="d512d-154">For more information, see [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span>

## <a name="change-your-profile-picture"></a><span data-ttu-id="d512d-155">Změnit váš profilový obrázek</span><span class="sxs-lookup"><span data-stu-id="d512d-155">Change your profile picture</span></span>

<span data-ttu-id="d512d-156">Galerie prostředí PowerShell spoléhá na Gravatar k uložení a zobrazení obrázku přidružený k profilu.</span><span class="sxs-lookup"><span data-stu-id="d512d-156">The PowerShell Gallery relies on Gravatar to store and display the picture associated with your profile.</span></span> <span data-ttu-id="d512d-157">Pokud chcete aktualizovat váš profilový obrázek, navštivte [Gravatar.com](http://www.gravatar.com/).</span><span class="sxs-lookup"><span data-stu-id="d512d-157">To update your profile image, visit [Gravatar.com](http://www.gravatar.com/).</span></span>
