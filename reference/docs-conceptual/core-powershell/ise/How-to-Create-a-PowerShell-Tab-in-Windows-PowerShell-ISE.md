---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vytvoření powershellové karty v prostředí Windows PowerShell ISE
ms.assetid: c10c18c7-9ece-4fd0-83dc-a19c53d4fd83
ms.openlocfilehash: 4d4388d889f2178b2cd24cb0f3350aee37327625
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="how-to-create-a-powershell-tab-in-windows-powershell-ise"></a><span data-ttu-id="0f8d1-103">Vytvoření powershellové karty v prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="0f8d1-103">How to Create a PowerShell Tab in Windows PowerShell ISE</span></span>

<span data-ttu-id="0f8d1-104">Karty v Windows PowerShell Integrované skriptovací prostředí (ISE) umožňují najednou vytvořit a použít více prostředích spuštění v rámci stejné aplikaci.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-104">Tabs in the Windows PowerShell Integrated Scripting Environment (ISE) allow you to simultaneously create and use several execution environments within the same application.</span></span>
<span data-ttu-id="0f8d1-105">Každé kartě prostředí PowerShell odpovídá prostředí pro spuštění samostatné nebo relace.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-105">Each PowerShell tab corresponds to a separate execution environment or session.</span></span>

> <span data-ttu-id="0f8d1-106">**POZNÁMKA:**:</span><span class="sxs-lookup"><span data-stu-id="0f8d1-106">**NOTE**:</span></span>
>
> <span data-ttu-id="0f8d1-107">Proměnné, funkce a aliasy, které vytvoříte v jedné karty se nepřenesou do jiné.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-107">Variables, functions, and aliases that you create in one tab do not carry over to another.</span></span> <span data-ttu-id="0f8d1-108">Jsou různé relace prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-108">They are different Windows PowerShell sessions.</span></span>

