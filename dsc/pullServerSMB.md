---
ms.date: 04/11/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Nastavení serveru vyžádané replikace SMB pro DSC
ms.openlocfilehash: 1eac6c51aeca3ed573ba8fa27188103436004920
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892861"
---
# <a name="setting-up-a-dsc-smb-pull-server"></a><span data-ttu-id="d44b8-103">Nastavení serveru vyžádané replikace SMB pro DSC</span><span class="sxs-lookup"><span data-stu-id="d44b8-103">Setting up a DSC SMB pull server</span></span>

<span data-ttu-id="d44b8-104">Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="d44b8-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d44b8-105">Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="d44b8-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="d44b8-106">Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="d44b8-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="d44b8-107">DSC [SMB](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831795(v=ws.11)) serveru vyžádané replikace je počítač hostující sdílené složky SMB, které zpřístupnit DSC konfigurační soubory a prostředky DSC cílové uzly při těchto uzlů požádat o nich.</span><span class="sxs-lookup"><span data-stu-id="d44b8-107">A DSC [SMB](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831795(v=ws.11)) pull server is a computer hosting SMB file shares that make DSC configuration files and DSC resources available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="d44b8-108">Chcete-li použít serveru vyžádané replikace SMB pro DSC, budete muset:</span><span class="sxs-lookup"><span data-stu-id="d44b8-108">To use an SMB pull server for DSC, you have to:</span></span>

- <span data-ttu-id="d44b8-109">Nastavení sdílené složky protokolu SMB na serveru se systémem Powershellu 4.0 nebo vyšší</span><span class="sxs-lookup"><span data-stu-id="d44b8-109">Set up an SMB file share on a server running PowerShell 4.0 or higher</span></span>
- <span data-ttu-id="d44b8-110">Konfigurace klienta, spouštění prostředí PowerShell 4.0 nebo vyšší na vyžádání z této sdílené složky SMB</span><span class="sxs-lookup"><span data-stu-id="d44b8-110">Configure a client running PowerShell 4.0 or higher to pull from that SMB share</span></span>

## <a name="using-the-xsmbshare-resource-to-create-an-smb-file-share"></a><span data-ttu-id="d44b8-111">Použití xSmbShare prostředků k vytvoření sdílené složky protokolu SMB</span><span class="sxs-lookup"><span data-stu-id="d44b8-111">Using the xSmbShare resource to create an SMB file share</span></span>

<span data-ttu-id="d44b8-112">Existuje mnoho způsobů, jak nastavit sdílenou složku SMB, ale podívejme se na tom, jak to provést pomocí DSC.</span><span class="sxs-lookup"><span data-stu-id="d44b8-112">There are a number of ways to set up an SMB file share, but let's look at how you can do this by using DSC.</span></span>

### <a name="install-the-xsmbshare-resource"></a><span data-ttu-id="d44b8-113">Nainstalujte xSmbShare prostředků</span><span class="sxs-lookup"><span data-stu-id="d44b8-113">Install the xSmbShare resource</span></span>

<span data-ttu-id="d44b8-114">Volání [Install-Module](/powershell/module/PowershellGet/Install-Module) rutinu instalace **xSmbShare** modulu.</span><span class="sxs-lookup"><span data-stu-id="d44b8-114">Call the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xSmbShare** module.</span></span>

> [!NOTE]
> <span data-ttu-id="d44b8-115">`Install-Module` je součástí **PowerShellGet** modulu, která je obsažena v Powershellu 5.0.</span><span class="sxs-lookup"><span data-stu-id="d44b8-115">`Install-Module` is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="d44b8-116">Můžete stáhnout **PowerShellGet** modulu pro PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="d44b8-116">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>
> <span data-ttu-id="d44b8-117">**XSmbShare** obsahuje prostředek DSC **xSmbShare**, který slouží k vytvoření sdílené složky SMB.</span><span class="sxs-lookup"><span data-stu-id="d44b8-117">The **xSmbShare** contains the DSC resource **xSmbShare**, which can be used to create an SMB file share.</span></span>

