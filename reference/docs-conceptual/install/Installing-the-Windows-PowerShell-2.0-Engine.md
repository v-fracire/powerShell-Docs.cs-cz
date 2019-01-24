---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Instalace jádra Windows PowerShellu 2.0
ms.assetid: 82928f2b-f96a-4ae6-a0d0-6e7b181da308
ms.openlocfilehash: b625b61b4e191402074f57ea2e942f800dbbcd53
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403792"
---
# <a name="installing-the-windows-powershell-20-engine"></a><span data-ttu-id="ffa6f-103">Instalace jádra Windows PowerShellu 2.0</span><span class="sxs-lookup"><span data-stu-id="ffa6f-103">Installing the Windows PowerShell 2.0 Engine</span></span>
<span data-ttu-id="ffa6f-104">Toto téma vysvětluje, jak nainstalovat modul Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-104">This topic explains how to install the Windows PowerShell 2.0 Engine.</span></span>

<span data-ttu-id="ffa6f-105">Windows PowerShell 3.0 je navržena jako zpětně kompatibilní s Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-105">Windows PowerShell 3.0 is designed to be backwards compatible with Windows PowerShell 2.0.</span></span> <span data-ttu-id="ffa6f-106">Rutiny, poskytovatelů, moduly snap in, moduly a skriptech psaných pro Windows PowerShell 2.0 bez jakýchkoli změn ve Windows Powershellu 3.0 a Windows PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-106">Cmdlets, providers, snap-ins, modules, and scripts written for Windows PowerShell 2.0 run unchanged in Windows PowerShell 3.0 and Windows PowerShell 4.0.</span></span> <span data-ttu-id="ffa6f-107">Nicméně z důvodu změn v zásadách aktivace modulu runtime v rozhraní Microsoft .NET Framework 4, programy hostitele prostředí Windows PowerShell, které byly napsány pro Windows PowerShell 2.0 a zkompilován s Common Language Runtime (CLR) 2.0 nelze spustit beze změny v později verze prostředí Windows PowerShell, který je kompilován s CLR 4.0.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-107">However, due to a change in the runtime activation policy in Microsoft .NET Framework 4, Windows PowerShell host programs that were written for Windows PowerShell 2.0 and compiled with Common Language Runtime (CLR) 2.0 cannot run without modification in later releases of Windows PowerShell, which is compiled with CLR 4.0.</span></span>

<span data-ttu-id="ffa6f-108">Zachování zpětné kompatibility s příkazy a hostitele programy, které jsou těmito změnami ovlivněny, moduly Windows Powershellu 2.0, Windows PowerShell 3.0 a Windows PowerShell 4.0 slouží ke spouštění vedle sebe.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-108">To maintain backward compatibility with commands and host programs that are affected by these changes, the Windows PowerShell 2.0, Windows PowerShell 3.0, and Windows PowerShell 4.0 engines are designed to run side-by-side.</span></span> <span data-ttu-id="ffa6f-109">Modul Windows PowerShell 2.0 je také součástí systému Windows Server 2012 R2, Windows 8.1, Windows 8, Windows Server 2012 a Windows Management Framework 3.0.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-109">Also, the Windows PowerShell 2.0 Engine is included in Windows Server 2012 R2, Windows 8.1, Windows 8, Windows Server 2012, and Windows Management Framework 3.0.</span></span> <span data-ttu-id="ffa6f-110">Modul Windows PowerShell 2.0 je určena pro použití pouze v případě stávajícího skriptu nebo hostitele program nelze spustit, protože není kompatibilní s Windows PowerShell 3.0, Windows PowerShell 4.0 nebo Microsoft .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-110">The Windows PowerShell 2.0 Engine is intended to be used only when an existing script or host program cannot run because it is incompatible with Windows PowerShell 3.0, Windows PowerShell 4.0, or Microsoft .NET Framework 4.</span></span> <span data-ttu-id="ffa6f-111">Očekává se, že tyto případy docházet zřídka.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-111">Such cases are expected to be rare.</span></span>

