---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Nastavení serveru DSC SMB vyžádání obsahu"
ms.openlocfilehash: ff3faeb1952e6116cf97b1aaf8f125d8931dd35e
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="setting-up-a-dsc-smb-pull-server"></a><span data-ttu-id="ea370-103">Nastavení serveru DSC SMB vyžádání obsahu</span><span class="sxs-lookup"><span data-stu-id="ea370-103">Setting up a DSC SMB pull server</span></span>

><span data-ttu-id="ea370-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ea370-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="ea370-105">DSC [SMB](https://technet.microsoft.com/library/hh831795.aspx) vyžádání obsahu server je počítač hostování sdílených složek SMB, které zpřístupnit DSC konfiguračních souborů a prostředků DSC pro cílové uzly při uzly, zeptejte se pro ně.</span><span class="sxs-lookup"><span data-stu-id="ea370-105">A DSC [SMB](https://technet.microsoft.com/library/hh831795.aspx) pull server is a computer hosting SMB file shares that make DSC configuration files and DSC resources available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="ea370-106">Chcete-li použít vyžádání serveru SMB pro DSC, budete muset:</span><span class="sxs-lookup"><span data-stu-id="ea370-106">To use an SMB pull server for DSC, you have to:</span></span>
- <span data-ttu-id="ea370-107">Nastavení sdílené složky SMB na serveru se systémem prostředí PowerShell 4.0 nebo vyšší</span><span class="sxs-lookup"><span data-stu-id="ea370-107">Set up an SMB file share on a server running PowerShell 4.0 or higher</span></span>
- <span data-ttu-id="ea370-108">Konfigurace klienta se systémem prostředí PowerShell 4.0 nebo vyšší načítat z této sdílené složce protokolu SMB</span><span class="sxs-lookup"><span data-stu-id="ea370-108">Configure a client running PowerShell 4.0 or higher to pull from that SMB share</span></span>

## <a name="using-the-xsmbshare-resource-to-create-an-smb-file-share"></a><span data-ttu-id="ea370-109">Použití xSmbShare prostředků k vytvoření sdílené složky SMB</span><span class="sxs-lookup"><span data-stu-id="ea370-109">Using the xSmbShare resource to create an SMB file share</span></span>

<span data-ttu-id="ea370-110">Existuje několik způsobů, jak nastavit sdílenou složku SMB, ale podíváme, jak můžete to provést pomocí DSC.</span><span class="sxs-lookup"><span data-stu-id="ea370-110">There are a number of ways to set up an SMB file share, but let's look at how you can do this by using DSC.</span></span>

### <a name="install-the-xsmbshare-resource"></a><span data-ttu-id="ea370-111">Nainstalujte xSmbShare prostředků</span><span class="sxs-lookup"><span data-stu-id="ea370-111">Install the xSmbShare resource</span></span>

