---
ms.date: 2017-08-09
keywords: "prostředí PowerShell, rutiny, stažení, instalace, instalační program, windows 10, windows 8.1, windows 8.0, windows 7"
title: "Instalace prostředí Windows PowerShell"
ms.openlocfilehash: 781bf50b6ac649e72bcdbb708555275fb7422d94
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2017
---
# <a name="installing-windows-powershell"></a><span data-ttu-id="46ee0-103">Instalace prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="46ee0-103">Installing Windows PowerShell</span></span>

<span data-ttu-id="46ee0-104">Prostředí PowerShell nainstalovaný ve výchozím nastavení v každé Windows od verze Windows 7 SP1 a Windows Server 2008 R2 SP1.</span><span class="sxs-lookup"><span data-stu-id="46ee0-104">PowerShell comes installed by default in every Windows, starting with Windows 7 SP1 and Windows Server 2008 R2 SP1.</span></span>

<span data-ttu-id="46ee0-105">Uživatelé Linuxu, systému macOS a systému Windows, které chcete nainstalovat **prostředí PowerShell 6** (beta) ve své počítače, třeba:</span><span class="sxs-lookup"><span data-stu-id="46ee0-105">Linux, macOS, and Windows users that would like to install **PowerShell 6** (beta), in their machines, need to:</span></span>

