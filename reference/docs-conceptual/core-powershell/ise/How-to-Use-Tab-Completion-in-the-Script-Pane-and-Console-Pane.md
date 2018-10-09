---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití klávesy Tab k dokončování příkazů ve skriptovacím podokně a v podokně konzoly
ms.assetid: 3b752c3c-0bd0-4eca-a2d3-2d5a37fd9d84
ms.openlocfilehash: 24a3f00987ff5ca4bf82d1a3206857ec3c4b3f09
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851131"
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a>Použití klávesy Tab k dokončování příkazů ve skriptovacím podokně a v podokně konzoly

Dokončování pomocí tabulátoru poskytuje automatické Nápověda při zadávání v podokně se skriptem nebo v příkazovém podokně. Abyste mohli využít tuto funkci, postupujte následovně:

## <a name="to-automatically-complete-a-command-entry"></a>Automatické dokončení položky příkazu

V okně příkazu nebo skriptu zadejte několik znaků příkaz a dvakrát stiskněte klávesu TAB k výběru požadované dokončování textu. Pokud více položek začíná zadaným textem, který jste původně zadali a pak pokračujte stisknutím klávesy Tab, dokud nenajdete položku, kterou chcete. TAB k dokončování příkazů může pomoct tak, že napíšete název rutiny, název parametru, název proměnné, název vlastnosti objektu nebo cestu k souboru.

> [!NOTE]
> V podokně se skriptem klávesy TAB automaticky dokončí příkaz pouze při úpravách .ps1, .psd1 nebo soubory .psm1. Dokončování pomocí tabulátoru funguje kdykoli, když píšete v příkazovém podokně.

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a>Automatické dokončení vstupní parametr rutiny

V podokně podokna příkazu nebo skriptu zadejte rutinu, za nímž následuje pomlčka a dvakrát stiskněte klávesu TAB.

Zadejte například `Get-Process -` a stiskněte klávesu TAB více než jednou pro každý z parametrů pro rutinu zase zobrazení.

## <a name="see-also"></a>Viz také

- [Představení Windows PowerShell ISE](Introducing-the-Windows-PowerShell-ISE.md)
- [Vytvoření karty Powershellu](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)