<span data-ttu-id="ea370-112">Volání [instalace modulu](https://technet.microsoft.com/library/dn807162.aspx) k instalaci **xSmbShare** modulu.</span><span class="sxs-lookup"><span data-stu-id="ea370-112">Call the [Install-Module](https://technet.microsoft.com/library/dn807162.aspx) cmdlet to install the **xSmbShare** module.</span></span>
><span data-ttu-id="ea370-113">**Poznámka:**: **instalace modulu** je součástí **PowerShellGet** modul, který je součástí prostředí PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="ea370-113">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="ea370-114">Si můžete stáhnout **PowerShellGet** modul pro prostředí PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="ea370-114">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span> <span data-ttu-id="ea370-115">**XSmbShare** obsahuje prostředek DSC **xSmbShare**, který slouží k vytvoření sdílené složky SMB.</span><span class="sxs-lookup"><span data-stu-id="ea370-115">The **xSmbShare** contains the DSC resource **xSmbShare**, which can be used to create an SMB file share.</span></span>

### <a name="create-the-directory-and-file-share"></a><span data-ttu-id="ea370-116">Vytvoření sdílené složky pro adresáře a souboru</span><span class="sxs-lookup"><span data-stu-id="ea370-116">Create the directory and file share</span></span>

<span data-ttu-id="ea370-117">Používá následující konfigurace [soubor](fileResource.md) prostředek pro vytvoření adresáře pro sdílenou složku a **xSmbShare** prostředků nastavit sdílenou složku SMB:</span><span class="sxs-lookup"><span data-stu-id="ea370-117">The following configuration uses the [File](fileResource.md) resource to create the directory for the share and the **xSmbShare** resource to set up the SMB share:</span></span>

```powershell
Configuration SmbShare {

Import-DscResource -ModuleName PSDesiredStateConfiguration
Import-DscResource -ModuleName xSmbShare
 
    Node localhost {
 
        File CreateFolder {
 
            DestinationPath = 'C:\DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'
 
        }
 
        xSMBShare CreateShare {
 
            Name = 'DscSmbShare'
            Path = 'C:\DscSmbShare'
            FullAccess = 'admininstrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'
 
        }
        
    }
 
}
```

<span data-ttu-id="ea370-118">Konfigurace vytvoří adresář `C:\DscSmbShare` Pokud tomu tak není již existuje a pak použije tento adresář jako sdílenou složku SMB.</span><span class="sxs-lookup"><span data-stu-id="ea370-118">The configuration creates the directory `C:\DscSmbShare` if it doesn't already exists, and then uses that directory as an SMB file share.</span></span> <span data-ttu-id="ea370-119">**FullAccess** má být poskytnut k nějakému účtu, který potřebuje zapisovat nebo odstranit ze sdílené složky a **oprávnění ke čtení** musí být poskytnut do žádného uzlu klienta, které získají ze sdílené složky (totiž konfigurace nebo prostředky DSC DSC jako systémový účet ve výchozím nastavení spustí, takže přímo počítač musí mít přístup ke sdílené složce).</span><span class="sxs-lookup"><span data-stu-id="ea370-119">**FullAccess** should be given to any account that needs to write to or delete from the file share, and **ReadAccess** must be given to any client nodes that get configurations and/or DSC resources from the share ( this is because DSC runs as the system account by default, so the computer itself has to have access to the share).</span></span>


### <a name="give-file-system-access-to-the-pull-client"></a><span data-ttu-id="ea370-120">Poskytnout přístupu k systému souborů k vyžádání klienta</span><span class="sxs-lookup"><span data-stu-id="ea370-120">Give file system access to the pull client</span></span>

<span data-ttu-id="ea370-121">Poskytnutí **oprávnění ke čtení** klientovi uzel umožňuje tento uzel k přístupu ke sdílené složce protokolu SMB, ale aby se soubory nebo složky, jež se sdílet.</span><span class="sxs-lookup"><span data-stu-id="ea370-121">Giving **ReadAccess** to a client node allows that node to access the SMB share, but not to files or folders within that share.</span></span> <span data-ttu-id="ea370-122">Je nutné explicitně udělit klienta uzly přístup k protokolu SMB sdílenou složku a podsložky.</span><span class="sxs-lookup"><span data-stu-id="ea370-122">You have to explicitly grant client nodes access to the SMB share folder and sub-folders.</span></span> <span data-ttu-id="ea370-123">Jsme to provést pomocí DSC přidáním pomocí **cNtfsPermissionEntry** prostředku, který je součástí [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) modulu.</span><span class="sxs-lookup"><span data-stu-id="ea370-123">We can do this with DSC by adding using the **cNtfsPermissionEntry** resource, which is contained in the [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) module.</span></span> <span data-ttu-id="ea370-124">Přidá následující konfigurace **cNtfsPermissionEntry** blok, který uděluje přístup ReadAndExecute klient pro vyžádání obsahu:</span><span class="sxs-lookup"><span data-stu-id="ea370-124">The following configuration adds a **cNtfsPermissionEntry** block that grants ReadAndExecute access to the pull client:</span></span>

```powershell
Configuration DSCSMB {

Import-DscResource -ModuleName PSDesiredStateConfiguration
Import-DscResource -ModuleName xSmbShare
Import-DscResource -ModuleName cNtfsAccessControl
 
    Node localhost {
 
        File CreateFolder {
 
            DestinationPath = 'DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'
 
        }
 
        xSMBShare CreateShare {
 
            Name = 'DscSmbShare'
            Path = 'DscSmbShare'
            FullAccess = 'administrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'
 
        }

        cNtfsPermissionEntry PermissionSet1 {
            
        Ensure = 'Present'
        Path = 'C:\DSCSMB'
        Principal = 'myDomain\Contoso-Server$'
        AccessControlInformation = @(
            cNtfsAccessControlInformation
            {
                AccessControlType = 'Allow'
                FileSystemRights = 'ReadAndExecute'
                Inheritance = 'ThisFolderSubfoldersAndFiles'
                NoPropagateInherit = $false
            }
        )
        DependsOn = '[File]CreateFolder'
        
        }
 
        
    }
 
}
```

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="ea370-125">Umístění konfigurace a prostředky</span><span class="sxs-lookup"><span data-stu-id="ea370-125">Placing configurations and resources</span></span>

<span data-ttu-id="ea370-126">Uložte všechny soubory MOF konfigurace nebo prostředky DSC, které chcete uzly klienta stáhnout sdílenou složku SMB.</span><span class="sxs-lookup"><span data-stu-id="ea370-126">Save any configuration MOF files and/or DSC resources that you want client nodes to pull in the SMB share folder.</span></span>

<span data-ttu-id="ea370-127">Musí mít název konfiguračního souboru MOF _ConfigurationID_MOF, kde _ConfigurationID_ je hodnota **ConfigurationID** vlastnost LCM cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="ea370-127">Any configuration MOF file must be named _ConfigurationID_.mof, where _ConfigurationID_ is the value of the **ConfigurationID** property of the target node's LCM.</span></span> <span data-ttu-id="ea370-128">Další informace o nastavení klientů pro vyžádání obsahu najdete v tématu [nastavení vyžadování klienta pomocí ID konfigurace](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="ea370-128">For more information about setting up pull clients, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

><span data-ttu-id="ea370-129">**Poznámka:** ID konfigurace musíte použít, pokud používáte vyžádání serveru SMB.</span><span class="sxs-lookup"><span data-stu-id="ea370-129">**Note:** You must use configuration IDs if you are using an SMB pull server.</span></span> <span data-ttu-id="ea370-130">Názvy konfigurace nejsou podporovány pro protokol SMB.</span><span class="sxs-lookup"><span data-stu-id="ea370-130">Configuration names are not supported for SMB.</span></span>

<span data-ttu-id="ea370-131">Každý modul prostředků musí být ZIP a s názvem podle následující vzor `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="ea370-131">Each resource module needs to be zipped and named according the the following pattern `{Module Name}_{Module Version}.zip`.</span></span> <span data-ttu-id="ea370-132">Například modul s názvem xWebAdminstration verzí modulu 3.1.2.0 by se jmenovala 'xWebAdministration_3.2.1.0.zip'.</span><span class="sxs-lookup"><span data-stu-id="ea370-132">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span> <span data-ttu-id="ea370-133">Každá verze nástroje modul musí být obsažena v souboru zip jeden.</span><span class="sxs-lookup"><span data-stu-id="ea370-133">Each version of a module must be contained in a single zip file.</span></span> <span data-ttu-id="ea370-134">Vzhledem k tomu, že existuje jenom jedna verze nástroje prostředků do každého souboru zip modulu formát přidali v WMF 5.0 s není dostupná podpora pro více verze modulu v jednom adresáři.</span><span class="sxs-lookup"><span data-stu-id="ea370-134">Since there is only a single version of a resource in each zip file the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span> <span data-ttu-id="ea370-135">To znamená, že před balení až moduly prostředků DSC pro použití s načítacího serveru je potřeba provést změnu malá strukturu adresáře.</span><span class="sxs-lookup"><span data-stu-id="ea370-135">This means that before packaging up DSC resource modules for use with pull server you need to make a small change to the directory structure.</span></span> <span data-ttu-id="ea370-136">Výchozí formát modulů obsahující prostředek DSC v WMF 5.0 je ' {složku modulu}\{verze modulu} \DscResources\{Složka prostředků DSC}\'.</span><span class="sxs-lookup"><span data-stu-id="ea370-136">The default format of modules containing DSC resource in WMF 5.0 is '{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\'.</span></span> <span data-ttu-id="ea370-137">Před balení pro vyžádání obsahu server jednoduše odeberte **{verze modulu}** složku, cesta k přestane ' {složku modulu} \DscResources\{Složka prostředků DSC}\'.</span><span class="sxs-lookup"><span data-stu-id="ea370-137">Before packaging up for the pull server simply remove the **{Module version}** folder so the path becomes '{Module Folder}\DscResources\{DSC Resource Folder}\'.</span></span> <span data-ttu-id="ea370-138">Díky této změně složky zip, jak je popsáno výše a umístěte tyto soubory zip v sdílenou složku SMB.</span><span class="sxs-lookup"><span data-stu-id="ea370-138">With this change, zip the folder as described above and place these zip files in the SMB share folder.</span></span> 

## <a name="creating-the-mof-checksum"></a><span data-ttu-id="ea370-139">Vytváření kontrolního součtu MOF</span><span class="sxs-lookup"><span data-stu-id="ea370-139">Creating the MOF checksum</span></span>
<span data-ttu-id="ea370-140">Konfigurační soubor MOF musí být spárována s soubor kontrolního součtu, takže LCM na cílový uzel můžete konfiguraci ověřit.</span><span class="sxs-lookup"><span data-stu-id="ea370-140">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span> <span data-ttu-id="ea370-141">Chcete-li vytvořit kontrolní součet, zavolejte [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="ea370-141">To create a checksum, call the [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) cmdlet.</span></span> <span data-ttu-id="ea370-142">Rutina trvá **cesta** parametr, který určuje složku, kde se nachází v konfiguraci MOF.</span><span class="sxs-lookup"><span data-stu-id="ea370-142">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span> <span data-ttu-id="ea370-143">Rutina vytvoří kontrolní součet souboru s názvem `ConfigurationMOFName.mof.checksum`, kde `ConfigurationMOFName` je název konfiguračního souboru mof.</span><span class="sxs-lookup"><span data-stu-id="ea370-143">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span> <span data-ttu-id="ea370-144">Pokud existují minimálně jedna konfigurace soubory MOF do určené složky, vytvoří se pro každou konfiguraci ve složce kontrolní součet.</span><span class="sxs-lookup"><span data-stu-id="ea370-144">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>

<span data-ttu-id="ea370-145">Soubor kontrolního součtu musí být ve stejném adresáři jako konfiguračního souboru MOF (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` ve výchozím nastavení), a mít stejný název `.checksum` příponou.</span><span class="sxs-lookup"><span data-stu-id="ea370-145">The checksum file must be present in the same directory as the configuration MOF file (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` by default), and have the same name with the `.checksum` extension appended.</span></span>

><span data-ttu-id="ea370-146">**Poznámka:**: Pokud změníte konfigurační soubor MOF žádným způsobem, musíte také znovu vytvořit soubor kontrolního součtu.</span><span class="sxs-lookup"><span data-stu-id="ea370-146">**Note**: If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

## <a name="setting-up-a-pull-client-for-smb"></a><span data-ttu-id="ea370-147">Nastavení klienta vyžádání obsahu pro protokol SMB</span><span class="sxs-lookup"><span data-stu-id="ea370-147">Setting up a pull client for SMB</span></span>

<span data-ttu-id="ea370-148">Chcete-li nastavení klienta, který vrátí konfigurace nebo prostředky ze složky protokolu SMB, je nakonfigurovat klienta místní Configuration Manager (LCM) s **ConfigurationRepositoryShare** a **ResourceRepositoryShare** bloků, které zadejte sdílenou složku, ze kterého mají být konfigurací a prostředků DSC pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="ea370-148">To set up a client that pulls configurations and/or resources from an SMB share, you configure the client's Local Configuration Manager (LCM) with **ConfigurationRepositoryShare** and **ResourceRepositoryShare** blocks that specify the share from which to pull configurations and DSC resources.</span></span>

<span data-ttu-id="ea370-149">Další informace o konfiguraci LCM najdete v tématu [nastavení vyžadování klienta pomocí ID konfigurace](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="ea370-149">For more information about configuring the LCM, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

><span data-ttu-id="ea370-150">**Poznámka:** pro jednoduchost, v tomto příkladu **PSDscAllowPlainTextPassword** umožňující předávání heslo jako prostý text k **přihlašovacích údajů** parametr.</span><span class="sxs-lookup"><span data-stu-id="ea370-150">**Note:** For simplicity, this example uses the **PSDscAllowPlainTextPassword** to allow passing a plaintext password to the **Credential** parameter.</span></span> <span data-ttu-id="ea370-151">Informace o předávání pověření bezpečněji najdete v tématu [možností pověření v konfigurační Data](configDataCredentials.md).</span><span class="sxs-lookup"><span data-stu-id="ea370-151">For information about passing credentials more securely, see [Credentials Options in Configuration Data](configDataCredentials.md).</span></span>

><span data-ttu-id="ea370-152">**Poznámka:** je nutné zadat **ConfigurationID** v **nastavení** blok metakonfiguraci pro vyžádání obsahu serveru SMB, i když jsou pouze stahování prostředky.</span><span class="sxs-lookup"><span data-stu-id="ea370-152">**Note:** You must specify a **ConfigurationID** in the **Settings** block of a metaconfiguration for an SMB pull server, even if you are only pulling resources.</span></span>

```powershell
$secpasswd = ConvertTo-SecureString “Pass1Word” -AsPlainText -Force
$mycreds = New-Object System.Management.Automation.PSCredential (“TestUser”, $secpasswd)

[DSCLocalConfigurationManager()]
configuration SmbCredTest
{
    Node $AllNodes.NodeName
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
            ConfigurationID    = '16db7357-9083-4806-a80c-ebbaf4acd6c1'
        }
         
         ConfigurationRepositoryShare SmbConfigShare      
        {
            SourcePath = '\\WIN-E0TRU6U11B1\DscSmbShare'
            Credential = $mycreds
        }

        ResourceRepositoryShare SmbResourceShare
        {
            SourcePath = '\\WIN-E0TRU6U11B1\DscSmbShare'
            Credential = $mycreds
            
        }      
    }
}

