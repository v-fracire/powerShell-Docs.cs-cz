---
title: Pro vzdálené úpravy a ladění pomocí Visual Studio Code
description: Pro vzdálené úpravy a ladění pomocí Visual Studio Code
ms.date: 08/06/2018
ms.openlocfilehash: bab1a629a7e9dafd5957cf93025abb18b8a4f326
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655503"
---
# <a name="using-visual-studio-code-for-remote-editing-and-debugging"></a><span data-ttu-id="c30e5-103">Pro vzdálené úpravy a ladění pomocí Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c30e5-103">Using Visual Studio Code for remote editing and debugging</span></span>

<span data-ttu-id="c30e5-104">Pro ty, které byly znáte ISE, si pravděpodobně pamatujete, aby bylo možné spustit `psedit file.ps1` z integrovaná Konzola pro otevření souborů – místních nebo vzdálených - pravým tlačítkem myši v prostředí ISE.</span><span class="sxs-lookup"><span data-stu-id="c30e5-104">For those of you that were familiar with the ISE, you may recall that you could run `psedit file.ps1` from the integrated console to open files - local or remote - right in the ISE.</span></span>

<span data-ttu-id="c30e5-105">Jak ukázalo se, tato funkce je také k dispozici v rozšíření prostředí PowerShell pro VSCode.</span><span class="sxs-lookup"><span data-stu-id="c30e5-105">As it turns out, this feature is also available in the PowerShell extension for VSCode.</span></span> <span data-ttu-id="c30e5-106">Tato příručka obsahuje pokyny k tomu.</span><span class="sxs-lookup"><span data-stu-id="c30e5-106">This guide will show you how to do it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c30e5-107">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="c30e5-107">Prerequisites</span></span>

<span data-ttu-id="c30e5-108">Tato příručka předpokládá, že máte:</span><span class="sxs-lookup"><span data-stu-id="c30e5-108">This guide assumes that you have:</span></span>

- <span data-ttu-id="c30e5-109">vzdálený prostředek (ex: virtuální počítač, kontejner), abyste měli přístup k</span><span class="sxs-lookup"><span data-stu-id="c30e5-109">a remote resource (ex: a VM, a container) that you have access to</span></span>
- <span data-ttu-id="c30e5-110">Powershellu spouštěné na ně a hostitelského počítače</span><span class="sxs-lookup"><span data-stu-id="c30e5-110">PowerShell running on it and the host machine</span></span>
- <span data-ttu-id="c30e5-111">VSCode a rozšíření prostředí PowerShell pro VSCode</span><span class="sxs-lookup"><span data-stu-id="c30e5-111">VSCode and the PowerShell extension for VSCode</span></span>

<span data-ttu-id="c30e5-112">Tato funkce funguje v prostředí Windows PowerShell a PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="c30e5-112">This feature works on Windows PowerShell and PowerShell Core.</span></span>

