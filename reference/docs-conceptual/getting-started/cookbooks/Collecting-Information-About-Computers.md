---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Shromažďování informací o počítačích
ms.assetid: 9e7b6a2d-34f7-4731-a92c-8b3382eb51bb
ms.openlocfilehash: ca92474eaf6fa546c3d6450f5a282e45157018a8
ms.sourcegitcommit: 4a841ebda3339ae2477e0f5f5be8c01740221232
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2018
---
# <a name="collecting-information-about-computers"></a><span data-ttu-id="d742c-103">Shromažďování informací o počítačích</span><span class="sxs-lookup"><span data-stu-id="d742c-103">Collecting Information About Computers</span></span>

<span data-ttu-id="d742c-104">Rutiny z **CimCmdlets** modulu jsou nejdůležitější rutiny pro úlohy správy obecného systému.</span><span class="sxs-lookup"><span data-stu-id="d742c-104">Cmdlets from **CimCmdlets** module are the most important cmdlets for general system management tasks.</span></span>
<span data-ttu-id="d742c-105">Všechna nastavení kritické subsystém se zveřejňují přes rozhraní WMI.</span><span class="sxs-lookup"><span data-stu-id="d742c-105">All critical subsystem settings are exposed through WMI.</span></span>
<span data-ttu-id="d742c-106">Kromě toho WMI data jsou považovány za objekty, které jsou v kolekcích jednu nebo více položek.</span><span class="sxs-lookup"><span data-stu-id="d742c-106">Furthermore, WMI treats data as objects that are in collections of one or more items.</span></span>
<span data-ttu-id="d742c-107">Protože prostředí Windows PowerShell taky pracuje s objekty a má kanál, který vám umožní zacházet s jednoho nebo více objektů stejným způsobem, obecný přístup WMI umožňuje provádět některé pokročilé úlohy s uživatele příliš mnoho zásahů.</span><span class="sxs-lookup"><span data-stu-id="d742c-107">Because Windows PowerShell also works with objects and has a pipeline that allows you to treat single or multiple objects in the same way, generic WMI access allows you to perform some advanced tasks with very little work.</span></span>

<span data-ttu-id="d742c-108">Následující příklady ukazují, jak shromažďovat konkrétní informace pomocí `Get-CimInstance` libovolný počítač.</span><span class="sxs-lookup"><span data-stu-id="d742c-108">The following examples demonstrate how to collect specific information by using `Get-CimInstance` against an arbitrary computer.</span></span>
<span data-ttu-id="d742c-109">Určíme **ComputerName** parametr s hodnotou tečkou (**.**), který představuje místní počítač.</span><span class="sxs-lookup"><span data-stu-id="d742c-109">We specify the **ComputerName** parameter with the dot value (**.**), which represents the local computer.</span></span>
<span data-ttu-id="d742c-110">Můžete zadat název nebo IP adresu přidruženou libovolného počítače, které lze získat přístup pomocí rozhraní WMI.</span><span class="sxs-lookup"><span data-stu-id="d742c-110">You can specify a name or IP address associated with any computer you can reach through WMI.</span></span>
<span data-ttu-id="d742c-111">Pokud chcete načíst informace o místním počítači, může vynechat **ComputerName** parametr.</span><span class="sxs-lookup"><span data-stu-id="d742c-111">To retrieve information about the local computer, you could omit the **ComputerName** parameter.</span></span>

### <a name="listing-desktop-settings"></a><span data-ttu-id="d742c-112">Výpis nastavení plochy</span><span class="sxs-lookup"><span data-stu-id="d742c-112">Listing Desktop Settings</span></span>

