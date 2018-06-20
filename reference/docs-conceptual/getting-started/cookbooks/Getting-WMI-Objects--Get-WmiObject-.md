---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Získávání objekty rozhraní WMI získat WmiObject
ms.assetid: f0ddfc7d-6b5e-4832-82de-2283597ea70d
ms.openlocfilehash: 279e656b4affd27450be71015a5d6bd21af9f7ad
ms.sourcegitcommit: a9aa5e8d0fab0cbb3e4e6cff0e3ca8c0339ab4e6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/27/2018
ms.locfileid: "32018055"
---
# <a name="getting-wmi-objects-get-wmiobject"></a><span data-ttu-id="64858-103">Získávání objekty rozhraní WMI (Get-WmiObject)</span><span class="sxs-lookup"><span data-stu-id="64858-103">Getting WMI Objects (Get-WmiObject)</span></span>

## <a name="getting-wmi-objects-get-wmiobject"></a><span data-ttu-id="64858-104">Získávání objekty rozhraní WMI (Get-WmiObject)</span><span class="sxs-lookup"><span data-stu-id="64858-104">Getting WMI Objects (Get-WmiObject)</span></span>

<span data-ttu-id="64858-105">Windows Management Instrumentation (WMI) je technologie jádra pro správu systému Windows, protože poskytuje celou řadu informací jednotným způsobem.</span><span class="sxs-lookup"><span data-stu-id="64858-105">Windows Management Instrumentation (WMI) is a core technology for Windows system administration because it exposes a wide range of information in a uniform manner.</span></span> <span data-ttu-id="64858-106">Z důvodu Kolik rozhraní WMI je možné, rutiny prostředí Windows PowerShell pro přístup k rozhraní WMI objekty **Get-WmiObject**, je jedním z velmi užitečné pro skutečné pracuje.</span><span class="sxs-lookup"><span data-stu-id="64858-106">Because of how much WMI makes possible, the Windows PowerShell cmdlet for accessing WMI objects, **Get-WmiObject**, is one of the most useful for doing real work.</span></span> <span data-ttu-id="64858-107">Přidáme popisují postup Get-WmiObject používat pro přístup k rozhraní WMI objekty a provádět konkrétní akce pomocí objektů služby WMI.</span><span class="sxs-lookup"><span data-stu-id="64858-107">We are going to discuss how to use Get-WmiObject to access WMI objects and then how to use WMI objects to do specific things.</span></span>

### <a name="listing-wmi-classes"></a><span data-ttu-id="64858-108">Seznam tříd WMI</span><span class="sxs-lookup"><span data-stu-id="64858-108">Listing WMI Classes</span></span>

<span data-ttu-id="64858-109">První problém, ke které dojde k většina uživatelů rozhraní WMI se pokouší zjistit, co můžete udělat pomocí rozhraní WMI.</span><span class="sxs-lookup"><span data-stu-id="64858-109">The first problem most WMI users encounter is trying to find out what can be done with WMI.</span></span> <span data-ttu-id="64858-110">Třídy služby WMI popisují prostředky, které je možné spravovat.</span><span class="sxs-lookup"><span data-stu-id="64858-110">WMI classes describe the resources that can be managed.</span></span> <span data-ttu-id="64858-111">Existují stovky tříd WMI, z nichž některé obsahují desítek vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="64858-111">There are hundreds of WMI classes, some of which contain dozens of properties.</span></span>

<span data-ttu-id="64858-112">**Get-WmiObject** tento problém řeší tím, že zjistitelný rozhraní WMI.</span><span class="sxs-lookup"><span data-stu-id="64858-112">**Get-WmiObject** addresses this problem by making WMI discoverable.</span></span> <span data-ttu-id="64858-113">Zadáním můžete získat seznam tříd WMI, která je k dispozici v místním počítači:</span><span class="sxs-lookup"><span data-stu-id="64858-113">You can get a list of the WMI classes available on the local computer by typing:</span></span>

```
PS> Get-WmiObject -List

__SecurityRelatedClass                  __NTLMUser9X
__PARAMETERS                            __SystemSecurity
__NotifyStatus                          __ExtendedStatus
Win32_PrivilegesStatus                  Win32_TSNetworkAdapterSettingError
Win32_TSRemoteControlSettingError       Win32_TSEnvironmentSettingError
...
```

