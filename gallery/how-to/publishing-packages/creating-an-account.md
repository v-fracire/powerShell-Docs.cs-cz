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
# <a name="creating-a-powershell-gallery-account"></a>Vytváří se účet Galerie prostředí PowerShell

Před publikováním nic v galerii prostředí PowerShell, musíte vytvořit účet Galerie prostředí PowerShell.
Galerie prostředí PowerShell účty musí být propojený s účtem přihlášení povolený e-mail. Tento účet může být účet služby Azure Active Directory nebo Microsoft ID, jako jsou e-mailového účtu outlook.com nebo hotmail.com.

Pokud chcete vytvořit účet Galerie prostředí PowerShell, přejděte na [ https://PowerShellGallery.com ](https://PowerShellGallery.com) a klikněte na **přihlášení** jak je znázorněno na následujícím obrázku.

![Zaregistrujte nový účet](../../Images/CreateAccount-Register.png)

Chcete-li použít účet služby Azure Active Directory, vyberte **pracovního nebo školního účtu**a přihlaste se pomocí svého účtu. Pokud chcete používat Microsoft ID, zvolte **osobní účet** a přihlaste se.

V dalším kroku se výzva k vytvoření uživatelského jména v galerii prostředí PowerShell. Seznamte se s podmínkami použití a zásadami ochrany osobních údajů, zadejte uživatelské jméno a potom klikněte na tlačítko **zaregistrovat**.

> [!NOTE]
> Po vytvoření nelze změnit název účtu. Další informace najdete v tématu [Správa vlastníků balíčku](managing-package-owners.md).

## <a name="recommended-practices-for-powershell-gallery-accounts"></a>Doporučené postupy pro účty Galerie prostředí PowerShell

Je důležité, abyste aktivně monitorovat e-mailový účet, používat s vaším účtem Galerie prostředí PowerShell. Veškerá komunikace s vlastníky balíčky Galerie prostředí PowerShell je prostřednictvím této e-mailovou adresu. Pokud provozní Galerie prostředí PowerShell tým nemůže kontaktovat vlastníka balíčku, nám může být nutné odstranit balíček.

Organizace, které často publikují v galerii prostředí PowerShell vytvořit jedinečný účet externích pro tento účel. Doporučujeme, abyste že použití předávání e-mailu přeposílat oznámení na adresu v rámci vaší organizace.

Když více vlastníkům jsou spojeny s balíčkem, se všechny Galerie prostředí PowerShell oznámení odesílat pro všechny vlastníky. Další informace najdete v tématu [Správa vlastníků balíčku](managing-package-owners.md).
