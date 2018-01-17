---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Nastavení webového serveru vyžádané replikace DSC"
ms.openlocfilehash: 9a09804ef0efe3e4c92923910884710187d44ac5
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="setting-up-a-dsc-web-pull-server"></a><span data-ttu-id="14417-103">Nastavení webového serveru vyžádané replikace DSC</span><span class="sxs-lookup"><span data-stu-id="14417-103">Setting up a DSC web pull server</span></span>

> <span data-ttu-id="14417-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="14417-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="14417-105">Webový server vyžádané replikace DSC je webová služba ve službě IIS, který používá rozhraní OData k dispozici DSC konfigurační soubory do cílové uzly uzly, zeptejte se pro ně.</span><span class="sxs-lookup"><span data-stu-id="14417-105">A DSC web pull server is a web service in IIS that uses an OData interface to make DSC configuration files available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="14417-106">Požadavky pro používání serveru vyžádané replikace:</span><span class="sxs-lookup"><span data-stu-id="14417-106">Requirements for using a pull server:</span></span>

* <span data-ttu-id="14417-107">Serveru se systémem:</span><span class="sxs-lookup"><span data-stu-id="14417-107">A server running:</span></span>
  - <span data-ttu-id="14417-108">WMF nebo PowerShell 5.0 nebo novější</span><span class="sxs-lookup"><span data-stu-id="14417-108">WMF/PowerShell 5.0 or greater</span></span>
  - <span data-ttu-id="14417-109">Role serveru IIS</span><span class="sxs-lookup"><span data-stu-id="14417-109">IIS server role</span></span>
  - <span data-ttu-id="14417-110">DSC služby</span><span class="sxs-lookup"><span data-stu-id="14417-110">DSC Service</span></span>
* <span data-ttu-id="14417-111">V ideálním případě některé znamená generování certifikát, k zabezpečení přihlašovacích údajů předaných na místní Configuration Manager (LCM) na cílové uzly</span><span class="sxs-lookup"><span data-stu-id="14417-111">Ideally, some means of generating a certificate, to secure credentials passed to the Local Configuration Manager (LCM) on target nodes</span></span>

<span data-ttu-id="14417-112">Role serveru IIS a DSC služby můžete přidat pomocí Průvodce přidáním rolí a funkcí ve Správci serveru nebo pomocí prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14417-112">You can add the IIS server role and DSC Service with the Add Roles and Features wizard in Server Manager, or by using PowerShell.</span></span> <span data-ttu-id="14417-113">Ukázkové skripty uvedené v tomto tématu bude zpracovávat oba tyto kroky pro vás také.</span><span class="sxs-lookup"><span data-stu-id="14417-113">The sample scripts included in this topic will handle both of these steps for you as well.</span></span>

## <a name="using-the-xdscwebservice-resource"></a><span data-ttu-id="14417-114">Pomocí xDSCWebService prostředků</span><span class="sxs-lookup"><span data-stu-id="14417-114">Using the xDSCWebService resource</span></span>
<span data-ttu-id="14417-115">Nejjednodušší způsob, jak nastavit webový server vyžádané replikace se má používat k prostředku xWebService, který je součástí modulu xPSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="14417-115">The easiest way to set up a web pull server is to use the xWebService resource, included in the xPSDesiredStateConfiguration module.</span></span> <span data-ttu-id="14417-116">Následující kroky popisují, jak se daný prostředek v konfiguraci, která nastaví webovou službu.</span><span class="sxs-lookup"><span data-stu-id="14417-116">The following steps explain how to use the resource in a configuration that sets up the web service.</span></span>

