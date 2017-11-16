---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Jak používat dokončování pomocí tabulátorů v podokně skriptu a podokna konzoly"
ms.assetid: 3b752c3c-0bd0-4eca-a2d3-2d5a37fd9d84
ms.openlocfilehash: ba8d0af7e7fc0f1df9f65116be899097b0a97a3c
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a>Jak používat dokončování pomocí tabulátorů v podokně skriptu a podokna konzoly
Dokončování pomocí tabulátorů poskytuje automatickou pomoc při psaní v podokně skriptu nebo v podokně příkaz. Pokud chcete využít výhod tuto funkci použijte následující postup:

## <a name="to-automatically-complete-a-command-entry"></a>K dokončení automaticky zadání příkazu
V okně příkazu nebo skriptu zadejte pár znaků příkaz a stiskněte klávesu TAB vyberte požadovanou dokončení text. Více položek začínat text, který jste původně zadali, pokračujte stisknutím klávesy Tab, dokud se nezobrazí položku, kterou chcete. Dokončování pomocí tabulátorů může pomoct s zadáte název rutiny, název parametru, název proměnné, název vlastnosti objektu nebo cestu k souboru.

> [!NOTE]
> V podokně skriptu stisknutím klávesy TAB automaticky dokončí příkaz jenom v případě, že jsou úpravy, .ps1, .psd1 nebo soubory .psm1. Dokončování pomocí tabulátorů funguje kdykoli, kdy text v podokně příkaz.

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a>Chcete-li automaticky dokončení zadání parametru rutiny
V podokně podokně příkaz nebo skript zadejte rutiny následované pomlčkou a potom stiskněte klávesu TAB.

Můžete například zadat `Get-Process -` a stiskněte klávesu TAB více než jednou pro každou z parametrů poskytnutých rutině zase zobrazení.

## <a name="see-also"></a>Viz také
- [Pomocí Windows PowerShell ISE](using-the-windows-powershell-ise.md)
- [Postup vytvoření karty prostředí PowerShell](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)