<span data-ttu-id="64858-114">Stejné informace ze vzdáleného počítače můžete načíst pomocí parametrem ComputerName zadání názvu počítače nebo IP adresa:</span><span class="sxs-lookup"><span data-stu-id="64858-114">You can retrieve the same information from a remote computer by using the ComputerName parameter, specifying a computer name or IP address:</span></span>

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
__ProviderRegistration                  __ObjectProviderRegistration
...
```

<span data-ttu-id="64858-115">Výpis třída vrácený vzdálené počítače nemusí být z důvodu konkrétní operační systém, který počítač běží a konkrétní rozšíření rozhraní WMI přidal nainstalovaných aplikací.</span><span class="sxs-lookup"><span data-stu-id="64858-115">The class listing returned by remote computers may vary due to the specific operating system the computer is running and the particular WMI extensions added by installed applications.</span></span>

> [!NOTE]
> <span data-ttu-id="64858-116">Při použití Get-WmiObject pro připojení ke vzdálenému počítači, vzdáleném počítači musí běžet rozhraní WMI, a v části výchozí konfigurace, musí být účet, který používáte v místní skupiny administrators na vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="64858-116">When using Get-WmiObject to connect to a remote computer, the remote computer must be running WMI and, under the default configuration, the account you are using must be in the local administrators group on the remote computer.</span></span> <span data-ttu-id="64858-117">Vzdáleném systému není nutné mít nainstalované prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64858-117">The remote system does not need to have Windows PowerShell installed.</span></span> <span data-ttu-id="64858-118">To umožňuje spravovat operační systémy, které nejsou spuštěné prostředí Windows PowerShell, ale jsou k dispozici rozhraní WMI.</span><span class="sxs-lookup"><span data-stu-id="64858-118">This allows you to administer operating systems that are not running Windows PowerShell, but do have WMI available.</span></span>

<span data-ttu-id="64858-119">Hodnota vlastnosti ComputerName můžete zahrnout i při připojování k místní systém.</span><span class="sxs-lookup"><span data-stu-id="64858-119">You can even include the ComputerName when connecting to the local system.</span></span> <span data-ttu-id="64858-120">Můžete použít název místního počítače, jeho IP adresu (nebo adresu zpětné smyčky 127.0.0.1), nebo rozhraní WMI-style '.' jako název počítače.</span><span class="sxs-lookup"><span data-stu-id="64858-120">You can use the local computer's name, its IP address (or the loopback address 127.0.0.1), or the WMI-style '.' as the computer name.</span></span> <span data-ttu-id="64858-121">Pokud používáte prostředí Windows PowerShell do počítače s názvem Admin01 s IP adresou 192.168.1.90, následující příkazy všechny vrátí třídu služby WMI výpis pro tento počítač:</span><span class="sxs-lookup"><span data-stu-id="64858-121">If you are running Windows PowerShell on a computer named Admin01 with IP address 192.168.1.90, the following commands will all return the WMI class listing for that computer:</span></span>

```powershell
Get-WmiObject -List
Get-WmiObject -List -ComputerName .
Get-WmiObject -List -ComputerName Admin01
Get-WmiObject -List -ComputerName 192.168.1.90
Get-WmiObject -List -ComputerName 127.0.0.1
Get-WmiObject -List -ComputerName localhost
```

<span data-ttu-id="64858-122">Get-WmiObject používá obor názvů root nebo cimv2 ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="64858-122">Get-WmiObject uses the root/cimv2 namespace by default.</span></span> <span data-ttu-id="64858-123">Pokud chcete zadat jiný obor názvů rozhraní WMI, použijte **Namespace** parametr a zadejte odpovídající cestě k oboru názvů:</span><span class="sxs-lookup"><span data-stu-id="64858-123">If you want to specify another WMI namespace, use the **Namespace** parameter and specify the corresponding namespace path:</span></span>

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29 -Namespace root

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
...
```

### <a name="displaying-wmi-class-details"></a><span data-ttu-id="64858-124">Zobrazení podrobností třídy služby WMI</span><span class="sxs-lookup"><span data-stu-id="64858-124">Displaying WMI Class Details</span></span>

<span data-ttu-id="64858-125">Pokud znáte název třídy WMI, můžete získat informace o okamžitě.</span><span class="sxs-lookup"><span data-stu-id="64858-125">If you already know the name of a WMI class, you can use it to get information immediately.</span></span> <span data-ttu-id="64858-126">Je třeba jednu z tříd WMI běžně používá pro načtení informací o počítači **Win32_OperatingSystem**.</span><span class="sxs-lookup"><span data-stu-id="64858-126">For example, one of the WMI classes commonly used for retrieving information about a computer is **Win32_OperatingSystem**.</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName .

