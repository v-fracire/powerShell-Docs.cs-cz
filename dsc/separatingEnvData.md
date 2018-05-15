---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Oddělení konfiguračních dat od dat prostředí
ms.openlocfilehash: 3308b83555b3a917e2aa993efcbfa0b946e44048
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="separating-configuration-and-environment-data"></a><span data-ttu-id="5caca-103">Oddělení konfiguračních dat od dat prostředí</span><span class="sxs-lookup"><span data-stu-id="5caca-103">Separating configuration and environment data</span></span>

><span data-ttu-id="5caca-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="5caca-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="5caca-105">Může být užitečné k oddělení dat použít v konfiguraci DSC z konfigurace samotného pomocí konfigurační data.</span><span class="sxs-lookup"><span data-stu-id="5caca-105">It can be useful to separate the data used in a DSC configuration from the configuration itself by using configuration data.</span></span>
<span data-ttu-id="5caca-106">Díky tomu můžete konfigurací jedné pro prostředí s více.</span><span class="sxs-lookup"><span data-stu-id="5caca-106">By doing this, you can use a single configuration for multiple environments.</span></span>

<span data-ttu-id="5caca-107">Například pokud vyvíjíte aplikaci, můžete použít jednu konfiguraci pro vývoj a produkční prostředí a konfigurační data použijte k určení dat pro každé prostředí.</span><span class="sxs-lookup"><span data-stu-id="5caca-107">For example, if you are developing an application, you can use one configuration for both development and production environments, and use configuration data to specify data for each environment.</span></span>

## <a name="what-is-configuration-data"></a><span data-ttu-id="5caca-108">Co je konfigurační data?</span><span class="sxs-lookup"><span data-stu-id="5caca-108">What is configuration data?</span></span>

<span data-ttu-id="5caca-109">Konfigurační data jsou data, která je definována v zatřiďovací tabulky a předaný konfigurace DSC při kompilaci pro tuto konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="5caca-109">Configuration data is data that is defined in a hashtable and passed to a DSC configuration when you compile that configuration.</span></span>

<span data-ttu-id="5caca-110">Podrobný popis **ConfigurationData** zatřiďovací tabulky, najdete v části [pomocí konfiguračních dat](configData.md).</span><span class="sxs-lookup"><span data-stu-id="5caca-110">For a detailed description of the **ConfigurationData** hashtable, see [Using configuration data](configData.md).</span></span>

## <a name="a-simple-example"></a><span data-ttu-id="5caca-111">Jednoduchý příklad</span><span class="sxs-lookup"><span data-stu-id="5caca-111">A simple example</span></span>

<span data-ttu-id="5caca-112">Podívejme se na velmi jednoduchý příklad, pokud chcete zobrazit, jak to funguje.</span><span class="sxs-lookup"><span data-stu-id="5caca-112">Let's look at a very simple example to see how this works.</span></span>
<span data-ttu-id="5caca-113">Vytvoříme konfigurací jedné, který zajistí, že **IIS** je k dispozici v některé uzly a zda **technologie Hyper-V** je k dispozici na jiných:</span><span class="sxs-lookup"><span data-stu-id="5caca-113">We'll create a single configuration that ensures that **IIS** is present on some nodes, and that **Hyper-V** is present on others:</span></span>

```powershell
Configuration MyDscConfiguration {

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        WindowsFeature IISInstall {
            Ensure = 'Present'
            Name   = 'Web-Server'
        }

    }
    Node $AllNodes.Where{$_.Role -eq "VMHost"}.NodeName
    {
        WindowsFeature HyperVInstall {
            Ensure = 'Present'
            Name   = 'Hyper-V'
        }
    }
}

$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName    = 'VM-1'
            Role = 'WebServer'
        },

        @{
            NodeName    = 'VM-2'
            Role = 'VMHost'
        }
    )
}

MyDscConfiguration -ConfigurationData $MyData
```

<span data-ttu-id="5caca-114">Tento skript na posledním řádku zkompiluje konfiguraci předávání `$MyData` jako hodnota **ConfigurationData** parametr.</span><span class="sxs-lookup"><span data-stu-id="5caca-114">The last line in this script compiles the configuration, passing `$MyData` as the value **ConfigurationData** parameter.</span></span>

<span data-ttu-id="5caca-115">Výsledkem je, že jsou vytvořeny dva soubory MOF:</span><span class="sxs-lookup"><span data-stu-id="5caca-115">The result is that two MOF files are created:</span></span>

