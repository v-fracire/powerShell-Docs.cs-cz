---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Správa vlastníků balíčku
ms.openlocfilehash: 5cf26a7195ac446177cbb7f3a055e8e0a78569cc
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004033"
---
# <a name="managing-package-owners"></a>Správa vlastníků balíčku

Vlastnictví balíčku v galerii prostředí PowerShell je definována vydavatele balíček do galerie.
Tato metadata je někdy potřeba spravovat nad rámec počáteční balíček publikování, což znamená, že vlastník metadat musí být Měnitelná při samotném balíčku není.

Všechny vlastníky balíčku se partnerské uzly.
To znamená, že všechny vlastníka balíčku můžete publikovat novou verzi balíčku. Také znamená, že všechny vlastníka balíčku můžete odebrat ostatní vlastníka balíčku.
Žádný vlastník má více oprávnění než další vlastníky.

## <a name="setting-a-packages-initial-owner"></a>Nastavení původního vlastníka balíčku

Při publikování nového balíčku do Galerie prostředí PowerShell původního vlastníka je definovaný uživatelem, která publikuje balíček. To je určen, rozhraním API, jejichž klíč použila rutinu Publish-Module.

## <a name="adding-owners"></a>Přidávají se vlastníci

Jakmile balíčku se publikoval do Galerie prostředí PowerShell, velmi snadno pozvat další uživatele se vlastníky balíčku.

1. [Přihlaste se na](https://powershellgallery.com/users/account/LogOn) v galerii prostředí PowerShell pomocí účtu, který je aktuální vlastník balíčku.
2. Přejděte na stránku balíčku na kartě "Položky", hledání nebo kliknutím na své uživatelské jméno a potom [ **spravovat Moje balíčky**](https://www.powershellgallery.com/account/Packages).
3. Po přihlášení se jako vlastník balíčku, je na levé straně klikněte na odkaz Spravovat vlastníky.
4. Zadejte uživatelské jméno osoby, které chcete přidat jako vlastníka a klikněte na tlačítko 'Přidat'.
5. E-mailu se pak posílají do nové spoluvlastník jako pozvánku k vlastníka balíčku.
6. Jakmile se tento uživatel klikne na odkaz, jsou úplné spoluvlastník s úplnou kontrolou nad balíček, včetně možnosti odebírat další uživatele jako vlastníky.

**Poznámka:**: dokud nový vlastník potvrdí vlastnictví, jejich *nebudou* uvedení jako vlastníci balíčku.
Při prohlížení **Spravovat vlastníky** stránky, zobrazí se položka "čekající na schválení" aktuální vlastníky.
Je možné odebrat tuto pozvánku; stejně jako další vlastníky je možné odebrat.
Tento proces pozvánky zabraňuje uživatelům falešně přidávání jiných uživatelů jako vlastníky své balíčky.

Mějte na paměti, že metadata "Autoři" je čistě volný text; pouze vlastníci"" jsou řízeny.


## <a name="removing-owners"></a>Odebrat vlastníky

Když balíček obsahuje více vlastníkům a jeden je potřeba odebrat, tento proces je prostý:

1. [Přihlaste se na](https://powershellgallery.com/users/account/LogOn) galerii prostředí PowerShell pomocí účtu, který je aktuální vlastník balíčku.
2. Přejděte na stránku balíčku na kartě balíčky, hledání nebo kliknutím na své uživatelské jméno a potom [ **spravovat Moje balíčky**](https://www.powershellgallery.com/account/Packages).
3. Po přihlášení se jako vlastník balíčku, je na levé straně klikněte na tlačítko; Spravovat vlastníky odkaz
4. Klikněte na odkaz "Odebrat" vedle vlastníka k odebrání.



## <a name="transferring-package-ownership"></a>Přenos vlastnictví balíčku

Někdy získáme žádosti o podporu pro přenos vlastnictví balíčku z jednoho uživatele do jiného, ale můžete téměř vždy provést sami.
Přenosu vlastnictví z jednoho uživatele je jednoduše kombinace obou funkcí výše.

1. Aktuální vlastník vyzývá nového uživatele, aby se spoluvlastník a nový uživatel přijme pozvánku;
2. Nový uživatel odebere staré uživatele ze seznamu vlastníků.

Tento požadavek má spadají několika formuláře, ale proces funguje stejně.

- Vlastnictví balíčku se mění z jeden vývojář na jiný
- Balíček byl náhodnému publikování pomocí k nesprávnému účtu.


## <a name="orphaned-packages"></a>Osamocené balíčky

Došlo k poslední jeden scénář, ale ne mnohokrát.
Balíčky se staly osamocené položky a pouze vlastník účtu balíčku nelze použít k přidání novým vlastníkům.
Tady je několik příkladů tohoto scénáře:

- Vlastníka účtu je spojen s e-mailovou adresu, která už existuje a uživatel zapomněl svoje heslo
- Registrovaný vlastník opustil společnost, která vytvoří balíček a je nedostupné k aktualizaci balíčku vlastnictví
- Kvůli chybě, která má vliv jenom na několik balíčků balíček je nějakým způsobem ownerless v galerii

Správci Galerie prostředí PowerShell můžete přistupovat k Spravovat vlastníky propojení pro všechny balíčky.
Pokud jsou právoplatného vlastníka balíčku a kontaktovat aktuálního vlastníka k získání vlastnictví oprávnění, použijte odkaz "Ohlášení zneužití" v galerii k dosažení správci Galerie prostředí PowerShell.
Pak budeme postupovat procesu ověřit vlastnictví balíčku.
Pokud vyhodnotíme, že by měl být vlastníka balíčku, budeme používali odkaz Spravovat vlastníky pro tento balíček a odeslat pozvánku pro stát vlastníkem.
Pouze Uděláme to po ověření, že by měl být vlastníkem a tento proces se liší podle okolností.
Častým použije adresu URL projektu daného balíčku hledal způsob, jak se obraťte na správce projektu, ale můžeme také používat Twitter, e-mailu nebo jiným způsobem pro kontaktování Vlastník projektu.