SystemDirectory : C:\WINDOWS\system32
Organization    : Global Network Solutions
BuildNumber     : 2600
RegisteredUser  : Oliver W. Jones
SerialNumber    : 12345-678-9012345-67890
Version         : 5.1.2600
```

<span data-ttu-id="64858-127">I když jsme zobrazují všechny parametry, dají se vyjádřit příkaz více stručného způsobem.</span><span class="sxs-lookup"><span data-stu-id="64858-127">Although we are showing all of the parameters, the command can be expressed in a more succinct way.</span></span> <span data-ttu-id="64858-128">**ComputerName** parametr není třeba při připojování k místní systém.</span><span class="sxs-lookup"><span data-stu-id="64858-128">The **ComputerName** parameter is not necessary when connecting to the local system.</span></span> <span data-ttu-id="64858-129">Ukážeme ho k předvedení nejobecnější případ a zobrazení upozornění na parametr.</span><span class="sxs-lookup"><span data-stu-id="64858-129">We show it to demonstrate the most general case and remind you about the parameter.</span></span> <span data-ttu-id="64858-130">**Namespace** výchozí nastavení je kořenový/cimv2 a také lze vynechat.</span><span class="sxs-lookup"><span data-stu-id="64858-130">The **Namespace** defaults to root/cimv2, and can be omitted as well.</span></span> <span data-ttu-id="64858-131">Většina rutiny navíc umožňují vypuštění názvu společných parametrů.</span><span class="sxs-lookup"><span data-stu-id="64858-131">Finally, most cmdlets allow you to omit the name of common parameters.</span></span> <span data-ttu-id="64858-132">S Get-WmiObject, pokud není zadán žádný název prvního parametru, prostředí Windows PowerShell považována za **třída** parametr.</span><span class="sxs-lookup"><span data-stu-id="64858-132">With Get-WmiObject, if no name is specified for the first parameter, Windows PowerShell treats it as the **Class** parameter.</span></span> <span data-ttu-id="64858-133">To znamená, že poslední příkaz může vystavené zadáním:</span><span class="sxs-lookup"><span data-stu-id="64858-133">This means the last command could have been issued by typing:</span></span>

```powershell
Get-WmiObject Win32_OperatingSystem
```

<span data-ttu-id="64858-134">**Win32_OperatingSystem** třída má mnohem více vlastností než ty, které zobrazí tady.</span><span class="sxs-lookup"><span data-stu-id="64858-134">The **Win32_OperatingSystem** class has many more properties than those displayed here.</span></span> <span data-ttu-id="64858-135">Get-člen můžete zobrazit všechny vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="64858-135">You can use Get-Member to see all the properties.</span></span> <span data-ttu-id="64858-136">Vlastnosti třídy WMI jsou automaticky dostupné jako ostatní vlastnosti objektu:</span><span class="sxs-lookup"><span data-stu-id="64858-136">The properties of a WMI class are automatically available like other object properties:</span></span>

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

#### <a name="displaying-non-default-properties-with-format-cmdlets"></a><span data-ttu-id="64858-137">Zobrazení vlastností jiné než výchozí s rutinami formátu</span><span class="sxs-lookup"><span data-stu-id="64858-137">Displaying Non-Default Properties with Format Cmdlets</span></span>

<span data-ttu-id="64858-138">Pokud chcete informace obsažené v **Win32_OperatingSystem** třídy, který je nezobrazí ve výchozím nastavení, můžete ji zobrazit pomocí **formát** rutiny.</span><span class="sxs-lookup"><span data-stu-id="64858-138">If you want information contained in the **Win32_OperatingSystem** class that is not displayed by default, you can display it by using the **Format** cmdlets.</span></span> <span data-ttu-id="64858-139">Například pokud chcete zobrazit data dostupná paměť, zadejte:</span><span class="sxs-lookup"><span data-stu-id="64858-139">For example, if you want to display available memory data, type:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-Table -Property TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize TotalVisibleMemory FreePhysicalMemory FreeVirtualMemory FreeSpaceInPagingFiles
---------------------- ---------------    ------------------ -==--------------------- ---------------
               2097024          785904                305808           2056724                1558232
```

> [!NOTE]
> <span data-ttu-id="64858-140">Zástupné znaky pracovat s názvy vlastností v **Format-Table**, takže element konečné kanálu se může snížit na `Format-Table -Property Total,Free`</span><span class="sxs-lookup"><span data-stu-id="64858-140">Wildcards work with property names in **Format-Table**, so the final pipeline element can be reduced to `Format-Table -Property Total,Free`</span></span>

<span data-ttu-id="64858-141">Data paměti může být lépe čitelný, pokud je formátovat jako seznam zadáním:</span><span class="sxs-lookup"><span data-stu-id="64858-141">The memory data might be more readable if you format it as a list by typing:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-List TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize : 2097024
TotalVisibleMemorySize : 785904
FreePhysicalMemory     : 301876
FreeVirtualMemory      : 2056724
FreeSpaceInPagingFiles : 1556644
```
