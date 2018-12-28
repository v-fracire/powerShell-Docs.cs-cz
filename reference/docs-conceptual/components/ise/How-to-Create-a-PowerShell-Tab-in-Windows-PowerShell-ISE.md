---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vytvoření powershellové karty v prostředí Windows PowerShell ISE
ms.assetid: c10c18c7-9ece-4fd0-83dc-a19c53d4fd83
ms.openlocfilehash: 080fe89bf1443f51460589b445431913fa20b4b8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403662"
---
# <a name="how-to-create-a-powershell-tab-in-windows-powershell-ise"></a><span data-ttu-id="77eea-103">Vytvoření powershellové karty v prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="77eea-103">How to Create a PowerShell Tab in Windows PowerShell ISE</span></span>

<span data-ttu-id="77eea-104">Karty v Windows Powershellu integrovaném skriptovacím prostředí (ISE) umožňují najednou vytvořit a použít několik prostředí provádění v rámci stejné aplikace.</span><span class="sxs-lookup"><span data-stu-id="77eea-104">Tabs in the Windows PowerShell Integrated Scripting Environment (ISE) allow you to simultaneously create and use several execution environments within the same application.</span></span>
<span data-ttu-id="77eea-105">Každá karta Powershellu odpovídá samostatné spouštěcí prostředí nebo relace.</span><span class="sxs-lookup"><span data-stu-id="77eea-105">Each PowerShell tab corresponds to a separate execution environment or session.</span></span>

> [!NOTE]
> <span data-ttu-id="77eea-106">Proměnné, funkce a aliasy, které vytvoříte v jedné karty se nepřenesou do jiné.</span><span class="sxs-lookup"><span data-stu-id="77eea-106">Variables, functions, and aliases that you create in one tab do not carry over to another.</span></span> <span data-ttu-id="77eea-107">Jsou různé relace Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="77eea-107">They are different Windows PowerShell sessions.</span></span>

