---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití pokokna konzoly v prostředí PowerShell ISE
ms.assetid: 44d67705-87c7-4a69-a53e-6471fdebb757
ms.openlocfilehash: 5bbbdd3b1f0324ff1a4f2298459f58640c4dc9a6
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403868"
---
# <a name="how-to-use-the-console-pane-in-the-windows-powershell-ise"></a>Použití pokokna konzoly v prostředí PowerShell ISE

V podokně konzoly v Windows Powershellu integrovaném skriptovacím prostředí (ISE) funguje úplně stejně jako samostatné okno konzoly Windows PowerShell ISE.

Ke spuštění příkazu v konzole, zadejte příkaz a stiskněte klávesu ENTER. Chcete-li zadat více příkazů, které chcete spustit v pořadí, zadejte SHIFT + ENTER mezi příkazy. Zobrazit [postupy použití Tab k dokončování příkazů ve skriptovacím podokně a podokně konzoly](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) pomoc při zadávání příkazů.

Příkaz, na panelu nástrojů, klikněte na tlačítko **zastavení operace**, nebo stiskněte kombinaci kláves CTRL + BREAK. Také vám pomůže CTRL + C zastavte příkazu, pokud kontext je jednoznačný. Například pokud byl vybrán nějaký text v podokně aktuální, CTRL + C mapuje na operaci kopírování.

Počínaje Windows PowerShell verze 3, v podokně výstup byl v kombinaci s podokně konzoly. To má výhodu chovají jako samostatné konzoly Windows Powershellu a eliminuje rozdíly v postupech, které byly potřebné, pokud byly samostatné. Můžeš:

- Vyberte a zkopírujte text z podokna konzoly do schránky a vkládání v jiném okně. Vyberte text, klepněte a podržte ukazatel myši v podokně výstup při přetahování myší na text, který chcete zaznamenat. Můžete také použít klávesy se šipkami kurzoru při držení **SHIFT** s výběrem textu. Potom stiskněte klávesu CTRL + C nebo klikněte na tlačítko **kopírování** ikonu na panelu nástrojů.

- Vložte vybraný text na aktuální pozici kurzoru. Klikněte na tlačítko **vložit** ikonu na panelu nástrojů.

- Odstraňte veškerý text v podokně konzoly. K vymazání v podokně konzoly, klikněte **vymazat podokně konzoly** ikonu na panelu nástrojů nebo spusťte příkaz **Clear-Host** nebo její alias **kompatibilní se specifikací**.

## <a name="see-also"></a>Viz také

- [Představení Windows PowerShell ISE](Introducing-the-Windows-PowerShell-ISE.md)