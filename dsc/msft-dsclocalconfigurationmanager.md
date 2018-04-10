---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Třída MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 598bd7490043975d9d965c12a7337fb3475b3ded
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="ff268-103">Třída MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="ff268-103">MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="ff268-104">Místní Configuration Manager (LCM), které řídí stavy konfigurace soubory a používá konfiguraci agenta použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="ff268-104">The Local Configuration Manager (LCM) that controls the states of configuration files and uses Configuration Agent to apply the configurations.</span></span>

<span data-ttu-id="ff268-105">Následující syntaxe je jednodušší z kódu formátu MOF (Managed Object) a zahrnuje všechny zděděné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="ff268-105">The following syntax is simplified from Managed Object Format (MOF) code and includes all of the inherited properties.</span></span>

## <a name="syntax"></a><span data-ttu-id="ff268-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ff268-106">Syntax</span></span>
------

``` syntax
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## <a name="members"></a><span data-ttu-id="ff268-107">Členové</span><span class="sxs-lookup"><span data-stu-id="ff268-107">Members</span></span>
-------

<span data-ttu-id="ff268-108">**MSFT_DSCLocalConfigurationManager** třída má následující členy:</span><span class="sxs-lookup"><span data-stu-id="ff268-108">The **MSFT_DSCLocalConfigurationManager** class has the following members:</span></span>

-   <span data-ttu-id="ff268-109">[Metody] []</span><span class="sxs-lookup"><span data-stu-id="ff268-109">[Methods][]</span></span>

### <a name="methods"></a><span data-ttu-id="ff268-110">Metody</span><span class="sxs-lookup"><span data-stu-id="ff268-110">Methods</span></span>

<span data-ttu-id="ff268-111">**MSFT_DSCLocalConfigurationManager** třída má tyto metody.</span><span class="sxs-lookup"><span data-stu-id="ff268-111">The **MSFT_DSCLocalConfigurationManager** class has these methods.</span></span>

|<span data-ttu-id="ff268-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="ff268-112">Method</span></span> |<span data-ttu-id="ff268-113">Popis</span><span class="sxs-lookup"><span data-stu-id="ff268-113">Description</span></span> |
|:--- |:---|
| [<span data-ttu-id="ff268-114">ApplyConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff268-114">ApplyConfiguration</span></span>](msft-dsclocalconfigurationmanager-applyconfiguration.md)| <span data-ttu-id="ff268-115">Používá Agent konfigurace můžete použít konfiguraci, která čeká na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="ff268-115">Uses the Configuration Agent to apply the configuration that is pending.</span></span>|
| [<span data-ttu-id="ff268-116">DisableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff268-116">DisableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| <span data-ttu-id="ff268-117">Zakáže ladění prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="ff268-117">Disables DSC resource debugging.</span></span>|
| [<span data-ttu-id="ff268-118">EnableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff268-118">EnableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| <span data-ttu-id="ff268-119">Povolí ladění na prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="ff268-119">Enables DSC resource debugging.</span></span>|
| [<span data-ttu-id="ff268-120">Getconfiguration –</span><span class="sxs-lookup"><span data-stu-id="ff268-120">GetConfiguration</span></span>](msft-dsclocalconfigurationmanager-getconfiguration.md)| <span data-ttu-id="ff268-121">Odešle spravovaný uzel dokumentu konfigurace a používá **získat** metoda konfigurace agenta pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="ff268-121">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>|
| [<span data-ttu-id="ff268-122">GetConfigurationResultOutput</span><span class="sxs-lookup"><span data-stu-id="ff268-122">GetConfigurationResultOutput</span></span>](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| <span data-ttu-id="ff268-123">Získá výstup Agent konfigurace týkající se určité úlohy.</span><span class="sxs-lookup"><span data-stu-id="ff268-123">Gets the Configuration Agent output relating to a specific job.</span></span>|
| [<span data-ttu-id="ff268-124">GetConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="ff268-124">GetConfigurationStatus</span></span>](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| <span data-ttu-id="ff268-125">Načtení historie stav konfigurace.</span><span class="sxs-lookup"><span data-stu-id="ff268-125">Get the configuration status history.</span></span>|
| [<span data-ttu-id="ff268-126">GetMetaConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff268-126">GetMetaConfiguration</span></span>](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| <span data-ttu-id="ff268-127">Získá LCM nastavení, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="ff268-127">Gets the LCM settings that are used to control Configuration Agent.</span></span>|
| [<span data-ttu-id="ff268-128">PerformRequiredConfigurationChecks</span><span class="sxs-lookup"><span data-stu-id="ff268-128">PerformRequiredConfigurationChecks</span></span>](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| <span data-ttu-id="ff268-129">Spustí kontrolu konzistence.</span><span class="sxs-lookup"><span data-stu-id="ff268-129">Starts the consistency check.</span></span>|
| [<span data-ttu-id="ff268-130">RemoveConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff268-130">RemoveConfiguration</span></span>](msft-dsclocalconfigurationmanager-removeconfiguration.md)| <span data-ttu-id="ff268-131">Odebere konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="ff268-131">Removes the configuration files.</span></span>|
| [<span data-ttu-id="ff268-132">ResourceGet</span><span class="sxs-lookup"><span data-stu-id="ff268-132">ResourceGet</span></span>](msft-dsclocalconfigurationmanager-resourceget.md)| <span data-ttu-id="ff268-133">Volá přímo **získat** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="ff268-133">Directly calls the **Get** method of a DSC resource.</span></span>|
| [<span data-ttu-id="ff268-134">ResourceSet</span><span class="sxs-lookup"><span data-stu-id="ff268-134">ResourceSet</span></span>](msft-dsclocalconfigurationmanager-resourceset.md)| <span data-ttu-id="ff268-135">Volá přímo **nastavit** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="ff268-135">Directly calls the **Set** method of a DSC resource.</span></span>|
| [<span data-ttu-id="ff268-136">ResourceTest</span><span class="sxs-lookup"><span data-stu-id="ff268-136">ResourceTest</span></span>](msft-dsclocalconfigurationmanager-resourcetest.md)| <span data-ttu-id="ff268-137">Volá přímo **Test** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="ff268-137">Directly calls the **Test** method of a DSC resource.</span></span>|
| [<span data-ttu-id="ff268-138">RollBack</span><span class="sxs-lookup"><span data-stu-id="ff268-138">RollBack</span></span>](msft-dsclocalconfigurationmanager-rollback.md)| <span data-ttu-id="ff268-139">Zobrazí souhrn zpět na předchozí konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="ff268-139">Rolls back to a previous configuration.</span></span>|
| [<span data-ttu-id="ff268-140">SendConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff268-140">SendConfiguration</span></span>](msft-dsclocalconfigurationmanager-sendconfiguration.md)| <span data-ttu-id="ff268-141">Odešle spravovaný uzel dokumentu konfigurace a uloží ji jako nevyřízenou změnu.</span><span class="sxs-lookup"><span data-stu-id="ff268-141">Sends the configuration document to the managed node and saves it as a pending change.</span></span>|
| [<span data-ttu-id="ff268-142">SendConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="ff268-142">SendConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| <span data-ttu-id="ff268-143">Odešle spravovaný uzel dokumentu konfigurace a používá Agent konfigurace můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="ff268-143">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>|
| [<span data-ttu-id="ff268-144">SendConfigurationApplyAsync</span><span class="sxs-lookup"><span data-stu-id="ff268-144">SendConfigurationApplyAsync</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| <span data-ttu-id="ff268-145">Poslat spravovaný uzel dokumentu konfigurace a spustí pomocí konfigurace agenta pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="ff268-145">Send the configuration document to the managed node and start using the Configuration Agent to apply the configuration.</span></span> <span data-ttu-id="ff268-146">Pomocí GetConfigurationResultOutput načíst výstup výsledků.</span><span class="sxs-lookup"><span data-stu-id="ff268-146">Use GetConfigurationResultOutput to retrieve result output.</span></span>|
| [<span data-ttu-id="ff268-147">SendMetaConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="ff268-147">SendMetaConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| <span data-ttu-id="ff268-148">Nastaví LCM nastavení, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="ff268-148">Sets the LCM settings that are used to control the Configuration Agent.</span></span>|
| [<span data-ttu-id="ff268-149">StopConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff268-149">StopConfiguration</span></span>](msft-dsclocalconfigurationmanager-stopconfiguration.md)| <span data-ttu-id="ff268-150">Zastaví konfiguraci, která je v průběhu.</span><span class="sxs-lookup"><span data-stu-id="ff268-150">Stops the configuration that is in progress.</span></span>|
| [<span data-ttu-id="ff268-151">TestConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff268-151">TestConfiguration</span></span>](msft-dsclocalconfigurationmanager-testconfiguration.md)| <span data-ttu-id="ff268-152">Odešle spravovaný uzel dokumentu konfigurace a zkontroluje aktuální konfiguraci proti dokumentu.</span><span class="sxs-lookup"><span data-stu-id="ff268-152">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>|





## <a name="requirements"></a><span data-ttu-id="ff268-153">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ff268-153">Requirements</span></span>
------------
><span data-ttu-id="ff268-154">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="ff268-154">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="ff268-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="ff268-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>