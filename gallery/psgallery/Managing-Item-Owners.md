---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery
title: Správa vlastníků položek
ms.openlocfilehash: e550b74ebde00cfbb154dbf4fb1fa4ae0582e029
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="managing-item-owners"></a>Správa vlastníků položek

Vlastnictví položky v galerii prostředí PowerShell je definována položka kdo publikoval do galerie.
V některých případech je potřeba spravovat nad rámec publikování počáteční položky, což znamená, že metadata vlastník musí být měnitelný při samotnou položku není tato metadata.

Všechny položky vlastníky jsou partnerské uzly.
To znamená, že všechny položky vlastníka můžete publikovat novou verzi položky. Taky to znamená, že vlastník všechny položky můžete odebrat všechny ostatní položky vlastníka.
Vlastník má další autority než ostatní vlastníky.

## <a name="setting-an-items-initial-owner"></a>Nastavení počáteční vlastník položky

Při publikování nové položky galerie prostředí PowerShell, vlastník počáteční definované uživatelem, který publikované položky. To je určen, jejichž rozhraní API klíče v rutině modulu publikovat.

## <a name="adding-owners"></a>Přidání vlastníky

Jakmile položku se publikoval do Galerie prostředí PowerShell, je snadné pozvaným dalším uživatelům stane vlastníci položky.

1. [Přihlaste se](https://powershellgallery.com/users/account/LogOn) do Galerie prostředí PowerShell pomocí účtu, který je vlastníkem aktuální položky.
2. Přejděte na stránku položku na kartě "položky, hledání nebo kliknutím na své uživatelské jméno a potom [ **spravovat Moje položky**](https://www.powershellgallery.com/account/Packages).
3. Při přihlášení se jako vlastník položky, je na levé straně klikněte na odkaz Spravovat vlastníky.
4. Zadejte uživatelské jméno osoby, k přidání jako vlastníka a klikněte na tlačítko "Přidat".
5. E-mailu se pak posílají do nové spoluvlastník jako Pozvánka se vlastníkem položku.
6. Jakmile tento uživatel klikne na odkaz, nejsou úplné spoluvlastník s plnou kontrolu nad položku, včetně možnosti odstranit další uživatele jako vlastníci.

**Poznámka:**: dokud nový vlastník potvrdí vlastnictví, jejich *nikoli* uveden jako vlastníka položky.
Při zobrazení **Spravovat vlastníky** stránky, zobrazí se položka "čekající na schválení" v aktuální vlastníky.
Tuto pozvánku lze odebrat; stejně jako ostatní vlastníků lze odebrat.
Tento proces pozvánek zabrání uživatelům v nesprávně jako vlastníci jejich položek přidávání jiných uživatelů.

Upozorňujeme, že metadata "Autoři" je čistě volného tvaru textu. jsou ovládaná pouze "vlastníci".


## <a name="removing-owners"></a>Odebrání vlastníky
Pokud má více vlastníky, položku a jedna je potřeba odstranit, proces je jednoduchý:

1. [Přihlaste se](https://powershellgallery.com/users/account/LogOn) do Galerie prostředí PowerShell pomocí účtu, který je vlastníkem aktuální položky;
2. Přejděte na stránku položek pomocí karty položek, hledání nebo kliknutím na své uživatelské jméno a potom [ **spravovat Moje položky**](https://www.powershellgallery.com/account/Packages).
3. Při přihlášení se jako vlastník položky, je Spravovat vlastníky odkaz na levé straně klikněte na;
4. Klikněte na odkaz "Odebrat" vedle vlastník odeberou.



## <a name="transferring-item-ownership"></a>Převedení vlastnictví položky
V některých případech nám získat žádosti o podporu pro přenos položky vlastnictví z jednoho uživatele do jiného, ale můžete provést téměř vždy sobě.
Převedení vlastnictví z jednoho uživatele je jednoduše kombinací tyto dvě funkce výše.

1. Aktuální vlastník žádostí nového uživatele se spoluvlastník a nový uživatel přijme podmínky pozvání;
2. Nový uživatel odebere staré uživatele ze seznamu vlastníků.

Tento požadavek zase pod několik forms ale proces funguje stejně.

* Vlastnictví položky se mění z jedné vývojáře do jiného
* Položka byla omylem publikována pomocí nesprávného účtu


## <a name="orphaned-items"></a>Osamocené položky
Došlo k jedné posledním scénáři, ale není tolikrát, kolikrát.
Položky se staly osamocené položky a jenom vlastník účtu položky nelze použít k přidání nové vlastníky.
Zde je několik příkladů tohoto scénáře:

* Účet vlastníka souvisí s e-mailovou adresu, která už existuje a uživatel zapomene své heslo
* Registrovaný vlastník opustil společnost, která vytváří položky a nelze získat přístup k aktualizaci položky vlastnictví
* Z důvodu chyb, který má vliv pouze několik položek položka je nějakým způsobem ownerless na Galerie

Správci Galerie prostředí PowerShell můžete přístup k Spravovat vlastníky odkazu pro libovolnou položku.
Pokud jste jeho oprávněný vlastník položku a nemůže kontaktovat aktuální vlastník pro získání vlastnictví oprávnění, pak použijte odkaz 'Oznámení zneužití' v galerii k dosažení správci Galerie prostředí PowerShell.
Nemůžeme se potom postupujte podle procesu ověřit vlastnictví položky.
Pokud jsme určit, že by měla být vlastníkem položky, jsme použije Spravovat vlastníky odkaz pro položku označována a poslat pozvání k vlastníka.
Pouze Uděláme to po ověření, že by měl být vlastníka a pro tento proces se liší podle okolností.
Častým použijeme adresy URL projektu položky najít způsob, jak obraťte se na vlastníka projektu, ale můžeme také používat Twitter, e-mailu nebo jiným způsobem pro kontaktování vlastníka projektu.