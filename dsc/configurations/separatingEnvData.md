---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Oddělení konfiguračních dat od dat prostředí
ms.openlocfilehash: 24a92e5e4f15959498b57a1488a688d5548f3585
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403679"
---
# <a name="separating-configuration-and-environment-data"></a>Oddělení konfiguračních dat od dat prostředí

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Může být užitečné oddělit data používaná v konfiguraci DSC v konfiguraci samotného pomocí konfigurační data.
Tímto způsobem můžete použít jediné konfiguraci pro více prostředí.

Například pokud vyvíjíte aplikaci, můžete použít jednu konfiguraci pro vývoj a provoz prostředí a konfigurační data můžete zadat data pro každé prostředí.

## <a name="what-is-configuration-data"></a>Co je konfigurační data?

Konfigurační data jsou data, která je definována v zatřiďovací tabulku a předat konfigurace DSC při kompilaci konfigurace.

Podrobný popis **ConfigurationData** zatřiďovací tabulky, najdete v článku [pomocí konfigurační data](configData.md).

## <a name="a-simple-example"></a>Jednoduchý příklad

Podívejme se na velmi jednoduchý příklad, pokud chcete zobrazit, jak to funguje.
Vytvoříme jediné konfiguraci, která zajistí, že **IIS** je k dispozici v některé uzly, které **Hyper-V** je k dispozici na jiných:

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

Poslední řádek v tomto skriptu zkompiluje konfiguraci předávání `$MyData` jako hodnota **ConfigurationData** parametru.

Výsledkem je, že se vytvoří dva soubory MOF:

```
    Directory: C:\DscTests\MyDscConfiguration


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/31/2017   5:09 PM           1968 VM-1.mof
-a----        3/31/2017   5:09 PM           1970 VM-2.mof
```

`$MyData` Určuje dvou jiných uzlech, každou s vlastním `NodeName` a `Role`. Konfigurace dynamicky vytvoří **uzel** bloky provedením je kolekce uzlů získá z `$MyData` (konkrétně `$AllNodes`) a filtry pro tuto kolekci `Role` vlastnost...

## <a name="using-configuration-data-to-define-development-and-production-environments"></a>Definování vývojovém a produkčním prostředí pomocí konfiguračních dat

Podívejme se na kompletní příklad, který používá jediné konfiguraci do nastavení prostředí vývoje a provozu webu. Ve vývojovém prostředí služba IIS a SQL Server nainstalují na jednotlivé uzly. V produkčním prostředí jsou nainstalované IIS a SQL Server na samostatných uzlech. Soubor konfiguračních dat .psd1 použijeme zadání dat pro dvě různá prostředí.

 ### <a name="configuration-data-file"></a>Soubor konfiguračních dat

Budeme definovat dat prostředí vývoje a provozu do souboru s názvem `DevProdEnvData.psd1` následujícím způsobem:

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

### <a name="configuration-script-file"></a>Soubor skriptu konfigurace

Teď se v konfiguraci, která je definovaná v `.ps1` soubor, můžeme filtrovat uzly jsme definovali v `DevProdEnvData.psd1` podle jejich role (`MSSQL`, `Dev`, nebo obojí) a nakonfigurovat je odpovídajícím způsobem.
Vývojové prostředí má systém SQL Server a služby IIS na jednom uzlu, zatímco má produkční prostředí na dvou různých uzlech.
Obsah webu se také liší, jak jsou určené `SiteContents` vlastnosti.

Na konci konfigurační skript říkáme konfiguraci (kompilována se dokument MOF), předají `DevProdEnvData.psd1` jako `$ConfigurationData` parametru.

>**Poznámka:** Tato konfigurace vyžaduje moduly `xSqlPs` a `xWebAdministration` nainstalovat na cílový uzel.

Umožňuje definovat konfiguraci do souboru s názvem `MyWebApp.ps1`:

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

Při spuštění této konfigurace se vytvoří tři soubory MOF (jeden pro každou položku s názvem **AllNodes** pole):

```
    Directory: C:\DscTests\MyWebApp


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/31/2017   5:47 PM           2944 Prod-SQL.mof
-a----        3/31/2017   5:47 PM           6994 Dev.mof
-a----        3/31/2017   5:47 PM           5338 Prod-IIS.mof
```

## <a name="using-non-node-data"></a>Použití dat mimo uzel

Můžete přidat další klíče **ConfigurationData** zatřiďovací tabulky pro data, která není specifická pro uzel.
Následující konfigurace zajišťuje existenci dva weby.
Data pro každý z těchto webů, které jsou definovány v **AllNodes** pole.
Soubor `Config.xml` se používá pro oba weby, takže jsme jej definovat na další klíč s názvem `NonNodeData`.
Všimněte si, že můžete mít libovolný počet dalších klíčů a chcete, můžete pojmenovat je všechno, co chcete.
`NonNodeData` není o vyhrazené slovo, je právě co jsme se rozhodli pojmenujte Další klíč.

Přístup k další klíče pomocí speciální proměnné **$ConfigurationData**.
V tomto příkladu `ConfigFileContents` je přistupováno pomocí řádku:
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
            NodeName           = “*”
            LogPath            = “C:\Logs”
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
            Name         = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure       = “Present”
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
- [Použití konfiguračních dat](configData.md)
- [Možnosti přihlašovacích údajů v konfiguračních datech](configDataCredentials.md)
- [Konfigurace DSC](configurations.md)
