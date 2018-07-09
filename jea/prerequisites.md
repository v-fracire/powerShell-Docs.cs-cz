---
ms.date: 06/12/2017
keywords: jea, powershell, zabezpečení
title: Požadavky na funkce JEA
ms.openlocfilehash: acc16c0c7eec357b621c0706a66b8752ae5578cd
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893031"
---
# <a name="prerequisites"></a><span data-ttu-id="e6380-103">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="e6380-103">Prerequisites</span></span>

> <span data-ttu-id="e6380-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e6380-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="e6380-105">Just Enough Administration je funkce zahrnuté pomocí Windows Powershellu 5.0 a vyšším.</span><span class="sxs-lookup"><span data-stu-id="e6380-105">Just Enough Administration is a feature included with Windows PowerShell 5.0 and higher.</span></span>
<span data-ttu-id="e6380-106">Toto téma popisuje požadavky, které musí být splněny, aby bylo možné začít používat funkce JEA.</span><span class="sxs-lookup"><span data-stu-id="e6380-106">This topic describes the prerequisites that must be satisfied in order to start using JEA.</span></span>

## <a name="install-jea"></a><span data-ttu-id="e6380-107">Instalace funkce JEA</span><span class="sxs-lookup"><span data-stu-id="e6380-107">Install JEA</span></span>

<span data-ttu-id="e6380-108">JEA je k dispozici pomocí Windows Powershellu 5.0 a vyšším, ale pro všechny funkce se doporučuje nainstalovat nejnovější verzi prostředí PowerShell, které jsou k dispozici pro váš systém.</span><span class="sxs-lookup"><span data-stu-id="e6380-108">JEA is available with Windows PowerShell 5.0 and higher, but for full functionality it is recommended that you install the latest version of PowerShell available for your system.</span></span>
<span data-ttu-id="e6380-109">Následující tabulka popisuje JEA na dostupnost ve Windows serveru:</span><span class="sxs-lookup"><span data-stu-id="e6380-109">The following table describes JEA's availability on Windows Server:</span></span>

<span data-ttu-id="e6380-110">Serverový operační systém</span><span class="sxs-lookup"><span data-stu-id="e6380-110">Server Operating System</span></span>   | <span data-ttu-id="e6380-111">Dostupnost funkce JEA</span><span class="sxs-lookup"><span data-stu-id="e6380-111">JEA Availability</span></span>
--------------------------|--------------------------------
<span data-ttu-id="e6380-112">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e6380-112">Windows Server 2016</span></span>       | <span data-ttu-id="e6380-113">Předinstalované</span><span class="sxs-lookup"><span data-stu-id="e6380-113">Preinstalled</span></span>
<span data-ttu-id="e6380-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e6380-114">Windows Server 2012 R2</span></span>    | <span data-ttu-id="e6380-115">Všechny funkce s WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="e6380-115">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="e6380-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e6380-116">Windows Server 2012</span></span>       | <span data-ttu-id="e6380-117">Všechny funkce s WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="e6380-117">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="e6380-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="e6380-118">Windows Server 2008 R2</span></span>    | <span data-ttu-id="e6380-119">Funkčnost omezená<sup>1</sup> s WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="e6380-119">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>

<span data-ttu-id="e6380-120">Můžete také JEA domácí nebo pracovní počítače:</span><span class="sxs-lookup"><span data-stu-id="e6380-120">You can also use JEA on your home or work computer:</span></span>

<span data-ttu-id="e6380-121">Klientský operační systém</span><span class="sxs-lookup"><span data-stu-id="e6380-121">Client Operating System</span></span>   | <span data-ttu-id="e6380-122">Dostupnost funkce JEA</span><span class="sxs-lookup"><span data-stu-id="e6380-122">JEA Availability</span></span>
--------------------------|-----------------------------------------------------
<span data-ttu-id="e6380-123">Windows 10 1607+</span><span class="sxs-lookup"><span data-stu-id="e6380-123">Windows 10 1607+</span></span>          | <span data-ttu-id="e6380-124">Předinstalované</span><span class="sxs-lookup"><span data-stu-id="e6380-124">Preinstalled</span></span>
<span data-ttu-id="e6380-125">Windows 10 1603, 1511</span><span class="sxs-lookup"><span data-stu-id="e6380-125">Windows 10 1603, 1511</span></span>     | <span data-ttu-id="e6380-126">Předinstalované, s funkčnost omezená<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="e6380-126">Preinstalled, with reduced functionality<sup>2</sup></span></span>
<span data-ttu-id="e6380-127">Windows 10 1507</span><span class="sxs-lookup"><span data-stu-id="e6380-127">Windows 10 1507</span></span>           | <span data-ttu-id="e6380-128">Nedostupné</span><span class="sxs-lookup"><span data-stu-id="e6380-128">Not available</span></span>
<span data-ttu-id="e6380-129">Windows 8, 8.1</span><span class="sxs-lookup"><span data-stu-id="e6380-129">Windows 8, 8.1</span></span>            | <span data-ttu-id="e6380-130">Všechny funkce s WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="e6380-130">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="e6380-131">Windows 7</span><span class="sxs-lookup"><span data-stu-id="e6380-131">Windows 7</span></span>                 | <span data-ttu-id="e6380-132">Funkčnost omezená<sup>1</sup> s WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="e6380-132">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>