<span data-ttu-id="77eea-108">Otevřít nebo zavřít karty v prostředí Windows PowerShell použijte následující postup.</span><span class="sxs-lookup"><span data-stu-id="77eea-108">Use the following steps to open or close a tab in Windows PowerShell.</span></span>
<span data-ttu-id="77eea-109">Chcete-li přejmenovat kartu, nastavte [DisplayName](object-model/The-PowerShellTab-Object.md#displayname) vlastnost v objektu skriptu Windows PowerShell Tab.</span><span class="sxs-lookup"><span data-stu-id="77eea-109">To rename a tab, set the [DisplayName](object-model/The-PowerShellTab-Object.md#displayname) property on the Windows PowerShell Tab scripting object.</span></span>

## <a name="to-create-and-use-a-new-powershell-tab"></a><span data-ttu-id="77eea-110">Jak vytvořit a používat na nové kartě prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="77eea-110">To create and use a new PowerShell Tab</span></span>

<span data-ttu-id="77eea-111">Na **souboru** nabídky, klikněte na tlačítko **nový PowerShell Tab**. Vždy otevře se nová karta prostředí PowerShell jako aktivní okno.</span><span class="sxs-lookup"><span data-stu-id="77eea-111">On the **File** menu, click **New PowerShell Tab**. The new PowerShell tab always opens as the active window.</span></span>
<span data-ttu-id="77eea-112">Karty Powershellu jsou číslovány postupně v pořadí, že jsou otevřené.</span><span class="sxs-lookup"><span data-stu-id="77eea-112">PowerShell tabs are incrementally numbered in the order that they are opened.</span></span>
<span data-ttu-id="77eea-113">Každá karta souvisí s vlastní okna konzoly Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="77eea-113">Each tab is associated with its own Windows PowerShell console window.</span></span>
<span data-ttu-id="77eea-114">Můžete mít až 32 karty Powershellu s vlastní relace, otevřete v čase (to je omezené na 8 na Windows PowerShell ISE 2.0.)</span><span class="sxs-lookup"><span data-stu-id="77eea-114">You can have up to 32 PowerShell tabs with their own session open at a time (this is limited to 8 on Windows PowerShell ISE 2.0.)</span></span>

<span data-ttu-id="77eea-115">Všimněte si, že kliknete na **nový** nebo **otevřít** ikon na panelu nástrojů nevytvoří novou kartu samostatné relaci.</span><span class="sxs-lookup"><span data-stu-id="77eea-115">Note that clicking the **New** or **Open** icons on the toolbar does not create a new tab with a separate session.</span></span>
<span data-ttu-id="77eea-116">Místo toho těchto tlačítek otevření souboru nového nebo existujícího skriptu na kartě aktuálně aktivní relaci.</span><span class="sxs-lookup"><span data-stu-id="77eea-116">Instead, those buttons open a new or existing script file on the currently active tab with a session.</span></span>
<span data-ttu-id="77eea-117">Můžete mít více skriptu, který otevření souborů s každou kartu a relace.</span><span class="sxs-lookup"><span data-stu-id="77eea-117">You can have multiple script files open with each tab and session.</span></span>
<span data-ttu-id="77eea-118">Karty skript pro relaci se zobrazí pouze pod karty relace při aktivním přidružená relace.</span><span class="sxs-lookup"><span data-stu-id="77eea-118">The script tabs for a session only appear below the session tabs when the associated session is active.</span></span>

<span data-ttu-id="77eea-119">Abyste aktivovali Powershellové karty, klikněte na kartu. Můžete vybírat z všechny karty Powershellu, které jsou otevřeny v **zobrazení** nabídky, klikněte na kartu prostředí PowerShell, kterou chcete použít.</span><span class="sxs-lookup"><span data-stu-id="77eea-119">To make a PowerShell tab active, click the tab. To select from all PowerShell tabs that are open, on the **View** menu, click the PowerShell tab you want to use.</span></span>

## <a name="to-create-and-use-a-new-remote-powershell-tab"></a><span data-ttu-id="77eea-120">Jak vytvořit a používat na nové kartě vzdáleného prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="77eea-120">To create and use a new Remote PowerShell tab</span></span>

<span data-ttu-id="77eea-121">Na **souboru** nabídky, klikněte na tlačítko **nové karty vzdálený PowerShell** k vytvoření relace na vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="77eea-121">On the **File** menu, click **New Remote PowerShell Tab** to establish a session on a remote computer.</span></span>
<span data-ttu-id="77eea-122">Dialogové okno se zobrazí a zobrazí výzvu k zadání podrobností, které jsou potřebné k navázání vzdáleného připojení.</span><span class="sxs-lookup"><span data-stu-id="77eea-122">A dialog box appears and prompts you to enter details required to establish the remote connection.</span></span>
<span data-ttu-id="77eea-123">Kartě Vzdálená funguje stejně jako místní Powershellové karty, ale příkazy a skripty se spouštějí na vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="77eea-123">The remote tab functions just like a local PowerShell tab, but the commands and scripts are run on the remote computer.</span></span>

## <a name="to-close-a-powershell-tab"></a><span data-ttu-id="77eea-124">Zavřete kartu prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="77eea-124">To close a PowerShell Tab</span></span>

<span data-ttu-id="77eea-125">Zavřete kartu, můžete použít některý z následujících postupů:</span><span class="sxs-lookup"><span data-stu-id="77eea-125">To close a tab, you can use any of the following techniques:</span></span>

- <span data-ttu-id="77eea-126">Klikněte na kartu, kterou chcete zavřít.</span><span class="sxs-lookup"><span data-stu-id="77eea-126">Click the tab that you want to close.</span></span>

- <span data-ttu-id="77eea-127">Na **souboru** nabídky, klikněte na tlačítko **zavřete PowerShell Tab**, nebo kliknutím na tlačítko Zavřít (**X**) na aktivní kartě kartu zavřete.</span><span class="sxs-lookup"><span data-stu-id="77eea-127">On the **File** menu, click **Close PowerShell Tab**, or click  the Close button  (**X**) on an active tab to close the tab.</span></span>

<span data-ttu-id="77eea-128">Pokud máte neuložené soubory otevřít v PowerShell tab, že chcete zavřít, zobrazí se výzva k ukládání nebo zahazování je.</span><span class="sxs-lookup"><span data-stu-id="77eea-128">If you have unsaved files open in the PowerShell tab that you are closing, you are prompted to save or discard them.</span></span>
<span data-ttu-id="77eea-129">Další informace o tom, jak uložit skript najdete v tématu [jak uložit skript](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).</span><span class="sxs-lookup"><span data-stu-id="77eea-129">For more information about how to save a script, see [How to Save a Script](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).</span></span>

## <a name="see-also"></a><span data-ttu-id="77eea-130">Viz také</span><span class="sxs-lookup"><span data-stu-id="77eea-130">See Also</span></span>

- [<span data-ttu-id="77eea-131">Představení Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="77eea-131">Introducing the Windows PowerShell ISE</span></span>](Introducing-the-Windows-PowerShell-ISE.md)
- [<span data-ttu-id="77eea-132">Použití Pokokna konzoly v prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="77eea-132">How to Use the Console Pane in the Windows PowerShell ISE</span></span>](How-to-Use-the-Console-Pane-in-the-Windows-PowerShell-ISE.md)