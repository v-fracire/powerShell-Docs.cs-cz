---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Získávání objektů WMI získat WmiObject
ms.assetid: f0ddfc7d-6b5e-4832-82de-2283597ea70d
ms.openlocfilehash: 522822ac3ea6f08b20fa5af6c9accb48b01035d3
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403641"
---
# <a name="getting-wmi-objects-get-wmiobject"></a><span data-ttu-id="c54d7-103">Získávání objektů WMI (Get-WmiObject)</span><span class="sxs-lookup"><span data-stu-id="c54d7-103">Getting WMI Objects (Get-WmiObject)</span></span>

## <a name="getting-wmi-objects-get-wmiobject"></a><span data-ttu-id="c54d7-104">Získávání objektů WMI (Get-WmiObject)</span><span class="sxs-lookup"><span data-stu-id="c54d7-104">Getting WMI Objects (Get-WmiObject)</span></span>

<span data-ttu-id="c54d7-105">Windows Management Instrumentation (WMI) je základní technologie pro správu systému Windows, protože poskytuje širokou škálu informací jednotným způsobem.</span><span class="sxs-lookup"><span data-stu-id="c54d7-105">Windows Management Instrumentation (WMI) is a core technology for Windows system administration because it exposes a wide range of information in a uniform manner.</span></span> <span data-ttu-id="c54d7-106">Z důvodu kolik WMI umožňují, rutiny prostředí Windows PowerShell pro získání přístupu k objektům služby WMI **Get-WmiObject**, patří mezi nejužitečnější plnit skutečnou práci.</span><span class="sxs-lookup"><span data-stu-id="c54d7-106">Because of how much WMI makes possible, the Windows PowerShell cmdlet for accessing WMI objects, **Get-WmiObject**, is one of the most useful for doing real work.</span></span> <span data-ttu-id="c54d7-107">Budeme o tom, jak pomocí Get-WmiObject pro přístup k objektům rozhraní WMI a pak použití objektů WMI provádět konkrétní akce.</span><span class="sxs-lookup"><span data-stu-id="c54d7-107">We are going to discuss how to use Get-WmiObject to access WMI objects and then how to use WMI objects to do specific things.</span></span>

### <a name="listing-wmi-classes"></a><span data-ttu-id="c54d7-108">Třídy služby WMI pro výpis</span><span class="sxs-lookup"><span data-stu-id="c54d7-108">Listing WMI Classes</span></span>

<span data-ttu-id="c54d7-109">První problém, ke které dojde k většině uživatelů služby WMI se pokouší zjistit, co se dá dělat s rozhraním WMI.</span><span class="sxs-lookup"><span data-stu-id="c54d7-109">The first problem most WMI users encounter is trying to find out what can be done with WMI.</span></span> <span data-ttu-id="c54d7-110">Třídy služby WMI popisují prostředky, které je možné spravovat.</span><span class="sxs-lookup"><span data-stu-id="c54d7-110">WMI classes describe the resources that can be managed.</span></span> <span data-ttu-id="c54d7-111">Existují stovky třídy služby WMI, z nichž některé obsahovat desítky vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="c54d7-111">There are hundreds of WMI classes, some of which contain dozens of properties.</span></span>

<span data-ttu-id="c54d7-112">**Get-WmiObject** tento problém řeší tím, že WMI zjistitelné.</span><span class="sxs-lookup"><span data-stu-id="c54d7-112">**Get-WmiObject** addresses this problem by making WMI discoverable.</span></span> <span data-ttu-id="c54d7-113">Seznam tříd WMI, která je k dispozici v místním počítači můžete získat tak, že zadáte:</span><span class="sxs-lookup"><span data-stu-id="c54d7-113">You can get a list of the WMI classes available on the local computer by typing:</span></span>

```
PS> Get-WmiObject -List

__SecurityRelatedClass                  __NTLMUser9X
__PARAMETERS                            __SystemSecurity
__NotifyStatus                          __ExtendedStatus
Win32_PrivilegesStatus                  Win32_TSNetworkAdapterSettingError
Win32_TSRemoteControlSettingError       Win32_TSEnvironmentSettingError
...
```

