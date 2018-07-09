---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 0e8d0cb1e4afa7bc791d45bfb0b981654cb09ed5
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892565"
---
# <a name="unified-and-consistent-state-and-status-representation"></a><span data-ttu-id="1c8f5-102">Jednotné vyjádření stavu</span><span class="sxs-lookup"><span data-stu-id="1c8f5-102">Unified and Consistent State and Status Representation</span></span>

<span data-ttu-id="1c8f5-103">Řadu vylepšení byly provedeny v této verzi za účelem automatizace založená LCM stavu a statusu DSC.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-103">A series of enhancements have been made in this release for automations built LCM state and DSC status.</span></span> <span data-ttu-id="1c8f5-104">Patří mezi ně jednotné stavu a statusu reprezentace, spravovat data a času vlastnost stavu objektů vrácených podle `Get-DscConfigurationStatus` rutiny a vylepšené LCM stavu podrobnosti vlastnosti vrácené `Get-DscLocalConfigurationManager` rutiny.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-104">These include unified and consistent state and status representations, manageable datetime property of status objects returned by `Get-DscConfigurationStatus` cmdlet and enhanced LCM state details property returned by `Get-DscLocalConfigurationManager` cmdlet.</span></span>

<span data-ttu-id="1c8f5-105">Vyjádření stavu LCM a stav operace DSC se znovu obrácena pozornost a unified podle následujících pravidel:</span><span class="sxs-lookup"><span data-stu-id="1c8f5-105">The representation of LCM state and DSC operation status are revisited and unified according to following rules:</span></span>

