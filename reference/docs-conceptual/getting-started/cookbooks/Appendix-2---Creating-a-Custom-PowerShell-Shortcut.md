---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: 'Příloha 2: Vytvoření vlastního zástupce PowerShellu'
ms.assetid: 5d4fd421-5d43-4ec7-86fd-acfe887b066e
ms.openlocfilehash: e8081b7a64d313c8ef4bbccf95f250445dd68ad9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="appendix-2---creating-a-custom-powershell-shortcut"></a><span data-ttu-id="b26fc-103">Příloha 2 – Vytvoření zástupce vlastní prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="b26fc-103">Appendix 2 - Creating a Custom PowerShell Shortcut</span></span>

<span data-ttu-id="b26fc-104">Následující postup popisuje, jak vytvořit zástupce prostředí Windows PowerShell, který má několik vhodné možnosti přizpůsobit.</span><span class="sxs-lookup"><span data-stu-id="b26fc-104">The following procedure describes how to create a shortcut to Windows PowerShell that has several convenient options customized.</span></span>

1. <span data-ttu-id="b26fc-105">Vytvořte zástupce, který odkazuje na Powershell.exe.</span><span class="sxs-lookup"><span data-stu-id="b26fc-105">Create a shortcut that points to Powershell.exe.</span></span>

2. <span data-ttu-id="b26fc-106">Klikněte pravým tlačítkem na zástupce a pak klikněte na **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="b26fc-106">Right-click the shortcut, and then click **Properties**.</span></span>

3. <span data-ttu-id="b26fc-107">Klikněte **možnosti** kartě.</span><span class="sxs-lookup"><span data-stu-id="b26fc-107">Click the **Options** tab.</span></span>

4. <span data-ttu-id="b26fc-108">V **upravit možnosti** vyberte **rychlých úprav** zaškrtávací políčko.</span><span class="sxs-lookup"><span data-stu-id="b26fc-108">In the **Edit Options** section, select the **QuickEdit** check box.</span></span>

    <span data-ttu-id="b26fc-109">Toto nastavení umožňuje vybrat text v okně konzoly prostředí Windows PowerShell tak, že přetáhnete levým tlačítkem myši a umožňuje vám text do schránky Kopírovat stisknutím klávesy ENTER nebo kliknutím pravým tlačítkem myši.</span><span class="sxs-lookup"><span data-stu-id="b26fc-109">This setting lets you select text in the Windows PowerShell console window by dragging the left mouse button, and it lets you copy text to the clipboard by pressing ENTER or by right-clicking the mouse.</span></span>

5. <span data-ttu-id="b26fc-110">V **upravit možnosti** vyberte **vložit režimu** zaškrtávací políčko.</span><span class="sxs-lookup"><span data-stu-id="b26fc-110">In the **Edit Options** section, select the **Insert Mode** check box.</span></span> <span data-ttu-id="b26fc-111">Toto nastavení umožňuje klikněte pravým tlačítkem myši v okně konzoly se automaticky vložit text ze schránky.</span><span class="sxs-lookup"><span data-stu-id="b26fc-111">This setting lets you right-click in the console window to automatically paste text from the clipboard.</span></span>

6. <span data-ttu-id="b26fc-112">V **historie příkazů** části zadejte nebo vyberte číslo mezi 1 a 999 v **velikost vyrovnávací paměti** pole.</span><span class="sxs-lookup"><span data-stu-id="b26fc-112">In the **Command History** section, type or select a number between 1 and 999 in the **Buffer Size** box.</span></span> <span data-ttu-id="b26fc-113">Toto nastaví počet psaných příkazů, které budou zachovány v konzole vyrovnávací paměti.</span><span class="sxs-lookup"><span data-stu-id="b26fc-113">This sets the number of typed commands that will be kept in the console buffer.</span></span>

7. <span data-ttu-id="b26fc-114">V **historie příkazů** vyberte **Zahodit původní duplikáty** políčko eliminovat opakované příkazy z konzoly vyrovnávací paměti.</span><span class="sxs-lookup"><span data-stu-id="b26fc-114">In the **Command History** section, select the **Discard Old Duplicates** check box to eliminate repeated commands from the console buffer.</span></span>

8. <span data-ttu-id="b26fc-115">Klikněte **rozložení** kartě.</span><span class="sxs-lookup"><span data-stu-id="b26fc-115">Click the **Layout** tab.</span></span>

9. <span data-ttu-id="b26fc-116">V **vyrovnávací paměti** zadejte číslo mezi 1 a 9999 v **výška** pole.</span><span class="sxs-lookup"><span data-stu-id="b26fc-116">In the **Screen Buffer** section, type a number between 1 and 9999 in the **Height** box.</span></span> <span data-ttu-id="b26fc-117">Výška představuje počet řádků výstupu, které jsou do vyrovnávací paměti.</span><span class="sxs-lookup"><span data-stu-id="b26fc-117">The height represents the number of lines of output that are buffered.</span></span> <span data-ttu-id="b26fc-118">Toto je maximální počet řádků, které uchovávají pro zobrazení při posouvání v okně konzoly.</span><span class="sxs-lookup"><span data-stu-id="b26fc-118">This is the maximum number of lines retained for viewing when you scroll through the console window.</span></span> <span data-ttu-id="b26fc-119">Pokud tento počet je menší než výška ukazuje **velikost okna** části výšku velikosti okna se automaticky sníží na stejnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="b26fc-119">If this number is lower than the height shown in the **Window size** section, the window size height will automatically be reduced to the same value.</span></span>

10. <span data-ttu-id="b26fc-120">V **velikost okna** zadejte číslo mezi 1 a 9999 pro šířku.</span><span class="sxs-lookup"><span data-stu-id="b26fc-120">In the **Window Size** section, type a number between 1 and 9999 for the width.</span></span> <span data-ttu-id="b26fc-121">To představuje počet znaků, které se zobrazují v okně konzoly.</span><span class="sxs-lookup"><span data-stu-id="b26fc-121">This represents the number of characters that are displayed across the console window.</span></span> <span data-ttu-id="b26fc-122">Výchozí je 80 a prostředí Windows PowerShell výstupní formátování je určená pro tuto šířku.</span><span class="sxs-lookup"><span data-stu-id="b26fc-122">The default width is 80, and Windows PowerShell's output formatting is designed for this width.</span></span>

11. <span data-ttu-id="b26fc-123">Pokud chcete umístit konzole na určitém místě na ploše, když je otevřen, zrušte **okno pozice systémem** zaškrtávací políčko **umístění okna** části a poté změňte hodnoty  **Vlevo** a **horní** oknech **umístění okna** části.</span><span class="sxs-lookup"><span data-stu-id="b26fc-123">If you want to place the console at a particular point on the desktop when it is opened, clear the **Let system position window** check box in the **Window position** section, and then change the values in the **Left** and **Top** boxes in the **Window position** section.</span></span>

12. <span data-ttu-id="b26fc-124">Klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="b26fc-124">Click **OK**.</span></span>