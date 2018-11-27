---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Spuštění Windows PowerShellu
ms.assetid: 59b649a2-c90c-4cf4-bf95-a740c59148e7
ms.openlocfilehash: 9184e8b0e508610e7f4775f1032f3a69c93bb8c1
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320529"
---
# <a name="starting-windows-powershell"></a><span data-ttu-id="b188d-103">Spuštění Windows PowerShellu</span><span class="sxs-lookup"><span data-stu-id="b188d-103">Starting Windows PowerShell</span></span>
<span data-ttu-id="b188d-104">PowerShell je skriptovací modul dll, která je součástí několika hostitelích.</span><span class="sxs-lookup"><span data-stu-id="b188d-104">PowerShell is a scripting engine dll which is embedded into multiple hosts.</span></span>  <span data-ttu-id="b188d-105">Nejběžnější hostitele, bude zahájena jsou interaktivního příkazového řádku PowerShell.exe a interaktivní prostředí PowerShell_ISE.exe skriptování.</span><span class="sxs-lookup"><span data-stu-id="b188d-105">The most common host you will start are the interactive command line PowerShell.exe and the Interactive Scripting Environment PowerShell_ISE.exe.</span></span>

<span data-ttu-id="b188d-106">Spusťte Windows PowerShell® na Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012 a Windows 8, naleznete v tématu [běžné úlohy správy a navigace](https://technet.microsoft.com/library/hh831491.aspx).</span><span class="sxs-lookup"><span data-stu-id="b188d-106">To start Windows PowerShell® on Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012, and Windows 8, see [Common Management Tasks and Navigation](https://technet.microsoft.com/library/hh831491.aspx).</span></span>

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a><span data-ttu-id="b188d-107">Postup spuštění prostředí Windows PowerShell na starších verzích Windows</span><span class="sxs-lookup"><span data-stu-id="b188d-107">How to Start Windows PowerShell on Earlier Versions of Windows</span></span>

<span data-ttu-id="b188d-108">Tato část vysvětluje, jak spustit prostředí Windows PowerShell a Windows Powershellu integrovaném skriptovacím prostředí (ISE) ve Windows® 7, Windows Server® 2008 R2 a Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="b188d-108">This section explains how to start Windows PowerShell and Windows PowerShell Integrated Scripting Environment (ISE) on Windows® 7, Windows Server® 2008 R2, and Windows Server® 2008.</span></span> <span data-ttu-id="b188d-109">Také vysvětluje, jak povolit volitelné funkce pro Windows PowerShell ISE Windows PowerShell 2.0 na Windows Server® 2008 R2 a Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="b188d-109">It also explains how to enable the optional feature for Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server® 2008 R2 and Windows Server® 2008.</span></span>

<span data-ttu-id="b188d-110">Použijte některou z následujících metod spustit nainstalovanou verzi Windows PowerShell 3.0 nebo Windows PowerShell 4.0, kde je to možné.</span><span class="sxs-lookup"><span data-stu-id="b188d-110">Use any of the following methods to start the installed version of Windows PowerShell 3.0, or Windows PowerShell 4.0, where applicable.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="b188d-111">Z nabídky Start</span><span class="sxs-lookup"><span data-stu-id="b188d-111">From the Start Menu</span></span>

- <span data-ttu-id="b188d-112">Klikněte na tlačítko **Start**, typ **PowerShell**a potom klikněte na tlačítko **prostředí Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b188d-112">Click **Start**, type **PowerShell**, and then click **Windows PowerShell**.</span></span>
- <span data-ttu-id="b188d-113">Z **Start** nabídky, klikněte na tlačítko **Start**, klikněte na tlačítko **všechny programy**, klikněte na tlačítko **Příslušenství**, klikněte na tlačítko **prostředí Windows PowerShell**  složku a pak klikněte na tlačítko **prostředí Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b188d-113">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="b188d-114">Na příkazovém řádku</span><span class="sxs-lookup"><span data-stu-id="b188d-114">At the Command Prompt</span></span>

<span data-ttu-id="b188d-115">Do pole Cmd.exe, prostředí Windows PowerShell nebo ISE Windows PowerShell spusťte prostředí Windows PowerShell, zadejte:</span><span class="sxs-lookup"><span data-stu-id="b188d-115">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

```
PowerShell
```

<span data-ttu-id="b188d-116">Parametry programu PowerShell.exe můžete také použít k přizpůsobení relace.</span><span class="sxs-lookup"><span data-stu-id="b188d-116">You can also use the parameters of the PowerShell.exe program to customize the session.</span></span> <span data-ttu-id="b188d-117">Další informace najdete v tématu [Nápověda příkazového řádku pro PowerShell.exe](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span><span class="sxs-lookup"><span data-stu-id="b188d-117">For more information, see [PowerShell.exe Command-Line Help](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span></span>

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="b188d-118">Pomocí správy oprávnění ("Spustit jako správce")</span><span class="sxs-lookup"><span data-stu-id="b188d-118">With Administrative privileges ("Run as administrator")</span></span>

<span data-ttu-id="b188d-119">Klikněte na tlačítko **Start**, typ **PowerShell**, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na tlačítko **spustit jako správce**.</span><span class="sxs-lookup"><span data-stu-id="b188d-119">Click **Start**, type **PowerShell**, right-click **Windows PowerShell**, and then click **Run as administrator**.</span></span>

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="b188d-120">Postup spuštění Windows PowerShell ISE na starších verzích Windows</span><span class="sxs-lookup"><span data-stu-id="b188d-120">How to Start Windows PowerShell ISE on Earlier Releases of Windows</span></span>

<span data-ttu-id="b188d-121">Použijte některý z následujících metod ke spuštění Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="b188d-121">Use any of the following methods to start Windows PowerShell ISE.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="b188d-122">Z nabídky Start</span><span class="sxs-lookup"><span data-stu-id="b188d-122">From the Start Menu</span></span>

- <span data-ttu-id="b188d-123">Klikněte na tlačítko **Start**, typ **ISE**a potom klikněte na tlačítko **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="b188d-123">Click **Start**, type **ISE**, and then click **Windows PowerShell ISE**.</span></span>
- <span data-ttu-id="b188d-124">Z **Start** nabídky, klikněte na tlačítko **Start**, klikněte na tlačítko **všechny programy**, klikněte na tlačítko **Příslušenství**, klikněte na tlačítko **prostředí Windows PowerShell**  složku a pak klikněte na tlačítko **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="b188d-124">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell ISE**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="b188d-125">Na příkazovém řádku</span><span class="sxs-lookup"><span data-stu-id="b188d-125">At the Command Prompt</span></span>

<span data-ttu-id="b188d-126">Do pole Cmd.exe, prostředí Windows PowerShell nebo ISE Windows PowerShell spusťte prostředí Windows PowerShell, zadejte:</span><span class="sxs-lookup"><span data-stu-id="b188d-126">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

```
PowerShell_ISE
```

<span data-ttu-id="b188d-127">nebo</span><span class="sxs-lookup"><span data-stu-id="b188d-127">or</span></span>

```
ISE
```

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="b188d-128">Pomocí správy oprávnění ("Spustit jako správce")</span><span class="sxs-lookup"><span data-stu-id="b188d-128">With Administrative privileges ("Run as administrator")</span></span>

<span data-ttu-id="b188d-129">Klikněte na tlačítko **Start**, typ **ISE**, klikněte pravým tlačítkem na **Windows PowerShell ISE**a potom klikněte na tlačítko **spustit jako správce**.</span><span class="sxs-lookup"><span data-stu-id="b188d-129">Click **Start**, type **ISE**, right-click **Windows PowerShell ISE**, and then click **Run as administrator**.</span></span>

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="b188d-130">Jak povolit ISE Windows PowerShell na starších verzích Windows</span><span class="sxs-lookup"><span data-stu-id="b188d-130">How to Enable Windows PowerShell ISE on Earlier Releases of Windows</span></span>

<span data-ttu-id="b188d-131">Ve Windows Powershellu 4.0 a Windows PowerShell 3.0 je Windows PowerShell ISE povolena ve výchozím nastavení ve všech verzích Windows.</span><span class="sxs-lookup"><span data-stu-id="b188d-131">In Windows PowerShell 4.0 and Windows PowerShell 3.0, Windows PowerShell ISE is enabled by default on all versions of Windows.</span></span> <span data-ttu-id="b188d-132">Pokud ještě není povolené, Windows Management Framework 4.0 nebo Windows Management Framework 3.0 povolí ho.</span><span class="sxs-lookup"><span data-stu-id="b188d-132">If it is not already enabled, Windows Management Framework 4.0 or Windows Management Framework 3.0 enables it.</span></span>

<span data-ttu-id="b188d-133">V rozhraní Windows PowerShell 2.0 je Windows PowerShell ISE povolena ve výchozím nastavení ve Windows 7.</span><span class="sxs-lookup"><span data-stu-id="b188d-133">In Windows PowerShell 2.0, Windows PowerShell ISE is enabled by default on Windows 7.</span></span> <span data-ttu-id="b188d-134">V systému Windows Server 2008 R2 a Windows Server 2008, je však volitelná funkce.</span><span class="sxs-lookup"><span data-stu-id="b188d-134">However, on Windows Server 2008 R2 and Windows Server 2008, it is an optional feature.</span></span>

<span data-ttu-id="b188d-135">Pokud chcete povolit Windows PowerShell ISE Windows PowerShell 2.0 na Windows Server 2008 R2 nebo Windows Server 2008, pomocí následujícího postupu.</span><span class="sxs-lookup"><span data-stu-id="b188d-135">To enable Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server 2008 R2 or Windows Server 2008, use the following procedure.</span></span>

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a><span data-ttu-id="b188d-136">Povolit Windows Powershellu integrovaném skriptovacím prostředí (ISE)</span><span class="sxs-lookup"><span data-stu-id="b188d-136">To enable Windows PowerShell Integrated Scripting Environment (ISE)</span></span>

1. <span data-ttu-id="b188d-137">Spusťte Správce serveru.</span><span class="sxs-lookup"><span data-stu-id="b188d-137">Start Server Manager.</span></span>
2. <span data-ttu-id="b188d-138">Klikněte na tlačítko **funkce** a potom klikněte na tlačítko **přidat funkce**.</span><span class="sxs-lookup"><span data-stu-id="b188d-138">Click **Features** and then click **Add Features**.</span></span>
3. <span data-ttu-id="b188d-139">V části Vybrat funkce klikněte na Windows Powershellu integrovaném skriptovacím prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="b188d-139">In Select Features, click Windows PowerShell Integrated Scripting Environment (ISE).</span></span>

## <a name="starting-the-32-bit-version-of-windows-powershell"></a><span data-ttu-id="b188d-140">Spuštění 32bitové verze Windows Powershellu</span><span class="sxs-lookup"><span data-stu-id="b188d-140">Starting the 32-Bit Version of Windows PowerShell</span></span>

<span data-ttu-id="b188d-141">Při instalaci prostředí Windows PowerShell na 64bitovém počítači **prostředí Windows PowerShell (x86)**, kromě 64bitovou verzi je nainstalovaná 32bitová verze Windows powershellu.</span><span class="sxs-lookup"><span data-stu-id="b188d-141">When you install Windows PowerShell on a 64-bit computer, **Windows PowerShell (x86)**, a 32-bit version of Windows PowerShell is installed in addition to the 64-bit version.</span></span> <span data-ttu-id="b188d-142">Při spuštění prostředí Windows PowerShell ve výchozím nastavení spustí 64bitovou verzi.</span><span class="sxs-lookup"><span data-stu-id="b188d-142">When you run Windows PowerShell, the 64-bit version runs by default.</span></span>

<span data-ttu-id="b188d-143">Však můžete někdy potřebovat ke spuštění **prostředí Windows PowerShell (x86)**, například při použití modulu, který vyžaduje 32bitovou verzi nebo kdy se vzdáleně připojují k 32bitového počítače.</span><span class="sxs-lookup"><span data-stu-id="b188d-143">However, you might occasionally need to run **Windows PowerShell (x86)**, such as when you are using a module that requires the 32-bit version or when you are connecting remotely to a 32-bit computer.</span></span>

<span data-ttu-id="b188d-144">Pokud chcete spustit 32bitovou verzi Windows powershellu, použijte některý z následujících postupů.</span><span class="sxs-lookup"><span data-stu-id="b188d-144">To start a 32-bit version of Windows PowerShell, use any of the following procedures.</span></span>

#### <a name="in-windows-server-2012-r2"></a><span data-ttu-id="b188d-145">Ve Windows Server® 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b188d-145">In Windows Server® 2012 R2</span></span>

- <span data-ttu-id="b188d-146">Na **Start** zadejte **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="b188d-146">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="b188d-147">Klikněte na tlačítko **prostředí Windows PowerShell x86** dlaždici.</span><span class="sxs-lookup"><span data-stu-id="b188d-147">Click the **Windows PowerShell x86** tile.</span></span>
- <span data-ttu-id="b188d-148">V **správce serveru**, z **nástroje** nabídce vyberte možnost **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="b188d-148">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b188d-149">Přesunutí kurzoru v pravém horním rohu klikněte na ploše **hledání**, typ **PowerShell x86** a potom klikněte na tlačítko **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="b188d-149">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b188d-150">Pomocí příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="b188d-150">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-server-2012"></a><span data-ttu-id="b188d-151">V Windows Server® 2012</span><span class="sxs-lookup"><span data-stu-id="b188d-151">In Windows Server® 2012</span></span>

- <span data-ttu-id="b188d-152">Na **Start** zadejte **PowerShell** a potom klikněte na tlačítko **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="b188d-152">On the **Start** screen, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b188d-153">V **správce serveru**, z **nástroje** nabídce vyberte možnost **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="b188d-153">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b188d-154">Přesunutí kurzoru v pravém horním rohu klikněte na ploše **hledání**, typ **Powershellu** a potom klikněte na tlačítko **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="b188d-154">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b188d-155">Pomocí příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="b188d-155">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-81"></a><span data-ttu-id="b188d-156">V Windows® 8.1</span><span class="sxs-lookup"><span data-stu-id="b188d-156">In Windows® 8.1</span></span>

- <span data-ttu-id="b188d-157">Na **Start** zadejte **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="b188d-157">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="b188d-158">Klikněte na tlačítko **prostředí Windows PowerShell x86** dlaždici.</span><span class="sxs-lookup"><span data-stu-id="b188d-158">Click the **Windows PowerShell x86** tile.</span></span>
- <span data-ttu-id="b188d-159">Pokud používáte [nástroje pro vzdálenou správu serveru](https://go.microsoft.com/fwlink/?LinkID=304145) pro Windows 8.1, můžete také otevřít prostředí Windows PowerShell x86 z **Server ManagerTools** nabídky.</span><span class="sxs-lookup"><span data-stu-id="b188d-159">If you are running [Remote Server Administration Tools](https://go.microsoft.com/fwlink/?LinkID=304145) for Windows 8.1, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span>
  <span data-ttu-id="b188d-160">Vyberte **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="b188d-160">Select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b188d-161">Přesunutí kurzoru v pravém horním rohu klikněte na ploše **hledání**, typ **PowerShell x86** a potom klikněte na tlačítko **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="b188d-161">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b188d-162">Pomocí příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="b188d-162">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-8"></a><span data-ttu-id="b188d-163">V Windows® 8</span><span class="sxs-lookup"><span data-stu-id="b188d-163">In Windows® 8</span></span>

- <span data-ttu-id="b188d-164">Na **Start** obrazovky, přesuňte kurzor na pravém horním rohu, klikněte na tlačítko **nastavení**, klikněte na tlačítko **dlaždice**a poté přesuňte **zobrazit nástroje pro správu** posuvník na hodnotu Ano.</span><span class="sxs-lookup"><span data-stu-id="b188d-164">On the **Start** screen, move the cursor to the upper right corner, click **Settings**, click **Tiles**, and then move the **Show Administrative Tools** slider to Yes.</span></span> <span data-ttu-id="b188d-165">Potom zadejte **PowerShell** a klikněte na tlačítko **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="b188d-165">Then, type **PowerShell** and click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b188d-166">Pokud používáte [nástroje pro vzdálenou správu serveru](https://www.microsoft.com/download/details.aspx?id=28972) pro systém Windows 8, můžete také otevřít prostředí Windows PowerShell x86 z **Server ManagerTools** nabídky.</span><span class="sxs-lookup"><span data-stu-id="b188d-166">If you are running [Remote Server Administration Tools](https://www.microsoft.com/download/details.aspx?id=28972) for Windows 8, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span> <span data-ttu-id="b188d-167">Vyberte **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="b188d-167">Select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b188d-168">Na **Start** obrazovky nebo stolní počítač, zadejte **PowerShell (x86)** a potom klikněte na tlačítko **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="b188d-168">On the **Start** screen or the desktop, type **PowerShell (x86)** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="b188d-169">Pomocí příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="b188d-169">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>