1. <span data-ttu-id="1c8f5-106">Notprocessed prostředků neovlivní LCM stavu a statusu DSC.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-106">Notprocessed resource does not impact LCM state and DSC status.</span></span>
2. <span data-ttu-id="1c8f5-107">LCM zastavení zpracování další prostředky, jakmile narazí na prostředek, který vyžaduje restartování.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-107">LCM stop processing further resources once it encounters a resource that requests reboot.</span></span>
3. <span data-ttu-id="1c8f5-108">Prostředek, který požaduje restartování není v požadovaném stavu, dokud se ve skutečnosti stane restartování.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-108">A resource that requests reboot is not in desired state until reboot actually happens.</span></span>
4. <span data-ttu-id="1c8f5-109">Po zjištění prostředek, který selže, LCM zajišťuje zpracování další prostředky, dokud nejsou závislé na selhání jedné.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-109">After encountering a resource that fails, LCM keeps processing further resources as long as they are not dependent on the failure one.</span></span>
5. <span data-ttu-id="1c8f5-110">Celkový stav vrácený `Get-DscConfigurationStatus` rutina je super sadu stavu všechny prostředky.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-110">The overall status returned by `Get-DscConfigurationStatus` cmdlet is the super set of all resources' status.</span></span>
6. <span data-ttu-id="1c8f5-111">Stav PendingReboot je nadmnožinou PendingConfiguration stavu.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-111">The PendingReboot state is a superset of PendingConfiguration state.</span></span>

   <span data-ttu-id="1c8f5-112">Následující tabulka uvádí, výsledné stavy souvisejících vlastností v rámci několika typické scénáře.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-112">The table below illustrates the resultant state and status related properties under a few typical scenarios.</span></span>

   | <span data-ttu-id="1c8f5-113">Scénář</span><span class="sxs-lookup"><span data-stu-id="1c8f5-113">Scenario</span></span>                    | <span data-ttu-id="1c8f5-114">LCMState</span><span class="sxs-lookup"><span data-stu-id="1c8f5-114">LCMState</span></span>       | <span data-ttu-id="1c8f5-115">Stav</span><span class="sxs-lookup"><span data-stu-id="1c8f5-115">Status</span></span> | <span data-ttu-id="1c8f5-116">Požadováno restartování</span><span class="sxs-lookup"><span data-stu-id="1c8f5-116">Reboot Requested</span></span>  | <span data-ttu-id="1c8f5-117">ResourcesInDesiredState</span><span class="sxs-lookup"><span data-stu-id="1c8f5-117">ResourcesInDesiredState</span></span>  | <span data-ttu-id="1c8f5-118">ResourcesNotInDesiredState</span><span class="sxs-lookup"><span data-stu-id="1c8f5-118">ResourcesNotInDesiredState</span></span> |
   |---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
   | <span data-ttu-id="1c8f5-119">S**^**</span><span class="sxs-lookup"><span data-stu-id="1c8f5-119">S**^**</span></span>                          | <span data-ttu-id="1c8f5-120">Nečinnosti</span><span class="sxs-lookup"><span data-stu-id="1c8f5-120">Idle</span></span>                 | <span data-ttu-id="1c8f5-121">Úspěch</span><span class="sxs-lookup"><span data-stu-id="1c8f5-121">Success</span></span>    | <span data-ttu-id="1c8f5-122">$false</span><span class="sxs-lookup"><span data-stu-id="1c8f5-122">$false</span></span>        | <span data-ttu-id="1c8f5-123">S</span><span class="sxs-lookup"><span data-stu-id="1c8f5-123">S</span></span>                            | <span data-ttu-id="1c8f5-124">$null</span><span class="sxs-lookup"><span data-stu-id="1c8f5-124">$null</span></span>                          |
   | <span data-ttu-id="1c8f5-125">F**^**</span><span class="sxs-lookup"><span data-stu-id="1c8f5-125">F**^**</span></span>                          | <span data-ttu-id="1c8f5-126">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="1c8f5-126">PendingConfiguration</span></span> | <span data-ttu-id="1c8f5-127">Chyba</span><span class="sxs-lookup"><span data-stu-id="1c8f5-127">Failure</span></span>    | <span data-ttu-id="1c8f5-128">$false</span><span class="sxs-lookup"><span data-stu-id="1c8f5-128">$false</span></span>        | <span data-ttu-id="1c8f5-129">$null</span><span class="sxs-lookup"><span data-stu-id="1c8f5-129">$null</span></span>                        | <span data-ttu-id="1c8f5-130">F</span><span class="sxs-lookup"><span data-stu-id="1c8f5-130">F</span></span>                              |
   | <span data-ttu-id="1c8f5-131">S,F</span><span class="sxs-lookup"><span data-stu-id="1c8f5-131">S,F</span></span>                             | <span data-ttu-id="1c8f5-132">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="1c8f5-132">PendingConfiguration</span></span> | <span data-ttu-id="1c8f5-133">Chyba</span><span class="sxs-lookup"><span data-stu-id="1c8f5-133">Failure</span></span>    | <span data-ttu-id="1c8f5-134">$false</span><span class="sxs-lookup"><span data-stu-id="1c8f5-134">$false</span></span>        | <span data-ttu-id="1c8f5-135">S</span><span class="sxs-lookup"><span data-stu-id="1c8f5-135">S</span></span>                            | <span data-ttu-id="1c8f5-136">F</span><span class="sxs-lookup"><span data-stu-id="1c8f5-136">F</span></span>                              |
   | <span data-ttu-id="1c8f5-137">F,S</span><span class="sxs-lookup"><span data-stu-id="1c8f5-137">F,S</span></span>                             | <span data-ttu-id="1c8f5-138">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="1c8f5-138">PendingConfiguration</span></span> | <span data-ttu-id="1c8f5-139">Chyba</span><span class="sxs-lookup"><span data-stu-id="1c8f5-139">Failure</span></span>    | <span data-ttu-id="1c8f5-140">$false</span><span class="sxs-lookup"><span data-stu-id="1c8f5-140">$false</span></span>        | <span data-ttu-id="1c8f5-141">S</span><span class="sxs-lookup"><span data-stu-id="1c8f5-141">S</span></span>                            | <span data-ttu-id="1c8f5-142">F</span><span class="sxs-lookup"><span data-stu-id="1c8f5-142">F</span></span>                              |
   | <span data-ttu-id="1c8f5-143">S<sub>1</sub>, F, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="1c8f5-143">S<sub>1</sub>, F, S<sub>2</sub></span></span> | <span data-ttu-id="1c8f5-144">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="1c8f5-144">PendingConfiguration</span></span> | <span data-ttu-id="1c8f5-145">Chyba</span><span class="sxs-lookup"><span data-stu-id="1c8f5-145">Failure</span></span>    | <span data-ttu-id="1c8f5-146">$false</span><span class="sxs-lookup"><span data-stu-id="1c8f5-146">$false</span></span>        | <span data-ttu-id="1c8f5-147">S<sub>1</sub>, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="1c8f5-147">S<sub>1</sub>, S<sub>2</sub></span></span> | <span data-ttu-id="1c8f5-148">F</span><span class="sxs-lookup"><span data-stu-id="1c8f5-148">F</span></span>                              |
   | <span data-ttu-id="1c8f5-149">F<sub>1</sub>, S, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="1c8f5-149">F<sub>1</sub>, S, F<sub>2</sub></span></span> | <span data-ttu-id="1c8f5-150">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="1c8f5-150">PendingConfiguration</span></span> | <span data-ttu-id="1c8f5-151">Chyba</span><span class="sxs-lookup"><span data-stu-id="1c8f5-151">Failure</span></span>    | <span data-ttu-id="1c8f5-152">$false</span><span class="sxs-lookup"><span data-stu-id="1c8f5-152">$false</span></span>        | <span data-ttu-id="1c8f5-153">S</span><span class="sxs-lookup"><span data-stu-id="1c8f5-153">S</span></span>                            | <span data-ttu-id="1c8f5-154">F<sub>1</sub>, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="1c8f5-154">F<sub>1</sub>, F<sub>2</sub></span></span>   |
   | <span data-ttu-id="1c8f5-155">S, r</span><span class="sxs-lookup"><span data-stu-id="1c8f5-155">S, r</span></span>                            | <span data-ttu-id="1c8f5-156">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="1c8f5-156">PendingReboot</span></span>        | <span data-ttu-id="1c8f5-157">Úspěch</span><span class="sxs-lookup"><span data-stu-id="1c8f5-157">Success</span></span>    | <span data-ttu-id="1c8f5-158">$true</span><span class="sxs-lookup"><span data-stu-id="1c8f5-158">$true</span></span>         | <span data-ttu-id="1c8f5-159">S</span><span class="sxs-lookup"><span data-stu-id="1c8f5-159">S</span></span>                            | <span data-ttu-id="1c8f5-160">r</span><span class="sxs-lookup"><span data-stu-id="1c8f5-160">r</span></span>                              |
   | <span data-ttu-id="1c8f5-161">F, r</span><span class="sxs-lookup"><span data-stu-id="1c8f5-161">F, r</span></span>                            | <span data-ttu-id="1c8f5-162">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="1c8f5-162">PendingReboot</span></span>        | <span data-ttu-id="1c8f5-163">Chyba</span><span class="sxs-lookup"><span data-stu-id="1c8f5-163">Failure</span></span>    | <span data-ttu-id="1c8f5-164">$true</span><span class="sxs-lookup"><span data-stu-id="1c8f5-164">$true</span></span>         | <span data-ttu-id="1c8f5-165">$null</span><span class="sxs-lookup"><span data-stu-id="1c8f5-165">$null</span></span>                        | <span data-ttu-id="1c8f5-166">F, r</span><span class="sxs-lookup"><span data-stu-id="1c8f5-166">F, r</span></span>                           |
   | <span data-ttu-id="1c8f5-167">r, S</span><span class="sxs-lookup"><span data-stu-id="1c8f5-167">r, S</span></span>                            | <span data-ttu-id="1c8f5-168">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="1c8f5-168">PendingReboot</span></span>        | <span data-ttu-id="1c8f5-169">Úspěch</span><span class="sxs-lookup"><span data-stu-id="1c8f5-169">Success</span></span>    | <span data-ttu-id="1c8f5-170">$true</span><span class="sxs-lookup"><span data-stu-id="1c8f5-170">$true</span></span>         | <span data-ttu-id="1c8f5-171">$null</span><span class="sxs-lookup"><span data-stu-id="1c8f5-171">$null</span></span>                        | <span data-ttu-id="1c8f5-172">r</span><span class="sxs-lookup"><span data-stu-id="1c8f5-172">r</span></span>                              |
   | <span data-ttu-id="1c8f5-173">r, F</span><span class="sxs-lookup"><span data-stu-id="1c8f5-173">r, F</span></span>                            | <span data-ttu-id="1c8f5-174">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="1c8f5-174">PendingReboot</span></span>        | <span data-ttu-id="1c8f5-175">Úspěch</span><span class="sxs-lookup"><span data-stu-id="1c8f5-175">Success</span></span>    | <span data-ttu-id="1c8f5-176">$true</span><span class="sxs-lookup"><span data-stu-id="1c8f5-176">$true</span></span>         | <span data-ttu-id="1c8f5-177">$null</span><span class="sxs-lookup"><span data-stu-id="1c8f5-177">$null</span></span>                        | <span data-ttu-id="1c8f5-178">r</span><span class="sxs-lookup"><span data-stu-id="1c8f5-178">r</span></span>                              |

   <span data-ttu-id="1c8f5-179">^
   S<sub>můžu</sub>: řadu prostředků, které se úspěšně použila F<sub>můžu</sub>: řadu prostředků, které se použijí neúspěšně r: A prostředků, která vyžaduje restartování \*</span><span class="sxs-lookup"><span data-stu-id="1c8f5-179">^
   S<sub>i</sub>: A series of resources that applied successfully F<sub>i</sub>: A series of resources that applied unsuccessfully r: A resource that requires reboot \*</span></span>

   ```powershell
   $LCMState = (Get-DscLocalConfigurationManager).LCMState
   $Status = (Get-DscConfigurationStatus).Status

   $RebootRequested = (Get-DscConfigurationStatus).RebootRequested

   $ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

   $ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
   ```