<span data-ttu-id="d742c-113">Začneme příkaz, který shromažďuje informace o stolní počítače v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="d742c-113">We'll begin with a command that collects information about the desktops on the local computer.</span></span>

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName .
```

<span data-ttu-id="d742c-114">Tento příkaz vrátí informace pro všechny pracovní plochy, zda jsou právě používány, nebo ne.</span><span class="sxs-lookup"><span data-stu-id="d742c-114">This returns information for all desktops, whether they are in use or not.</span></span>

> [!NOTE]
> <span data-ttu-id="d742c-115">Informace o vrácené některé třídy WMI může být velmi podrobné a často obsahují metadata o třídu služby WMI.</span><span class="sxs-lookup"><span data-stu-id="d742c-115">Information returned by some WMI classes can be very detailed, and often include metadata about the WMI class.</span></span>
<span data-ttu-id="d742c-116">Protože většina těchto metadat vlastností názvy, které začínají **Cim**, můžete filtrovat pomocí vlastností `Select-Object`.</span><span class="sxs-lookup"><span data-stu-id="d742c-116">Because most of these metadata properties have names that begin with **Cim**, you can filter the properties using `Select-Object`.</span></span>
<span data-ttu-id="d742c-117">Zadejte **- ExcludeProperty** parametr s "Cim \*" jako hodnotu.</span><span class="sxs-lookup"><span data-stu-id="d742c-117">Specify the **-ExcludeProperty** parameter with "Cim\*" as the value.</span></span>
<span data-ttu-id="d742c-118">Příklad:</span><span class="sxs-lookup"><span data-stu-id="d742c-118">For example:</span></span>

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

<span data-ttu-id="d742c-119">Filtrovat metadata, použijte operátor kanálu (|) k odeslání výsledky `Get-CimInstance` příkaz `Select-Object -ExcludeProperty "CIM*"`.</span><span class="sxs-lookup"><span data-stu-id="d742c-119">To filter out the metadata, use a pipeline operator (|) to send the results of the `Get-CimInstance` command to `Select-Object -ExcludeProperty "CIM*"`.</span></span>

### <a name="listing-bios-information"></a><span data-ttu-id="d742c-120">Výpis informace o systému BIOS</span><span class="sxs-lookup"><span data-stu-id="d742c-120">Listing BIOS Information</span></span>

<span data-ttu-id="d742c-121">Služba WMI **Win32_BIOS** třída vrátí poměrně compact a úplné informace o systému BIOS v místním počítači:</span><span class="sxs-lookup"><span data-stu-id="d742c-121">The WMI **Win32_BIOS** class returns fairly compact and complete information about the system BIOS on the local computer:</span></span>

```powershell
Get-CimInstance -ClassName Win32_BIOS -ComputerName .
```

### <a name="listing-processor-information"></a><span data-ttu-id="d742c-122">Výpis informace o procesoru</span><span class="sxs-lookup"><span data-stu-id="d742c-122">Listing Processor Information</span></span>

<span data-ttu-id="d742c-123">Informace o obecné procesoru můžete načíst pomocí rozhraní WMI na **Win32_Processor** třídy, i když budete pravděpodobně chtít filtrování informací:</span><span class="sxs-lookup"><span data-stu-id="d742c-123">You can retrieve general processor information by using WMI's **Win32_Processor** class, although you will likely want to filter the information:</span></span>

```powershell
Get-CimInstance -ClassName Win32_Processor -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

<span data-ttu-id="d742c-124">Obecný popis řetězce třídu procesoru, může jen vrátit **typ SystemType** vlastnost:</span><span class="sxs-lookup"><span data-stu-id="d742c-124">For a generic description string of the processor family, you can just return the **SystemType** property:</span></span>

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -ComputerName . | Select-Object -Property SystemType

SystemType
----------
X86-based PC
```

### <a name="listing-computer-manufacturer-and-model"></a><span data-ttu-id="d742c-125">Výpis Model a výrobce počítače</span><span class="sxs-lookup"><span data-stu-id="d742c-125">Listing Computer Manufacturer and Model</span></span>

<span data-ttu-id="d742c-126">Informace o modelu počítače je také dostupná z **Win32_ComputerSystem**.</span><span class="sxs-lookup"><span data-stu-id="d742c-126">Computer model information is also available from **Win32_ComputerSystem**.</span></span>
<span data-ttu-id="d742c-127">Ve standardním výstupu zobrazeného nebudete potřebovat jakéhokoli filtrování poskytující OEM data:</span><span class="sxs-lookup"><span data-stu-id="d742c-127">The standard displayed output will not need any filtering to provide OEM data:</span></span>

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem
```

```output
Name PrimaryOwnerName Domain    TotalPhysicalMemory Model                   Manufacturer
---- ---------------- ------    ------------------- -----                   ------------
MyPC Jane Doe         WORKGROUP 804765696           DA243A-ABA 6415cl NA910 Compaq Presario 06
```