<span data-ttu-id="0f8d1-109">Pomocí následujících kroků spustit nebo zavřít karty v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-109">Use the following steps to open or close a tab in Windows PowerShell.</span></span>
<span data-ttu-id="0f8d1-110">Chcete-li přejmenovat na kartě, nastavte [DisplayName](The-PowerShellTab-Object.md#displayname) vlastnost u objektu skriptování, karta Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-110">To rename a tab, set the [DisplayName](The-PowerShellTab-Object.md#displayname) property on the Windows PowerShell Tab scripting object.</span></span>

## <a name="to-create-and-use-a-new-powershell-tab"></a><span data-ttu-id="0f8d1-111">Vytváření a používání novou kartu prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f8d1-111">To create and use a new PowerShell Tab</span></span>

<span data-ttu-id="0f8d1-112">Na **souboru** nabídky, klikněte na **novou kartu prostředí PowerShell**. Na nové kartě prostředí PowerShell se vždy otevře jako aktivní okno.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-112">On the **File** menu, click **New PowerShell Tab**. The new PowerShell tab always opens as the active window.</span></span>
<span data-ttu-id="0f8d1-113">Prostředí PowerShell karty jsou číslované postupně v pořadí, že jsou otevřené.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-113">PowerShell tabs are incrementally numbered in the order that they are opened.</span></span>
<span data-ttu-id="0f8d1-114">Každé kartě souvisí s její vlastní konzole okno prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-114">Each tab is associated with its own Windows PowerShell console window.</span></span>
<span data-ttu-id="0f8d1-115">Může mít až 32 karet prostředí PowerShell s vlastní relaci otevřené v čase (to je omezené na 8 v prostředí Windows PowerShell ISE 2.0.)</span><span class="sxs-lookup"><span data-stu-id="0f8d1-115">You can have up to 32 PowerShell tabs with their own session open at a time (this is limited to 8 on Windows PowerShell ISE 2.0.)</span></span>

<span data-ttu-id="0f8d1-116">Všimněte si, že kliknete **nový** nebo **otevřete** ikon na panelu nástrojů nevytvoří novou kartu s samostatných relací.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-116">Note that clicking the **New** or **Open** icons on the toolbar does not create a new tab with a separate session.</span></span>
<span data-ttu-id="0f8d1-117">Místo toho těchto tlačítek otevřete soubor skriptu nový nebo existující na kartě aktuálně aktivní s relací.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-117">Instead, those buttons open a new or existing script file on the currently active tab with a session.</span></span>
<span data-ttu-id="0f8d1-118">Můžete mít více skript, který otevřít soubory s každou kartu a relace.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-118">You can have multiple script files open with each tab and session.</span></span>
<span data-ttu-id="0f8d1-119">Skript karty pro relaci se zobrazí pouze pod karty relace při aktivním přidružená relace.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-119">The script tabs for a session only appear below the session tabs when the associated session is active.</span></span>

<span data-ttu-id="0f8d1-120">Aktivujte na kartě prostředí PowerShell, klikněte na kartu. A vyberte všechny karty prostředí PowerShell, které jsou otevřené a na **zobrazení** nabídky, klikněte na kartu prostředí PowerShell, kterou chcete použít.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-120">To make a PowerShell tab active, click the tab. To select from all PowerShell tabs that are open, on the **View** menu, click the PowerShell tab you want to use.</span></span>

## <a name="to-create-and-use-a-new-remote-powershell-tab"></a><span data-ttu-id="0f8d1-121">Vytváření a používání novou kartu vzdáleného prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f8d1-121">To create and use a new Remote PowerShell tab</span></span>

<span data-ttu-id="0f8d1-122">Na **soubor** nabídky, klikněte na tlačítko **novou kartu vzdáleného prostředí PowerShell** k vytvoření relace na vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-122">On the **File** menu, click **New Remote PowerShell Tab** to establish a session on a remote computer.</span></span>
<span data-ttu-id="0f8d1-123">Dialogové okno se zobrazí a výzvu k zadání podrobností nutný k vytvoření vzdáleného připojení.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-123">A dialog box appears and prompts you to enter details required to establish the remote connection.</span></span>
<span data-ttu-id="0f8d1-124">Karty vzdálený funguje stejně jako místní kartě prostředí PowerShell, ale příkazy a skripty se spouštějí ve vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-124">The remote tab functions just like a local PowerShell tab, but the commands and scripts are run on the remote computer.</span></span>

## <a name="to-close-a-powershell-tab"></a><span data-ttu-id="0f8d1-125">Zavřete kartu prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f8d1-125">To close a PowerShell Tab</span></span>

<span data-ttu-id="0f8d1-126">Na kartě zavřete, můžete použít některý z následujících postupů:</span><span class="sxs-lookup"><span data-stu-id="0f8d1-126">To close a tab, you can use any of the following techniques:</span></span>

- <span data-ttu-id="0f8d1-127">Klikněte na kartu, která chcete zavřít.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-127">Click the tab that you want to close.</span></span>

- <span data-ttu-id="0f8d1-128">Na **soubor** nabídky, klikněte na tlačítko **zavřete kartu prostředí PowerShell**, nebo klikněte na tlačítko Zavřít (**X**) active karty zavřete kartu.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-128">On the **File** menu, click **Close PowerShell Tab**, or click  the Close button  (**X**) on an active tab to close the tab.</span></span>

<span data-ttu-id="0f8d1-129">Pokud máte neuložené otevřete soubory na kartě prostředí PowerShell, že chcete zavřít, zobrazí se výzva k uložte nebo zahoďte je.</span><span class="sxs-lookup"><span data-stu-id="0f8d1-129">If you have unsaved files open in the PowerShell tab that you are closing, you are prompted to save or discard them.</span></span>
<span data-ttu-id="0f8d1-130">Další informace o tom, jak uložit skript najdete v tématu [postup uložit skript](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).</span><span class="sxs-lookup"><span data-stu-id="0f8d1-130">For more information about how to save a script, see [How to Save a Script](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).</span></span>

## <a name="see-also"></a><span data-ttu-id="0f8d1-131">Viz také</span><span class="sxs-lookup"><span data-stu-id="0f8d1-131">See Also</span></span>

- [<span data-ttu-id="0f8d1-132">Představení Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="0f8d1-132">Introducing the Windows PowerShell ISE</span></span>](Introducing-the-Windows-PowerShell-ISE.md)
- [<span data-ttu-id="0f8d1-133">Jak používat podokně konzoly v systému Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="0f8d1-133">How to Use the Console Pane in the Windows PowerShell ISE</span></span>](How-to-Use-the-Console-Pane-in-the-Windows-PowerShell-ISE.md)