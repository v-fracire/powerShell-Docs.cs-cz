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
# <a name="install-additional-dsc-resources"></a><span data-ttu-id="2de71-103">Nainstalujte další DSC prostředky</span><span class="sxs-lookup"><span data-stu-id="2de71-103">Install Additional DSC Resources</span></span>

<span data-ttu-id="2de71-104">Prostředí PowerShell obsahuje několik prostředků Out-of-the-box pro Desired State Configuration (DSC).</span><span class="sxs-lookup"><span data-stu-id="2de71-104">PowerShell includes several Out-of-the-box resources for Desired State Configuration (DSC).</span></span> <span data-ttu-id="2de71-105">**PSDesiredStateConfiguration** modul obsahuje všechny dostupné na konkrétní instanci prostředí PowerShell DSC OOB prostředky.</span><span class="sxs-lookup"><span data-stu-id="2de71-105">The **PSDesiredStateConfiguration** module contains all of the OOB DSC resources available on your specific instance of PowerShell.</span></span>

<span data-ttu-id="2de71-106">Toto je seznam prostředků OOB zahrnuté v Powershellu 4.0 a popis prostředku funkcí.</span><span class="sxs-lookup"><span data-stu-id="2de71-106">This is a list of the OOB resources included in PowerShell 4.0 and a description of the resource's capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="2de71-107">To je neúplný seznam, protože počet OOB prostředků rozrostl s jednotlivými verzemi sady prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2de71-107">This is an incomplete list, as the number of OOB resources has grown with each version of PowerShell.</span></span>