<span data-ttu-id="c54d7-114">Stejné informace ze vzdáleného počítače můžete načíst pomocí parametru ComputerName zadání názvu počítače nebo IP adresa:</span><span class="sxs-lookup"><span data-stu-id="c54d7-114">You can retrieve the same information from a remote computer by using the ComputerName parameter, specifying a computer name or IP address:</span></span>

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
__ProviderRegistration                  __ObjectProviderRegistration
...
```

<span data-ttu-id="c54d7-115">Třída výpis vrácený vzdálených počítačů se můžou lišit kvůli konkrétní operační systém, který je spuštěna a konkrétní rozšíření služby WMI přidal nainstalovaných aplikací.</span><span class="sxs-lookup"><span data-stu-id="c54d7-115">The class listing returned by remote computers may vary due to the specific operating system the computer is running and the particular WMI extensions added by installed applications.</span></span>

> [!NOTE]
> <span data-ttu-id="c54d7-116">Při použití Get-WmiObject k připojení ke vzdálenému počítači, vzdáleném počítači musí běžet rozhraní WMI a pod výchozí konfiguraci, musí být účet, který používáte ve skupině místních správců na vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="c54d7-116">When using Get-WmiObject to connect to a remote computer, the remote computer must be running WMI and, under the default configuration, the account you are using must be in the local administrators group on the remote computer.</span></span> <span data-ttu-id="c54d7-117">Vzdálený systém není potřeba mít Windows PowerShell nainstalovaný.</span><span class="sxs-lookup"><span data-stu-id="c54d7-117">The remote system does not need to have Windows PowerShell installed.</span></span> <span data-ttu-id="c54d7-118">To umožňuje spravovat operační systémy, které nejsou spuštěné prostředí Windows PowerShell, ale mají k dispozici rozhraní WMI.</span><span class="sxs-lookup"><span data-stu-id="c54d7-118">This allows you to administer operating systems that are not running Windows PowerShell, but do have WMI available.</span></span>

<span data-ttu-id="c54d7-119">Hodnota vlastnosti ComputerName můžete zahrnout i při připojování k místní systém.</span><span class="sxs-lookup"><span data-stu-id="c54d7-119">You can even include the ComputerName when connecting to the local system.</span></span> <span data-ttu-id="c54d7-120">Můžete použít název místního počítače, jeho IP adresy (nebo na adresu zpětné smyčky 127.0.0.1), nebo rozhraní WMI-style '.' jako název počítače.</span><span class="sxs-lookup"><span data-stu-id="c54d7-120">You can use the local computer's name, its IP address (or the loopback address 127.0.0.1), or the WMI-style '.' as the computer name.</span></span> <span data-ttu-id="c54d7-121">Pokud používáte prostředí Windows PowerShell do počítače s názvem Admin01 s IP adresou 192.168.1.90, následující příkazy všechny vrátí třídu služby WMI pro tento počítač:</span><span class="sxs-lookup"><span data-stu-id="c54d7-121">If you are running Windows PowerShell on a computer named Admin01 with IP address 192.168.1.90, the following commands will all return the WMI class listing for that computer:</span></span>

```powershell
Get-WmiObject -List
Get-WmiObject -List -ComputerName .
Get-WmiObject -List -ComputerName Admin01
Get-WmiObject -List -ComputerName 192.168.1.90
Get-WmiObject -List -ComputerName 127.0.0.1
Get-WmiObject -List -ComputerName localhost
```

<span data-ttu-id="c54d7-122">Get-WmiObject používá obor názvů root/cimv2 ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="c54d7-122">Get-WmiObject uses the root/cimv2 namespace by default.</span></span> <span data-ttu-id="c54d7-123">Pokud chcete zadat jiný obor názvů rozhraní WMI, použijte **Namespace** parametr a zadejte odpovídající cestě k oboru názvů:</span><span class="sxs-lookup"><span data-stu-id="c54d7-123">If you want to specify another WMI namespace, use the **Namespace** parameter and specify the corresponding namespace path:</span></span>

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29 -Namespace root

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
...
```

### <a name="displaying-wmi-class-details"></a><span data-ttu-id="c54d7-124">Zobrazení podrobností třídy služby WMI</span><span class="sxs-lookup"><span data-stu-id="c54d7-124">Displaying WMI Class Details</span></span>

<span data-ttu-id="c54d7-125">Pokud již znáte název třídy služby WMI, můžete získat informace o okamžitě.</span><span class="sxs-lookup"><span data-stu-id="c54d7-125">If you already know the name of a WMI class, you can use it to get information immediately.</span></span> <span data-ttu-id="c54d7-126">Je třeba jeden z třídy služby WMI pro načtení informací o počítači běžně používá **Win32_OperatingSystem**.</span><span class="sxs-lookup"><span data-stu-id="c54d7-126">For example, one of the WMI classes commonly used for retrieving information about a computer is **Win32_OperatingSystem**.</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName .

