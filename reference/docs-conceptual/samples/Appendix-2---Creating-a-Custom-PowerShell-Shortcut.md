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
# <a name="appendix-2---creating-a-custom-powershell-shortcut"></a><span data-ttu-id="522af-103">Příloha 2 – Vytvoření vlastního zástupce Powershellu</span><span class="sxs-lookup"><span data-stu-id="522af-103">Appendix 2 - Creating a Custom PowerShell Shortcut</span></span>

<span data-ttu-id="522af-104">Následující postup popisuje, jak vytvořit zástupce pro prostředí Windows PowerShell, který má několik vhodné možnosti přizpůsobit.</span><span class="sxs-lookup"><span data-stu-id="522af-104">The following procedure describes how to create a shortcut to Windows PowerShell that has several convenient options customized.</span></span>

1. <span data-ttu-id="522af-105">Vytvořte zástupce, který odkazuje na Powershell.exe.</span><span class="sxs-lookup"><span data-stu-id="522af-105">Create a shortcut that points to Powershell.exe.</span></span>

2. <span data-ttu-id="522af-106">Klikněte pravým tlačítkem na zástupce a potom klikněte na tlačítko **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="522af-106">Right-click the shortcut, and then click **Properties**.</span></span>

3. <span data-ttu-id="522af-107">Klikněte na tlačítko **možnosti** kartu.</span><span class="sxs-lookup"><span data-stu-id="522af-107">Click the **Options** tab.</span></span>

4. <span data-ttu-id="522af-108">V **upravit možnosti** vyberte **rychlých úprav** zaškrtávací políčko.</span><span class="sxs-lookup"><span data-stu-id="522af-108">In the **Edit Options** section, select the **QuickEdit** check box.</span></span>

    <span data-ttu-id="522af-109">Toto nastavení umožňuje vybrat text v okně konzoly Windows Powershellu pomocí přetažení levým tlačítkem myši a umožňuje zkopírování textu do schránky. stisknutím klávesy ENTER nebo kliknutím pravým tlačítkem myši.</span><span class="sxs-lookup"><span data-stu-id="522af-109">This setting lets you select text in the Windows PowerShell console window by dragging the left mouse button, and it lets you copy text to the clipboard by pressing ENTER or by right-clicking the mouse.</span></span>

5. <span data-ttu-id="522af-110">V **upravit možnosti** vyberte **vložit režimu** zaškrtávací políčko.</span><span class="sxs-lookup"><span data-stu-id="522af-110">In the **Edit Options** section, select the **Insert Mode** check box.</span></span> <span data-ttu-id="522af-111">Toto nastavení umožňuje klikněte pravým tlačítkem v okně konzoly se automaticky vložit text ze schránky.</span><span class="sxs-lookup"><span data-stu-id="522af-111">This setting lets you right-click in the console window to automatically paste text from the clipboard.</span></span>

6. <span data-ttu-id="522af-112">V **historie příkazů** části, zadejte nebo vyberte číslo mezi 1 a 999 v **velikost vyrovnávací paměti** pole.</span><span class="sxs-lookup"><span data-stu-id="522af-112">In the **Command History** section, type or select a number between 1 and 999 in the **Buffer Size** box.</span></span> <span data-ttu-id="522af-113">Tím se nastaví počet psaných příkazů, které budou zachovány v vyrovnávací paměti konzoly.</span><span class="sxs-lookup"><span data-stu-id="522af-113">This sets the number of typed commands that will be kept in the console buffer.</span></span>

7. <span data-ttu-id="522af-114">V **historie příkazů** vyberte **zrušit starý duplikuje** zaškrtávací políčko k odstranění opakovaných příkazy z vyrovnávací paměti konzoly.</span><span class="sxs-lookup"><span data-stu-id="522af-114">In the **Command History** section, select the **Discard Old Duplicates** check box to eliminate repeated commands from the console buffer.</span></span>

8. <span data-ttu-id="522af-115">Klikněte na tlačítko **rozložení** kartu.</span><span class="sxs-lookup"><span data-stu-id="522af-115">Click the **Layout** tab.</span></span>

9. <span data-ttu-id="522af-116">V **vyrovnávací paměti obrazovky** části, zadejte číslo mezi 1 a 9999 v **výška** pole.</span><span class="sxs-lookup"><span data-stu-id="522af-116">In the **Screen Buffer** section, type a number between 1 and 9999 in the **Height** box.</span></span> <span data-ttu-id="522af-117">Výška představuje počet řádků výstupu, které jsou ukládány do vyrovnávací paměti.</span><span class="sxs-lookup"><span data-stu-id="522af-117">The height represents the number of lines of output that are buffered.</span></span> <span data-ttu-id="522af-118">Toto je maximální počet řádků, které uchovávají po dobu sledovat, i když při procházení v okně konzoly.</span><span class="sxs-lookup"><span data-stu-id="522af-118">This is the maximum number of lines retained for viewing when you scroll through the console window.</span></span> <span data-ttu-id="522af-119">Pokud toto číslo je menší než výška ukazuje **velikost okna** oddílu, výška velikosti okna se automaticky sníží na stejnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="522af-119">If this number is lower than the height shown in the **Window size** section, the window size height will automatically be reduced to the same value.</span></span>

10. <span data-ttu-id="522af-120">V **velikost okna** části, zadejte číslo mezi 1 a 9999 šířky.</span><span class="sxs-lookup"><span data-stu-id="522af-120">In the **Window Size** section, type a number between 1 and 9999 for the width.</span></span> <span data-ttu-id="522af-121">To představuje počet znaků, které jsou zobrazeny v okně konzoly.</span><span class="sxs-lookup"><span data-stu-id="522af-121">This represents the number of characters that are displayed across the console window.</span></span> <span data-ttu-id="522af-122">Výchozí šířka nastaven na 80 a formátování výstupu prostředí Windows PowerShell je určený pro tuto šířku.</span><span class="sxs-lookup"><span data-stu-id="522af-122">The default width is 80, and Windows PowerShell's output formatting is designed for this width.</span></span>

11. <span data-ttu-id="522af-123">Pokud chcete umístit konzoly v určitém místě v klientských počítačích při otevření, zrušte **okno pozice systémem** zaškrtávací políčko **pozice okna** části a potom změňte hodnoty  **Vlevo** a **horní** polích v **pozice okna** oddílu.</span><span class="sxs-lookup"><span data-stu-id="522af-123">If you want to place the console at a particular point on the desktop when it is opened, clear the **Let system position window** check box in the **Window position** section, and then change the values in the **Left** and **Top** boxes in the **Window position** section.</span></span>

12. <span data-ttu-id="522af-124">Klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="522af-124">Click **OK**.</span></span>