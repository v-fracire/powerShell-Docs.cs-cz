---
ms.date: 06/12/2017
keywords: jea, prostředí powershell, zabezpečení
title: JEA požadavky
ms.openlocfilehash: a5cf5519b30b24d44c12bdeedcf4cd763e2edbde
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189767"
---
# <a name="prerequisites"></a><span data-ttu-id="74429-103">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="74429-103">Prerequisites</span></span>

> <span data-ttu-id="74429-104">Platí pro: prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="74429-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="74429-105">Právě dostatečně správy je funkce modulu pomocí prostředí Windows PowerShell 5.0 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="74429-105">Just Enough Administration is a feature included with Windows PowerShell 5.0 and higher.</span></span>
<span data-ttu-id="74429-106">Toto téma popisuje požadavky, které je nutné splnit, aby bylo možné začít používat JEA.</span><span class="sxs-lookup"><span data-stu-id="74429-106">This topic describes the prerequisites that must be satisfied in order to start using JEA.</span></span>

## <a name="install-jea"></a><span data-ttu-id="74429-107">Nainstalujte JEA</span><span class="sxs-lookup"><span data-stu-id="74429-107">Install JEA</span></span>

<span data-ttu-id="74429-108">JEA je k dispozici v prostředí Windows PowerShell 5.0 a vyšší, ale pro plnou funkčnost se doporučuje nainstalovat nejnovější verzi prostředí PowerShell, které jsou k dispozici pro váš systém.</span><span class="sxs-lookup"><span data-stu-id="74429-108">JEA is available with Windows PowerShell 5.0 and higher, but for full functionality it is recommended that you install the latest version of PowerShell available for your system.</span></span>
<span data-ttu-id="74429-109">Následující tabulka popisuje dostupnost JEA je v systému Windows Server:</span><span class="sxs-lookup"><span data-stu-id="74429-109">The following table describes JEA's availability on Windows Server:</span></span>

<span data-ttu-id="74429-110">Serverový operační systém</span><span class="sxs-lookup"><span data-stu-id="74429-110">Server Operating System</span></span>   | <span data-ttu-id="74429-111">JEA dostupnosti</span><span class="sxs-lookup"><span data-stu-id="74429-111">JEA Availability</span></span>
--------------------------|--------------------------------
<span data-ttu-id="74429-112">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="74429-112">Windows Server 2016</span></span>       | <span data-ttu-id="74429-113">Předinstalována</span><span class="sxs-lookup"><span data-stu-id="74429-113">Preinstalled</span></span>
<span data-ttu-id="74429-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="74429-114">Windows Server 2012 R2</span></span>    | <span data-ttu-id="74429-115">Plnou funkčnost služby WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="74429-115">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="74429-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="74429-116">Windows Server 2012</span></span>       | <span data-ttu-id="74429-117">Plnou funkčnost služby WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="74429-117">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="74429-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="74429-118">Windows Server 2008 R2</span></span>    | <span data-ttu-id="74429-119">Snížená funkce<sup>1</sup> s WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="74429-119">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>

<span data-ttu-id="74429-120">Můžete taky JEA v počítači domácí nebo pracovní:</span><span class="sxs-lookup"><span data-stu-id="74429-120">You can also use JEA on your home or work computer:</span></span>

