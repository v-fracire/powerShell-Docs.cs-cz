---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 4e0c1638bf10e57580a463c46595ac9bc142a5b4
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="just-enough-administration-jea"></a>Akorát správy (JEA)
Právě dostatečně správy je nová funkce v WMF 5.0, která umožňuje správu na základě rolí pomocí vzdálenou komunikaci prostředí PowerShell.  Ji rozšiřuje stávající infrastrukturu omezené koncový bod umožňuje jiným uživatelům než správcům ke spuštění konkrétních příkazů, skripty a spustitelné soubory jako správce.  To umožňuje snížit počet úplná oprávnění správce ve vašem prostředí a zlepšit zabezpečení.  JEA se dá použít pro všechny objekty, které spravujete pomocí prostředí PowerShell; Pokud budete moct spravovat něco pomocí prostředí PowerShell, můžete JEA provést tak více bezpečně.  Pro podrobné podívejte se na právě dostatečně správy, podívejte se [prostředí průvodce](http://aka.ms/JEA).

Na rozdíl od původního omezené koncových bodů JEA je efektivní a snadno konfiguruje.  Možnosti uživatele v sadě nástrojů JEA lze granularly řídit, a omezení, které sady parametrů a hodnoty můžete zadat konkrétní příkaz. Akce uživatele se spouštějí v kontextu jednorázové virtuální účet, který má práva k provedení akce správce.  Příkazy vyvolané uživatele lze protokolovat audity zabezpečení.

JEA funguje tak, že umožňuje vytvářet speciálně nakonfigurovat omezené koncové body.  Tyto koncové body mají několik důležité charakteristiky:

1. Uživatelů, kteří se připojují k nim "Spustit jako" privilegované virtuální účet, který existuje pouze po dobu trvání této vzdálené relace.  Ve výchozím nastavení, je tento virtuální účet členem předdefinované skupiny Administrators, stejně jako správce domény na řadičích domény (Poznámka: Tato oprávnění se dají konfigurovat). Pomocí připojení jako jeden uživatel a spuštění jako jiný, privilegovaných uživatelů, můžete povolit uživatelům bez oprávnění k provádění specifických úloh správy bez nutnosti poskytnutí oprávnění správce ve vašich systémech.
2. Koncový bod je uzamčené.  To znamená, prostředí PowerShell se spustí v režimu žádný jazyk.  Pouze určité příkazy, skripty a spustitelné soubory jsou viditelné pro uživatele.
3. Různých uživatelů, kteří se připojují k ruce jinou sadu funkcí, které jsou založené na členství ve skupině.  Můžete zadat různé role různé možnosti v stejný koncový bod.