<span data-ttu-id="d742c-128">Výstup z příkazy jako to, které vrací informace přímo z některé hardwaru, je pouze jako vhodný jako data, která máte.</span><span class="sxs-lookup"><span data-stu-id="d742c-128">Your output from commands such as this, which return information directly from some hardware, is only as good as the data you have.</span></span>
<span data-ttu-id="d742c-129">Některé informace není správně nakonfigurováno podle výrobců hardwaru a proto pravděpodobně není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="d742c-129">Some information is not correctly configured by hardware manufacturers and may therefore be unavailable.</span></span>

### <a name="listing-installed-hotfixes"></a><span data-ttu-id="d742c-130">Výpis nainstalovaných oprav hotfix</span><span class="sxs-lookup"><span data-stu-id="d742c-130">Listing Installed Hotfixes</span></span>

<span data-ttu-id="d742c-131">Můžete vytvořit seznam všech nainstalovaných oprav hotfix s použitím **Win32_QuickFixEngineering**:</span><span class="sxs-lookup"><span data-stu-id="d742c-131">You can list all installed hotfixes by using **Win32_QuickFixEngineering**:</span></span>

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName .
```

<span data-ttu-id="d742c-132">Tato třída vrátí seznam oprav hotfix, které vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="d742c-132">This class returns a list of hotfixes that looks like this:</span></span>

```output
Source Description     HotFixID  InstalledBy   InstalledOn PSComputerName
------ -----------     --------  -----------   ----------- --------------
       Security Update KB4048951 Administrator 12/16/2017  .
```

<span data-ttu-id="d742c-133">Pro více stručného výstup můžete chtít vyloučit některé vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="d742c-133">For more succinct output, you may want to exclude some properties.</span></span>
<span data-ttu-id="d742c-134">Přestože je možné použít `Get-CimInstance`na **vlastnost** parametr zvolit pouze **HotFixID**, to tak, budou vracet další informace, protože je ve výchozím nastavení zobrazí všechna metadata:</span><span class="sxs-lookup"><span data-stu-id="d742c-134">Although you can use the `Get-CimInstance`'s **Property** parameter to choose only the **HotFixID**, doing so will actually return more information, because all the metadata is displayed by default:</span></span>

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName . -Property HotFixID
```

```output
PSShowComputerName    : True
InstalledOn           :
Caption               :
Description           :
InstallDate           :
Name                  :
Status                :
CSName                :
FixComments           :
HotFixID              : KB4048951
InstalledBy           :
ServicePackInEffect   :
PSComputerName        : .
CimClass              : root/cimv2:Win32_QuickFixEngineering
CimInstanceProperties : {Caption, Description, InstallDate, Name...}
CimSystemProperties   : Microsoft.Management.Infrastructure.CimSystemProperties
```

<span data-ttu-id="d742c-135">Vrátí další data, protože parametr vlastností v `Get-CimInstance` omezuje vlastnosti vrácená z instancí třídy služby WMI, není objekt byl vrácen do prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d742c-135">The additional data is returned, because the Property parameter in `Get-CimInstance` restricts the properties returned from WMI class instances, not the object returned to Windows PowerShell.</span></span>
<span data-ttu-id="d742c-136">Chcete-li snížit výstup, použijte `Select-Object`:</span><span class="sxs-lookup"><span data-stu-id="d742c-136">To reduce the output, use `Select-Object`:</span></span>

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName . -Property HotFixId | Select-Object -Property HotFixId
```

```output
HotFixId
--------
KB4048951
```

### <a name="listing-operating-system-version-information"></a><span data-ttu-id="d742c-137">Výpis informace o verzi operačního systému</span><span class="sxs-lookup"><span data-stu-id="d742c-137">Listing Operating System Version Information</span></span>

<span data-ttu-id="d742c-138">**Win32_OperatingSystem** vlastnosti třídy zahrnují informace o verzi a service pack.</span><span class="sxs-lookup"><span data-stu-id="d742c-138">The **Win32_OperatingSystem** class properties include version and service pack information.</span></span>
<span data-ttu-id="d742c-139">Můžete vybrat explicitně pouze tyto vlastnosti k získání informací o verzi shrnutí z **Win32_OperatingSystem**:</span><span class="sxs-lookup"><span data-stu-id="d742c-139">You can explicitly select only these properties to get a version information summary from **Win32_OperatingSystem**:</span></span>

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property BuildNumber,BuildType,OSType,ServicePackMajorVersion,ServicePackMinorVersion
```

