---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Systémové požadavky Windows PowerShellu
ms.assetid: 6d1d3c75-3be4-4fc9-8805-ca9b2c454d42
ms.openlocfilehash: 8850cf26b0313dfb8898ccb66b4767d695860d4c
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320733"
---
# <a name="windows-powershell-system-requirements"></a><span data-ttu-id="e7c1b-103">Systémové požadavky Windows PowerShellu</span><span class="sxs-lookup"><span data-stu-id="e7c1b-103">Windows PowerShell System Requirements</span></span>
<span data-ttu-id="e7c1b-104">Toto téma uvádí požadavky na systém pro Windows PowerShell 3.0, Windows PowerShell 4.0 a Windows Powershellu 5.0 a Windows PowerShell 5.1 a speciálních funkcí, jako je Windows PowerShell integrovaném skriptovacím prostředí (ISE), příkazů CIM, a pracovní postupy.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-104">This topic lists the system requirements for Windows PowerShell 3.0, Windows PowerShell 4.0 and Windows PowerShell 5.0, and Windows PowerShell 5.1 and for special features, such as Windows PowerShell Integrated Scripting Environment (ISE), CIM commands, and workflows.</span></span>

<span data-ttu-id="e7c1b-105">Windows® 8.1 a systému Windows Server® 2012 R2 obsahovat všechny požadované programy.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-105">Windows® 8.1 and Windows Server® 2012 R2 include all required programs.</span></span> <span data-ttu-id="e7c1b-106">Toto téma je navržená pro uživatele v dřívějších verzích Windows.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-106">This topic is designed for users of earlier releases of Windows.</span></span>

## <a name="operating-system-requirements"></a><span data-ttu-id="e7c1b-107">Požadavky na operační systém</span><span class="sxs-lookup"><span data-stu-id="e7c1b-107">Operating System Requirements</span></span>
<span data-ttu-id="e7c1b-108">Windows PowerShell 5.1 běží v následujících verzích Windows.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-108">Windows PowerShell 5.1 runs on the following versions of Windows.</span></span>

- <span data-ttu-id="e7c1b-109">Windows Server. 2019, ve výchozím nastavení nainstalovaná</span><span class="sxs-lookup"><span data-stu-id="e7c1b-109">Windows Server 2019, installed by default</span></span>

- <span data-ttu-id="e7c1b-110">Windows Server 2016 nainstalované ve výchozím nastavení</span><span class="sxs-lookup"><span data-stu-id="e7c1b-110">Windows Server 2016, installed by default</span></span>

