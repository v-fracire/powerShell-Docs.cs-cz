---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: b279d388754c5ee42215f21317f7b3d8089b7608
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093877"
---
# <a name="unified-and-consistent-state-and-status-representation"></a><span data-ttu-id="07f23-102">Jednotné vyjádření stavu</span><span class="sxs-lookup"><span data-stu-id="07f23-102">Unified and Consistent State and Status Representation</span></span>

<span data-ttu-id="07f23-103">Řadu vylepšení byly provedeny v této verzi za účelem automatizace založená LCM stavu a statusu DSC.</span><span class="sxs-lookup"><span data-stu-id="07f23-103">A series of enhancements have been made in this release for automations built LCM state and DSC status.</span></span> <span data-ttu-id="07f23-104">Patří mezi ně jednotné stavu a statusu reprezentace, spravovat data a času vlastnost stavu objektů vrácených podle `Get-DscConfigurationStatus` rutiny a vylepšené LCM stavu podrobnosti vlastnosti vrácené `Get-DscLocalConfigurationManager` rutiny.</span><span class="sxs-lookup"><span data-stu-id="07f23-104">These include unified and consistent state and status representations, manageable datetime property of status objects returned by `Get-DscConfigurationStatus` cmdlet and enhanced LCM state details property returned by `Get-DscLocalConfigurationManager` cmdlet.</span></span>

<span data-ttu-id="07f23-105">Vyjádření stavu LCM a stav operace DSC se znovu obrácena pozornost a unified podle následujících pravidel:</span><span class="sxs-lookup"><span data-stu-id="07f23-105">The representation of LCM state and DSC operation status are revisited and unified according to following rules:</span></span>

