---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Osvědčené postupy serveru vyžádané replikace
ms.openlocfilehash: 04ad6940f443bc23d5e2347952b2d173aceac408
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893446"
---
# <a name="pull-server-best-practices"></a><span data-ttu-id="fcb25-103">Osvědčené postupy serveru vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="fcb25-103">Pull server best practices</span></span>

<span data-ttu-id="fcb25-104">Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="fcb25-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcb25-105">Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="fcb25-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="fcb25-106">Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="fcb25-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="fcb25-107">Shrnutí: Tento dokument je určený proces a rozšiřitelnost pomáhat techniků, kteří se připravuje pro řešení.</span><span class="sxs-lookup"><span data-stu-id="fcb25-107">Summary: This document is intended to include process and extensibility to assist engineers who are preparing for the solution.</span></span> <span data-ttu-id="fcb25-108">Podrobnosti by měly poskytnout doporučené postupy jsme uvedli, zákazníky a poté ověřen produktovému týmu a zkontrolujte doporučení jsou budoucí přístupem a považovat za stabilní.</span><span class="sxs-lookup"><span data-stu-id="fcb25-108">Details should provide best practices as identified by customers and then validated by the product team to ensure recommendations are future facing and considered stable.</span></span>

| |<span data-ttu-id="fcb25-109">Informace o dokumentu</span><span class="sxs-lookup"><span data-stu-id="fcb25-109">Doc Info</span></span>|
|:---|:---|
<span data-ttu-id="fcb25-110">Autor</span><span class="sxs-lookup"><span data-stu-id="fcb25-110">Author</span></span> | <span data-ttu-id="fcb25-111">Michael Greene</span><span class="sxs-lookup"><span data-stu-id="fcb25-111">Michael Greene</span></span>
<span data-ttu-id="fcb25-112">Recenzenti</span><span class="sxs-lookup"><span data-stu-id="fcb25-112">Reviewers</span></span> | <span data-ttu-id="fcb25-113">Robert Gelens, Ravikanth Chaganti Aleksandar Nikolic</span><span class="sxs-lookup"><span data-stu-id="fcb25-113">Ben Gelens, Ravikanth Chaganti, Aleksandar Nikolic</span></span>
<span data-ttu-id="fcb25-114">Publikování</span><span class="sxs-lookup"><span data-stu-id="fcb25-114">Published</span></span> | <span data-ttu-id="fcb25-115">Duben 2015</span><span class="sxs-lookup"><span data-stu-id="fcb25-115">April, 2015</span></span>

## <a name="abstract"></a><span data-ttu-id="fcb25-116">Abstraktní</span><span class="sxs-lookup"><span data-stu-id="fcb25-116">Abstract</span></span>

<span data-ttu-id="fcb25-117">Cílem tohoto dokumentu je poskytnout oficiální pokyny pro vývojáře plánující pro implementaci serveru pro vyžádání obsahu Windows PowerShell Desired State Configuration.</span><span class="sxs-lookup"><span data-stu-id="fcb25-117">This document is designed to provide official guidance for anyone planning for a Windows PowerShell Desired State Configuration pull server implementation.</span></span> <span data-ttu-id="fcb25-118">Serveru vyžádané replikace je jednoduché služby, který zabere jenom pár minut nasadit.</span><span class="sxs-lookup"><span data-stu-id="fcb25-118">A pull server is a simple service that should take only minutes to deploy.</span></span> <span data-ttu-id="fcb25-119">I když tento dokument nabídne technické příručkách s postupy, které lze použít v nasazení, hodnota tohoto dokumentu je jako reference pro osvědčené postupy a co zvážit před nasazením.</span><span class="sxs-lookup"><span data-stu-id="fcb25-119">Although this document will offer technical how-to guidance that can be used in a deployment, the value of this document is as a reference for best practices and what to think about before deploying.</span></span>
<span data-ttu-id="fcb25-120">Čtenáři by měl mít základní znalost DSC a termíny používané k popisu komponenty, které jsou součástí nasazení DSC.</span><span class="sxs-lookup"><span data-stu-id="fcb25-120">Readers should have basic familiarity with DSC, and the terms used to describe the components that are included in a DSC deployment.</span></span> <span data-ttu-id="fcb25-121">Další informace najdete v tématu [Windows PowerShell Desired State Configuration přehled](/powershell/dsc/overview) tématu.</span><span class="sxs-lookup"><span data-stu-id="fcb25-121">For more information, see the [Windows PowerShell Desired State Configuration Overview](/powershell/dsc/overview)  topic.</span></span>
<span data-ttu-id="fcb25-122">Rozvoj na cloudové tempo očekávaným DSC je základní technologie, včetně serveru vyžádané replikace také očekává se vyvíjí a zavádět nové funkce.</span><span class="sxs-lookup"><span data-stu-id="fcb25-122">As DSC is expected to evolve at cloud cadence, the underlying technology including pull server is also expected to evolve and to introduce new capabilities.</span></span> <span data-ttu-id="fcb25-123">Tento dokument obsahuje tabulku verzí v dodatku, která poskytuje odkazy na předchozích verzích a odkazy na budoucí vypadající řešení podporovat budoucnost návrhy.</span><span class="sxs-lookup"><span data-stu-id="fcb25-123">This document includes a version table in the appendix that provides references to previous releases and references to future looking solutions to encourage forward-looking designs.</span></span>

<span data-ttu-id="fcb25-124">Dvě hlavní části tohoto dokumentu:</span><span class="sxs-lookup"><span data-stu-id="fcb25-124">The two major sections of this document:</span></span>

- <span data-ttu-id="fcb25-125">Plánování konfigurace</span><span class="sxs-lookup"><span data-stu-id="fcb25-125">Configuration Planning</span></span>
- <span data-ttu-id="fcb25-126">Průvodce instalací</span><span class="sxs-lookup"><span data-stu-id="fcb25-126">Installation Guide</span></span>

### <a name="versions-of-the-windows-management-framework"></a><span data-ttu-id="fcb25-127">Verze rozhraní Windows Management Framework</span><span class="sxs-lookup"><span data-stu-id="fcb25-127">Versions of the Windows Management Framework</span></span>

<span data-ttu-id="fcb25-128">Informace v tomto dokumentu slouží platí pro Windows Management Framework 5.0.</span><span class="sxs-lookup"><span data-stu-id="fcb25-128">The information in this document is intended to apply to Windows Management Framework 5.0.</span></span> <span data-ttu-id="fcb25-129">Zatímco WMF 5.0 není vyžadována pro nasazení a používání serveru vyžádané replikace, verze 5.0 je hlavním cílem tohoto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fcb25-129">While WMF 5.0 is not required for deploying and operating a pull server, version 5.0 is the focus of this document.</span></span>

### <a name="windows-powershell-desired-state-configuration"></a><span data-ttu-id="fcb25-130">Prostředí Windows PowerShell Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="fcb25-130">Windows PowerShell Desired State Configuration</span></span>

