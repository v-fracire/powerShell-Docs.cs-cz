---
ms.date: 06/12/2017
keywords: jea, powershell, zabezpečení
title: Konfigurace registrace funkce JEA
ms.openlocfilehash: 2c4a8f64c966903a6eb8fcabe4cd25ae7f98b2c4
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522845"
---
# <a name="registering-jea-configurations"></a><span data-ttu-id="c1a94-103">Konfigurace registrace funkce JEA</span><span class="sxs-lookup"><span data-stu-id="c1a94-103">Registering JEA Configurations</span></span>

> <span data-ttu-id="c1a94-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c1a94-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="c1a94-105">Poslední krok před použitím JEA až budete mít vaše [funkce rolí](role-capabilities.md) a [relace konfigurační soubor](session-configurations.md) vytvořili, je registrace koncového bodu JEA.</span><span class="sxs-lookup"><span data-stu-id="c1a94-105">The last step before you can use JEA once you have your [role capabilities](role-capabilities.md) and [session configuration file](session-configurations.md) created is to register the JEA endpoint.</span></span>
<span data-ttu-id="c1a94-106">Tento proces informace o konfiguraci relace se vztahuje na systém a zpřístupňuje koncový bod pro uživatele a moduly služby automation.</span><span class="sxs-lookup"><span data-stu-id="c1a94-106">This process applies the session configuration information to the system and makes the endpoint available for use by users and automation engines.</span></span>

## <a name="single-machine-configuration"></a><span data-ttu-id="c1a94-107">Konfigurace jednoho počítače</span><span class="sxs-lookup"><span data-stu-id="c1a94-107">Single machine configuration</span></span>