$ConfigurationData = @{

    AllNodes = @(

        @{

            #the "*" means "all nodes named in ConfigData" so we don't have to repeat ourselves

            NodeName="localhost"

            PSDscAllowPlainTextPassword = $true

        })

        

}
```

## <a name="acknowledgements"></a><span data-ttu-id="ea370-153">Poděkování</span><span class="sxs-lookup"><span data-stu-id="ea370-153">Acknowledgements</span></span>

<span data-ttu-id="ea370-154">Zvláštní díky následující:</span><span class="sxs-lookup"><span data-stu-id="ea370-154">Special thanks to the following:</span></span>

- <span data-ttu-id="ea370-155">Jan F. Robbins, jejichž příspěvcích na pomocí protokolu SMB pro DSC pomohl informovat obsah v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="ea370-155">Mike F. Robbins, whose posts on using SMB for DSC helped inform the content in this topic.</span></span> <span data-ttu-id="ea370-156">Jeho blogu je na [Karel F Robbins](http://mikefrobbins.com/).</span><span class="sxs-lookup"><span data-stu-id="ea370-156">His blog is at [Mike F Robbins](http://mikefrobbins.com/).</span></span>
- <span data-ttu-id="ea370-157">Serge Nikalaichyk, kdo vytvořené **cNtfsAccessControl** modulu.</span><span class="sxs-lookup"><span data-stu-id="ea370-157">Serge Nikalaichyk, who authored the **cNtfsAccessControl** module.</span></span> <span data-ttu-id="ea370-158">Zdroj pro tento modul je v https://github.com/SNikalaichyk/cNtfsAccessControl.</span><span class="sxs-lookup"><span data-stu-id="ea370-158">The source for this module is at https://github.com/SNikalaichyk/cNtfsAccessControl.</span></span>

## <a name="see-also"></a><span data-ttu-id="ea370-159">Viz taky</span><span class="sxs-lookup"><span data-stu-id="ea370-159">See also</span></span>
- [<span data-ttu-id="ea370-160">Přehled stavu konfigurace požadovaného prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea370-160">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
- [<span data-ttu-id="ea370-161">Přijetí konfigurace</span><span class="sxs-lookup"><span data-stu-id="ea370-161">Enacting configurations</span></span>](enactingConfigurations.md)
- [<span data-ttu-id="ea370-162">Použití konfiguračních identifikátorů k nastavení načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="ea370-162">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)

 