<span data-ttu-id="74429-121">Klientský operační systém</span><span class="sxs-lookup"><span data-stu-id="74429-121">Client Operating System</span></span>   | <span data-ttu-id="74429-122">JEA dostupnosti</span><span class="sxs-lookup"><span data-stu-id="74429-122">JEA Availability</span></span>
--------------------------|-----------------------------------------------------
<span data-ttu-id="74429-123">Windows 10 1607+</span><span class="sxs-lookup"><span data-stu-id="74429-123">Windows 10 1607+</span></span>          | <span data-ttu-id="74429-124">Předinstalována</span><span class="sxs-lookup"><span data-stu-id="74429-124">Preinstalled</span></span>
<span data-ttu-id="74429-125">Windows 10 1603, 1511</span><span class="sxs-lookup"><span data-stu-id="74429-125">Windows 10 1603, 1511</span></span>     | <span data-ttu-id="74429-126">Předinstalována, se snižuje funkce<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="74429-126">Preinstalled, with reduced functionality<sup>2</sup></span></span>
<span data-ttu-id="74429-127">Windows 10 1507</span><span class="sxs-lookup"><span data-stu-id="74429-127">Windows 10 1507</span></span>           | <span data-ttu-id="74429-128">Nedostupné</span><span class="sxs-lookup"><span data-stu-id="74429-128">Not available</span></span>
<span data-ttu-id="74429-129">Windows 8, 8.1</span><span class="sxs-lookup"><span data-stu-id="74429-129">Windows 8, 8.1</span></span>            | <span data-ttu-id="74429-130">Plnou funkčnost služby WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="74429-130">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="74429-131">Windows 7</span><span class="sxs-lookup"><span data-stu-id="74429-131">Windows 7</span></span>                 | <span data-ttu-id="74429-132">Snížená funkce<sup>1</sup> s WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="74429-132">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>

<span data-ttu-id="74429-133"><sup>1</sup> JEA nedá nakonfigurovat na použití skupinové účty spravované služby v systému Windows Server 2008 R2 nebo Windows 7.</span><span class="sxs-lookup"><span data-stu-id="74429-133"><sup>1</sup> JEA cannot be configured to use group managed service accounts on Windows Server 2008 R2 or Windows 7.</span></span>
<span data-ttu-id="74429-134">Virtuální účty a další funkce JEA *jsou* podporována.</span><span class="sxs-lookup"><span data-stu-id="74429-134">Virtual accounts and other JEA features *are* supported.</span></span>

<span data-ttu-id="74429-135"><sup>2</sup> Windows 10 verze 1511 a 1603 nepodporují následující funkce JEA: spuštěna jako skupinu spravovaný účet služby, pravidla podmíněného přístupu v konfigurace relace, jednotky uživatele a přidělit přístup k místní uživatelské účty.</span><span class="sxs-lookup"><span data-stu-id="74429-135"><sup>2</sup> Windows 10 versions 1511 and 1603 do not support the following JEA features: running as a group managed service account, conditional access rules in session configurations, the user drive, and granting access to local user accounts.</span></span>
<span data-ttu-id="74429-136">Získat podporu pro tyto funkce, aktualizujte Windows verze 1607 (výročí aktualizace) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="74429-136">To get support for these features, update Windows to version 1607 (Anniversary Update) or higher.</span></span>

### <a name="check-which-version-of-powershell-is-installed"></a><span data-ttu-id="74429-137">Zkontrolujte nainstalované verze prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="74429-137">Check which version of PowerShell is installed</span></span>

<span data-ttu-id="74429-138">Chcete-li zkontrolovat, která verze prostředí PowerShell je nainstalovaná ve vašem systému, zkontrolujte `$PSVersionTable` proměnné v řádku prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74429-138">To check which version of PowerShell is installed on your system, check the `$PSVersionTable` variable in a Windows PowerShell prompt.</span></span>