SystemDirectory : C:\WINDOWS\system32
Organization    : Global Network Solutions
BuildNumber     : 2600
RegisteredUser  : Oliver W. Jones
SerialNumber    : 12345-678-9012345-67890
Version         : 5.1.2600
```

<span data-ttu-id="c54d7-127">I když jsme se zobrazují všechny parametry, tento příkaz lze vyjádřit stručnější způsobem.</span><span class="sxs-lookup"><span data-stu-id="c54d7-127">Although we are showing all of the parameters, the command can be expressed in a more succinct way.</span></span> <span data-ttu-id="c54d7-128">**ComputerName** parametr není nezbytné, při připojování k místní systém.</span><span class="sxs-lookup"><span data-stu-id="c54d7-128">The **ComputerName** parameter is not necessary when connecting to the local system.</span></span> <span data-ttu-id="c54d7-129">Ukážeme ukazují nejobecnější případ a upozorňovat na parametr.</span><span class="sxs-lookup"><span data-stu-id="c54d7-129">We show it to demonstrate the most general case and remind you about the parameter.</span></span> <span data-ttu-id="c54d7-130">**Namespace** výchozí hodnota je root/cimv2 a také lze vynechat.</span><span class="sxs-lookup"><span data-stu-id="c54d7-130">The **Namespace** defaults to root/cimv2, and can be omitted as well.</span></span> <span data-ttu-id="c54d7-131">A konečně většina rutin umožňují vynechat název společných parametrů.</span><span class="sxs-lookup"><span data-stu-id="c54d7-131">Finally, most cmdlets allow you to omit the name of common parameters.</span></span> <span data-ttu-id="c54d7-132">Pomocí Get-WmiObject, pokud není zadán žádný název pro první parametr, prostředí Windows PowerShell zpracovává **třídy** parametru.</span><span class="sxs-lookup"><span data-stu-id="c54d7-132">With Get-WmiObject, if no name is specified for the first parameter, Windows PowerShell treats it as the **Class** parameter.</span></span> <span data-ttu-id="c54d7-133">To znamená, že poslední příkaz by byl vydán zadáním:</span><span class="sxs-lookup"><span data-stu-id="c54d7-133">This means the last command could have been issued by typing:</span></span>

```powershell
Get-WmiObject Win32_OperatingSystem
```

<span data-ttu-id="c54d7-134">**Win32_OperatingSystem** třída má mnohem více vlastností než ty, které tady zobrazí.</span><span class="sxs-lookup"><span data-stu-id="c54d7-134">The **Win32_OperatingSystem** class has many more properties than those displayed here.</span></span> <span data-ttu-id="c54d7-135">Get-Member můžete zobrazit všechny vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="c54d7-135">You can use Get-Member to see all the properties.</span></span> <span data-ttu-id="c54d7-136">Vlastnosti třídy WMI jsou automaticky dostupné jako ostatní vlastnosti objektu:</span><span class="sxs-lookup"><span data-stu-id="c54d7-136">The properties of a WMI class are automatically available like other object properties:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Get-Member -MemberType Property

   TypeName: System.Management.ManagementObject#root\cimv2\Win32_OperatingSyste
m

Name                                      MemberType Definition
----                                      ---------- ----------
__CLASS                                   Property   System.String __CLASS {...
...
BootDevice                                Property   System.String BootDevic...
BuildNumber                               Property   System.String BuildNumb...
...
```

#### <a name="displaying-non-default-properties-with-format-cmdlets"></a><span data-ttu-id="c54d7-137">Zobrazení vlastností jiné než výchozí s rutinami formátu</span><span class="sxs-lookup"><span data-stu-id="c54d7-137">Displaying Non-Default Properties with Format Cmdlets</span></span>

<span data-ttu-id="c54d7-138">Pokud chcete informace obsažené v **Win32_OperatingSystem** třídy, který je ve výchozím nastavení se nezobrazuje, můžete ho zobrazit pomocí **formátu** rutiny.</span><span class="sxs-lookup"><span data-stu-id="c54d7-138">If you want information contained in the **Win32_OperatingSystem** class that is not displayed by default, you can display it by using the **Format** cmdlets.</span></span> <span data-ttu-id="c54d7-139">Pokud chcete zobrazit data dostupná paměť, zadejte například:</span><span class="sxs-lookup"><span data-stu-id="c54d7-139">For example, if you want to display available memory data, type:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-Table -Property TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize TotalVisibleMemory FreePhysicalMemory FreeVirtualMemory FreeSpaceInPagingFiles
---------------------- ---------------    ------------------ -==--------------------- ---------------
               2097024          785904                305808           2056724                1558232
```

> [!NOTE]
> <span data-ttu-id="c54d7-140">Zástupné znaky pracovat s názvy vlastností v **Format-Table**, takže konečný kanálu element může být snížena na `Format-Table -Property Total,Free`</span><span class="sxs-lookup"><span data-stu-id="c54d7-140">Wildcards work with property names in **Format-Table**, so the final pipeline element can be reduced to `Format-Table -Property Total,Free`</span></span>

<span data-ttu-id="c54d7-141">Data paměti může být lépe čitelný, pokud je formátovat jako seznam tak, že zadáte:</span><span class="sxs-lookup"><span data-stu-id="c54d7-141">The memory data might be more readable if you format it as a list by typing:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-List TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize : 2097024
TotalVisibleMemorySize : 785904
FreePhysicalMemory     : 301876
FreeVirtualMemory      : 2056724
FreeSpaceInPagingFiles : 1556644
```