<span data-ttu-id="ffa6f-112">Modul Windows PowerShell 2.0 je volitelná funkce systému Windows Server 2012 R2, Windows 8.1, Windows® 8 a systému Windows Server® 2012.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-112">The Windows PowerShell 2.0 Engine is an optional feature of Windows Server 2012 R2, Windows 8.1, Windows® 8 and Windows Server® 2012.</span></span> <span data-ttu-id="ffa6f-113">Ve starších verzích Windows když instalujete Windows Management Framework 3.0 instalace Windows Powershellu 3.0 zcela nahrazují instalace Windows PowerShell 2.0 v adresáři instalace prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-113">On earlier versions of Windows, when you install Windows Management Framework 3.0, the Windows PowerShell 3.0 installation completely replaces the Windows PowerShell 2.0 installation in the Windows PowerShell installation directory.</span></span> <span data-ttu-id="ffa6f-114">Nicméně se uchovávají modul Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-114">However, the Windows PowerShell 2.0 Engine is retained.</span></span>

<span data-ttu-id="ffa6f-115">Informace o spuštění jádra Windows Powershellu 2.0 najdete v tématu [spuštění jádra Windows Powershellu 2.0](../getting-started/Starting-the-Windows-PowerShell-2.0-Engine.md).</span><span class="sxs-lookup"><span data-stu-id="ffa6f-115">For information about starting the Windows PowerShell 2.0 Engine, see [Starting the Windows PowerShell 2.0 Engine](../getting-started/Starting-the-Windows-PowerShell-2.0-Engine.md).</span></span>

## <a name="on-windows-81-and-windows-8"></a><span data-ttu-id="ffa6f-116">Zařízení s Windows 8.1 a Windows 8</span><span class="sxs-lookup"><span data-stu-id="ffa6f-116">On Windows 8.1 and Windows 8</span></span>
<span data-ttu-id="ffa6f-117">Na Windows 8.1 a Windows 8 je funkce jádra Windows Powershellu 2.0 ve výchozím nastavení zapnutá.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-117">On Windows 8.1 and Windows 8, the Windows PowerShell 2.0 Engine feature is turned on by default.</span></span> <span data-ttu-id="ffa6f-118">Však použít, budete muset zapnout možnost pro rozhraní Microsoft .NET Framework 3.5, který vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-118">However, to use it, you need to turn on the option for Microsoft .NET Framework 3.5, which it requires.</span></span> <span data-ttu-id="ffa6f-119">Tato část také vysvětluje, jak zapnout a vypnout funkci modul Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-119">This section also explains how to turn the Windows PowerShell 2.0 Engine feature on and off.</span></span>

#### <a name="to-turn-on-net-framework-35"></a><span data-ttu-id="ffa6f-120">Chcete-li na rozhraní .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="ffa6f-120">To turn on .NET Framework 3.5</span></span>

1. <span data-ttu-id="ffa6f-121">Na **Start** zadejte **funkce Windows**.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-121">On the **Start** screen, type **Windows Features**.</span></span>

2. <span data-ttu-id="ffa6f-122">Na **aplikace** panelu, klikněte na tlačítko **nastavení**a potom klikněte na tlačítko **Windows zapnout nebo vypnout funkce**.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-122">On the **Apps** bar, click **Settings**, and then click **Turn Windows features on or off**.</span></span>