|<span data-ttu-id="2de71-108">Prostředek</span><span class="sxs-lookup"><span data-stu-id="2de71-108">Resource</span></span>  |<span data-ttu-id="2de71-109">Popis</span><span class="sxs-lookup"><span data-stu-id="2de71-109">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="2de71-110">**Soubor**</span><span class="sxs-lookup"><span data-stu-id="2de71-110">**File**</span></span>|<span data-ttu-id="2de71-111">Řídí stav souborů a adresářů.</span><span class="sxs-lookup"><span data-stu-id="2de71-111">Controls the state of files and directories.</span></span> <span data-ttu-id="2de71-112">Zkopíruje soubory z **zdroj** k **cílové** a aktualizuje je při **zdroj** změny porovnáním data, kontrolní součty a hodnoty hash.</span><span class="sxs-lookup"><span data-stu-id="2de71-112">Copies files from a **Source** to a **Destination** and updates them when the **Source** changes by comparing dates, checksums, and hashes.</span></span>|
|<span data-ttu-id="2de71-113">**Archiv**</span><span class="sxs-lookup"><span data-stu-id="2de71-113">**Archive**</span></span>|<span data-ttu-id="2de71-114">Rozbalí archivy a do zadaného umístění.</span><span class="sxs-lookup"><span data-stu-id="2de71-114">Unpacks archives and a specified location.</span></span> <span data-ttu-id="2de71-115">Ověří archivy se zadaným **kontrolního součtu**.</span><span class="sxs-lookup"><span data-stu-id="2de71-115">Validates the archives with a specified **Checksum**.</span></span>|
|<span data-ttu-id="2de71-116">**Prostředí**</span><span class="sxs-lookup"><span data-stu-id="2de71-116">**Environment**</span></span>|<span data-ttu-id="2de71-117">Spravuje proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="2de71-117">Manages environment variables.</span></span>|
|<span data-ttu-id="2de71-118">**Skupina**</span><span class="sxs-lookup"><span data-stu-id="2de71-118">**Group**</span></span>|<span data-ttu-id="2de71-119">Spravuje místní skupiny a řídí členství ve skupině.</span><span class="sxs-lookup"><span data-stu-id="2de71-119">Manages local groups and controls group membership.</span></span>|
|<span data-ttu-id="2de71-120">**Protokol**</span><span class="sxs-lookup"><span data-stu-id="2de71-120">**Log**</span></span>|<span data-ttu-id="2de71-121">Zapisuje zprávy do `Microsoft-Windows-Desired State Configuration/Analytic` protokolu událostí.</span><span class="sxs-lookup"><span data-stu-id="2de71-121">Writes messages to the `Microsoft-Windows-Desired State Configuration/Analytic` event log.</span></span>|
|<span data-ttu-id="2de71-122">**Balíček**</span><span class="sxs-lookup"><span data-stu-id="2de71-122">**Package**</span></span>|<span data-ttu-id="2de71-123">Nainstaluje nebo odinstaluje balíčků s využitím **argumenty**, **LogPath**, **ReturnCode**, ostatní nastavení.</span><span class="sxs-lookup"><span data-stu-id="2de71-123">Installs or uninstalls packages using **Arguments**, **LogPath**, **ReturnCode**, other settings.</span></span>|
|<span data-ttu-id="2de71-124">**registru**</span><span class="sxs-lookup"><span data-stu-id="2de71-124">**Registry**</span></span>|<span data-ttu-id="2de71-125">Slouží ke správě klíčů a hodnot registru.</span><span class="sxs-lookup"><span data-stu-id="2de71-125">Manages registry keys and values.</span></span>|
|<span data-ttu-id="2de71-126">**Skript**</span><span class="sxs-lookup"><span data-stu-id="2de71-126">**Script**</span></span>|<span data-ttu-id="2de71-127">Umožňuje vám umožní navrhnout vlastní [připravit test](../resources/get-test-set.md) bloky skriptu.</span><span class="sxs-lookup"><span data-stu-id="2de71-127">Allows you to design your own [get-test-set](../resources/get-test-set.md) script blocks.</span></span>|
|<span data-ttu-id="2de71-128">**Služba**</span><span class="sxs-lookup"><span data-stu-id="2de71-128">**Service**</span></span>|<span data-ttu-id="2de71-129">Konfiguruje služby Windows.</span><span class="sxs-lookup"><span data-stu-id="2de71-129">Configures Windows services.</span></span>|
|<span data-ttu-id="2de71-130">**Uživatel**</span><span class="sxs-lookup"><span data-stu-id="2de71-130">**User**</span></span> |<span data-ttu-id="2de71-131">Spravuje místní uživatelé a atributy.</span><span class="sxs-lookup"><span data-stu-id="2de71-131">Manages local users and attributes.</span></span>|
|<span data-ttu-id="2de71-132">**WindowsFeature**</span><span class="sxs-lookup"><span data-stu-id="2de71-132">**WindowsFeature**</span></span>|<span data-ttu-id="2de71-133">Slouží ke správě rolí a funkcí.</span><span class="sxs-lookup"><span data-stu-id="2de71-133">Manages roles and features.</span></span>|
|<span data-ttu-id="2de71-134">**WindowsProcess**</span><span class="sxs-lookup"><span data-stu-id="2de71-134">**WindowsProcess**</span></span>|<span data-ttu-id="2de71-135">Nakonfiguruje Windows procesy.</span><span class="sxs-lookup"><span data-stu-id="2de71-135">Configures Windows processes.</span></span>|

<span data-ttu-id="2de71-136">Prostředky OOB povolit dobrým výchozím bodem pro běžné operace.</span><span class="sxs-lookup"><span data-stu-id="2de71-136">The OOB resources allow a good starting point for common operations.</span></span> <span data-ttu-id="2de71-137">Pokud prostředky OOB nevyhovují vašim potřebám, můžete napsat vlastní [vlastní prostředek](../resources/authoringResource.md).</span><span class="sxs-lookup"><span data-stu-id="2de71-137">If the OOB resources do not meet your needs, you can write your own [Custom Resource](../resources/authoringResource.md).</span></span> <span data-ttu-id="2de71-138">Než napíšete vlastní prostředek váš problém vyřešit, by měl projít číslo obrovského množství prostředků DSC, které již byly vytvořeny od Microsoftu a komunity Powershellu.</span><span class="sxs-lookup"><span data-stu-id="2de71-138">Before you write a custom resource to solve your problem, you should look through the vast number of DSC resources that have already been created by both Microsoft and the PowerShell community.</span></span>

