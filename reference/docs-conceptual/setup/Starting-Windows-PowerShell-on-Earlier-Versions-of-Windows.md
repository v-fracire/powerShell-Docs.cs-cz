---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Spuštění Windows PowerShellu v předchozích verzích Windows"
ms.assetid: 57125436-3d1e-4e7f-b5c4-8f0ecb49d642
ms.openlocfilehash: 52e3acc1fd3009ecad3b7134008e38d4edfb5ca7
ms.sourcegitcommit: 18e3bfae83ffe282d3fd1a45f5386f3b7250f0c0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/08/2018
---
# <a name="starting-windows-powershell-on-earlier-versions-of-windows"></a><span data-ttu-id="883ca-103">Spuštění Windows PowerShellu v předchozích verzích Windows</span><span class="sxs-lookup"><span data-stu-id="883ca-103">Starting Windows PowerShell on Earlier Versions of Windows</span></span>
<span data-ttu-id="883ca-104">Tato část vysvětluje, jak spustit prostředí Windows PowerShell a Windows PowerShell Integrované skriptovací prostředí (ISE) v systému Windows® 7, Windows Server® 2008 R2 a Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="883ca-104">This section explains how to start Windows PowerShell and Windows PowerShell Integrated Scripting Environment (ISE) on Windows® 7, Windows Server® 2008 R2, and Windows Server® 2008.</span></span> <span data-ttu-id="883ca-105">Také vysvětluje, jak povolit volitelné funkce pro Windows PowerShell ISE v prostředí Windows PowerShell 2.0 na Windows Server® 2008 R2 a Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="883ca-105">It also explains how to enable the optional feature for Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server® 2008 R2 and Windows Server® 2008.</span></span>

<span data-ttu-id="883ca-106">Chcete-li nainstalovat prostředí Windows PowerShell 4.0 na podporovaných systémů, stáhněte a nainstalujte [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881).</span><span class="sxs-lookup"><span data-stu-id="883ca-106">To install Windows PowerShell 4.0 on supported systems, download and install [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881).</span></span> <span data-ttu-id="883ca-107">Další informace najdete v tématu [instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md).</span><span class="sxs-lookup"><span data-stu-id="883ca-107">For more information, see [Installing Windows PowerShell](Installing-Windows-PowerShell.md).</span></span>