1. <span data-ttu-id="07f23-106">Notprocessed prostředků neovlivní LCM stavu a statusu DSC.</span><span class="sxs-lookup"><span data-stu-id="07f23-106">Notprocessed resource does not impact LCM state and DSC status.</span></span>
1. <span data-ttu-id="07f23-107">LCM zastavení zpracování další prostředky, jakmile narazí na prostředek, který vyžaduje restartování.</span><span class="sxs-lookup"><span data-stu-id="07f23-107">LCM stop processing further resources once it encounters a resource that requests reboot.</span></span>
1. <span data-ttu-id="07f23-108">Prostředek, který požaduje restartování není v požadovaném stavu, dokud se ve skutečnosti stane restartování.</span><span class="sxs-lookup"><span data-stu-id="07f23-108">A resource that requests reboot is not in desired state until reboot actually happens.</span></span>
1. <span data-ttu-id="07f23-109">Po zjištění prostředek, který selže, LCM zajišťuje zpracování další prostředky, dokud nejsou závislé na selhání jedné.</span><span class="sxs-lookup"><span data-stu-id="07f23-109">After encountering a resource that fails, LCM keeps processing further resources as long as they are not dependent on the failure one.</span></span>
1. <span data-ttu-id="07f23-110">Celkový stav vrácený `Get-DscConfigurationStatus` rutina je super sadu stavu všechny prostředky.</span><span class="sxs-lookup"><span data-stu-id="07f23-110">The overall status returned by `Get-DscConfigurationStatus` cmdlet is the super set of all resources' status.</span></span>
1. <span data-ttu-id="07f23-111">Stav PendingReboot je nadmnožinou PendingConfiguration stavu.</span><span class="sxs-lookup"><span data-stu-id="07f23-111">The PendingReboot state is a superset of PendingConfiguration state.</span></span>

   <span data-ttu-id="07f23-112">Následující tabulka uvádí, výsledné stavy souvisejících vlastností v rámci několika typické scénáře.</span><span class="sxs-lookup"><span data-stu-id="07f23-112">The table below illustrates the resultant state and status related properties under a few typical scenarios.</span></span>

   | <span data-ttu-id="07f23-113">Scénář</span><span class="sxs-lookup"><span data-stu-id="07f23-113">Scenario</span></span>                    | <span data-ttu-id="07f23-114">LCMState</span><span class="sxs-lookup"><span data-stu-id="07f23-114">LCMState</span></span>       | <span data-ttu-id="07f23-115">Stav</span><span class="sxs-lookup"><span data-stu-id="07f23-115">Status</span></span> | <span data-ttu-id="07f23-116">Požadováno restartování</span><span class="sxs-lookup"><span data-stu-id="07f23-116">Reboot Requested</span></span>  | <span data-ttu-id="07f23-117">ResourcesInDesiredState</span><span class="sxs-lookup"><span data-stu-id="07f23-117">ResourcesInDesiredState</span></span>  | <span data-ttu-id="07f23-118">ResourcesNotInDesiredState</span><span class="sxs-lookup"><span data-stu-id="07f23-118">ResourcesNotInDesiredState</span></span> |
   |---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
   | <span data-ttu-id="07f23-119">S**^**</span><span class="sxs-lookup"><span data-stu-id="07f23-119">S**^**</span></span>                          | <span data-ttu-id="07f23-120">Nečinnosti</span><span class="sxs-lookup"><span data-stu-id="07f23-120">Idle</span></span>                 | <span data-ttu-id="07f23-121">Úspěch</span><span class="sxs-lookup"><span data-stu-id="07f23-121">Success</span></span>    | <span data-ttu-id="07f23-122">$false</span><span class="sxs-lookup"><span data-stu-id="07f23-122">$false</span></span>        | <span data-ttu-id="07f23-123">S</span><span class="sxs-lookup"><span data-stu-id="07f23-123">S</span></span>                            | <span data-ttu-id="07f23-124">$null</span><span class="sxs-lookup"><span data-stu-id="07f23-124">$null</span></span>                          |
   | <span data-ttu-id="07f23-125">F**^**</span><span class="sxs-lookup"><span data-stu-id="07f23-125">F**^**</span></span>                          | <span data-ttu-id="07f23-126">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="07f23-126">PendingConfiguration</span></span> | <span data-ttu-id="07f23-127">Chyba</span><span class="sxs-lookup"><span data-stu-id="07f23-127">Failure</span></span>    | <span data-ttu-id="07f23-128">$false</span><span class="sxs-lookup"><span data-stu-id="07f23-128">$false</span></span>        | <span data-ttu-id="07f23-129">$null</span><span class="sxs-lookup"><span data-stu-id="07f23-129">$null</span></span>                        | <span data-ttu-id="07f23-130">F</span><span class="sxs-lookup"><span data-stu-id="07f23-130">F</span></span>                              |
   | <span data-ttu-id="07f23-131">S,F</span><span class="sxs-lookup"><span data-stu-id="07f23-131">S,F</span></span>                             | <span data-ttu-id="07f23-132">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="07f23-132">PendingConfiguration</span></span> | <span data-ttu-id="07f23-133">Chyba</span><span class="sxs-lookup"><span data-stu-id="07f23-133">Failure</span></span>    | <span data-ttu-id="07f23-134">$false</span><span class="sxs-lookup"><span data-stu-id="07f23-134">$false</span></span>        | <span data-ttu-id="07f23-135">S</span><span class="sxs-lookup"><span data-stu-id="07f23-135">S</span></span>                            | <span data-ttu-id="07f23-136">F</span><span class="sxs-lookup"><span data-stu-id="07f23-136">F</span></span>                              |
   | <span data-ttu-id="07f23-137">F,S</span><span class="sxs-lookup"><span data-stu-id="07f23-137">F,S</span></span>                             | <span data-ttu-id="07f23-138">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="07f23-138">PendingConfiguration</span></span> | <span data-ttu-id="07f23-139">Chyba</span><span class="sxs-lookup"><span data-stu-id="07f23-139">Failure</span></span>    | <span data-ttu-id="07f23-140">$false</span><span class="sxs-lookup"><span data-stu-id="07f23-140">$false</span></span>        | <span data-ttu-id="07f23-141">S</span><span class="sxs-lookup"><span data-stu-id="07f23-141">S</span></span>                            | <span data-ttu-id="07f23-142">F</span><span class="sxs-lookup"><span data-stu-id="07f23-142">F</span></span>                              |
   | <span data-ttu-id="07f23-143">S<sub>1</sub>, F, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="07f23-143">S<sub>1</sub>, F, S<sub>2</sub></span></span> | <span data-ttu-id="07f23-144">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="07f23-144">PendingConfiguration</span></span> | <span data-ttu-id="07f23-145">Chyba</span><span class="sxs-lookup"><span data-stu-id="07f23-145">Failure</span></span>    | <span data-ttu-id="07f23-146">$false</span><span class="sxs-lookup"><span data-stu-id="07f23-146">$false</span></span>        | <span data-ttu-id="07f23-147">S<sub>1</sub>, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="07f23-147">S<sub>1</sub>, S<sub>2</sub></span></span> | <span data-ttu-id="07f23-148">F</span><span class="sxs-lookup"><span data-stu-id="07f23-148">F</span></span>                              |
   | <span data-ttu-id="07f23-149">F<sub>1</sub>, S, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="07f23-149">F<sub>1</sub>, S, F<sub>2</sub></span></span> | <span data-ttu-id="07f23-150">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="07f23-150">PendingConfiguration</span></span> | <span data-ttu-id="07f23-151">Chyba</span><span class="sxs-lookup"><span data-stu-id="07f23-151">Failure</span></span>    | <span data-ttu-id="07f23-152">$false</span><span class="sxs-lookup"><span data-stu-id="07f23-152">$false</span></span>        | <span data-ttu-id="07f23-153">S</span><span class="sxs-lookup"><span data-stu-id="07f23-153">S</span></span>                            | <span data-ttu-id="07f23-154">F<sub>1</sub>, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="07f23-154">F<sub>1</sub>, F<sub>2</sub></span></span>   |
   | <span data-ttu-id="07f23-155">S, r</span><span class="sxs-lookup"><span data-stu-id="07f23-155">S, r</span></span>                            | <span data-ttu-id="07f23-156">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="07f23-156">PendingReboot</span></span>        | <span data-ttu-id="07f23-157">Úspěch</span><span class="sxs-lookup"><span data-stu-id="07f23-157">Success</span></span>    | <span data-ttu-id="07f23-158">$true</span><span class="sxs-lookup"><span data-stu-id="07f23-158">$true</span></span>         | <span data-ttu-id="07f23-159">S</span><span class="sxs-lookup"><span data-stu-id="07f23-159">S</span></span>                            | <span data-ttu-id="07f23-160">r</span><span class="sxs-lookup"><span data-stu-id="07f23-160">r</span></span>                              |
   | <span data-ttu-id="07f23-161">F, r</span><span class="sxs-lookup"><span data-stu-id="07f23-161">F, r</span></span>                            | <span data-ttu-id="07f23-162">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="07f23-162">PendingReboot</span></span>        | <span data-ttu-id="07f23-163">Chyba</span><span class="sxs-lookup"><span data-stu-id="07f23-163">Failure</span></span>    | <span data-ttu-id="07f23-164">$true</span><span class="sxs-lookup"><span data-stu-id="07f23-164">$true</span></span>         | <span data-ttu-id="07f23-165">$null</span><span class="sxs-lookup"><span data-stu-id="07f23-165">$null</span></span>                        | <span data-ttu-id="07f23-166">F, r</span><span class="sxs-lookup"><span data-stu-id="07f23-166">F, r</span></span>                           |
   | <span data-ttu-id="07f23-167">r, S</span><span class="sxs-lookup"><span data-stu-id="07f23-167">r, S</span></span>                            | <span data-ttu-id="07f23-168">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="07f23-168">PendingReboot</span></span>        | <span data-ttu-id="07f23-169">Úspěch</span><span class="sxs-lookup"><span data-stu-id="07f23-169">Success</span></span>    | <span data-ttu-id="07f23-170">$true</span><span class="sxs-lookup"><span data-stu-id="07f23-170">$true</span></span>         | <span data-ttu-id="07f23-171">$null</span><span class="sxs-lookup"><span data-stu-id="07f23-171">$null</span></span>                        | <span data-ttu-id="07f23-172">r</span><span class="sxs-lookup"><span data-stu-id="07f23-172">r</span></span>                              |
   | <span data-ttu-id="07f23-173">r, F</span><span class="sxs-lookup"><span data-stu-id="07f23-173">r, F</span></span>                            | <span data-ttu-id="07f23-174">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="07f23-174">PendingReboot</span></span>        | <span data-ttu-id="07f23-175">Úspěch</span><span class="sxs-lookup"><span data-stu-id="07f23-175">Success</span></span>    | <span data-ttu-id="07f23-176">$true</span><span class="sxs-lookup"><span data-stu-id="07f23-176">$true</span></span>         | <span data-ttu-id="07f23-177">$null</span><span class="sxs-lookup"><span data-stu-id="07f23-177">$null</span></span>                        | <span data-ttu-id="07f23-178">r</span><span class="sxs-lookup"><span data-stu-id="07f23-178">r</span></span>                              |

   <span data-ttu-id="07f23-179">^
   S<sub>můžu</sub>: řadu prostředků, které se úspěšně použila F<sub>můžu</sub>: řadu prostředků, které se použijí neúspěšně r: A prostředků, která vyžaduje restartování \*</span><span class="sxs-lookup"><span data-stu-id="07f23-179">^
   S<sub>i</sub>: A series of resources that applied successfully F<sub>i</sub>: A series of resources that applied unsuccessfully r: A resource that requires reboot \*</span></span>

   ```powershell
   $LCMState = (Get-DscLocalConfigurationManager).LCMState
   $Status = (Get-DscConfigurationStatus).Status

   $RebootRequested = (Get-DscConfigurationStatus).RebootRequested

   $ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

   $ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
   ```

