---
ms.date: 12/12/2018
keywords: DSC, powershell, zdroj, galerie, instalační program
title: Nainstalujte další DSC prostředky
ms.openlocfilehash: ecaf176230ccd934b57b1c27d72ff83e6ba906e9
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403813"
---
# <a name="install-additional-dsc-resources"></a>Nainstalujte další DSC prostředky

Prostředí PowerShell obsahuje několik prostředků Out-of-the-box pro Desired State Configuration (DSC). **PSDesiredStateConfiguration** modul obsahuje všechny dostupné na konkrétní instanci prostředí PowerShell DSC OOB prostředky.

Toto je seznam prostředků OOB zahrnuté v Powershellu 4.0 a popis prostředku funkcí.

> [!NOTE]
> To je neúplný seznam, protože počet OOB prostředků rozrostl s jednotlivými verzemi sady prostředí PowerShell.

|Prostředek  |Popis  |
|---------|---------|
|**Soubor**|Řídí stav souborů a adresářů. Zkopíruje soubory z **zdroj** k **cílové** a aktualizuje je při **zdroj** změny porovnáním data, kontrolní součty a hodnoty hash.|
|**Archiv**|Rozbalí archivy a do zadaného umístění. Ověří archivy se zadaným **kontrolního součtu**.|
|**Prostředí**|Spravuje proměnné prostředí.|
|**Skupina**|Spravuje místní skupiny a řídí členství ve skupině.|
|**Protokol**|Zapisuje zprávy do `Microsoft-Windows-Desired State Configuration/Analytic` protokolu událostí.|
|**Balíček**|Nainstaluje nebo odinstaluje balíčků s využitím **argumenty**, **LogPath**, **ReturnCode**, ostatní nastavení.|
|**registru**|Slouží ke správě klíčů a hodnot registru.|
|**Skript**|Umožňuje vám umožní navrhnout vlastní [připravit test](../resources/get-test-set.md) bloky skriptu.|
|**Služba**|Konfiguruje služby Windows.|
|**Uživatel** |Spravuje místní uživatelé a atributy.|
|**WindowsFeature**|Slouží ke správě rolí a funkcí.|
|**WindowsProcess**|Nakonfiguruje Windows procesy.|

Prostředky OOB povolit dobrým výchozím bodem pro běžné operace. Pokud prostředky OOB nevyhovují vašim potřebám, můžete napsat vlastní [vlastní prostředek](../resources/authoringResource.md). Než napíšete vlastní prostředek váš problém vyřešit, by měl projít číslo obrovského množství prostředků DSC, které již byly vytvořeny od Microsoftu a komunity Powershellu.