<span data-ttu-id="e6380-133"><sup>1</sup> JEA nedá nakonfigurovat na použití skupinové účty spravované služby v systému Windows Server 2008 R2 nebo Windows 7.</span><span class="sxs-lookup"><span data-stu-id="e6380-133"><sup>1</sup> JEA cannot be configured to use group managed service accounts on Windows Server 2008 R2 or Windows 7.</span></span>
<span data-ttu-id="e6380-134">Virtuální účty a další funkce JEA *jsou* podporována.</span><span class="sxs-lookup"><span data-stu-id="e6380-134">Virtual accounts and other JEA features *are* supported.</span></span>

<span data-ttu-id="e6380-135"><sup>2</sup> Windows 10 verze 1511 a 1603 nepodporuje následující funkce JEA: spuštění jako skupinu spravovaný účet služby, pravidla podmíněného přístupu v konfiguraci relace, uživatel jednotky a poskytnutí přístupu pro místní uživatelské účty.</span><span class="sxs-lookup"><span data-stu-id="e6380-135"><sup>2</sup> Windows 10 versions 1511 and 1603 do not support the following JEA features: running as a group managed service account, conditional access rules in session configurations, the user drive, and granting access to local user accounts.</span></span>
<span data-ttu-id="e6380-136">Chcete-li získat podporu pro tyto funkce, aktualizaci Windows verze 1607 (Anniversary Update) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="e6380-136">To get support for these features, update Windows to version 1607 (Anniversary Update) or higher.</span></span>

### <a name="check-which-version-of-powershell-is-installed"></a><span data-ttu-id="e6380-137">Zkontrolujte, kterou verzi prostředí PowerShell je nainstalovaný.</span><span class="sxs-lookup"><span data-stu-id="e6380-137">Check which version of PowerShell is installed</span></span>

<span data-ttu-id="e6380-138">Ke kontrole, kterou verzi prostředí PowerShell je nainstalovaný ve vašem systému, zkontrolujte, `$PSVersionTable` proměnné v příkazový řádek Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="e6380-138">To check which version of PowerShell is installed on your system, check the `$PSVersionTable` variable in a Windows PowerShell prompt.</span></span>

```powershell
$PSVersionTable.PSVersion
```

