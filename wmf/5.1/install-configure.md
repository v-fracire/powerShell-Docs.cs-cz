---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
contributor: keithb
title: Instalace a konfigurace WMF 5.1
ms.openlocfilehash: e5c7968744a442b4be9f1e43a45e91429a6d6165
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="install-and-configure-wmf-51"></a><span data-ttu-id="22293-103">Instalace a konfigurace WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="22293-103">Install and Configure WMF 5.1</span></span> #


## <a name="download-and-install-the-wmf-51-package"></a><span data-ttu-id="22293-104">Stáhněte a nainstalujte balíček WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="22293-104">Download and install the WMF 5.1 package</span></span>

<span data-ttu-id="22293-105">Stáhněte si balíček WMF 5.1 pro operační systém a architektura, které chcete nainstalovat na:</span><span class="sxs-lookup"><span data-stu-id="22293-105">Download the WMF 5.1 package for the operating system and architecture you wish to install it on:</span></span>

| <span data-ttu-id="22293-106">Operační systém</span><span class="sxs-lookup"><span data-stu-id="22293-106">Operating System</span></span>       | <span data-ttu-id="22293-107">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="22293-107">Prerequisites</span></span>           | <span data-ttu-id="22293-108">Balíček odkazy</span><span class="sxs-lookup"><span data-stu-id="22293-108">Package Links</span></span>                          |
|------------------------|-------------------------|----------------------------------------|
| <span data-ttu-id="22293-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="22293-109">Windows Server 2012 R2</span></span> |                         | <span data-ttu-id="22293-110">[Win8.1AndW2K12R2-KB3191564-x64.msu][]</span><span class="sxs-lookup"><span data-stu-id="22293-110">[Win8.1AndW2K12R2-KB3191564-x64.msu][]</span></span> |
| <span data-ttu-id="22293-111">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="22293-111">Windows Server 2012</span></span>    |                         | <span data-ttu-id="22293-112">[W2K12-KB3191565-x64.msu][]</span><span class="sxs-lookup"><span data-stu-id="22293-112">[W2K12-KB3191565-x64.msu][]</span></span>            |
| <span data-ttu-id="22293-113">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="22293-113">Windows Server 2008 R2</span></span> | <span data-ttu-id="22293-114">[Rozhraní .NET framework 4.5.2][]</span><span class="sxs-lookup"><span data-stu-id="22293-114">[.NET Framework 4.5.2][]</span></span>| <span data-ttu-id="22293-115">[Win7AndW2K8R2. KB3191566 x64.ZIP][]</span><span class="sxs-lookup"><span data-stu-id="22293-115">[Win7AndW2K8R2-KB3191566-x64.ZIP][]</span></span>    |
| <span data-ttu-id="22293-116">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="22293-116">Windows 8.1</span></span>            |                         | <span data-ttu-id="22293-117">**x64:** [Win8.1AndW2K12R2-KB3191564-x64.msu][]</span><span class="sxs-lookup"><span data-stu-id="22293-117">**x64:** [Win8.1AndW2K12R2-KB3191564-x64.msu][]</span></span></br><span data-ttu-id="22293-118">**x86:** [Win8.1-KB3191564-x86.msu][]</span><span class="sxs-lookup"><span data-stu-id="22293-118">**x86:** [Win8.1-KB3191564-x86.msu][]</span></span> |
| <span data-ttu-id="22293-119">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="22293-119">Windows 7 SP1</span></span>          | <span data-ttu-id="22293-120">[Rozhraní .NET framework 4.5.2][]</span><span class="sxs-lookup"><span data-stu-id="22293-120">[.NET Framework 4.5.2][]</span></span>| <span data-ttu-id="22293-121">**x64:** [Win7AndW2K8R2. KB3191566 x64.ZIP][]</span><span class="sxs-lookup"><span data-stu-id="22293-121">**x64:** [Win7AndW2K8R2-KB3191566-x64.ZIP][]</span></span></br><span data-ttu-id="22293-122">**x86:** [Win7. KB3191566 x86.ZIP][]</span><span class="sxs-lookup"><span data-stu-id="22293-122">**x86:** [Win7-KB3191566-x86.ZIP][]</span></span> |

