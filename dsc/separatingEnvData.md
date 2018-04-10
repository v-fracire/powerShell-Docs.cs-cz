---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Oddělení konfiguračních dat od dat prostředí
ms.openlocfilehash: c89e26105611eae59a926be1432079913c40671f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="separating-configuration-and-environment-data"></a>Oddělení konfiguračních dat od dat prostředí

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Může být užitečné k oddělení dat použít v konfiguraci DSC z konfigurace samotného pomocí konfigurační data.
Díky tomu můžete konfigurací jedné pro prostředí s více.

Například pokud vyvíjíte aplikaci, můžete použít jednu konfiguraci pro vývoj a produkční prostředí a konfigurační data použijte k určení dat pro každé prostředí.

## <a name="what-is-configuration-data"></a>Co je konfigurační data?

Konfigurační data jsou data, která je definována v zatřiďovací tabulky a předaný konfigurace DSC při kompilaci pro tuto konfiguraci.

Podrobný popis **ConfigurationData** zatřiďovací tabulky, najdete v části [pomocí konfiguračních dat](configData.md).

## <a name="a-simple-example"></a>Jednoduchý příklad

Podívejme se na velmi jednoduchý příklad, pokud chcete zobrazit, jak to funguje.
Vytvoříme konfigurací jedné, který zajistí, že **IIS** je k dispozici v některé uzly a zda **technologie Hyper-V** je k dispozici na jiných:

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

Tento skript na posledním řádku zkompiluje konfiguraci předávání `$MyData` jako hodnota **ConfigurationData** parametr.

Výsledkem je, že jsou vytvořeny dva soubory MOF:

```
    Directory: C:\DscTests\MyDscConfiguration


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/31/2017   5:09 PM           1968 VM-1.mof
-a----        3/31/2017   5:09 PM           1970 VM-2.mof
```

`$MyData` Určuje dvou různých uzlech, každou s vlastním `NodeName` a `Role`. Konfigurace dynamicky vytvoří **uzlu** bloky provedením kolekce uzlů získá ze `$MyData` (konkrétně `$AllNodes`) a filtry pro tuto kolekci `Role` vlastnost...

## <a name="using-configuration-data-to-define-development-and-production-environments"></a>Pomocí konfigurační data, abyste definovali vývoj a produkční prostředí

Podívejme se na kompletní příklad, který používá jednu konfiguraci nastavit vývoj a produkční prostředí webu. Ve vývojovém prostředí jsou nainstalované IIS a SQL Server na jednom uzlech. V provozním prostředí jsou nainstalované IIS a SQL Server na samostatné uzly. Konfigurační soubor .psd1 data použijeme k určení data pro dvě různá prostředí.

 ### <a name="configuration-data-file"></a>Soubor konfiguračních dat

Budeme definovat dat vývoj a produkční prostředí v souboru namd `DevProdEnvData.psd1` následujícím způsobem:

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

### <a name="configuration-script-file"></a>Konfigurační soubor skriptu

Nyní v konfiguraci, která je definována v `.ps1` souboru jsme filtrování uzlů definovaného v `DevProdEnvData.psd1` podle jejich role (`MSSQL`, `Dev`, nebo obojí) a příslušným způsobem nakonfigurujte.
Vývojové prostředí má systém SQL Server a služby IIS na jednom uzlu, zatímco v provozním prostředí je má na dvou různých uzlech.
Obsah webu se také liší podle specifikace `SiteContents` vlastnosti.

Na konci konfigurační skript, říkáme konfigurace (Kompilovat jej do dokumentu MOF), předávání `DevProdEnvData.psd1` jako `$ConfigurationData` parametr.

>**Poznámka:** tato konfigurace vyžaduje moduly `xSqlPs` a `xWebAdministration` být nainstalovaný na cílovém uzlu.

Umožňuje definovat konfigurace do souboru s názvem `MyWebApp.ps1`:

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

Při spuštění této konfiguraci jsou vytvořeny tři soubory MOF (jeden pro každou položku v pojmenované **AllNodes** pole):

```
    Directory: C:\DscTests\MyWebApp


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/31/2017   5:47 PM           2944 Prod-SQL.mof
-a----        3/31/2017   5:47 PM           6994 Dev.mof
-a----        3/31/2017   5:47 PM           5338 Prod-IIS.mof
```

## <a name="using-non-node-data"></a>Pomocí data bez uzlu

Můžete přidat další klíče **ConfigurationData** zatřiďovací tabulky pro data, která není specifické pro uzel.
Následující konfigurace zajišťuje přítomnost dva weby.
Data pro každý web jsou definovány v **AllNodes** pole.
Soubor `Config.xml` se používá pro oba weby, takže jsme definovali v další klíč s názvem `NonNodeData`.
Všimněte si, že můžete mít libovolný počet dalších klíčů, přičemž můžete pojmenovat je všechno, co chcete.
`NonNodeData` je vyhrazené slovo, je právě co jsme se rozhodli název další klíč.

Máte přístup k další klíče pomocí speciální proměnná **$ConfigurationData**.
V tomto příkladu `ConfigFileContents` přistupuje řádek:
```powershell
 Contents = $ConfigurationData.NonNodeData.ConfigFileContents
 ```
 v `File` prostředků bloku.


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


## <a name="see-also"></a>Viz také
- [Pomocí konfigurační data](configData.md)
- [Možnosti přihlašovací údaje v konfiguračních dat](configDataCredentials.md)
- [Konfigurace DSC](configurations.md)