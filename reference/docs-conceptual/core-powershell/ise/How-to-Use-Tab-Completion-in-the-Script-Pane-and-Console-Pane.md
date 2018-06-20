---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití klávesy Tab k dokončování příkazů ve skriptovacím podokně a v podokně konzoly
ms.assetid: 3b752c3c-0bd0-4eca-a2d3-2d5a37fd9d84
ms.openlocfilehash: e1f8146b6113a82fd3d857c98550ec2e459715a4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954921"
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a>Použití klávesy Tab k dokončování příkazů ve skriptovacím podokně a v podokně konzoly

Dokončování pomocí tabulátorů poskytuje automatickou pomoc při psaní v podokně skriptu nebo v podokně příkaz. Pokud chcete využít výhod tuto funkci použijte následující postup:

## <a name="to-automatically-complete-a-command-entry"></a>K dokončení automaticky zadání příkazu

V okně příkazu nebo skriptu zadejte pár znaků příkaz a stiskněte klávesu TAB vyberte požadovanou dokončení text. Více položek začínat text, který jste původně zadali, pokračujte stisknutím klávesy Tab, dokud se nezobrazí položku, kterou chcete. Dokončování pomocí tabulátorů může pomoct s zadáte název rutiny, název parametru, název proměnné, název vlastnosti objektu nebo cestu k souboru.

> [!NOTE]
> V podokně skriptu stisknutím klávesy TAB automaticky dokončí příkaz jenom v případě, že jsou úpravy, .ps1, .psd1 nebo soubory .psm1. Dokončování pomocí tabulátorů funguje kdykoli, kdy text v podokně příkaz.

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a>Chcete-li automaticky dokončení zadání parametru rutiny

V podokně podokně příkaz nebo skript zadejte rutiny následované pomlčkou a potom stiskněte klávesu TAB.

Můžete například zadat `Get-Process -` a stiskněte klávesu TAB více než jednou pro každou z parametrů poskytnutých rutině zase zobrazení.

## <a name="see-also"></a>Viz také

- [Představení Windows PowerShell ISE](Introducing-the-Windows-PowerShell-ISE.md)
- [Postup vytvoření karty prostředí PowerShell](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)