<span data-ttu-id="c30e5-113">Tato funkce funguje i při připojování ke vzdálenému počítači prostřednictvím služby WinRM, přímou službu PowerShell nebo SSH.</span><span class="sxs-lookup"><span data-stu-id="c30e5-113">This feature also works when connecting to a remote machine via WinRM, PowerShell Direct, or SSH.</span></span> <span data-ttu-id="c30e5-114">Pokud chcete použít SSH, ale používají Windows, podívejte se [Win32 verzi SSH](https://github.com/PowerShell/Win32-OpenSSH)!</span><span class="sxs-lookup"><span data-stu-id="c30e5-114">If you want to use SSH, but are using Windows, check out the [Win32 version of SSH](https://github.com/PowerShell/Win32-OpenSSH)!</span></span>

## <a name="lets-go"></a><span data-ttu-id="c30e5-115">Jdeme</span><span class="sxs-lookup"><span data-stu-id="c30e5-115">Let's go</span></span>

<span data-ttu-id="c30e5-116">V této části můžu zabývat vzdálené úpravy a ladění z mé MacBook Pro do virtuálního počítače s Ubuntu v Azure.</span><span class="sxs-lookup"><span data-stu-id="c30e5-116">In this section, I'll walk through remote editing and debugging from my MacBook Pro, to an Ubuntu VM running in Azure.</span></span> <span data-ttu-id="c30e5-117">Můžu možná nepoužívají Windows, ale **je stejný jako proces**.</span><span class="sxs-lookup"><span data-stu-id="c30e5-117">I might not be using Windows, but **the process is identical**.</span></span>

### <a name="local-file-editing-with-open-editorfile"></a><span data-ttu-id="c30e5-118">Úpravy s Open-EditorFile místního souboru</span><span class="sxs-lookup"><span data-stu-id="c30e5-118">Local file editing with Open-EditorFile</span></span>

<span data-ttu-id="c30e5-119">Díky rozšíření prostředí PowerShell pro VSCode spuštění a integrovaná konzola Powershellu otevřít, můžeme zadat `Open-EditorFile foo.ps1` nebo `psedit foo.ps1` otevřít místní foo.ps1 souboru přímo v editoru.</span><span class="sxs-lookup"><span data-stu-id="c30e5-119">With the PowerShell extension for VSCode started and the PowerShell Integrated Console opened, we can type `Open-EditorFile foo.ps1` or `psedit foo.ps1` to open the local foo.ps1 file right in the editor.</span></span>

![Otevřít EditorFile foo.ps1 funguje místně](https://user-images.githubusercontent.com/2644648/34895897-7c2c46ac-f79c-11e7-9410-a252aff52f13.png)

>[!NOTE]
> <span data-ttu-id="c30e5-121">foo.ps1 už musí existovat.</span><span class="sxs-lookup"><span data-stu-id="c30e5-121">foo.ps1 must already exist.</span></span>

<span data-ttu-id="c30e5-122">Tady můžeme:</span><span class="sxs-lookup"><span data-stu-id="c30e5-122">From there, we can:</span></span>

<span data-ttu-id="c30e5-123">přidat zarážky do mřížky ![přidání zarážky na ovládací prvek](https://user-images.githubusercontent.com/2644648/34895893-7bdc38e2-f79c-11e7-8026-8ad53f9a1bad.png)</span><span class="sxs-lookup"><span data-stu-id="c30e5-123">add breakpoints to the gutter ![adding breakpoint to gutter](https://user-images.githubusercontent.com/2644648/34895893-7bdc38e2-f79c-11e7-8026-8ad53f9a1bad.png)</span></span>

<span data-ttu-id="c30e5-124">a stisknutím klávesy F5, chcete-li ladit skript prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c30e5-124">and hit F5 to debug the PowerShell script.</span></span>
<span data-ttu-id="c30e5-125">![ladění místní skript prostředí PowerShell](https://user-images.githubusercontent.com/2644648/34895894-7bedb874-f79c-11e7-9180-7e0dc2d02af8.png)</span><span class="sxs-lookup"><span data-stu-id="c30e5-125">![debugging the PowerShell local script](https://user-images.githubusercontent.com/2644648/34895894-7bedb874-f79c-11e7-9180-7e0dc2d02af8.png)</span></span>

<span data-ttu-id="c30e5-126">Při ladění, můžete pracovat s konzolou pro ladění, podívejte se na proměnné v oboru na levé straně a všechny ostatní standardní nástroje pro ladění.</span><span class="sxs-lookup"><span data-stu-id="c30e5-126">While debugging, you can interact with the debug console, check out the variables in the scope on the left, and all the other standard debugging tools.</span></span>

### <a name="remote-file-editing-with-open-editorfile"></a><span data-ttu-id="c30e5-127">Vzdálený soubor s Open-EditorFile úpravy</span><span class="sxs-lookup"><span data-stu-id="c30e5-127">Remote file editing with Open-EditorFile</span></span>

<span data-ttu-id="c30e5-128">Teď Pojďme na vzdálený soubor, úpravy a ladění.</span><span class="sxs-lookup"><span data-stu-id="c30e5-128">Now let's get into remote file editing and debugging.</span></span> <span data-ttu-id="c30e5-129">Postup je téměř stejný, stačí jednou z věcí, musíme nejprve – zadání naše relace prostředí PowerShell ke vzdálenému serveru.</span><span class="sxs-lookup"><span data-stu-id="c30e5-129">The steps are nearly the same, there's just one thing we need to do first - enter our PowerShell session to the remote server.</span></span>

<span data-ttu-id="c30e5-130">K tomu je pro rutinu.</span><span class="sxs-lookup"><span data-stu-id="c30e5-130">There's a cmdlet for to do so.</span></span> <span data-ttu-id="c30e5-131">Je volána `Enter-PSSession`.</span><span class="sxs-lookup"><span data-stu-id="c30e5-131">It's called `Enter-PSSession`.</span></span>

<span data-ttu-id="c30e5-132">Je watered dolů vysvětlení rutiny:</span><span class="sxs-lookup"><span data-stu-id="c30e5-132">The watered down explanation of the cmdlet is:</span></span>

- <span data-ttu-id="c30e5-133">`Enter-PSSession -ComputerName foo` Spustí relaci prostřednictvím služby WinRM</span><span class="sxs-lookup"><span data-stu-id="c30e5-133">`Enter-PSSession -ComputerName foo` starts a session via WinRM</span></span>
- <span data-ttu-id="c30e5-134">`Enter-PSSession -ContainerId foo` a `Enter-PSSession -VmId foo` spuštění relace přes přímou službu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c30e5-134">`Enter-PSSession -ContainerId foo` and `Enter-PSSession -VmId foo` start a session via PowerShell Direct</span></span>
- <span data-ttu-id="c30e5-135">`Enter-PSSession -HostName foo` Spustí relaci pomocí protokolu SSH</span><span class="sxs-lookup"><span data-stu-id="c30e5-135">`Enter-PSSession -HostName foo` starts a session via SSH</span></span>

<span data-ttu-id="c30e5-136">Další informace o `Enter-PSSession`, podívejte se na webu docs [tady](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/enter-pssession?view=powershell-6).</span><span class="sxs-lookup"><span data-stu-id="c30e5-136">For more info on `Enter-PSSession`, check out the docs [here](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/enter-pssession?view=powershell-6).</span></span>

<span data-ttu-id="c30e5-137">Můžu používat SSH pro vzdálenou komunikaci od teď předvedu ze systému macOS virtuálního počítače s Ubuntu v Azure.</span><span class="sxs-lookup"><span data-stu-id="c30e5-137">I'll be using SSH for remoting since I'm going from macOS to an Ubuntu VM in Azure.</span></span>

<span data-ttu-id="c30e5-138">Nejprve v konzole integrovaného spustíme naše Enter-PSSession.</span><span class="sxs-lookup"><span data-stu-id="c30e5-138">First, in the Integrated Console, let's run our Enter-PSSession.</span></span> <span data-ttu-id="c30e5-139">Budete vědět, že jste v relaci, protože `[something]` , zobrazí se nalevo od vaší řádku.</span><span class="sxs-lookup"><span data-stu-id="c30e5-139">You'll know that you're in the session because `[something]` will show up to the left of your prompt.</span></span>

![Volání Enter-PSSession](https://user-images.githubusercontent.com/2644648/34895896-7c18e0bc-f79c-11e7-9b36-6f4bd0e9b0db.png)

<span data-ttu-id="c30e5-141">Tady můžeme udělat přesný postup jako v případě, že jsme dříve upravovali místní skript.</span><span class="sxs-lookup"><span data-stu-id="c30e5-141">From there, we can do the exact steps as if we were editing a local script.</span></span>

1. <span data-ttu-id="c30e5-142">Spustit `Open-EditorFile test.ps1` nebo `psedit test.ps1` otevřete vzdáleného `test.ps1` souboru ![Open-EditorFile test.ps1 souboru](https://user-images.githubusercontent.com/2644648/34895898-7c3e6a12-f79c-11e7-8bdf-549b591ecbcb.png)</span><span class="sxs-lookup"><span data-stu-id="c30e5-142">Run `Open-EditorFile test.ps1` or `psedit test.ps1` to open the remote `test.ps1` file ![Open-EditorFile the test.ps1 file](https://user-images.githubusercontent.com/2644648/34895898-7c3e6a12-f79c-11e7-8bdf-549b591ecbcb.png)</span></span>
2. <span data-ttu-id="c30e5-143">Upravit soubor nebo nastavit zarážky</span><span class="sxs-lookup"><span data-stu-id="c30e5-143">Edit the file/set breakpoints</span></span> ![Upravit a nastavit zarážky](https://user-images.githubusercontent.com/2644648/34895892-7bb68246-f79c-11e7-8c0a-c2121773afbb.png)
3. <span data-ttu-id="c30e5-145">Spustit ladění (F5) vzdáleného souboru</span><span class="sxs-lookup"><span data-stu-id="c30e5-145">Start debugging (F5) the remote file</span></span>

![ladění vzdáleného souboru](https://user-images.githubusercontent.com/2644648/34895895-7c040782-f79c-11e7-93ea-47724fa5c10d.png)

<span data-ttu-id="c30e5-147">To je všechno je to!</span><span class="sxs-lookup"><span data-stu-id="c30e5-147">That's all there's to it!</span></span> <span data-ttu-id="c30e5-148">Doufáme, že tento průvodce pomáhá vymazat nahoru jakékoliv otázky týkající se vzdáleného ladění a úpravy Powershellu ve VSCode.</span><span class="sxs-lookup"><span data-stu-id="c30e5-148">We hope that this guide helped clear up any questions about remote debugging and editing PowerShell in VSCode.</span></span>

<span data-ttu-id="c30e5-149">Pokud máte jakékoli problémy, neváhejte hlásit problémy [v úložišti Githubu](http://github.com/powershell/vscode-powershell).</span><span class="sxs-lookup"><span data-stu-id="c30e5-149">If you have any problems, feel free to open issues [on the GitHub repo](http://github.com/powershell/vscode-powershell).</span></span>