```
    Directory: C:\DscTests\MyDscConfiguration


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/31/2017   5:09 PM           1968 VM-1.mof
-a----        3/31/2017   5:09 PM           1970 VM-2.mof
```

<span data-ttu-id="5caca-116">`$MyData` Určuje dvou různých uzlech, každou s vlastním `NodeName` a `Role`.</span><span class="sxs-lookup"><span data-stu-id="5caca-116">`$MyData` specifies two different nodes, each with its own `NodeName` and `Role`.</span></span> <span data-ttu-id="5caca-117">Konfigurace dynamicky vytvoří **uzlu** bloky provedením kolekce uzlů získá ze `$MyData` (konkrétně `$AllNodes`) a filtry pro tuto kolekci `Role` vlastnost...</span><span class="sxs-lookup"><span data-stu-id="5caca-117">The configuration dynamically creates **Node** blocks by taking the collection of nodes it gets from `$MyData` (specifically, `$AllNodes`) and filters that collection against the `Role` property..</span></span>

## <a name="using-configuration-data-to-define-development-and-production-environments"></a><span data-ttu-id="5caca-118">Pomocí konfigurační data, abyste definovali vývoj a produkční prostředí</span><span class="sxs-lookup"><span data-stu-id="5caca-118">Using configuration data to define development and production environments</span></span>

<span data-ttu-id="5caca-119">Podívejme se na kompletní příklad, který používá jednu konfiguraci nastavit vývoj a produkční prostředí webu.</span><span class="sxs-lookup"><span data-stu-id="5caca-119">Let's look at a complete example that uses a single configuration to set up both development and production environments of a website.</span></span> <span data-ttu-id="5caca-120">Ve vývojovém prostředí jsou nainstalované IIS a SQL Server na jednom uzlech.</span><span class="sxs-lookup"><span data-stu-id="5caca-120">In the development environment, both IIS and SQL Server are installed on a single nodes.</span></span> <span data-ttu-id="5caca-121">V provozním prostředí jsou nainstalované IIS a SQL Server na samostatné uzly.</span><span class="sxs-lookup"><span data-stu-id="5caca-121">In the production environment, IIS and SQL Server are installed on separate nodes.</span></span> <span data-ttu-id="5caca-122">Konfigurační soubor .psd1 data použijeme k určení data pro dvě různá prostředí.</span><span class="sxs-lookup"><span data-stu-id="5caca-122">We'll use a configuration data .psd1 file to specify the data for the two different environments.</span></span>

 ### <a name="configuration-data-file"></a><span data-ttu-id="5caca-123">Soubor konfiguračních dat</span><span class="sxs-lookup"><span data-stu-id="5caca-123">Configuration data file</span></span>

<span data-ttu-id="5caca-124">Budeme definovat dat vývoj a produkční prostředí do souboru s názvem `DevProdEnvData.psd1` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="5caca-124">We'll define the development and production environment data in a file named `DevProdEnvData.psd1` as follows:</span></span>

```powershell
@{

    AllNodes = @(

        @{
            NodeName        = "*"
            SQLServerName   = "MySQLServer"
            SqlSource       = "C:\Software\Sql"
            DotNetSrc       = "C:\Software\sxs"
        WebSiteName     = "New website"
        },

        @{
            NodeName        = "Prod-SQL"
            Role            = "MSSQL"
        },

        @{
            NodeName        = "Prod-IIS"
            Role            = "Web"
            SiteContents    = "C:\Website\Prod\SiteContents\"
            SitePath        = "\\Prod-IIS\Website\"
        },

        @{
            NodeName         = "Dev"
            Role             = "MSSQL", "Web"
            SiteContents     = "C:\Website\Dev\SiteContents\"
            SitePath         = "\\Dev\Website\"
        }
    )
}
```

### <a name="configuration-script-file"></a><span data-ttu-id="5caca-125">Konfigurační soubor skriptu</span><span class="sxs-lookup"><span data-stu-id="5caca-125">Configuration script file</span></span>

