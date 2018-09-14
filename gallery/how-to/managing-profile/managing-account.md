---
ms.date: 09/05/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Nastavení účtu Galerie prostředí PowerShell
ms.openlocfilehash: dd7b8b3a99b5b7fbfec5d7f82b81dd6d5cfb906c
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523308"
---
# <a name="powershell-gallery-account-settings"></a>Nastavení účtu Galerie prostředí PowerShell

Váš účet Galerie prostředí PowerShell je veřejně viditelný název, který je propojený s identitou. Tato identita je buď Microsoft ID, jako je třeba `user@hotmail.com` nebo `user@outlook.com`, nebo účet Azure Active Directory (AAD).

Galerie prostředí PowerShell poskytuje následující nastavení účtu:

- E-mailový účet spojený s vaším účtem Galerie prostředí PowerShell
- Možnosti e-mailových oznámení odeslané z Galerie prostředí PowerShell
- Uživatelský účet spojený s vaším účtem Galerie prostředí PowerShell
- Obrázek spojené s vaším účtem Galerie prostředí PowerShell

## <a name="email-address"></a>E-mailová adresa

E-mailová adresa je cílem pro oznámení Galerie prostředí PowerShell. Nemusí se shodovat s účtem přihlášení. Můžete použít libovolné e-mailový účet, ke kterým máte přístup. E-mailová adresa zadaná v galerii prostředí PowerShell nikdy nesmí přímo ostatním uživatelům.

![Změna e-mailovou adresu](../../Images/PSGallery_AcccountEmailAddress.png)

Po zadání nové e-mailová adresa se v galerii prostředí PowerShell odešle e-mailu ověřovací k této adrese. Ověření e-mailu obsahuje odkaz zpět do Galerie prostředí PowerShell, dokončete proces změn. Až do dokončení procesu ověření se všechna oznámení odeslané na adresu předchozí.

## <a name="email-notifications"></a>E-mailových oznámení

Galerie prostředí PowerShell poskytuje následující možnosti oznámení:

- Uživatelé mě mohli kontaktovat v galerii prostředí PowerShell
- Upozornit, když se položka převede do Galerie prostředí PowerShell pomocí svého účtu

![Změna e-mailovou adresu](../../Images/PSGallery_AccountEmailOptions.png)

Důležité oznámení z Galerie prostředí PowerShell nejdou zakázat, jak je uvedeno na stránce.
Patří k nim:

- Upozornění zabezpečení
- Účet správy oznámení z Galerie prostředí PowerShell správce
- Oznámení o testy spouštět pomocí Galerie prostředí PowerShell pro odesílání, které jste provedli

## <a name="change-your-login-account"></a>Změnit přihlašovací účet

Chcete-li změnit přihlašovací účet, musíte být přihlášeni pomocí aktuálního účtu. K dokončení změny použijte následující postup.

![Nastavení účtu přihlášení](../../Images/PSGallery_LoginAccountSettings.png)

1. Klikněte na **změnit účet**. Automaticky otevírané okno vysvětluje, že změna přihlášení účtu vztahuje na všechna použití daného účtu v galerii prostředí PowerShell. Přečtěte si informace a pak klikněte na **OK** pokračujte.

   ![Nastavení účtu přihlášení](../../Images/PSGallery_LoginAccountChange-1.png)

2. Zobrazí se výzva k přihlášení pomocí _nový účet_.

   ![Nastavení účtu přihlášení](../../Images/PSGallery_LoginAccountChange-2.png)

3. Po kliknutí na **Další**, zobrazí se zpráva, že jste přihlášeni pomocí aktuálního účtu.
   Klikněte na tlačítko **přihlásit na více instancí a přihlaste se pomocí jiného účtu**.

   ![Nastavení účtu přihlášení](../../Images/PSGallery_LoginAccountChange-3.png)

4. Zadejte heslo pro nový účet. Po zadání hesla, budete přesměrováni zpět na stránku nastavení účtu znázorňující, že účet přihlášení byl aktualizován.


## <a name="enable-two-factor-authentication-2fa"></a>Povolení dvoufaktorového ověřování (2FA)

Dvoufaktorové ověřování doporučujeme pro všechny uživatele, kteří ručně publikovat v galerii prostředí PowerShell. Pokud chcete povolit dvoufaktorové ověřování, přihlašovací účet musí mít alespoň dva typy ověřování zaregistrovaný. Jeden je heslo a může být jiné:

- Telefonní číslo, které můžou přijímat textové zprávy
- Registrovaný ověřovací aplikace, jako je například Microsoft Authenticator pro váš mobilní telefon

Tyto formy ověřování musí být nakonfigurován v informace o vašem účtu AAD nebo v nastavení zabezpečení ID účtu Microsoft.

Jakmile povolíte službu 2FA, musíte se ověřit pomocí nakonfigurovaného formy ověřování pokaždé, když se přihlásíte do Galerie prostředí PowerShell.

> [!IMPORTANT]
> Povolení dvoufaktorového ověřování pro galerii prostředí PowerShell nevyžaduje, abyste zapnuli 2FA pro všechny výskyty přihlašovací účet. Další informace najdete v tématu [o dvoustupňovém ověřování](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).

## <a name="change-your-profile-picture"></a>Změnit váš profilový obrázek

Galerie prostředí PowerShell spoléhá na Gravatar k uložení a zobrazení obrázku přidružený k profilu. Pokud chcete aktualizovat váš profilový obrázek, navštivte [Gravatar.com](http://www.gravatar.com/).
