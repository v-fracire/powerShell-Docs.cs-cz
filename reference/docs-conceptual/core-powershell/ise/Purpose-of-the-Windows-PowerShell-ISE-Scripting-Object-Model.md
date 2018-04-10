---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE
ms.assetid: d176a131-ab0c-43ee-80c1-f824ab8e4a05
ms.openlocfilehash: fd5ac2c34b173d4eba7636bb5760b1ac9abb4277
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="purpose-of-the-windows-powershell-ise-scripting-object-model"></a>Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE

Objekty jsou přidružené k formuláře a funkce systému Windows PowerShell Integrované skriptovací prostředí (ISE). Odkaz na objekt modelu poskytuje podrobnosti o člen vlastnosti a metody, které zveřejňují tyto objekty. Příklady slouží k zobrazení, jak můžete použít skripty přímý přístup k tyto metody a vlastnosti. Skriptovací objektový model usnadňuje následující řadu úloh.

## <a name="customizing-the-appearance-of-windows-powershell-ise"></a>Přizpůsobení vzhledu Windows PowerShell ISE

Objektový model můžete upravit nastavení aplikace a možnosti. Například můžete je upravit takto:

- Můžete změnit barvu chyby, upozornění, podrobné výstupy a ladění výstupu.
- Můžete získat nebo nastavit barvy pozadí v podokně příkaz, podokno výstup a v podokně skriptu.
- Můžete nastavit barvu popředí podokno výstup.
- Název písma a velikost písma lze nastavit pro Windows PowerShell ISE.
- Můžete konfigurovat upozornění. Toto nastavení zahrnuje upozornění, které jsou vydány po otevření souboru v několik karet prostředí PowerShell nebo pokud se předtím, než byl uložen soubor, spustí se skript v souboru.
- Můžete přepínat mezi zobrazení, kdy jsou v podokně skriptu a v podokně výstup vedle sebe a zobrazení kde v podokně skriptu je nad podokno výstup. V podokně příkaz můžete ukotvit dolní nebo horní podokno výstup.

## <a name="enhancing-the-functionality-of-windows-powershell-ise"></a>Rozšíření funkce systému Windows PowerShell ISE

Objektový model můžete použít k rozšíření funkcí Windows PowerShell ISE. Například můžete:

- Přidání a změna instanci ISE Windows PowerShell, sám sebe. Chcete-li změnit v nabídkách, můžete například přidávat nové položky nabídky a nové položky nabídky mapy skriptů.
- Vytvořte skripty, které provést některé úlohy, které můžete provádět pomocí tlačítka a příkazy nabídky v systému Windows PowerShell ISE. Například můžete přidat, odebrat nebo vyberte na kartě prostředí PowerShell.
- Doplňkovým úlohy, které lze provést pomocí tlačítka a příkazy nabídky. Můžete například přejmenovat na kartě prostředí PowerShell.
- Upravit textové vyrovnávací paměti pro příkaz podokno, podokno výstup a v podokně skriptu, přidružené k souboru. Například můžete:
  - Získání nebo nastavení veškerého textu.
  - Získání nebo nastavení výběr textu.
  - Spuštění skriptu nebo spustit vybranou část skriptu.
  - Na řádku přejděte do zobrazení.
  - Vložte text na pozici pomocí kurzoru.
  - Vyberte blok textu.
  - Získejte poslední číslo řádku.
- Provedení operace se soubory. Například můžete:
  - Otevření souboru, uložit soubor nebo uložení souboru pomocí jiný název.
  - Určí, zda soubor byla změněna od posledního uložení.
  - Získání názvu souboru.
  - Vyberte soubor.

## <a name="automating-tasks"></a>Automatizaci úloh

Skriptovací objekt modelu můžete použít k vytvoření klávesové zkratky pro časté operace.

## <a name="see-also"></a>Viz taky

- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)