3. <span data-ttu-id="ffa6f-123">V **funkce Windows** klikněte **rozhraní .NET Framework 3.5 (zahrnuje .NET 2.0 a 3.0** ji vyberte.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-123">In the **Windows Features** box, click **.NET Framework 3.5 (includes .NET 2.0 and 3.0** to select it.</span></span>

    <span data-ttu-id="ffa6f-124">Když vyberete **rozhraní .NET Framework 3.5 (zahrnuje .NET 2.0 a 3.0**, pole se vyplní k označení, že je vybrána pouze část funkce.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-124">When you select **.NET Framework 3.5 (includes .NET 2.0 and 3.0**, the box fills to indicate that only part of the feature is selected.</span></span> <span data-ttu-id="ffa6f-125">To je však dostatečná pro modul Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-125">However, this is sufficient for the Windows PowerShell 2.0 Engine.</span></span>

#### <a name="to-turn-the-windows-powershell-20-engine-on-and-off"></a><span data-ttu-id="ffa6f-126">K zapnutí a vypnutí modulu Windows Powershellu 2.0</span><span class="sxs-lookup"><span data-stu-id="ffa6f-126">To turn the Windows PowerShell 2.0 Engine on and off</span></span>

1. <span data-ttu-id="ffa6f-127">Na **Start** zadejte **funkce Windows**.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-127">On the **Start** screen, type **Windows Features**.</span></span>

2. <span data-ttu-id="ffa6f-128">Na **aplikace** panelu, klikněte na tlačítko **nastavení**a potom klikněte na tlačítko **Windows zapnout nebo vypnout funkce**.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-128">On the **Apps** bar, click **Settings**, and then click **Turn Windows features on or off**.</span></span>

3. <span data-ttu-id="ffa6f-129">V **funkce Windows** rozbalte **Windows PowerShell 2.0** uzel a klikněte na tlačítko **jádra Windows Powershellu 2.0** a vyberte nebo zrušte zaškrtnutí.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-129">In the **Windows Features** box, expand the **Windows PowerShell 2.0** node, and click the **Windows PowerShell 2.0 Engine** box to select or clear it.</span></span>

## <a name="on-windows-server-2012-r2-and-windows-server-2012"></a><span data-ttu-id="ffa6f-130">V systému Windows Server 2012 R2 a Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ffa6f-130">On Windows Server 2012 R2 and Windows Server 2012</span></span>
<span data-ttu-id="ffa6f-131">Pomocí následujících postupů můžete přidat modul Windows PowerShell 2.0 a funkce rozhraní Microsoft .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-131">Use the following procedures to add the Windows PowerShell 2.0 Engine and Microsoft .NET Framework 3.5 features.</span></span> <span data-ttu-id="ffa6f-132">Modul Windows PowerShell 2.0 vyžaduje rozhraní Microsoft .NET Framework 2.0.50727 minimálně.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-132">The Windows PowerShell 2.0 Engine requires Microsoft .NET Framework 2.0.50727 at a minimum.</span></span> <span data-ttu-id="ffa6f-133">Tento požadavek splněn rozhraním Microsoft .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-133">This requirement is fulfilled by Microsoft .NET Framework 3.5.</span></span>

#### <a name="to-add-the-net-framework-35-feature"></a><span data-ttu-id="ffa6f-134">Chcete-li přidat funkci rozhraní .NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="ffa6f-134">To add the .NET Framework 3.5 feature</span></span>

1. <span data-ttu-id="ffa6f-135">V **správce serveru**, z **spravovat** nabídce vyberte možnost **přidat role a funkce**.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-135">In **Server Manager**, from the **Manage** menu, select **Add Roles and Features**.</span></span>

    <span data-ttu-id="ffa6f-136">Nebo v **správce serveru**, klikněte na tlačítko **všechny servery**, klikněte pravým tlačítkem na název serveru a pak vyberte **přidat role a funkce**.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-136">Or in **Server Manager**, click **All Servers**, right-click a server name, and then select **Add Roles and Features**.</span></span>

2. <span data-ttu-id="ffa6f-137">Na **typ instalace** stránce **instalace na základě rolí nebo na základě funkcí**.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-137">On the **Installation Type** page, select **Role-based or feature-based installation**.</span></span>

3. <span data-ttu-id="ffa6f-138">Na **funkce** stránce, rozbalte **funkce rozhraní .NET Framework 3.5** uzel a vyberte možnost **rozhraní .NET Framework 3.5 (zahrnuje .NET 2.0 a 3.0)**.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-138">On the **Features** page, expand the **.NET 3.5 Framework Features** node and select **.NET Framework 3.5 (includes .NET 2.0 and 3.0)**.</span></span>

    <span data-ttu-id="ffa6f-139">Další možnosti v tomto uzlu se nevyžadují pro modul Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-139">The other options under that node are not required for the Windows PowerShell 2.0 Engine.</span></span>

#### <a name="to-add-the-windows-powershell-20-engine-feature"></a><span data-ttu-id="ffa6f-140">Chcete-li přidat funkci modul Windows Powershellu 2.0</span><span class="sxs-lookup"><span data-stu-id="ffa6f-140">To add the Windows PowerShell 2.0 Engine feature</span></span>

- <span data-ttu-id="ffa6f-141">V **správce serveru**, z **spravovat** nabídce vyberte možnost **přidat role a funkce**.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-141">In **Server Manager**, from the **Manage** menu, select **Add Roles and Features**.</span></span>

    <span data-ttu-id="ffa6f-142">Nebo **správce serveru**, klikněte na tlačítko **všechny servery**, klikněte pravým tlačítkem na název serveru a pak vyberte **přidat role a funkce**.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-142">Or **Server Manager**, click **All Servers**, right-click a server name, and then select **Add Roles and Features**.</span></span>

- <span data-ttu-id="ffa6f-143">Na **typ instalace** stránce **instalace na základě rolí nebo na základě funkcí**.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-143">On the **Installation Type** page, select **Role-based or feature-based installation**.</span></span>

- <span data-ttu-id="ffa6f-144">Na **funkce** stránce, rozbalte **prostředí Windows PowerShell (nainstalováno)** uzel a vyberte možnost **jádra Windows Powershellu 2.0**.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-144">On the **Features** page, expand the **Windows PowerShell (Installed)** node and select **Windows PowerShell 2.0 Engine**.</span></span>

<span data-ttu-id="ffa6f-145">Informace o spuštění jádra Windows Powershellu 2.0 najdete v tématu [spuštění jádra Windows Powershellu 2.0](../getting-started/Starting-the-Windows-PowerShell-2.0-Engine.md).</span><span class="sxs-lookup"><span data-stu-id="ffa6f-145">For information about starting the Windows PowerShell 2.0 Engine, see [Starting the Windows PowerShell 2.0 Engine](../getting-started/Starting-the-Windows-PowerShell-2.0-Engine.md).</span></span>

## <a name="on-earlier-systems"></a><span data-ttu-id="ffa6f-146">V předchozích verzích systému</span><span class="sxs-lookup"><span data-stu-id="ffa6f-146">On Earlier Systems</span></span>
<span data-ttu-id="ffa6f-147">[Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkID=293881) balíček, který nainstaluje Windows 7, Windows Server 2008 R2 a Windows Server 2012, Windows PowerShell 4.0 obsahuje modul Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-147">The [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkID=293881) package that installs Windows PowerShell 4.0 on Windows 7, Windows Server 2008 R2, and Windows Server 2012, includes the Windows PowerShell 2.0 Engine.</span></span> <span data-ttu-id="ffa6f-148">Modul Windows PowerShell 2.0 je aktivní a připravený k použití, v případě potřeby bez další instalace, konfigurace nebo nastavení.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-148">The Windows PowerShell 2.0 Engine is enabled and ready to use, if necessary, without additional installation, setup, or configuration.</span></span>

<span data-ttu-id="ffa6f-149">Balíček Windows Management Framework 3.0, která nainstaluje Windows 7, Windows Server 2008 R2 a Windows Server 2008, Windows PowerShell 3.0 obsahuje modul Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-149">The Windows Management Framework 3.0 package that installs Windows PowerShell 3.0 on Windows 7, Windows Server 2008 R2, and Windows Server 2008, includes the Windows PowerShell 2.0 Engine.</span></span> <span data-ttu-id="ffa6f-150">Modul Windows PowerShell 2.0 je aktivní a připravený k použití, v případě potřeby bez další instalace, konfigurace nebo nastavení.</span><span class="sxs-lookup"><span data-stu-id="ffa6f-150">The Windows PowerShell 2.0 Engine is enabled and ready to use, if necessary, without additional installation, setup, or configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="ffa6f-151">Viz také</span><span class="sxs-lookup"><span data-stu-id="ffa6f-151">See Also</span></span>
- [<span data-ttu-id="ffa6f-152">Požadavky na prostředí PowerShell systému Windows</span><span class="sxs-lookup"><span data-stu-id="ffa6f-152">Windows PowerShell System Requirements</span></span>](Windows-PowerShell-System-Requirements.md)
- [<span data-ttu-id="ffa6f-153">Instalace prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffa6f-153">Installing Windows PowerShell</span></span>](Installing-Windows-PowerShell.md)
- [<span data-ttu-id="ffa6f-154">Spuštění Windows Powershellu</span><span class="sxs-lookup"><span data-stu-id="ffa6f-154">Starting Windows PowerShell</span></span>](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)
- [<span data-ttu-id="ffa6f-155">Spuštění jádra Windows PowerShellu 2.0</span><span class="sxs-lookup"><span data-stu-id="ffa6f-155">Starting the Windows PowerShell 2.0 Engine</span></span>](../getting-started/Starting-the-Windows-PowerShell-2.0-Engine.md)