### <a name="create-the-directory-and-file-share"></a><span data-ttu-id="d44b8-118">Vytvoření sdílené složky adresáře a souboru</span><span class="sxs-lookup"><span data-stu-id="d44b8-118">Create the directory and file share</span></span>

<span data-ttu-id="d44b8-119">Následující konfigurace se používá [souboru](fileResource.md) prostředek pro vytvoření sdílené složky v adresáři a **xSmbShare** prostředků nastavení sdílené složky SMB:</span><span class="sxs-lookup"><span data-stu-id="d44b8-119">The following configuration uses the [File](fileResource.md) resource to create the directory for the share and the **xSmbShare** resource to set up the SMB share:</span></span>

```powershell
Configuration SmbShare
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Import-DscResource -ModuleName xSmbShare

    Node localhost
    {

        File CreateFolder
        {
            DestinationPath = 'C:\DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'
        }

        xSMBShare CreateShare
        {
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

<span data-ttu-id="d44b8-120">Konfigurace vytvoří adresář `C:\DscSmbShare` Pokud zatím již existuje a použije tento adresář jako sdílené složky protokolu SMB.</span><span class="sxs-lookup"><span data-stu-id="d44b8-120">The configuration creates the directory `C:\DscSmbShare` if it doesn't already exists, and then uses that directory as an SMB file share.</span></span> <span data-ttu-id="d44b8-121">**FullAccess** by měla být věnována libovolný účet, který se musí zapisovat nebo odstranit ze sdílené složky a **oprávnění ke čtení** musí předávat žádné uzly klienta, které si mohli služby konfigurace a prostředky DSC ze sdílené složky (totiž DSC jako systémový účet ve výchozím nastavení spustí, takže přímo počítač musí mít přístup ke sdílené složce).</span><span class="sxs-lookup"><span data-stu-id="d44b8-121">**FullAccess** should be given to any account that needs to write to or delete from the file share, and **ReadAccess** must be given to any client nodes that get configurations and/or DSC resources from the share ( this is because DSC runs as the system account by default, so the computer itself has to have access to the share).</span></span>

### <a name="give-file-system-access-to-the-pull-client"></a><span data-ttu-id="d44b8-122">Poskytnout přístup systému souborů k načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="d44b8-122">Give file system access to the pull client</span></span>

<span data-ttu-id="d44b8-123">Poskytuje **oprávnění ke čtení** klientovi uzel umožňuje přístup ke sdílené složce protokolu SMB, ale ne na soubory nebo složky, které sdílejí tento uzel.</span><span class="sxs-lookup"><span data-stu-id="d44b8-123">Giving **ReadAccess** to a client node allows that node to access the SMB share, but not to files or folders within that share.</span></span> <span data-ttu-id="d44b8-124">Je nutné explicitně udělit klienta uzlům přístup do sdílené složky protokolu SMB a podsložky.</span><span class="sxs-lookup"><span data-stu-id="d44b8-124">You have to explicitly grant client nodes access to the SMB share folder and sub-folders.</span></span> <span data-ttu-id="d44b8-125">Můžeme to udělat pomocí DSC tak, že přidáte pomocí **cNtfsPermissionEntry** prostředek, který je součástí [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) modulu.</span><span class="sxs-lookup"><span data-stu-id="d44b8-125">We can do this with DSC by adding using the **cNtfsPermissionEntry** resource, which is contained in the [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) module.</span></span> <span data-ttu-id="d44b8-126">V následující konfiguraci přidáte **cNtfsPermissionEntry** blok, který uděluje přístup ReadAndExecute načítacího klienta:</span><span class="sxs-lookup"><span data-stu-id="d44b8-126">The following configuration adds a **cNtfsPermissionEntry** block that grants ReadAndExecute access to the pull client:</span></span>

```powershell
Configuration DSCSMB
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Import-DscResource -ModuleName xSmbShare
    Import-DscResource -ModuleName cNtfsAccessControl

    Node localhost
    {

        File CreateFolder
        {
            DestinationPath = 'DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'
        }

        xSMBShare CreateShare
        {
            Name = 'DscSmbShare'
            Path = 'DscSmbShare'
            FullAccess = 'administrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'
        }

        cNtfsPermissionEntry PermissionSet1
        {
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

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="d44b8-127">Uvedení konfigurací a prostředků</span><span class="sxs-lookup"><span data-stu-id="d44b8-127">Placing configurations and resources</span></span>

<span data-ttu-id="d44b8-128">Uložte konfigurační soubory MOF a/nebo prostředky DSC, které mají klienta uzly, aby se načetla sdílenou složku SMB.</span><span class="sxs-lookup"><span data-stu-id="d44b8-128">Save any configuration MOF files and/or DSC resources that you want client nodes to pull in the SMB share folder.</span></span>

<span data-ttu-id="d44b8-129">Musí mít název konfiguračního souboru MOF *ConfigurationID*.mof, kde *ConfigurationID* je hodnota **ConfigurationID** vlastnost LCM cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="d44b8-129">Any configuration MOF file must be named *ConfigurationID*.mof, where *ConfigurationID* is the value of the **ConfigurationID** property of the target node's LCM.</span></span> <span data-ttu-id="d44b8-130">Další informace o nastavení klientů o přijetí změn najdete v tématu [nastavení načítacího klienta použití konfiguračních identifikátorů](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="d44b8-130">For more information about setting up pull clients, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d44b8-131">Pokud používáte serveru vyžádané replikace SMB je nutné použít ID konfigurace.</span><span class="sxs-lookup"><span data-stu-id="d44b8-131">You must use configuration IDs if you are using an SMB pull server.</span></span> <span data-ttu-id="d44b8-132">Názvy konfigurace nejsou podporovány pro protokolu SMB.</span><span class="sxs-lookup"><span data-stu-id="d44b8-132">Configuration names are not supported for SMB.</span></span>

<span data-ttu-id="d44b8-133">Každý modul prostředků musí být metoda ZIP a s názvem podle následující vzor `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="d44b8-133">Each resource module needs to be zipped and named according the the following pattern `{Module Name}_{Module Version}.zip`.</span></span> <span data-ttu-id="d44b8-134">Například modul s názvem xWebAdminstration s verzí modulu 3.1.2.0 by se pojmenoval "xWebAdministration_3.2.1.0.zip".</span><span class="sxs-lookup"><span data-stu-id="d44b8-134">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span> <span data-ttu-id="d44b8-135">Každá verze modulu musí být součástí jedné zip soubor.</span><span class="sxs-lookup"><span data-stu-id="d44b8-135">Each version of a module must be contained in a single zip file.</span></span> <span data-ttu-id="d44b8-136">Vzhledem k tomu, že existuje pouze jedna verze prostředku v každém souboru zip formát modulu přidáno ve WMF 5.0 s více verzí modulu v jednom adresáři není podporované.</span><span class="sxs-lookup"><span data-stu-id="d44b8-136">Since there is only a single version of a resource in each zip file the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span> <span data-ttu-id="d44b8-137">To znamená, že před zabalení moduly prostředků DSC pro použití se serverem o přijetí změn je potřeba proveďte malou změnu do struktury adresářů.</span><span class="sxs-lookup"><span data-stu-id="d44b8-137">This means that before packaging up DSC resource modules for use with pull server you need to make a small change to the directory structure.</span></span> <span data-ttu-id="d44b8-138">Je výchozí formát pro moduly obsahující prostředek DSC ve WMF 5.0 `{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\`.</span><span class="sxs-lookup"><span data-stu-id="d44b8-138">The default format of modules containing DSC resource in WMF 5.0 is `{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\`.</span></span> <span data-ttu-id="d44b8-139">Před balení do serveru vyžádané replikace jednoduše odebrat `{Module version}` složku, cesta bude `{Module Folder}\DscResources\{DSC Resource Folder}\`.</span><span class="sxs-lookup"><span data-stu-id="d44b8-139">Before packaging up for the pull server simply remove the `{Module version}` folder so the path becomes `{Module Folder}\DscResources\{DSC Resource Folder}\`.</span></span> <span data-ttu-id="d44b8-140">Díky této změně složky zip, jak je popsáno výše a umístí tyto souboru zip do sdílené složky SMB.</span><span class="sxs-lookup"><span data-stu-id="d44b8-140">With this change, zip the folder as described above and place these zip files in the SMB share folder.</span></span>

## <a name="creating-the-mof-checksum"></a><span data-ttu-id="d44b8-141">Vytváří se kontrolní součet MOF</span><span class="sxs-lookup"><span data-stu-id="d44b8-141">Creating the MOF checksum</span></span>

<span data-ttu-id="d44b8-142">Konfiguračního souboru MOF musí být párována s typem kontrolního součtu souboru tak, aby LCM na cílový uzel můžete konfiguraci ověřit.</span><span class="sxs-lookup"><span data-stu-id="d44b8-142">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span>
<span data-ttu-id="d44b8-143">Chcete-li vytvořit kontrolní součet, zavolejte [New-DSCCheckSum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum) rutiny.</span><span class="sxs-lookup"><span data-stu-id="d44b8-143">To create a checksum, call the [New-DSCCheckSum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum) cmdlet.</span></span> <span data-ttu-id="d44b8-144">Přijímá rutina `Path` parametr, který určuje složku, ve kterém se nachází konfigurační soubor MOF.</span><span class="sxs-lookup"><span data-stu-id="d44b8-144">The cmdlet takes a `Path` parameter that specifies the folder where the configuration MOF is located.</span></span> <span data-ttu-id="d44b8-145">Rutina vytvoří kontrolní součet souboru s názvem `ConfigurationMOFName.mof.checksum`, kde `ConfigurationMOFName` je název konfiguračního souboru mof.</span><span class="sxs-lookup"><span data-stu-id="d44b8-145">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span>
<span data-ttu-id="d44b8-146">Pokud existuje více než jednu konfiguraci soubory MOF v zadané složce, kontrolní součet se vytvoří pro každou konfiguraci ve složce.</span><span class="sxs-lookup"><span data-stu-id="d44b8-146">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>

<span data-ttu-id="d44b8-147">Kontrolní součet souboru musí být ve stejném adresáři jako konfigurační soubor MOF (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` ve výchozím nastavení), a mít stejný název `.checksum` připojenou příponou.</span><span class="sxs-lookup"><span data-stu-id="d44b8-147">The checksum file must be present in the same directory as the configuration MOF file (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` by default), and have the same name with the `.checksum` extension appended.</span></span>

> [!NOTE]
> <span data-ttu-id="d44b8-148">Pokud změníte konfiguračního souboru MOF žádným způsobem, je nutné znovu vytvořit kontrolní součet souboru.</span><span class="sxs-lookup"><span data-stu-id="d44b8-148">If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

## <a name="setting-up-a-pull-client-for-smb"></a><span data-ttu-id="d44b8-149">Nastavení načítacího klienta pro SMB</span><span class="sxs-lookup"><span data-stu-id="d44b8-149">Setting up a pull client for SMB</span></span>

<span data-ttu-id="d44b8-150">Nastavení klienta, který si vyžádá konfigurace a/nebo prostředky z do sdílené složky SMB, můžete nakonfigurovat klienta místní Configuration Manageru (LCM) s **ConfigurationRepositoryShare** a **ResourceRepositoryShare** bloky, které určují sdílenou složku, ze kterého chcete o přijetí změn konfigurace a prostředky DSC.</span><span class="sxs-lookup"><span data-stu-id="d44b8-150">To set up a client that pulls configurations and/or resources from an SMB share, you configure the client's Local Configuration Manager (LCM) with **ConfigurationRepositoryShare** and **ResourceRepositoryShare** blocks that specify the share from which to pull configurations and DSC resources.</span></span>

<span data-ttu-id="d44b8-151">Další informace týkající se konfigurace LCM v tématu [nastavení načítacího klienta použití konfiguračních identifikátorů](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="d44b8-151">For more information about configuring the LCM, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d44b8-152">Pro zjednodušení tento příklad používá **PSDscAllowPlainTextPassword** umožňuje předání hesla ve formátu prostého textu **přihlašovacích údajů** parametru.</span><span class="sxs-lookup"><span data-stu-id="d44b8-152">For simplicity, this example uses the **PSDscAllowPlainTextPassword** to allow passing a plaintext password to the **Credential** parameter.</span></span> <span data-ttu-id="d44b8-153">Informace o předávání přihlašovacích údajů bezpečněji, naleznete v tématu [možnosti přihlašovacích údajů v konfiguračních datech](configDataCredentials.md).</span><span class="sxs-lookup"><span data-stu-id="d44b8-153">For information about passing credentials more securely, see [Credentials Options in Configuration Data](configDataCredentials.md).</span></span>
>
> <span data-ttu-id="d44b8-154">Můžete **musí** zadat **ConfigurationID** v **nastavení** bloku metaconfiguration pro serveru vyžádané replikace SMB, i když jsou pouze souhrnné informace prostředky.</span><span class="sxs-lookup"><span data-stu-id="d44b8-154">You **MUST** specify a **ConfigurationID** in the **Settings** block of a metaconfiguration for an SMB pull server, even if you are only pulling resources.</span></span>

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

## <a name="acknowledgements"></a><span data-ttu-id="d44b8-155">Poděkování</span><span class="sxs-lookup"><span data-stu-id="d44b8-155">Acknowledgements</span></span>

<span data-ttu-id="d44b8-156">Speciální díky následující:</span><span class="sxs-lookup"><span data-stu-id="d44b8-156">Special thanks to the following:</span></span>

- <span data-ttu-id="d44b8-157">Mike F. Robbins, jehož příspěvky na použití protokolu SMB pro DSC pomohla informovat obsah v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="d44b8-157">Mike F. Robbins, whose posts on using SMB for DSC helped inform the content in this topic.</span></span> <span data-ttu-id="d44b8-158">Jeho blogu je na [Mike F Robbins](http://mikefrobbins.com/).</span><span class="sxs-lookup"><span data-stu-id="d44b8-158">His blog is at [Mike F Robbins](http://mikefrobbins.com/).</span></span>
- <span data-ttu-id="d44b8-159">Serge Nikalaichyk, kdo vytvořil **cNtfsAccessControl** modulu.</span><span class="sxs-lookup"><span data-stu-id="d44b8-159">Serge Nikalaichyk, who authored the **cNtfsAccessControl** module.</span></span> <span data-ttu-id="d44b8-160">Zdroj pro tento modul je na [cNtfsAccessControl](https://github.com/SNikalaichyk/cNtfsAccessControl).</span><span class="sxs-lookup"><span data-stu-id="d44b8-160">The source for this module is at [cNtfsAccessControl](https://github.com/SNikalaichyk/cNtfsAccessControl).</span></span>

## <a name="see-also"></a><span data-ttu-id="d44b8-161">Viz taky</span><span class="sxs-lookup"><span data-stu-id="d44b8-161">See also</span></span>

[<span data-ttu-id="d44b8-162">Prostředí Windows PowerShell Desired State Configuration – přehled</span><span class="sxs-lookup"><span data-stu-id="d44b8-162">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)

[<span data-ttu-id="d44b8-163">Přijetí konfigurace</span><span class="sxs-lookup"><span data-stu-id="d44b8-163">Enacting configurations</span></span>](enactingConfigurations.md)

[<span data-ttu-id="d44b8-164">Použití konfiguračních identifikátorů k nastavení načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="d44b8-164">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)