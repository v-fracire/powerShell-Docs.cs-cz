---
ms.date: 06/12/2017
keywords: jea, prostředí powershell, zabezpečení
title: Registrace JEA konfigurace
ms.openlocfilehash: cda899b20378b0183a3d88ecfd593aaf7356e967
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188509"
---
# <a name="registering-jea-configurations"></a><span data-ttu-id="c2196-103">Registrace JEA konfigurace</span><span class="sxs-lookup"><span data-stu-id="c2196-103">Registering JEA Configurations</span></span>

> <span data-ttu-id="c2196-104">Platí pro: prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c2196-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="c2196-105">Poslední krok, abyste mohli používat JEA, až budete mít vaše [role možnosti](role-capabilities.md) a [relace konfigurační soubor](session-configurations.md) vytvořený a zaregistrujte koncový bod JEA je.</span><span class="sxs-lookup"><span data-stu-id="c2196-105">The last step before you can use JEA once you have your [role capabilities](role-capabilities.md) and [session configuration file](session-configurations.md) created is to register the JEA endpoint.</span></span>
<span data-ttu-id="c2196-106">Tento proces informace o konfiguraci relace se vztahuje na systém a zpřístupní koncový bod pro uživatele a automatizace moduly.</span><span class="sxs-lookup"><span data-stu-id="c2196-106">This process applies the session configuration information to the system and makes the endpoint available for use by users and automation engines.</span></span>

## <a name="single-machine-configuration"></a><span data-ttu-id="c2196-107">Konfigurace jednoho počítače</span><span class="sxs-lookup"><span data-stu-id="c2196-107">Single machine configuration</span></span>