[Rozhraní .NET framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42642
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42642
[W2K12-KB3191565-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839513
[Win7. KB3191566 x86.ZIP]: https://go.microsoft.com/fwlink/?linkid=839522
[Win7-KB3191566-x86.ZIP]: https://go.microsoft.com/fwlink/?linkid=839522
[Win7AndW2K8R2. KB3191566 x64.ZIP]: https://go.microsoft.com/fwlink/?linkid=839523
[Win7AndW2K8R2-KB3191566-x64.ZIP]: https://go.microsoft.com/fwlink/?linkid=839523
[Win8.1-KB3191564-x86.msu]: https://go.microsoft.com/fwlink/?linkid=839521
[Win8.1AndW2K12R2-KB3191564-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839516

## <a name="install-wmf-51-for-windows-server-2008-r2-and-windows-7"></a><span data-ttu-id="22293-129">WMF 5.1 nainstalovat pro systém Windows Server 2008 R2 a Windows 7</span><span class="sxs-lookup"><span data-stu-id="22293-129">Install WMF 5.1 for Windows Server 2008 R2 and Windows 7</span></span>

> <span data-ttu-id="22293-130">**Poznámka:** pokyny k instalaci pro Windows Server 2008 R2 a Windows 7 změnily a se liší od pokynů pro ostatní balíčky.</span><span class="sxs-lookup"><span data-stu-id="22293-130">**Note:** Installation instructions for Windows Server 2008 R2 and Windows 7 have changed, and differ from the instructions for the other packages.</span></span> <span data-ttu-id="22293-131">Pokyny k instalaci pro Windows Server 2012 R2, Windows Server 2012 a Windows 8.1 jsou níže.</span><span class="sxs-lookup"><span data-stu-id="22293-131">Installation instructions for Windows Server 2012 R2, Windows Server 2012, and Windows 8.1 are below.</span></span>

<span data-ttu-id="22293-132">**Instalaci WMF 5.1 v systému Windows Server 2008 R2 a Windows 7**</span><span class="sxs-lookup"><span data-stu-id="22293-132">**Installing WMF 5.1 on Windows Server 2008 R2 and Windows 7**</span></span>

1. <span data-ttu-id="22293-133">Přejděte do složky, do které jste stáhli soubor ZIP.</span><span class="sxs-lookup"><span data-stu-id="22293-133">Navigate to the folder into which you downloaded the ZIP file.</span></span>

2. <span data-ttu-id="22293-134">Klikněte pravým tlačítkem na soubor ZIP a vyberte "Extrahujte všechny...".</span><span class="sxs-lookup"><span data-stu-id="22293-134">Right-click on the ZIP file, and select "Extract All...".</span></span> <span data-ttu-id="22293-135">Souboru Zip obsahuje soubory, 2: MSU a souboru skriptu instalace WMF5.1.PS1.</span><span class="sxs-lookup"><span data-stu-id="22293-135">The Zip contains 2 files: an MSU and the Install-WMF5.1.PS1 script file.</span></span>
<span data-ttu-id="22293-136">Jakmile jste rozbalili souboru ZIP, můžete zkopírovat obsah do jakéhokoli počítače se systémem Windows 7 nebo Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="22293-136">Once you have unpacked the ZIP file, you can copy the contents to any machine running Windows 7 or Windows Server 2008 R2.</span></span>

3. <span data-ttu-id="22293-137">Po extrahování obsahu souboru ZIP, otevřete PowerShell jako správce a pak přejděte do složky obsahující obsah souboru ZIP.</span><span class="sxs-lookup"><span data-stu-id="22293-137">After extracting the ZIP file contents, open PowerShell as administrator, then navigate to the folder containing the contents of the ZIP file.</span></span>

4. <span data-ttu-id="22293-138">Spuštění skriptu Install-Wmf5.1.ps1 v této složce a postupujte podle pokynů.</span><span class="sxs-lookup"><span data-stu-id="22293-138">Run the Install-Wmf5.1.ps1 script in that folder, and follow the instructions.</span></span> <span data-ttu-id="22293-139">Tento skript zkontroluje požadavky v místním počítači a nainstalujte WMF 5.1, pokud byly splněny požadavky.</span><span class="sxs-lookup"><span data-stu-id="22293-139">This script will check the prerequisites on the local machine, and install WMF 5.1 if the prerequisites have been met.</span></span> <span data-ttu-id="22293-140">Požadavky jsou uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="22293-140">The prerequisites are listed below.</span></span>

<span data-ttu-id="22293-141">Instalace WMF5.1.ps1 mají následující parametry k usnadnění automatizace instalaci na Windows Server 2008 R2 a Windows 7:</span><span class="sxs-lookup"><span data-stu-id="22293-141">Install-WMF5.1.ps1 takes the following parameters to ease automating the installation on Windows Server 2008 R2 and Windows 7:</span></span>

- <span data-ttu-id="22293-142">AcceptEula: Pokud je tento parametr zahrnuta, se smlouvou EULA automaticky přijato a nebudou zobrazeny.</span><span class="sxs-lookup"><span data-stu-id="22293-142">AcceptEula: When this parameter is included, the EULA is automatically accepted and will not be displayed.</span></span>
- <span data-ttu-id="22293-143">AllowRestart: Tento parametr můžete pouze použijí, pokud je zadán AcceptEula.</span><span class="sxs-lookup"><span data-stu-id="22293-143">AllowRestart: This parameter can only be used if AcceptEula is specified.</span></span> <span data-ttu-id="22293-144">Pokud tento parametr je součástí, a po instalaci WMF 5.1 je vyžadováno restartování, stane se restartování bez zobrazení výzvy ihned po dokončení instalace.</span><span class="sxs-lookup"><span data-stu-id="22293-144">If this parameter is included, and a restart is required after installing WMF 5.1, the restart will happen without prompting immediately after the installation is completed.</span></span>

<span data-ttu-id="22293-145">**WMF 5.1 požadavky pro Windows Server 2008 R2 SP1 a Windows 7 SP1**</span><span class="sxs-lookup"><span data-stu-id="22293-145">**WMF 5.1 Prerequisites for Windows Server 2008 R2 SP1 and Windows 7 SP1**</span></span>

<span data-ttu-id="22293-146">Instalaci WMF 5.1 v systému Windows Server 2008 R2 SP1 nebo Windows 7 SP1 vyžaduje následující:</span><span class="sxs-lookup"><span data-stu-id="22293-146">Installation of WMF 5.1 on either Windows Server 2008 R2 SP1 or Windows 7 SP1, requires the following:</span></span>
- <span data-ttu-id="22293-147">Musí být nainstalován nejnovější aktualizaci service pack.</span><span class="sxs-lookup"><span data-stu-id="22293-147">Latest service pack must be installed.</span></span>
- <span data-ttu-id="22293-148">Podpora produktu WMF 3.0 **musí není** nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="22293-148">WMF 3.0 **must not** be installed.</span></span> <span data-ttu-id="22293-149">Instalaci WMF 5.1 přes WMF 3.0, bude mít za následek ztrátu PSModulePath, což může způsobit chybu jiných aplikací.</span><span class="sxs-lookup"><span data-stu-id="22293-149">Installing WMF 5.1 over WMF 3.0 will result in the loss of the PSModulePath, which can cause other applications to fail.</span></span> <span data-ttu-id="22293-150">Před instalací WMF 5.1, musíte buď odinstalaci produktu WMF 3.0, nebo uložit PSModulePath a obnovte ji ručně po dokončení instalace WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="22293-150">Before installing WMF 5.1, you must either un-install WMF 3.0, or save the PSModulePath and then restore it manually after WMF 5.1 installation is complete.</span></span>
- <span data-ttu-id="22293-151">WMF 5.1 vyžaduje alespoň [rozhraní .NET Framework 4.5.2](https://www.microsoft.com/en-ca/download/details.aspx?id=42642).</span><span class="sxs-lookup"><span data-stu-id="22293-151">WMF 5.1 requires at least [.NET Framework 4.5.2](https://www.microsoft.com/en-ca/download/details.aspx?id=42642).</span></span>
<span data-ttu-id="22293-152">Podle pokynů v umístění můžete nainstalovat rozhraní Microsoft .NET Framework 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="22293-152">You can install Microsoft .NET Framework 4.5.2 by following the instructions at the download location.</span></span>

<span data-ttu-id="22293-153">**WinRM závislostí**</span><span class="sxs-lookup"><span data-stu-id="22293-153">**WinRM Dependency**</span></span>

<span data-ttu-id="22293-154">Požadovaného stavu aplikace Windows PowerShell (DSC) závisí na vzdálené správy systému Windows.</span><span class="sxs-lookup"><span data-stu-id="22293-154">Windows PowerShell Desired State Configuration (DSC) depends on WinRM.</span></span>
<span data-ttu-id="22293-155">WinRM není povoleno ve výchozím nastavení na Windows Server 2008 R2 a Windows 7.</span><span class="sxs-lookup"><span data-stu-id="22293-155">WinRM is not enabled by default on Windows Server 2008 R2 and Windows 7.</span></span>
<span data-ttu-id="22293-156">Spustit `Set-WSManQuickConfig`, v prostředí Windows PowerShell se zvýšenými oprávněními relace, aby Služba WinRM.</span><span class="sxs-lookup"><span data-stu-id="22293-156">Run `Set-WSManQuickConfig`, in a Windows PowerShell elevated session, to enable WinRM.</span></span>


## <a name="install-wmf-51-for-windows-server-2012-r2-windows-server-2012-and-windows-81"></a><span data-ttu-id="22293-157">WMF 5.1 nainstalovat pro systém Windows Server 2012 R2, Windows Server 2012 a Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="22293-157">Install WMF 5.1 for Windows Server 2012 R2, Windows Server 2012, and Windows 8.1</span></span>
<span data-ttu-id="22293-158">**Nainstalujte z Průzkumníka Windows (nebo v Průzkumníku souborů v systému Windows Server 2012 R2 nebo Windows 8.1)**</span><span class="sxs-lookup"><span data-stu-id="22293-158">**Install from Windows Explorer (or File Explorer in Windows Server 2012 R2 or Windows 8.1)**</span></span>

1. <span data-ttu-id="22293-159">Přejděte do složky, do které jste stáhli soubor MSU.</span><span class="sxs-lookup"><span data-stu-id="22293-159">Navigate to the folder into which you downloaded the MSU file.</span></span>
2. <span data-ttu-id="22293-160">Dvakrát klikněte na MSU ji spustit.</span><span class="sxs-lookup"><span data-stu-id="22293-160">Double-click the MSU to run it.</span></span>

<span data-ttu-id="22293-161">**Instalace z příkazového řádku**</span><span class="sxs-lookup"><span data-stu-id="22293-161">**Installing from the Command Prompt**</span></span>

1. <span data-ttu-id="22293-162">Po stažení správný balíček pro architekturu vašeho počítače, otevřete okno příkazového řádku se zvýšenými uživatelskými právy (příkazem Spustit jako správce).</span><span class="sxs-lookup"><span data-stu-id="22293-162">After downloading the correct package for your computer's architecture, open a Command Prompt window with elevated user rights (Run as Administrator).</span></span> <span data-ttu-id="22293-163">V možnosti instalace jádra serveru systému Windows Server 2012 R2, Windows Server 2012 nebo Windows Server 2008 R2 SP1 příkazový řádek se zvýšenými uživatelskými právy ve výchozím nastavení otevře.</span><span class="sxs-lookup"><span data-stu-id="22293-163">On the Server Core installation options of Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1, Command Prompt opens with elevated user rights by default.</span></span>
2. <span data-ttu-id="22293-164">Změňte adresář na složku, do které jste stáhli nebo zkopírovat WMF 5.1 instalační balíček.</span><span class="sxs-lookup"><span data-stu-id="22293-164">Change directories to the folder into which you have downloaded or copied the WMF 5.1 installation package.</span></span>
3. <span data-ttu-id="22293-165">Spusťte jeden z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="22293-165">Run one of the following commands:</span></span>
   - <span data-ttu-id="22293-166">Na počítačích se systémem Windows Server 2012 R2 nebo Windows 8.1 x64 spusťte `Win8.1AndW2K12R2-KB3191564-x64.msu /quiet`.</span><span class="sxs-lookup"><span data-stu-id="22293-166">On computers that are running Windows Server 2012 R2 or Windows 8.1 x64, run `Win8.1AndW2K12R2-KB3191564-x64.msu /quiet`.</span></span>
   - <span data-ttu-id="22293-167">Na počítačích se systémem Windows Server 2012 spusťte `W2K12-KB3191565-x64.msu /quiet`.</span><span class="sxs-lookup"><span data-stu-id="22293-167">On computers that are running Windows Server 2012, run `W2K12-KB3191565-x64.msu /quiet`.</span></span>
   - <span data-ttu-id="22293-168">Na počítačích se systémem Windows 8.1 x86 spusťte `Win8.1-KB3191564-x86.msu /quiet`.</span><span class="sxs-lookup"><span data-stu-id="22293-168">On computers that are running Windows 8.1 x86, run `Win8.1-KB3191564-x86.msu /quiet`.</span></span>

> [!NOTE]
> <span data-ttu-id="22293-169">Instalaci WMF 5.1 vyžaduje restartování počítače.</span><span class="sxs-lookup"><span data-stu-id="22293-169">Installing WMF 5.1 requires a reboot.</span></span> <span data-ttu-id="22293-170">Pomocí `/quiet` možnost se restartovat systém bez upozornění.</span><span class="sxs-lookup"><span data-stu-id="22293-170">Using the `/quiet` option will reboot the system without warning.</span></span>
> <span data-ttu-id="22293-171">Použití `/norestart` možnost, aby se zabránilo restartování.</span><span class="sxs-lookup"><span data-stu-id="22293-171">Use the `/norestart` option to avoid rebooting.</span></span> <span data-ttu-id="22293-172">WMF 5.1 však nebudou nainstalovány, dokud je restartovat.</span><span class="sxs-lookup"><span data-stu-id="22293-172">However, WMF 5.1 will not be installed until you have rebooted.</span></span>
