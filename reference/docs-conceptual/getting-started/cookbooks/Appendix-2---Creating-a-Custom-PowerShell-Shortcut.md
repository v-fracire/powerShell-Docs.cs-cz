---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Příloha 2 Vytvoření zástupce vlastní prostředí PowerShell"
ms.assetid: 5d4fd421-5d43-4ec7-86fd-acfe887b066e
ms.openlocfilehash: d5e554f6f062fc5bf1beddd2aca1acf0b93d2133
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="appendix-2---creating-a-custom-powershell-shortcut"></a>Příloha 2 – Vytvoření zástupce vlastní prostředí PowerShell
Následující postup popisuje, jak vytvořit zástupce prostředí Windows PowerShell, který má několik vhodné možnosti přizpůsobit.

1. Vytvořte zástupce, který odkazuje na Powershell.exe.

2. Klikněte pravým tlačítkem na zástupce a pak klikněte na **vlastnosti**.

3. Klikněte **možnosti** kartě.

4. V **upravit možnosti** vyberte **rychlých úprav** zaškrtávací políčko.

    Toto nastavení umožňuje vybrat text v okně konzoly prostředí Windows PowerShell tak, že přetáhnete levým tlačítkem myši a umožňuje vám text do schránky Kopírovat stisknutím klávesy ENTER nebo kliknutím pravým tlačítkem myši.

5. V **upravit možnosti** vyberte **vložit režimu** zaškrtávací políčko. Toto nastavení umožňuje klikněte pravým tlačítkem myši v okně konzoly se automaticky vložit text ze schránky.

6. V **historie příkazů** části zadejte nebo vyberte číslo mezi 1 a 999 v **velikost vyrovnávací paměti** pole. Toto nastaví počet psaných příkazů, které budou zachovány v konzole vyrovnávací paměti.

7. V **historie příkazů** vyberte **Zahodit původní duplikáty** políčko eliminovat opakované příkazy z konzoly vyrovnávací paměti.

8. Klikněte **rozložení** kartě.

9. V **vyrovnávací paměti** zadejte číslo mezi 1 a 9999 v **výška** pole. Výška představuje počet řádků výstupu, které jsou do vyrovnávací paměti. Toto je maximální počet řádků, které uchovávají pro zobrazení při posouvání v okně konzoly. Pokud tento počet je menší než výška ukazuje **velikost okna** části výšku velikosti okna se automaticky sníží na stejnou hodnotu.

10. V **velikost okna** zadejte číslo mezi 1 a 9999 pro šířku. To představuje počet znaků, které se zobrazují v okně konzoly. Výchozí je 80 a prostředí Windows PowerShell výstupní formátování je určená pro tuto šířku.

11. Pokud chcete umístit konzole na určitém místě na ploše, když je otevřen, zrušte **okno pozice systémem** zaškrtávací políčko **umístění okna** části a poté změňte hodnoty  **Vlevo** a **horní** oknech **umístění okna** části.

12. Klikněte na **OK**.