1. <span data-ttu-id="14417-117">Volání [instalace modulu](https://technet.microsoft.com/en-us/library/dn807162.aspx) k instalaci **xPSDesiredStateConfiguration** modulu.</span><span class="sxs-lookup"><span data-stu-id="14417-117">Call the [Install-Module](https://technet.microsoft.com/en-us/library/dn807162.aspx) cmdlet to install the **xPSDesiredStateConfiguration** module.</span></span> <span data-ttu-id="14417-118">**Poznámka:**: **instalace modulu** je součástí **PowerShellGet** modul, který je součástí prostředí PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="14417-118">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="14417-119">Si můžete stáhnout **PowerShellGet** modul pro prostředí PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="14417-119">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span> 
1. <span data-ttu-id="14417-120">Získání certifikátu SSL pro vyžádání obsahu DSC server od důvěryhodné certifikační autority, buď v rámci vaší organizace nebo z veřejné autority.</span><span class="sxs-lookup"><span data-stu-id="14417-120">Get an SSL certificate for the DSC Pull server from a trusted Certificate Authority, either within your organization or a public authority.</span></span> <span data-ttu-id="14417-121">Certifikát obdržený od autority je obvykle ve formátu PFX.</span><span class="sxs-lookup"><span data-stu-id="14417-121">The certificate received from the authority is usually in the PFX format.</span></span> <span data-ttu-id="14417-122">Nainstalujte certifikát na uzlu, který se stane DSC vyžádání serveru ve výchozím umístění, které by se měly CERT: \LocalMachine\My.</span><span class="sxs-lookup"><span data-stu-id="14417-122">Install the certificate on the node that will become the DSC Pull server in the default location which should be CERT:\LocalMachine\My.</span></span> <span data-ttu-id="14417-123">Poznamenejte si kryptografický otisk certifikátu.</span><span class="sxs-lookup"><span data-stu-id="14417-123">Make a note of the certificate thumbprint.</span></span>
1. <span data-ttu-id="14417-124">Vyberte identifikátor GUID, který má být použit jako registrační klíč.</span><span class="sxs-lookup"><span data-stu-id="14417-124">Select a GUID to be used as the Registration Key.</span></span> <span data-ttu-id="14417-125">Generovat jednu pomocí prostředí PowerShell zadejte následující PS řádku a stiskněte klávesu enter: '``` [guid]::newGuid()```'nebo'```New-Guid```'.</span><span class="sxs-lookup"><span data-stu-id="14417-125">To generate one using PowerShell enter the following at the PS prompt and press enter: '``` [guid]::newGuid()```' or '```New-Guid```'.</span></span> <span data-ttu-id="14417-126">Tento klíč se použije klient uzly jako sdílený klíč k ověření během registrace.</span><span class="sxs-lookup"><span data-stu-id="14417-126">This key will be used by client nodes as a shared key to authenticate during registration.</span></span> <span data-ttu-id="14417-127">Další informace najdete v části registrační klíč níže.</span><span class="sxs-lookup"><span data-stu-id="14417-127">For more information see the Registration Key section below.</span></span>
1. <span data-ttu-id="14417-128">V integrovaném Skriptovacím prostředí PowerShell, spusťte (F5) následující konfigurační skript (zahrnutý ve složce příklad **xPSDesiredStateConfiguration** modulu jako Sample_xDscWebService.ps1).</span><span class="sxs-lookup"><span data-stu-id="14417-128">In the PowerShell ISE, start (F5) the following configuration script (included in the Example folder of the  **xPSDesiredStateConfiguration** module as Sample_xDscWebService.ps1).</span></span> <span data-ttu-id="14417-129">Tento skript nastaví server vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="14417-129">This script sets up the pull server.</span></span>
  
    ```powershell
    configuration Sample_xDscPullServer
    { 
        param  
        ( 
                [string[]]$NodeName = 'localhost', 

                [ValidateNotNullOrEmpty()] 
                [string] $certificateThumbPrint,

                [Parameter(Mandatory)]
                [ValidateNotNullOrEmpty()]
                [string] $RegistrationKey 
         ) 
         
         Import-DSCResource -ModuleName xPSDesiredStateConfiguration
         Import-DSCResource –ModuleName PSDesiredStateConfiguration

         Node $NodeName 
         { 
             WindowsFeature DSCServiceFeature 
             { 
                 Ensure = 'Present'
                 Name   = 'DSC-Service'             
             } 

             xDscWebService PSDSCPullServer 
             { 
                 Ensure                   = 'Present' 
                 EndpointName             = 'PSDSCPullServer' 
                 Port                     = 8080 
                 PhysicalPath             = "$env:SystemDrive\inetpub\PSDSCPullServer" 
                 CertificateThumbPrint    = $certificateThumbPrint          
                 ModulePath               = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules" 
                 ConfigurationPath        = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration" 
                 State                    = 'Started'
                 DependsOn                = '[WindowsFeature]DSCServiceFeature'     
                 UseSecurityBestPractices = $false
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

1. <span data-ttu-id="14417-130">Spustit v konfiguraci předávání kryptografický otisk certifikátu SSL, jako **certificateThumbPrint** parametr a identifikátor GUID registrační klíč jako **RegistrationKey** parametr:</span><span class="sxs-lookup"><span data-stu-id="14417-130">Run the configuration, passing the thumbprint of the SSL certificate as the **certificateThumbPrint** parameter and a GUID registration key as the **RegistrationKey** parameter:</span></span>

    ```powershell
    # To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store 
    # and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
    dir Cert:\LocalMachine\my

    # Then include this thumbprint when running the configuration
    Sample_xDSCPullServer -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

    # Run the compiled configuration to make the target node a DSC Pull Server
    Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
    ```

## <a name="registration-key"></a><span data-ttu-id="14417-131">Registrační klíč</span><span class="sxs-lookup"><span data-stu-id="14417-131">Registration Key</span></span>
<span data-ttu-id="14417-132">Povolit klientské uzly registraci se serverem a používají názvy konfigurace místo ID konfigurace, registrační klíč, který byl vytvořen výše konfigurace je uložen v souboru s názvem `RegistrationKeys.txt` v `C:\Program Files\WindowsPowerShell\DscService`.</span><span class="sxs-lookup"><span data-stu-id="14417-132">To allow client nodes to register with the server so that they can use configuration names instead of a configuration ID, a registration key which was created by the above configuration is saved in a file named `RegistrationKeys.txt` in `C:\Program Files\WindowsPowerShell\DscService`.</span></span> <span data-ttu-id="14417-133">Registrační klíč funguje jako sdílený tajný klíč používá při počáteční registraci klienta se serverem pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="14417-133">The registration key functions as a shared secret used during the initial registration by the client with the pull server.</span></span> <span data-ttu-id="14417-134">Klient vygeneruje certifikát podepsaný svým držitelem, který slouží k jednoznačné ověření na serveru vyžádané replikace po úspěšném dokončení registrace se.</span><span class="sxs-lookup"><span data-stu-id="14417-134">The client will generate a self-signed certificate which is used to uniquely authenticate to the pull server once registration is successfully completed.</span></span> <span data-ttu-id="14417-135">Kryptografický otisk tohoto certifikátu je uložený místně a přidružené k adrese URL serveru pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="14417-135">The thumbprint of this certificate is stored locally and associated with the URL of the pull server.</span></span>
> <span data-ttu-id="14417-136">**Poznámka:**: registrace klíče nejsou podporovány v prostředí PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="14417-136">**Note**: Registration keys are not supported in PowerShell 4.0.</span></span> 

<span data-ttu-id="14417-137">Chcete-li nakonfigurovat uzel k ověření serveru vyžádané replikace registrace klíč musí být v metakonfiguraci pro cílový uzel, který bude registrace k tomuto serveru pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="14417-137">In order to configure a node to authenticate with the pull server the registration key needs to be in the metaconfiguration for any target node that will be registering with this pull server.</span></span> <span data-ttu-id="14417-138">Všimněte si, že **RegistrationKey** v metakonfiguraci níže se odebere po úspěšně zaregistrovala cílový počítač, a hodnota '140a952b-b9d6-406b-b416-e0f759c9c0e4' se musí shodovat s hodnotou uloženou v RegistrationKeys.txt soubor na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="14417-138">Note that the **RegistrationKey** in the metaconfiguration below is removed after the target machine has successfully registered, and that the value '140a952b-b9d6-406b-b416-e0f759c9c0e4' must match the value stored in the RegistrationKeys.txt file on the pull server.</span></span> <span data-ttu-id="14417-139">Vždy zacházet s hodnotou klíče registrace bezpečně, protože vědomí umožňuje, aby všechny cílové počítače k registraci se serverem pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="14417-139">Always treat the registration key value securely, because knowing it allows any target machine to register with the pull server.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode          = 'Pull'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded   = $true
        }
        
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey    = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('ClientConfig')
        }   
        
        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
        }
    }
}

PullClientConfigID -OutputPath c:\Configs\TargetNodes
```
> <span data-ttu-id="14417-140">**Poznámka:**: **ReportServerWeb** části umožňuje data k odeslání na server vyžádané replikace pro vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="14417-140">**Note**: The **ReportServerWeb** section allows reporting data to be sent to the pull server.</span></span> 

<span data-ttu-id="14417-141">Nedostatek **ConfigurationID** vlastnost v souboru metakonfiguraci implicitně znamená serveru vyžádané replikace se nepodporuje verze V2 protokol server vyžádané replikace, a proto je požadována počáteční registrace.</span><span class="sxs-lookup"><span data-stu-id="14417-141">The lack of the **ConfigurationID** property in the metaconfiguration file implicitly means that pull server is supporting the V2 version of the pull server protocol so an initial registration is required.</span></span> <span data-ttu-id="14417-142">Naopak přítomnosti **ConfigurationID** znamená, že se používá protokol server vyžádané replikace verze V1 a neexistuje žádné zpracování registrace.</span><span class="sxs-lookup"><span data-stu-id="14417-142">Conversely, the presence of a **ConfigurationID** means that the V1 version of the pull server protocol is used and there is no registration processing.</span></span>

><span data-ttu-id="14417-143">**Poznámka:**: V PUSH scénáři chyby existuje v aktuální uvolňování, díky které je potřeba definovat ConfigurationID vlastnost v souboru metakonfiguraci pro uzly, které nikdy zaregistrovali načítacího serveru.</span><span class="sxs-lookup"><span data-stu-id="14417-143">**Note**: In a PUSH scenario, a bug exists in the current relase that makes it necessary to define a ConfigurationID property in the metaconfiguration file for nodes that have never registered with a pull server.</span></span> <span data-ttu-id="14417-144">Tato akce vynutí protokol serveru vyžádané replikace V1 a vyhnout zprávy o selhání registrace.</span><span class="sxs-lookup"><span data-stu-id="14417-144">This will force the V1 Pull Server protocol and avoid registration failure messages.</span></span>

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="14417-145">Umístění konfigurace a prostředky</span><span class="sxs-lookup"><span data-stu-id="14417-145">Placing configurations and resources</span></span>

<span data-ttu-id="14417-146">Po vyžádání obsahu server dokončení instalačního programu, složky, které jsou definované **ConfigurationPath** a **ModulePath** vlastnosti v konfiguraci serveru vyžádané replikace jsou, kam umístíte modulů a konfigurací které budou k dispozici pro cílové uzly načítat.</span><span class="sxs-lookup"><span data-stu-id="14417-146">After the pull server setup completes, the folders defined by the **ConfigurationPath** and **ModulePath** properties in the pull server configuration are where you will place modules and configurations that will be available for target nodes to pull.</span></span> <span data-ttu-id="14417-147">Tyto soubory musí být v konkrétním formátu v pořadí pro vyžádání obsahu server správně zpracovat.</span><span class="sxs-lookup"><span data-stu-id="14417-147">These files need to be in a specific format in order for the pull server to correctly process them.</span></span> 

### <a name="dsc-resource-module-package-format"></a><span data-ttu-id="14417-148">Formát balíčku modulu prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="14417-148">DSC resource module package format</span></span>

<span data-ttu-id="14417-149">Každý modul prostředků musí být ZIP a s názvem podle vzoru následující `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="14417-149">Each resource module needs to be zipped and named according the following pattern `{Module Name}_{Module Version}.zip`.</span></span> <span data-ttu-id="14417-150">Například modul s názvem xWebAdminstration verzí modulu 3.1.2.0 by se jmenovala 'xWebAdministration_3.2.1.0.zip'.</span><span class="sxs-lookup"><span data-stu-id="14417-150">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span> <span data-ttu-id="14417-151">Každá verze nástroje modul musí být obsažena v souboru zip jeden.</span><span class="sxs-lookup"><span data-stu-id="14417-151">Each version of a module must be contained in a single zip file.</span></span> <span data-ttu-id="14417-152">Vzhledem k tomu, že existuje jenom jedna verze nástroje prostředků do každého souboru zip modulu formát přidali v WMF 5.0 s není dostupná podpora pro více verze modulu v jednom adresáři.</span><span class="sxs-lookup"><span data-stu-id="14417-152">Since there is only a single version of a resource in each zip file the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span> <span data-ttu-id="14417-153">To znamená, že před zabalení moduly prostředků DSC pro použití s načítacího serveru budete muset provést změnu malá strukturu adresáře.</span><span class="sxs-lookup"><span data-stu-id="14417-153">This means that before packaging up DSC resource modules for use with pull server you will need to make a small change to the directory structure.</span></span> <span data-ttu-id="14417-154">Výchozí formát modulů obsahující prostředek DSC v WMF 5.0 je ' {složku modulu}\{verze modulu} \DscResources\{Složka prostředků DSC}\'.</span><span class="sxs-lookup"><span data-stu-id="14417-154">The default format of modules containing DSC resource in WMF 5.0 is '{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\'.</span></span> <span data-ttu-id="14417-155">Před balení pro vyžádání obsahu server jednoduše odeberte **{verze modulu}** složku, cesta k přestane ' {složku modulu} \DscResources\{Složka prostředků DSC}\'.</span><span class="sxs-lookup"><span data-stu-id="14417-155">Before packaging up for the pull server simply remove the **{Module version}** folder so the path becomes '{Module Folder}\DscResources\{DSC Resource Folder}\'.</span></span> <span data-ttu-id="14417-156">Díky této změně zip složce, jak je popsáno výše a nastavovat tyto soubory zip v **ModulePath** složky.</span><span class="sxs-lookup"><span data-stu-id="14417-156">With this change, zip the folder as described above and place these zip files in the **ModulePath** folder.</span></span>

<span data-ttu-id="14417-157">Použití `new-dscchecksum {module zip file}` vytvořte soubor kontrolního součtu pro modul nově přidaná.</span><span class="sxs-lookup"><span data-stu-id="14417-157">Use `new-dscchecksum {module zip file}` to create a checksum file for the newly-added module.</span></span>

### <a name="configuration-mof-format"></a><span data-ttu-id="14417-158">Formát MOF konfigurace</span><span class="sxs-lookup"><span data-stu-id="14417-158">Configuration MOF format</span></span> 
<span data-ttu-id="14417-159">Konfigurační soubor MOF musí být spárována s soubor kontrolního součtu, takže LCM na cílový uzel můžete konfiguraci ověřit.</span><span class="sxs-lookup"><span data-stu-id="14417-159">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span> <span data-ttu-id="14417-160">Chcete-li vytvořit kontrolní součet, zavolejte [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="14417-160">To create a checksum, call the [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) cmdlet.</span></span> <span data-ttu-id="14417-161">Rutina trvá **cesta** parametr, který určuje složku, kde se nachází v konfiguraci MOF.</span><span class="sxs-lookup"><span data-stu-id="14417-161">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span> <span data-ttu-id="14417-162">Rutina vytvoří kontrolní součet souboru s názvem `ConfigurationMOFName.mof.checksum`, kde `ConfigurationMOFName` je název konfiguračního souboru mof.</span><span class="sxs-lookup"><span data-stu-id="14417-162">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span> <span data-ttu-id="14417-163">Pokud existují minimálně jedna konfigurace soubory MOF do určené složky, vytvoří se pro každou konfiguraci ve složce kontrolní součet.</span><span class="sxs-lookup"><span data-stu-id="14417-163">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span> <span data-ttu-id="14417-164">Umístěte soubory MOF a jejich přidružené kontrolního součtu souborů v **ConfigurationPath** složky.</span><span class="sxs-lookup"><span data-stu-id="14417-164">Place the MOF files and their associated checksum files in the the **ConfigurationPath** folder.</span></span>

><span data-ttu-id="14417-165">**Poznámka:**: Pokud změníte konfigurační soubor MOF žádným způsobem, musíte také znovu vytvořit soubor kontrolního součtu.</span><span class="sxs-lookup"><span data-stu-id="14417-165">**Note**: If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

## <a name="tooling"></a><span data-ttu-id="14417-166">Nástrojů</span><span class="sxs-lookup"><span data-stu-id="14417-166">Tooling</span></span>
<span data-ttu-id="14417-167">Chcete-li nastavení tvoří, ověření a Správa serveru vyžádané replikace jednodušší, tyto nástroje jsou zahrnuty jako příklady v nejnovější verzi modulu xPSDesiredStateConfiguration:</span><span class="sxs-lookup"><span data-stu-id="14417-167">In order to make setting up, validating and managing the pull server easier, the following tools are included as examples in the latest version of the xPSDesiredStateConfiguration module:</span></span>
1. <span data-ttu-id="14417-168">Modul, který vám pomůže s balení moduly prostředků DSC a konfigurační soubory pro použití na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="14417-168">A module that will help with packaging DSC resource modules and configuration files for use on the pull server.</span></span> <span data-ttu-id="14417-169">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span><span class="sxs-lookup"><span data-stu-id="14417-169">[PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1).</span></span> <span data-ttu-id="14417-170">Následující příklady:</span><span class="sxs-lookup"><span data-stu-id="14417-170">Examples below:</span></span>

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @("xWebAdministration", "xPhp") 
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList 

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. <span data-ttu-id="14417-171">Skript, který ověří načítacího serveru správně nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="14417-171">A script that validates the pull server is configured correctly.</span></span> <span data-ttu-id="14417-172">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span><span class="sxs-lookup"><span data-stu-id="14417-172">[PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).</span></span>


## <a name="pull-client-configuration"></a><span data-ttu-id="14417-173">Konfigurace klienta pro vyžádání obsahu</span><span class="sxs-lookup"><span data-stu-id="14417-173">Pull client configuration</span></span> 
<span data-ttu-id="14417-174">Následující témata popisují nastavení klientů pro vyžádání obsahu podrobně:</span><span class="sxs-lookup"><span data-stu-id="14417-174">The following topics describe setting up pull clients in detail:</span></span>

* [<span data-ttu-id="14417-175">Nastavení klienta vyžádání DSC pomocí ID konfigurace</span><span class="sxs-lookup"><span data-stu-id="14417-175">Setting up a DSC pull client using a configuration ID</span></span>](pullClientConfigID.md)
* [<span data-ttu-id="14417-176">Nastavení klienta vyžádání DSC pomocí názvy konfigurace</span><span class="sxs-lookup"><span data-stu-id="14417-176">Setting up a DSC pull client using configuration names</span></span>](pullClientConfigNames.md)
* [<span data-ttu-id="14417-177">Částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="14417-177">Partial configurations</span></span>](partialConfigs.md)


## <a name="see-also"></a><span data-ttu-id="14417-178">Viz taky</span><span class="sxs-lookup"><span data-stu-id="14417-178">See also</span></span>
* [<span data-ttu-id="14417-179">Přehled stavu konfigurace požadovaného prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="14417-179">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
* [<span data-ttu-id="14417-180">Přijetí konfigurace</span><span class="sxs-lookup"><span data-stu-id="14417-180">Enacting configurations</span></span>](enactingConfigurations.md)
* [<span data-ttu-id="14417-181">Použití serveru sestav DSC</span><span class="sxs-lookup"><span data-stu-id="14417-181">Using a DSC report server</span></span>](reportServer.md)