## <a name="enhancement-in-get-dscconfigurationstatus-cmdlet"></a><span data-ttu-id="07f23-180">Vylepšení v rutině Get-DscConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="07f23-180">Enhancement in Get-DscConfigurationStatus cmdlet</span></span>

<span data-ttu-id="07f23-181">Bylo provedeno několik vylepšení na `Get-DscConfigurationStatus` rutiny v této verzi.</span><span class="sxs-lookup"><span data-stu-id="07f23-181">A few enhancements have been made to `Get-DscConfigurationStatus` cmdlet in this release.</span></span> <span data-ttu-id="07f23-182">Vlastnost StartDate objektů vrací rutina dříve, je typu řetězec.</span><span class="sxs-lookup"><span data-stu-id="07f23-182">Previously, the StartDate property of objects returned by the cmdlet is of String type.</span></span> <span data-ttu-id="07f23-183">Nyní je typu datum a čas, který umožňuje komplexní, výběr a filtrování snadněji založené na vnitřní vlastnosti objektu data a času.</span><span class="sxs-lookup"><span data-stu-id="07f23-183">Now, it is of Datetime type, which enables complex selecting and filtering easier based on the intrinsic properties of a Datetime object.</span></span>

```powershell
(Get-DscConfigurationStatus).StartDate | Format-List *
DateTime : Friday, November 13, 2015 1:39:44 PM
Date : 11/13/2015 12:00:00 AM
Day : 13
DayOfWeek : Friday
DayOfYear : 317
Hour : 13
Kind : Local
Millisecond : 886
Minute : 39
Month : 11
Second : 44
Ticks : 635830187848860000
TimeOfDay : 13:39:44.8860000
Year : 2015
```

