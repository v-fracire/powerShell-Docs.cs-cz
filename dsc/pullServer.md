---
ms.date: 04/11/2018
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Načítací služba DSC
ms.openlocfilehash: 057da50843e79ae31eef4fea1fa58e882a9d1ace
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189988"
---
# <a name="desired-state-configuration-pull-service"></a><span data-ttu-id="ffaa1-103">Vyžádání služba Konfigurace požadovaného stavu</span><span class="sxs-lookup"><span data-stu-id="ffaa1-103">Desired State Configuration Pull Service</span></span>

> <span data-ttu-id="ffaa1-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ffaa1-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffaa1-105">Server pro vyžádání obsahu (funkce systému Windows *DSC služby*) je podporované součásti systému Windows Server jsou však nejsou žádné plány, které nabízí nové funkce nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="ffaa1-106">Doporučujeme začít Přechod spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace s v systému Windows Server) nebo jedno z řešení komunity uvedené [zde](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="ffaa1-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="ffaa1-107">Správce místní konfigurace můžou být centrálně spravované řešením pro vyžádání obsahu služby.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-107">Local Configuration Manager can be centrally managed by a Pull Service solution.</span></span>
<span data-ttu-id="ffaa1-108">Pokud používáte tuto metodu, je uzlu, který je spravován zaregistrován službou a přiřazen konfiguraci v LCM nastavení.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-108">When using this approach, the node that is being managed is registered with a service and assigned a configuration in LCM settings.</span></span>
<span data-ttu-id="ffaa1-109">Konfigurace a všechny prostředky DSC potřebné jako závislosti pro konfiguraci se stáhnout do počítače a používá LCM ke správě konfigurace.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-109">The configuration and all DSC resources needed as dependencies for the configuration are downloaded to the machine and used by LCM to manage the configuration.</span></span>
<span data-ttu-id="ffaa1-110">Informace o stavu je počítač spravován se odešlou do služby pro vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-110">Information about the state of the machine being managed is uploaded to the service for reporting.</span></span>
<span data-ttu-id="ffaa1-111">Tento koncept se označuje jako "vyžádání služba".</span><span class="sxs-lookup"><span data-stu-id="ffaa1-111">This concept is referred to as "pull service."</span></span>

<span data-ttu-id="ffaa1-112">Aktuální možnosti pro vyžádání obsahu službu:</span><span class="sxs-lookup"><span data-stu-id="ffaa1-112">The current options for pull service include:</span></span>

- <span data-ttu-id="ffaa1-113">Služba konfigurace stavu žádaný automatizace Azure</span><span class="sxs-lookup"><span data-stu-id="ffaa1-113">Azure Automation Desired State Configuration service</span></span>
- <span data-ttu-id="ffaa1-114">Vyžádání služby spuštěné v systému Windows Server</span><span class="sxs-lookup"><span data-stu-id="ffaa1-114">A pull service running on Windows Server</span></span>
- <span data-ttu-id="ffaa1-115">Komunita udržovat open-source řešení</span><span class="sxs-lookup"><span data-stu-id="ffaa1-115">Community maintained open-source solutions</span></span>
- <span data-ttu-id="ffaa1-116">Sdílené složce SMB</span><span class="sxs-lookup"><span data-stu-id="ffaa1-116">An SMB share</span></span>

<span data-ttu-id="ffaa1-117">**Doporučené řešení**, a s nejvíce funkcemi, které jsou k dispozici, není [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ffaa1-117">**The recommended solution**, and the option with the most features available, is [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span></span>

<span data-ttu-id="ffaa1-118">Uzly na místě v datových centrech privátní nebo veřejné cloudy, například Azure a AWS můžete spravovat službu Azure.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-118">The Azure service can manage nodes on-premises in private datacenters, or in public clouds such as Azure and AWS.</span></span>
<span data-ttu-id="ffaa1-119">U privátních prostředí, kde nelze servery připojit přímo k Internetu, zvažte omezení odchozí provoz jenom publikované Azure rozsah IP adres (viz [rozsahy IP Datacentra Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span><span class="sxs-lookup"><span data-stu-id="ffaa1-119">For private environments where servers cannot directly connect to the Internet, consider limiting outbound traffic to only the published Azure IP range (see [Azure Datacenter IP Ranges](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).</span></span>

<span data-ttu-id="ffaa1-120">Funkce služby online, které nejsou momentálně k dispozici ve službě vyžádání v systému Windows Server:</span><span class="sxs-lookup"><span data-stu-id="ffaa1-120">Features of the online service that are not currently available in the pull service on Windows Server include:</span></span>
- <span data-ttu-id="ffaa1-121">Všechna data se šifrují během přenosu a v klidovém stavu</span><span class="sxs-lookup"><span data-stu-id="ffaa1-121">All data is encrypted in transit and at rest</span></span>
- <span data-ttu-id="ffaa1-122">Klientské certifikáty se vytváří a spravují automaticky</span><span class="sxs-lookup"><span data-stu-id="ffaa1-122">Client certificates are created and managed automatically</span></span>
- <span data-ttu-id="ffaa1-123">Ukládat tajné klíče pro centrální správu [hesla nebo přihlašovací údaje](/azure/automation/automation-credentials), nebo [proměnné](/azure/automation/automation-variables) například názvy serverů nebo připojovací řetězce</span><span class="sxs-lookup"><span data-stu-id="ffaa1-123">Secrets store for centrally managing [passwords/credentials](/azure/automation/automation-credentials), or [variables](/azure/automation/automation-variables) such as server names or connection strings</span></span>
- <span data-ttu-id="ffaa1-124">Centrálně spravovat uzlu [LCM konfigurace](metaConfig.md#basic-settings)</span><span class="sxs-lookup"><span data-stu-id="ffaa1-124">Centrally manage node [LCM configuration](metaConfig.md#basic-settings)</span></span>
- <span data-ttu-id="ffaa1-125">Centrálně přiřadit konfigurace pro klienta uzly</span><span class="sxs-lookup"><span data-stu-id="ffaa1-125">Centrally assign configurations to client nodes</span></span>
- <span data-ttu-id="ffaa1-126">Konfigurace verze se změní na "lesknice skupiny" pro testování dříve, než dorazila produkční</span><span class="sxs-lookup"><span data-stu-id="ffaa1-126">Release configuration changes to "canary groups" for testing before reaching production</span></span>
- <span data-ttu-id="ffaa1-127">Grafické vytváření sestav</span><span class="sxs-lookup"><span data-stu-id="ffaa1-127">Graphical reporting</span></span>
  - <span data-ttu-id="ffaa1-128">Podrobná sestava stavu na úrovni prostředků DSC členitosti</span><span class="sxs-lookup"><span data-stu-id="ffaa1-128">Status detail at the DSC resource level of granularity</span></span>
  - <span data-ttu-id="ffaa1-129">Podrobné chybové zprávy z klientských počítačů pro řešení potíží</span><span class="sxs-lookup"><span data-stu-id="ffaa1-129">Verbose error messages from client machines for troubleshooting</span></span>
- <span data-ttu-id="ffaa1-130">[Integrace s Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) pro výstrahy, automatizované úlohy, aplikace pro Android nebo iOS pro vytváření sestav a výstrahy</span><span class="sxs-lookup"><span data-stu-id="ffaa1-130">[Integration with Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) for alerting, automated tasks, Android/iOS app for reporting and alerting</span></span>

## <a name="dsc-pull-service-in-windows-server"></a><span data-ttu-id="ffaa1-131">DSC vyžádání služby v systému Windows Server</span><span class="sxs-lookup"><span data-stu-id="ffaa1-131">DSC pull service in Windows Server</span></span>

<span data-ttu-id="ffaa1-132">Je možné ke konfiguraci služby přijetí změn pro spouštění v systému Windows Server.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-132">It is possible to configuring a pull service to run on Windows Server.</span></span>
<span data-ttu-id="ffaa1-133">Se doporučuje, aby řešení služby vyžádání obsahu, který je součástí systému Windows Server obsahuje pouze funkce ukládání konfigurace nebo moduly pro stahování a zaznamenávání dat sestav v databázi.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-133">Be advised that the pull service solution included in Windows Server includes only capabilities of storing configurations/modules for download and capturing report data in to database.</span></span>
<span data-ttu-id="ffaa1-134">Nezahrnuje řadu funkce nabízené služby v Azure a proto není funkční nástroj pro vyhodnocení, jak se použije službu.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-134">It does not include many of the capabilities offered by the service in Azure and so is not a good tool for evaluating how the service would be used.</span></span>

<span data-ttu-id="ffaa1-135">Službu vyžádání obsahu k dispozici v systému Windows Server je webová služba ve službě IIS, který používá rozhraní OData k dispozici DSC konfigurační soubory do cílové uzly uzly, zeptejte se pro ně.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-135">The pull service offered in Windows Server is a web service in IIS that uses an OData interface to make DSC configuration files available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="ffaa1-136">Požadavky pro používání serveru vyžádané replikace:</span><span class="sxs-lookup"><span data-stu-id="ffaa1-136">Requirements for using a pull server:</span></span>

- <span data-ttu-id="ffaa1-137">Serveru se systémem:</span><span class="sxs-lookup"><span data-stu-id="ffaa1-137">A server running:</span></span>
  - <span data-ttu-id="ffaa1-138">WMF nebo PowerShell 5.0 nebo novější</span><span class="sxs-lookup"><span data-stu-id="ffaa1-138">WMF/PowerShell 5.0 or greater</span></span>
  - <span data-ttu-id="ffaa1-139">Role serveru IIS</span><span class="sxs-lookup"><span data-stu-id="ffaa1-139">IIS server role</span></span>
  - <span data-ttu-id="ffaa1-140">DSC služby</span><span class="sxs-lookup"><span data-stu-id="ffaa1-140">DSC Service</span></span>
- <span data-ttu-id="ffaa1-141">V ideálním případě některé znamená generování certifikát, k zabezpečení přihlašovacích údajů předaných na místní Configuration Manager (LCM) na cílové uzly</span><span class="sxs-lookup"><span data-stu-id="ffaa1-141">Ideally, some means of generating a certificate, to secure credentials passed to the Local Configuration Manager (LCM) on target nodes</span></span>

<span data-ttu-id="ffaa1-142">Nejlepší způsob, jak konfigurovat Windows Server k hostitelské službě. vyžádanou je použití konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-142">The best way to configure Windows Server to host pull service is to use a DSC configuration.</span></span>
<span data-ttu-id="ffaa1-143">Ukázkový skript je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-143">An example script is provided below.</span></span>

### <a name="supported-database-systems"></a><span data-ttu-id="ffaa1-144">Podporované databázové systémy</span><span class="sxs-lookup"><span data-stu-id="ffaa1-144">Supported database systems</span></span>

|<span data-ttu-id="ffaa1-145">FORMÁT WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="ffaa1-145">WMF 4.0</span></span>   |<span data-ttu-id="ffaa1-146">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="ffaa1-146">WMF 5.0</span></span>  |<span data-ttu-id="ffaa1-147">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="ffaa1-147">WMF 5.1</span></span> |<span data-ttu-id="ffaa1-148">Podpora produktu WMF (Windows Server zevnitř Preview 17090) 5.1</span><span class="sxs-lookup"><span data-stu-id="ffaa1-148">WMF 5.1 (Windows Server Insider Preview 17090)</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="ffaa1-149">MDB</span><span class="sxs-lookup"><span data-stu-id="ffaa1-149">MDB</span></span>     |<span data-ttu-id="ffaa1-150">ESENT (výchozí), MDB</span><span class="sxs-lookup"><span data-stu-id="ffaa1-150">ESENT (Default), MDB</span></span> |<span data-ttu-id="ffaa1-151">ESENT (výchozí), MDB</span><span class="sxs-lookup"><span data-stu-id="ffaa1-151">ESENT (Default), MDB</span></span>|<span data-ttu-id="ffaa1-152">ESENT (výchozí), SQL Server, MDB</span><span class="sxs-lookup"><span data-stu-id="ffaa1-152">ESENT (Default), SQL Server, MDB</span></span>

<span data-ttu-id="ffaa1-153">Od verze 17090 z [systému Windows Server zevnitř Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server je podporovaná možnost pro službu pro vyžádání obsahu (funkce systému Windows *DSC služby*).</span><span class="sxs-lookup"><span data-stu-id="ffaa1-153">Starting in release 17090 of [Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server is a supported option for the Pull Service (Windows Feature *DSC-Service*).</span></span>  <span data-ttu-id="ffaa1-154">To nabízí novou možnost pro škálování velkých prostředích DSC, které nebyly migrovány do [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ffaa1-154">This provides a new option for scaling large DSC environments that have not migrated to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).</span></span>

> <span data-ttu-id="ffaa1-155">**Poznámka:**: podpora systému SQL Server se nepřidají k předchozí verze 5.1 WMF (nebo starší) a bude k dispozici v systému Windows Server verze větší než nebo rovna hodnotě 17090 pouze.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-155">**Note**: SQL Server support will not be added to previous versions of WMF 5.1 (or earlier) and will only be available on Windows Server versions greater than or equal to 17090.</span></span>

<span data-ttu-id="ffaa1-156">Konfigurace serveru vyžádané replikace pro použití systému SQL Server, nastavte **SqlProvider** k `$true` a **SqlConnectionString** na platný připojovací řetězec SQL serveru.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-156">To configure the pull server to use SQL Server, set **SqlProvider** to `$true` and **SqlConnectionString** to a valid SQL Server Connection String.</span></span>  <span data-ttu-id="ffaa1-157">Další informace najdete v tématu [SqlClient připojovací řetězce](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).</span><span class="sxs-lookup"><span data-stu-id="ffaa1-157">For more information, see [SqlClient Connection Strings](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).</span></span>
<span data-ttu-id="ffaa1-158">Příklad konfigurace SQL serveru s **xDscWebService**, nejdřív přečíst [pomocí prostředků xDscWebService](#using-the-xdscwebservice-resource) a poté zkontrolovat [Sample_xDscWebServiceRegistration_ UseSQLProvider.ps1 na Githubu](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).</span><span class="sxs-lookup"><span data-stu-id="ffaa1-158">For an example of SQL Server configuration with **xDscWebService**, first read [Using the xDscWebService resource](#using-the-xdscwebservice-resource) and then review [Sample_xDscWebServiceRegistration_UseSQLProvider.ps1 on GitHub](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).</span></span>

### <a name="using-the-xdscwebservice-resource"></a><span data-ttu-id="ffaa1-159">Pomocí xDscWebService prostředků</span><span class="sxs-lookup"><span data-stu-id="ffaa1-159">Using the xDscWebService resource</span></span>

<span data-ttu-id="ffaa1-160">Nejjednodušší způsob, jak nastavit webový server vyžádání obsahu je použití **xDscWebService** prostředku, které jsou součástí **xPSDesiredStateConfiguration** modulu.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-160">The easiest way to set up a web pull server is to use the **xDscWebService** resource, included in the **xPSDesiredStateConfiguration** module.</span></span>
<span data-ttu-id="ffaa1-161">Následující kroky popisují, jak se daný prostředek v konfiguraci, která nastaví webovou službu.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-161">The following steps explain how to use the resource in a configuration that sets up the web service.</span></span>

1. <span data-ttu-id="ffaa1-162">Volání [instalace modulu](/powershell/module/PowershellGet/Install-Module) k instalaci **xPSDesiredStateConfiguration** modulu.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-162">Call the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xPSDesiredStateConfiguration** module.</span></span> <span data-ttu-id="ffaa1-163">**Poznámka:**: **instalace modulu** je součástí **PowerShellGet** modul, který je součástí prostředí PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-163">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="ffaa1-164">Si můžete stáhnout **PowerShellGet** modul pro prostředí PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="ffaa1-164">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>
1. <span data-ttu-id="ffaa1-165">Získání certifikátu SSL pro vyžádání obsahu DSC server od důvěryhodné certifikační autority, buď v rámci vaší organizace nebo z veřejné autority.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-165">Get an SSL certificate for the DSC Pull server from a trusted Certificate Authority, either within your organization or a public authority.</span></span> <span data-ttu-id="ffaa1-166">Certifikát obdržený od autority je obvykle ve formátu PFX.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-166">The certificate received from the authority is usually in the PFX format.</span></span> <span data-ttu-id="ffaa1-167">Nainstalujte certifikát na uzlu, který se stane DSC vyžádání serveru ve výchozím umístění, které by se měly CERT: \LocalMachine\My.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-167">Install the certificate on the node that will become the DSC Pull server in the default location, which should be CERT:\LocalMachine\My.</span></span> <span data-ttu-id="ffaa1-168">Poznamenejte si kryptografický otisk certifikátu.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-168">Make a note of the certificate thumbprint.</span></span>
1. <span data-ttu-id="ffaa1-169">Vyberte identifikátor GUID, který má být použit jako registrační klíč.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-169">Select a GUID to be used as the Registration Key.</span></span> <span data-ttu-id="ffaa1-170">Generovat jednu pomocí prostředí PowerShell zadejte následující PS řádku a stiskněte klávesu enter: '``` [guid]::newGuid()```'nebo'```New-Guid```'.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-170">To generate one using PowerShell enter the following at the PS prompt and press enter: '``` [guid]::newGuid()```' or '```New-Guid```'.</span></span> <span data-ttu-id="ffaa1-171">Tento klíč se použije klient uzly jako sdílený klíč k ověření během registrace.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-171">This key will be used by client nodes as a shared key to authenticate during registration.</span></span> <span data-ttu-id="ffaa1-172">Další informace najdete v části registrační klíč níže.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-172">For more information, see the Registration Key section below.</span></span>
1. <span data-ttu-id="ffaa1-173">V integrovaném Skriptovacím prostředí PowerShell, spusťte (F5) následující konfigurační skript (zahrnutý ve složce Příklady **xPSDesiredStateConfiguration** modulu jako Sample_xDscWebServiceRegistration.ps1).</span><span class="sxs-lookup"><span data-stu-id="ffaa1-173">In the PowerShell ISE, start (F5) the following configuration script (included in the Examples folder of the  **xPSDesiredStateConfiguration** module as Sample_xDscWebServiceRegistration.ps1).</span></span> <span data-ttu-id="ffaa1-174">Tento skript nastaví server vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-174">This script sets up the pull server.</span></span>

```powershell
configuration Sample_xDscWebServiceRegistration
{
    param
    (
        [string[]]$NodeName = 'localhost',

        [ValidateNotNullOrEmpty()]
        [string] $certificateThumbPrint,

        [Parameter(HelpMessage='This should be a string with enough entropy (randomness) to protect the registration of clients to the pull server.  We will use new GUID by default.')]
        [ValidateNotNullOrEmpty()]
        [string] $RegistrationKey   # A guid that clients use to initiate conversation with pull server
    )

    Import-DSCResource -ModuleName xPSDesiredStateConfiguration

    Node $NodeName
    {
        WindowsFeature DSCServiceFeature
        {
            Ensure = "Present"
            Name   = "DSC-Service"
        }

        xDscWebService PSDSCPullServer
        {
            Ensure                  = "Present"
            EndpointName            = "PSDSCPullServer"
            Port                    = 8080
            PhysicalPath            = "$env:SystemDrive\inetpub\PSDSCPullServer"
            CertificateThumbPrint   = $certificateThumbPrint
            ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
            ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
            State                   = "Started"
            DependsOn               = "[WindowsFeature]DSCServiceFeature"
            RegistrationKeyPath     = "$env:PROGRAMFILES\WindowsPowerShell\DscService"
            AcceptSelfSignedCertificates = $true
            Enable32BitAppOnWin64   = $false
        }

        File RegistrationKeyFile
        {
            Ensure          = 'Present'
            Type            = 'File'
            DestinationPath = "$env:ProgramFiles\WindowsPowerShell\DscService\RegistrationKeys.txt"
            Contents        = $RegistrationKey
        }
    }
}
```

1. <span data-ttu-id="ffaa1-175">Spustit v konfiguraci předávání kryptografický otisk certifikátu SSL, jako **certificateThumbPrint** parametr a identifikátor GUID registrační klíč jako **RegistrationKey** parametr:</span><span class="sxs-lookup"><span data-stu-id="ffaa1-175">Run the configuration, passing the thumbprint of the SSL certificate as the **certificateThumbPrint** parameter and a GUID registration key as the **RegistrationKey** parameter:</span></span>

```powershell
# To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store
# and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
dir Cert:\LocalMachine\my

# Then include this thumbprint when running the configuration
Sample_xDSCPullServer -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

# Run the compiled configuration to make the target node a DSC Pull Server
Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
```

#### <a name="registration-key"></a><span data-ttu-id="ffaa1-176">Registrační klíč</span><span class="sxs-lookup"><span data-stu-id="ffaa1-176">Registration Key</span></span>

<span data-ttu-id="ffaa1-177">Povolit klientské uzly registraci se serverem a používají názvy konfigurace místo ID konfigurace, registrační klíč, který byl vytvořen výše konfigurace je uložen v souboru s názvem `RegistrationKeys.txt` v `C:\Program Files\WindowsPowerShell\DscService`.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-177">To allow client nodes to register with the server so that they can use configuration names instead of a configuration ID, a registration key that was created by the above configuration is saved in a file named `RegistrationKeys.txt` in `C:\Program Files\WindowsPowerShell\DscService`.</span></span> <span data-ttu-id="ffaa1-178">Registrační klíč funguje jako sdílený tajný klíč používá při počáteční registraci klienta se serverem pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-178">The registration key functions as a shared secret used during the initial registration by the client with the pull server.</span></span> <span data-ttu-id="ffaa1-179">Klient vygeneruje certifikát podepsaný svým držitelem, který slouží k jednoznačné ověření na serveru vyžádané replikace po úspěšném dokončení registrace se.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-179">The client will generate a self-signed certificate that is used to uniquely authenticate to the pull server once registration is successfully completed.</span></span> <span data-ttu-id="ffaa1-180">Kryptografický otisk tohoto certifikátu je uložený místně a přidružené k adrese URL serveru pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-180">The thumbprint of this certificate is stored locally and associated with the URL of the pull server.</span></span>
> <span data-ttu-id="ffaa1-181">**Poznámka:**: registrace klíče nejsou podporovány v prostředí PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-181">**Note**: Registration keys are not supported in PowerShell 4.0.</span></span>

<span data-ttu-id="ffaa1-182">Chcete-li nakonfigurovat uzel k ověření se serverem pro vyžádání obsahu, registrační klíč musí být v metakonfiguraci pro cílový uzel, který bude registrace k tomuto serveru pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-182">In order to configure a node to authenticate with the pull server, the registration key needs to be in the metaconfiguration for any target node that will be registering with this pull server.</span></span> <span data-ttu-id="ffaa1-183">Všimněte si, že **RegistrationKey** v metakonfiguraci níže se odebere po úspěšně zaregistrovala cílový počítač, a hodnota '140a952b-b9d6-406b-b416-e0f759c9c0e4' se musí shodovat s hodnotou uloženou v RegistrationKeys.txt soubor na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-183">Note that the **RegistrationKey** in the metaconfiguration below is removed after the target machine has successfully registered, and that the value '140a952b-b9d6-406b-b416-e0f759c9c0e4' must match the value stored in the RegistrationKeys.txt file on the pull server.</span></span> <span data-ttu-id="ffaa1-184">Vždy zacházet s hodnotou klíče registrace bezpečně, protože vědomí umožňuje, aby všechny cílové počítače k registraci se serverem pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-184">Always treat the registration key value securely, because knowing it allows any target machine to register with the pull server.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration Sample_MetaConfigurationToRegisterWithLessSecurePullServer
{
    param
    (
        [ValidateNotNullOrEmpty()]
        [string] $NodeName = 'localhost',

        [ValidateNotNullOrEmpty()]
        [string] $RegistrationKey, #same as the one used to setup pull server in previous configuration

        [ValidateNotNullOrEmpty()]
        [string] $ServerName = 'localhost' #node name of the pull server, same as $NodeName used in previous configuration
    )

    Node $NodeName
    {
        Settings
        {
            RefreshMode        = 'Pull'
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = "https://$ServerName`:8080/PSDSCPullServer.svc" # notice it is https
            RegistrationKey    = $RegistrationKey
            ConfigurationNames = @('ClientConfig')
        }

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL       = "https://$ServerName`:8080/PSDSCPullServer.svc" # notice it is https
            RegistrationKey = $RegistrationKey
        }
    }
}

Sample_MetaConfigurationToRegisterWithLessSecurePullServer -RegistrationKey $RegistrationKey -OutputPath c:\Configs\TargetNodes
```

> <span data-ttu-id="ffaa1-185">**Poznámka:**: **ReportServerWeb** části umožňuje data k odeslání na server vyžádané replikace pro vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-185">**Note**: The **ReportServerWeb** section allows reporting data to be sent to the pull server.</span></span>

<span data-ttu-id="ffaa1-186">Nedostatek **ConfigurationID** vlastnost v souboru metakonfiguraci implicitně znamená serveru vyžádané replikace se nepodporuje verze V2 protokol server vyžádané replikace, a proto je požadována počáteční registrace.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-186">The lack of the **ConfigurationID** property in the metaconfiguration file implicitly means that pull server is supporting the V2 version of the pull server protocol so an initial registration is required.</span></span>
<span data-ttu-id="ffaa1-187">Naopak přítomnosti **ConfigurationID** znamená, že se používá protokol server vyžádané replikace verze V1 a neexistuje žádné zpracování registrace.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-187">Conversely, the presence of a **ConfigurationID** means that the V1 version of the pull server protocol is used and there is no registration processing.</span></span>

><span data-ttu-id="ffaa1-188">**Poznámka:**: V PUSH scénáři chyby existuje v aktuální verzi, díky které je potřeba definovat ConfigurationID vlastnost v souboru metakonfiguraci pro uzly, které nikdy zaregistrovali načítacího serveru.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-188">**Note**: In a PUSH scenario, a bug exists in the current release that makes it necessary to define a ConfigurationID property in the metaconfiguration file for nodes that have never registered with a pull server.</span></span> <span data-ttu-id="ffaa1-189">Tato akce vynutí protokol serveru vyžádané replikace V1 a vyhnout zprávy o selhání registrace.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-189">This will force the V1 Pull Server protocol and avoid registration failure messages.</span></span>

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="ffaa1-190">Umístění konfigurace a prostředky</span><span class="sxs-lookup"><span data-stu-id="ffaa1-190">Placing configurations and resources</span></span>

<span data-ttu-id="ffaa1-191">Po vyžádání obsahu server dokončení instalačního programu, složky, které jsou definované **ConfigurationPath** a **ModulePath** vlastnosti v konfiguraci serveru vyžádané replikace jsou, kam umístíte modulů a konfigurací které budou k dispozici pro cílové uzly načítat.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-191">After the pull server setup completes, the folders defined by the **ConfigurationPath** and **ModulePath** properties in the pull server configuration are where you will place modules and configurations that will be available for target nodes to pull.</span></span>
<span data-ttu-id="ffaa1-192">Tyto soubory musí být v konkrétním formátu v pořadí pro vyžádání obsahu server správně zpracovat.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-192">These files need to be in a specific format in order for the pull server to correctly process them.</span></span>

### <a name="dsc-resource-module-package-format"></a><span data-ttu-id="ffaa1-193">Formát balíčku modulu prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="ffaa1-193">DSC resource module package format</span></span>

<span data-ttu-id="ffaa1-194">Každý modul prostředků musí být ZIP a s názvem podle vzoru následující `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-194">Each resource module needs to be zipped and named according to the following pattern `{Module Name}_{Module Version}.zip`.</span></span>
<span data-ttu-id="ffaa1-195">Například modul s názvem xWebAdminstration verzí modulu 3.1.2.0 by se jmenovala 'xWebAdministration_3.2.1.0.zip'.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-195">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span>
<span data-ttu-id="ffaa1-196">Každá verze nástroje modul musí být obsažena v souboru zip jeden.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-196">Each version of a module must be contained in a single zip file.</span></span>
<span data-ttu-id="ffaa1-197">Vzhledem k tomu, že existuje jenom jedna verze nástroje prostředků do každého souboru zip, formát modulu přidána v WMF 5.0 se podpora pro více verze modulu v jednom adresáři není podporovaný.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-197">Since there is only a single version of a resource in each zip file, the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span>
<span data-ttu-id="ffaa1-198">To znamená, že před zabalení moduly prostředků DSC pro použití s načítacího serveru budete muset provést změnu malá strukturu adresáře.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-198">This means that before packaging up DSC resource modules for use with pull server you will need to make a small change to the directory structure.</span></span>
<span data-ttu-id="ffaa1-199">Výchozí formát modulů obsahující prostředek DSC v WMF 5.0 je ' {složku modulu}\{verze modulu} \DscResources\{Složka prostředků DSC}\'.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-199">The default format of modules containing DSC resource in WMF 5.0 is '{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\'.</span></span>
<span data-ttu-id="ffaa1-200">Před balení pro vyžádání obsahu serveru, odeberte **{verze modulu}** složky, stane se cesta ' {složku modulu} \DscResources\{Složka prostředků DSC}\'.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-200">Before packaging up for the pull server, remove the **{Module version}** folder so the path becomes '{Module Folder}\DscResources\{DSC Resource Folder}\'.</span></span>
<span data-ttu-id="ffaa1-201">Díky této změně zip složce, jak je popsáno výše a nastavovat tyto soubory zip v **ModulePath** složky.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-201">With this change, zip the folder as described above and place these zip files in the **ModulePath** folder.</span></span>

<span data-ttu-id="ffaa1-202">Použití `New-DscChecksum {module zip file}` vytvořit soubor kontrolního součtu pro nově přidaným modulem.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-202">Use `New-DscChecksum {module zip file}` to create a checksum file for the newly added module.</span></span>

### <a name="configuration-mof-format"></a><span data-ttu-id="ffaa1-203">Formát MOF konfigurace</span><span class="sxs-lookup"><span data-stu-id="ffaa1-203">Configuration MOF format</span></span>

<span data-ttu-id="ffaa1-204">Konfigurační soubor MOF musí být spárována s soubor kontrolního součtu, takže LCM na cílový uzel můžete konfiguraci ověřit.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-204">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span>
<span data-ttu-id="ffaa1-205">Chcete-li vytvořit kontrolní součet, zavolejte [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) rutiny.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-205">To create a checksum, call the [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) cmdlet.</span></span>
<span data-ttu-id="ffaa1-206">Rutina trvá **cesta** parametr, který určuje složku, kde se nachází v konfiguraci MOF.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-206">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span>
<span data-ttu-id="ffaa1-207">Rutina vytvoří kontrolní součet souboru s názvem `ConfigurationMOFName.mof.checksum`, kde `ConfigurationMOFName` je název konfiguračního souboru mof.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-207">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span>
<span data-ttu-id="ffaa1-208">Pokud existují minimálně jedna konfigurace soubory MOF do určené složky, vytvoří se pro každou konfiguraci ve složce kontrolní součet.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-208">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>
<span data-ttu-id="ffaa1-209">Umístěte soubory MOF a jejich přidružené kontrolního součtu souborů v **ConfigurationPath** složky.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-209">Place the MOF files and their associated checksum files in the **ConfigurationPath** folder.</span></span>

><span data-ttu-id="ffaa1-210">**Poznámka:**: Pokud změníte konfigurační soubor MOF žádným způsobem, musíte také znovu vytvořit soubor kontrolního součtu.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-210">**Note**: If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

### <a name="tooling"></a><span data-ttu-id="ffaa1-211">Nástrojů</span><span class="sxs-lookup"><span data-stu-id="ffaa1-211">Tooling</span></span>

<span data-ttu-id="ffaa1-212">Chcete-li nastavení tvoří, ověření a Správa serveru vyžádané replikace jednodušší, tyto nástroje jsou zahrnuty jako příklady v nejnovější verzi modulu xPSDesiredStateConfiguration:</span><span class="sxs-lookup"><span data-stu-id="ffaa1-212">In order to make setting up, validating and managing the pull server easier, the following tools are included as examples in the latest version of the xPSDesiredStateConfiguration module:</span></span>

1. <span data-ttu-id="ffaa1-213">Modul, který vám pomůže s balení moduly prostředků DSC a konfigurační soubory pro použití na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-213">A module that will help with packaging DSC resource modules and configuration files for use on the pull server.</span></span> <span data-ttu-id="ffaa1-214">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span><span class="sxs-lookup"><span data-stu-id="ffaa1-214">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span></span> <span data-ttu-id="ffaa1-215">Následující příklady:</span><span class="sxs-lookup"><span data-stu-id="ffaa1-215">Examples below:</span></span>

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. <span data-ttu-id="ffaa1-216">Skript, který ověří načítacího serveru správně nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-216">A script that validates the pull server is configured correctly.</span></span> <span data-ttu-id="ffaa1-217">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span><span class="sxs-lookup"><span data-stu-id="ffaa1-217">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span></span>

## <a name="community-solutions-for-pull-service"></a><span data-ttu-id="ffaa1-218">Řešení komunity pro vyžádání obsahu služby</span><span class="sxs-lookup"><span data-stu-id="ffaa1-218">Community Solutions for Pull Service</span></span>

<span data-ttu-id="ffaa1-219">Komunita DSC má vytvořené více řešení k implementaci protokol služby vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-219">The DSC community has authored multiple solutions to implement the pull service protocol.</span></span>
<span data-ttu-id="ffaa1-220">Pro místní prostředí tyto nabízí možnosti služby vyžádání obsahu a příležitost přispívání do komunity Přírůstkové vylepšení.</span><span class="sxs-lookup"><span data-stu-id="ffaa1-220">For on-premises environments, these offer pull service capabilities and an opportunity to contribute back to the community with incremental enhancements.</span></span>

- [<span data-ttu-id="ffaa1-221">Tug</span><span class="sxs-lookup"><span data-stu-id="ffaa1-221">Tug</span></span>](https://github.com/powershellorg/tug)
- [<span data-ttu-id="ffaa1-222">DSC TRÆK</span><span class="sxs-lookup"><span data-stu-id="ffaa1-222">DSC-TRÆK</span></span>](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a><span data-ttu-id="ffaa1-223">Konfigurace klienta pro vyžádání obsahu</span><span class="sxs-lookup"><span data-stu-id="ffaa1-223">Pull client configuration</span></span>

<span data-ttu-id="ffaa1-224">Následující témata popisují nastavení klientů pro vyžádání obsahu podrobně:</span><span class="sxs-lookup"><span data-stu-id="ffaa1-224">The following topics describe setting up pull clients in detail:</span></span>

- [<span data-ttu-id="ffaa1-225">Nastavení klienta vyžádání DSC pomocí ID konfigurace</span><span class="sxs-lookup"><span data-stu-id="ffaa1-225">Setting up a DSC pull client using a configuration ID</span></span>](pullClientConfigID.md)
- [<span data-ttu-id="ffaa1-226">Nastavení klienta vyžádání DSC pomocí názvy konfigurace</span><span class="sxs-lookup"><span data-stu-id="ffaa1-226">Setting up a DSC pull client using configuration names</span></span>](pullClientConfigNames.md)
- [<span data-ttu-id="ffaa1-227">Částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="ffaa1-227">Partial configurations</span></span>](partialConfigs.md)

## <a name="see-also"></a><span data-ttu-id="ffaa1-228">Viz taky</span><span class="sxs-lookup"><span data-stu-id="ffaa1-228">See also</span></span>

- [<span data-ttu-id="ffaa1-229">Přehled stavu konfigurace požadovaného prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffaa1-229">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
- [<span data-ttu-id="ffaa1-230">Přijetí konfigurace</span><span class="sxs-lookup"><span data-stu-id="ffaa1-230">Enacting configurations</span></span>](enactingConfigurations.md)
- [<span data-ttu-id="ffaa1-231">Použití serveru sestav DSC</span><span class="sxs-lookup"><span data-stu-id="ffaa1-231">Using a DSC report server</span></span>](reportServer.md)
- <span data-ttu-id="ffaa1-232">[[MS-DSCPM]: Desired State Configuration přijetí změn modelu protokolu](https://msdn.microsoft.com/library/dn393548.aspx)</span><span class="sxs-lookup"><span data-stu-id="ffaa1-232">[[MS-DSCPM]: Desired State Configuration Pull Model Protocol](https://msdn.microsoft.com/library/dn393548.aspx)</span></span>
- <span data-ttu-id="ffaa1-233">[[MS-DSCPM]: Desired State Configuration přijetí změn modelu protokol chyby](https://msdn.microsoft.com/library/mt612824.aspx)</span><span class="sxs-lookup"><span data-stu-id="ffaa1-233">[[MS-DSCPM]: Desired State Configuration Pull Model Protocol Errata](https://msdn.microsoft.com/library/mt612824.aspx)</span></span>