<span data-ttu-id="fcb25-131">Desired State Configuration (DSC) je platforma pro správu, který umožňuje nasazení a správa konfiguračních dat pomocí syntaxe oboru s názvem formát MOF (Managed Object) pro popis Common Information Model (CIM).</span><span class="sxs-lookup"><span data-stu-id="fcb25-131">Desired State Configuration (DSC) is a management platform that enables deploying and managing configuration data by using an industry syntax named the Managed Object Format (MOF) to describe the Common Information Model (CIM).</span></span> <span data-ttu-id="fcb25-132">Opensourcový projekt, otevřete Management Infrastructure (OMI), existuje další rozvoj těchto standardů napříč platformami, včetně Linuxu a síťové hardwaru operační systémy.</span><span class="sxs-lookup"><span data-stu-id="fcb25-132">An open source project, Open Management Infrastructure (OMI), exists to further development of these standards across platforms including Linux and network hardware operating systems.</span></span> <span data-ttu-id="fcb25-133">Další informace najdete v tématu [DMTF stránky propojení specifikací MOF](https://www.dmtf.org/standards/cim), a [OMI dokumenty a zdroj](https://collaboration.opengroup.org/omi/documents.php).</span><span class="sxs-lookup"><span data-stu-id="fcb25-133">For more information, see the [DMTF page linking to MOF specifications](https://www.dmtf.org/standards/cim), and [OMI Documents and Source](https://collaboration.opengroup.org/omi/documents.php).</span></span>

<span data-ttu-id="fcb25-134">Prostředí Windows PowerShell poskytuje sadu jazyková rozšíření pro Desired State Configuration, můžete použít k vytvoření a správa deklarativních konfigurací.</span><span class="sxs-lookup"><span data-stu-id="fcb25-134">Windows PowerShell provides a set of language extensions for Desired State Configuration that you can use to create and manage declarative configurations.</span></span>

### <a name="pull-server-role"></a><span data-ttu-id="fcb25-135">Role serveru o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="fcb25-135">Pull server role</span></span>

<span data-ttu-id="fcb25-136">Načítacího serveru poskytuje centralizované služby k uložení konfigurace, které budou přístupné pro cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="fcb25-136">A pull server provides a centralized service to store configurations that will be accessible to target nodes.</span></span>

<span data-ttu-id="fcb25-137">Role serveru o přijetí změn můžete nasadit jako instance webového serveru nebo sdílené složky protokolu SMB.</span><span class="sxs-lookup"><span data-stu-id="fcb25-137">The pull server role can be deployed as either a Web Server instance or an SMB file share.</span></span> <span data-ttu-id="fcb25-138">Funkce webového serveru zahrnuje rozhraní OData a může volitelně zahrnovat možnosti pro cílové uzly k hlášení zpět potvrzení úspěch nebo neúspěch jako konfigurace se použijí.</span><span class="sxs-lookup"><span data-stu-id="fcb25-138">The web server capability includes an OData interface and can optionally include capabilities for target nodes to report back confirmation of success or failure as configurations are applied.</span></span> <span data-ttu-id="fcb25-139">Tato funkce je užitečná v prostředích, kdy existuje velký počet cílových uzlů.</span><span class="sxs-lookup"><span data-stu-id="fcb25-139">This functionality is useful in environments where there are a large number of target nodes.</span></span>
<span data-ttu-id="fcb25-140">Po dokončení konfigurace cílový uzel (také označované jako klient) tak, aby odkazoval na serveru vyžádané replikace nejnovější konfiguraci. jsou data a všechny požadované skripty stáhnout a použít.</span><span class="sxs-lookup"><span data-stu-id="fcb25-140">After configuring a target node (also referred to as a client) to point to the pull server the latest configuration data and any required scripts are downloaded and applied.</span></span> <span data-ttu-id="fcb25-141">Může to jako jednorázová nasazení nebo znovu se vyskytující úlohy, která také umožňuje serveru vyžádané replikace prostředek důležité pro správu změn ve velkém měřítku.</span><span class="sxs-lookup"><span data-stu-id="fcb25-141">This can happen as a one-time deployment or as a re-occurring job which also makes the pull server an important asset for managing change at scale.</span></span> <span data-ttu-id="fcb25-142">Další informace najdete v tématu [Windows PowerShell Desired State Configuration o přijetí změn servery](/powershell/dsc/pullServer) a</span><span class="sxs-lookup"><span data-stu-id="fcb25-142">For more information, see [Windows PowerShell Desired State Configuration Pull Servers](/powershell/dsc/pullServer) and</span></span>

<span data-ttu-id="fcb25-143">[Nabízená a vyžádaná režimů konfigurace](/powershell/dsc/pullServer).</span><span class="sxs-lookup"><span data-stu-id="fcb25-143">[Push and Pull Configuration Modes](/powershell/dsc/pullServer).</span></span>

## <a name="configuration-planning"></a><span data-ttu-id="fcb25-144">Plánování konfigurace</span><span class="sxs-lookup"><span data-stu-id="fcb25-144">Configuration planning</span></span>

<span data-ttu-id="fcb25-145">Pro každé nasazení softwaru enterprise je informace, které lze shromažďovat v předstihu vám pomohou při plánování pro správnou architekturu a abyste byli připraveni kroky potřebné k dokončení nasazení.</span><span class="sxs-lookup"><span data-stu-id="fcb25-145">For any enterprise software deployment there is information that can be collected in advance to help plan for the correct architecture and to be prepared for the steps required to complete the deployment.</span></span> <span data-ttu-id="fcb25-146">Následující části obsahují informace o tom, jak připravit a organizační připojení, které pravděpodobně budete muset předem stát.</span><span class="sxs-lookup"><span data-stu-id="fcb25-146">The following sections provide information regarding how to prepare and the organizational connections that will likely need to happen in advance.</span></span>

### <a name="software-requirements"></a><span data-ttu-id="fcb25-147">Požadavky na software</span><span class="sxs-lookup"><span data-stu-id="fcb25-147">Software requirements</span></span>

<span data-ttu-id="fcb25-148">Nasazení serveru vyžádané replikace vyžaduje funkce DSC služby systému Windows Server.</span><span class="sxs-lookup"><span data-stu-id="fcb25-148">Deployment of a pull server requires the DSC Service feature of Windows Server.</span></span> <span data-ttu-id="fcb25-149">Tato funkce byla zavedena v systému Windows Server 2012 a byl aktualizován prostřednictvím probíhající vydání služby Windows Management Frameworku (WMF).</span><span class="sxs-lookup"><span data-stu-id="fcb25-149">This feature was introduced in Windows Server 2012, and has been updated through ongoing releases of Windows Management Framework (WMF).</span></span>

### <a name="software-downloads"></a><span data-ttu-id="fcb25-150">Stahování softwaru</span><span class="sxs-lookup"><span data-stu-id="fcb25-150">Software downloads</span></span>

<span data-ttu-id="fcb25-151">Kromě instalace nejnovější obsah z webu Windows Update, jsou k dispozici dva soubory ke stažení považovat za osvědčený postup nasazení serveru vyžádané replikace DSC: nejnovější verzi Windows Management Framework a modulu DSC můžete automatizovat zřizování serveru o přijetí změn.</span><span class="sxs-lookup"><span data-stu-id="fcb25-151">In addition to installing the latest content from Windows Update, there are two downloads considered best practice to deploy a DSC pull server: The latest version of Windows Management Framework, and a DSC module to automate pull server provisioning.</span></span>

### <a name="wmf"></a><span data-ttu-id="fcb25-152">WMF</span><span class="sxs-lookup"><span data-stu-id="fcb25-152">WMF</span></span>

<span data-ttu-id="fcb25-153">Windows Server 2012 R2 obsahuje funkci s názvem služby DSC.</span><span class="sxs-lookup"><span data-stu-id="fcb25-153">Windows Server 2012 R2 includes a feature named the DSC Service.</span></span> <span data-ttu-id="fcb25-154">Funkce služby DSC poskytuje funkce serveru o přijetí změn, včetně binárních souborů, které podporují koncový bod OData.</span><span class="sxs-lookup"><span data-stu-id="fcb25-154">The DSC Service feature provides the pull server functionality, including the binaries that support the OData endpoint.</span></span>
<span data-ttu-id="fcb25-155">WMF je součástí systému Windows Server a dojde k aktualizaci na agilní tempo mezi verzemi Windows serveru.</span><span class="sxs-lookup"><span data-stu-id="fcb25-155">WMF is included in Windows Server and is updated on an agile cadence between Windows Server releases.</span></span> <span data-ttu-id="fcb25-156">[Nové verze WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=54616) mohou obsahovat aktualizace funkcí DSC služby.</span><span class="sxs-lookup"><span data-stu-id="fcb25-156">[New versions of WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=54616)  can include updates to the DSC Service feature.</span></span> <span data-ttu-id="fcb25-157">Z tohoto důvodu je osvědčeným postupem stažení nejnovější verze WMF a přečtěte si poznámky k určení, pokud tato verze obsahuje aktualizace funkcí služby DSC.</span><span class="sxs-lookup"><span data-stu-id="fcb25-157">For this reason, it is a best practice to download the latest release of WMF and to review the release notes to determine if the release includes an update to the DSC service feature.</span></span> <span data-ttu-id="fcb25-158">Také byste měli revidovat část poznámky k verzi, která určuje, zda je stav návrhu pro aktualizaci nebo scénář uveden jako stabilní nebo experimentální.</span><span class="sxs-lookup"><span data-stu-id="fcb25-158">You should also review the section of the release notes that indicates whether the design status for an update or scenario is listed as stable or experimental.</span></span>
<span data-ttu-id="fcb25-159">Povolit pro agilní vývojového cyklu, jednotlivé funkce mohou být deklarovány stabilní, což znamená, funkce je připravená k použití v produkčním prostředí, dokonce i za běhu WMF vydání ve verzi preview.</span><span class="sxs-lookup"><span data-stu-id="fcb25-159">To allow for an agile release cycle, individual features can be declared stable, which indicates the feature is ready to be used in a production environment even while WMF is released in preview.</span></span>
<span data-ttu-id="fcb25-160">Další funkce, které v minulosti byly aktualizovány podle verze WMF (viz poznámky k verzi WMF podrobnosti):</span><span class="sxs-lookup"><span data-stu-id="fcb25-160">Other features that have historically been updated by WMF releases (see the WMF Release Notes for further detail):</span></span>

- <span data-ttu-id="fcb25-161">Integrované skriptovací prostředí Windows PowerShell, Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcb25-161">Windows PowerShell Windows PowerShell Integrated Scripting</span></span>
- <span data-ttu-id="fcb25-162">Prostředí (ISE) Windows Powershellu webové služby (správu OData</span><span class="sxs-lookup"><span data-stu-id="fcb25-162">Environment (ISE) Windows PowerShell Web Services (Management OData</span></span>
- <span data-ttu-id="fcb25-163">Rozšíření IIS pro službu) Windows Powershellu Desired State Configuration (DSC)</span><span class="sxs-lookup"><span data-stu-id="fcb25-163">IIS Extension)  Windows PowerShell Desired State Configuration (DSC)</span></span>
- <span data-ttu-id="fcb25-164">Windows (WinRM) Vzdálená správa Windows Management Instrumentation (WMI)</span><span class="sxs-lookup"><span data-stu-id="fcb25-164">Windows Remote Management (WinRM) Windows Management Instrumentation (WMI)</span></span>

### <a name="dsc-resource"></a><span data-ttu-id="fcb25-165">Prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="fcb25-165">DSC resource</span></span>

<span data-ttu-id="fcb25-166">Nasazení serveru o přijetí změn se dá zjednodušit tím, že zajistíte služby pomocí skriptu konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="fcb25-166">A pull server deployment can be simplified by provisioning the service using a DSC configuration script.</span></span> <span data-ttu-id="fcb25-167">Tento dokument obsahuje konfigurační skripty, které lze použít k nasazení uzlu produkční server připravený.</span><span class="sxs-lookup"><span data-stu-id="fcb25-167">This document includes configuration scripts that can be used to deploy a production ready server node.</span></span> <span data-ttu-id="fcb25-168">Pokud chcete používat konfigurační skripty, DSC modul je potřeba, který je nejsou zahrnuty v systému Windows Server.</span><span class="sxs-lookup"><span data-stu-id="fcb25-168">To use the configuration scripts, a DSC module is required that is not included in Windows Server.</span></span> <span data-ttu-id="fcb25-169">Je název požadované modulu **xPSDesiredStateConfiguration**, což zahrnuje prostředků DSC **xDscWebService**.</span><span class="sxs-lookup"><span data-stu-id="fcb25-169">The required module name is **xPSDesiredStateConfiguration**, which includes the DSC resource **xDscWebService**.</span></span> <span data-ttu-id="fcb25-170">Je možné stáhnout modul xPSDesiredStateConfiguration [tady](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).</span><span class="sxs-lookup"><span data-stu-id="fcb25-170">The xPSDesiredStateConfiguration module can be downloaded [here](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).</span></span>

<span data-ttu-id="fcb25-171">Použití `Install-Module` rutiny z **PowerShellGet** modulu.</span><span class="sxs-lookup"><span data-stu-id="fcb25-171">Use the `Install-Module` cmdlet from the **PowerShellGet** module.</span></span>

```powershell
Install-Module xPSDesiredStateConfiguration
```

<span data-ttu-id="fcb25-172">**PowerShellGet** modulu stáhne modul:</span><span class="sxs-lookup"><span data-stu-id="fcb25-172">The **PowerShellGet** module will download the module to:</span></span>

`C:\Program Files\Windows PowerShell\Modules`

<span data-ttu-id="fcb25-173">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="fcb25-173">Planning task</span></span>|
---|
<span data-ttu-id="fcb25-174">Máte přístup k souborům instalace pro Windows Server 2012 R2?</span><span class="sxs-lookup"><span data-stu-id="fcb25-174">Do you have access to the installation files for Windows Server 2012 R2?</span></span>|
<span data-ttu-id="fcb25-175">Prostředí nasazení bude mít přístup k Internetu stáhnout WMF a modul z online galerie?</span><span class="sxs-lookup"><span data-stu-id="fcb25-175">Will the deployment environment have Internet access to download WMF and the module from the online gallery?</span></span>|
<span data-ttu-id="fcb25-176">Jak budou instalovat nejnovější aktualizace zabezpečení po instalaci operačního systému?</span><span class="sxs-lookup"><span data-stu-id="fcb25-176">How will you install the latest security updates after installing the operating system?</span></span>|
<span data-ttu-id="fcb25-177">Prostředí bude mít přístup k Internetu k získání aktualizací nebo bude mít na místním serveru Windows Server Update Services (WSUS)?</span><span class="sxs-lookup"><span data-stu-id="fcb25-177">Will the environment have Internet access to obtain updates, or will it have a local Windows Server Update Services (WSUS) server?</span></span>|
<span data-ttu-id="fcb25-178">Máte přístup k Windows serveru instalační soubory, které už zahrnují aktualizace prostřednictvím injektáže offline?</span><span class="sxs-lookup"><span data-stu-id="fcb25-178">Do you have access to Windows Server installation files that already include updates through offline injection?</span></span>|

### <a name="hardware-requirements"></a><span data-ttu-id="fcb25-179">Požadavky na hardware</span><span class="sxs-lookup"><span data-stu-id="fcb25-179">Hardware requirements</span></span>

<span data-ttu-id="fcb25-180">Nasazení serveru vyžádané replikace se podporují na fyzických i virtuálních serverů.</span><span class="sxs-lookup"><span data-stu-id="fcb25-180">Pull server deployments are supported on both physical and virtual servers.</span></span> <span data-ttu-id="fcb25-181">Požadavky na velikost pro vyžádání obsahu server souladu s požadavky na systém Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="fcb25-181">The sizing requirements for pull server align with the requirements for Windows Server 2012 R2.</span></span>

<span data-ttu-id="fcb25-182">: 1,4 GHz 64bitový procesor paměti: 512 MB místa na disku: 32 GB sítě: adaptér Gigabit Ethernet</span><span class="sxs-lookup"><span data-stu-id="fcb25-182">CPU: 1.4 GHz 64-bit processor Memory: 512 MB Disk Space: 32 GB Network: Gigabit Ethernet Adapter</span></span>

<span data-ttu-id="fcb25-183">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="fcb25-183">Planning task</span></span>|
---|
<span data-ttu-id="fcb25-184">Budete nasazovat na fyzickém hardwaru nebo na virtualizační platformě?</span><span class="sxs-lookup"><span data-stu-id="fcb25-184">Will you deploy on physical hardware or on a virtualization platform?</span></span>|
<span data-ttu-id="fcb25-185">Jaký je proces požádat o nový server pro cílové prostředí?</span><span class="sxs-lookup"><span data-stu-id="fcb25-185">What is the process to request a new server for your target environment?</span></span>|
<span data-ttu-id="fcb25-186">Co je průměrná doba vyřízení pro server k dispozici?</span><span class="sxs-lookup"><span data-stu-id="fcb25-186">What is the average turnaround time for a server to become available?</span></span>|
<span data-ttu-id="fcb25-187">Jaké velikosti serveru bude požadovat?</span><span class="sxs-lookup"><span data-stu-id="fcb25-187">What size server will you request?</span></span>|

### <a name="accounts"></a><span data-ttu-id="fcb25-188">Účty</span><span class="sxs-lookup"><span data-stu-id="fcb25-188">Accounts</span></span>

<span data-ttu-id="fcb25-189">Neexistují žádné požadavky na účet služby pro nasazení instance serveru o přijetí změn.</span><span class="sxs-lookup"><span data-stu-id="fcb25-189">There are no service account requirements to deploy a pull server instance.</span></span>
<span data-ttu-id="fcb25-190">Existují ale scénáře, ve kterém webu může běžet v kontextu účtu místního uživatele.</span><span class="sxs-lookup"><span data-stu-id="fcb25-190">However, there are scenarios where the website could run in the context of a local user account.</span></span>
<span data-ttu-id="fcb25-191">Například pokud není potřeba přístup sdílené složky úložiště obsahu webu a Windows Server nebo zařízení, který je hostitelem sdílené úložiště nejsou připojené k doméně.</span><span class="sxs-lookup"><span data-stu-id="fcb25-191">For example, if there is a need to access a storage share for website content and either the Windows Server or the device hosting the storage share are not domain joined.</span></span>

### <a name="dns-records"></a><span data-ttu-id="fcb25-192">Záznamy DNS</span><span class="sxs-lookup"><span data-stu-id="fcb25-192">DNS records</span></span>

<span data-ttu-id="fcb25-193">Budete potřebovat název serveru, který má použít při konfiguraci klientů pro práci s prostředím serveru o přijetí změn.</span><span class="sxs-lookup"><span data-stu-id="fcb25-193">You will need a server name to use when configuring clients to work with a pull server environment.</span></span>
<span data-ttu-id="fcb25-194">V testovacích prostředích obvykle se používá název hostitele serveru nebo IP adresa serveru je možné, pokud překlad názvů DNS není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="fcb25-194">In test environments, typically the server hostname is used, or the IP address for the server can be used if DNS name resolution is not available.</span></span>
<span data-ttu-id="fcb25-195">V produkčním prostředí nebo v testovacím prostředí, která je určená pro produkční nasazení představují osvědčeným postupem je vytvořit záznam DNS CNAME.</span><span class="sxs-lookup"><span data-stu-id="fcb25-195">In production environments or in a lab environment that is intended to represent a production deployment, the best practice is to create a DNS CNAME record.</span></span>

<span data-ttu-id="fcb25-196">Záznam CNAME DNS můžete vytvořit alias pro odkazování na hostitele (A) záznam.</span><span class="sxs-lookup"><span data-stu-id="fcb25-196">A DNS CNAME allows you to create an alias to refer to your host (A) record.</span></span>
<span data-ttu-id="fcb25-197">Záměrem další název záznamu je zvýšit flexibilitu, třeba změny požadované v budoucnu.</span><span class="sxs-lookup"><span data-stu-id="fcb25-197">The intent of the additional name record is to increase flexibility should a change be required in the future.</span></span>
<span data-ttu-id="fcb25-198">Může pomoct záznam CNAME izolace konfigurace klienta tak, aby změny serverovým prostředím, jako je například nahrazení serveru vyžádané replikace nebo při přidávání serverů další o přijetí změn, nebude vyžadovat odpovídající změnu konfigurace klienta.</span><span class="sxs-lookup"><span data-stu-id="fcb25-198">A CNAME can help to isolate the client configuration so that changes to the server environment, such as replacing a pull server or adding additional pull servers, will not require a corresponding change to the client configuration.</span></span>

<span data-ttu-id="fcb25-199">Pokud zvolíte, že název záznamu DNS, mějte architekturu řešení.</span><span class="sxs-lookup"><span data-stu-id="fcb25-199">When choosing a name for the DNS record, keep the solution architecture in mind.</span></span>
<span data-ttu-id="fcb25-200">Pokud pomocí vyrovnávání zatížení, bude nutné mají stejný název jako záznam DNS certifikát používaný k zabezpečení přenosů přes protokol HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fcb25-200">If using load balancing, the certificate used to secure traffic over HTTPS will need to share the same name as the DNS record.</span></span>

<span data-ttu-id="fcb25-201">Scénář</span><span class="sxs-lookup"><span data-stu-id="fcb25-201">Scenario</span></span> |<span data-ttu-id="fcb25-202">Osvědčený postup</span><span class="sxs-lookup"><span data-stu-id="fcb25-202">Best Practice</span></span>
:---|:---
<span data-ttu-id="fcb25-203">Testovací prostředí</span><span class="sxs-lookup"><span data-stu-id="fcb25-203">Test Environment</span></span> |<span data-ttu-id="fcb25-204">Pokud je to možné reprodukujte plánované produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="fcb25-204">Reproduce the planned production environment, if possible.</span></span> <span data-ttu-id="fcb25-205">Název hostitele serveru je vhodný pro jednoduchá konfigurace.</span><span class="sxs-lookup"><span data-stu-id="fcb25-205">A server hostname is suitable for simple configurations.</span></span> <span data-ttu-id="fcb25-206">Pokud DNS není k dispozici, IP adresu lze namísto názvu hostitele.</span><span class="sxs-lookup"><span data-stu-id="fcb25-206">If DNS is not available, an IP address may be used in lieu of a hostname.</span></span>|
<span data-ttu-id="fcb25-207">Nasazení s jedním uzlem</span><span class="sxs-lookup"><span data-stu-id="fcb25-207">Single Node Deployment</span></span> |<span data-ttu-id="fcb25-208">Vytvořte záznam DNS CNAME, který odkazuje na název hostitele serveru.</span><span class="sxs-lookup"><span data-stu-id="fcb25-208">Create a DNS CNAME record that points to the server hostname.</span></span>|

<span data-ttu-id="fcb25-209">Další informace najdete v tématu [konfigurace kruhové dotazování DNS ve Windows serveru](/previous-versions/windows/it-pro/windows-server-2003/cc787484(v=ws.10)).</span><span class="sxs-lookup"><span data-stu-id="fcb25-209">For more information, see [Configuring DNS Round Robin in Windows Server](/previous-versions/windows/it-pro/windows-server-2003/cc787484(v=ws.10)).</span></span>

<span data-ttu-id="fcb25-210">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="fcb25-210">Planning task</span></span>|
---|
<span data-ttu-id="fcb25-211">Víte, koho se obrátit na záznamy DNS vytvořit a změnit?</span><span class="sxs-lookup"><span data-stu-id="fcb25-211">Do you know who to contact to have DNS records created and changed?</span></span>|
<span data-ttu-id="fcb25-212">Co je průměrná obrátkou pro požadavek na záznam DNS?</span><span class="sxs-lookup"><span data-stu-id="fcb25-212">What is the average turnaround for a request for a DNS record?</span></span>|
<span data-ttu-id="fcb25-213">Každý modul musí být zabaleny v určitém formátu souboru .zip s názvem ModuleName_Version.zip obsahující datové části modulu.</span><span class="sxs-lookup"><span data-stu-id="fcb25-213">Do you need to request static Hostname (A) records for servers?</span></span>|
<span data-ttu-id="fcb25-214">Po zkopírování souboru na server, je nutné vytvořit kontrolní součet souboru.</span><span class="sxs-lookup"><span data-stu-id="fcb25-214">What will you request as a CNAME?</span></span>|
<span data-ttu-id="fcb25-215">Pokud se klienti připojují k serveru, kontrolní součet se používá k ověření, že obsah modulu DSC se nezměnil, protože byla publikována.</span><span class="sxs-lookup"><span data-stu-id="fcb25-215">If needed, what type of Load Balancing solution will you utilize?</span></span> <span data-ttu-id="fcb25-216">Pokud plánujete prostředí test nebo testovací prostředí, které scénáře jsou klíčem k ověření?</span><span class="sxs-lookup"><span data-stu-id="fcb25-216">(see section titled Load Balancing for details)</span></span>|

### <a name="public-key-infrastructure"></a><span data-ttu-id="fcb25-217">Existují veřejně dostupných modulů, které obsahují prostředky vám pomůžou se vším, co potřebujete, nebo bude muset vytvořit vlastní prostředky?</span><span class="sxs-lookup"><span data-stu-id="fcb25-217">Public Key Infrastructure</span></span>

<span data-ttu-id="fcb25-218">Prostředí bude mít přístup k Internetu se načíst veřejný moduly?</span><span class="sxs-lookup"><span data-stu-id="fcb25-218">Most organizations today require that network traffic, especially traffic that includes such sensitive data as how servers are configured, must be validated and/or encrypted during transit.</span></span>
<span data-ttu-id="fcb25-219">Kdo bude zodpovídat za revize DSC moduly?</span><span class="sxs-lookup"><span data-stu-id="fcb25-219">While it is possible to deploy a pull server using HTTP which facilitates client requests in clear text, it is a best practice to secure traffic using HTTPS.</span></span> <span data-ttu-id="fcb25-220">Pokud plánujete do produkčního prostředí co budete používat jako místní úložiště pro ukládání DSC moduly?</span><span class="sxs-lookup"><span data-stu-id="fcb25-220">The service can be configured to use HTTPS using a set of parameters in the DSC resource **xPSDesiredStateConfiguration**.</span></span>

<span data-ttu-id="fcb25-221">Přijme centrální tým DSC moduly z aplikační týmy?</span><span class="sxs-lookup"><span data-stu-id="fcb25-221">The certificate requirements to secure HTTPS traffic for pull server are not different than securing any other HTTPS web site.</span></span> <span data-ttu-id="fcb25-222">Co bude procesu?</span><span class="sxs-lookup"><span data-stu-id="fcb25-222">The **Web Server** template in a Windows Server Certificate Services satisfies the required capabilities.</span></span>

<span data-ttu-id="fcb25-223">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="fcb25-223">Planning task</span></span>|
---|
<span data-ttu-id="fcb25-224">Můžete automatizovat vytváření balíčků, kopírování a vytváření kontrolního součtu pro produkční prostředí DSC moduly na server z vašeho úložiště zdrojového kódu?</span><span class="sxs-lookup"><span data-stu-id="fcb25-224">If certificate requests are not automated, who will you need to contact to requests a certificate?</span></span>|
<span data-ttu-id="fcb25-225">Bude váš tým zodpovědného za správu platformu automatizace?</span><span class="sxs-lookup"><span data-stu-id="fcb25-225">What is the average turnaround for the request?</span></span>|
<span data-ttu-id="fcb25-226">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="fcb25-226">How will the certificate file be transferred to you?</span></span>|
<span data-ttu-id="fcb25-227">Účelem serveru vyžádané replikace je centralizovaná mechanismus pro distribuci konfigurací DSC na uzly klienta.</span><span class="sxs-lookup"><span data-stu-id="fcb25-227">How will the certificate private key be transferred to you?</span></span>|
<span data-ttu-id="fcb25-228">Tyto konfigurace jsou uloženy na serveru jako MOF dokumenty.</span><span class="sxs-lookup"><span data-stu-id="fcb25-228">How long is the default expiration time?</span></span>|
<span data-ttu-id="fcb25-229">Každý dokument budou mít názvy jedinečný identifikátor GUID.</span><span class="sxs-lookup"><span data-stu-id="fcb25-229">Have you settled on a DNS name for the pull server environment, that you can use for the certificate name?</span></span>|

### <a name="choosing-an-architecture"></a><span data-ttu-id="fcb25-230">Když jsou klienti nakonfigurováni pro připojení k serveru vyžádané replikace, jsou také uvedeny identifikátor GUID pro konfiguraci, kterou by měl žádat o.</span><span class="sxs-lookup"><span data-stu-id="fcb25-230">Choosing an architecture</span></span>

<span data-ttu-id="fcb25-231">Tento systém odkazuje na konfigurace podle identifikátoru GUID zaručuje jedinečnost globální a je flexibilní, takže konfiguraci lze použít s členitosti podle počtu uzlů, nebo jako konfiguraci role, která zahrnuje mnoho serverů, které by měly mít stejné konfigurace.</span><span class="sxs-lookup"><span data-stu-id="fcb25-231">A pull server can be deployed using either a web service hosted on IIS, or an SMB file share.</span></span> <span data-ttu-id="fcb25-232">Identifikátory GUID</span><span class="sxs-lookup"><span data-stu-id="fcb25-232">In most situations, the web service option will provide greater flexibility.</span></span> <span data-ttu-id="fcb25-233">Plánování konfigurace GUID je vhodné další pozornost dala až po nasazení serveru o přijetí změn.</span><span class="sxs-lookup"><span data-stu-id="fcb25-233">It is not uncommon for HTTPS traffic to traverse network boundaries, whereas SMB traffic is often filtered or blocked between networks.</span></span> <span data-ttu-id="fcb25-234">Neexistuje žádný konkrétní požadavek, způsob zpracování identifikátory GUID a proces je pravděpodobně být jedinečný pro každé prostředí.</span><span class="sxs-lookup"><span data-stu-id="fcb25-234">The web service also offers the option to include a Conformance Server or Web Reporting Manager (both topics to be addressed in a future version of this document) that provide a mechanism for clients to report status back to a server for centralized visibility.</span></span>
<span data-ttu-id="fcb25-235">Proces může být v rozsahu od jednoduché složité: centrálně uloženého souboru CSV, jednoduché tabulky SQL, databáze CMDB nebo komplexní řešení, která vyžadují integraci s jiným řešením nástroj nebo softwaru.</span><span class="sxs-lookup"><span data-stu-id="fcb25-235">SMB provides an option for environments where policy dictates that a web server should not be utilized, and for other environmental requirements that make a web server role undesirable.</span></span>
<span data-ttu-id="fcb25-236">Existují dvě obecné metody:</span><span class="sxs-lookup"><span data-stu-id="fcb25-236">In either case, remember to evaluate the requirements for signing and encrypting traffic.</span></span> <span data-ttu-id="fcb25-237">Přiřazení identifikátory GUID na server – poskytuje míru záruky, že všechny konfigurace serveru je řízen jednotlivě.</span><span class="sxs-lookup"><span data-stu-id="fcb25-237">HTTPS, SMB signing, and IPSEC policies are all options worth considering.</span></span>

#### <a name="load-balancing"></a><span data-ttu-id="fcb25-238">Vyrovnávání zatížení</span><span class="sxs-lookup"><span data-stu-id="fcb25-238">Load balancing</span></span>

<span data-ttu-id="fcb25-239">To poskytuje úroveň přesnosti kolem aktualizace a může fungovat i v prostředí s několika servery.</span><span class="sxs-lookup"><span data-stu-id="fcb25-239">Clients interacting with the web service make a request for information that is returned in a single response.</span></span> <span data-ttu-id="fcb25-240">Přiřazení identifikátory GUID na roli serveru – všechny servery, které provádí stejnou funkci, jako jsou třeba webové servery, použijte stejný identifikátor GUID odkazovat na požadované konfigurační data.</span><span class="sxs-lookup"><span data-stu-id="fcb25-240">No sequential requests are required, so it is not necessary for the load balancing platform to ensure sessions are maintained on a single server at any point in time.</span></span>

<span data-ttu-id="fcb25-241">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="fcb25-241">Planning task</span></span>|
---|
<span data-ttu-id="fcb25-242">Mějte na paměti, že pokud mnoho serverů sdílejí stejný identifikátor GUID, všechny z nich se aktualizují najednou při změně konfigurace.</span><span class="sxs-lookup"><span data-stu-id="fcb25-242">What solution will be used for load balancing traffic across servers?</span></span>|
<span data-ttu-id="fcb25-243">Identifikátor GUID je něco, co by měl být citlivá data vzhledem k tomu, že může využít uživatel s úmyslem získat informace o tom, jak jsou servery nasazené a nakonfigurovaných ve vašem prostředí.</span><span class="sxs-lookup"><span data-stu-id="fcb25-243">If using a hardware load balancer, who will take a request to add a new configuration to the device?</span></span>|
<span data-ttu-id="fcb25-244">Další informace najdete v tématu bezpečně přidělování identifikátorů GUID v prostředí PowerShell Desired State Configuration o přijetí změn režimu.</span><span class="sxs-lookup"><span data-stu-id="fcb25-244">What is the average turnaround for a request to configure a new load balanced web service?</span></span>|
<span data-ttu-id="fcb25-245">Kdo bude zodpovídat za konfigurací v kopírování do složky na serveru o přijetí změn, jakmile jsou připravené?</span><span class="sxs-lookup"><span data-stu-id="fcb25-245">What information will be required for the request?</span></span>|
<span data-ttu-id="fcb25-246">Pokud konfigurace vytvořené týmem aplikace, co proces bude je předat?</span><span class="sxs-lookup"><span data-stu-id="fcb25-246">Will you need to request an additional IP or will the team responsible for load balancing handle that?</span></span>|
<span data-ttu-id="fcb25-247">Bude využívat úložiště k ukládání konfigurace podle jejich probíhá čtení zleva doprava, napříč týmy?</span><span class="sxs-lookup"><span data-stu-id="fcb25-247">Do you have the DNS records needed, and will this be required by the team responsible for configuring the load balancing solution?</span></span>|
<span data-ttu-id="fcb25-248">Můžete automatizovat proces kopírování konfigurace do serveru a vytváření kontrolní součet, jakmile jsou připravené?</span><span class="sxs-lookup"><span data-stu-id="fcb25-248">Does the load balancing solution require that PKI be handled by the device or can it load balance HTTPS traffic as long as there are no session requirements?</span></span>|

### <a name="staging-configurations-and-modules-on-the-pull-server"></a><span data-ttu-id="fcb25-249">Jak se namapujete identifikátory GUID na servery nebo role a kdy to se uloží?</span><span class="sxs-lookup"><span data-stu-id="fcb25-249">Staging configurations and modules on the pull server</span></span>

<span data-ttu-id="fcb25-250">Co budete používat jako proces ke konfiguraci klientských počítačů a jak ji integrovat s vaším procesem pro vytváření a ukládání konfigurace identifikátory GUID?</span><span class="sxs-lookup"><span data-stu-id="fcb25-250">As part of configuration planning, you will need to think about which DSC modules and configurations will be hosted by the pull server.</span></span> <span data-ttu-id="fcb25-251">Skripty, které jsou uvedené v tomto dokumentu jsou stabilní příklady.</span><span class="sxs-lookup"><span data-stu-id="fcb25-251">For the purpose of configuration planning it is important to have a basic understanding of how to prepare and deploy content to a pull server.</span></span>

<span data-ttu-id="fcb25-252">Vždy zkontrolujte pečlivě skripty před spuštěním v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="fcb25-252">In the future, this section will be expanded and included in an Operations Guide for DSC Pull Server.</span></span>  <span data-ttu-id="fcb25-253">Chcete-li ověřit verzi prostředí PowerShell na vašem serveru použijte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="fcb25-253">The guide will discuss the day to day process for managing modules and configurations over time with automation.</span></span>

#### <a name="dsc-modules"></a><span data-ttu-id="fcb25-254">Pokud je to možné upgradujte na nejnovější verzi Windows Management Framework.</span><span class="sxs-lookup"><span data-stu-id="fcb25-254">DSC modules</span></span>

<span data-ttu-id="fcb25-255">Dále si stáhněte  modul pomocí následujícího příkazu.</span><span class="sxs-lookup"><span data-stu-id="fcb25-255">Clients that request a configuration will need the required DSC modules.</span></span> <span data-ttu-id="fcb25-256">Příkaz vyzve ke schválení před stažením modulu.</span><span class="sxs-lookup"><span data-stu-id="fcb25-256">A functionality of the pull server is to automate distribution on demand of DSC modules to clients.</span></span> <span data-ttu-id="fcb25-257">Instalace a konfigurace skriptů</span><span class="sxs-lookup"><span data-stu-id="fcb25-257">If you are deploying a pull server for the first time, perhaps as a lab or proof of concept, you are likely going to depend on DSC modules that are available from public repositories such as the PowerShell Gallery or the PowerShell.org GitHub repositories for DSC modules.</span></span>

<span data-ttu-id="fcb25-258">Nejlepší metodou k nasazení serveru vyžádané replikace DSC je použití skriptu konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="fcb25-258">It is critical to remember that even for trusted online sources such as the PowerShell Gallery, any module that is downloaded from a public repository should be reviewed by someone with PowerShell experience and knowledge of the environment where the modules will be used prior to being used in production.</span></span> <span data-ttu-id="fcb25-259">Tento dokument zobrazíte skripty, včetně obě základní nastavení, které by konfigurovat jenom webovou službu DSC a upřesňující nastavení, která by konfigurovat Windows Server začátku do konce včetně DSC webové služby.</span><span class="sxs-lookup"><span data-stu-id="fcb25-259">While completing this task it is a good time to check for any additional payload in the module that can be removed such as documentation and example scripts.</span></span> <span data-ttu-id="fcb25-260">Poznámka: Aktuálně  DSC modul vyžaduje serveru, aby se národního prostředí EN-US.</span><span class="sxs-lookup"><span data-stu-id="fcb25-260">This will reduce the network bandwidth per client in their first request, when modules will be downloaded over the network from server to client.</span></span>

<span data-ttu-id="fcb25-261">Základní konfigurace pro Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="fcb25-261">Each module must be packaged in a specific format, a ZIP file named ModuleName_Version.zip that contains the module payload.</span></span> <span data-ttu-id="fcb25-262">Upřesňující konfigurace pro Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="fcb25-262">After the file is copied to the server a checksum file must be created.</span></span> <span data-ttu-id="fcb25-263">Ověřte funkčnost serveru o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="fcb25-263">When clients connect to the server, the checksum is used to verify the content of the DSC module has not changed since it was published.</span></span>

```powershell
New-DscChecksum -ConfigurationPath .\ -OutPath .\
```

<span data-ttu-id="fcb25-264">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="fcb25-264">Planning task</span></span>|
---|
<span data-ttu-id="fcb25-265">Konfigurace klientů</span><span class="sxs-lookup"><span data-stu-id="fcb25-265">If you are planning a test or lab environment which scenarios are key to validate?</span></span>|
<span data-ttu-id="fcb25-266">Další odkazy na fragmenty kódu a příklady</span><span class="sxs-lookup"><span data-stu-id="fcb25-266">Are there publicly available modules that contain resources to cover everything you need or will you need to author your own resources?</span></span>|
<span data-ttu-id="fcb25-267">Tento příklad ukazuje, jak ručně zahájit připojení klienta (vyžaduje WMF5) pro účely testování.</span><span class="sxs-lookup"><span data-stu-id="fcb25-267">Will your environment have Internet access to retrieve public modules?</span></span>|
<span data-ttu-id="fcb25-268">Přidat DnsServerResourceRecordName rutina se používá k přidání typ záznamu CNAME do zóny DNS.</span><span class="sxs-lookup"><span data-stu-id="fcb25-268">Who will be responsible for reviewing DSC modules?</span></span>|
<span data-ttu-id="fcb25-269">Funkce, prostředí PowerShell vytvoření kontrolního součtu a publikovat MOF DSC na serveru vyžádané replikace SMB automaticky vytvoří požadované kontrolního součtu a pak zkopíruje MOF konfigurace i soubory kontrolního součtu serveru vyžádané replikace SMB.</span><span class="sxs-lookup"><span data-stu-id="fcb25-269">If you are planning a production environment what will you use as a local repository for storing DSC modules?</span></span>|
<span data-ttu-id="fcb25-270">Příloha – Principy ODATA typy dat služby souborů</span><span class="sxs-lookup"><span data-stu-id="fcb25-270">Will a central team accept DSC modules from application teams?</span></span> <span data-ttu-id="fcb25-271">Datový soubor je uložen vytvořit informace během nasazování serveru vyžádané replikace, který obsahuje webovou službu OData.</span><span class="sxs-lookup"><span data-stu-id="fcb25-271">What will the process be?</span></span>|
<span data-ttu-id="fcb25-272">Typ souboru závisí na operačním systému, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="fcb25-272">Will you automate packaging, copying, and creating a checksum for production-ready DSC modules to the server, from your source repo?</span></span>|
<span data-ttu-id="fcb25-273">Windows Server 2012 typ souboru bude vždy .mdb</span><span class="sxs-lookup"><span data-stu-id="fcb25-273">Will your team be responsible for managing the automation platform as well?</span></span>|

#### <a name="dsc-configurations"></a><span data-ttu-id="fcb25-274">Windows Server 2012 R2 typ souboru se ve výchozím nastavení .edb v konfiguraci je uvedeno .mdb</span><span class="sxs-lookup"><span data-stu-id="fcb25-274">DSC configurations</span></span>

<span data-ttu-id="fcb25-275">V Advanced ukázkový skript pro instalaci serveru vyžádaných replikací s také najdete příklad toho, jak automaticky řídit nastavení souboru web.config, aby se zabránilo pravděpodobné, že chyba způsobená podle typu souboru.</span><span class="sxs-lookup"><span data-stu-id="fcb25-275">The purpose of a pull server is to provide a centralized mechanism for distributing DSC configurations to client nodes.</span></span> <span data-ttu-id="fcb25-276">Tyto konfigurace jsou uloženy na serveru jako MOF dokumenty.</span><span class="sxs-lookup"><span data-stu-id="fcb25-276">The configurations are stored on the server as MOF documents.</span></span>
<span data-ttu-id="fcb25-277">Každý dokument budou mít názvy jedinečný identifikátor GUID.</span><span class="sxs-lookup"><span data-stu-id="fcb25-277">Each document will be named with a unique GUID.</span></span> <span data-ttu-id="fcb25-278">Když jsou klienti nakonfigurováni pro připojení k serveru vyžádané replikace, jsou také uvedeny identifikátor GUID pro konfiguraci, kterou by měl žádat o.</span><span class="sxs-lookup"><span data-stu-id="fcb25-278">When clients are configured to connect with a pull server, they are also given the GUID for the configuration they should request.</span></span> <span data-ttu-id="fcb25-279">Tento systém odkazuje na konfigurace podle identifikátoru GUID zaručuje jedinečnost globální a je flexibilní, takže konfiguraci lze použít s členitosti podle počtu uzlů, nebo jako konfiguraci role, která zahrnuje mnoho serverů, které by měly mít stejné konfigurace.</span><span class="sxs-lookup"><span data-stu-id="fcb25-279">This system of referencing configurations by GUID guarantees global uniqueness and is flexible such that a configuration can be applied with granularity per node, or as a role configuration that spans many servers that should have identical configurations.</span></span>

#### <a name="guids"></a><span data-ttu-id="fcb25-280">Identifikátory GUID</span><span class="sxs-lookup"><span data-stu-id="fcb25-280">GUIDs</span></span>

<span data-ttu-id="fcb25-281">Plánování konfigurace GUID je vhodné další pozornost dala až po nasazení serveru o přijetí změn.</span><span class="sxs-lookup"><span data-stu-id="fcb25-281">Planning for configuration GUIDs is worth additional attention when thinking through a pull server deployment.</span></span> <span data-ttu-id="fcb25-282">Neexistuje žádný konkrétní požadavek, způsob zpracování identifikátory GUID a proces je pravděpodobně být jedinečný pro každé prostředí.</span><span class="sxs-lookup"><span data-stu-id="fcb25-282">There is no specific requirement for how to handle GUIDs and the process is likely to be unique for each environment.</span></span> <span data-ttu-id="fcb25-283">Proces může být v rozsahu od jednoduché složité: centrálně uloženého souboru CSV, jednoduché tabulky SQL, databáze CMDB nebo komplexní řešení, která vyžadují integraci s jiným řešením nástroj nebo softwaru.</span><span class="sxs-lookup"><span data-stu-id="fcb25-283">The process can range from simple to complex: a centrally stored CSV file, a simple SQL table, a CMDB, or a complex solution requiring integration with another tool or software solution.</span></span> <span data-ttu-id="fcb25-284">Existují dvě obecné metody:</span><span class="sxs-lookup"><span data-stu-id="fcb25-284">There are two general approaches:</span></span>

- <span data-ttu-id="fcb25-285">**Přiřazení identifikátory GUID na server** – poskytuje míru záruky, že všechny konfigurace serveru je řízen jednotlivě.</span><span class="sxs-lookup"><span data-stu-id="fcb25-285">**Assigning GUIDs per server** — Provides a measure of assurance that every server configuration is controlled individually.</span></span> <span data-ttu-id="fcb25-286">To poskytuje úroveň přesnosti kolem aktualizace a může fungovat i v prostředí s několika servery.</span><span class="sxs-lookup"><span data-stu-id="fcb25-286">This provides a level of precision around updates and can work well in environments with few servers.</span></span>
- <span data-ttu-id="fcb25-287">**Přiřazení identifikátory GUID na roli serveru** – všechny servery, které provádí stejnou funkci, jako jsou třeba webové servery, použijte stejný identifikátor GUID odkazovat na požadované konfigurační data.</span><span class="sxs-lookup"><span data-stu-id="fcb25-287">**Assigning GUIDs per server role** — All servers that perform the same function, such as web servers, use the same GUID to reference the required configuration data.</span></span>  <span data-ttu-id="fcb25-288">Mějte na paměti, že pokud mnoho serverů sdílejí stejný identifikátor GUID, všechny z nich se aktualizují najednou při změně konfigurace.</span><span class="sxs-lookup"><span data-stu-id="fcb25-288">Be aware that if many servers share the same GUID, all of them would be updated simultaneously when the configuration changes.</span></span>

  <span data-ttu-id="fcb25-289">Identifikátor GUID je něco, co by měl být citlivá data vzhledem k tomu, že může využít uživatel s úmyslem získat informace o tom, jak jsou servery nasazené a nakonfigurovaných ve vašem prostředí.</span><span class="sxs-lookup"><span data-stu-id="fcb25-289">The GUID is something that should be considered sensitive data because it could be leveraged by someone with malicious intent to gain intelligence about how servers are deployed and configured in your environment.</span></span> <span data-ttu-id="fcb25-290">Další informace najdete v tématu [bezpečně přidělování identifikátorů GUID v prostředí PowerShell Desired State Configuration o přijetí změn režimu](https://blogs.msdn.microsoft.com/powershell/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode/).</span><span class="sxs-lookup"><span data-stu-id="fcb25-290">For more information, see [Securely allocating GUIDs in PowerShell Desired State Configuration Pull Mode](https://blogs.msdn.microsoft.com/powershell/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode/).</span></span>

<span data-ttu-id="fcb25-291">Plánování úkolů</span><span class="sxs-lookup"><span data-stu-id="fcb25-291">Planning task</span></span>|
---|
<span data-ttu-id="fcb25-292">Kdo bude zodpovídat za konfigurací v kopírování do složky na serveru o přijetí změn, jakmile jsou připravené?</span><span class="sxs-lookup"><span data-stu-id="fcb25-292">Who will be responsible for copying configurations in to the pull server folder when they are ready?</span></span>|
<span data-ttu-id="fcb25-293">Pokud konfigurace vytvořené týmem aplikace, co proces bude je předat?</span><span class="sxs-lookup"><span data-stu-id="fcb25-293">If Configurations are authored by an application team, what will the process be to hand them off?</span></span>|
<span data-ttu-id="fcb25-294">Bude využívat úložiště k ukládání konfigurace podle jejich probíhá čtení zleva doprava, napříč týmy?</span><span class="sxs-lookup"><span data-stu-id="fcb25-294">Will you leverage a repository to store configurations as they are being authored, across teams?</span></span>|
<span data-ttu-id="fcb25-295">Můžete automatizovat proces kopírování konfigurace do serveru a vytváření kontrolní součet, jakmile jsou připravené?</span><span class="sxs-lookup"><span data-stu-id="fcb25-295">Will you automate the process of copying configurations to the server and creating a checksum when they are ready?</span></span>|
<span data-ttu-id="fcb25-296">Jak se namapujete identifikátory GUID na servery nebo role a kdy to se uloží?</span><span class="sxs-lookup"><span data-stu-id="fcb25-296">How will you map GUIDs to servers or roles, and where will this be stored?</span></span>|
<span data-ttu-id="fcb25-297">Co budete používat jako proces ke konfiguraci klientských počítačů a jak ji integrovat s vaším procesem pro vytváření a ukládání konfigurace identifikátory GUID?</span><span class="sxs-lookup"><span data-stu-id="fcb25-297">What will you use as a process to configure client machines, and how will it integrate with your process for creating and storing Configuration GUIDs?</span></span>|

## <a name="installation-guide"></a><span data-ttu-id="fcb25-298">Průvodce instalací</span><span class="sxs-lookup"><span data-stu-id="fcb25-298">Installation Guide</span></span>

<span data-ttu-id="fcb25-299">*Skripty, které jsou uvedené v tomto dokumentu jsou stabilní příklady. Vždy zkontrolujte pečlivě skripty před spuštěním v produkčním prostředí.*</span><span class="sxs-lookup"><span data-stu-id="fcb25-299">*Scripts given in this document are stable examples. Always review scripts carefully before executing them in a production environment.*</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fcb25-300">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="fcb25-300">Prerequisites</span></span>

<span data-ttu-id="fcb25-301">Chcete-li ověřit verzi prostředí PowerShell na vašem serveru použijte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="fcb25-301">To verify the version of PowerShell on your server use the following command.</span></span>

```powershell
$PSVersionTable.PSVersion
```

<span data-ttu-id="fcb25-302">Pokud je to možné upgradujte na nejnovější verzi Windows Management Framework.</span><span class="sxs-lookup"><span data-stu-id="fcb25-302">If possible, upgrade to the latest version of Windows Management Framework.</span></span>
<span data-ttu-id="fcb25-303">Dále si stáhněte `xPsDesiredStateConfiguration` modul pomocí následujícího příkazu.</span><span class="sxs-lookup"><span data-stu-id="fcb25-303">Next, download the `xPsDesiredStateConfiguration` module using the following command.</span></span>

```powershell
Install-Module xPSDesiredStateConfiguration
```

<span data-ttu-id="fcb25-304">Příkaz vyzve ke schválení před stažením modulu.</span><span class="sxs-lookup"><span data-stu-id="fcb25-304">The command will ask for your approval before downloading the module.</span></span>

### <a name="installation-and-configuration-scripts"></a><span data-ttu-id="fcb25-305">Instalace a konfigurace skriptů</span><span class="sxs-lookup"><span data-stu-id="fcb25-305">Installation and configuration scripts</span></span>

<span data-ttu-id="fcb25-306">Nejlepší metodou k nasazení serveru vyžádané replikace DSC je použití skriptu konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="fcb25-306">The best method to deploy a DSC pull server is to use a DSC configuration script.</span></span> <span data-ttu-id="fcb25-307">Tento dokument zobrazíte skripty, včetně obě základní nastavení, které by konfigurovat jenom webovou službu DSC a upřesňující nastavení, která by konfigurovat Windows Server začátku do konce včetně DSC webové služby.</span><span class="sxs-lookup"><span data-stu-id="fcb25-307">This document will present scripts including both basic settings that would configure only the DSC web service and advanced settings that would configure a Windows Server end-to-end including DSC web service.</span></span>

<span data-ttu-id="fcb25-308">Poznámka: Aktuálně `xPSDesiredStateConfiguation` DSC modul vyžaduje serveru, aby se národního prostředí EN-US.</span><span class="sxs-lookup"><span data-stu-id="fcb25-308">Note:  Currently the `xPSDesiredStateConfiguation` DSC module requires the server to be EN-US locale.</span></span>

### <a name="basic-configuration-for-windows-server-2012"></a><span data-ttu-id="fcb25-309">Základní konfigurace pro Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="fcb25-309">Basic configuration for Windows Server 2012</span></span>

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

### <a name="advanced-configuration-for-windows-server-2012-r2"></a><span data-ttu-id="fcb25-310">Upřesňující konfigurace pro Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="fcb25-310">Advanced configuration for Windows Server 2012 R2</span></span>

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

### <a name="verify-pull-server-functionality"></a><span data-ttu-id="fcb25-311">Ověřte funkčnost serveru o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="fcb25-311">Verify pull server functionality</span></span>

```powershell
# This function is meant to simplify a check against a DSC pull server. If you do not use the default service URL, you will need to adjust accordingly.
function Verify-DSCPullServer ($fqdn) {
    ([xml](Invoke-WebRequest "https://$($fqdn):8080/psdscpullserver.svc" | % Content)).service.workspace.collection.href
}

Verify-DSCPullServer 'INSERT SERVER FQDN'
```

```output
Expected Result:
Action
Module
StatusReport
Node
```

### <a name="configure-clients"></a><span data-ttu-id="fcb25-312">Konfigurace klientů</span><span class="sxs-lookup"><span data-stu-id="fcb25-312">Configure clients</span></span>

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

## <a name="additional-references-snippets-and-examples"></a><span data-ttu-id="fcb25-313">Další odkazy na fragmenty kódu a příklady</span><span class="sxs-lookup"><span data-stu-id="fcb25-313">Additional references, snippets, and examples</span></span>

<span data-ttu-id="fcb25-314">Tento příklad ukazuje, jak ručně zahájit připojení klienta (vyžaduje WMF5) pro účely testování.</span><span class="sxs-lookup"><span data-stu-id="fcb25-314">This example shows how to manually initiate a client connection (requires WMF5) for testing.</span></span>

```powershell
Update-DscConfiguration –Wait -Verbose
```

<span data-ttu-id="fcb25-315">[Přidat DnsServerResourceRecordName](http://bit.ly/1G1H31L) rutina se používá k přidání typ záznamu CNAME do zóny DNS.</span><span class="sxs-lookup"><span data-stu-id="fcb25-315">The [Add-DnsServerResourceRecordName](http://bit.ly/1G1H31L) cmdlet is used to add a type CNAME record to a DNS zone.</span></span>

<span data-ttu-id="fcb25-316">Funkce, prostředí PowerShell [vytvoření kontrolního součtu a publikovat MOF DSC na serveru vyžádané replikace SMB](https://gallery.technet.microsoft.com/scriptcenter/PowerShell-Function-to-3bc4b7f0) automaticky vytvoří požadované kontrolního součtu a pak zkopíruje MOF konfigurace i soubory kontrolního součtu serveru vyžádané replikace SMB.</span><span class="sxs-lookup"><span data-stu-id="fcb25-316">The PowerShell Function to [Create a Checksum and Publish DSC MOF to SMB Pull Server](https://gallery.technet.microsoft.com/scriptcenter/PowerShell-Function-to-3bc4b7f0) automatically generates the required checksum, and then copies both the MOF configuration and checksum files to the SMB pull server.</span></span>

## <a name="appendix---understanding-odata-service-data-file-types"></a><span data-ttu-id="fcb25-317">Příloha – Principy ODATA typy dat služby souborů</span><span class="sxs-lookup"><span data-stu-id="fcb25-317">Appendix - Understanding ODATA service data file types</span></span>

<span data-ttu-id="fcb25-318">Datový soubor je uložen vytvořit informace během nasazování serveru vyžádané replikace, který obsahuje webovou službu OData.</span><span class="sxs-lookup"><span data-stu-id="fcb25-318">A data file is stored to create information during deployment of a pull server that includes the OData web service.</span></span> <span data-ttu-id="fcb25-319">Typ souboru závisí na operačním systému, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="fcb25-319">The type of file depends on the operating system, as described below.</span></span>

- <span data-ttu-id="fcb25-320">**Windows Server 2012** typ souboru bude vždy .mdb</span><span class="sxs-lookup"><span data-stu-id="fcb25-320">**Windows Server 2012** The file type will always be   .mdb</span></span>
- <span data-ttu-id="fcb25-321">**Windows Server 2012 R2** typ souboru se ve výchozím nastavení .edb v konfiguraci je uvedeno .mdb</span><span class="sxs-lookup"><span data-stu-id="fcb25-321">**Windows Server 2012 R2** The file type will default to .edb unless a .mdb is specified in the configuration</span></span>

<span data-ttu-id="fcb25-322">V [Advanced ukázkový skript](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) pro instalaci serveru vyžádaných replikací s také najdete příklad toho, jak automaticky řídit nastavení souboru web.config, aby se zabránilo pravděpodobné, že chyba způsobená podle typu souboru.</span><span class="sxs-lookup"><span data-stu-id="fcb25-322">In the [Advanced example script](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) for installing a Pull Server, you will also find an example of how to automatically control the web.config file settings to prevent any chance of error caused by file type.</span></span>