1. <span data-ttu-id="46ee0-106">Získat prostředí PowerShell pro konkrétní operační systém a verze, ze [Githubu](https://github.com/powershell/powershell#get-powershell)</span><span class="sxs-lookup"><span data-stu-id="46ee0-106">Get PowerShell for the specific OS and version, from [GitHub](https://github.com/powershell/powershell#get-powershell)</span></span>
1. <span data-ttu-id="46ee0-107">Postupujte podle pokynů pro instalaci</span><span class="sxs-lookup"><span data-stu-id="46ee0-107">Follow the installation instructions</span></span>
  - [<span data-ttu-id="46ee0-108">Linux</span><span class="sxs-lookup"><span data-stu-id="46ee0-108">Linux</span></span>](https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md)
  - [<span data-ttu-id="46ee0-109">systému macOS</span><span class="sxs-lookup"><span data-stu-id="46ee0-109">macOS</span></span>](https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md#macos-1012)
  - [<span data-ttu-id="46ee0-110">Windows</span><span class="sxs-lookup"><span data-stu-id="46ee0-110">Windows</span></span>](https://github.com/PowerShell/PowerShell/blob/master/docs/installation/windows.md#msi)

<span data-ttu-id="46ee0-111">6 prostředí PowerShell je také k dispozici pro Docker; v tématu [Docker instalace](https://github.com/PowerShell/PowerShell/tree/master/docker) pokyny.</span><span class="sxs-lookup"><span data-stu-id="46ee0-111">PowerShell 6 is also available for Docker; see [Docker installation](https://github.com/PowerShell/PowerShell/tree/master/docker) instructions.</span></span>

## <a name="finding-powershell-in-windows-10-81-80-and-7"></a><span data-ttu-id="46ee0-112">Hledání prostředí PowerShell v systému Windows 10, 8.1, 8.0 a 7</span><span class="sxs-lookup"><span data-stu-id="46ee0-112">Finding PowerShell in Windows 10, 8.1, 8.0, and 7</span></span>

<span data-ttu-id="46ee0-113">Někdy vyhledání prostředí PowerShell konzoly nebo ISE (Integrované skriptovací prostředí) v systému Windows může být složité, jako jeho umístění přechází z jedné verze systému Windows na další.</span><span class="sxs-lookup"><span data-stu-id="46ee0-113">Sometimes locating PowerShell console or ISE (Integrated Scripting Environment) in Windows can be difficult, as it's location moves from one version of Windows to the next.</span></span>

<span data-ttu-id="46ee0-114">Následující tabulky by měly pomoci při hledání prostředí PowerShell ve vaší verzi systému Windows.</span><span class="sxs-lookup"><span data-stu-id="46ee0-114">The following tables should help you find PowerShell in your Windows version.</span></span>
<span data-ttu-id="46ee0-115">Všechny verze tady jsou původní verze, vydání, s žádné aktualizace.</span><span class="sxs-lookup"><span data-stu-id="46ee0-115">All versions listed here are the original version, as released, with no updates.</span></span>

### <a name="for-console"></a><span data-ttu-id="46ee0-116">Pro konzolu</span><span class="sxs-lookup"><span data-stu-id="46ee0-116">For Console</span></span>

<span data-ttu-id="46ee0-117">Verze</span><span class="sxs-lookup"><span data-stu-id="46ee0-117">Version</span></span> | <span data-ttu-id="46ee0-118">Umístění</span><span class="sxs-lookup"><span data-stu-id="46ee0-118">Location</span></span>
-- | --
<span data-ttu-id="46ee0-119">Windows 10</span><span class="sxs-lookup"><span data-stu-id="46ee0-119">Windows 10</span></span> | <span data-ttu-id="46ee0-120">Klikněte levém dolním rohu Windows ikonu, začněte psát prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="46ee0-120">Click left lower corner Windows icon, start typing PowerShell</span></span>
<span data-ttu-id="46ee0-121">Windows 8.1, 8.0</span><span class="sxs-lookup"><span data-stu-id="46ee0-121">Windows 8.1, 8.0</span></span> | <span data-ttu-id="46ee0-122">Na obrazovce start začněte psát prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46ee0-122">On the start screen, start typing PowerShell.</span></span><br/><span data-ttu-id="46ee0-123">Pokud na ploše klikněte levém dolním rohu Windows ikonu, začněte psát prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="46ee0-123">If on desktop, click left lower corner Windows icon, start typing PowerShell</span></span>
<span data-ttu-id="46ee0-124">Windows 7 s aktualizací SP1</span><span class="sxs-lookup"><span data-stu-id="46ee0-124">Windows 7 SP1</span></span> | <span data-ttu-id="46ee0-125">Klikněte na levém dolním rohu Windows ikonu, při spuštění pole hledání zadáte prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="46ee0-125">Click left lower corner Windows icon, on the search box start typing PowerShell</span></span>

### <a name="for-ise"></a><span data-ttu-id="46ee0-126">Pro ISE</span><span class="sxs-lookup"><span data-stu-id="46ee0-126">For ISE</span></span>

<span data-ttu-id="46ee0-127">Verze</span><span class="sxs-lookup"><span data-stu-id="46ee0-127">Version</span></span> | <span data-ttu-id="46ee0-128">Umístění</span><span class="sxs-lookup"><span data-stu-id="46ee0-128">Location</span></span>
-- | --
<span data-ttu-id="46ee0-129">Windows 10</span><span class="sxs-lookup"><span data-stu-id="46ee0-129">Windows 10</span></span> | <span data-ttu-id="46ee0-130">Klikněte levém dolním rohu Windows ikonu, začněte psát ISE</span><span class="sxs-lookup"><span data-stu-id="46ee0-130">Click left lower corner Windows icon, start typing ISE</span></span>
<span data-ttu-id="46ee0-131">Windows 8.1, 8.0</span><span class="sxs-lookup"><span data-stu-id="46ee0-131">Windows 8.1, 8.0</span></span> | <span data-ttu-id="46ee0-132">Na obrazovce start zadejte **prostředí PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="46ee0-132">On the start screen, type **PowerShell ISE**.</span></span><br/><span data-ttu-id="46ee0-133">Pokud je na ploše, klikněte na ikonu Windows dolním rohu, zadejte **prostředí PowerShell ISE**</span><span class="sxs-lookup"><span data-stu-id="46ee0-133">If on desktop, click left lower corner Windows icon, type **PowerShell ISE**</span></span>
<span data-ttu-id="46ee0-134">Windows 7 s aktualizací SP1</span><span class="sxs-lookup"><span data-stu-id="46ee0-134">Windows 7 SP1</span></span> | <span data-ttu-id="46ee0-135">Klikněte na levém dolním rohu Windows ikonu, při spuštění pole hledání zadáte prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="46ee0-135">Click left lower corner Windows icon, on the search box start typing PowerShell</span></span>

## <a name="finding-powershell-in-windows-server-versions"></a><span data-ttu-id="46ee0-136">Hledání v systému Windows Server verze prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="46ee0-136">Finding PowerShell in Windows Server versions</span></span>

<span data-ttu-id="46ee0-137">Od verze Windows Server 2008 R2, můžete nainstalovat operační systém Windows bez grafické uživatelské rozhraní (GUI).</span><span class="sxs-lookup"><span data-stu-id="46ee0-137">Starting with Windows Server 2008 R2, Windows operating system can be installed without the graphical user interface (GUI).</span></span>
<span data-ttu-id="46ee0-138">Edice systému Windows Server bez grafického uživatelského rozhraní jsou pojmenované **základní** s názvem edice a edice s grafické uživatelské rozhraní **plochy**.</span><span class="sxs-lookup"><span data-stu-id="46ee0-138">Editions of Windows Server without GUI are named **Core** editions, and editions with the GUI are named **Desktop**.</span></span>

### <a name="windows-server-core-editions"></a><span data-ttu-id="46ee0-139">Edice systému Windows Server Core</span><span class="sxs-lookup"><span data-stu-id="46ee0-139">Windows Server Core editions</span></span>

<span data-ttu-id="46ee0-140">Ve všech edicích základní při přihlášení k serveru zobrazí okno příkazového řádku systému Windows.</span><span class="sxs-lookup"><span data-stu-id="46ee0-140">In all Core editions, when you log to the server you get a Windows command prompt window.</span></span>

<span data-ttu-id="46ee0-141">Typ `powershell` a stiskněte klávesu **ENTER** spuštění prostředí PowerShell v relaci příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="46ee0-141">Type `powershell` and press **ENTER** to start PowerShell inside the command prompt session.</span></span> <span data-ttu-id="46ee0-142">Typ `exit` ukončit relaci prostředí PowerShell a vrátíte se do příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="46ee0-142">Type `exit` to terminate the PowerShell session and return to command prompt.</span></span>

### <a name="windows-server-desktop-editions"></a><span data-ttu-id="46ee0-143">Edice Windows serveru Desktop</span><span class="sxs-lookup"><span data-stu-id="46ee0-143">Windows Server Desktop editions</span></span>

<span data-ttu-id="46ee0-144">Ve všech edicích plochy klikněte na ikonu Windows levém dolním rohu, začněte psát prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46ee0-144">In all desktop editions, click the left lower corner Windows icon, start typing PowerShell.</span></span>
<span data-ttu-id="46ee0-145">Zobrazí konzole a možnosti ISE.</span><span class="sxs-lookup"><span data-stu-id="46ee0-145">You get both console and ISE options.</span></span>

<span data-ttu-id="46ee0-146">Jedinou výjimkou výše uvedené pravidlo je (ISE) v systému Windows Server 2008 R2 SP1; v takovém případě klikněte na ikonu Windows levém dolním rohu, zadejte PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="46ee0-146">The only exception to the above rule is the ISE in Windows Server 2008 R2 SP1; in this case, click the left lower corner Windows icon, type PowerShell ISE.</span></span>

## <a name="how-to-check-the-version-of-powershell"></a><span data-ttu-id="46ee0-147">Postupy: Kontrola verze prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="46ee0-147">How to check the version of PowerShell</span></span>

<span data-ttu-id="46ee0-148">K vyhledání, která verze prostředí PowerShell jste nainstalovali, spusťte konzolu PowerShell (nebo ISE) a typ `$PSVersionTable` a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="46ee0-148">To find which version of PowerShell you have installed, start a PowerShell console (or the ISE) and type `$PSVersionTable` and press **ENTER**.</span></span>

## <a name="upgrading-existing-windows-powershell"></a><span data-ttu-id="46ee0-149">Upgrade stávající prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="46ee0-149">Upgrading existing Windows PowerShell</span></span>

<span data-ttu-id="46ee0-150">Instalační balíček pro prostředí PowerShell dodává uvnitř instalační program WMF.</span><span class="sxs-lookup"><span data-stu-id="46ee0-150">The installation package for PowerShell comes inside a WMF installer.</span></span>
<span data-ttu-id="46ee0-151">Verze Instalační služby WMF odpovídá verzi prostředí PowerShell; není k dispozici žádný samostatný instalační program pro prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46ee0-151">The version of the WMF installer matches the version of PowerShell; there's no stand alone installer for Windows PowerShell.</span></span>

<span data-ttu-id="46ee0-152">Pokud je potřeba aktualizovat vaší stávající verzi prostředí PowerShell, v systému Windows, použijte v následující tabulce vyhledejte instalační program pro verzi prostředí PowerShell, které chcete aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="46ee0-152">If you need to update your existing version of PowerShell, in Windows, use the following table to locate the installer for the version of PowerShell you want to update to.</span></span>

<span data-ttu-id="46ee0-153">Windows</span><span class="sxs-lookup"><span data-stu-id="46ee0-153">Windows</span></span> | <span data-ttu-id="46ee0-154">PS 3.0</span><span class="sxs-lookup"><span data-stu-id="46ee0-154">PS 3.0</span></span> | <span data-ttu-id="46ee0-155">PS 4.0</span><span class="sxs-lookup"><span data-stu-id="46ee0-155">PS 4.0</span></span> | <span data-ttu-id="46ee0-156">PS 5.0</span><span class="sxs-lookup"><span data-stu-id="46ee0-156">PS 5.0</span></span> | <span data-ttu-id="46ee0-157">PS 5.1</span><span class="sxs-lookup"><span data-stu-id="46ee0-157">PS 5.1</span></span> |
--|--|--|--|--|
<span data-ttu-id="46ee0-158">Windows 10 (viz Note1)</span><span class="sxs-lookup"><span data-stu-id="46ee0-158">Windows 10 (see Note1)</span></span><br/><span data-ttu-id="46ee0-159">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="46ee0-159">Windows Server 2016</span></span> | - | - | - | <span data-ttu-id="46ee0-160">nainstalovaná</span><span class="sxs-lookup"><span data-stu-id="46ee0-160">installed</span></span>
<span data-ttu-id="46ee0-161">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="46ee0-161">Windows 8.1</span></span><br/><span data-ttu-id="46ee0-162">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="46ee0-162">Windows Server 2012 R2</span></span> | - | <span data-ttu-id="46ee0-163">nainstalovaná</span><span class="sxs-lookup"><span data-stu-id="46ee0-163">installed</span></span> | [<span data-ttu-id="46ee0-164">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="46ee0-164">WMF 5.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [<span data-ttu-id="46ee0-165">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="46ee0-165">WMF 5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
<span data-ttu-id="46ee0-166">Windows 8</span><span class="sxs-lookup"><span data-stu-id="46ee0-166">Windows 8</span></span><br/><span data-ttu-id="46ee0-167">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="46ee0-167">Windows Server 2012</span></span> | <span data-ttu-id="46ee0-168">nainstalovaná</span><span class="sxs-lookup"><span data-stu-id="46ee0-168">installed</span></span> | [<span data-ttu-id="46ee0-169">FORMÁT WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="46ee0-169">WMF 4.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [<span data-ttu-id="46ee0-170">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="46ee0-170">WMF 5.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [<span data-ttu-id="46ee0-171">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="46ee0-171">WMF 5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
<span data-ttu-id="46ee0-172">Windows 7 s aktualizací SP1</span><span class="sxs-lookup"><span data-stu-id="46ee0-172">Windows 7 SP1</span></span><br/><span data-ttu-id="46ee0-173">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="46ee0-173">Windows Server 2008 R2 SP1</span></span> | [<span data-ttu-id="46ee0-174">PODPORA PRODUKTU WMF 3.0</span><span class="sxs-lookup"><span data-stu-id="46ee0-174">WMF 3.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=34595) | [<span data-ttu-id="46ee0-175">FORMÁT WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="46ee0-175">WMF 4.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [<span data-ttu-id="46ee0-176">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="46ee0-176">WMF 5.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [<span data-ttu-id="46ee0-177">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="46ee0-177">WMF 5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=54616)

> <span data-ttu-id="46ee0-178">**Poznámka: 1**:</span><span class="sxs-lookup"><span data-stu-id="46ee0-178">**Note 1**:</span></span>
  >>
  >> <span data-ttu-id="46ee0-179">Počáteční verze Windows 10 ve funkci Automatické aktualizace povolena získá z verze 5.0 pro 5.1 aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46ee0-179">On the initial release of Windows 10, with automatic updates enabled, PowerShell gets updated from version 5.0 to 5.1.</span></span>
  >>
  >> <span data-ttu-id="46ee0-180">Pokud původní verzi Windows 10 není aktualizován prostřednictvím aktualizací systému Windows, verze prostředí PowerShell je 5.0.</span><span class="sxs-lookup"><span data-stu-id="46ee0-180">If the original version of Windows 10 is not updated through Windows Updates, the version of PowerShell is 5.0.</span></span>

## <a name="need-azure-powershell"></a><span data-ttu-id="46ee0-181">Třeba prostředí Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="46ee0-181">Need Azure PowerShell</span></span>

<span data-ttu-id="46ee0-182">Pokud hledáte **prostředí Azure PowerShell**, můžete začít s [Přehled prostředí Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure).</span><span class="sxs-lookup"><span data-stu-id="46ee0-182">If you're looking for **Azure PowerShell**, you could start with [Overview of Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure).</span></span>

<span data-ttu-id="46ee0-183">Co může být nutné, jinak je [nainstalovat a nakonfigurovat Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="46ee0-183">Otherwise, what you might need is [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)</span></span>

## <a name="see-also"></a><span data-ttu-id="46ee0-184">Viz také</span><span class="sxs-lookup"><span data-stu-id="46ee0-184">See Also</span></span>

- [<span data-ttu-id="46ee0-185">Požadavky na prostředí PowerShell systému Windows</span><span class="sxs-lookup"><span data-stu-id="46ee0-185">Windows PowerShell System Requirements</span></span>](Windows-PowerShell-System-Requirements.md)
- [<span data-ttu-id="46ee0-186">Spuštění prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="46ee0-186">Starting Windows PowerShell</span></span>](Starting-Windows-PowerShell.md)