<span data-ttu-id="883ca-108">Chcete-li nainstalovat prostředí Windows PowerShell 3.0 na podporovaných systémů, stáhněte a nainstalujte [Windows Management Framework 3.0](http://go.microsoft.com/fwlink/?LinkID=240290).</span><span class="sxs-lookup"><span data-stu-id="883ca-108">To install Windows PowerShell 3.0 on supported systems, download and install [Windows Management Framework 3.0](http://go.microsoft.com/fwlink/?LinkID=240290).</span></span> <span data-ttu-id="883ca-109">Další informace najdete v tématu [instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md).</span><span class="sxs-lookup"><span data-stu-id="883ca-109">For more information, see [Installing Windows PowerShell](Installing-Windows-PowerShell.md).</span></span>

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a><span data-ttu-id="883ca-110">Postup spuštění prostředí Windows PowerShell na starších verzích systému Windows</span><span class="sxs-lookup"><span data-stu-id="883ca-110">How to Start Windows PowerShell on Earlier Versions of Windows</span></span>
<span data-ttu-id="883ca-111">Ke spuštění nainstalovaná verze prostředí Windows PowerShell 3.0 nebo prostředí Windows PowerShell 4.0, kde je to možné, použijte některý z následujících metod.</span><span class="sxs-lookup"><span data-stu-id="883ca-111">Use any of the following methods to start the installed version of Windows PowerShell 3.0, or Windows PowerShell 4.0, where applicable.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="883ca-112">Z nabídky Start</span><span class="sxs-lookup"><span data-stu-id="883ca-112">From the Start Menu</span></span>

- <span data-ttu-id="883ca-113">Klikněte na tlačítko **spustit**, typ **prostředí PowerShell**a potom klikněte na **prostředí Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="883ca-113">Click **Start**, type **PowerShell**, and then click **Windows PowerShell**.</span></span>

- <span data-ttu-id="883ca-114">Z **spustit** nabídky, klikněte na tlačítko **spustit**, klikněte na tlačítko **všechny programy**, klikněte na tlačítko **Příslušenství**, klikněte na tlačítko **prostředí Windows PowerShell**  složku a pak klikněte na tlačítko **prostředí Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="883ca-114">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="883ca-115">Na příkazovém řádku</span><span class="sxs-lookup"><span data-stu-id="883ca-115">At the Command Prompt</span></span>

- <span data-ttu-id="883ca-116">V Cmd.exe, prostředí Windows PowerShell nebo ISE Windows PowerShell spusťte prostředí Windows PowerShell, zadejte:</span><span class="sxs-lookup"><span data-stu-id="883ca-116">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

    ```
    PowerShell
    ```

    <span data-ttu-id="883ca-117">Můžete taky parametry programu PowerShell.exe přizpůsobit relace.</span><span class="sxs-lookup"><span data-stu-id="883ca-117">You can also use the parameters of the PowerShell.exe program to customize the session.</span></span> <span data-ttu-id="883ca-118">Další informace najdete v tématu [Nápověda příkazového řádku PowerShell.exe](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span><span class="sxs-lookup"><span data-stu-id="883ca-118">For more information, see [PowerShell.exe Command-Line Help](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span></span>

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="883ca-119">Pomocí správy oprávnění ("Spustit jako správce")</span><span class="sxs-lookup"><span data-stu-id="883ca-119">With Administrative privileges ("Run as administrator")</span></span>

1. <span data-ttu-id="883ca-120">Klikněte na tlačítko **spustit**, typ **prostředí PowerShell**, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na **spustit jako správce**.</span><span class="sxs-lookup"><span data-stu-id="883ca-120">Click **Start**, type **PowerShell**, right-click **Windows PowerShell**, and then click **Run as administrator**.</span></span>

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="883ca-121">Postup spuštění Windows PowerShell ISE na starších verzích systému Windows</span><span class="sxs-lookup"><span data-stu-id="883ca-121">How to Start Windows PowerShell ISE on Earlier Releases of Windows</span></span>
<span data-ttu-id="883ca-122">Ke spuštění Windows PowerShell ISE, použijte některý z následujících metod.</span><span class="sxs-lookup"><span data-stu-id="883ca-122">Use any of the following methods to start Windows PowerShell ISE.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="883ca-123">Z nabídky Start</span><span class="sxs-lookup"><span data-stu-id="883ca-123">From the Start Menu</span></span>

- <span data-ttu-id="883ca-124">Klikněte na tlačítko **spustit**, typ **ISE**a potom klikněte na **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="883ca-124">Click **Start**, type **ISE**, and then click **Windows PowerShell ISE**.</span></span>

- <span data-ttu-id="883ca-125">Z **spustit** nabídky, klikněte na tlačítko **spustit**, klikněte na tlačítko **všechny programy**, klikněte na tlačítko **Příslušenství**, klikněte na tlačítko **prostředí Windows PowerShell**  složku a pak klikněte na tlačítko **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="883ca-125">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell ISE**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="883ca-126">Na příkazovém řádku</span><span class="sxs-lookup"><span data-stu-id="883ca-126">At the Command Prompt</span></span>

- <span data-ttu-id="883ca-127">V Cmd.exe, prostředí Windows PowerShell nebo ISE Windows PowerShell spusťte prostředí Windows PowerShell, zadejte:</span><span class="sxs-lookup"><span data-stu-id="883ca-127">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

    ```
    PowerShell_ISE
    ```

    <span data-ttu-id="883ca-128">nebo</span><span class="sxs-lookup"><span data-stu-id="883ca-128">or</span></span>

    ```
    ISE
    ```

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="883ca-129">Pomocí správy oprávnění ("Spustit jako správce")</span><span class="sxs-lookup"><span data-stu-id="883ca-129">With Administrative privileges ("Run as administrator")</span></span>

1. <span data-ttu-id="883ca-130">Klikněte na tlačítko **spustit**, typ **ISE**, klikněte pravým tlačítkem na **Windows PowerShell ISE**a potom klikněte na **spustit jako správce**.</span><span class="sxs-lookup"><span data-stu-id="883ca-130">Click **Start**, type **ISE**, right-click **Windows PowerShell ISE**, and then click **Run as administrator**.</span></span>

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="883ca-131">Postup povolení ISE Windows PowerShell na starších verzích systému Windows</span><span class="sxs-lookup"><span data-stu-id="883ca-131">How to Enable Windows PowerShell ISE on Earlier Releases of Windows</span></span>
<span data-ttu-id="883ca-132">V prostředí Windows PowerShell 4.0 a prostředí Windows PowerShell 3.0 je povoleno Windows PowerShell ISE ve výchozím nastavení ve všech verzích systému Windows.</span><span class="sxs-lookup"><span data-stu-id="883ca-132">In Windows PowerShell 4.0 and Windows PowerShell 3.0, Windows PowerShell ISE is enabled by default on all versions of Windows.</span></span> <span data-ttu-id="883ca-133">Pokud již není povolena, Windows Management Framework 4.0 nebo Windows Management Framework 3.0 povolí ho.</span><span class="sxs-lookup"><span data-stu-id="883ca-133">If it is not already enabled, Windows Management Framework 4.0 or Windows Management Framework 3.0 enables it.</span></span>

<span data-ttu-id="883ca-134">V prostředí Windows PowerShell 2.0 je povoleno Windows PowerShell ISE ve výchozím nastavení v systému Windows 7.</span><span class="sxs-lookup"><span data-stu-id="883ca-134">In Windows PowerShell 2.0, Windows PowerShell ISE is enabled by default on Windows 7.</span></span> <span data-ttu-id="883ca-135">Na Windows Server 2008 R2 a Windows Server 2008, je však volitelná funkce.</span><span class="sxs-lookup"><span data-stu-id="883ca-135">However, on Windows Server 2008 R2 and Windows Server 2008, it is an optional feature.</span></span>

<span data-ttu-id="883ca-136">Pokud chcete povolit ISE Windows PowerShell v prostředí Windows PowerShell 2.0 na Windows Server 2008 R2 nebo Windows Server 2008, použijte následující postup.</span><span class="sxs-lookup"><span data-stu-id="883ca-136">To enable Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server 2008 R2 or Windows Server 2008, use the following procedure.</span></span>

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a><span data-ttu-id="883ca-137">Chcete-li povolit Windows PowerShell Integrované skriptovací prostředí (ISE)</span><span class="sxs-lookup"><span data-stu-id="883ca-137">To enable Windows PowerShell Integrated Scripting Environment (ISE)</span></span>

1. <span data-ttu-id="883ca-138">Spusťte Správce serveru.</span><span class="sxs-lookup"><span data-stu-id="883ca-138">Start Server Manager.</span></span>

2. <span data-ttu-id="883ca-139">Klikněte na tlačítko **funkce** a pak klikněte na **přidat funkce**.</span><span class="sxs-lookup"><span data-stu-id="883ca-139">Click **Features** and then click **Add Features**.</span></span>

3. <span data-ttu-id="883ca-140">V části Vybrat funkce klikněte na tlačítko Windows PowerShell Integrované skriptovací prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="883ca-140">In Select Features, click Windows PowerShell Integrated Scripting Environment (ISE).</span></span>