```powershell
PS C:\> $PSVersionTable.PSVersion

Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

<span data-ttu-id="74429-139">Budete chtít použít JEA, pokud *hlavní* verze je rovna nebo větší než **5**.</span><span class="sxs-lookup"><span data-stu-id="74429-139">You are ready to use JEA if the *Major* version is equal to or greater than **5**.</span></span>
<span data-ttu-id="74429-140">Pro dosažení co nejlepších výsledků a získat přístup k nejnovějším funkcím, doporučuje se upgradovat na verzi prostředí PowerShell **5.1** Pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="74429-140">For the best experience, and to have access to all the latest features, it is recommended that you upgrade to PowerShell version **5.1** when possible.</span></span>

### <a name="install-windows-management-framework"></a><span data-ttu-id="74429-141">Nainstalovat Windows Management Framework</span><span class="sxs-lookup"><span data-stu-id="74429-141">Install Windows Management Framework</span></span>

<span data-ttu-id="74429-142">Pokud používáte starší verzi prostředí PowerShell, budete muset aktualizovat systém s nejnovější aktualizace služby Windows Management Framework (WMF).</span><span class="sxs-lookup"><span data-stu-id="74429-142">If you are running an older version of PowerShell, you will need to update your system with the latest Windows Management Framework (WMF) update.</span></span>
<span data-ttu-id="74429-143">Balíčky aktualizací a odkaz na nejnovější poznámky k verzi WMF jsou k dispozici v [Download Center](https://aka.ms/WMF5).</span><span class="sxs-lookup"><span data-stu-id="74429-143">Update packages and a link to the latest WMF release notes are available in the [Download Center](https://aka.ms/WMF5).</span></span>

<span data-ttu-id="74429-144">Důrazně doporučujeme, abyste otestovali vaše úlohy kompatibilitu s WMF před upgradem všech vašich serverů.</span><span class="sxs-lookup"><span data-stu-id="74429-144">It is strongly recommended that you test your workload's compatibility with WMF before upgrading all of your servers.</span></span>

<span data-ttu-id="74429-145">Uživatelé Windows 10 měli nainstalovat nejnovější aktualizace funkcí na aktuální verzi prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74429-145">Windows 10 users should install the latest feature updates to obtain the current version of Windows PowerShell.</span></span>

## <a name="enable-powershell-remoting"></a><span data-ttu-id="74429-146">Povolit vzdálenou komunikaci prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="74429-146">Enable PowerShell Remoting</span></span>

<span data-ttu-id="74429-147">Vzdálená komunikace prostředí PowerShell poskytuje základ, na kterém je vytvořené JEA.</span><span class="sxs-lookup"><span data-stu-id="74429-147">PowerShell Remoting provides the foundation on which JEA is built.</span></span>
<span data-ttu-id="74429-148">Je proto nutné zajistit povolena vzdálená komunikace PowerShell a [správně zabezpečené](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity) ve vašem systému, než budete moci použít JEA.</span><span class="sxs-lookup"><span data-stu-id="74429-148">It is therefore necessary to ensure PowerShell Remoting is enabled and [properly secured](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity) on your system before you can use JEA.</span></span>

<span data-ttu-id="74429-149">Ve výchozím nastavení v systému Windows Server 2012, 2012 R2 a 2016 je povolena vzdálená komunikace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74429-149">PowerShell Remoting is enabled by default on Windows Server 2012, 2012 R2, and 2016.</span></span>
<span data-ttu-id="74429-150">Můžete povolit vzdálenou komunikaci prostředí PowerShell spuštěním následujícího příkazu v okně Powershellu se zvýšenými oprávněními.</span><span class="sxs-lookup"><span data-stu-id="74429-150">You can enable PowerShell Remoting by running the following command in an elevated PowerShell window.</span></span>

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a><span data-ttu-id="74429-151">Povolit modul prostředí PowerShell a protokolování bloku skriptu (volitelné)</span><span class="sxs-lookup"><span data-stu-id="74429-151">Enable PowerShell module and script block logging (optional)</span></span>

<span data-ttu-id="74429-152">Následující postup povolení protokolování pro všechny akce prostředí PowerShell v systému.</span><span class="sxs-lookup"><span data-stu-id="74429-152">The following steps enable logging for all PowerShell actions on your system.</span></span>
<span data-ttu-id="74429-153">Protokolování modulu PowerShell není vyžadován pro JEA, ale důrazně doporučujeme zapnout je zajistit, že uživatelé příkazy spouštět se protokolují v centrálním umístění.</span><span class="sxs-lookup"><span data-stu-id="74429-153">PowerShell Module Logging is not required for JEA, however it is strongly recommended that you turn it on to ensure the commands users run are logged in a central location.</span></span>

<span data-ttu-id="74429-154">Můžete nakonfigurovat pomocí zásad skupiny Zásady protokolování modulu prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74429-154">You can configure the PowerShell Module Logging policy using Group Policy.</span></span>

1. <span data-ttu-id="74429-155">Otevřete Editor místních zásad skupiny na pracovní stanici nebo objektu zásad skupiny v konzole pro správu zásad skupiny na řadič domény služby Active Directory</span><span class="sxs-lookup"><span data-stu-id="74429-155">Open the Local Group Policy Editor on a workstation or a Group Policy Object in the Group Policy Management Console on an Active Directory Domain Controller</span></span>
2. <span data-ttu-id="74429-156">Přejděte na **konfigurace počítače\\šablony pro správu\\součásti systému Windows\\prostředí Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="74429-156">Navigate to **Computer Configuration\\Administrative Templates\\Windows Components\\Windows PowerShell**</span></span>
3. <span data-ttu-id="74429-157">Dvakrát klikněte na **zapnout protokolování modulu**</span><span class="sxs-lookup"><span data-stu-id="74429-157">Double click on **Turn on Module Logging**</span></span>
4. <span data-ttu-id="74429-158">Klikněte na tlačítko **povoleno**</span><span class="sxs-lookup"><span data-stu-id="74429-158">Click **Enabled**</span></span>
5. <span data-ttu-id="74429-159">V části možnosti klikněte na **zobrazit** vedle názvy modulů</span><span class="sxs-lookup"><span data-stu-id="74429-159">In the Options section, click on **Show** next to Module Names</span></span>
6. <span data-ttu-id="74429-160">Typ "**\***" v zobrazeném okně.</span><span class="sxs-lookup"><span data-stu-id="74429-160">Type "**\***" in the pop up window.</span></span> <span data-ttu-id="74429-161">Tím se nastaví prostředí PowerShell k protokolování příkazy ze všech modulů.</span><span class="sxs-lookup"><span data-stu-id="74429-161">This instructs PowerShell to log commands from all modules.</span></span>
7. <span data-ttu-id="74429-162">Klikněte na tlačítko **OK** nastavit zásady</span><span class="sxs-lookup"><span data-stu-id="74429-162">Click **OK** to set the policy</span></span>
8. <span data-ttu-id="74429-163">Dvakrát klikněte na **zapnout protokolování bloku skriptu prostředí PowerShell**</span><span class="sxs-lookup"><span data-stu-id="74429-163">Double click on **Turn on PowerShell Script Block Logging**</span></span>
9. <span data-ttu-id="74429-164">Klikněte na tlačítko **povoleno**</span><span class="sxs-lookup"><span data-stu-id="74429-164">Click **Enabled**</span></span>
10. <span data-ttu-id="74429-165">Klikněte na tlačítko **OK** nastavit zásady</span><span class="sxs-lookup"><span data-stu-id="74429-165">Click **OK** to set the policy</span></span>
11. <span data-ttu-id="74429-166">(Na připojený k doméně počítače pouze) Spustit **gpupdate** nebo počkejte na zpracování aktualizované zásady a použít nastavení zásad skupiny</span><span class="sxs-lookup"><span data-stu-id="74429-166">(On domain-joined machines only) Run **gpupdate** or wait for Group Policy to process the updated policy and apply the settings</span></span>

<span data-ttu-id="74429-167">Můžete také povolit systémového prostředí PowerShell přepis prostřednictvím zásad skupiny.</span><span class="sxs-lookup"><span data-stu-id="74429-167">You can also enable system-wide PowerShell transcription through Group Policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74429-168">Další kroky</span><span class="sxs-lookup"><span data-stu-id="74429-168">Next steps</span></span>

- [<span data-ttu-id="74429-169">Vytvořte soubor schopnosti role</span><span class="sxs-lookup"><span data-stu-id="74429-169">Create a role capability file</span></span>](role-capabilities.md)
- [<span data-ttu-id="74429-170">Vytvoření konfiguračního souboru relace</span><span class="sxs-lookup"><span data-stu-id="74429-170">Create a session configuration file</span></span>](session-configurations.md)

## <a name="see-also"></a><span data-ttu-id="74429-171">Viz taky</span><span class="sxs-lookup"><span data-stu-id="74429-171">See also</span></span>

- [<span data-ttu-id="74429-172">Další informace o zabezpečení vzdálenou komunikaci prostředí PowerShell a WinRM</span><span class="sxs-lookup"><span data-stu-id="74429-172">Additional information about PowerShell Remoting and WinRM security</span></span>](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity)
- [<span data-ttu-id="74429-173">*Prostředí PowerShell ♥ týmem Blue* příspěvku na blogu na zabezpečení</span><span class="sxs-lookup"><span data-stu-id="74429-173">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)