- <span data-ttu-id="e7c1b-111">Nainstalujte Windows Server 2012 R2, [Windows Management Framework 5.1](https://aka.ms/wmf5download) spustit Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="e7c1b-111">Windows Server 2012 R2, install [Windows Management Framework 5.1](https://aka.ms/wmf5download) to run Windows PowerShell 5.1</span></span>

- <span data-ttu-id="e7c1b-112">Nainstalujte Windows Server 2012, [Windows Management Framework 5.1](https://aka.ms/wmf5download) spustit Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-112">Windows Server 2012, install [Windows Management Framework 5.1](https://aka.ms/wmf5download) to run Windows PowerShell 5.0</span></span>

- <span data-ttu-id="e7c1b-113">Nainstalujte Windows Server 2008 R2 s aktualizací Service Pack 1, [Windows Management Framework 5.1](https://aka.ms/wmf5download) spustit Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="e7c1b-113">Windows Server 2008 R2 with Service Pack 1, install [Windows Management Framework 5.1](https://aka.ms/wmf5download) to run Windows PowerShell 5.1</span></span>

- <span data-ttu-id="e7c1b-114">Windows 10 verze 1607 a až – ve výchozím nastavení nainstalovaná.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-114">Windows 10 version 1607 and up - installed by default</span></span>

- <span data-ttu-id="e7c1b-115">Nainstalujte Windows 10 verze 1507, 1511 - [Windows Management Framework 5.1](https://aka.ms/wmf5download) spustit Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="e7c1b-115">Windows 10 version 1507, 1511 - install [Windows Management Framework 5.1](https://aka.ms/wmf5download) to run Windows PowerShell 5.1</span></span>

- <span data-ttu-id="e7c1b-116">Nainstalujte Windows 8.1, [Windows Management Framework 5.1](https://aka.ms/wmf5download) spustit Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="e7c1b-116">Windows 8.1, install [Windows Management Framework 5.1](https://aka.ms/wmf5download) to run Windows PowerShell 5.1</span></span>

- <span data-ttu-id="e7c1b-117">Nainstalovat Windows 7 s aktualizací Service Pack 1, [Windows Management Framework 5.1](https://aka.ms/wmf5download) spustit Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="e7c1b-117">Windows 7 with Service Pack 1, install [Windows Management Framework 5.1](https://aka.ms/wmf5download) to run Windows PowerShell 5.1</span></span>

<span data-ttu-id="e7c1b-118">Windows PowerShell 5.0 (Superceeded pomocí Windows PowerShell 5.1) běží na následující verze systému Windows.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-118">Windows PowerShell 5.0 (Superceeded by Windows PowerShell 5.1) runs on the following versions of Windows.</span></span>

- <span data-ttu-id="e7c1b-119">Windows Server 2019 ve výchozím nastavení nainstalovaná vyšší verze</span><span class="sxs-lookup"><span data-stu-id="e7c1b-119">Windows Server 2019, higher version installed by default</span></span>

- <span data-ttu-id="e7c1b-120">Ve výchozím nastavení nainstalovaná vyšší verze Windows serveru 2016</span><span class="sxs-lookup"><span data-stu-id="e7c1b-120">Windows Server 2016, higher version installed by default</span></span>

- <span data-ttu-id="e7c1b-121">Nainstalujte Windows Server 2012 R2, [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) spustit Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-121">Windows Server 2012 R2, install [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) to run Windows PowerShell 5.0</span></span>

- <span data-ttu-id="e7c1b-122">Nainstalujte Windows Server 2012, [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) spustit Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-122">Windows Server 2012, install [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) to run Windows PowerShell 5.0</span></span>

- <span data-ttu-id="e7c1b-123">Nainstalujte Windows Server 2008 R2 s aktualizací Service Pack 1, [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) spustit Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-123">Windows Server 2008 R2 with Service Pack 1, install [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) to run Windows PowerShell 5.0</span></span>

- <span data-ttu-id="e7c1b-124">Windows 10 verze 1607 a novějšími verzemi – ve výchozím nastavení nainstalovaná vyšší verze</span><span class="sxs-lookup"><span data-stu-id="e7c1b-124">Windows 10 version 1607 and up - higher version installed by default</span></span>

- <span data-ttu-id="e7c1b-125">Windows 10 verze 1507, 1511 – ve výchozím nastavení nainstalovaná</span><span class="sxs-lookup"><span data-stu-id="e7c1b-125">Windows 10 version 1507, 1511 - installed by default</span></span>

- <span data-ttu-id="e7c1b-126">Nainstalujte Windows 8.1, [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) spustit Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-126">Windows 8.1, install [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) to run Windows PowerShell 5.0</span></span>

- <span data-ttu-id="e7c1b-127">Nainstalovat Windows 7 s aktualizací Service Pack 1, [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) spustit Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-127">Windows 7 with Service Pack 1, install [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) to run Windows PowerShell 5.0</span></span>

<span data-ttu-id="e7c1b-128">Windows PowerShell 4.0 běží v následujících verzích Windows.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-128">Windows PowerShell 4.0 runs on the following versions of Windows.</span></span>

- <span data-ttu-id="e7c1b-129">Windows 8.1, ve výchozím nastavení nainstalovaná</span><span class="sxs-lookup"><span data-stu-id="e7c1b-129">Windows 8.1, installed by default</span></span>

- <span data-ttu-id="e7c1b-130">Windows Server 2012 R2, ve výchozím nastavení nainstalovaná</span><span class="sxs-lookup"><span data-stu-id="e7c1b-130">Windows Server 2012 R2, installed by default</span></span>

- <span data-ttu-id="e7c1b-131">Nainstalujte Windows® 7 s aktualizací Service Pack 1, [Windows Management Framework 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) ke spuštění Windows Powershellu 4.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-131">Windows® 7 with Service Pack 1, install [Windows Management Framework 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) to run Windows PowerShell 4.0</span></span>

- <span data-ttu-id="e7c1b-132">Nainstalujte Windows Server® 2008 R2 s aktualizací Service Pack 1, [Windows Management Framework 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) ke spuštění Windows Powershellu 4.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-132">Windows Server® 2008 R2 with Service Pack 1, install [Windows Management Framework 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) to run Windows PowerShell 4.0</span></span>

<span data-ttu-id="e7c1b-133">Windows PowerShell 3.0 se spouští na následující verze systému Windows.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-133">Windows PowerShell 3.0 runs on the following versions of Windows.</span></span>

- <span data-ttu-id="e7c1b-134">Windows 8 nainstalované ve výchozím nastavení</span><span class="sxs-lookup"><span data-stu-id="e7c1b-134">Windows 8, installed by default</span></span>

- <span data-ttu-id="e7c1b-135">Windows Server 2012, ve výchozím nastavení nainstalovaná</span><span class="sxs-lookup"><span data-stu-id="e7c1b-135">Windows Server 2012, installed by default</span></span>

- <span data-ttu-id="e7c1b-136">Nainstalujte Windows® 7 s aktualizací Service Pack 1, [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) spustit Windows PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-136">Windows® 7 with Service Pack 1, install [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) to run Windows PowerShell 3.0</span></span>

- <span data-ttu-id="e7c1b-137">Nainstalujte Windows Server® 2008 R2 s aktualizací Service Pack 1, [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) spustit Windows PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-137">Windows Server® 2008 R2 with Service Pack 1, install [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) to run Windows PowerShell 3.0</span></span>

- <span data-ttu-id="e7c1b-138">Nainstalujte Windows Server 2008 s aktualizací Service Pack 2, [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) spustit Windows PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-138">Windows Server 2008 with Service Pack 2, install [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) to run Windows PowerShell 3.0</span></span>

## <a name="microsoft-net-framework-requirements"></a><span data-ttu-id="e7c1b-139">Požadavky na rozhraní Microsoft .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e7c1b-139">Microsoft .NET Framework Requirements</span></span>
<span data-ttu-id="e7c1b-140">Windows PowerShell 5.1 vyžaduje úplnou instalaci rozhraní Microsoft .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-140">Windows PowerShell 5.1 requires the full installation of Microsoft .NET Framework 4.5.</span></span> <span data-ttu-id="e7c1b-141">Windows 8.1 a Windows Server 2012 R2 zahrnout rozhraní Microsoft .NET Framework 4.5 ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-141">Windows 8.1 and Windows Server 2012 R2 include Microsoft .NET Framework 4.5 by default.</span></span>

<span data-ttu-id="e7c1b-142">Windows PowerShell 5.0 vyžaduje úplnou instalaci rozhraní Microsoft .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-142">Windows PowerShell 5.0 requires the full installation of Microsoft .NET Framework 4.5.</span></span> <span data-ttu-id="e7c1b-143">Windows 8.1 a Windows Server 2012 R2 zahrnout rozhraní Microsoft .NET Framework 4.5 ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-143">Windows 8.1 and Windows Server 2012 R2 include Microsoft .NET Framework 4.5 by default.</span></span>

<span data-ttu-id="e7c1b-144">Windows PowerShell 4.0 vyžaduje úplnou instalaci rozhraní Microsoft .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-144">Windows PowerShell 4.0 requires the full installation of Microsoft .NET Framework 4.5.</span></span> <span data-ttu-id="e7c1b-145">Windows 8.1 a Windows Server 2012 R2 zahrnout rozhraní Microsoft .NET Framework 4.5 ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-145">Windows 8.1 and Windows Server 2012 R2 include Microsoft .NET Framework 4.5 by default.</span></span>

<span data-ttu-id="e7c1b-146">Windows PowerShell 3.0 vyžaduje úplnou instalaci rozhraní Microsoft .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-146">Windows PowerShell 3.0 requires the full installation of Microsoft .NET Framework 4.</span></span> <span data-ttu-id="e7c1b-147">Windows 8 a Windows Server 2012 zahrnují rozhraní Microsoft .NET Framework 4.5 ve výchozím nastavení, která splňuje tento požadavek.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-147">Windows 8 and Windows Server 2012 include Microsoft .NET Framework 4.5 by default, which fulfills this requirement.</span></span>

<span data-ttu-id="e7c1b-148">Pokud chcete nainstalovat rozhraní Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe), najdete v článku [rozhraní Microsoft .NET Framework 4.5](https://go.microsoft.com/fwlink/?LinkID=242919) na webu Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-148">To install Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe), see [Microsoft .NET Framework 4.5](https://go.microsoft.com/fwlink/?LinkID=242919) on the Microsoft Download Center.</span></span>

<span data-ttu-id="e7c1b-149">Pokud chcete nainstalovat úplnou instalaci rozhraní Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe), najdete v článku [rozhraní Microsoft .NET Framework 4 (Webová instalační služba)](https://go.microsoft.com/fwlink/?LinkID=212931) na webu Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-149">To install the full installation of Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe), see [Microsoft .NET Framework 4 (Web Installer)](https://go.microsoft.com/fwlink/?LinkID=212931) on the Microsoft Download Center.</span></span>

## <a name="windows-management-framework-40"></a><span data-ttu-id="e7c1b-150">Windows Management Framework 4.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-150">Windows Management Framework 4.0</span></span>
<span data-ttu-id="e7c1b-151">Vyžaduje Windows Management Framework 4.0 na předinstalován v systému Windows Server 2008 R2 SP1 a Windows 7 SP1, Windows PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-151">Windows PowerShell 5.0 requires Windows Management Framework 4.0 to be preinstalled on Windows Server 2008 R2 SP1 and Windows 7 SP1.</span></span>

## <a name="ws-management-30"></a><span data-ttu-id="e7c1b-152">WS-Management 3.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-152">WS-Management 3.0</span></span>
<span data-ttu-id="e7c1b-153">Windows PowerShell 3.0 a Windows PowerShell 4.0 vyžadují 3.0 WS-Management, která podporuje službu WinRM a protokolu WSMan.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-153">Windows PowerShell 3.0 and Windows PowerShell 4.0 require WS-Management 3.0, which supports the WinRM service and WSMan protocol.</span></span> <span data-ttu-id="e7c1b-154">Tento program je součástí Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows Management Framework 4.0 a Windows Management Framework 3.0.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-154">This program is included in Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows Management Framework 4.0, and Windows Management Framework 3.0.</span></span>

## <a name="windows-management-instrumentation-30"></a><span data-ttu-id="e7c1b-155">Windows Management Instrumentation 3.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-155">Windows Management Instrumentation 3.0</span></span>
<span data-ttu-id="e7c1b-156">Windows PowerShell 3.0 a Windows PowerShell 4.0 vyžadují Windows Management Instrumentation 3.0 (WMI).</span><span class="sxs-lookup"><span data-stu-id="e7c1b-156">Windows PowerShell 3.0 and Windows PowerShell 4.0 require Windows Management Instrumentation 3.0 (WMI).</span></span> <span data-ttu-id="e7c1b-157">Tento program je součástí Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows Management Framework 4.0 a Windows Management Framework 3.0.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-157">This program is included in Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows Management Framework 4.0, and Windows Management Framework 3.0.</span></span> <span data-ttu-id="e7c1b-158">Pokud tento program není nainstalovaná na počítači, funkce, které vyžadují rozhraní WMI, jako je například příkazů CIM, se nespustí.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-158">If this program is not installed on the computer, features that require WMI, such as CIM commands, do not run.</span></span>

## <a name="common-language-runtime-40"></a><span data-ttu-id="e7c1b-159">Modul Common Language Runtime 4.0</span><span class="sxs-lookup"><span data-stu-id="e7c1b-159">Common Language Runtime 4.0</span></span>
<span data-ttu-id="e7c1b-160">Windows PowerShell 3.0, Windows PowerShell 4.0 a Windows Powershellu 5.0 se kompilují proti Common Language Runtime (CLR) 4.0.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-160">Windows PowerShell 3.0, Windows PowerShell 4.0, and Windows PowerShell 5.0 are compiled against Common Language Runtime (CLR) 4.0.</span></span>

## <a name="graphical-user-interface-requirements"></a><span data-ttu-id="e7c1b-161">Požadavky na grafickém uživatelském rozhraní</span><span class="sxs-lookup"><span data-stu-id="e7c1b-161">Graphical User Interface Requirements</span></span>
<span data-ttu-id="e7c1b-162">Prostředí Windows PowerShell je konzolové aplikace, která nevyžaduje grafické uživatelské rozhraní.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-162">Windows PowerShell is a console-based application that does not require a graphical user interface.</span></span> <span data-ttu-id="e7c1b-163">V důsledku toho je je vhodná pro počítače, které nemají obrazovky nebo monitorů nebo uživatelské rozhraní, jako jsou možnosti instalace jádra serveru systému Windows Server 2012 R2 nebo Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-163">As such, is it well suited to computers that do not have screens or monitors, or a user interface, such as the Server Core installation options of Windows Server 2012 R2 or Windows Server 2012.</span></span>

<span data-ttu-id="e7c1b-164">Vyžadují grafické uživatelské rozhraní, ale některé položky, jako je následující.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-164">However, some items, such as the following, require a graphical user interface.</span></span> <span data-ttu-id="e7c1b-165">Podrobnosti najdete v tématu nápovědy pro každou položku.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-165">For details, see the help topic for each item.</span></span>

- <span data-ttu-id="e7c1b-166">Integrované skriptovací prostředí (ISE) v prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7c1b-166">Windows PowerShell Integrated Scripting Environment (ISE)</span></span>

- <span data-ttu-id="e7c1b-167">Rutina</span><span class="sxs-lookup"><span data-stu-id="e7c1b-167">Cmdlets</span></span>

    1.  [<span data-ttu-id="e7c1b-168">Out – GridView</span><span class="sxs-lookup"><span data-stu-id="e7c1b-168">Out-GridView</span></span>](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/out-gridview)

    2.  [<span data-ttu-id="e7c1b-169">Show-– příkaz</span><span class="sxs-lookup"><span data-stu-id="e7c1b-169">Show-Command</span></span>](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Utility/Show-Command)

    3.  [<span data-ttu-id="e7c1b-170">Show ControlPanelItem</span><span class="sxs-lookup"><span data-stu-id="e7c1b-170">Show-ControlPanelItem</span></span>](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Management/Show-ControlPanelItem)

    4.  [<span data-ttu-id="e7c1b-171">Zobrazit protokol událostí</span><span class="sxs-lookup"><span data-stu-id="e7c1b-171">Show-EventLog</span></span>](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Management/Show-EventLog)

- <span data-ttu-id="e7c1b-172">Parameters</span><span class="sxs-lookup"><span data-stu-id="e7c1b-172">Parameters</span></span>

    1.  <span data-ttu-id="e7c1b-173">**ShowWindow** parametr [Get-Help](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Get-Help) rutiny.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-173">**ShowWindow** parameter of the [Get-Help](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Get-Help) cmdlet.</span></span>

    2.  <span data-ttu-id="e7c1b-174">**ShowSecurityDescriptorUI** parametr [Register-PSSessionConfiguration](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Register-PSSessionConfiguration) a [Set-PSSessionConfiguration](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Set-PSSessionConfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-174">**ShowSecurityDescriptorUI** parameter of the [Register-PSSessionConfiguration](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Register-PSSessionConfiguration) and [Set-PSSessionConfiguration](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Set-PSSessionConfiguration) cmdlets.</span></span>

## <a name="windows-powershell-engine-requirements"></a><span data-ttu-id="e7c1b-175">Požadavky Windows Powershellu modul</span><span class="sxs-lookup"><span data-stu-id="e7c1b-175">Windows PowerShell Engine Requirements</span></span>
<span data-ttu-id="e7c1b-176">Windows PowerShell 4.0 je navržena jako zpětně kompatibilní s Windows PowerShell 3.0 a Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-176">Windows PowerShell 4.0 is designed to be backwards compatible with Windows PowerShell 3.0 and Windows PowerShell 2.0.</span></span> <span data-ttu-id="e7c1b-177">Rutiny, poskytovatelů, moduly snap in, moduly a skriptech psaných pro Windows PowerShell 2.0 a Windows PowerShell 3.0 bez jakýchkoli změn ve Windows Powershellu 4.0.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-177">Cmdlets, providers, snap-ins, modules, and scripts written for Windows PowerShell 2.0 and Windows PowerShell 3.0 run unchanged in Windows PowerShell 4.0.</span></span>

<span data-ttu-id="e7c1b-178">Z důvodu změn v zásadách aktivace modulu runtime v rozhraní Microsoft .NET Framework 4, ale programy hostitele prostředí Windows PowerShell, které byly napsány pro Windows PowerShell 2.0 a zkompilován s Common Language Runtime (CLR) 2.0 nelze spustit bez jakýchkoli úprav ve Windows Prostředí PowerShell 3.0, který je kompilován s CLR 4.0.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-178">However, due to a change in the runtime activation policy in Microsoft .NET Framework 4, Windows PowerShell host programs that were written for Windows PowerShell 2.0 and compiled with Common Language Runtime (CLR) 2.0 cannot run without modification in Windows PowerShell 3.0, which is compiled with CLR 4.0.</span></span>

<span data-ttu-id="e7c1b-179">Modul Windows PowerShell 2.0 vyžaduje rozhraní Microsoft .NET Framework 2.0.50727 minimálně.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-179">The Windows PowerShell 2.0 engine requires Microsoft .NET Framework 2.0.50727 at a minimum.</span></span> <span data-ttu-id="e7c1b-180">Tento požadavek je pracující na rozhraní Microsoft .NET Framework 3.5 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-180">This requirement is fulfilled by Microsoft .NET Framework 3.5 Service Pack 1.</span></span> <span data-ttu-id="e7c1b-181">Tento požadavek není splněn pomocí rozhraní Microsoft .NET Framework 4 a novější verze rozhraní Microsoft .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-181">This requirement is not fulfilled by Microsoft .NET Framework 4 and later releases of Microsoft .NET Framework.</span></span>

<span data-ttu-id="e7c1b-182">Informace o přidání nebo instalace jádra Windows Powershellu 2.0 a přidání nebo instalaci požadované verze rozhraní Microsoft .NET Framework najdete v tématu [instalace jádra Windows Powershellu 2.0](Installing-the-Windows-PowerShell-2.0-Engine.md).</span><span class="sxs-lookup"><span data-stu-id="e7c1b-182">For information about adding or installing the Windows PowerShell 2.0 engine, and adding or installing the required versions of the Microsoft .NET Framework, see [Installing the Windows PowerShell 2.0 Engine](Installing-the-Windows-PowerShell-2.0-Engine.md).</span></span> <span data-ttu-id="e7c1b-183">Informace o spuštění jádra Windows PowerShell 2.0 naleznete v tématu [spuštění jádra Windows Powershellu 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md).</span><span class="sxs-lookup"><span data-stu-id="e7c1b-183">For information about starting the Windows PowerShell 2.0 engine, see [Starting the Windows PowerShell 2.0 Engine](Starting-the-Windows-PowerShell-2.0-Engine.md).</span></span>

## <a name="windows-preinstallation-environment"></a><span data-ttu-id="e7c1b-184">Předinstalační prostředí systému Windows</span><span class="sxs-lookup"><span data-stu-id="e7c1b-184">Windows Preinstallation Environment</span></span>
<span data-ttu-id="e7c1b-185">Windows PowerShell 2.0, Windows PowerShell 3.0 a 4.0 Windows PowerShell spusťte v prostředí Windows Preinstallation Environment (Windows PE).</span><span class="sxs-lookup"><span data-stu-id="e7c1b-185">Windows PowerShell 2.0, Windows PowerShell 3.0, and Windows PowerShell 4.0 run in the Windows Preinstallation Environment (Windows PE).</span></span> <span data-ttu-id="e7c1b-186">Tyto rutiny ale podporované nejsou.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-186">However, the following cmdlets are not supported.</span></span>

- [<span data-ttu-id="e7c1b-187">Rutiny Background Intelligent Transfer Service (BITS)</span><span class="sxs-lookup"><span data-stu-id="e7c1b-187">Background Intelligent Transfer Service (BITS) Cmdlets</span></span>](https://go.microsoft.com/fwlink/?LinkId=257514)

- [<span data-ttu-id="e7c1b-188">Get-EventLog</span><span class="sxs-lookup"><span data-stu-id="e7c1b-188">Get-EventLog</span></span>](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Management/Get-EventLog)

- [<span data-ttu-id="e7c1b-189">Get-WinEvent</span><span class="sxs-lookup"><span data-stu-id="e7c1b-189">Get-WinEvent</span></span>](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent)

- [<span data-ttu-id="e7c1b-190">Save-Help</span><span class="sxs-lookup"><span data-stu-id="e7c1b-190">Save-Help</span></span>](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Save-Help)

- [<span data-ttu-id="e7c1b-191">Update-Help</span><span class="sxs-lookup"><span data-stu-id="e7c1b-191">Update-Help</span></span>](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Update-Help)

<span data-ttu-id="e7c1b-192">Také **WinRM** služba není k dispozici v prostředí Windows PE.</span><span class="sxs-lookup"><span data-stu-id="e7c1b-192">Also, the **WinRM** service is not present on Windows PE.</span></span>

## <a name="see-also"></a><span data-ttu-id="e7c1b-193">Viz také</span><span class="sxs-lookup"><span data-stu-id="e7c1b-193">See Also</span></span>
- [<span data-ttu-id="e7c1b-194">Začínáme s prostředím Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7c1b-194">Getting Started with Windows PowerShell</span></span>](../getting-started/Getting-Started-with-Windows-PowerShell.md)
- [<span data-ttu-id="e7c1b-195">Instalace prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7c1b-195">Installing Windows PowerShell</span></span>](Installing-Windows-PowerShell.md)
- [<span data-ttu-id="e7c1b-196">Spuštění Windows Powershellu</span><span class="sxs-lookup"><span data-stu-id="e7c1b-196">Starting Windows PowerShell</span></span>](Starting-Windows-PowerShell.md)