<span data-ttu-id="5caca-126">Nyní v konfiguraci, která je definována v `.ps1` souboru jsme filtrování uzlů definovaného v `DevProdEnvData.psd1` podle jejich role (`MSSQL`, `Dev`, nebo obojí) a příslušným způsobem nakonfigurujte.</span><span class="sxs-lookup"><span data-stu-id="5caca-126">Now, in the configuration, which is defined in a `.ps1` file, we filter the nodes we defined in `DevProdEnvData.psd1` by their role (`MSSQL`, `Dev`, or both), and configure them accordingly.</span></span>
<span data-ttu-id="5caca-127">Vývojové prostředí má systém SQL Server a služby IIS na jednom uzlu, zatímco v provozním prostředí je má na dvou různých uzlech.</span><span class="sxs-lookup"><span data-stu-id="5caca-127">The development environment has both the SQL Server and IIS on one node, while the production environment has them on two different nodes.</span></span>
<span data-ttu-id="5caca-128">Obsah webu se také liší podle specifikace `SiteContents` vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="5caca-128">The site contents is also different, as specified by the `SiteContents` properties.</span></span>

<span data-ttu-id="5caca-129">Na konci konfigurační skript, říkáme konfigurace (Kompilovat jej do dokumentu MOF), předávání `DevProdEnvData.psd1` jako `$ConfigurationData` parametr.</span><span class="sxs-lookup"><span data-stu-id="5caca-129">At the end of the configuration script, we call the configuration (compile it into a MOF document), passing `DevProdEnvData.psd1` as the `$ConfigurationData` parameter.</span></span>

><span data-ttu-id="5caca-130">**Poznámka:** tato konfigurace vyžaduje moduly `xSqlPs` a `xWebAdministration` být nainstalovaný na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="5caca-130">**Note:** This configuration requires the modules `xSqlPs` and `xWebAdministration` to be installed on the target node.</span></span>

<span data-ttu-id="5caca-131">Umožňuje definovat konfigurace do souboru s názvem `MyWebApp.ps1`:</span><span class="sxs-lookup"><span data-stu-id="5caca-131">Let's define the configuration in a file named `MyWebApp.ps1`:</span></span>

```powershell
Configuration MyWebApp
{
    Import-DscResource -Module PSDesiredStateConfiguration
    Import-DscResource -Module xSqlPs
    Import-DscResource -Module xWebAdministration

    Node $AllNodes.Where{$_.Role -contains "MSSQL"}.NodeName
   {
        # Install prerequisites
        WindowsFeature installdotNet35
        {
            Ensure      = "Present"
            Name        = "Net-Framework-Core"
            Source      = "c:\software\sxs"
        }

        # Install SQL Server
        xSqlServerInstall InstallSqlServer
        {
            InstanceName = $Node.SQLServerName
            SourcePath   = $Node.SqlSource
            Features     = "SQLEngine,SSMS"
            DependsOn    = "[WindowsFeature]installdotNet35"

        }
   }

   Node $AllNodes.Where{$_.Role -contains "Web"}.NodeName
   {
        # Install the IIS role
        WindowsFeature IIS
        {
            Ensure       = 'Present'
            Name         = 'Web-Server'
        }

        # Install the ASP .NET 4.5 role
        WindowsFeature AspNet45
        {
            Ensure       = 'Present'
            Name         = 'Web-Asp-Net45'

        }

        # Stop the default website
        xWebsite DefaultSite
        {
            Ensure       = 'Present'
            Name         = 'Default Web Site'
            State        = 'Stopped'
            PhysicalPath = 'C:\inetpub\wwwroot'
            DependsOn    = '[WindowsFeature]IIS'

        }

        # Copy the website content
        File WebContent

        {
            Ensure          = 'Present'
            SourcePath      = $Node.SiteContents
            DestinationPath = $Node.SitePath
            Recurse         = $true
            Type            = 'Directory'
            DependsOn       = '[WindowsFeature]AspNet45'

        }


        # Create the new Website

        xWebsite NewWebsite

        {

            Ensure          = 'Present'
            Name            = $Node.WebSiteName
            State           = 'Started'
            PhysicalPath    = $Node.SitePath
            DependsOn       = '[File]WebContent'
        }

    }

}

MyWebApp -ConfigurationData DevProdEnvData.psd1
```

<span data-ttu-id="5caca-132">Při spuštění této konfiguraci jsou vytvořeny tři soubory MOF (jeden pro každou položku v pojmenované **AllNodes** pole):</span><span class="sxs-lookup"><span data-stu-id="5caca-132">When you run this configuration, three MOF files are created (one for each named entry in the **AllNodes** array):</span></span>

```
    Directory: C:\DscTests\MyWebApp


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/31/2017   5:47 PM           2944 Prod-SQL.mof
-a----        3/31/2017   5:47 PM           6994 Dev.mof
-a----        3/31/2017   5:47 PM           5338 Prod-IIS.mof
```

