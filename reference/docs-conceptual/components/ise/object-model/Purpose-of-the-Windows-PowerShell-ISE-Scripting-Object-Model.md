---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE
ms.assetid: d176a131-ab0c-43ee-80c1-f824ab8e4a05
ms.openlocfilehash: fd5ac2c34b173d4eba7636bb5760b1ac9abb4277
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404091"
---
# <a name="purpose-of-the-windows-powershell-ise-scripting-object-model"></a>Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE

Objekty jsou spojeny s formuláře a funkce z Windows Powershellu integrovaném skriptovacím prostředí (ISE). Referenční dokumentace objektového modelu obsahuje podrobné informace o členu vlastnostem a metodám, které zveřejňují tyto objekty. Příklady jsou k dispozici k zobrazení, jak můžete použít skripty pro přímý přístup k těmto metodám a vlastnostem. Skriptovací objektový model usnadňuje následující řadu úloh.

## <a name="customizing-the-appearance-of-windows-powershell-ise"></a>Přizpůsobení vzhledu Windows PowerShell ISE

Objektový model můžete upravit nastavení aplikace a možnosti. Například můžete upravit následujícím způsobem:

- Můžete změnit barvu chyby, upozornění, verbose výstupy a výstup ladění.
- Můžete získat nebo nastavit barvy pozadí v příkazovém podokně, v podokně výstup a v podokně skriptu.
- Můžete nastavit barvu popředí pro podokno výstup.
- Název písma a velikost písma lze nastavit pro Windows PowerShell ISE.
- Můžete nakonfigurovat upozornění. Toto nastavení obsahuje upozornění, které jsou vydány, když je soubor otevřen v několika karty Powershellu nebo při spuštění skriptu v souboru dříve, než byl uložen soubor.
- Můžete přepínat mezi zobrazením kde skriptovacím podokně a v podokně výstupu jsou vedle sebe a zobrazení se v podokně skriptu nad podokno výstup. V příkazovém podokně můžete ukotvit dolní nebo horní podokno výstup.

## <a name="enhancing-the-functionality-of-windows-powershell-ise"></a>Vylepšení funkce Windows PowerShell ISE

Objektový model můžete použít k rozšíření funkcí Windows PowerShell ISE. Například můžete:

- Přidat a upravit instance Windows PowerShell ISE samotný. Chcete-li změnit nabídky, můžete například přidávat nové položky nabídky a mapování nových položek nabídky do skriptů.
- Vytváření skriptů, které provádějí některé úlohy, které můžete provádět pomocí příkazů nabídky a tlačítka v prostředí Windows PowerShell ISE. Například můžete přidat, odebrat nebo vyberte kartu prostředí PowerShell.
- Doplněk úkoly, které lze provést pomocí příkazů nabídky a tlačítka. Například můžete přejmenovat kartu prostředí PowerShell.
- Manipulace s vyrovnávací paměti textu v příkazovém podokně, v podokně výstup a v podokně skriptu, které jsou spojeny se souborem. Například můžete:
  - Získání nebo nastavení veškerý text.
  - Získání nebo nastavení výběru textu.
  - Spustit skript nebo vybrané části skriptu.
  - Posuňte řádek do zobrazení.
  - Vložení textu na pozici blikajícího kurzoru.
  - Vyberte blok textu.
  - Vrátí poslední číslo řádku.
- Provedení operace se soubory. Například můžete:
  - Otevřete soubor, uložit soubor nebo uložit soubor s použitím jiný název.
  - Určení, zda soubor po posledního uložení změněn.
  - Získání názvu souboru.
  - Vyberte soubor.

## <a name="automating-tasks"></a>Automatizace úloh

Skriptovací objektový model slouží k vytvoření klávesové zkratky pro časté operace.

## <a name="see-also"></a>Viz taky

- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)