---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Jak používat podokně konzoly v systému Windows PowerShell ISE"
ms.assetid: 44d67705-87c7-4a69-a53e-6471fdebb757
ms.openlocfilehash: 59e97bbc12269d855c4f3715171636647d4cc634
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="how-to-use-the-console-pane-in-the-windows-powershell-ise"></a>Jak používat podokně konzoly v systému Windows PowerShell ISE
V podokně konzoly v Windows PowerShell Integrované skriptovací prostředí (ISE) pracuje úplně stejně jako samostatné okna konzoly Windows PowerShell ISE.

Pokud chcete spustit příkaz v podokně konzoly, zadejte příkaz a stiskněte klávesu ENTER. Chcete-li zadat více příkazů, které chcete spustit v pořadí, zadejte SHIFT + ENTER mezi příkazy. V tématu [postup dokončování pomocí tabulátorů použijte v skriptu podokně a podokně konzoly](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) pomoc při zadávání příkazů.

Chcete-li zastavit příkazu na panelu nástrojů, klikněte na tlačítko **zastavit operaci**, nebo stiskněte klávesu CTRL + BREAK. CTRL + C můžete také zastavit příkaz, pokud kontext je jednoznačné. Například pokud nějaký text byla vybrána v podokně aktuální, pak CTRL + C mapuje kopírování.

Od verze prostředí Windows PowerShell v3, se podokno výstup kombinovat s podokně konzoly. To má výhodu chovají jako samostatné konzoly Windows Powershellu a eliminuje rozdíly v postupech, které byly potřebné, pokud byly samostatné. Můžeš:

- Vyberte a zkopírujte text z podokna konzoly do schránky pro vložení v jiné okno. Vyberte text, klikněte na tlačítko a podržte tlačítko myši v podokně výstup při přetahování myší nad text, který chcete zaznamenat. Můžete také použít klávesy se šipkami kurzoru při uložení **SHIFT** výběr textu. Pak stiskněte kombinaci kláves CTRL + C nebo klikněte na tlačítko **kopie** ikonu na panelu nástrojů.

- Vložte vybraný text na aktuální pozici kurzoru. Klikněte **vložení** ikonu na panelu nástrojů.

- Vymažte všechny text v podokně konzoly. Zrušte podokně konzoly, můžete kliknout na **vymazat podokna konzoly** ikonu na panelu nástrojů nebo spusťte příkaz **Clear-Host** nebo jeho alias **specifikací cls**.

## <a name="see-also"></a>Viz také
- [Pomocí Windows PowerShell ISE](Using-the-Windows-PowerShell-ISE.md)