## <a name="enhancement-in-get-dscconfigurationstatus-cmdlet"></a><span data-ttu-id="1c8f5-180">Vylepšení v rutině Get-DscConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="1c8f5-180">Enhancement in Get-DscConfigurationStatus cmdlet</span></span>

<span data-ttu-id="1c8f5-181">Bylo provedeno několik vylepšení na `Get-DscConfigurationStatus` rutiny v této verzi.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-181">A few enhancements have been made to `Get-DscConfigurationStatus` cmdlet in this release.</span></span> <span data-ttu-id="1c8f5-182">Vlastnost StartDate objektů vrací rutina dříve, je typu řetězec.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-182">Previously, the StartDate property of objects returned by the cmdlet is of String type.</span></span> <span data-ttu-id="1c8f5-183">Nyní je typu datum a čas, který umožňuje komplexní, výběr a filtrování snadněji založené na vnitřní vlastnosti objektu data a času.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-183">Now, it is of Datetime type, which enables complex selecting and filtering easier based on the intrinsic properties of a Datetime object.</span></span>

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

<span data-ttu-id="1c8f5-184">Tady je příklad, který vrátí že všechny záznamy operace DSC došlo ve stejný den v týdnu jako dnes.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-184">Following is an example that returns all DSC operation records happened on the same day of week as today.</span></span>

