---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Známé problémy v WMF 5.1
ms.openlocfilehash: d53031bea978087c68fcb22989c7cd2e2cf2d9fa
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="known-issues-in-wmf-51"></a><span data-ttu-id="15e23-103">Známé problémy v WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="15e23-103">Known Issues in WMF 5.1</span></span> #

> <span data-ttu-id="15e23-104">Poznámka: Tyto informace se mohou změnit.</span><span class="sxs-lookup"><span data-stu-id="15e23-104">Note: This information is subject to change.</span></span>

## <a name="starting-powershell-shortcut-as-administrator"></a><span data-ttu-id="15e23-105">Počáteční zástupce prostředí PowerShell jako správce</span><span class="sxs-lookup"><span data-stu-id="15e23-105">Starting PowerShell shortcut as Administrator</span></span>
<span data-ttu-id="15e23-106">Po instalaci WMF, pokud se pokusíte spustit PowerShell jako správce pomocí zástupce, můžete obdržet zprávu "Nespecifikovaná chyba".</span><span class="sxs-lookup"><span data-stu-id="15e23-106">Upon installing WMF, if you try to start PowerShell as administrator from the shortcut, you may get an "Unspecified error" message.</span></span>
<span data-ttu-id="15e23-107">Otevřete zástupce jako bez oprávnění správce a zástupce teď funguje i jako správce.</span><span class="sxs-lookup"><span data-stu-id="15e23-107">Reopen the shortcut as non-administrator and the shortcut now works even as administrator.</span></span>

## <a name="pester"></a><span data-ttu-id="15e23-108">Pester</span><span class="sxs-lookup"><span data-stu-id="15e23-108">Pester</span></span>
<span data-ttu-id="15e23-109">V této verzi existují dva problémy, které byste měli vědět, když používáte Pester na Nano Server:</span><span class="sxs-lookup"><span data-stu-id="15e23-109">In this release, there are two issues you should be aware of when using Pester on Nano Server:</span></span>

* <span data-ttu-id="15e23-110">Spouštění testů proti Pester samotné může způsobit některé selhání kvůli rozdíly mezi úplné CLR a základní CLR.</span><span class="sxs-lookup"><span data-stu-id="15e23-110">Running tests against Pester itself can result in some failures because of differences between FULL CLR and CORE CLR.</span></span> <span data-ttu-id="15e23-111">Na konkrétní metodu Validate není k dispozici na typ dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="15e23-111">In particular, the Validate method is not available on the XmlDocument type.</span></span> <span data-ttu-id="15e23-112">Šest testy, které se pokoušejí o ověření schématu NUnit výstupní protokoly jsou známé selhání.</span><span class="sxs-lookup"><span data-stu-id="15e23-112">Six tests which attempt to validate the schema of the NUnit output logs are known to fail.</span></span>
* <span data-ttu-id="15e23-113">Jeden pokrytí kódu test nezdaří aktuálně, protože *WindowsFeature* prostředek DSC v Nano Server neexistuje.</span><span class="sxs-lookup"><span data-stu-id="15e23-113">One Code Coverage test fails currently because the *WindowsFeature* DSC Resource does not exist in Nano Server.</span></span> <span data-ttu-id="15e23-114">Ale tyto chyby jsou obvykle neškodný a můžete bezpečně ignorovat.</span><span class="sxs-lookup"><span data-stu-id="15e23-114">However, these failures are generally benign and can safely be ignored.</span></span>

## <a name="operation-validation"></a><span data-ttu-id="15e23-115">Ověření operace</span><span class="sxs-lookup"><span data-stu-id="15e23-115">Operation Validation</span></span>

* <span data-ttu-id="15e23-116">Update-Help selže pro modul Microsoft.PowerShell.Operation.Validation z důvodu mimo pracovní Nápověda identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="15e23-116">Update-Help fails for Microsoft.PowerShell.Operation.Validation module due to non-working help URI</span></span>

## <a name="dsc-after-uninstall-wmf"></a><span data-ttu-id="15e23-117">DSC po odinstalaci WMF</span><span class="sxs-lookup"><span data-stu-id="15e23-117">DSC after uninstall WMF</span></span>
* <span data-ttu-id="15e23-118">Odinstalace WMF neodstraní DSC MOF dokumenty ve složce Konfigurace.</span><span class="sxs-lookup"><span data-stu-id="15e23-118">Uninstalling WMF does not delete DSC MOF documents from the configuration folder.</span></span> <span data-ttu-id="15e23-119">DSC nebude pracovat správně, pokud MOF dokumenty obsahují novější vlastností, které nejsou k dispozici na starších systémů.</span><span class="sxs-lookup"><span data-stu-id="15e23-119">DSC won't work properly if the MOF documents contain newer properties which are not available on the older systems.</span></span> <span data-ttu-id="15e23-120">V takovém případě spusťte následující skript zvýšenými konzole PowerShell vyčistěte stavy DSC.</span><span class="sxs-lookup"><span data-stu-id="15e23-120">In this case, run the following script from elevated PowerShell console to to clean up the DSC states.</span></span>
 ```powershell
    $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
            "$env:windir\system32\configuration\*.mof.checksum",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
           )

    $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
 ```

## <a name="jea-virtual-accounts"></a><span data-ttu-id="15e23-121">JEA virtuální účty</span><span class="sxs-lookup"><span data-stu-id="15e23-121">JEA Virtual Accounts</span></span>
<span data-ttu-id="15e23-122">JEA koncových bodů a konfigurace relace, které jsou nakonfigurované na používání virtuální účty v WMF 5.0 nebude nakonfigurovaný na používání virtuálních účtu po upgradu na WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="15e23-122">JEA endpoints and session configurations configured to use virtual accounts in WMF 5.0 will not be configured to use a virtual account after upgrading to WMF 5.1.</span></span>
<span data-ttu-id="15e23-123">To znamená, že příkazy běží v relacích JEA budou spouštěny pod identitu připojování uživatelů místo dočasný správce účtu, potenciálně bránit uživateli v příkazů, které vyžadují zvýšená oprávnění.</span><span class="sxs-lookup"><span data-stu-id="15e23-123">This means that commands run in JEA sessions will run under the connecting user's identity instead of a temporary administrator account, potentially preventing the user from running commands which require elevated privileges.</span></span>
<span data-ttu-id="15e23-124">Pokud chcete obnovit virtuální účty, musíte zrušit registraci a znovu zaregistrovat všechny konfigurace relace, které používají virtuální účty.</span><span class="sxs-lookup"><span data-stu-id="15e23-124">To restore the virtual accounts, you need to unregister and re-register any session configurations that use virtual accounts.</span></span>

```powershell
# Find the JEA endpoint by its name
$jea = Get-PSSessionConfiguration -Name MyJeaEndpoint

# Copy the cached PSSC file so it can be re-registered
$pssc = Copy-Item $jea.ConfigFilePath $env:temp -PassThru

# Unregister the current PSSC
Unregister-PSSessionConfiguration -Name $jea.Name

# Re-register the PSSC
Register-PSSessionConfiguration -Name $jea.Name -Path $pssc.FullName -Force

# Ensure the access policies remain the same
Set-PSSessionConfiguration -Name $newjea.Name -SecurityDescriptorSddl $jea.SecurityDescriptorSddl
```
