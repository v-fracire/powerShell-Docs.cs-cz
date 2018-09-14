---
ms.date: 09/10/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Správa klíčů rozhraní API
ms.openlocfilehash: 954eb27c25babdb8efe50c13caf5f2d287c6b3e3
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523309"
---
# <a name="managing-api-keys"></a>Správa klíčů rozhraní API

Galerie prostředí PowerShell podporuje vytváření více klíčů rozhraní API pro podporu rozsahu publikování požadavky. Klíč rozhraní API můžete použít na jeden nebo více balíčků, udělí zvláštní oprávnění a má datum vypršení platnosti.

> [!IMPORTANT]
> Uživatelé, kteří publikují do Galerie prostředí PowerShell před zavedením s vymezeným oborem klíče rozhraní API budou mít "API key úplný přístup". Vylepšení zabezpečení integrované s vymezeným oborem klíče rozhraní API není nutné úplné přístupové klíče. Úplné přístupové klávesy nikdy vyprší platnost a platí pro všechno, co vlastněné uživatelem. Pokud odstraníte tento klíč, nemůže být obnovena.

Následující obrázek ukazuje možnosti dostupné při vytváření oboru klíč rozhraní API.

![Vytvoření klíče rozhraní API](../../Images/PSGallery_KeyScoped.png)

V tomto příkladu jsme vytvořili klíč rozhraní API s názvem **AzureRMDataFactory**. Tato hodnota klíče je možné tak, aby nabízel balíčků s názvy, které začínají řetězcem "AzureRM.DataFactory" a je platný 365 dní. Toto je typický scénář, když pracují různé týmy v rámci stejné organizace na různých balíčcích. Členové týmu mají klíč, který udělí oprávnění pro konkrétní balíček, který pracují na.
Hodnota vypršení platnosti brání použití zastaralé či zapomenutí klíčů.

## <a name="using-glob-patterns"></a>Pomocí glob vzory

Pokud pracujete ve více balíčků, můžete použít vzorů podpory zástupných znaků tak, aby odpovídaly více balíčků jako skupinu. Oprávnění ke klíči rozhraní API platí pro všechny nové balíčky pro odpovídající vzoru glob. Například v předchozím příkladu používá **Glob vzor** hodnotu "AzureRM.DataFactory*". Můžete odeslat balíček s názvem pomocí tohoto klíče, protože balíček shoduje se vzorem glob AzureRm.DataFactoryV2.Netcore.

## <a name="create-api-keys-securely"></a>Vytvořte bezpečně klíče rozhraní API

Pro zabezpečení nově vytvořený hodnotu klíče se nikdy zobrazí na obrazovce a je dostupná jenom při tlačítka pro kopírování, jak je znázorněno níže.

![Získání nové hodnoty klíče rozhraní API](../../Images/PSGallery_CopyCreatedKey.png)

> [!IMPORTANT]
> Kopírovat můžete pouze hodnotu klíče rozhraní API ihned po vytvoření nebo aktualizaci. Se nezobrazí a nebudete mít přístup znovu po aktualizaci stránky. Pokud ztratíte hodnota klíče, musíte použít znovu vygenerovat klíč a zkopírujte klíč, až se znovu vygeneroval.

## <a name="key-permissions-and-expiration"></a>Oprávnění ke klíči a vypršení platnosti

S vymezeným oborem klíče rozhraní API můžete přiřadit některé z těchto oprávnění:

- Vložit nové balíčky
- Vložit nový nebo aktualizovat balíčky
- Vyjmutí ze seznamu balíčků

Každý nový klíč má vypršení platnosti. Ve dnech se měří hodnota vypršení platnosti. Možné hodnoty pro vypršení platnosti jsou:

- 1 den
- 90 dnů
- 180 dnů
- 270 dní
- 365 dnů (výchozí)

Tato nastavení nelze změnit po vytvoření klíče. Nelze vytvořit nový klíč, který nikdy nevyprší.

## <a name="editing-and-deleting-existing-api-keys"></a>Úpravy a odstranění existující klíče rozhraní API

Můžete změnit některá nastavení existujícího klíče. Jak již bylo uvedeno výše nelze změnit obor zabezpečení pro existující klíč rozhraní API nebo změnit vypršení platnosti. Změnit možnosti můžete vidět na následujícím snímku obrazovky:

![Získání nové hodnoty klíče rozhraní API](../../Images/PSGallery_EditAPIKey.png)

Chcete-li změnit balíčky řídí klíč, můžete zvolit jednotlivé balíčky ze seznamu nebo změnit glob vzor.

Kliknutím na **znovu vygenerovat** vytvoří novou hodnotu klíče. Stejně jako při původně vytvořil klíč, je třeba **kopírování** hodnotu klíče ihned po jeho aktualizace. **Kopírování** možnost není k dispozici po opuštění této stránky.

Kliknutím na **odstranit** zobrazí potvrzovací zpráva. Po odstranění klíče nepoužitelné.

## <a name="key-expiration"></a>Vypršení platnosti klíče

Deset dní před vypršením platnosti, galerie prostředí PowerShell odešle e-mail s upozorněním držitele účtu, klíč rozhraní API. Po vypršení platnosti klíčem nepoužitelné. Upozornění se zobrazí v horní části stránky správy klíčů rozhraní API, zobrazení, které klíče už nejsou platné. Můžete generovat nové hodnoty klíče.
