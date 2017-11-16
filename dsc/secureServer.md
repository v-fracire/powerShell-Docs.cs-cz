---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Doporučené postupy pro vyžádání obsahu"
ms.openlocfilehash: 66b97f4edb43926866b39731d720a2dc8c91eb2e
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="pull-server-best-practices"></a><span data-ttu-id="6da81-103">Doporučené postupy pro vyžádání obsahu</span><span class="sxs-lookup"><span data-stu-id="6da81-103">Pull server best practices</span></span>

><span data-ttu-id="6da81-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6da81-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="6da81-105">Souhrn: Tento dokument je určený zahrnuje proces a rozšiřitelnost pomůže technici, kteří jsou Příprava řešení.</span><span class="sxs-lookup"><span data-stu-id="6da81-105">Summary: This document is intended to include process and extensibility to assist engineers who are preparing for the solution.</span></span> <span data-ttu-id="6da81-106">Podrobnosti by měl poskytovat osvědčené postupy, jak identifikovaný zákazníků a potom ověřit produktový tým zajistit doporučení jsou budoucí přístupem a považovat za stabilní.</span><span class="sxs-lookup"><span data-stu-id="6da81-106">Details should provide best practices as identified by customers and then validated by the product team to ensure recommendations are future facing and considered stable.</span></span>

| |<span data-ttu-id="6da81-107">Informace o dokumentu</span><span class="sxs-lookup"><span data-stu-id="6da81-107">Doc Info</span></span>|
|:---|:---|
<span data-ttu-id="6da81-108">Autor</span><span class="sxs-lookup"><span data-stu-id="6da81-108">Author</span></span> | <span data-ttu-id="6da81-109">Michael Greene</span><span class="sxs-lookup"><span data-stu-id="6da81-109">Michael Greene</span></span>  
<span data-ttu-id="6da81-110">Recenzenti</span><span class="sxs-lookup"><span data-stu-id="6da81-110">Reviewers</span></span> | <span data-ttu-id="6da81-111">Ben Gelens, Ravikanth Chaganti Aleksandar Nikolic</span><span class="sxs-lookup"><span data-stu-id="6da81-111">Ben Gelens, Ravikanth Chaganti, Aleksandar Nikolic</span></span>  
<span data-ttu-id="6da81-112">Publikovat</span><span class="sxs-lookup"><span data-stu-id="6da81-112">Published</span></span> | <span data-ttu-id="6da81-113">Duben 2015</span><span class="sxs-lookup"><span data-stu-id="6da81-113">April, 2015</span></span>

## <a name="abstract"></a><span data-ttu-id="6da81-114">Abstraktní</span><span class="sxs-lookup"><span data-stu-id="6da81-114">Abstract</span></span>

