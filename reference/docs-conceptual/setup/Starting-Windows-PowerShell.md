---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Spuštění Windows PowerShellu
ms.assetid: 59b649a2-c90c-4cf4-bf95-a740c59148e7
ms.openlocfilehash: b56ddc2f577225646729b99f3a2abcb8cc60d307
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="starting-windows-powershell"></a><span data-ttu-id="ab6a9-103">Spuštění Windows PowerShellu</span><span class="sxs-lookup"><span data-stu-id="ab6a9-103">Starting Windows PowerShell</span></span>
<span data-ttu-id="ab6a9-104">PowerShell je skriptovací modulu dll, která je integrována do více hostitelů.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-104">PowerShell is a scripting engine dll which is embedded into multiple hosts.</span></span>  <span data-ttu-id="ab6a9-105">Nejběžnější hostitele, který se spustí jsou interaktivního příkazového řádku PowerShell.exe a interaktivní PowerShell_ISE.exe prostředí skriptování.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-105">The most common host you will start are the interactive command line PowerShell.exe and the Interactive Scripting Environment PowerShell_ISE.exe.</span></span>

<span data-ttu-id="ab6a9-106">Pokud chcete spustit Windows PowerShell® v systému Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012 a Windows 8, přečtěte si téma [běžné úlohy správy a navigace](http://technet.microsoft.com/library/hh831491.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab6a9-106">To start Windows PowerShell® on Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012, and Windows 8, see [Common Management Tasks and Navigation](http://technet.microsoft.com/library/hh831491.aspx).</span></span>

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a><span data-ttu-id="ab6a9-107">Postup spuštění prostředí Windows PowerShell na starších verzích systému Windows</span><span class="sxs-lookup"><span data-stu-id="ab6a9-107">How to Start Windows PowerShell on Earlier Versions of Windows</span></span>

<span data-ttu-id="ab6a9-108">Tato část vysvětluje, jak spustit prostředí Windows PowerShell a Windows PowerShell Integrované skriptovací prostředí (ISE) v systému Windows® 7, Windows Server® 2008 R2 a Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-108">This section explains how to start Windows PowerShell and Windows PowerShell Integrated Scripting Environment (ISE) on Windows® 7, Windows Server® 2008 R2, and Windows Server® 2008.</span></span> <span data-ttu-id="ab6a9-109">Také vysvětluje, jak povolit volitelné funkce pro Windows PowerShell ISE v prostředí Windows PowerShell 2.0 na Windows Server® 2008 R2 a Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-109">It also explains how to enable the optional feature for Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server® 2008 R2 and Windows Server® 2008.</span></span>

<span data-ttu-id="ab6a9-110">Ke spuštění nainstalovaná verze prostředí Windows PowerShell 3.0 nebo prostředí Windows PowerShell 4.0, kde je to možné, použijte některý z následujících metod.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-110">Use any of the following methods to start the installed version of Windows PowerShell 3.0, or Windows PowerShell 4.0, where applicable.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="ab6a9-111">Z nabídky Start</span><span class="sxs-lookup"><span data-stu-id="ab6a9-111">From the Start Menu</span></span>

- <span data-ttu-id="ab6a9-112">Klikněte na tlačítko **spustit**, typ **prostředí PowerShell**a potom klikněte na **prostředí Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-112">Click **Start**, type **PowerShell**, and then click **Windows PowerShell**.</span></span>
- <span data-ttu-id="ab6a9-113">Z **spustit** nabídky, klikněte na tlačítko **spustit**, klikněte na tlačítko **všechny programy**, klikněte na tlačítko **Příslušenství**, klikněte na tlačítko **prostředí Windows PowerShell**  složku a pak klikněte na tlačítko **prostředí Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-113">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="ab6a9-114">Na příkazovém řádku</span><span class="sxs-lookup"><span data-stu-id="ab6a9-114">At the Command Prompt</span></span>

<span data-ttu-id="ab6a9-115">V Cmd.exe, prostředí Windows PowerShell nebo ISE Windows PowerShell spusťte prostředí Windows PowerShell, zadejte:</span><span class="sxs-lookup"><span data-stu-id="ab6a9-115">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

```
PowerShell
```

<span data-ttu-id="ab6a9-116">Můžete taky parametry programu PowerShell.exe přizpůsobit relace.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-116">You can also use the parameters of the PowerShell.exe program to customize the session.</span></span> <span data-ttu-id="ab6a9-117">Další informace najdete v tématu [Nápověda příkazového řádku PowerShell.exe](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span><span class="sxs-lookup"><span data-stu-id="ab6a9-117">For more information, see [PowerShell.exe Command-Line Help](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span></span>

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="ab6a9-118">Pomocí správy oprávnění ("Spustit jako správce")</span><span class="sxs-lookup"><span data-stu-id="ab6a9-118">With Administrative privileges ("Run as administrator")</span></span>

<span data-ttu-id="ab6a9-119">Klikněte na tlačítko **spustit**, typ **prostředí PowerShell**, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na **spustit jako správce**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-119">Click **Start**, type **PowerShell**, right-click **Windows PowerShell**, and then click **Run as administrator**.</span></span>

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="ab6a9-120">Postup spuštění Windows PowerShell ISE na starších verzích systému Windows</span><span class="sxs-lookup"><span data-stu-id="ab6a9-120">How to Start Windows PowerShell ISE on Earlier Releases of Windows</span></span>

<span data-ttu-id="ab6a9-121">Ke spuštění Windows PowerShell ISE, použijte některý z následujících metod.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-121">Use any of the following methods to start Windows PowerShell ISE.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="ab6a9-122">Z nabídky Start</span><span class="sxs-lookup"><span data-stu-id="ab6a9-122">From the Start Menu</span></span>

- <span data-ttu-id="ab6a9-123">Klikněte na tlačítko **spustit**, typ **ISE**a potom klikněte na **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-123">Click **Start**, type **ISE**, and then click **Windows PowerShell ISE**.</span></span>
- <span data-ttu-id="ab6a9-124">Z **spustit** nabídky, klikněte na tlačítko **spustit**, klikněte na tlačítko **všechny programy**, klikněte na tlačítko **Příslušenství**, klikněte na tlačítko **prostředí Windows PowerShell**  složku a pak klikněte na tlačítko **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-124">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell ISE**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="ab6a9-125">Na příkazovém řádku</span><span class="sxs-lookup"><span data-stu-id="ab6a9-125">At the Command Prompt</span></span>

<span data-ttu-id="ab6a9-126">V Cmd.exe, prostředí Windows PowerShell nebo ISE Windows PowerShell spusťte prostředí Windows PowerShell, zadejte:</span><span class="sxs-lookup"><span data-stu-id="ab6a9-126">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

```
PowerShell_ISE
```

<span data-ttu-id="ab6a9-127">nebo</span><span class="sxs-lookup"><span data-stu-id="ab6a9-127">or</span></span>

```
ISE
```

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="ab6a9-128">Pomocí správy oprávnění ("Spustit jako správce")</span><span class="sxs-lookup"><span data-stu-id="ab6a9-128">With Administrative privileges ("Run as administrator")</span></span>

<span data-ttu-id="ab6a9-129">Klikněte na tlačítko **spustit**, typ **ISE**, klikněte pravým tlačítkem na **Windows PowerShell ISE**a potom klikněte na **spustit jako správce**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-129">Click **Start**, type **ISE**, right-click **Windows PowerShell ISE**, and then click **Run as administrator**.</span></span>

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="ab6a9-130">Postup povolení ISE Windows PowerShell na starších verzích systému Windows</span><span class="sxs-lookup"><span data-stu-id="ab6a9-130">How to Enable Windows PowerShell ISE on Earlier Releases of Windows</span></span>

<span data-ttu-id="ab6a9-131">V prostředí Windows PowerShell 4.0 a prostředí Windows PowerShell 3.0 je povoleno Windows PowerShell ISE ve výchozím nastavení ve všech verzích systému Windows.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-131">In Windows PowerShell 4.0 and Windows PowerShell 3.0, Windows PowerShell ISE is enabled by default on all versions of Windows.</span></span> <span data-ttu-id="ab6a9-132">Pokud již není povolena, Windows Management Framework 4.0 nebo Windows Management Framework 3.0 povolí ho.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-132">If it is not already enabled, Windows Management Framework 4.0 or Windows Management Framework 3.0 enables it.</span></span>

<span data-ttu-id="ab6a9-133">V prostředí Windows PowerShell 2.0 je povoleno Windows PowerShell ISE ve výchozím nastavení v systému Windows 7.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-133">In Windows PowerShell 2.0, Windows PowerShell ISE is enabled by default on Windows 7.</span></span> <span data-ttu-id="ab6a9-134">Na Windows Server 2008 R2 a Windows Server 2008, je však volitelná funkce.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-134">However, on Windows Server 2008 R2 and Windows Server 2008, it is an optional feature.</span></span>

<span data-ttu-id="ab6a9-135">Pokud chcete povolit ISE Windows PowerShell v prostředí Windows PowerShell 2.0 na Windows Server 2008 R2 nebo Windows Server 2008, použijte následující postup.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-135">To enable Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server 2008 R2 or Windows Server 2008, use the following procedure.</span></span>

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a><span data-ttu-id="ab6a9-136">Chcete-li povolit Windows PowerShell Integrované skriptovací prostředí (ISE)</span><span class="sxs-lookup"><span data-stu-id="ab6a9-136">To enable Windows PowerShell Integrated Scripting Environment (ISE)</span></span>

1. <span data-ttu-id="ab6a9-137">Spusťte Správce serveru.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-137">Start Server Manager.</span></span>
2. <span data-ttu-id="ab6a9-138">Klikněte na tlačítko **funkce** a pak klikněte na **přidat funkce**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-138">Click **Features** and then click **Add Features**.</span></span>
3. <span data-ttu-id="ab6a9-139">V části Vybrat funkce klikněte na tlačítko Windows PowerShell Integrované skriptovací prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="ab6a9-139">In Select Features, click Windows PowerShell Integrated Scripting Environment (ISE).</span></span>

## <a name="starting-the-32-bit-version-of-windows-powershell"></a><span data-ttu-id="ab6a9-140">Spuštění 32bitové verze prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab6a9-140">Starting the 32-Bit Version of Windows PowerShell</span></span>

<span data-ttu-id="ab6a9-141">Při instalaci prostředí Windows PowerShell na 64bitovém počítači **prostředí Windows PowerShell (x86)**, 32bitová verze prostředí Windows PowerShell je nainstalovaný kromě 64bitovou verzi.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-141">When you install Windows PowerShell on a 64-bit computer, **Windows PowerShell (x86)**, a 32-bit version of Windows PowerShell is installed in addition to the 64-bit version.</span></span> <span data-ttu-id="ab6a9-142">Při spuštění prostředí Windows PowerShell ve výchozím nastavení spustí 64bitovou verzi.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-142">When you run Windows PowerShell, the 64-bit version runs by default.</span></span>

<span data-ttu-id="ab6a9-143">Však může někdy musíte spustit **prostředí Windows PowerShell (x86)**, například při použití modulu, který vyžaduje 32bitovou verzi nebo kdy se vzdáleně připojují k 32bitového počítače.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-143">However, you might occasionally need to run **Windows PowerShell (x86)**, such as when you are using a module that requires the 32-bit version or when you are connecting remotely to a 32-bit computer.</span></span>

<span data-ttu-id="ab6a9-144">Spusťte 32bitovou verzi prostředí Windows PowerShell, použijte některý z následujících postupů.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-144">To start a 32-bit version of Windows PowerShell, use any of the following procedures.</span></span>

#### <a name="in-windows-server-2012-r2"></a><span data-ttu-id="ab6a9-145">In Windows Server® 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ab6a9-145">In Windows Server® 2012 R2</span></span>

- <span data-ttu-id="ab6a9-146">Na **spustit** zadejte **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-146">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="ab6a9-147">Klikněte **prostředí Windows PowerShell x86** dlaždici.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-147">Click the **Windows PowerShell x86** tile.</span></span>
- <span data-ttu-id="ab6a9-148">V **správce serveru**, z **nástroje** nabídce vyberte možnost **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-148">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="ab6a9-149">Přesunutí kurzoru do pravého horního rohu klikněte na ploše **vyhledávání**, typ **prostředí PowerShell x86** a pak klikněte na **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-149">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="ab6a9-150">Prostřednictvím příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="ab6a9-150">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-server-2012"></a><span data-ttu-id="ab6a9-151">In Windows Server® 2012</span><span class="sxs-lookup"><span data-stu-id="ab6a9-151">In Windows Server® 2012</span></span>

- <span data-ttu-id="ab6a9-152">Na **spustit** zadejte **prostředí PowerShell** a pak klikněte na **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-152">On the **Start** screen, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="ab6a9-153">V **správce serveru**, z **nástroje** nabídce vyberte možnost **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-153">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="ab6a9-154">Přesunutí kurzoru do pravého horního rohu klikněte na ploše **vyhledávání**, typ **prostředí PowerShell** a pak klikněte na **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-154">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="ab6a9-155">Prostřednictvím příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="ab6a9-155">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-81"></a><span data-ttu-id="ab6a9-156">V Windows® 8.1</span><span class="sxs-lookup"><span data-stu-id="ab6a9-156">In Windows® 8.1</span></span>

- <span data-ttu-id="ab6a9-157">Na **spustit** zadejte **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-157">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="ab6a9-158">Klikněte **prostředí Windows PowerShell x86** dlaždici.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-158">Click the **Windows PowerShell x86** tile.</span></span>
- <span data-ttu-id="ab6a9-159">Pokud používáte [nástrojů pro vzdálenou správu serveru](http://go.microsoft.com/fwlink/?LinkID=304145) pro Windows 8.1, můžete také otevřít prostředí Windows PowerShell x86 z **Server ManagerTools** nabídky.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-159">If you are running [Remote Server Administration Tools](http://go.microsoft.com/fwlink/?LinkID=304145) for Windows 8.1, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span>
  <span data-ttu-id="ab6a9-160">Vyberte **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-160">Select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="ab6a9-161">Přesunutí kurzoru do pravého horního rohu klikněte na ploše **vyhledávání**, typ **prostředí PowerShell x86** a pak klikněte na **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-161">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="ab6a9-162">Prostřednictvím příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="ab6a9-162">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-8"></a><span data-ttu-id="ab6a9-163">V Windows® 8</span><span class="sxs-lookup"><span data-stu-id="ab6a9-163">In Windows® 8</span></span>

- <span data-ttu-id="ab6a9-164">Na **spustit** obrazovky, přesuňte se ukazatelem do pravého horního rohu, klikněte na **nastavení**, klikněte na tlačítko **dlaždice**a poté přesuňte **zobrazit nástroje pro správu** jezdec na Ano.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-164">On the **Start** screen, move the cursor to the upper right corner, click **Settings**, click **Tiles**, and then move the **Show Administrative Tools** slider to Yes.</span></span> <span data-ttu-id="ab6a9-165">Poté zadejte **prostředí PowerShell** a klikněte na tlačítko **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-165">Then, type **PowerShell** and click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="ab6a9-166">Pokud používáte [nástrojů pro vzdálenou správu serveru](http://www.microsoft.com/download/details.aspx?id=28972) pro systém Windows 8, můžete také otevřít prostředí Windows PowerShell x86 z **Server ManagerTools** nabídky.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-166">If you are running [Remote Server Administration Tools](http://www.microsoft.com/download/details.aspx?id=28972) for Windows 8, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span> <span data-ttu-id="ab6a9-167">Vyberte **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-167">Select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="ab6a9-168">Na **spustit** obrazovky nebo plocha, zadejte **prostředí PowerShell (x86)** a pak klikněte na **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="ab6a9-168">On the **Start** screen or the desktop, type **PowerShell (x86)** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="ab6a9-169">Prostřednictvím příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="ab6a9-169">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>