<span data-ttu-id="d742c-140">Můžete také použít zástupné znaky s `Select-Object`na **vlastnost** parametr.</span><span class="sxs-lookup"><span data-stu-id="d742c-140">You can also use wildcards with the `Select-Object`'s **Property** parameter.</span></span>
<span data-ttu-id="d742c-141">Protože všechny vlastnosti počínaje buď **sestavení** nebo **aktualizace Service Pack** jsou důležité pro použití Zde jsme zkrátit to pro následující tvar:</span><span class="sxs-lookup"><span data-stu-id="d742c-141">Because all the properties beginning with either **Build** or **ServicePack** are important to use here, we can shorten this to the following form:</span></span>

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property Build*,OSType,ServicePack*
```

```output
BuildNumber             : 16299
BuildType               : Multiprocessor Free
OSType                  : 18
ServicePackMajorVersion : 0
ServicePackMinorVersion : 0
```

### <a name="listing-local-users-and-owner"></a><span data-ttu-id="d742c-142">Výpis místní uživatelé a vlastníka</span><span class="sxs-lookup"><span data-stu-id="d742c-142">Listing Local Users and Owner</span></span>

<span data-ttu-id="d742c-143">Místní obecné informace o uživateli – počet oprávněných uživatelů, aktuální počet uživatelů a jméno vlastníka – lze najít pomocí výběr **Win32_OperatingSystem** vlastnosti třídy se.</span><span class="sxs-lookup"><span data-stu-id="d742c-143">Local general user information — number of licensed users, current number of users, and owner name — can be found with a selection of **Win32_OperatingSystem** class' properties.</span></span>
<span data-ttu-id="d742c-144">Můžete vybrat explicitně vlastnosti zobrazíte takto:</span><span class="sxs-lookup"><span data-stu-id="d742c-144">You can explicitly select the properties to display like this:</span></span>

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property NumberOfLicensedUsers,NumberOfUsers,RegisteredUser
```

<span data-ttu-id="d742c-145">Použití zástupných znaků více stručného verze je:</span><span class="sxs-lookup"><span data-stu-id="d742c-145">A more succinct version using wildcards is:</span></span>

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property *user*
```

### <a name="getting-available-disk-space"></a><span data-ttu-id="d742c-146">Získávání volného místa na disku</span><span class="sxs-lookup"><span data-stu-id="d742c-146">Getting Available Disk Space</span></span>

<span data-ttu-id="d742c-147">Pokud chcete zobrazit místa na disku a volné místo pro místní disky, můžete použít třídu služby WMI Win32_LogicalDisk.</span><span class="sxs-lookup"><span data-stu-id="d742c-147">To see the disk space and free space for local drives, you can use the Win32_LogicalDisk WMI class.</span></span>
<span data-ttu-id="d742c-148">Je třeba zobrazit pouze instance s DriveType 3 – hodnota WMI používá pro pevné disky.</span><span class="sxs-lookup"><span data-stu-id="d742c-148">You need to see only instances with a DriveType of 3 — the value WMI uses for fixed hard disks.</span></span>

```powershell
Get-CimInstance -ClassName Win32_LogicalDisk -Filter "DriveType=3" -ComputerName .

DeviceID DriveType ProviderName VolumeName Size         FreeSpace   PSComputerName
-------- --------- ------------ ---------- ----         ---------   --------------
C:       3                      Local Disk 203912880128 65541357568 .
Q:       3                      New Volume 122934034432 44298250240 .

Get-CimInstance -ClassName Win32_LogicalDisk -Filter "DriveType=3" -ComputerName . | Measure-Object -Property FreeSpace,Size -Sum | Select-Object -Property Property,Sum

