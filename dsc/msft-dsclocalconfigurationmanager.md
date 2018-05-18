---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Třída MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 615f2998b11a0a927d3868d852e0d408f500c86d
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="da8e0-103">Třída MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="da8e0-103">MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="da8e0-104">Místní Configuration Manager (LCM), které řídí stavy konfigurace soubory a používá konfiguraci agenta použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="da8e0-104">The Local Configuration Manager (LCM) that controls the states of configuration files and uses Configuration Agent to apply the configurations.</span></span>

<span data-ttu-id="da8e0-105">Následující syntaxe je jednodušší z kódu formátu MOF (Managed Object) a zahrnuje všechny zděděné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="da8e0-105">The following syntax is simplified from Managed Object Format (MOF) code and includes all of the inherited properties.</span></span>

## <a name="syntax"></a><span data-ttu-id="da8e0-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="da8e0-106">Syntax</span></span>
------

``` syntax
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## <a name="members"></a><span data-ttu-id="da8e0-107">Členové</span><span class="sxs-lookup"><span data-stu-id="da8e0-107">Members</span></span>
-------

<span data-ttu-id="da8e0-108">**MSFT_DSCLocalConfigurationManager** třída má následující členy:</span><span class="sxs-lookup"><span data-stu-id="da8e0-108">The **MSFT_DSCLocalConfigurationManager** class has the following members:</span></span>

-   <span data-ttu-id="da8e0-109">[Metody] []</span><span class="sxs-lookup"><span data-stu-id="da8e0-109">[Methods][]</span></span>

### <a name="methods"></a><span data-ttu-id="da8e0-110">Metody</span><span class="sxs-lookup"><span data-stu-id="da8e0-110">Methods</span></span>

<span data-ttu-id="da8e0-111">**MSFT_DSCLocalConfigurationManager** třída má tyto metody.</span><span class="sxs-lookup"><span data-stu-id="da8e0-111">The **MSFT_DSCLocalConfigurationManager** class has these methods.</span></span>

|<span data-ttu-id="da8e0-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="da8e0-112">Method</span></span> |<span data-ttu-id="da8e0-113">Popis</span><span class="sxs-lookup"><span data-stu-id="da8e0-113">Description</span></span> |
|:--- |:---|
| [<span data-ttu-id="da8e0-114">ApplyConfiguration</span><span class="sxs-lookup"><span data-stu-id="da8e0-114">ApplyConfiguration</span></span>](msft-dsclocalconfigurationmanager-applyconfiguration.md)| <span data-ttu-id="da8e0-115">Používá Agent konfigurace můžete použít konfiguraci, která čeká na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="da8e0-115">Uses the Configuration Agent to apply the configuration that is pending.</span></span>|
| [<span data-ttu-id="da8e0-116">DisableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="da8e0-116">DisableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| <span data-ttu-id="da8e0-117">Zakáže ladění prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="da8e0-117">Disables DSC resource debugging.</span></span>|
| [<span data-ttu-id="da8e0-118">EnableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="da8e0-118">EnableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| <span data-ttu-id="da8e0-119">Povolí ladění na prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="da8e0-119">Enables DSC resource debugging.</span></span>|
| [<span data-ttu-id="da8e0-120">Getconfiguration –</span><span class="sxs-lookup"><span data-stu-id="da8e0-120">GetConfiguration</span></span>](msft-dsclocalconfigurationmanager-getconfiguration.md)| <span data-ttu-id="da8e0-121">Odešle spravovaný uzel dokumentu konfigurace a používá **získat** metoda konfigurace agenta pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="da8e0-121">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>|
| [<span data-ttu-id="da8e0-122">GetConfigurationResultOutput</span><span class="sxs-lookup"><span data-stu-id="da8e0-122">GetConfigurationResultOutput</span></span>](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| <span data-ttu-id="da8e0-123">Získá výstup Agent konfigurace týkající se určité úlohy.</span><span class="sxs-lookup"><span data-stu-id="da8e0-123">Gets the Configuration Agent output relating to a specific job.</span></span>|
| [<span data-ttu-id="da8e0-124">GetConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="da8e0-124">GetConfigurationStatus</span></span>](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| <span data-ttu-id="da8e0-125">Načtení historie stav konfigurace.</span><span class="sxs-lookup"><span data-stu-id="da8e0-125">Get the configuration status history.</span></span>|
| [<span data-ttu-id="da8e0-126">GetMetaConfiguration</span><span class="sxs-lookup"><span data-stu-id="da8e0-126">GetMetaConfiguration</span></span>](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| <span data-ttu-id="da8e0-127">Získá LCM nastavení, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="da8e0-127">Gets the LCM settings that are used to control Configuration Agent.</span></span>|
| [<span data-ttu-id="da8e0-128">PerformRequiredConfigurationChecks</span><span class="sxs-lookup"><span data-stu-id="da8e0-128">PerformRequiredConfigurationChecks</span></span>](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| <span data-ttu-id="da8e0-129">Spustí kontrolu konzistence.</span><span class="sxs-lookup"><span data-stu-id="da8e0-129">Starts the consistency check.</span></span>|
| [<span data-ttu-id="da8e0-130">RemoveConfiguration</span><span class="sxs-lookup"><span data-stu-id="da8e0-130">RemoveConfiguration</span></span>](msft-dsclocalconfigurationmanager-removeconfiguration.md)| <span data-ttu-id="da8e0-131">Odebere konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="da8e0-131">Removes the configuration files.</span></span>|
| [<span data-ttu-id="da8e0-132">ResourceGet</span><span class="sxs-lookup"><span data-stu-id="da8e0-132">ResourceGet</span></span>](msft-dsclocalconfigurationmanager-resourceget.md)| <span data-ttu-id="da8e0-133">Volá přímo **získat** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="da8e0-133">Directly calls the **Get** method of a DSC resource.</span></span>|
| [<span data-ttu-id="da8e0-134">resourceSet</span><span class="sxs-lookup"><span data-stu-id="da8e0-134">ResourceSet</span></span>](msft-dsclocalconfigurationmanager-resourceset.md)| <span data-ttu-id="da8e0-135">Volá přímo **nastavit** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="da8e0-135">Directly calls the **Set** method of a DSC resource.</span></span>|
| [<span data-ttu-id="da8e0-136">ResourceTest</span><span class="sxs-lookup"><span data-stu-id="da8e0-136">ResourceTest</span></span>](msft-dsclocalconfigurationmanager-resourcetest.md)| <span data-ttu-id="da8e0-137">Volá přímo **Test** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="da8e0-137">Directly calls the **Test** method of a DSC resource.</span></span>|
| [<span data-ttu-id="da8e0-138">Vrácení zpět</span><span class="sxs-lookup"><span data-stu-id="da8e0-138">RollBack</span></span>](msft-dsclocalconfigurationmanager-rollback.md)| <span data-ttu-id="da8e0-139">Zobrazí souhrn zpět na předchozí konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="da8e0-139">Rolls back to a previous configuration.</span></span>|
| [<span data-ttu-id="da8e0-140">SendConfiguration</span><span class="sxs-lookup"><span data-stu-id="da8e0-140">SendConfiguration</span></span>](msft-dsclocalconfigurationmanager-sendconfiguration.md)| <span data-ttu-id="da8e0-141">Odešle spravovaný uzel dokumentu konfigurace a uloží ji jako nevyřízenou změnu.</span><span class="sxs-lookup"><span data-stu-id="da8e0-141">Sends the configuration document to the managed node and saves it as a pending change.</span></span>|
| [<span data-ttu-id="da8e0-142">SendConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="da8e0-142">SendConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| <span data-ttu-id="da8e0-143">Odešle spravovaný uzel dokumentu konfigurace a používá Agent konfigurace můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="da8e0-143">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>|
| [<span data-ttu-id="da8e0-144">SendConfigurationApplyAsync</span><span class="sxs-lookup"><span data-stu-id="da8e0-144">SendConfigurationApplyAsync</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| <span data-ttu-id="da8e0-145">Poslat spravovaný uzel dokumentu konfigurace a spustí pomocí konfigurace agenta pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="da8e0-145">Send the configuration document to the managed node and start using the Configuration Agent to apply the configuration.</span></span> <span data-ttu-id="da8e0-146">Pomocí GetConfigurationResultOutput načíst výstup výsledků.</span><span class="sxs-lookup"><span data-stu-id="da8e0-146">Use GetConfigurationResultOutput to retrieve result output.</span></span>|
| [<span data-ttu-id="da8e0-147">SendMetaConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="da8e0-147">SendMetaConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| <span data-ttu-id="da8e0-148">Nastaví LCM nastavení, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="da8e0-148">Sets the LCM settings that are used to control the Configuration Agent.</span></span>|
| [<span data-ttu-id="da8e0-149">StopConfiguration</span><span class="sxs-lookup"><span data-stu-id="da8e0-149">StopConfiguration</span></span>](msft-dsclocalconfigurationmanager-stopconfiguration.md)| <span data-ttu-id="da8e0-150">Zastaví konfiguraci, která je v průběhu.</span><span class="sxs-lookup"><span data-stu-id="da8e0-150">Stops the configuration that is in progress.</span></span>|
| [<span data-ttu-id="da8e0-151">TestConfiguration</span><span class="sxs-lookup"><span data-stu-id="da8e0-151">TestConfiguration</span></span>](msft-dsclocalconfigurationmanager-testconfiguration.md)| <span data-ttu-id="da8e0-152">Odešle spravovaný uzel dokumentu konfigurace a zkontroluje aktuální konfiguraci proti dokumentu.</span><span class="sxs-lookup"><span data-stu-id="da8e0-152">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>|





## <a name="requirements"></a><span data-ttu-id="da8e0-153">Požadavky</span><span class="sxs-lookup"><span data-stu-id="da8e0-153">Requirements</span></span>
------------
><span data-ttu-id="da8e0-154">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="da8e0-154">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="da8e0-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="da8e0-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>