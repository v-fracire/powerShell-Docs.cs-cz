---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: 'Příloha 2: Vytvoření vlastního zástupce PowerShellu'
ms.assetid: 5d4fd421-5d43-4ec7-86fd-acfe887b066e
ms.openlocfilehash: e8081b7a64d313c8ef4bbccf95f250445dd68ad9
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404084"
---
# <a name="appendix-2---creating-a-custom-powershell-shortcut"></a>Příloha 2 – Vytvoření vlastního zástupce Powershellu

Následující postup popisuje, jak vytvořit zástupce pro prostředí Windows PowerShell, který má několik vhodné možnosti přizpůsobit.

1. Vytvořte zástupce, který odkazuje na Powershell.exe.

2. Klikněte pravým tlačítkem na zástupce a potom klikněte na tlačítko **vlastnosti**.

3. Klikněte na tlačítko **možnosti** kartu.

4. V **upravit možnosti** vyberte **rychlých úprav** zaškrtávací políčko.

    Toto nastavení umožňuje vybrat text v okně konzoly Windows Powershellu pomocí přetažení levým tlačítkem myši a umožňuje zkopírování textu do schránky. stisknutím klávesy ENTER nebo kliknutím pravým tlačítkem myši.

5. V **upravit možnosti** vyberte **vložit režimu** zaškrtávací políčko. Toto nastavení umožňuje klikněte pravým tlačítkem v okně konzoly se automaticky vložit text ze schránky.

6. V **historie příkazů** části, zadejte nebo vyberte číslo mezi 1 a 999 v **velikost vyrovnávací paměti** pole. Tím se nastaví počet psaných příkazů, které budou zachovány v vyrovnávací paměti konzoly.

7. V **historie příkazů** vyberte **zrušit starý duplikuje** zaškrtávací políčko k odstranění opakovaných příkazy z vyrovnávací paměti konzoly.

8. Klikněte na tlačítko **rozložení** kartu.

9. V **vyrovnávací paměti obrazovky** části, zadejte číslo mezi 1 a 9999 v **výška** pole. Výška představuje počet řádků výstupu, které jsou ukládány do vyrovnávací paměti. Toto je maximální počet řádků, které uchovávají po dobu sledovat, i když při procházení v okně konzoly. Pokud toto číslo je menší než výška ukazuje **velikost okna** oddílu, výška velikosti okna se automaticky sníží na stejnou hodnotu.

10. V **velikost okna** části, zadejte číslo mezi 1 a 9999 šířky. To představuje počet znaků, které jsou zobrazeny v okně konzoly. Výchozí šířka nastaven na 80 a formátování výstupu prostředí Windows PowerShell je určený pro tuto šířku.

11. Pokud chcete umístit konzoly v určitém místě v klientských počítačích při otevření, zrušte **okno pozice systémem** zaškrtávací políčko **pozice okna** části a potom změňte hodnoty  **Vlevo** a **horní** polích v **pozice okna** oddílu.

12. Klikněte na **OK**.