Property           Sum
--------           ---
FreeSpace 109839607808
Size      326846914560
```

### <a name="getting-logon-session-information"></a><span data-ttu-id="d742c-149">Získávání informací o relaci přihlášení</span><span class="sxs-lookup"><span data-stu-id="d742c-149">Getting Logon Session Information</span></span>

<span data-ttu-id="d742c-150">Obecné informace o přidružená k uživatelům prostřednictvím relace přihlášení můžete získat **Win32_LogonSession** třídu služby WMI:</span><span class="sxs-lookup"><span data-stu-id="d742c-150">You can get general information about logon sessions associated with users through the **Win32_LogonSession** WMI class:</span></span>

```powershell
Get-CimInstance -ClassName Win32_LogonSession -ComputerName .
```

### <a name="getting-the-user-logged-on-to-a-computer"></a><span data-ttu-id="d742c-151">Získávání uživateli přihlášenému k počítači</span><span class="sxs-lookup"><span data-stu-id="d742c-151">Getting the User Logged on to a Computer</span></span>

<span data-ttu-id="d742c-152">Můžete zobrazit uživateli přihlášenému k určitému počítači systému pomocí Win32_ComputerSystem.</span><span class="sxs-lookup"><span data-stu-id="d742c-152">You can display the user logged on to a particular computer system using Win32_ComputerSystem.</span></span>
<span data-ttu-id="d742c-153">Tento příkaz vrátí jenom uživateli přihlášení k ploše systému:</span><span class="sxs-lookup"><span data-stu-id="d742c-153">This command returns only the user logged on to the system desktop:</span></span>

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -Property UserName -ComputerName .
```

### <a name="getting-local-time-from-a-computer"></a><span data-ttu-id="d742c-154">Získávání z počítače, na místní čas</span><span class="sxs-lookup"><span data-stu-id="d742c-154">Getting Local Time from a Computer</span></span>

<span data-ttu-id="d742c-155">Aktuální místní čas v určitém počítači můžete načíst pomocí **Win32_LocalTime** třídu služby WMI.</span><span class="sxs-lookup"><span data-stu-id="d742c-155">You can retrieve the current local time on a specific computer by using the **Win32_LocalTime** WMI class.</span></span>

```powershell
Get-CimInstance -ClassName Win32_LocalTime -ComputerName .

Day          : 15
DayOfWeek    : 4
Hour         : 12
Milliseconds :
Minute       : 11
Month        : 6
Quarter      : 2
Second       : 52
WeekInMonth  : 3
Year         : 2017
PSComputerName : .
```

### <a name="displaying-service-status"></a><span data-ttu-id="d742c-156">Zobrazení stavu služby</span><span class="sxs-lookup"><span data-stu-id="d742c-156">Displaying Service Status</span></span>

<span data-ttu-id="d742c-157">Chcete-li zobrazit stav všech služeb v určitém počítači, místně můžete `Get-Service` rutiny.</span><span class="sxs-lookup"><span data-stu-id="d742c-157">To view the status of all services on a specific computer, you can locally use the `Get-Service` cmdlet.</span></span>
<span data-ttu-id="d742c-158">Pro vzdálené systémy, můžete použít **Win32_Service** třídu služby WMI.</span><span class="sxs-lookup"><span data-stu-id="d742c-158">For remote systems, you can use the **Win32_Service** WMI class.</span></span>
<span data-ttu-id="d742c-159">Pokud používáte také `Select-Object` filtrování výsledků na **stav**, **název**, a **DisplayName**, formát výstupu bude skoro stejná jako z `Get-Service`:</span><span class="sxs-lookup"><span data-stu-id="d742c-159">If you also use `Select-Object` to filter the results to **Status**, **Name**, and **DisplayName**, the output format will be almost identical to that from `Get-Service`:</span></span>

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Select-Object -Property Status,Name,DisplayName
```

<span data-ttu-id="d742c-160">Pokud chcete povolit úplný zobrazovaný názvů pro příležitostně služby s velmi dlouhé názvy, můžete chtít použít `Format-Table` s **AutoSize** a **zabalení** parametry za účelem optimalizace šířka sloupce a Povolit dlouhé názvy zabalit místo ke zkrácení:</span><span class="sxs-lookup"><span data-stu-id="d742c-160">To allow the complete display of names for the occasional services with extremely long names, you may want to use `Format-Table` with the **AutoSize** and **Wrap** parameters, to optimize column width and allow long names to wrap instead of being truncated:</span></span>

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Format-Table -Property Status,Name,DisplayName -AutoSize -Wrap
```