Prostředky DSC můžete najít v obou [Galerie prostředí PowerShell](https://www.powershellgallery.com/) a [Githubu](https://github.com/). Prostředky DSC můžete nainstalovat také přímo z konzoly Powershellu pomocí [PowerShellGet](/powershell/module/powershellget/).

## <a name="installing-powershellget"></a>Instalace modulu PowerShellGet

Chcete-li zjistit, jestli už máte **Powershellu** získat nebo pomoc s instalací, viz následující průvodce: [Instalace Správce balíčků PowerShellGet](/powershell/gallery/installing-psget).

## <a name="finding-dsc-resources-using-powershellget"></a>Hledání prostředků DSC použití modulu PowerShellGet

Jednou **PowerShellGet** je nainstalovaná ve vašem systému, můžete najít a nainstalovat prostředky DSC hostované v [Galerie prostředí PowerShell](https://www.powershellgallery.com/).

Nejprve [Find-DSCResource](/powershell/module/powershellget/find-dscresource) rutiny můžete najít prostředky DSC. Při spuštění `Find-DSCResource` poprvé, zobrazí následující výzva k instalaci zprostředkovatele NuGet"".

```
PS> Find-DSCResource

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The
NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\xAdministrator\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider
 by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to
install and import the NuGet provider now?
[Y] Yes  [N] No  [?] Help (default is "Y"):
```

Po stisknutí "y" "NuGet" zprostředkovatel se nainstaluje, se zobrazí seznam prostředků DSC, které si můžete nainstalovat z Galerie prostředí PowerShell.

> [!NOTE]
> Seznam není zobrazen, protože je moc velká.

Můžete také určit `-Name` parametr pomocí zástupných znaků, nebo `-Filter` parametr bez zástupných znaků můžete zúžit hledání. V tomto příkladu se pokusí najít prostředek "Časové pásmo" DSC pomocí zástupných znaků.

> [!IMPORTANT]
> V současné době neexistuje chybu v `Find-DSCResource` rutinu, která brání použití zástupných znaků v obou `-Name` a `-Filter` parametry. Druhý příklad ukazuje alternativní řešení pomocí `Where-Object`.

```
PS> Find-DSCResource -Name *Time*

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Carbon_EnvironmentVariable          2.6.0      Carbon                              PSGallery
Carbon_FirewallRule                 2.6.0      Carbon                              PSGallery
Carbon_Group                        2.6.0      Carbon                              PSGallery
Carbon_IniFile                      2.6.0      Carbon                              PSGallery
Carbon_Permission                   2.6.0      Carbon                              PSGallery
Carbon_Privilege                    2.6.0      Carbon                              PSGallery
Carbon_ScheduledTask                2.6.0      Carbon                              PSGallery
Carbon_Service                      2.6.0      Carbon                              PSGallery
TimeZone                            6.0.0.0    ComputerManagementDsc               PSGallery
xTimeZone                           1.8.0.0    xTimeZone                           PSGallery
xSqlServerDefaultDir                1.0.0      mlSqlServerDSC                      PSGallery
xSqlServerMoveDatabaseFiles         1.0.0      mlSqlServerDSC                      PSGallery
xSqlServerSQLDataRoot               1.0.0      mlSqlServerDSC                      PSGallery
xSqlServerStartupParam              1.0.0      mlSqlServerDSC                      PSGallery
```

Můžete také použít `Where-Object` můžete najít prostředky DSC s podrobnější filtrování. Tento přístup bude pomalejší než při použití integrovaným parametry filtrování.

```
PS> Find-DSCResource | Where-Object {$_.Name -like "Time*"}

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
TimeZone                            6.0.0.0    ComputerManagementDsc               PSGallery
```

Další informace o filtrování najdete v tématu [Where-Object](/powershell/module/microsoft.powershell.core/where-object).

## <a name="installing-dsc-resources-using-powershellget"></a>Instalace pomocí Správce balíčků PowerShellGet prostředků DSC

Chcete-li nainstalovat prostředků DSC, použijte [Install-Module](/powershell/module/PowershellGet/Install-Module) rutiny, zadáte název modulu v části **modulu** název ve výsledcích hledání.

"Časové pásmo" existuje prostředek v modulu "ComputerManagementDSC" tak, že se že tento příklad nainstaluje modul.

> [!NOTE]
> Pokud ještě důvěryhodné Galerie prostředí PowerShell, zobrazí upozornění níže s výzvou k potvrzení a pokyny, jak se vyhnout následné výzvy na nainstaluje.

```
PS> Install-Module -Name ComputerManagementDSC

Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

Stisknutím klávesy "y", chcete-li pokračovat v instalaci modulu. Po instalaci, můžete ověřit, že nový prostředek se instaluje pomocí [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource).

```
PS> Get-DSCResource -Name TimeZone -Syntax

TimeZone [String] #ResourceName
{
    IsSingleInstance = [string]{ Yes }
    TimeZone = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
}
```

Můžete také zobrazit další materiály v nově nainstalovaný modul, tak, že zadáte `-ModuleName` parametru.

```
PS> Get-DSCResource -Module ComputerManagementDSC

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      Computer                  ComputerManagementDsc          6.0.0.0    {Name, Credential, DependsOn, ...
PowerShell      OfflineDomainJoin         ComputerManagementDsc          6.0.0.0    {IsSingleInstance, RequestFile...
PowerShell      PowerPlan                 ComputerManagementDsc          6.0.0.0    {IsSingleInstance, Name, Depen...
PowerShell      PowerShellExecutionPolicy ComputerManagementDsc          6.0.0.0    {ExecutionPolicy, ExecutionPol...
PowerShell      ScheduledTask             ComputerManagementDsc          6.0.0.0    {TaskName, ActionArguments, Ac...
PowerShell      TimeZone                  ComputerManagementDsc          6.0.0.0    {IsSingleInstance, TimeZone, D...
PowerShell      VirtualMemory             ComputerManagementDsc          6.0.0.0    {Drive, Type, DependsOn, Initi...
```

## <a name="see-also"></a>Viz taky

- [Co jsou prostředky?](../resources/resources.md)