```powershell
(Get-DscConfigurationStatus –All) | Where-Object { $_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

<span data-ttu-id="1c8f5-185">Záznamy operací, které nelze provést změny konfigurace uzlu (například pouze operace čtení) jsou odstraněny.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-185">Records of operations that do not make changes to node’s configuration (i.e. read only operations) are eliminated.</span></span> <span data-ttu-id="1c8f5-186">Proto `Test-DscConfiguration`, `Get-DscConfiguration` operace jsou již zfalšované v objektů vrácených z `Get-DscConfigurationStatus` rutiny.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-186">Therefore, `Test-DscConfiguration`, `Get-DscConfiguration` operations are no longer adulterated in returned objects from `Get-DscConfigurationStatus` cmdlet.</span></span>
<span data-ttu-id="1c8f5-187">Záznamy meta operace nastavení konfigurace se přidá do návrat `Get-DscConfigurationStatus` rutiny.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-187">Records of meta configuration setting operation is added to the return of `Get-DscConfigurationStatus` cmdlet.</span></span>

<span data-ttu-id="1c8f5-188">Tady je příklad výsledku vrácený z `Get-DscConfigurationStatus` – všechny rutiny.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-188">Following is an example of result returned from `Get-DscConfigurationStatus` –All cmdlet.</span></span>

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

## <a name="enhancement-in-get-dsclocalconfigurationmanager-cmdlet"></a><span data-ttu-id="1c8f5-189">Vylepšení v rutině Get-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="1c8f5-189">Enhancement in Get-DscLocalConfigurationManager cmdlet</span></span>

<span data-ttu-id="1c8f5-190">Přidání nového pole LCMStateDetail pro objekt vrácený z `Get-DscLocalConfigurationManager` rutiny.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-190">A new field of LCMStateDetail is added to the object returned from `Get-DscLocalConfigurationManager` cmdlet.</span></span> <span data-ttu-id="1c8f5-191">Toto pole se vyplní po LCMState "Zaneprázdněn".</span><span class="sxs-lookup"><span data-stu-id="1c8f5-191">This field is populated when LCMState is "Busy".</span></span> <span data-ttu-id="1c8f5-192">Se dá načíst pomocí následující rutiny:</span><span class="sxs-lookup"><span data-stu-id="1c8f5-192">It can be retrieved by following cmdlet:</span></span>

```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

<span data-ttu-id="1c8f5-193">Tady je příklad výstupu nepřetržitého monitorování v konfiguraci, která vyžaduje dvě restartování na vzdáleném uzlu.</span><span class="sxs-lookup"><span data-stu-id="1c8f5-193">Following is an example output of a continuous monitoring on a configuration that requires two reboots on a remote node.</span></span>

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