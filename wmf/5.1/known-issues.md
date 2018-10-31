---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Známé problémy ve WMF 5.1
ms.openlocfilehash: e59ea1b9a5282eb5727a37ce605c71724a219827
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2018
ms.locfileid: "50225841"
---
# <a name="known-issues-in-wmf-51"></a><span data-ttu-id="b7814-103">Známé problémy ve WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="b7814-103">Known Issues in WMF 5.1</span></span>

> [!Note]
> <span data-ttu-id="b7814-104">Tyto informace se mohou změnit.</span><span class="sxs-lookup"><span data-stu-id="b7814-104">This information is subject to change.</span></span>

## <a name="starting-powershell-shortcut-as-administrator"></a><span data-ttu-id="b7814-105">Spouští se místní prostředí PowerShell jako správce</span><span class="sxs-lookup"><span data-stu-id="b7814-105">Starting PowerShell shortcut as Administrator</span></span>

<span data-ttu-id="b7814-106">Po instalaci WMF, pokud se pokusíte spustit PowerShell jako správce z místní, může zobrazit zpráva "Nespecifikovaná chyba".</span><span class="sxs-lookup"><span data-stu-id="b7814-106">Upon installing WMF, if you try to start PowerShell as administrator from the shortcut, you may get an "Unspecified error" message.</span></span>
<span data-ttu-id="b7814-107">Znovu otevřít místní jako bez oprávnění správce a zástupce teď funguje i jako správce.</span><span class="sxs-lookup"><span data-stu-id="b7814-107">Reopen the shortcut as non-administrator and the shortcut now works even as administrator.</span></span>

## <a name="pester"></a><span data-ttu-id="b7814-108">Pester</span><span class="sxs-lookup"><span data-stu-id="b7814-108">Pester</span></span>

<span data-ttu-id="b7814-109">V této verzi jsou dva problémy, které byste měli vědět, když používáte Pester na Nano serveru:</span><span class="sxs-lookup"><span data-stu-id="b7814-109">In this release, there are two issues you should be aware of when using Pester on Nano Server:</span></span>

- <span data-ttu-id="b7814-110">Spouštění testů proti Pester sám může způsobit nějaké chyby kvůli rozdílům mezi úplné CLR a CORE CLR.</span><span class="sxs-lookup"><span data-stu-id="b7814-110">Running tests against Pester itself can result in some failures because of differences between FULL CLR and CORE CLR.</span></span> <span data-ttu-id="b7814-111">Zejména není k dispozici u typu třídou XMLDocument nastavenou na metodu Validate.</span><span class="sxs-lookup"><span data-stu-id="b7814-111">In particular, the Validate method is not available on the XmlDocument type.</span></span> <span data-ttu-id="b7814-112">Šest testů, které k pokusu o ověření schématu NUnit výstupní protokoly se ví nezdaří.</span><span class="sxs-lookup"><span data-stu-id="b7814-112">Six tests which attempt to validate the schema of the NUnit output logs are known to fail.</span></span>
- <span data-ttu-id="b7814-113">Jeden test pokrytí kódu nezdaří aktuálně, protože *WindowsFeature* prostředek DSC na Nano serveru neexistuje.</span><span class="sxs-lookup"><span data-stu-id="b7814-113">One Code Coverage test fails currently because the *WindowsFeature* DSC Resource does not exist in Nano Server.</span></span> <span data-ttu-id="b7814-114">Ale tyto chyby jsou obvykle neškodné a můžete bezpečně ignorovat.</span><span class="sxs-lookup"><span data-stu-id="b7814-114">However, these failures are generally benign and can safely be ignored.</span></span>

## <a name="operation-validation"></a><span data-ttu-id="b7814-115">Ověření operace</span><span class="sxs-lookup"><span data-stu-id="b7814-115">Operation Validation</span></span>

- <span data-ttu-id="b7814-116">`Update-Help` pro modul Microsoft.PowerShell.Operation.Validation kvůli nefunkční pomocný identifikátor URI se nezdaří</span><span class="sxs-lookup"><span data-stu-id="b7814-116">`Update-Help` fails for Microsoft.PowerShell.Operation.Validation module due to non-working help URI</span></span>

## <a name="dsc-after-uninstall-wmf"></a><span data-ttu-id="b7814-117">DSC po odinstalaci WMF</span><span class="sxs-lookup"><span data-stu-id="b7814-117">DSC after uninstall WMF</span></span>

- <span data-ttu-id="b7814-118">Odinstalace WMF nedojde k odstranění dokumentů DSC MOF ve složce Konfigurace.</span><span class="sxs-lookup"><span data-stu-id="b7814-118">Uninstalling WMF does not delete DSC MOF documents from the configuration folder.</span></span> <span data-ttu-id="b7814-119">DSC nebude fungovat správně, pokud MOF dokumenty obsahují novější vlastnosti, které nejsou k dispozici na starších systémů.</span><span class="sxs-lookup"><span data-stu-id="b7814-119">DSC won't work properly if the MOF documents contain newer properties which are not available on the older systems.</span></span> <span data-ttu-id="b7814-120">V tomto případě z vyčištění stavy DSC se zvýšenými oprávněními konzole Powershellu spusťte následující skript.</span><span class="sxs-lookup"><span data-stu-id="b7814-120">In this case, run the following script from elevated PowerShell console to clean up the DSC states.</span></span>

  ```powershell
    $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
            "$env:windir\system32\configuration\*.mof.checksum",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
           )
    $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
  ```

## <a name="jea-virtual-accounts"></a><span data-ttu-id="b7814-121">JEA virtuální účty</span><span class="sxs-lookup"><span data-stu-id="b7814-121">JEA Virtual Accounts</span></span>

<span data-ttu-id="b7814-122">Použití virtuální účet po upgradu na WMF 5.1 nenakonfigurují koncových bodů JEA a konfigurace relace, které umožňují použít virtuální účty ve WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="b7814-122">JEA endpoints and session configurations configured to use virtual accounts in WMF 5.0 will not be configured to use a virtual account after upgrading to WMF 5.1.</span></span>
<span data-ttu-id="b7814-123">To znamená, že příkazy se spouští v relacích JEA spustí pod identitou uživatele připojujícího ne s účtem správce dočasné potenciálně s příkazy, které vyžadují zvýšená oprávnění spustit uživatel.</span><span class="sxs-lookup"><span data-stu-id="b7814-123">This means that commands run in JEA sessions will run under the connecting user's identity instead of a temporary administrator account, potentially preventing the user from running commands which require elevated privileges.</span></span>
<span data-ttu-id="b7814-124">Pokud chcete obnovit virtuální účty, budete muset zrušit registraci a přeregistrovat konfigurace relace, které používají virtuální účty.</span><span class="sxs-lookup"><span data-stu-id="b7814-124">To restore the virtual accounts, you need to unregister and re-register any session configurations that use virtual accounts.</span></span>

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