<span data-ttu-id="6da81-115">Tento dokument určená k poskytování oficiální pokyny pro každý, kdo plánování implementaci serveru pro vyžádání obsahu konfigurace požadovaného stavu aplikace Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6da81-115">This document is designed to provide official guidance for anyone planning for a Windows PowerShell Desired State Configuration pull server implementation.</span></span> <span data-ttu-id="6da81-116">Vyžádání obsahu server je jednoduchý služba, která by měla trvat jenom k nasazení.</span><span class="sxs-lookup"><span data-stu-id="6da81-116">A pull server is a simple service that should take only minutes to deploy.</span></span> <span data-ttu-id="6da81-117">I když tento dokument nabídne technické postupy pokyny, které je možné v nasazení, hodnota tohoto dokumentu je referenční osvědčené postupy a co mají vezměte v úvahu před nasazením.</span><span class="sxs-lookup"><span data-stu-id="6da81-117">Although this document will offer technical how-to guidance that can be used in a deployment, the value of this document is as a reference for best practices and what to think about before deploying.</span></span>
<span data-ttu-id="6da81-118">Čtečky by měl mít základní znalost DSC a termínů používaných k popisu komponenty, které jsou zahrnuté v nasazení DSC.</span><span class="sxs-lookup"><span data-stu-id="6da81-118">Readers should have basic familiarity with DSC, and the terms used to describe the components that are included in a DSC deployment.</span></span> <span data-ttu-id="6da81-119">Další informace najdete v tématu [Přehled konfigurace prostředí Windows PowerShell požadovaného stavu](https://technet.microsoft.com/en-us/library/dn249912.aspx) tématu.</span><span class="sxs-lookup"><span data-stu-id="6da81-119">For more information, see the [Windows PowerShell Desired State Configuration Overview](https://technet.microsoft.com/en-us/library/dn249912.aspx)  topic.</span></span>
<span data-ttu-id="6da81-120">Očekávaným DSC vyvíjí v cloudu cadence základní technologii, včetně serveru vyžádané replikace se také očekává vyvíjí a zavádět nové funkce.</span><span class="sxs-lookup"><span data-stu-id="6da81-120">As DSC is expected to evolve at cloud cadence, the underlying technology including pull server is also expected to evolve and to introduce new capabilities.</span></span> <span data-ttu-id="6da81-121">Tento dokument obsahuje tabulku verze v příloze, která poskytuje odkazy na předchozí verze a odkazy na budoucí vypadající řešení podporovat budoucnost návrhů.</span><span class="sxs-lookup"><span data-stu-id="6da81-121">This document includes a version table in the appendix that provides references to previous releases and references to future looking solutions to encourage forward-looking designs.</span></span>

<span data-ttu-id="6da81-122">Dvě hlavní části tohoto dokumentu:</span><span class="sxs-lookup"><span data-stu-id="6da81-122">The two major sections of this document:</span></span>

 - <span data-ttu-id="6da81-123">Plánování konfigurace</span><span class="sxs-lookup"><span data-stu-id="6da81-123">Configuration Planning</span></span>
 - <span data-ttu-id="6da81-124">Průvodce instalací</span><span class="sxs-lookup"><span data-stu-id="6da81-124">Installation Guide</span></span>
 
### <a name="versions-of-the-windows-management-framework"></a><span data-ttu-id="6da81-125">Verze Windows Management Framework</span><span class="sxs-lookup"><span data-stu-id="6da81-125">Versions of the Windows Management Framework</span></span> 
<span data-ttu-id="6da81-126">Informace v tomto dokumentu je určena pro použití na Windows Management Framework 5.0.</span><span class="sxs-lookup"><span data-stu-id="6da81-126">The information in this document is intended to apply to Windows Management Framework 5.0.</span></span> <span data-ttu-id="6da81-127">Přestože WMF 5.0 není vyžadována pro nasazení a provozování vyžádání obsahu server, verze 5.0 je téma tohoto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="6da81-127">While WMF 5.0 is not required for deploying and operating a pull server, version 5.0 is the focus of this document.</span></span>

### <a name="windows-powershell-desired-state-configuration"></a><span data-ttu-id="6da81-128">Prostředí Windows PowerShell konfigurace požadovaného stavu</span><span class="sxs-lookup"><span data-stu-id="6da81-128">Windows PowerShell Desired State Configuration</span></span>
<span data-ttu-id="6da81-129">Požadované konfigurace stavu (DSC) je platformu správy, která umožňuje nasazení a správa konfiguračních dat pomocí syntaxe odvětví s názvem formát MOF (Managed Object) k popisu modelu CIM (Common Information).</span><span class="sxs-lookup"><span data-stu-id="6da81-129">Desired State Configuration (DSC) is a management platform that enables deploying and managing configuration data by using an industry syntax named the Managed Object Format (MOF) to describe the Common Information Model (CIM).</span></span> <span data-ttu-id="6da81-130">Opensourcový projekt, otevřete Management Infrastructure (OMI), existuje další vývoj těchto standardů napříč platformami, včetně Linux a síťové hardwaru operační systémy.</span><span class="sxs-lookup"><span data-stu-id="6da81-130">An open source project, Open Management Infrastructure (OMI), exists to further development of these standards across platforms including Linux and network hardware operating systems.</span></span> <span data-ttu-id="6da81-131">Další informace najdete v tématu [DMTF stránky propojení s MOF specifikace](http://dmtf.org/standards/cim), a [OMI dokumenty a zdroj](https://collaboration.opengroup.org/omi/documents.php).</span><span class="sxs-lookup"><span data-stu-id="6da81-131">For more information, see the [DMTF page linking to MOF specifications](http://dmtf.org/standards/cim), and [OMI Documents and Source](https://collaboration.opengroup.org/omi/documents.php).</span></span>

<span data-ttu-id="6da81-132">Prostředí Windows PowerShell poskytuje sadu jazyková rozšíření pro konfigurace požadovaného stavu, můžete použít k vytváření a správě deklarativní konfigurace.</span><span class="sxs-lookup"><span data-stu-id="6da81-132">Windows PowerShell provides a set of language extensions for Desired State Configuration that you can use to create and manage declarative configurations.</span></span>

### <a name="pull-server-role"></a><span data-ttu-id="6da81-133">Role serveru vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="6da81-133">Pull server role</span></span>  
<span data-ttu-id="6da81-134">Načítacího serveru poskytuje centralizované služby k uložení konfigurace, které budou přístupné pro cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="6da81-134">A pull server provides a centralized service to store configurations that will be accessible to target nodes.</span></span>
 
<span data-ttu-id="6da81-135">Role serveru vyžádané replikace se dá nasadit jako instance webového serveru nebo sdílené složky SMB.</span><span class="sxs-lookup"><span data-stu-id="6da81-135">The pull server role can be deployed as either a Web Server instance or an SMB file share.</span></span> <span data-ttu-id="6da81-136">Schopnost webového serveru obsahuje rozhraní OData a může volitelně obsahovat možnosti pro cílové uzly k hlášení zpět potvrzení úspěšné nebo neúspěšné, jako jsou použita konfigurace.</span><span class="sxs-lookup"><span data-stu-id="6da81-136">The web server capability includes an OData interface and can optionally include capabilities for target nodes to report back confirmation of success or failure as configurations are applied.</span></span> <span data-ttu-id="6da81-137">Tato funkce je užitečná v prostředích, kde je velké množství cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="6da81-137">This functionality is useful in environments where there are a large number of target nodes.</span></span> <span data-ttu-id="6da81-138">Po dokončení konfigurace cílový uzel (také označované jako klient) tak, aby odkazoval na server vyžádané replikace s nejnovější konfigurací jsou data a všechny požadované skripty stažení a použití.</span><span class="sxs-lookup"><span data-stu-id="6da81-138">After configuring a target node (also referred to as a client) to point to the pull server the latest configuration data and any required scripts are downloaded and applied.</span></span> <span data-ttu-id="6da81-139">Tato situace může nastat, jako jednorázové nasazení nebo jako znovu se vyskytující úlohy, který také umožňuje serveru vyžádané replikace prostředek důležité pro správu změn ve velkém měřítku.</span><span class="sxs-lookup"><span data-stu-id="6da81-139">This can happen as a one-time deployment or as a re-occurring job which also makes the pull server an important asset for managing change at scale.</span></span> <span data-ttu-id="6da81-140">Další informace najdete v tématu [Windows PowerShell požadovaného stavu konfigurace pro vyžádání obsahu servery](https://technet.microsoft.com/en-us/library/dn249913.aspx) a [nabízení a režimů pro vyžádání obsahu konfigurace](https://technet.microsoft.com/en-us/library/dn249913.aspx).</span><span class="sxs-lookup"><span data-stu-id="6da81-140">For more information, see [Windows PowerShell Desired State Configuration Pull Servers](https://technet.microsoft.com/en-us/library/dn249913.aspx) and [Push and Pull Configuration Modes](https://technet.microsoft.com/en-us/library/dn249913.aspx).</span></span>

## <a name="configuration-planning"></a><span data-ttu-id="6da81-141">Plánování konfigurace</span><span class="sxs-lookup"><span data-stu-id="6da81-141">Configuration planning</span></span>

<span data-ttu-id="6da81-142">Pro všechna nasazení softwaru enterprise je informace, které může být shromážděny předem vám pomohou při plánování pro správnou architekturu a abyste byli připraveni kroky potřebné k dokončení nasazení.</span><span class="sxs-lookup"><span data-stu-id="6da81-142">For any enterprise software deployment there is information that can be collected in advance to help plan for the correct architecture and to be prepared for the steps required to complete the deployment.</span></span> <span data-ttu-id="6da81-143">Následující části obsahují informace o tom, jak připravit a organizační připojení, která bude pravděpodobně potřeba předem dojít.</span><span class="sxs-lookup"><span data-stu-id="6da81-143">The following sections provide information regarding how to prepare and the organizational connections that will likely need to happen in advance.</span></span>

### <a name="software-requirements"></a><span data-ttu-id="6da81-144">Požadavky na software</span><span class="sxs-lookup"><span data-stu-id="6da81-144">Software requirements</span></span>

<span data-ttu-id="6da81-145">Nasazení serveru pro vyžádání obsahu vyžaduje funkci DSC služby systému Windows Server.</span><span class="sxs-lookup"><span data-stu-id="6da81-145">Deployment of a pull server requires the DSC Service feature of Windows Server.</span></span> <span data-ttu-id="6da81-146">Tato funkce byla zavedená v systému Windows Server 2012 a byl aktualizován prostřednictvím probíhající verzích Windows Management Framework (WMF).</span><span class="sxs-lookup"><span data-stu-id="6da81-146">This feature was introduced in Windows Server 2012, and has been updated through ongoing releases of Windows Management Framework (WMF).</span></span>

### <a name="software-downloads"></a><span data-ttu-id="6da81-147">Stahování softwaru</span><span class="sxs-lookup"><span data-stu-id="6da81-147">Software downloads</span></span>

<span data-ttu-id="6da81-148">Kromě instalace nejnovější obsah ze služby Windows Update, jsou považovány za osvědčený postup nasadit server DSC za dvě stahování: nejnovější verzi Windows Management Framework a modul DSC pro automatizaci vyžádání obsahu server zřizování.</span><span class="sxs-lookup"><span data-stu-id="6da81-148">In addition to installing the latest content from Windows Update, there are two downloads considered best practice to deploy a DSC pull server: The latest version of Windows Management Framework, and a DSC module to automate pull server provisioning.</span></span>

### <a name="wmf"></a><span data-ttu-id="6da81-149">WMF</span><span class="sxs-lookup"><span data-stu-id="6da81-149">WMF</span></span>

<span data-ttu-id="6da81-150">Windows Server 2012 R2 obsahuje funkci s názvem služby DSC.</span><span class="sxs-lookup"><span data-stu-id="6da81-150">Windows Server 2012 R2 includes a feature named the DSC Service.</span></span> <span data-ttu-id="6da81-151">Funkce služby DSC poskytuje funkce serveru vyžádané replikace, včetně binárních souborů, které podporují koncový bod OData.</span><span class="sxs-lookup"><span data-stu-id="6da81-151">The DSC Service feature provides the pull server functionality, including the binaries that support the OData endpoint.</span></span> <span data-ttu-id="6da81-152">WMF je součástí systému Windows Server a je aktualizován na agilní cadence mezi verzemi Windows serveru.</span><span class="sxs-lookup"><span data-stu-id="6da81-152">WMF is included in Windows Server and is updated on an agile cadence between Windows Server releases.</span></span> <span data-ttu-id="6da81-153">[Nové verze WMF 5.0](http://aka.ms/wmf5latest) můžete zahrnout aktualizace do funkce služby DSC.</span><span class="sxs-lookup"><span data-stu-id="6da81-153">[New versions of WMF 5.0](http://aka.ms/wmf5latest)  can include updates to the DSC Service feature.</span></span> <span data-ttu-id="6da81-154">Z tohoto důvodu je osvědčeným postupem stažení nejnovější verze WMF a přečtěte si poznámky k verzi k určení, pokud tato verze obsahuje aktualizaci funkce služby DSC.</span><span class="sxs-lookup"><span data-stu-id="6da81-154">For this reason, it is a best practice to download the latest release of WMF and to review the release notes to determine if the release includes an update to the DSC service feature.</span></span> <span data-ttu-id="6da81-155">Měli byste taky zkontrolovat v části poznámky k verzi, která určuje, zda je stav návrhu pro aktualizaci nebo scénář v stabilní nebo experimentální.</span><span class="sxs-lookup"><span data-stu-id="6da81-155">You should also review the section of the release notes that indicates whether the design status for an update or scenario is listed as stable or experimental.</span></span> <span data-ttu-id="6da81-156">Povolit pro agilní verze cyklus, jednotlivých funkcí lze deklarovat stabilní, což naznačuje funkci je připravený k použití v produkčním prostředí i podpora produktu WMF vydání ve verzi preview.</span><span class="sxs-lookup"><span data-stu-id="6da81-156">To allow for an agile release cycle, individual features can be declared stable, which indicates the feature is ready to be used in a production environment even while WMF is released in preview.</span></span>
<span data-ttu-id="6da81-157">Další funkce, které byly v minulosti aktualizovány podle verze WMF (viz poznámky k verzi WMF další podrobnosti):</span><span class="sxs-lookup"><span data-stu-id="6da81-157">Other features that have historically been updated by WMF releases (see the WMF Release Notes for further detail):</span></span>

 - <span data-ttu-id="6da81-158">Integrované skriptovací prostředí Windows PowerShell Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6da81-158">Windows PowerShell Windows PowerShell Integrated Scripting</span></span>
 - <span data-ttu-id="6da81-159">Prostředí (ISE) v prostředí Windows PowerShell webové služby (správu OData</span><span class="sxs-lookup"><span data-stu-id="6da81-159">Environment (ISE) Windows PowerShell Web Services (Management OData</span></span>
 - <span data-ttu-id="6da81-160">Rozšíření IIS) prostředí Windows PowerShell konfigurace požadovaného stavu (DSC)</span><span class="sxs-lookup"><span data-stu-id="6da81-160">IIS Extension)  Windows PowerShell Desired State Configuration (DSC)</span></span>
 - <span data-ttu-id="6da81-161">Windows (WinRM) Vzdálená správa Windows Management Instrumentation (WMI)</span><span class="sxs-lookup"><span data-stu-id="6da81-161">Windows Remote Management (WinRM) Windows Management Instrumentation (WMI)</span></span>

### <a name="dsc-resource"></a><span data-ttu-id="6da81-162">Prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="6da81-162">DSC resource</span></span>

<span data-ttu-id="6da81-163">Nasazení na server vyžádané replikace můžete zjednodušit tím zřizováním služby pomocí skriptu konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="6da81-163">A pull server deployment can be simplified by provisioning the service using a DSC configuration script.</span></span> <span data-ttu-id="6da81-164">Tento dokument obsahuje konfigurační skripty, které slouží k nasazení uzlem produkční připravené serveru.</span><span class="sxs-lookup"><span data-stu-id="6da81-164">This document includes configuration scripts that can be used to deploy a production ready server node.</span></span> <span data-ttu-id="6da81-165">Použít konfigurační skripty, DSC modul je potřeba který není součástí systému Windows Server.</span><span class="sxs-lookup"><span data-stu-id="6da81-165">To use the configuration scripts, a DSC module is required that is not included in Windows Server.</span></span> <span data-ttu-id="6da81-166">Název požadované modulu je **xPSDesiredStateConfiguration**, což zahrnuje prostředek DSC **xDscWebService**.</span><span class="sxs-lookup"><span data-stu-id="6da81-166">The required module name is **xPSDesiredStateConfiguration**, which includes the DSC resource **xDscWebService**.</span></span> <span data-ttu-id="6da81-167">Modul xPSDesiredStateConfiguration si můžete stáhnout [zde](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).</span><span class="sxs-lookup"><span data-stu-id="6da81-167">The xPSDesiredStateConfiguration module can be downloaded [here](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).</span></span>

<span data-ttu-id="6da81-168">Použití **instalace modulu** rutiny z **PowerShellGet** modulu.</span><span class="sxs-lookup"><span data-stu-id="6da81-168">Use the **Install-Module** cmdlet from the **PowerShellGet** module.</span></span>

```powershell
Install-Module xPSDesiredStateConfiguration
```

<span data-ttu-id="6da81-169">**PowerShellGet** modulu stáhne modulu:</span><span class="sxs-lookup"><span data-stu-id="6da81-169">The **PowerShellGet** module will download the module to:</span></span> 

`C:\Program Files\Windows PowerShell\Modules`

<span data-ttu-id="6da81-170">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="6da81-170">Planning task</span></span>|
---|
<span data-ttu-id="6da81-171">Máte přístup k instalačním souborům pro Windows Server 2012 R2?</span><span class="sxs-lookup"><span data-stu-id="6da81-171">Do you have access to the installation files for Windows Server 2012 R2?</span></span>|
<span data-ttu-id="6da81-172">Prostředí nasazení budou mít přístup k Internetu stahovat WMF a modul z online galerie?</span><span class="sxs-lookup"><span data-stu-id="6da81-172">Will the deployment environment have Internet access to download WMF and the module from the online gallery?</span></span>|
<span data-ttu-id="6da81-173">Jak budou instalovat nejnovější aktualizace zabezpečení po instalaci operačního systému?</span><span class="sxs-lookup"><span data-stu-id="6da81-173">How will you install the latest security updates after installing the operating system?</span></span>|
<span data-ttu-id="6da81-174">Prostředí bude mít přístup k Internetu k získání aktualizací, nebo bude mít na místním serveru Windows Server Update Services (WSUS)?</span><span class="sxs-lookup"><span data-stu-id="6da81-174">Will the environment have Internet access to obtain updates, or will it have a local Windows Server Update Services (WSUS) server?</span></span>|
<span data-ttu-id="6da81-175">Máte přístup k systému Windows Server instalační soubory, které již obsahují aktualizace prostřednictvím offline vkládání?</span><span class="sxs-lookup"><span data-stu-id="6da81-175">Do you have access to Windows Server installation files that already include updates through offline injection?</span></span>|

### <a name="hardware-requirements"></a><span data-ttu-id="6da81-176">Požadavky na hardware</span><span class="sxs-lookup"><span data-stu-id="6da81-176">Hardware requirements</span></span>

<span data-ttu-id="6da81-177">Nasazení serveru vyžádané replikace jsou podporovány na fyzické i virtuální servery.</span><span class="sxs-lookup"><span data-stu-id="6da81-177">Pull server deployments are supported on both physical and virtual servers.</span></span> <span data-ttu-id="6da81-178">Požadavky na nastavení velikosti pro vyžádání obsahu server zarovnané s požadavky na Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="6da81-178">The sizing requirements for pull server align with the requirements for Windows Server 2012 R2.</span></span>

<span data-ttu-id="6da81-179">: 1,4 GHz 64bitový procesor</span><span class="sxs-lookup"><span data-stu-id="6da81-179">CPU: 1.4 GHz 64-bit processor</span></span>  
<span data-ttu-id="6da81-180">Paměti: 512 MB</span><span class="sxs-lookup"><span data-stu-id="6da81-180">Memory: 512 MB</span></span>  
<span data-ttu-id="6da81-181">Místa na disku: 32 GB</span><span class="sxs-lookup"><span data-stu-id="6da81-181">Disk Space: 32 GB</span></span>  
<span data-ttu-id="6da81-182">Síť: Adaptér Gigabit Ethernet</span><span class="sxs-lookup"><span data-stu-id="6da81-182">Network: Gigabit Ethernet Adapter</span></span>  

<span data-ttu-id="6da81-183">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="6da81-183">Planning task</span></span>|
---|
<span data-ttu-id="6da81-184">Budete nasazovat na fyzickém hardwaru nebo na virtualizační platformě?</span><span class="sxs-lookup"><span data-stu-id="6da81-184">Will you deploy on physical hardware or on a virtualization platform?</span></span>|
<span data-ttu-id="6da81-185">Co je proces požádat o nový server pro cílové prostředí?</span><span class="sxs-lookup"><span data-stu-id="6da81-185">What is the process to request a new server for your target environment?</span></span>|
<span data-ttu-id="6da81-186">Co je průměrná doba vyřízení pro server k dispozici?</span><span class="sxs-lookup"><span data-stu-id="6da81-186">What is the average turnaround time for a server to become available?</span></span>|
<span data-ttu-id="6da81-187">Jaké velikost serveru bude požadovat?</span><span class="sxs-lookup"><span data-stu-id="6da81-187">What size server will you request?</span></span>|

### <a name="accounts"></a><span data-ttu-id="6da81-188">Účty</span><span class="sxs-lookup"><span data-stu-id="6da81-188">Accounts</span></span>

<span data-ttu-id="6da81-189">Nejsou žádné požadavky na účet služby pro nasazení do instance serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="6da81-189">There are no service account requirements to deploy a pull server instance.</span></span> <span data-ttu-id="6da81-190">Existují však scénáře, kde může web spustit v kontextu místního uživatelského účtu.</span><span class="sxs-lookup"><span data-stu-id="6da81-190">However, there are scenarios where the website could run in the context of a local user account.</span></span> <span data-ttu-id="6da81-191">Například pokud je potřeba přístup sdílené složky úložiště pro obsah webu a Windows Server nebo zařízení hostování sdílenou složku úložiště nejsou připojené k doméně.</span><span class="sxs-lookup"><span data-stu-id="6da81-191">For example, if there is a need to access a storage share for website content and either the Windows Server or the device hosting the storage share are not domain joined.</span></span>

### <a name="dns-records"></a><span data-ttu-id="6da81-192">Záznamy DNS</span><span class="sxs-lookup"><span data-stu-id="6da81-192">DNS records</span></span>

<span data-ttu-id="6da81-193">Budete potřebovat název serveru, který má použít při konfiguraci klientů pro práci s prostředím serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="6da81-193">You will need a server name to use when configuring clients to work with a pull server environment.</span></span> <span data-ttu-id="6da81-194">V testovacích prostředích obvykle se používá název hostitele serveru nebo adresu IP serveru lze použít, pokud překlad názvu DNS není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="6da81-194">In test environments, typically the server hostname is used, or the IP address for the server can be used if DNS name resolution is not available.</span></span> <span data-ttu-id="6da81-195">V produkčních prostředích nebo v testovacím prostředí, který reprezentuje produkční nasazení osvědčeným postupem je vytvořit záznam DNS CNAME.</span><span class="sxs-lookup"><span data-stu-id="6da81-195">In production environments or in a lab environment that is intended to represent a production deployment, the best practice is to create a DNS CNAME record.</span></span>

<span data-ttu-id="6da81-196">Záznam CNAME DNS umožňuje vytvořit alias, který bude odkazovat na váš hostitel (A) záznam.</span><span class="sxs-lookup"><span data-stu-id="6da81-196">A DNS CNAME allows you to create an alias to refer to your host (A) record.</span></span> <span data-ttu-id="6da81-197">Další název záznamu je cílem zvyšování flexibility, třeba změnu vyžadovat v budoucnu.</span><span class="sxs-lookup"><span data-stu-id="6da81-197">The intent of the additional name record is to increase flexibility should a change be required in the future.</span></span> <span data-ttu-id="6da81-198">Záznam CNAME pomůžou izolovat konfigurace klienta tak, aby změny prostředí serveru, jako je výměna načítacího serveru nebo přidání dalších vyžádání serverů, nebude vyžadovat odpovídající změny do konfigurace klienta.</span><span class="sxs-lookup"><span data-stu-id="6da81-198">A CNAME can help to isolate the client configuration so that changes to the server environment, such as replacing a pull server or adding additional pull servers, will not require a corresponding change to the client configuration.</span></span>

<span data-ttu-id="6da81-199">Když vyberete název záznamu DNS, uvědomte si architektury řešení.</span><span class="sxs-lookup"><span data-stu-id="6da81-199">When choosing a name for the DNS record, keep the solution architecture in mind.</span></span> <span data-ttu-id="6da81-200">Pokud pomocí vyrovnávání zatížení, bude nutné sdílet stejný název jako záznam DNS certifikát použitý k zabezpečení přenosů přes protokol HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6da81-200">If using load balancing, the certificate used to secure traffic over HTTPS will need to share the same name as the DNS record.</span></span> 

<span data-ttu-id="6da81-201">Scénář</span><span class="sxs-lookup"><span data-stu-id="6da81-201">Scenario</span></span> |<span data-ttu-id="6da81-202">Osvědčený postup</span><span class="sxs-lookup"><span data-stu-id="6da81-202">Best Practice</span></span>
:---|:---
<span data-ttu-id="6da81-203">Testovací prostředí</span><span class="sxs-lookup"><span data-stu-id="6da81-203">Test Environment</span></span> |<span data-ttu-id="6da81-204">Reprodukujte plánované provozní prostředí, pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="6da81-204">Reproduce the planned production environment, if possible.</span></span> <span data-ttu-id="6da81-205">Název hostitele serveru je vhodná pro jednoduché konfigurace.</span><span class="sxs-lookup"><span data-stu-id="6da81-205">A server hostname is suitable for simple configurations.</span></span> <span data-ttu-id="6da81-206">Pokud DNS není k dispozici, může místo název hostitele použít IP adresu.</span><span class="sxs-lookup"><span data-stu-id="6da81-206">If DNS is not available, an IP address may be used in lieu of a hostname.</span></span>|
<span data-ttu-id="6da81-207">Nasazení jednoho uzlu</span><span class="sxs-lookup"><span data-stu-id="6da81-207">Single Node Deployment</span></span> |<span data-ttu-id="6da81-208">Vytvořte záznam DNS CNAME, který odkazuje na název hostitele serveru.</span><span class="sxs-lookup"><span data-stu-id="6da81-208">Create a DNS CNAME record that points to the server hostname.</span></span>|

<span data-ttu-id="6da81-209">Další informace najdete v tématu [konfigurování kruhové dotazování DNS v systému Windows Server](https://technet.microsoft.com/en-us/library/cc787484(v=ws.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="6da81-209">For more information, see [Configuring DNS Round Robin in Windows Server](https://technet.microsoft.com/en-us/library/cc787484(v=ws.10).aspx).</span></span>

<span data-ttu-id="6da81-210">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="6da81-210">Planning task</span></span>|
---|
<span data-ttu-id="6da81-211">Víte, kdo má záznamy DNS vytvořené a změněné kontaktovat?</span><span class="sxs-lookup"><span data-stu-id="6da81-211">Do you know who to contact to have DNS records created and changed?</span></span>|
<span data-ttu-id="6da81-212">Jaká je průměrná vyřízení pro žádost o záznam DNS?</span><span class="sxs-lookup"><span data-stu-id="6da81-212">What is the average turnaround for a request for a DNS record?</span></span>|
<span data-ttu-id="6da81-213">Je třeba požádat o statické záznamy hostitele (A) pro servery?</span><span class="sxs-lookup"><span data-stu-id="6da81-213">Do you need to request static Hostname (A) records for servers?</span></span>|
<span data-ttu-id="6da81-214">Co se vám požadavku jako záznam CNAME?</span><span class="sxs-lookup"><span data-stu-id="6da81-214">What will you request as a CNAME?</span></span>|
<span data-ttu-id="6da81-215">V případě potřeby, jaký typ Vyrovnávání zatížení řešení bude využíváte?</span><span class="sxs-lookup"><span data-stu-id="6da81-215">If needed, what type of Load Balancing solution will you utilize?</span></span> <span data-ttu-id="6da81-216">(viz část s názvem Vyrovnávání zatížení podrobnosti)</span><span class="sxs-lookup"><span data-stu-id="6da81-216">(see section titled Load Balancing for details)</span></span>|

### <a name="public-key-infrastructure"></a><span data-ttu-id="6da81-217">Infrastruktura veřejných klíčů</span><span class="sxs-lookup"><span data-stu-id="6da81-217">Public Key Infrastructure</span></span>

<span data-ttu-id="6da81-218">Většina organizací dnes vyžadují, aby síťový provoz, zejména provoz, který zahrnuje takové citlivá data, jak jsou servery konfigurované, musí být ověřen nebo během přenosu šifrována.</span><span class="sxs-lookup"><span data-stu-id="6da81-218">Most organizations today require that network traffic, especially traffic that includes such sensitive data as how servers are configured, must be validated and/or encrypted during transit.</span></span> <span data-ttu-id="6da81-219">Když je možné nasadit vyžádání obsahu server pomocí protokolu HTTP, což usnadňuje požadavky klientů v prostý text, je osvědčeným postupem zabezpečení provozu pomocí protokolu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6da81-219">While it is possible to deploy a pull server using HTTP which facilitates client requests in clear text, it is a best practice to secure traffic using HTTPS.</span></span> <span data-ttu-id="6da81-220">Službu lze nakonfigurovat k využívání HTTPS pomocí sady parametrů v prostředek DSC **xPSDesiredStateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="6da81-220">The service can be configured to use HTTPS using a set of parameters in the DSC resource **xPSDesiredStateConfiguration**.</span></span>

<span data-ttu-id="6da81-221">Požadavky na certifikát k zabezpečení přenosů HTTPS pro vyžádání obsahu server nejsou jiné než zabezpečení jakékoli jiný webový server HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6da81-221">The certificate requirements to secure HTTPS traffic for pull server are not different than securing any other HTTPS web site.</span></span> <span data-ttu-id="6da81-222">**Webový Server** šablonu služby Windows Server certifikátů splňuje požadované možnosti.</span><span class="sxs-lookup"><span data-stu-id="6da81-222">The **Web Server** template in a Windows Server Certificate Services satisfies the required capabilities.</span></span>

<span data-ttu-id="6da81-223">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="6da81-223">Planning task</span></span>|
---|
<span data-ttu-id="6da81-224">Pokud nejsou automatizované žádosti o certifikát, který budete potřebovat obraťte se na požadavky na certifikát?</span><span class="sxs-lookup"><span data-stu-id="6da81-224">If certificate requests are not automated, who will you need to contact to requests a certificate?</span></span>|
<span data-ttu-id="6da81-225">Jaká je průměrná vyřízení žádosti?</span><span class="sxs-lookup"><span data-stu-id="6da81-225">What is the average turnaround for the request?</span></span>|
<span data-ttu-id="6da81-226">Jak bude na vás přenést soubor certifikátu?</span><span class="sxs-lookup"><span data-stu-id="6da81-226">How will the certificate file be transferred to you?</span></span>|
<span data-ttu-id="6da81-227">Jak se vám převede privátní klíč certifikátu?</span><span class="sxs-lookup"><span data-stu-id="6da81-227">How will the certificate private key be transferred to you?</span></span>|
<span data-ttu-id="6da81-228">Jak dlouho je výchozí doba vypršení platnosti?</span><span class="sxs-lookup"><span data-stu-id="6da81-228">How long is the default expiration time?</span></span>|
<span data-ttu-id="6da81-229">Mít vyrovnané na název DNS pro prostředí serveru vyžádání obsahu, který můžete použít pro název certifikátu?</span><span class="sxs-lookup"><span data-stu-id="6da81-229">Have you settled on a DNS name for the pull server environment, that you can use for the certificate name?</span></span>|

### <a name="choosing-an-architecture"></a><span data-ttu-id="6da81-230">Výběr architekturu</span><span class="sxs-lookup"><span data-stu-id="6da81-230">Choosing an architecture</span></span>

<span data-ttu-id="6da81-231">Vyžádání obsahu server se dá nasadit pomocí služby web hostované na IIS nebo sdílenou složku SMB.</span><span class="sxs-lookup"><span data-stu-id="6da81-231">A pull server can be deployed using either a web service hosted on IIS, or an SMB file share.</span></span> <span data-ttu-id="6da81-232">Ve většině případů bude možnosti webové služby poskytují větší flexibilitu.</span><span class="sxs-lookup"><span data-stu-id="6da81-232">In most situations, the web service option will provide greater flexibility.</span></span> <span data-ttu-id="6da81-233">Není komunikaci přes protokol HTTPS napříč síťovými hranicemi, zatímco přenosy SMB je často filtrované blokované nebo mezi sítěmi.</span><span class="sxs-lookup"><span data-stu-id="6da81-233">It is not uncommon for HTTPS traffic to traverse network boundaries, whereas SMB traffic is often filtered or blocked between networks.</span></span> <span data-ttu-id="6da81-234">Webová služba také nabízí možnost zahrnout Server shoda nebo Reporting správce webu (i témata vzít v úvahu v budoucí verzi tohoto dokumentu), poskytují mechanismus pro klienty odesílat zprávy o stavu zpět na server pro centralizované viditelnosti.</span><span class="sxs-lookup"><span data-stu-id="6da81-234">The web service also offers the option to include a Conformance Server or Web Reporting Manager (both topics to be addressed in a future version of this document) that provide a mechanism for clients to report status back to a server for centralized visibility.</span></span> <span data-ttu-id="6da81-235">SMB nabízí možnost v prostředích, kde zásady stanoví, že webový server by neměl být využité a další požadavky prostředí, které role Webový server nežádoucí.</span><span class="sxs-lookup"><span data-stu-id="6da81-235">SMB provides an option for environments where policy dictates that a web server should not be utilized, and for other environmental requirements that make a web server role undesirable.</span></span> <span data-ttu-id="6da81-236">V obou případech musíte vyhodnotit požadavky na podepisování a šifrování komunikace.</span><span class="sxs-lookup"><span data-stu-id="6da81-236">In either case, remember to evaluate the requirements for signing and encrypting traffic.</span></span> <span data-ttu-id="6da81-237">Protokol HTTPS, podepisování SMB a zásady protokolu IPSEC jsou všechny možnosti vhodné zvažování.</span><span class="sxs-lookup"><span data-stu-id="6da81-237">HTTPS, SMB signing, and IPSEC policies are all options worth considering.</span></span>

#### <a name="load-balancing"></a><span data-ttu-id="6da81-238">Vyrovnávání zatížení</span><span class="sxs-lookup"><span data-stu-id="6da81-238">Load balancing</span></span>  
<span data-ttu-id="6da81-239">Klienti interakci s webovou službou může požádat o informace, které je vrácený v odpověď o jedné.</span><span class="sxs-lookup"><span data-stu-id="6da81-239">Clients interacting with the web service make a request for information that is returned in a single response.</span></span> <span data-ttu-id="6da81-240">Žádné sekvenční požadavky jsou povinné, takže není nutné pro platformu, která Ujistěte se, že relace udržované na jednom serveru v libovolném bodě v čase Vyrovnávání zatížení.</span><span class="sxs-lookup"><span data-stu-id="6da81-240">No sequential requests are required, so it is not necessary for the load balancing platform to ensure sessions are maintained on a single server at any point in time.</span></span>

<span data-ttu-id="6da81-241">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="6da81-241">Planning task</span></span>|
---|
<span data-ttu-id="6da81-242">Jaká řešení se použije pro vyrovnávání zatížení provozu napříč servery?</span><span class="sxs-lookup"><span data-stu-id="6da81-242">What solution will be used for load balancing traffic across servers?</span></span>|
<span data-ttu-id="6da81-243">Pokud se používá Vyrovnávání zatížení hardwaru, který bude trvat žádost o přidání novou konfiguraci zařízení?</span><span class="sxs-lookup"><span data-stu-id="6da81-243">If using a hardware load balancer, who will take a request to add a new configuration to the device?</span></span>|
<span data-ttu-id="6da81-244">Co je průměrná vyřízení požadavku konfigurace nového zatížení vyrovnáváním webovou službu?</span><span class="sxs-lookup"><span data-stu-id="6da81-244">What is the average turnaround for a request to configure a new load balanced web service?</span></span>|
<span data-ttu-id="6da81-245">Jaké informace budou potřeba pro požadavek?</span><span class="sxs-lookup"><span data-stu-id="6da81-245">What information will be required for the request?</span></span>|
<span data-ttu-id="6da81-246">Budete potřebovat k vyžádání dalších IP adresy nebo týmem zodpovědný za vyrovnávání zatížení zpracovává který?</span><span class="sxs-lookup"><span data-stu-id="6da81-246">Will you need to request an additional IP or will the team responsible for load balancing handle that?</span></span>|
<span data-ttu-id="6da81-247">Máte k dispozici záznamy DNS, které jsou potřebné a bude to vyžadovat tým zodpovědná za konfiguraci řešení vyrovnávání zatížení?</span><span class="sxs-lookup"><span data-stu-id="6da81-247">Do you have the DNS records needed, and will this be required by the team responsible for configuring the load balancing solution?</span></span>|
<span data-ttu-id="6da81-248">Řešení vyrovnávání zatížení vyžaduje, aby zařízení zpracovávat infrastruktury veřejných KLÍČŮ nebo můžete ho Vyrovnávání zatížení, které přenosy HTTPS, dokud nejsou žádné požadavky relace?</span><span class="sxs-lookup"><span data-stu-id="6da81-248">Does the load balancing solution require that PKI be handled by the device or can it load balance HTTPS traffic as long as there are no session requirements?</span></span>|

### <a name="staging-configurations-and-modules-on-the-pull-server"></a><span data-ttu-id="6da81-249">Konfigurace pracovní a modulů na tomto serveru</span><span class="sxs-lookup"><span data-stu-id="6da81-249">Staging configurations and modules on the pull server</span></span>

<span data-ttu-id="6da81-250">Jako součást plánování konfigurace musíte se zamyslet, o které DSC se bude hostovat modulů a konfigurací serverem pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="6da81-250">As part of configuration planning, you will need to think about which DSC modules and configurations will be hosted by the pull server.</span></span> <span data-ttu-id="6da81-251">Pro účely plánování konfigurace je důležité mít základní znalosti o tom, jak připravit a nasadit obsah na server vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="6da81-251">For the purpose of configuration planning it is important to have a basic understanding of how to prepare and deploy content to a pull server.</span></span> 

<span data-ttu-id="6da81-252">V budoucnu v této části se rozšířit a zahrnuty v provozní příručce pro serveru vyžádané replikace s DSC.</span><span class="sxs-lookup"><span data-stu-id="6da81-252">In the future, this section will be expanded and included in an Operations Guide for DSC Pull Server.</span></span>  <span data-ttu-id="6da81-253">V Průvodci zabývat den proces pro správu modulů a konfigurací v čase s automatizace.</span><span class="sxs-lookup"><span data-stu-id="6da81-253">The guide will discuss the day to day process for managing modules and configurations over time with automation.</span></span> 

#### <a name="dsc-modules"></a><span data-ttu-id="6da81-254">Moduly DSC</span><span class="sxs-lookup"><span data-stu-id="6da81-254">DSC modules</span></span>  
<span data-ttu-id="6da81-255">Klienty, kteří požadují konfiguraci bude nutné požadované moduly DSC.</span><span class="sxs-lookup"><span data-stu-id="6da81-255">Clients that request a configuration will need the required DSC modules.</span></span> <span data-ttu-id="6da81-256">Funkce serveru pro vyžádání obsahu je automatizovat distribuci na vyžádání DSC moduly klientům.</span><span class="sxs-lookup"><span data-stu-id="6da81-256">A functionality of the pull server is to automate distribution on demand of DSC modules to clients.</span></span> <span data-ttu-id="6da81-257">Pokud nasadíte načítacího serveru poprvé, třeba jako testovacího prostředí nebo testování konceptu, pravděpodobně chcete závisí na DSC moduly, které jsou dostupné z veřejných úložišť, jako je například Galerie prostředí PowerShell nebo úložišť PowerShell.org GitHub pro moduly DSC .</span><span class="sxs-lookup"><span data-stu-id="6da81-257">If you are deploying a pull server for the first time, perhaps as a lab or proof of concept, you are likely going to depend on DSC modules that are available from public repositories such as the PowerShell Gallery or the PowerShell.org GitHub repositories for DSC modules.</span></span>

<span data-ttu-id="6da81-258">Je důležité si pamatovat, že i pro důvěryhodné online zdrojů, jako je například Galerie prostředí PowerShell, libovolný modul, který byl stažen z veřejného úložiště by měl být zkontrolovány uživatelem někdo pomocí prostředí PowerShell a znalosti o prostředí, kde budou moduly použít před používá v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="6da81-258">It is critical to remember that even for trusted online sources such as the PowerShell Gallery, any module that is downloaded from a public repository should be reviewed by someone with PowerShell experience and knowledge of the environment where the modules will be used prior to being used in production.</span></span> <span data-ttu-id="6da81-259">Při dokončení této úlohy je vhodná doba zkontrolujte všechny další datové části v modulu, který lze odebrat například dokumentaci a ukázkové skripty.</span><span class="sxs-lookup"><span data-stu-id="6da81-259">While completing this task it is a good time to check for any additional payload in the module that can be removed such as documentation and example scripts.</span></span> <span data-ttu-id="6da81-260">Tím se sníží šířku pásma sítě pro každého klienta v jejich první žádost, když moduly budou staženy přes síť ze serveru do klienta.</span><span class="sxs-lookup"><span data-stu-id="6da81-260">This will reduce the network bandwidth per client in their first request, when modules will be downloaded over the network from server to client.</span></span>

<span data-ttu-id="6da81-261">Každý modul musí být zabalené v konkrétním formátu ZIP soubor s názvem ModuleName_Version.zip, který obsahuje datové části modulu.</span><span class="sxs-lookup"><span data-stu-id="6da81-261">Each module must be packaged in a specific format, a ZIP file named ModuleName_Version.zip that contains the module payload.</span></span> <span data-ttu-id="6da81-262">Po zkopírování souboru na server musí být vytvořeny soubor kontrolního součtu.</span><span class="sxs-lookup"><span data-stu-id="6da81-262">After the file is copied to the server a checksum file must be created.</span></span> <span data-ttu-id="6da81-263">Pokud se klienti připojují k serveru, kontrolního součtu se používá k ověření, že obsah DSC modul nebylo změněno, protože byla publikována.</span><span class="sxs-lookup"><span data-stu-id="6da81-263">When clients connect to the server, the checksum is used to verify the content of the DSC module has not changed since it was published.</span></span>

```powershell
New-DscCheckSum -ConfigurationPath .\ -OutPath .\
```

<span data-ttu-id="6da81-264">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="6da81-264">Planning task</span></span>|
---|
<span data-ttu-id="6da81-265">Pokud plánujete testu nebo testovacím prostředí, které scénáře jsou klíčem k ověření?</span><span class="sxs-lookup"><span data-stu-id="6da81-265">If you are planning a test or lab environment which scenarios are key to validate?</span></span>|
<span data-ttu-id="6da81-266">Jsou veřejně dostupné moduly, které obsahují prostředky tak, aby pokrývalo vše, co potřebujete, nebo budete potřebovat vytvořit vaše vlastní prostředky?</span><span class="sxs-lookup"><span data-stu-id="6da81-266">Are there publicly available modules that contain resources to cover everything you need or will you need to author your own resources?</span></span>|
<span data-ttu-id="6da81-267">Prostředí, budou mít přístup k Internetu k načtení veřejné moduly?</span><span class="sxs-lookup"><span data-stu-id="6da81-267">Will your environment have Internet access to retrieve public modules?</span></span>|
<span data-ttu-id="6da81-268">Kdo je zodpovědná za kontrola DSC moduly?</span><span class="sxs-lookup"><span data-stu-id="6da81-268">Who will be responsible for reviewing DSC modules?</span></span>|
<span data-ttu-id="6da81-269">Pokud plánujete provozním prostředí co použijete jako místní úložiště pro ukládání DSC moduly?</span><span class="sxs-lookup"><span data-stu-id="6da81-269">If you are planning a production environment what will you use as a local repository for storing DSC modules?</span></span>|
<span data-ttu-id="6da81-270">Přijme centrální tým moduly DSC z týmy aplikací?</span><span class="sxs-lookup"><span data-stu-id="6da81-270">Will a central team accept DSC modules from application teams?</span></span> <span data-ttu-id="6da81-271">Co bude tento proces?</span><span class="sxs-lookup"><span data-stu-id="6da81-271">What will the process be?</span></span>|
<span data-ttu-id="6da81-272">Je balení, kopírování a vytváření kontrolních součtů pro produkční prostředí DSC moduly na server z vaší zdrojové úložiště bude automatizovat?</span><span class="sxs-lookup"><span data-stu-id="6da81-272">Will you automate packaging, copying, and creating a checksum for production-ready DSC modules to the server, from your source repo?</span></span>|
<span data-ttu-id="6da81-273">Bude váš tým zodpovědní za správu platformou automatizace?</span><span class="sxs-lookup"><span data-stu-id="6da81-273">Will your team be responsible for managing the automation platform as well?</span></span>|

#### <a name="dsc-configurations"></a><span data-ttu-id="6da81-274">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="6da81-274">DSC configurations</span></span>

<span data-ttu-id="6da81-275">Účelem serveru pro vyžádání obsahu je zajistit centralizovanou mechanismus pro distribuci konfigurací DSC uzlů klientů.</span><span class="sxs-lookup"><span data-stu-id="6da81-275">The purpose of a pull server is to provide a centralized mechanism for distributing DSC configurations to client nodes.</span></span> <span data-ttu-id="6da81-276">Konfigurace jsou uloženy na serveru jako MOF dokumenty.</span><span class="sxs-lookup"><span data-stu-id="6da81-276">The configurations are stored on the server as MOF documents.</span></span> <span data-ttu-id="6da81-277">Každý dokument budou mít názvy jedinečný identifikátor GUID.</span><span class="sxs-lookup"><span data-stu-id="6da81-277">Each document will be named with a unique GUID.</span></span> <span data-ttu-id="6da81-278">Pokud jsou klienti nakonfigurovaní pro připojení k serveru vyžádané replikace, jsou také uvedeny identifikátor GUID pro konfiguraci, kterou by měl žádat o.</span><span class="sxs-lookup"><span data-stu-id="6da81-278">When clients are configured to connect with a pull server, they are also given the GUID for the configuration they should request.</span></span> <span data-ttu-id="6da81-279">Tento systém odkazující na konfigurace pomocí identifikátoru GUID zaručuje globální jedinečnost a je flexibilní, tak, aby konfigurace lze použít s rozlišením na uzel, nebo jako konfiguraci role, která zahrnuje mnoho serverů, které by měl mít identické konfigurace.</span><span class="sxs-lookup"><span data-stu-id="6da81-279">This system of referencing configurations by GUID guarantees global uniqueness and is flexible such that a configuration can be applied with granularity per node, or as a role configuration that spans many servers that should have identical configurations.</span></span>

#### <a name="guids"></a><span data-ttu-id="6da81-280">Identifikátory GUID</span><span class="sxs-lookup"><span data-stu-id="6da81-280">GUIDs</span></span>

<span data-ttu-id="6da81-281">Plánování konfigurace identifikátory GUID je vhodné další pozornost, pokud se rozhodujete nasazení na server vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="6da81-281">Planning for configuration GUIDs is worth additional attention when thinking through a pull server deployment.</span></span> <span data-ttu-id="6da81-282">Neexistuje žádný konkrétní požadavek pro identifikátory GUID zpracování a proces je pravděpodobně být jedinečný pro každé prostředí.</span><span class="sxs-lookup"><span data-stu-id="6da81-282">There is no specific requirement for how to handle GUIDs and the process is likely to be unique for each environment.</span></span> <span data-ttu-id="6da81-283">Proces může být v rozsahu od jednoduchého do komplexní: centrálně uloženého souboru CSV, jednoduché tabulku SQL, databáze CMDB nebo komplexní řešení, které vyžadují integraci s jiné nástroje nebo softwaru řešení.</span><span class="sxs-lookup"><span data-stu-id="6da81-283">The process can range from simple to complex: a centrally stored CSV file, a simple SQL table, a CMDB, or a complex solution requiring integration with another tool or software solution.</span></span> <span data-ttu-id="6da81-284">Existují dvě obecné přístupy:</span><span class="sxs-lookup"><span data-stu-id="6da81-284">There are two general approaches:</span></span>

 - <span data-ttu-id="6da81-285">**Přiřazení identifikátory GUID na server** – poskytuje míru zajištění, že každý konfigurace serveru je řízena jednotlivě.</span><span class="sxs-lookup"><span data-stu-id="6da81-285">**Assigning GUIDs per server** — Provides a measure of assurance that every server configuration is controlled individually.</span></span> <span data-ttu-id="6da81-286">To poskytuje úroveň přesnost kolem aktualizace a může fungovat i v prostředí s několika servery.</span><span class="sxs-lookup"><span data-stu-id="6da81-286">This provides a level of precision around updates and can work well in environments with few servers.</span></span>
 - <span data-ttu-id="6da81-287">**Přiřazení identifikátory GUID podle role serveru** – všechny servery, které provádí stejnou funkci, jako jsou třeba webové servery používají stejný identifikátor GUID jako odkaz požadovaná konfigurační data.</span><span class="sxs-lookup"><span data-stu-id="6da81-287">**Assigning GUIDs per server role** — All servers that perform the same function, such as web servers, use the same GUID to reference the required configuration data.</span></span>  <span data-ttu-id="6da81-288">Upozorňujeme, že pokud mnoho servery sdílejí stejný identifikátor GUID, všechny z nich by aktualizován současně při změny v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="6da81-288">Be aware that if many servers share the same GUID, all of them would be updated simultaneously when the configuration changes.</span></span>

<span data-ttu-id="6da81-289">Identifikátor GUID je něco, co by měly zvažovat citlivá data, protože mohou být využity uživatel se zlými úmysly k získání zjištěných informací o tom, jak nasadit servery a ve svém prostředí nakonfigurováno.</span><span class="sxs-lookup"><span data-stu-id="6da81-289">The GUID is something that should be considered sensitive data because it could be leveraged by someone with malicious intent to gain intelligence about how servers are deployed and configured in your environment.</span></span> <span data-ttu-id="6da81-290">Další informace najdete v tématu [bezpečně přidělování identifikátorů GUID v režimu prostředí PowerShell požadovaného stavu konfigurace pro vyžádání obsahu](http://blogs.msdn.com/b/powershell/archive/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode.aspx).</span><span class="sxs-lookup"><span data-stu-id="6da81-290">For more information, see [Securely allocating GUIDs in PowerShell Desired State Configuration Pull Mode](http://blogs.msdn.com/b/powershell/archive/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode.aspx).</span></span>

<span data-ttu-id="6da81-291">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="6da81-291">Planning task</span></span>|
---|
<span data-ttu-id="6da81-292">Kdo je zodpovědná za kopírování konfigurace v ke složce pro vyžádání obsahu server, jakmile jsou připravené?</span><span class="sxs-lookup"><span data-stu-id="6da81-292">Who will be responsible for copying configurations in to the pull server folder when they are ready?</span></span>|
<span data-ttu-id="6da81-293">Pokud konfigurace vytvořené týmem aplikace, co proces bude přebírají je?</span><span class="sxs-lookup"><span data-stu-id="6da81-293">If Configurations are authored by an application team, what will the process be to hand them off?</span></span>|
<span data-ttu-id="6da81-294">Můžete využít úložiště k ukládání konfigurace, protože se právě vytvořené, mezi týmy?</span><span class="sxs-lookup"><span data-stu-id="6da81-294">Will you leverage a repository to store configurations as they are being authored, across teams?</span></span>|
<span data-ttu-id="6da81-295">Se dá automatizovat proces kopírování konfigurace na server a vytváření kontrolní součet, jakmile jsou připravené?</span><span class="sxs-lookup"><span data-stu-id="6da81-295">Will you automate the process of copying configurations to the server and creating a checksum when they are ready?</span></span>|
<span data-ttu-id="6da81-296">Jak budou namapujete identifikátory GUID na servery nebo role, a to uložení?</span><span class="sxs-lookup"><span data-stu-id="6da81-296">How will you map GUIDs to servers or roles, and where will this be stored?</span></span>|
<span data-ttu-id="6da81-297">Co můžete používat jako proces ke konfiguraci klientských počítačů, a způsobu, jakým bude ji integrovat váš proces pro vytváření a ukládání identifikátory GUID konfigurace?</span><span class="sxs-lookup"><span data-stu-id="6da81-297">What will you use as a process to configure client machines, and how will it integrate with your process for creating and storing Configuration GUIDs?</span></span>|

## <a name="installation-guide"></a><span data-ttu-id="6da81-298">Průvodce instalací</span><span class="sxs-lookup"><span data-stu-id="6da81-298">Installation Guide</span></span>

<span data-ttu-id="6da81-299">*Skripty zadané v tomto dokumentu jsou stabilní příklady. Vždy zkontrolujte si důkladně skripty před provedením jejich v produkčním prostředí.*</span><span class="sxs-lookup"><span data-stu-id="6da81-299">*Scripts given in this document are stable examples. Always review scripts carefully before executing them in a production environment.*</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6da81-300">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="6da81-300">Prerequisites</span></span>

<span data-ttu-id="6da81-301">Ověření verze prostředí PowerShell na serveru použijte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="6da81-301">To verify the version of PowerShell on your server use the following command.</span></span>

```powershell
$PSVersionTable.PSVersion
```

<span data-ttu-id="6da81-302">Pokud je to možné upgradujte na nejnovější verzi Windows Management Framework.</span><span class="sxs-lookup"><span data-stu-id="6da81-302">If possible, upgrade to the latest version of Windows Management Framework.</span></span>
<span data-ttu-id="6da81-303">V dalším kroku Stáhnout `xPsDesiredStateConfiguration` modulu pomocí následujícího příkazu.</span><span class="sxs-lookup"><span data-stu-id="6da81-303">Next, download the `xPsDesiredStateConfiguration` module using the following command.</span></span>


```powershell
Install-Module xPSDesiredStateConfiguration
```

<span data-ttu-id="6da81-304">Příkaz vyzve ke schválení před stažením modulu.</span><span class="sxs-lookup"><span data-stu-id="6da81-304">The command will ask for your approval before downloading the module.</span></span>

### <a name="installation-and-configuration-scripts"></a><span data-ttu-id="6da81-305">Instalace a konfigurace skriptů</span><span class="sxs-lookup"><span data-stu-id="6da81-305">Installation and configuration scripts</span></span>
-

<span data-ttu-id="6da81-306">Je nejlepší metody nasadit server DSC za použití skriptu konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="6da81-306">The best method to deploy a DSC pull server is to use a DSC configuration script.</span></span> <span data-ttu-id="6da81-307">Tento dokument nabídne skripty, včetně obě základní nastavení, které by konfigurovat jenom DSC webovou službu a upřesňující nastavení, která by konfigurovat Windows Server začátku do konce včetně DSC webové služby.</span><span class="sxs-lookup"><span data-stu-id="6da81-307">This document will present scripts including both basic settings that would configure only the DSC web service and advanced settings that would configure a Windows Server end-to-end including DSC web service.</span></span>

<span data-ttu-id="6da81-308">Poznámka: Aktuálně `xPSDesiredStateConfiguation` DSC modulu vyžaduje server jako národní prostředí cs-cz.</span><span class="sxs-lookup"><span data-stu-id="6da81-308">Note:  Currently the `xPSDesiredStateConfiguation` DSC module requires the server to be EN-US locale.</span></span>

### <a name="basic-configuration-for-windows-server-2012"></a><span data-ttu-id="6da81-309">Základní konfigurace pro Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="6da81-309">Basic configuration for Windows Server 2012</span></span>
-------------------------------------------
```powershell
# This is a very basic Configuration to deploy a pull server instance in a lab environment on Windows Server 2012.

Configuration PullServer {
Import-DscResource -ModuleName xPSDesiredStateConfiguration

        # Load the Windows Server DSC Service feature
        WindowsFeature DSCServiceFeature
        {
          Ensure = 'Present'
          Name = 'DSC-Service'
        }

        # Use the DSC Resource to simplify deployment of the web service
        xDSCWebService PSDSCPullServer
        {
          Ensure = 'Present'
          EndpointName = 'PSDSCPullServer'
          Port = 8080
          PhysicalPath = "$env:SYSTEMDRIVE\inetpub\wwwroot\PSDSCPullServer"
          CertificateThumbPrint = 'AllowUnencryptedTraffic'
          ModulePath = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
          ConfigurationPath = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
          State = 'Started'
          DependsOn = '[WindowsFeature]DSCServiceFeature'
        }
}
PullServer -OutputPath 'C:\PullServerConfig\'
Start-DscConfiguration -Wait -Force -Verbose -Path 'C:\PullServerConfig\'
```

### <a name="advanced-configuration-for-windows-server-2012-r2"></a><span data-ttu-id="6da81-310">Upřesňující konfigurace pro Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="6da81-310">Advanced configuration for Windows Server 2012 R2</span></span>

```powershell
# This is an advanced Configuration example for Pull Server production deployments on Windows Server 2012 R2.
# Many of the features demonstrated are optional and provided to demonstrate how to adapt the Configuration for multiple scenarios
# Select the needed resources based on the requirements for each environment.
# Optional scenarios include:
#      * Reduce footprint to Server Core
#      * Rename server and join domain
#      * Switch from SSL to TLS for HTTPS
#      * Automatically load certificate from Certificate Authority
#      * Locate Modules and Configuration data on remote SMB share
#      * Manage state of default websites in IIS
    
param (
        [Parameter(Mandatory=$true)] 
        [ValidateNotNullorEmpty()] 
        [System.String] $ServerName,
        [System.String] $DomainName,
        [System.String] $CARootName,
        [System.String] $CAServerFQDN,
        [System.String] $CertSubject,
        [System.String] $SMBShare,
        [Parameter(Mandatory=$true)] 
        [ValidateNotNullorEmpty()] 
        [PsCredential] $Credential
    )
    
Configuration PullServer {
    Import-DscResource -ModuleName xPSDesiredStateConfiguration, xWebAdministration, xCertificate, xComputerManagement
    Node localhost
    {
            
        # Configure the server to automatically corret configuration drift including reboots if needed.
        LocalConfigurationManager
        {
            ConfigurationMode = 'ApplyAndAutoCorrect'
            RebootNodeifNeeded = $node.RebootNodeifNeeded
            CertificateId = $node.Thumbprint
        }
    
        # Remove all GUI interfaces so the server has minimum running footprint.
        WindowsFeature ServerCore
        {
            Ensure = 'Absent'
            Name = 'User-Interfaces-Infra'
        }
    
        # Set the server name and if needed, join a domain. If not joining a domain, remove the DomainName parameter.
        xComputer DomainJoin
        {
            Name = $Node.ServerName
            DomainName = $Node.DomainName
            Credential = $Node.Credential
        }
    
        # The next series of settings disable SSL and enable TLS, for environments where that is required by policy.
        Registry TLS1_2ServerEnabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'
            ValueName = 'Enabled'
            ValueData = 1
            ValueType = 'Dword'
        }
        Registry TLS1_2ServerDisabledByDefault
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'
            ValueName = 'DisabledByDefault'
            ValueData = 0
            ValueType = 'Dword'
        }
        Registry TLS1_2ClientEnabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'
            ValueName = 'Enabled'
            ValueData = 1
            ValueType = 'Dword'
        }
        Registry TLS1_2ClientDisabledByDefault
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'
            ValueName = 'DisabledByDefault'
            ValueData = 0
            ValueType = 'Dword'
        }
        Registry SSL2ServerDisabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server'
            ValueName = 'Enabled'
            ValueData = 0
            ValueType = 'Dword'
        }
    
        # Install the Windows Server DSC Service feature
        WindowsFeature DSCServiceFeature
        {
            Ensure = 'Present'
            Name = 'DSC-Service'
        }
    
        # If using a certificate from a local Active Directory Enterprise Root Certificate Authority, complete a request and install the certificate
        xCertReq SSLCert
        {
            CARootName = $Node.CARootName
            CAServerFQDN = $Node.CAServerFQDN
            Subject = $Node.CertSubject
            AutoRenew = $Node.AutoRenew
            Credential = $Node.Credential
        }
    
        # Use the DSC resource to simplify deployment of the web service.  You might also consider modifying the default port, possibly leveraging port 443 in environments where that is enforced as a standard.
        xDSCWebService PSDSCPullServer
        {
            Ensure = 'Present'
            EndpointName = 'PSDSCPullServer'
            Port = 8080
            PhysicalPath = "$env:SYSTEMDRIVE\inetpub\wwwroot\PSDSCPullServer"
            CertificateThumbPrint = 'CertificateSubject'
            CertificateSubject = $Node.CertSubject
            ModulePath = "$($Node.SMBShare)\DscService\Modules"
            ConfigurationPath = "$($Node.SMBShare)\DscService\Configuration"
            State = 'Started'
            DependsOn = '[WindowsFeature]DSCServiceFeature'
        }
    
        # Validate web config file contains current DB settings
        xWebConfigKeyValue CorrectDBProvider
        { 
            ConfigSection = 'AppSettings'
            Key = 'dbprovider'
            Value = 'System.Data.OleDb'
            WebsitePath = 'IIS:\sites\PSDSCPullServer'
            DependsOn = '[xDSCWebService]PSDSCPullServer'
        }
        xWebConfigKeyValue CorrectDBConnectionStr
        { 
            ConfigSection = 'AppSettings'
            Key = 'dbconnectionstr'
            Value = 'Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Program Files\WindowsPowerShell\DscService\Devices.mdb;'
            WebsitePath = 'IIS:\sites\PSDSCPullServer'
            DependsOn = '[xDSCWebService]PSDSCPullServer'
        }
    
        # Stop the default website
        xWebsite StopDefaultSite  
        { 
            Ensure = 'Present'
            Name = 'Default Web Site'
            State = 'Stopped'
            PhysicalPath = 'C:\inetpub\wwwroot'
            DependsOn = '[WindowsFeature]DSCServiceFeature'
        }
    }
}
$configData = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            ServerName = $ServerName
            DomainName = $DomainName
            CARootName = $CARootName
            CAServerFQDN = $CAServerFQDN
            CertSubject = $CertSubject
            AutoRenew = $true
            SMBShare = $SMBShare
            Credential = $Credential
            RebootNodeifNeeded = $true
            CertificateFile = 'c:\PullServerConfig\Cert.cer'
            Thumbprint = 'B9A39921918B466EB1ADF2509E00F5DECB2EFDA9'
            }
        )
    }
PullServer -ConfigurationData $configData -OutputPath 'C:\PullServerConfig\'
Set-DscLocalConfigurationManager -ComputerName localhost -Path 'C:\PullServerConfig\'
Start-DscConfiguration -Wait -Force -Verbose -Path 'C:\PullServerConfig\'
    
# .\Script.ps1 -ServerName web1 -domainname 'test.pha' -carootname 'test-dc01-ca' -caserverfqdn 'dc01.test.pha' -certsubject 'CN=service.test.pha' -smbshare '\\sofs1.test.pha\share' 
```


### <a name="verify-pull-server-functionality"></a><span data-ttu-id="6da81-311">Ověřte funkčnost serveru vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="6da81-311">Verify pull server functionality</span></span>

```powershell
# This function is meant to simplify a check against a DSC pull server. If you do not use the default service URL, you will need to adjust accordingly.
function Verify-DSCPullServer ($fqdn) {
    ([xml](invoke-webrequest "https://$($fqdn):8080/psdscpullserver.svc" | % Content)).service.workspace.collection.href
}
Verify-DSCPullServer 'INSERT SERVER FQDN' 

Expected Result:
Action
Module
StatusReport
Node
```

### <a name="configure-clients"></a><span data-ttu-id="6da81-312">Konfigurace klientů</span><span class="sxs-lookup"><span data-stu-id="6da81-312">Configure clients</span></span>

```powershell
Configuration PullClient {
    param(
    $ID,
    $Server
    )
        LocalConfigurationManager 
                { 
                    ConfigurationID = $ID;
                    RefreshMode = 'PULL';
                    DownloadManagerName = 'WebDownloadManager';
                    RebootNodeIfNeeded = $true;
                    RefreshFrequencyMins = 30;
                    ConfigurationModeFrequencyMins = 15; 
                    ConfigurationMode = 'ApplyAndAutoCorrect';
                    DownloadManagerCustomData = @{ServerUrl = "http://"+$Server+":8080/PSDSCPullServer.svc"; AllowUnsecureConnection = $true}
                }
}
PullClient -ID 'INSERTGUID' -Server 'INSERTSERVER' -Output 'C:\DSCConfig\'
Set-DscLocalConfigurationManager -ComputerName 'Localhost' -Path 'C:\DSCConfig\' -Verbose
```


## <a name="additional-references-snippets-and-examples"></a><span data-ttu-id="6da81-313">Další informace, fragmenty kódu a příklady</span><span class="sxs-lookup"><span data-stu-id="6da81-313">Additional references, snippets, and examples</span></span>

<span data-ttu-id="6da81-314">Tento příklad ukazuje, jak chcete ručně zahájit připojení klienta (vyžaduje WMF5) pro testování.</span><span class="sxs-lookup"><span data-stu-id="6da81-314">This example shows how to manually initiate a client connection (requires WMF5) for testing.</span></span> 

```powershell
Update-DSCConfiguration –Wait -Verbose
```

<span data-ttu-id="6da81-315">[Přidat DnsServerResourceRecordName](http://bit.ly/1G1H31L) rutina se používá k přidání typu záznamu CNAME do zóny DNS.</span><span class="sxs-lookup"><span data-stu-id="6da81-315">The [Add-DnsServerResourceRecordName](http://bit.ly/1G1H31L) cmdlet is used to add a type CNAME record to a DNS zone.</span></span> 

<span data-ttu-id="6da81-316">Funkce prostředí PowerShell k [vytvoření kontrolního součtu a publikovat MOF DSC pro vyžádání obsahu serveru SMB](http://bit.ly/1E46BhI) automaticky vytvoří požadované kontrolního součtu a pak zkopíruje MOF konfigurace i kontrolního součtu souborů k vyžádání serveru SMB.</span><span class="sxs-lookup"><span data-stu-id="6da81-316">The PowerShell Function to [Create a Checksum and Publish DSC MOF to SMB Pull Server](http://bit.ly/1E46BhI) automatically generates the required checksum, and then copies both the MOF configuration and checksum files to the SMB pull server.</span></span>

## <a name="appendix---understanding-odata-service-data-file-types"></a><span data-ttu-id="6da81-317">Příloha – Principy ODATA data služby typy souborů</span><span class="sxs-lookup"><span data-stu-id="6da81-317">Appendix - Understanding ODATA service data file types</span></span>

<span data-ttu-id="6da81-318">Datový soubor je uložen vytvořit informace při nasazení serveru vyžádané replikace, která zahrnuje webovou službu OData.</span><span class="sxs-lookup"><span data-stu-id="6da81-318">A data file is stored to create information during deployment of a pull server that includes the OData web service.</span></span> <span data-ttu-id="6da81-319">Typ souboru závisí na operačním systému, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="6da81-319">The type of file depends on the operating system, as described below.</span></span>

 - <span data-ttu-id="6da81-320">**Windows Server 2012**</span><span class="sxs-lookup"><span data-stu-id="6da81-320">**Windows Server 2012**</span></span>  
<span data-ttu-id="6da81-321">Typ souboru bude vždy .mdb</span><span class="sxs-lookup"><span data-stu-id="6da81-321">The file type will always be   .mdb</span></span>
 - <span data-ttu-id="6da81-322">**Windows Server 2012 R2**</span><span class="sxs-lookup"><span data-stu-id="6da81-322">**Windows Server 2012 R2**</span></span>  
<span data-ttu-id="6da81-323">Typ souboru bude použita výchozí .edb .mdb uvedeno v konfiguraci</span><span class="sxs-lookup"><span data-stu-id="6da81-323">The file type will default to .edb unless a .mdb is specified in the configuration</span></span>

<span data-ttu-id="6da81-324">V [Advanced ukázkový skript](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) při instalaci serveru pro vyžádání obsahu, také najdete příklad toho, jak automaticky řídit nastavení souboru web.config, aby se zabránilo pravděpodobné, že chyba způsobila podle typu souboru.</span><span class="sxs-lookup"><span data-stu-id="6da81-324">In the [Advanced example script](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) for installing a Pull Server, you will also find an example of how to automatically control the web.config file settings to prevent any chance of error caused by file type.</span></span>

