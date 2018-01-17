---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "MSFT_DSCLocalConfigurationManager – třída"
ms.openlocfilehash: b2d2ce000988f2c10ab04c4ba5a4650bd3c75ec7
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="5ca95-103">MSFT_DSCLocalConfigurationManager – třída</span><span class="sxs-lookup"><span data-stu-id="5ca95-103">MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="5ca95-104">Místní Configuration Manager (LCM), které řídí stavy konfigurace soubory a používá konfiguraci agenta použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="5ca95-104">The Local Configuration Manager (LCM) that controls the states of configuration files and uses Configuration Agent to apply the configurations.</span></span>

<span data-ttu-id="5ca95-105">Následující syntaxe je jednodušší z kódu formátu MOF (Managed Object) a zahrnuje všechny zděděné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="5ca95-105">The following syntax is simplified from Managed Object Format (MOF) code and includes all of the inherited properties.</span></span>

## <a name="syntax"></a><span data-ttu-id="5ca95-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="5ca95-106">Syntax</span></span>
------

``` syntax
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## <a name="members"></a><span data-ttu-id="5ca95-107">Členové</span><span class="sxs-lookup"><span data-stu-id="5ca95-107">Members</span></span>
-------

<span data-ttu-id="5ca95-108">**MSFT_DSCLocalConfigurationManager** třída má následující členy:</span><span class="sxs-lookup"><span data-stu-id="5ca95-108">The **MSFT_DSCLocalConfigurationManager** class has the following members:</span></span>

-   <span data-ttu-id="5ca95-109">[Metody] []</span><span class="sxs-lookup"><span data-stu-id="5ca95-109">[Methods][]</span></span>

### <a name="methods"></a><span data-ttu-id="5ca95-110">Metody</span><span class="sxs-lookup"><span data-stu-id="5ca95-110">Methods</span></span>

<span data-ttu-id="5ca95-111">**MSFT_DSCLocalConfigurationManager** třída má tyto metody.</span><span class="sxs-lookup"><span data-stu-id="5ca95-111">The **MSFT_DSCLocalConfigurationManager** class has these methods.</span></span>

|<span data-ttu-id="5ca95-112">Metoda</span><span class="sxs-lookup"><span data-stu-id="5ca95-112">Method</span></span> |<span data-ttu-id="5ca95-113">Popis</span><span class="sxs-lookup"><span data-stu-id="5ca95-113">Description</span></span> |
|:--- |:---|
| [<span data-ttu-id="5ca95-114">ApplyConfiguration</span><span class="sxs-lookup"><span data-stu-id="5ca95-114">ApplyConfiguration</span></span>](msft-dsclocalconfigurationmanager-applyconfiguration.md)| <span data-ttu-id="5ca95-115">Používá Agent konfigurace můžete použít konfiguraci, která čeká na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="5ca95-115">Uses the Configuration Agent to apply the configuration that is pending.</span></span>| 
| [<span data-ttu-id="5ca95-116">DisableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="5ca95-116">DisableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| <span data-ttu-id="5ca95-117">Zakáže ladění prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="5ca95-117">Disables DSC resource debugging.</span></span>| 
| [<span data-ttu-id="5ca95-118">EnableDebugConfiguration</span><span class="sxs-lookup"><span data-stu-id="5ca95-118">EnableDebugConfiguration</span></span>](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| <span data-ttu-id="5ca95-119">Povolí ladění na prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="5ca95-119">Enables DSC resource debugging.</span></span>| 
| [<span data-ttu-id="5ca95-120">Getconfiguration –</span><span class="sxs-lookup"><span data-stu-id="5ca95-120">GetConfiguration</span></span>](msft-dsclocalconfigurationmanager-getconfiguration.md)| <span data-ttu-id="5ca95-121">Odešle spravovaný uzel dokumentu konfigurace a používá **získat** metoda konfigurace agenta pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="5ca95-121">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>| 
| [<span data-ttu-id="5ca95-122">GetConfigurationResultOutput</span><span class="sxs-lookup"><span data-stu-id="5ca95-122">GetConfigurationResultOutput</span></span>](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| <span data-ttu-id="5ca95-123">Získá výstup Agent konfigurace týkající se určité úlohy.</span><span class="sxs-lookup"><span data-stu-id="5ca95-123">Gets the Configuration Agent output relating to a specific job.</span></span>| 
| [<span data-ttu-id="5ca95-124">GetConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="5ca95-124">GetConfigurationStatus</span></span>](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| <span data-ttu-id="5ca95-125">Načtení historie stav konfigurace.</span><span class="sxs-lookup"><span data-stu-id="5ca95-125">Get the configuration status history.</span></span>| 
| [<span data-ttu-id="5ca95-126">GetMetaConfiguration</span><span class="sxs-lookup"><span data-stu-id="5ca95-126">GetMetaConfiguration</span></span>](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| <span data-ttu-id="5ca95-127">Získá LCM nastavení, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="5ca95-127">Gets the LCM settings that are used to control Configuration Agent.</span></span>| 
| [<span data-ttu-id="5ca95-128">PerformRequiredConfigurationChecks</span><span class="sxs-lookup"><span data-stu-id="5ca95-128">PerformRequiredConfigurationChecks</span></span>](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| <span data-ttu-id="5ca95-129">Spustí kontrolu konzistence.</span><span class="sxs-lookup"><span data-stu-id="5ca95-129">Starts the consistency check.</span></span>| 
| [<span data-ttu-id="5ca95-130">RemoveConfiguration</span><span class="sxs-lookup"><span data-stu-id="5ca95-130">RemoveConfiguration</span></span>](msft-dsclocalconfigurationmanager-removeconfiguration.md)| <span data-ttu-id="5ca95-131">Odebere konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="5ca95-131">Removes the configuration files.</span></span>| 
| [<span data-ttu-id="5ca95-132">ResourceGet</span><span class="sxs-lookup"><span data-stu-id="5ca95-132">ResourceGet</span></span>](msft-dsclocalconfigurationmanager-resourceget.md)| <span data-ttu-id="5ca95-133">Volá přímo **získat** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="5ca95-133">Directly calls the **Get** method of a DSC resource.</span></span>| 
| [<span data-ttu-id="5ca95-134">ResourceSet</span><span class="sxs-lookup"><span data-stu-id="5ca95-134">ResourceSet</span></span>](msft-dsclocalconfigurationmanager-resourceset.md)| <span data-ttu-id="5ca95-135">Volá přímo **nastavit** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="5ca95-135">Directly calls the **Set** method of a DSC resource.</span></span>| 
| [<span data-ttu-id="5ca95-136">ResourceTest</span><span class="sxs-lookup"><span data-stu-id="5ca95-136">ResourceTest</span></span>](msft-dsclocalconfigurationmanager-resourcetest.md)| <span data-ttu-id="5ca95-137">Volá přímo **Test** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="5ca95-137">Directly calls the **Test** method of a DSC resource.</span></span>| 
| [<span data-ttu-id="5ca95-138">RollBack</span><span class="sxs-lookup"><span data-stu-id="5ca95-138">RollBack</span></span>](msft-dsclocalconfigurationmanager-rollback.md)| <span data-ttu-id="5ca95-139">Zobrazí souhrn zpět na předchozí konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="5ca95-139">Rolls back to a previous configuration.</span></span>| 
| [<span data-ttu-id="5ca95-140">SendConfiguration</span><span class="sxs-lookup"><span data-stu-id="5ca95-140">SendConfiguration</span></span>](msft-dsclocalconfigurationmanager-sendconfiguration.md)| <span data-ttu-id="5ca95-141">Odešle spravovaný uzel dokumentu konfigurace a uloží ji jako nevyřízenou změnu.</span><span class="sxs-lookup"><span data-stu-id="5ca95-141">Sends the configuration document to the managed node and saves it as a pending change.</span></span>| 
| [<span data-ttu-id="5ca95-142">SendConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="5ca95-142">SendConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| <span data-ttu-id="5ca95-143">Odešle spravovaný uzel dokumentu konfigurace a používá Agent konfigurace můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="5ca95-143">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>| 
| [<span data-ttu-id="5ca95-144">SendConfigurationApplyAsync</span><span class="sxs-lookup"><span data-stu-id="5ca95-144">SendConfigurationApplyAsync</span></span>](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| <span data-ttu-id="5ca95-145">Poslat spravovaný uzel dokumentu konfigurace a spustí pomocí konfigurace agenta pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="5ca95-145">Send the configuration document to the managed node and start using the Configuration Agent to apply the configuration.</span></span> <span data-ttu-id="5ca95-146">Pomocí GetConfigurationResultOutput načíst výstup výsledků.</span><span class="sxs-lookup"><span data-stu-id="5ca95-146">Use GetConfigurationResultOutput to retrieve result output.</span></span>| 
| [<span data-ttu-id="5ca95-147">SendMetaConfigurationApply</span><span class="sxs-lookup"><span data-stu-id="5ca95-147">SendMetaConfigurationApply</span></span>](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| <span data-ttu-id="5ca95-148">Nastaví LCM nastavení, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="5ca95-148">Sets the LCM settings that are used to control the Configuration Agent.</span></span>| 
| [<span data-ttu-id="5ca95-149">StopConfiguration</span><span class="sxs-lookup"><span data-stu-id="5ca95-149">StopConfiguration</span></span>](msft-dsclocalconfigurationmanager-stopconfiguration.md)| <span data-ttu-id="5ca95-150">Zastaví konfiguraci, která je v průběhu.</span><span class="sxs-lookup"><span data-stu-id="5ca95-150">Stops the configuration that is in progress.</span></span>| 
| [<span data-ttu-id="5ca95-151">TestConfiguration</span><span class="sxs-lookup"><span data-stu-id="5ca95-151">TestConfiguration</span></span>](msft-dsclocalconfigurationmanager-testconfiguration.md)| <span data-ttu-id="5ca95-152">Odešle spravovaný uzel dokumentu konfigurace a zkontroluje aktuální konfiguraci proti dokumentu.</span><span class="sxs-lookup"><span data-stu-id="5ca95-152">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>| 



 

## <a name="requirements"></a><span data-ttu-id="5ca95-153">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5ca95-153">Requirements</span></span>
------------
><span data-ttu-id="5ca95-154">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="5ca95-154">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="5ca95-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="5ca95-155">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>



 

 