<span data-ttu-id="2de71-139">Prostředky DSC můžete najít v obou [Galerie prostředí PowerShell](https://www.powershellgallery.com/) a [Githubu](https://github.com/).</span><span class="sxs-lookup"><span data-stu-id="2de71-139">You can find DSC resources in both the [PowerShell Gallery](https://www.powershellgallery.com/) and [GitHub](https://github.com/).</span></span> <span data-ttu-id="2de71-140">Prostředky DSC můžete nainstalovat také přímo z konzoly Powershellu pomocí [PowerShellGet](/powershell/module/powershellget/).</span><span class="sxs-lookup"><span data-stu-id="2de71-140">You can also install DSC resources directly from the PowerShell console using [PowerShellGet](/powershell/module/powershellget/).</span></span>

## <a name="installing-powershellget"></a><span data-ttu-id="2de71-141">Instalace modulu PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="2de71-141">Installing PowerShellGet</span></span>

<span data-ttu-id="2de71-142">Chcete-li zjistit, jestli už máte **Powershellu** získat nebo pomoc s instalací, viz následující průvodce: [Instalace Správce balíčků PowerShellGet](/powershell/gallery/installing-psget).</span><span class="sxs-lookup"><span data-stu-id="2de71-142">To determine if you already have **PowerShell** get, or to get help installing it, see the following guide: [Installing PowerShellGet](/powershell/gallery/installing-psget).</span></span>

## <a name="finding-dsc-resources-using-powershellget"></a><span data-ttu-id="2de71-143">Hledání prostředků DSC použití modulu PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="2de71-143">Finding DSC resources using PowerShellGet</span></span>

<span data-ttu-id="2de71-144">Jednou **PowerShellGet** je nainstalovaná ve vašem systému, můžete najít a nainstalovat prostředky DSC hostované v [Galerie prostředí PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="2de71-144">Once **PowerShellGet** is installed on your system, you can find and install DSC resources hosted in the [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>

<span data-ttu-id="2de71-145">Nejprve [Find-DSCResource](/powershell/module/powershellget/find-dscresource) rutiny můžete najít prostředky DSC.</span><span class="sxs-lookup"><span data-stu-id="2de71-145">First, use the [Find-DSCResource](/powershell/module/powershellget/find-dscresource) cmdlet to find DSC resources.</span></span> <span data-ttu-id="2de71-146">Při spuštění `Find-DSCResource` poprvé, zobrazí následující výzva k instalaci zprostředkovatele NuGet"".</span><span class="sxs-lookup"><span data-stu-id="2de71-146">When you run `Find-DSCResource` for the first time, you see the following prompt to install the "NuGet provider".</span></span>

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

<span data-ttu-id="2de71-147">Po stisknutí "y" "NuGet" zprostředkovatel se nainstaluje, se zobrazí seznam prostředků DSC, které si můžete nainstalovat z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2de71-147">After pressing 'y', the "NuGet" provider is installed, you see a list of DSC resources that you can install from the PowerShell Gallery.</span></span>

> [!NOTE]
> <span data-ttu-id="2de71-148">Seznam není zobrazen, protože je moc velká.</span><span class="sxs-lookup"><span data-stu-id="2de71-148">List is not shown because it is very large.</span></span>

<span data-ttu-id="2de71-149">Můžete také určit `-Name` parametr pomocí zástupných znaků, nebo `-Filter` parametr bez zástupných znaků můžete zúžit hledání.</span><span class="sxs-lookup"><span data-stu-id="2de71-149">You can also specify the `-Name` parameter using wildcards, or `-Filter` parameter without wildcards to narrow down your search.</span></span> <span data-ttu-id="2de71-150">V tomto příkladu se pokusí najít prostředek "Časové pásmo" DSC pomocí zástupných znaků.</span><span class="sxs-lookup"><span data-stu-id="2de71-150">This example attempts to find a "TimeZone" DSC resource using the wildcards.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2de71-151">V současné době neexistuje chybu v `Find-DSCResource` rutinu, která brání použití zástupných znaků v obou `-Name` a `-Filter` parametry.</span><span class="sxs-lookup"><span data-stu-id="2de71-151">Currently there is a bug in the `Find-DSCResource` cmdlet that prevents using wildcards in both the `-Name` and `-Filter` parameters.</span></span> <span data-ttu-id="2de71-152">Druhý příklad ukazuje alternativní řešení pomocí `Where-Object`.</span><span class="sxs-lookup"><span data-stu-id="2de71-152">The second example below shows a workaround using `Where-Object`.</span></span>

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

<span data-ttu-id="2de71-153">Můžete také použít `Where-Object` můžete najít prostředky DSC s podrobnější filtrování.</span><span class="sxs-lookup"><span data-stu-id="2de71-153">You can also use `Where-Object` to find DSC resources with more granular filtering.</span></span> <span data-ttu-id="2de71-154">Tento přístup bude pomalejší než při použití integrovaným parametry filtrování.</span><span class="sxs-lookup"><span data-stu-id="2de71-154">This approach will be slower than using built in filtering parameters.</span></span>

```
PS> Find-DSCResource | Where-Object {$_.Name -like "Time*"}

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
TimeZone                            6.0.0.0    ComputerManagementDsc               PSGallery
```

<span data-ttu-id="2de71-155">Další informace o filtrování najdete v tématu [Where-Object](/powershell/module/microsoft.powershell.core/where-object).</span><span class="sxs-lookup"><span data-stu-id="2de71-155">For more information on filtering, see [Where-Object](/powershell/module/microsoft.powershell.core/where-object).</span></span>

## <a name="installing-dsc-resources-using-powershellget"></a><span data-ttu-id="2de71-156">Instalace pomocí Správce balíčků PowerShellGet prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="2de71-156">Installing DSC Resources using PowerShellGet</span></span>

<span data-ttu-id="2de71-157">Chcete-li nainstalovat prostředků DSC, použijte [Install-Module](/powershell/module/PowershellGet/Install-Module) rutiny, zadáte název modulu v části **modulu** název ve výsledcích hledání.</span><span class="sxs-lookup"><span data-stu-id="2de71-157">To install a DSC resource, use the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet, specifying the name of the module shown under **Module** name in your search results.</span></span>

<span data-ttu-id="2de71-158">"Časové pásmo" existuje prostředek v modulu "ComputerManagementDSC" tak, že se že tento příklad nainstaluje modul.</span><span class="sxs-lookup"><span data-stu-id="2de71-158">The "TimeZone" resource exists in the "ComputerManagementDSC" module, so that is the module this example installs.</span></span>

> [!NOTE]
> <span data-ttu-id="2de71-159">Pokud ještě důvěryhodné Galerie prostředí PowerShell, zobrazí upozornění níže s výzvou k potvrzení a pokyny, jak se vyhnout následné výzvy na nainstaluje.</span><span class="sxs-lookup"><span data-stu-id="2de71-159">If you have not trusted the PowerShell gallery, you see the warning below asking for confirmation, and instructing you how to avoid subsequent prompts on installs.</span></span>

```
PS> Install-Module -Name ComputerManagementDSC

Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

<span data-ttu-id="2de71-160">Stisknutím klávesy "y", chcete-li pokračovat v instalaci modulu.</span><span class="sxs-lookup"><span data-stu-id="2de71-160">Press 'y' to continue installing the module.</span></span> <span data-ttu-id="2de71-161">Po instalaci, můžete ověřit, že nový prostředek se instaluje pomocí [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource).</span><span class="sxs-lookup"><span data-stu-id="2de71-161">After install, you can verify that your new resource is installed using [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource).</span></span>

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

<span data-ttu-id="2de71-162">Můžete také zobrazit další materiály v nově nainstalovaný modul, tak, že zadáte `-ModuleName` parametru.</span><span class="sxs-lookup"><span data-stu-id="2de71-162">You can also view other resources in your newly installed module, by specifying the `-ModuleName` parameter.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="2de71-163">Viz taky</span><span class="sxs-lookup"><span data-stu-id="2de71-163">See also</span></span>

- [<span data-ttu-id="2de71-164">Co jsou prostředky?</span><span class="sxs-lookup"><span data-stu-id="2de71-164">What are Resources?</span></span>](../resources/resources.md)