<span data-ttu-id="c2196-108">Pro malá prostředí, můžete nasadit JEA registrace pomocí souboru konfigurace relace [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="c2196-108">For small environments, you can deploy JEA by registering the session configuration file using the [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) cmdlet.</span></span>

<span data-ttu-id="c2196-109">Než začnete, ujistěte se, že byly splněny následující požadavky:</span><span class="sxs-lookup"><span data-stu-id="c2196-109">Before you begin, ensure that the following prerequisites have been met:</span></span>
- <span data-ttu-id="c2196-110">Jeden nebo více rolí byla vytvořena a umístěný ve složce 'RoleCapabilities' platný modulu prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2196-110">One or more roles has been created and placed in the 'RoleCapabilities' folder of a valid PowerShell module.</span></span>
- <span data-ttu-id="c2196-111">Konfigurační soubor relace byla vytvořena a otestovat.</span><span class="sxs-lookup"><span data-stu-id="c2196-111">A session configuration file has been created and tested.</span></span>
- <span data-ttu-id="c2196-112">Uživatel registruje konfigurace JEA má práva správce na systémy.</span><span class="sxs-lookup"><span data-stu-id="c2196-112">The user registering the JEA configuration has administrator rights on the system(s).</span></span>

<span data-ttu-id="c2196-113">Musíte také vyberte název pro svůj koncový bod JEA.</span><span class="sxs-lookup"><span data-stu-id="c2196-113">You will also need to select a name for your JEA endpoint.</span></span>
<span data-ttu-id="c2196-114">Název koncového bodu JEA se bude vyžadovat, když uživatelé se chcete připojit k systému prostřednictvím JEA.</span><span class="sxs-lookup"><span data-stu-id="c2196-114">The name of the JEA endpoint will be required when users want to connect to the system using JEA.</span></span>
<span data-ttu-id="c2196-115">Můžete použít [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) rutiny Zkontrolujte názvy stávající koncové body v systému.</span><span class="sxs-lookup"><span data-stu-id="c2196-115">You can use the [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) cmdlet to check the names of existing endpoints on the system.</span></span>
<span data-ttu-id="c2196-116">Koncové body, které začínají "microsoft", jsou obvykle dodávané se systémem Windows.</span><span class="sxs-lookup"><span data-stu-id="c2196-116">Endpoints that start with 'microsoft' are typically shipped with Windows.</span></span>
<span data-ttu-id="c2196-117">Koncový bod, microsoft.powershell, je výchozí koncový bod používat při připojování ke vzdálený koncový bod prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2196-117">The 'microsoft.powershell' endpoint is the default endpoint used when connecting to a remote PowerShell endpoint.</span></span>

```powershell
PS C:\> Get-PSSessionConfiguration | Select-Object Name

Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

<span data-ttu-id="c2196-118">Pokud zjistíte, vhodný název pro svůj koncový bod JEA, spusťte následující příkaz k registraci koncového bodu.</span><span class="sxs-lookup"><span data-stu-id="c2196-118">When you have determined an appropriate name for your JEA endpoint, run the following command to register the endpoint.</span></span>

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="c2196-119">Výše uvedený příkaz restartuje službu WinRM na serveru.</span><span class="sxs-lookup"><span data-stu-id="c2196-119">The above command will restart the WinRM service on the system.</span></span>
> <span data-ttu-id="c2196-120">To, přeruší se všechny relace vzdálenou komunikaci prostředí PowerShell a také všechny probíhající konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="c2196-120">This will terminate all PowerShell remoting sessions as well as any ongoing DSC configurations.</span></span>
> <span data-ttu-id="c2196-121">Doporučujeme je provést všechny produkčního počítače do offline režimu před spuštěním příkazu, aby se zabránilo přerušení provoz firmy.</span><span class="sxs-lookup"><span data-stu-id="c2196-121">It is recommended that you take any production machines offline before running the command to avoid disrupting business operations.</span></span>

<span data-ttu-id="c2196-122">Pokud byla registrace úspěšná, jste připraveni k [použít JEA](using-jea.md).</span><span class="sxs-lookup"><span data-stu-id="c2196-122">If registration was successful, you are ready to [use JEA](using-jea.md).</span></span>
<span data-ttu-id="c2196-123">Kdykoli; může odstranit konfiguračního souboru relace Po registraci se nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="c2196-123">You may delete the session configuration file at any time; it is not used after registration.</span></span>

## <a name="multi-machine-configuration-with-dsc"></a><span data-ttu-id="c2196-124">Víc počítačů konfigurace s DSC</span><span class="sxs-lookup"><span data-stu-id="c2196-124">Multi-machine configuration with DSC</span></span>

<span data-ttu-id="c2196-125">Pokud nasazujete JEA ve více počítačích, je nejjednodušší model nasazení použít JEA [konfigurace požadovaného stavu](https://msdn.microsoft.com/en-us/powershell/dsc/overview) prostředek pro rychle a konzistentně nasazujte JEA na každém počítači.</span><span class="sxs-lookup"><span data-stu-id="c2196-125">If you are deploying JEA on multiple machines, the simplest deployment model is to use the JEA [Desired State Configuration](https://msdn.microsoft.com/en-us/powershell/dsc/overview) resource to quickly and consistently deploy JEA on each machine.</span></span>

<span data-ttu-id="c2196-126">Pokud chcete nasadit JEA s DSC, budete muset Ujistěte se, že jsou splněny následující požadavky:</span><span class="sxs-lookup"><span data-stu-id="c2196-126">To deploy JEA with DSC, you will need to ensure the following prerequisites are met:</span></span>
- <span data-ttu-id="c2196-127">Jeden nebo více možností role byly vytvořené a přidat na platný modul prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2196-127">One or more role capabilities have been authored and added to a valid PowerShell module.</span></span>
- <span data-ttu-id="c2196-128">Modul prostředí PowerShell, který obsahuje role je uložená na sdílené složce souborů (jen pro čtení), která je přístupný pomocí každý počítač.</span><span class="sxs-lookup"><span data-stu-id="c2196-128">The PowerShell module containing the roles is stored on a (read-only) file share accessible by each machine.</span></span>
- <span data-ttu-id="c2196-129">Nastavení pro konfiguraci relace byly určeny.</span><span class="sxs-lookup"><span data-stu-id="c2196-129">Settings for the session configuration have been determined.</span></span> <span data-ttu-id="c2196-130">Není nutné vytvořit konfigurační soubor relace při používání JEA DSC prostředků.</span><span class="sxs-lookup"><span data-stu-id="c2196-130">You do not need to create a session configuration file when using the JEA DSC resource.</span></span>
- <span data-ttu-id="c2196-131">Máte přihlašovací údaje, které vám umožní provádět akce správy na každém počítači, nebo mají přístup k serveru vyžádané replikace DSC používat ke správě těchto počítačů.</span><span class="sxs-lookup"><span data-stu-id="c2196-131">You have credentials that will allow you to perform administrative actions on each machine, or have access to a DSC pull server used to manage the machines.</span></span>
- <span data-ttu-id="c2196-132">Jste si stáhli [prostředek JEA DSC](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)</span><span class="sxs-lookup"><span data-stu-id="c2196-132">You have downloaded the [JEA DSC resource](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)</span></span>

<span data-ttu-id="c2196-133">Do cílového počítače (nebo načítacího serveru, pokud ji používáte) vytvořte konfiguraci DSC pro koncový bod služby JEA.</span><span class="sxs-lookup"><span data-stu-id="c2196-133">On a target machine (or pull server, if you are using one), create a DSC configuration for your JEA endpoint.</span></span>
<span data-ttu-id="c2196-134">V této konfiguraci použijete prostředek JustEnoughAdministration DSC nastavit relace konfigurační soubor a soubor prostředků pro kopírování prostřednictvím možnosti role ze sdílené složky.</span><span class="sxs-lookup"><span data-stu-id="c2196-134">In this configuration, you will use the JustEnoughAdministration DSC resource to set up the session configuration file and the File resource to copy over the role capabilities from the file share.</span></span>

<span data-ttu-id="c2196-135">Následující vlastnosti se dá konfigurovat pomocí prostředek DSC:</span><span class="sxs-lookup"><span data-stu-id="c2196-135">The following properties are configurable using the DSC resource:</span></span>
- <span data-ttu-id="c2196-136">Definice rolí</span><span class="sxs-lookup"><span data-stu-id="c2196-136">Role Definitions</span></span>
- <span data-ttu-id="c2196-137">Virtuální účet skupiny</span><span class="sxs-lookup"><span data-stu-id="c2196-137">Virtual Account groups</span></span>
- <span data-ttu-id="c2196-138">Název účtu spravované služby skupiny</span><span class="sxs-lookup"><span data-stu-id="c2196-138">Group Managed Service Account name</span></span>
- <span data-ttu-id="c2196-139">Přepis adresáře</span><span class="sxs-lookup"><span data-stu-id="c2196-139">Transcript directory</span></span>
- <span data-ttu-id="c2196-140">Jednotka uživatele</span><span class="sxs-lookup"><span data-stu-id="c2196-140">User drive</span></span>
- <span data-ttu-id="c2196-141">Pravidla podmíněného přístupu</span><span class="sxs-lookup"><span data-stu-id="c2196-141">Conditional access rules</span></span>
- <span data-ttu-id="c2196-142">Spouštěcí skripty pro relaci JEA</span><span class="sxs-lookup"><span data-stu-id="c2196-142">Startup scripts for the JEA session</span></span>

<span data-ttu-id="c2196-143">Syntaxe pro každou z těchto vlastností v konfiguraci DSC je konzistentní s konfiguračního souboru relace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2196-143">The syntax for each of these properties in a DSC configuration is consistent with the PowerShell session configuration file.</span></span>

<span data-ttu-id="c2196-144">Níže je ukázka konfigurace DSC pro modul obecný server údržby.</span><span class="sxs-lookup"><span data-stu-id="c2196-144">Below is a sample DSC configuration for a general server maintenance module.</span></span>

<span data-ttu-id="c2196-145">Předpokládá, že platný modul PowerShell obsahující možnosti role v podsložce 'RoleCapabilities' se nachází na '\\\\myfileshare\\JEA se sdílené složky.</span><span class="sxs-lookup"><span data-stu-id="c2196-145">It assumes that a valid PowerShell module containing role capabilities in a 'RoleCapabilities' subfolder is located on the '\\\\myfileshare\\JEA' file share.</span></span>


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

<span data-ttu-id="c2196-146">Tato konfigurace lze potom použít v systému podle [přímo vyvolání správce místní konfigurace](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) nebo aktualizaci [konfigurace serveru vyžádané](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver).</span><span class="sxs-lookup"><span data-stu-id="c2196-146">This configuration can then be applied on a system by [directly invoking the Local Configuration Manager](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) or updating the [pull server configuration](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver).</span></span>

<span data-ttu-id="c2196-147">Prostředek DSC umožňuje nahradit Microsoft.PowerShell vzdálenou komunikaci výchozí koncový bod.</span><span class="sxs-lookup"><span data-stu-id="c2196-147">The DSC resource also allows you to replace the default Microsoft.PowerShell remoting endpoint.</span></span>
<span data-ttu-id="c2196-148">Pokud to uděláte, bude prostředek automaticky zaregistrovat koncový bod zálohování unconstrainted s názvem "Microsoft.PowerShell.Restricted", který má výchozí seznam ACL WinRM (povolení Remote Management Users a místní správci členy skupiny pro přístup k ní).</span><span class="sxs-lookup"><span data-stu-id="c2196-148">If you do this, the resource will automatically register a backup unconstrainted endpoint named "Microsoft.PowerShell.Restricted" which has the default WinRM ACL (allowing Remote Management Users and local Administrators group members to access it).</span></span>

## <a name="unregistering-jea-configurations"></a><span data-ttu-id="c2196-149">Zrušení registrace JEA konfigurace</span><span class="sxs-lookup"><span data-stu-id="c2196-149">Unregistering JEA configurations</span></span>

<span data-ttu-id="c2196-150">Pokud chcete odstranit koncový bod JEA v systému, použijte [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="c2196-150">To remove a JEA endpoint on a system, use the [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) cmdlet.</span></span>
<span data-ttu-id="c2196-151">Zrušení registrace koncový bod JEA zabrání novým uživatelům ve vytváření nových JEA relací v systému.</span><span class="sxs-lookup"><span data-stu-id="c2196-151">Unregistering a JEA endpoint will prevent new users from creating new JEA sessions on the system.</span></span>
<span data-ttu-id="c2196-152">Také vám umožňuje aktualizovat konfiguraci JEA opakováním registrace konfigurační soubor aktualizované relace pomocí stejného názvu koncového bodu.</span><span class="sxs-lookup"><span data-stu-id="c2196-152">It also allows you to update a JEA configuration by re-registering an updated session configuration file using the same endpoint name.</span></span>

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> <span data-ttu-id="c2196-153">Zrušení registrace JEA koncový bod způsobí, že Služba WinRM restartovat.</span><span class="sxs-lookup"><span data-stu-id="c2196-153">Unregistering a JEA endpoint will cause the WinRM service to restart.</span></span>
> <span data-ttu-id="c2196-154">To přeruší vzdálený operace správy v průběhu, včetně jiných relací prostředí PowerShell, volání rozhraní WMI a některé nástroje pro správu.</span><span class="sxs-lookup"><span data-stu-id="c2196-154">This will interrupt most remote management operations in progress, including other PowerShell sessions, WMI invocations, and some management tools.</span></span>
> <span data-ttu-id="c2196-155">Pouze zrušte registraci prostředí PowerShell koncové body během plánované údržby windows.</span><span class="sxs-lookup"><span data-stu-id="c2196-155">Only unregister PowerShell endpoints during planned maintenance windows.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2196-156">Další kroky</span><span class="sxs-lookup"><span data-stu-id="c2196-156">Next steps</span></span>

- [<span data-ttu-id="c2196-157">Testování JEA koncový bod</span><span class="sxs-lookup"><span data-stu-id="c2196-157">Test the JEA endpoint</span></span>](using-jea.md)