<span data-ttu-id="c1a94-108">Pro malá prostředí, můžete nasadit JEA tak, že zaregistrujete pomocí souboru konfigurace relace [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="c1a94-108">For small environments, you can deploy JEA by registering the session configuration file using the [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) cmdlet.</span></span>

<span data-ttu-id="c1a94-109">Než začnete, ujistěte se, že jsou splněné následující požadavky:</span><span class="sxs-lookup"><span data-stu-id="c1a94-109">Before you begin, ensure that the following prerequisites have been met:</span></span>
- <span data-ttu-id="c1a94-110">Jeden nebo více rolí byla vytvořena a umístěny ve složce "RoleCapabilities" platný modulu prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1a94-110">One or more roles has been created and placed in the 'RoleCapabilities' folder of a valid PowerShell module.</span></span>
- <span data-ttu-id="c1a94-111">Soubor konfigurace relace byla vytvořena a testování.</span><span class="sxs-lookup"><span data-stu-id="c1a94-111">A session configuration file has been created and tested.</span></span>
- <span data-ttu-id="c1a94-112">Uživatel registruje JEA konfigurace má práva správce na systémy.</span><span class="sxs-lookup"><span data-stu-id="c1a94-112">The user registering the JEA configuration has administrator rights on the system(s).</span></span>

<span data-ttu-id="c1a94-113">Bude také nutné vybrat název vašeho koncového bodu JEA.</span><span class="sxs-lookup"><span data-stu-id="c1a94-113">You will also need to select a name for your JEA endpoint.</span></span>
<span data-ttu-id="c1a94-114">Název koncového bodu JEA bude vyžadovat, když uživatelé se chcete připojit k systému použití funkce JEA.</span><span class="sxs-lookup"><span data-stu-id="c1a94-114">The name of the JEA endpoint will be required when users want to connect to the system using JEA.</span></span>
<span data-ttu-id="c1a94-115">Můžete použít [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) rutiny zkontrolovat názvy stávající koncové body v systému.</span><span class="sxs-lookup"><span data-stu-id="c1a94-115">You can use the [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) cmdlet to check the names of existing endpoints on the system.</span></span>
<span data-ttu-id="c1a94-116">Koncové body, které začínají znakem "microsoft" je obvykle součástí Windows.</span><span class="sxs-lookup"><span data-stu-id="c1a94-116">Endpoints that start with 'microsoft' are typically shipped with Windows.</span></span>
<span data-ttu-id="c1a94-117">Koncový bod 'microsoft.powershell' je použit při připojování ke koncovému bodu vzdáleného prostředí PowerShell výchozí koncový bod.</span><span class="sxs-lookup"><span data-stu-id="c1a94-117">The 'microsoft.powershell' endpoint is the default endpoint used when connecting to a remote PowerShell endpoint.</span></span>

```powershell
PS C:\> Get-PSSessionConfiguration | Select-Object Name

Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

<span data-ttu-id="c1a94-118">Vyhodnoceného vhodný název vašeho koncového bodu JEA spuštěním následujícího příkazu zaregistrujte koncový bod.</span><span class="sxs-lookup"><span data-stu-id="c1a94-118">When you have determined an appropriate name for your JEA endpoint, run the following command to register the endpoint.</span></span>

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="c1a94-119">Výše uvedený příkaz restartuje službu WinRM v systému.</span><span class="sxs-lookup"><span data-stu-id="c1a94-119">The above command will restart the WinRM service on the system.</span></span>
> <span data-ttu-id="c1a94-120">To se ukončí všechny relace vzdálené komunikace prostředí PowerShell, jakož i všechny probíhající konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="c1a94-120">This will terminate all PowerShell remoting sessions as well as any ongoing DSC configurations.</span></span>
> <span data-ttu-id="c1a94-121">Doporučuje se provést jakékoli produkčního počítače do offline režimu před spuštěním příkazu, aby se zabránilo přerušení provozu firmy.</span><span class="sxs-lookup"><span data-stu-id="c1a94-121">It is recommended that you take any production machines offline before running the command to avoid disrupting business operations.</span></span>

<span data-ttu-id="c1a94-122">Pokud byla registrace úspěšná, budete chtít [použít JEA](using-jea.md).</span><span class="sxs-lookup"><span data-stu-id="c1a94-122">If registration was successful, you are ready to [use JEA](using-jea.md).</span></span>
<span data-ttu-id="c1a94-123">Kdykoli; může odstranit soubor konfigurace relace Po registraci není použit.</span><span class="sxs-lookup"><span data-stu-id="c1a94-123">You may delete the session configuration file at any time; it is not used after registration.</span></span>

## <a name="multi-machine-configuration-with-dsc"></a><span data-ttu-id="c1a94-124">Konfiguraci více počítačů s DSC</span><span class="sxs-lookup"><span data-stu-id="c1a94-124">Multi-machine configuration with DSC</span></span>

<span data-ttu-id="c1a94-125">Pokud nasazujete JEA ve více počítačích, je nejjednodušší model nasazení použít JEA [Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) prostředek, který se rychle a konzistentně nasazujte JEA na každém počítači.</span><span class="sxs-lookup"><span data-stu-id="c1a94-125">If you are deploying JEA on multiple machines, the simplest deployment model is to use the JEA [Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) resource to quickly and consistently deploy JEA on each machine.</span></span>

<span data-ttu-id="c1a94-126">Pokud chcete nasadit JEA s DSC, je potřeba zajistit, že jsou splněné následující požadavky:</span><span class="sxs-lookup"><span data-stu-id="c1a94-126">To deploy JEA with DSC, you will need to ensure the following prerequisites are met:</span></span>
- <span data-ttu-id="c1a94-127">Jeden nebo více funkcí role byly vytvořené a přidali na platný modul prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1a94-127">One or more role capabilities have been authored and added to a valid PowerShell module.</span></span>
- <span data-ttu-id="c1a94-128">Modul prostředí PowerShell, který obsahuje role se ukládá ve sdílené složce souboru (jen pro čtení), která je přístupná pomocí každý počítač.</span><span class="sxs-lookup"><span data-stu-id="c1a94-128">The PowerShell module containing the roles is stored on a (read-only) file share accessible by each machine.</span></span>
- <span data-ttu-id="c1a94-129">Nastavení pro konfiguraci relace byla určena.</span><span class="sxs-lookup"><span data-stu-id="c1a94-129">Settings for the session configuration have been determined.</span></span> <span data-ttu-id="c1a94-130">Není nutné k vytvoření souboru konfigurace relace, při použití DSC JEA prostředků.</span><span class="sxs-lookup"><span data-stu-id="c1a94-130">You do not need to create a session configuration file when using the JEA DSC resource.</span></span>
- <span data-ttu-id="c1a94-131">Máte přihlašovací údaje, které umožňují provádět akce správy na každém počítači, nebo mají přístup k serveru vyžádané replikace DSC používá ke správě počítačů.</span><span class="sxs-lookup"><span data-stu-id="c1a94-131">You have credentials that will allow you to perform administrative actions on each machine, or have access to a DSC pull server used to manage the machines.</span></span>
- <span data-ttu-id="c1a94-132">Jste si stáhli [prostředků DSC JEA](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)</span><span class="sxs-lookup"><span data-stu-id="c1a94-132">You have downloaded the [JEA DSC resource](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)</span></span>

<span data-ttu-id="c1a94-133">Do cílového počítače (nebo serveru vyžádané replikace, pokud použijete jeden) vytvořte konfiguraci DSC pro vašeho koncového bodu JEA.</span><span class="sxs-lookup"><span data-stu-id="c1a94-133">On a target machine (or pull server, if you are using one), create a DSC configuration for your JEA endpoint.</span></span>
<span data-ttu-id="c1a94-134">V této konfiguraci bude používat prostředek DSC JustEnoughAdministration k nastavení relace konfigurační soubor a soubor prostředek, který chcete zkopírovat role funkce ze sdílené složky.</span><span class="sxs-lookup"><span data-stu-id="c1a94-134">In this configuration, you will use the JustEnoughAdministration DSC resource to set up the session configuration file and the File resource to copy over the role capabilities from the file share.</span></span>

<span data-ttu-id="c1a94-135">Následující vlastnosti lze konfigurovat pomocí prostředků DSC:</span><span class="sxs-lookup"><span data-stu-id="c1a94-135">The following properties are configurable using the DSC resource:</span></span>
- <span data-ttu-id="c1a94-136">Definice rolí</span><span class="sxs-lookup"><span data-stu-id="c1a94-136">Role Definitions</span></span>
- <span data-ttu-id="c1a94-137">Virtuální účet skupiny</span><span class="sxs-lookup"><span data-stu-id="c1a94-137">Virtual Account groups</span></span>
- <span data-ttu-id="c1a94-138">Název účtu spravované služby skupiny</span><span class="sxs-lookup"><span data-stu-id="c1a94-138">Group Managed Service Account name</span></span>
- <span data-ttu-id="c1a94-139">Adresář přepisu</span><span class="sxs-lookup"><span data-stu-id="c1a94-139">Transcript directory</span></span>
- <span data-ttu-id="c1a94-140">Jednotka uživatele</span><span class="sxs-lookup"><span data-stu-id="c1a94-140">User drive</span></span>
- <span data-ttu-id="c1a94-141">Pravidla podmíněného přístupu</span><span class="sxs-lookup"><span data-stu-id="c1a94-141">Conditional access rules</span></span>
- <span data-ttu-id="c1a94-142">Spouštěcí skripty pro relaci JEA</span><span class="sxs-lookup"><span data-stu-id="c1a94-142">Startup scripts for the JEA session</span></span>

<span data-ttu-id="c1a94-143">Syntaxe pro každý z těchto vlastností v konfiguraci DSC je konzistentní se konfigurační soubor pro relaci Powershellu.</span><span class="sxs-lookup"><span data-stu-id="c1a94-143">The syntax for each of these properties in a DSC configuration is consistent with the PowerShell session configuration file.</span></span>

<span data-ttu-id="c1a94-144">Následuje ukázka konfigurace DSC pro obecný server modul údržby.</span><span class="sxs-lookup"><span data-stu-id="c1a94-144">Below is a sample DSC configuration for a general server maintenance module.</span></span>

<span data-ttu-id="c1a94-145">Předpokládá, že platný modulu prostředí PowerShell, který obsahuje funkce rolí v podsložce "RoleCapabilities" se nachází na "\\\\myfileshare\\JEA" sdílení souborů.</span><span class="sxs-lookup"><span data-stu-id="c1a94-145">It assumes that a valid PowerShell module containing role capabilities in a 'RoleCapabilities' subfolder is located on the '\\\\myfileshare\\JEA' file share.</span></span>


```powershell
Configuration JEAMaintenance
{
    Import-DscResource -Module JustEnoughAdministration, PSDesiredStateConfiguration

    File MaintenanceModule
    {
        SourcePath = "\\myfileshare\JEA\ContosoMaintenance"
        DestinationPath = "C:\Program Files\WindowsPowerShell\Modules\ContosoMaintenance"
        Checksum = "SHA-256"
        Ensure = "Present"
        Type = "Directory"
        Recurse = $true
    }

    JeaEndpoint JEAMaintenanceEndpoint
    {
        EndpointName = "JEAMaintenance"
        RoleDefinitions = "@{ 'CONTOSO\JEAMaintenanceAuditors' = @{ RoleCapabilities = 'GeneralServerMaintenance-Audit' }; 'CONTOSO\JEAMaintenanceAdmins' = @{ RoleCapabilities = 'GeneralServerMaintenance-Audit', 'GeneralServerMaintenance-Admin' } }"
        TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
        DependsOn = '[File]MaintenanceModule'
    }
}
```

<span data-ttu-id="c1a94-146">Potom tuto konfiguraci můžete použít v systému podle [přímo vyvoláním Local Configuration Manageru](https://msdn.microsoft.com/powershell/dsc/metaconfig) nebo aktualizaci [o přijetí změn konfigurace serveru](https://msdn.microsoft.com/powershell/dsc/pullserver).</span><span class="sxs-lookup"><span data-stu-id="c1a94-146">This configuration can then be applied on a system by [directly invoking the Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig) or updating the [pull server configuration](https://msdn.microsoft.com/powershell/dsc/pullserver).</span></span>

<span data-ttu-id="c1a94-147">Prostředek DSC také umožňuje nahradit výchozí koncový bod vzdálené komunikace Microsoft.PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1a94-147">The DSC resource also allows you to replace the default Microsoft.PowerShell remoting endpoint.</span></span>
<span data-ttu-id="c1a94-148">Pokud to uděláte, prostředek se automaticky zaregistrují koncový bod unconstrainted zálohování s názvem "Microsoft.PowerShell.Restricted", který má výchozí seznam ACL WinRM (povoluje Remote Management Users a místní správci členy skupiny pro přístup k ní).</span><span class="sxs-lookup"><span data-stu-id="c1a94-148">If you do this, the resource will automatically register a backup unconstrainted endpoint named "Microsoft.PowerShell.Restricted" which has the default WinRM ACL (allowing Remote Management Users and local Administrators group members to access it).</span></span>

## <a name="unregistering-jea-configurations"></a><span data-ttu-id="c1a94-149">Ruší se registrace funkce JEA konfigurace</span><span class="sxs-lookup"><span data-stu-id="c1a94-149">Unregistering JEA configurations</span></span>

<span data-ttu-id="c1a94-150">Chcete-li odebrat koncový bod JEA v systému, použijte [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="c1a94-150">To remove a JEA endpoint on a system, use the [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) cmdlet.</span></span>
<span data-ttu-id="c1a94-151">Zrušení registrace koncového bodu JEA zabrání novým uživatelům vytvoření nových JEA relací v systému.</span><span class="sxs-lookup"><span data-stu-id="c1a94-151">Unregistering a JEA endpoint will prevent new users from creating new JEA sessions on the system.</span></span>
<span data-ttu-id="c1a94-152">Také vám umožňuje aktualizovat tak, že znovu zaregistrujete soubor konfigurace relace aktualizované pomocí stejného názvu koncového bodu JEA konfigurace.</span><span class="sxs-lookup"><span data-stu-id="c1a94-152">It also allows you to update a JEA configuration by re-registering an updated session configuration file using the same endpoint name.</span></span>

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="c1a94-153">Odregistrace JEA koncový bod způsobí, že Služba WinRM k restartování.</span><span class="sxs-lookup"><span data-stu-id="c1a94-153">Unregistering a JEA endpoint will cause the WinRM service to restart.</span></span>
> <span data-ttu-id="c1a94-154">Tímto se přeruší nejvíce vzdálené správy operace probíhá, včetně jiných relacích Powershellu, rozhraní WMI volání a některé nástroje pro správu.</span><span class="sxs-lookup"><span data-stu-id="c1a94-154">This will interrupt most remote management operations in progress, including other PowerShell sessions, WMI invocations, and some management tools.</span></span>
> <span data-ttu-id="c1a94-155">Pouze zrušte registraci prostředí PowerShell koncové body během plánované údržby windows.</span><span class="sxs-lookup"><span data-stu-id="c1a94-155">Only unregister PowerShell endpoints during planned maintenance windows.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1a94-156">Další kroky</span><span class="sxs-lookup"><span data-stu-id="c1a94-156">Next steps</span></span>

- [<span data-ttu-id="c1a94-157">Testování koncového bodu JEA</span><span class="sxs-lookup"><span data-stu-id="c1a94-157">Test the JEA endpoint</span></span>](using-jea.md)