<span data-ttu-id="07f23-184">Tady je příklad, který vrátí že všechny záznamy operace DSC došlo ve stejný den v týdnu jako dnes.</span><span class="sxs-lookup"><span data-stu-id="07f23-184">Following is an example that returns all DSC operation records happened on the same day of week as today.</span></span>

```powershell
(Get-DscConfigurationStatus –All) | Where-Object { $_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

<span data-ttu-id="07f23-185">Záznamy operací, které nelze provést změny konfigurace uzlu (například pouze operace čtení) jsou odstraněny.</span><span class="sxs-lookup"><span data-stu-id="07f23-185">Records of operations that do not make changes to node’s configuration (i.e. read only operations) are eliminated.</span></span> <span data-ttu-id="07f23-186">Proto `Test-DscConfiguration`, `Get-DscConfiguration` operace jsou již zfalšované v objektů vrácených z `Get-DscConfigurationStatus` rutiny.</span><span class="sxs-lookup"><span data-stu-id="07f23-186">Therefore, `Test-DscConfiguration`, `Get-DscConfiguration` operations are no longer adulterated in returned objects from `Get-DscConfigurationStatus` cmdlet.</span></span>
<span data-ttu-id="07f23-187">Záznamy meta operace nastavení konfigurace se přidá do návrat `Get-DscConfigurationStatus` rutiny.</span><span class="sxs-lookup"><span data-stu-id="07f23-187">Records of meta configuration setting operation is added to the return of `Get-DscConfigurationStatus` cmdlet.</span></span>

<span data-ttu-id="07f23-188">Tady je příklad výsledku vrácený z `Get-DscConfigurationStatus` – všechny rutiny.</span><span class="sxs-lookup"><span data-stu-id="07f23-188">Following is an example of result returned from `Get-DscConfigurationStatus` –All cmdlet.</span></span>

```output
All configuration operations:

