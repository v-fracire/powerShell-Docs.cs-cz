---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "MSFT_DSCLocalConfigurationManager – třída"
ms.openlocfilehash: 35f732698fcc58f7bd43945edd10c143ffb79af9
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="e3a00-103">MSFT_DSCLocalConfigurationManager – třída</span><span class="sxs-lookup"><span data-stu-id="e3a00-103">MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="e3a00-104">Místní Configuration Manager (LCM), které řídí stavy konfigurace soubory a používá konfiguraci agenta použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e3a00-104">The Local Configuration Manager (LCM) that controls the states of configuration files and uses Configuration Agent to apply the configurations.</span></span>

<span data-ttu-id="e3a00-105">Následující syntaxe je jednodušší z kódu formátu MOF (Managed Object) a zahrnuje všechny zděděné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="e3a00-105">The following syntax is simplified from Managed Object Format (MOF) code and includes all of the inherited properties.</span></span>

## <a name="syntax"></a><span data-ttu-id="e3a00-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e3a00-106">Syntax</span></span>
------

``` syntax
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## <a name="members"></a><span data-ttu-id="e3a00-107">Členové</span><span class="sxs-lookup"><span data-stu-id="e3a00-107">Members</span></span>
-------

<span data-ttu-id="e3a00-108">**MSFT_DSCLocalConfigurationManager** třída má následující členy:</span><span class="sxs-lookup"><span data-stu-id="e3a00-108">The **MSFT_DSCLocalConfigurationManager** class has the following members:</span></span>

-   <span data-ttu-id="e3a00-109">[Metody] []</span><span class="sxs-lookup"><span data-stu-id="e3a00-109">[Methods][]</span></span>

### <a name="methods"></a><span data-ttu-id="e3a00-110">Metody</span><span class="sxs-lookup"><span data-stu-id="e3a00-110">Methods</span></span>

<span data-ttu-id="e3a00-111">**MSFT_DSCLocalConfigurationManager** třída má tyto metody.</span><span class="sxs-lookup"><span data-stu-id="e3a00-111">The **MSFT_DSCLocalConfigurationManager** class has these methods.</span></span>

|<span data-ttu-id="e3a00-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="e3a00-112">Method</span></span> |<span data-ttu-id="e3a00-113">Popis</span><span class="sxs-lookup"><span data-stu-id="e3a00-113">Description</span></span> |
|:--- |:---|
| [<span data-ttu-id="e3a00-114">ApplyConfiguration</span><span class="sxs-lookup"><span data-stu-id="e3a00-114">ApplyConfiguration</span></span>](msft-dsclocalconfigurationmanager-applyconfiguration.md)| <span data-ttu-id="e3a00-115">Používá Agent konfigurace můžete použít konfiguraci, která čeká na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="e3a00-115">Uses the Configuration Agent to apply the configuration that is pending.</span></span>| 
| [<span data-ttu-id="e3a00-116">DisableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="e3a00-116">DisableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| <span data-ttu-id="e3a00-117">Zakáže ladění prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="e3a00-117">Disables DSC resource debugging.</span></span>| 
| [<span data-ttu-id="e3a00-118">EnableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="e3a00-118">EnableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| <span data-ttu-id="e3a00-119">Povolí ladění na prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="e3a00-119">Enables DSC resource debugging.</span></span>| 
| [<span data-ttu-id="e3a00-120">Getconfiguration –</span><span class="sxs-lookup"><span data-stu-id="e3a00-120">GetConfiguration</span></span>](msft-dsclocalconfigurationmanager-getconfiguration.md)| <span data-ttu-id="e3a00-121">Odešle spravovaný uzel dokumentu konfigurace a používá **získat** metoda konfigurace agenta pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e3a00-121">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>| 
| [<span data-ttu-id="e3a00-122">GetConfigurationResultOutput</span><span class="sxs-lookup"><span data-stu-id="e3a00-122">GetConfigurationResultOutput</span></span>](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| <span data-ttu-id="e3a00-123">Získá výstup Agent konfigurace týkající se určité úlohy.</span><span class="sxs-lookup"><span data-stu-id="e3a00-123">Gets the Configuration Agent output relating to a specific job.</span></span>| 
| [<span data-ttu-id="e3a00-124">GetConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="e3a00-124">GetConfigurationStatus</span></span>](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| <span data-ttu-id="e3a00-125">Načtení historie stav konfigurace.</span><span class="sxs-lookup"><span data-stu-id="e3a00-125">Get the configuration status history.</span></span>| 
| [<span data-ttu-id="e3a00-126">GetMetaConfiguration</span><span class="sxs-lookup"><span data-stu-id="e3a00-126">GetMetaConfiguration</span></span>](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| <span data-ttu-id="e3a00-127">Získá LCM nastavení, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="e3a00-127">Gets the LCM settings that are used to control Configuration Agent.</span></span>| 
| [<span data-ttu-id="e3a00-128">PerformRequiredConfigurationChecks</span><span class="sxs-lookup"><span data-stu-id="e3a00-128">PerformRequiredConfigurationChecks</span></span>](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| <span data-ttu-id="e3a00-129">Spustí kontrolu konzistence.</span><span class="sxs-lookup"><span data-stu-id="e3a00-129">Starts the consistency check.</span></span>| 
| [<span data-ttu-id="e3a00-130">RemoveConfiguration</span><span class="sxs-lookup"><span data-stu-id="e3a00-130">RemoveConfiguration</span></span>](msft-dsclocalconfigurationmanager-removeconfiguration.md)| <span data-ttu-id="e3a00-131">Odebere konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="e3a00-131">Removes the configuration files.</span></span>| 
| [<span data-ttu-id="e3a00-132">ResourceGet</span><span class="sxs-lookup"><span data-stu-id="e3a00-132">ResourceGet</span></span>](msft-dsclocalconfigurationmanager-resourceget.md)| <span data-ttu-id="e3a00-133">Volá přímo **získat** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="e3a00-133">Directly calls the **Get** method of a DSC resource.</span></span>| 
| [<span data-ttu-id="e3a00-134">ResourceSet</span><span class="sxs-lookup"><span data-stu-id="e3a00-134">ResourceSet</span></span>](msft-dsclocalconfigurationmanager-resourceset.md)| <span data-ttu-id="e3a00-135">Volá přímo **nastavit** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="e3a00-135">Directly calls the **Set** method of a DSC resource.</span></span>| 
| [<span data-ttu-id="e3a00-136">ResourceTest</span><span class="sxs-lookup"><span data-stu-id="e3a00-136">ResourceTest</span></span>](msft-dsclocalconfigurationmanager-resourcetest.md)| <span data-ttu-id="e3a00-137">Volá přímo **Test** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="e3a00-137">Directly calls the **Test** method of a DSC resource.</span></span>| 
| [<span data-ttu-id="e3a00-138">Vrácení zpět</span><span class="sxs-lookup"><span data-stu-id="e3a00-138">RollBack</span></span>](msft-dsclocalconfigurationmanager-rollback.md)| <span data-ttu-id="e3a00-139">Zobrazí souhrn zpět na předchozí konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e3a00-139">Rolls back to a previous configuration.</span></span>| 
| [<span data-ttu-id="e3a00-140">SendConfiguration</span><span class="sxs-lookup"><span data-stu-id="e3a00-140">SendConfiguration</span></span>](msft-dsclocalconfigurationmanager-sendconfiguration.md)| <span data-ttu-id="e3a00-141">Odešle spravovaný uzel dokumentu konfigurace a uloží ji jako nevyřízenou změnu.</span><span class="sxs-lookup"><span data-stu-id="e3a00-141">Sends the configuration document to the managed node and saves it as a pending change.</span></span>| 
| [<span data-ttu-id="e3a00-142">SendConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="e3a00-142">SendConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| <span data-ttu-id="e3a00-143">Odešle spravovaný uzel dokumentu konfigurace a používá Agent konfigurace můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e3a00-143">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>| 
| [<span data-ttu-id="e3a00-144">SendConfigurationApplyAsync</span><span class="sxs-lookup"><span data-stu-id="e3a00-144">SendConfigurationApplyAsync</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| <span data-ttu-id="e3a00-145">Poslat spravovaný uzel dokumentu konfigurace a spustí pomocí konfigurace agenta pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e3a00-145">Send the configuration document to the managed node and start using the Configuration Agent to apply the configuration.</span></span> <span data-ttu-id="e3a00-146">Pomocí GetConfigurationResultOutput načíst výstup výsledků.</span><span class="sxs-lookup"><span data-stu-id="e3a00-146">Use GetConfigurationResultOutput to retrieve result output.</span></span>| 
| [<span data-ttu-id="e3a00-147">SendMetaConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="e3a00-147">SendMetaConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| <span data-ttu-id="e3a00-148">Nastaví LCM nastavení, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="e3a00-148">Sets the LCM settings that are used to control the Configuration Agent.</span></span>| 
| [<span data-ttu-id="e3a00-149">StopConfiguration</span><span class="sxs-lookup"><span data-stu-id="e3a00-149">StopConfiguration</span></span>](msft-dsclocalconfigurationmanager-stopconfiguration.md)| <span data-ttu-id="e3a00-150">Zastaví konfiguraci, která je v průběhu.</span><span class="sxs-lookup"><span data-stu-id="e3a00-150">Stops the configuration that is in progress.</span></span>| 
| [<span data-ttu-id="e3a00-151">TestConfiguration</span><span class="sxs-lookup"><span data-stu-id="e3a00-151">TestConfiguration</span></span>](msft-dsclocalconfigurationmanager-testconfiguration.md)| <span data-ttu-id="e3a00-152">Odešle spravovaný uzel dokumentu konfigurace a zkontroluje aktuální konfiguraci proti dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e3a00-152">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>| 



 

## <a name="requirements"></a><span data-ttu-id="e3a00-153">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e3a00-153">Requirements</span></span>
------------
><span data-ttu-id="e3a00-154">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="e3a00-154">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="e3a00-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e3a00-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>



 

 