```output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

<span data-ttu-id="e6380-139">Jste připraveni používat funkce JEA, pokud *hlavní* verze je větší než nebo rovno **5**.</span><span class="sxs-lookup"><span data-stu-id="e6380-139">You are ready to use JEA if the *Major* version is equal to or greater than **5**.</span></span>
<span data-ttu-id="e6380-140">Pro dosažení co nejlepších výsledků a mít přístup k nejnovějším funkcím, doporučuje se, že upgradujete na verzi prostředí PowerShell **5.1** Pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="e6380-140">For the best experience, and to have access to all the latest features, it is recommended that you upgrade to PowerShell version **5.1** when possible.</span></span>

### <a name="install-windows-management-framework"></a><span data-ttu-id="e6380-141">Nainstalujte Windows Management Framework</span><span class="sxs-lookup"><span data-stu-id="e6380-141">Install Windows Management Framework</span></span>

<span data-ttu-id="e6380-142">Pokud používáte starší verzi prostředí PowerShell, je potřeba aktualizovat váš systém pomocí nejnovější aktualizace Windows Management Frameworku (WMF).</span><span class="sxs-lookup"><span data-stu-id="e6380-142">If you are running an older version of PowerShell, you will need to update your system with the latest Windows Management Framework (WMF) update.</span></span>
<span data-ttu-id="e6380-143">Balíčky aktualizací a odkaz na nejnovější poznámky k verzi WMF jsou k dispozici v [Download Center](https://blogs.msdn.microsoft.com/powershell/2016/02/24/windows-management-framework-wmf-5-0-rtm-packages-has-been-republished/).</span><span class="sxs-lookup"><span data-stu-id="e6380-143">Update packages and a link to the latest WMF release notes are available in the [Download Center](https://blogs.msdn.microsoft.com/powershell/2016/02/24/windows-management-framework-wmf-5-0-rtm-packages-has-been-republished/).</span></span>

<span data-ttu-id="e6380-144">Důrazně doporučujeme, abyste otestovali kompatibilitu vašich úloh s WMF před provedením upgradu všech serverů.</span><span class="sxs-lookup"><span data-stu-id="e6380-144">It is strongly recommended that you test your workload's compatibility with WMF before upgrading all of your servers.</span></span>

<span data-ttu-id="e6380-145">Uživatelé Windows 10 nainstalujte nejnovější aktualizace funkcí k získání aktuální verze Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="e6380-145">Windows 10 users should install the latest feature updates to obtain the current version of Windows PowerShell.</span></span>

## <a name="enable-powershell-remoting"></a><span data-ttu-id="e6380-146">Povolení vzdálené komunikace Powershellu</span><span class="sxs-lookup"><span data-stu-id="e6380-146">Enable PowerShell Remoting</span></span>

<span data-ttu-id="e6380-147">Vzdálenou komunikaci prostředí PowerShell poskytuje základ, na kterém je sestavena JEA.</span><span class="sxs-lookup"><span data-stu-id="e6380-147">PowerShell Remoting provides the foundation on which JEA is built.</span></span>
<span data-ttu-id="e6380-148">Proto je nutné zajistit, je povolená Vzdálená komunikace prostředí PowerShell a [správně zabezpečená](/powershell/scripting/setup/winrmsecurity) ve vašem systému, abyste mohli používat JEA.</span><span class="sxs-lookup"><span data-stu-id="e6380-148">It is therefore necessary to ensure PowerShell Remoting is enabled and [properly secured](/powershell/scripting/setup/winrmsecurity) on your system before you can use JEA.</span></span>

<span data-ttu-id="e6380-149">Ve výchozím nastavení systému Windows Server 2012, 2012 R2 a 2016 je povolená Vzdálená komunikace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6380-149">PowerShell Remoting is enabled by default on Windows Server 2012, 2012 R2, and 2016.</span></span>
<span data-ttu-id="e6380-150">Můžete povolit vzdálenou komunikaci prostředí PowerShell spuštěním následujícího příkazu v okně PowerShell se zvýšenými oprávněními.</span><span class="sxs-lookup"><span data-stu-id="e6380-150">You can enable PowerShell Remoting by running the following command in an elevated PowerShell window.</span></span>

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a><span data-ttu-id="e6380-151">Povolit modul prostředí PowerShell a protokolování bloku skriptu (volitelné)</span><span class="sxs-lookup"><span data-stu-id="e6380-151">Enable PowerShell module and script block logging (optional)</span></span>

<span data-ttu-id="e6380-152">Následujícím postupem povolíte protokolování pro všechny akce prostředí PowerShell v systému.</span><span class="sxs-lookup"><span data-stu-id="e6380-152">The following steps enable logging for all PowerShell actions on your system.</span></span>
<span data-ttu-id="e6380-153">Není vyžadováno pro JEA protokolování modulu prostředí PowerShell, ale důrazně doporučujeme zapnout je zajistit, že uživatelé příkazy spouštět se protokolují v centrálním umístění.</span><span class="sxs-lookup"><span data-stu-id="e6380-153">PowerShell Module Logging is not required for JEA, however it is strongly recommended that you turn it on to ensure the commands users run are logged in a central location.</span></span>

<span data-ttu-id="e6380-154">Můžete nakonfigurovat pomocí zásad skupiny Zásady protokolování modulu prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6380-154">You can configure the PowerShell Module Logging policy using Group Policy.</span></span>

1. <span data-ttu-id="e6380-155">Otevřete Editor místních zásad skupiny na pracovní stanici nebo objektu zásad skupiny v konzole pro správu zásad skupiny na řadič domény služby Active Directory</span><span class="sxs-lookup"><span data-stu-id="e6380-155">Open the Local Group Policy Editor on a workstation or a Group Policy Object in the Group Policy Management Console on an Active Directory Domain Controller</span></span>
2. <span data-ttu-id="e6380-156">Přejděte do **konfigurace počítače\\šablony pro správu\\součásti Windows\\prostředí Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="e6380-156">Navigate to **Computer Configuration\\Administrative Templates\\Windows Components\\Windows PowerShell**</span></span>
3. <span data-ttu-id="e6380-157">Dvakrát klikněte na **zapnout protokolování modulu**</span><span class="sxs-lookup"><span data-stu-id="e6380-157">Double click on **Turn on Module Logging**</span></span>
4. <span data-ttu-id="e6380-158">Klikněte na tlačítko **povoleno**</span><span class="sxs-lookup"><span data-stu-id="e6380-158">Click **Enabled**</span></span>
5. <span data-ttu-id="e6380-159">V části Možnosti, klikněte na **zobrazit** vedle názvů modulů</span><span class="sxs-lookup"><span data-stu-id="e6380-159">In the Options section, click on **Show** next to Module Names</span></span>
6. <span data-ttu-id="e6380-160">Typ `\*` v zobrazeném okně.</span><span class="sxs-lookup"><span data-stu-id="e6380-160">Type `\*` in the pop up window.</span></span> <span data-ttu-id="e6380-161">Toto dá pokyn k protokolování příkazy ze všech modulů Powershellu.</span><span class="sxs-lookup"><span data-stu-id="e6380-161">This instructs PowerShell to log commands from all modules.</span></span>
7. <span data-ttu-id="e6380-162">Klikněte na tlačítko **OK** nastavení zásad</span><span class="sxs-lookup"><span data-stu-id="e6380-162">Click **OK** to set the policy</span></span>
8. <span data-ttu-id="e6380-163">Dvakrát klikněte na **zapnout protokolování bloku skriptu prostředí PowerShell**</span><span class="sxs-lookup"><span data-stu-id="e6380-163">Double click on **Turn on PowerShell Script Block Logging**</span></span>
9. <span data-ttu-id="e6380-164">Klikněte na tlačítko **povoleno**</span><span class="sxs-lookup"><span data-stu-id="e6380-164">Click **Enabled**</span></span>
10. <span data-ttu-id="e6380-165">Klikněte na tlačítko **OK** nastavení zásad</span><span class="sxs-lookup"><span data-stu-id="e6380-165">Click **OK** to set the policy</span></span>
11. <span data-ttu-id="e6380-166">(Počítačích připojených k doméně jenom) Spustit `gpupdate` nebo počkejte na zpracování aktualizované zásady a použít nastavení zásad skupiny</span><span class="sxs-lookup"><span data-stu-id="e6380-166">(On domain-joined machines only) Run `gpupdate` or wait for Group Policy to process the updated policy and apply the settings</span></span>

<span data-ttu-id="e6380-167">Můžete také povolit přepis systémová Powershellu prostřednictvím zásad skupiny.</span><span class="sxs-lookup"><span data-stu-id="e6380-167">You can also enable system-wide PowerShell transcription through Group Policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6380-168">Další kroky</span><span class="sxs-lookup"><span data-stu-id="e6380-168">Next steps</span></span>

[<span data-ttu-id="e6380-169">Vytvořte soubor funkce rolí</span><span class="sxs-lookup"><span data-stu-id="e6380-169">Create a role capability file</span></span>](role-capabilities.md)

[<span data-ttu-id="e6380-170">Vytvoření konfiguračního souboru relace</span><span class="sxs-lookup"><span data-stu-id="e6380-170">Create a session configuration file</span></span>](session-configurations.md)

## <a name="see-also"></a><span data-ttu-id="e6380-171">Viz taky</span><span class="sxs-lookup"><span data-stu-id="e6380-171">See also</span></span>

[<span data-ttu-id="e6380-172">Další informace o zabezpečení vzdálené komunikace Powershellu a WinRM</span><span class="sxs-lookup"><span data-stu-id="e6380-172">Additional information about PowerShell Remoting and WinRM security</span></span>](/powershell/scripting/setup/winrmsecurity)

[<span data-ttu-id="e6380-173">*Prostředí PowerShell ♥ modrý tým* blogový příspěvek o zabezpečení</span><span class="sxs-lookup"><span data-stu-id="e6380-173">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)