## <a name="using-non-node-data"></a><span data-ttu-id="5caca-133">Pomocí data bez uzlu</span><span class="sxs-lookup"><span data-stu-id="5caca-133">Using non-node data</span></span>

<span data-ttu-id="5caca-134">Můžete přidat další klíče **ConfigurationData** zatřiďovací tabulky pro data, která není specifické pro uzel.</span><span class="sxs-lookup"><span data-stu-id="5caca-134">You can add additional keys to the **ConfigurationData** hashtable for data that is not specific to a node.</span></span>
<span data-ttu-id="5caca-135">Následující konfigurace zajišťuje přítomnost dva weby.</span><span class="sxs-lookup"><span data-stu-id="5caca-135">The following configuration ensures the presence of two websites.</span></span>
<span data-ttu-id="5caca-136">Data pro každý web jsou definovány v **AllNodes** pole.</span><span class="sxs-lookup"><span data-stu-id="5caca-136">Data for each website are defined in the **AllNodes** array.</span></span>
<span data-ttu-id="5caca-137">Soubor `Config.xml` se používá pro oba weby, takže jsme definovali v další klíč s názvem `NonNodeData`.</span><span class="sxs-lookup"><span data-stu-id="5caca-137">The file `Config.xml` is used for both websites, so we define it in an additional key with the name `NonNodeData`.</span></span>
<span data-ttu-id="5caca-138">Všimněte si, že můžete mít libovolný počet dalších klíčů, přičemž můžete pojmenovat je všechno, co chcete.</span><span class="sxs-lookup"><span data-stu-id="5caca-138">Note that you can have as many additional keys as you want, and you can name them anything you want.</span></span>
<span data-ttu-id="5caca-139">`NonNodeData` je vyhrazené slovo, je právě co jsme se rozhodli název další klíč.</span><span class="sxs-lookup"><span data-stu-id="5caca-139">`NonNodeData` is not a reserved word, it is just what we decided to name the additional key.</span></span>

<span data-ttu-id="5caca-140">Máte přístup k další klíče pomocí speciální proměnná **$ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="5caca-140">You access additional keys by using the special variable **$ConfigurationData**.</span></span>
<span data-ttu-id="5caca-141">V tomto příkladu `ConfigFileContents` přistupuje řádek:</span><span class="sxs-lookup"><span data-stu-id="5caca-141">In this example, `ConfigFileContents` is accessed with the line:</span></span>
```powershell
 Contents = $ConfigurationData.NonNodeData.ConfigFileContents
 ```
 <span data-ttu-id="5caca-142">v `File` prostředků bloku.</span><span class="sxs-lookup"><span data-stu-id="5caca-142">in the `File` resource block.</span></span>


```powershell
$MyData =
@{
    AllNodes =
    @(
        @{
            NodeName           = “*”
            LogPath            = “C:\Logs”
        },

        @{
            NodeName = “VM-1”
            SiteContents = “C:\Site1”
            SiteName = “Website1”
        },


        @{
            NodeName = “VM-2”;
            SiteContents = “C:\Site2”
            SiteName = “Website2”
        }
    );

    NonNodeData =
    @{
        ConfigFileContents = (Get-Content C:\Template\Config.xml)
     }
}

configuration WebsiteConfig
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    node $AllNodes.NodeName
    {
        xWebsite Site
        {
            Name         = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure       = “Present”
        }

        File ConfigFile
        {
            DestinationPath = $Node.SiteContents + “\\config.xml”
            Contents = $ConfigurationData.NonNodeData.ConfigFileContents
        }
    }
}
```


## <a name="see-also"></a><span data-ttu-id="5caca-143">Viz také</span><span class="sxs-lookup"><span data-stu-id="5caca-143">See Also</span></span>
- [<span data-ttu-id="5caca-144">Pomocí konfigurační data</span><span class="sxs-lookup"><span data-stu-id="5caca-144">Using configuration data</span></span>](configData.md)
- [<span data-ttu-id="5caca-145">Možnosti přihlašovací údaje v konfiguračních dat</span><span class="sxs-lookup"><span data-stu-id="5caca-145">Credentials Options in Configuration Data</span></span>](configDataCredentials.md)
- [<span data-ttu-id="5caca-146">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="5caca-146">DSC Configurations</span></span>](configurations.md)