Status StartDate Type RebootRequested
------ --------- ---- ---------------
Success 11/13/2015 11:38:16 AM Consistency False
Success 11/13/2015 11:23:16 AM Reboot False
Success 11/13/2015 11:21:43 AM Reboot True
Success 11/13/2015 11:20:44 AM Initial True
Success 11/13/2015 11:20:44 AM LocalConfigurationManager False
```

## <a name="enhancement-in-get-dsclocalconfigurationmanager-cmdlet"></a><span data-ttu-id="07f23-189">Vylepšení v rutině Get-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="07f23-189">Enhancement in Get-DscLocalConfigurationManager cmdlet</span></span>

<span data-ttu-id="07f23-190">Přidání nového pole LCMStateDetail pro objekt vrácený z `Get-DscLocalConfigurationManager` rutiny.</span><span class="sxs-lookup"><span data-stu-id="07f23-190">A new field of LCMStateDetail is added to the object returned from `Get-DscLocalConfigurationManager` cmdlet.</span></span> <span data-ttu-id="07f23-191">Toto pole se vyplní po LCMState "Zaneprázdněn".</span><span class="sxs-lookup"><span data-stu-id="07f23-191">This field is populated when LCMState is "Busy".</span></span> <span data-ttu-id="07f23-192">Se dá načíst pomocí následující rutiny:</span><span class="sxs-lookup"><span data-stu-id="07f23-192">It can be retrieved by following cmdlet:</span></span>

```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

<span data-ttu-id="07f23-193">Tady je příklad výstupu nepřetržitého monitorování v konfiguraci, která vyžaduje dvě restartování na vzdáleném uzlu.</span><span class="sxs-lookup"><span data-stu-id="07f23-193">Following is an example output of a continuous monitoring on a configuration that requires two reboots on a remote node.</span></span>

```output
Start a configuration that requires two reboots

Monitor LCM State:
LCM State: Busy, LCM is applying a new configuration.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: Idle,
LCM State: Busy, LCM is performing a consistency check.
LCM State: Idle,
```