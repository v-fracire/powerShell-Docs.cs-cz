---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Získávání objekty rozhraní WMI získat WmiObject
ms.assetid: f0ddfc7d-6b5e-4832-82de-2283597ea70d
ms.openlocfilehash: 67922426ae3f13ef5f4c70bc70bb3ce1594d3d05
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="getting-wmi-objects-get-wmiobject"></a>Získávání objekty rozhraní WMI (Get-WmiObject)

## <a name="getting-wmi-objects-get-wmiobject"></a>Získávání objekty rozhraní WMI (Get-WmiObject)

Windows Management Instrumentation (WMI) je technologie jádra pro správu systému Windows, protože poskytuje celou řadu informací jednotným způsobem. Z důvodu Kolik rozhraní WMI je možné, rutiny prostředí Windows PowerShell pro přístup k rozhraní WMI objekty **Get-WmiObject**, je jedním z velmi užitečné pro skutečné pracuje. Přidáme popisují postup Get-WmiObject používat pro přístup k rozhraní WMI objekty a provádět konkrétní akce pomocí objektů služby WMI.

### <a name="listing-wmi-classes"></a>Seznam tříd WMI

První problém, ke které dojde k většina uživatelů rozhraní WMI se pokouší zjistit, co můžete udělat pomocí rozhraní WMI. Třídy služby WMI popisují prostředky, které je možné spravovat. Existují stovky tříd WMI, z nichž některé obsahují desítek vlastnosti.

**Get-WmiObject** tento problém řeší tím, že zjistitelný rozhraní WMI. Zadáním můžete získat seznam tříd WMI, která je k dispozici v místním počítači:

```
PS> Get-WmiObject -List

__SecurityRelatedClass                  __NTLMUser9X
__PARAMETERS                            __SystemSecurity
__NotifyStatus                          __ExtendedStatus
Win32_PrivilegesStatus                  Win32_TSNetworkAdapterSettingError
Win32_TSRemoteControlSettingError       Win32_TSEnvironmentSettingError
...
```

Stejné informace ze vzdáleného počítače můžete načíst pomocí parametrem ComputerName zadání názvu počítače nebo IP adresa:

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
__ProviderRegistration                  __ObjectProviderRegistration
...
```

Výpis třída vrácený vzdálené počítače nemusí být z důvodu konkrétní operační systém, který počítač běží a konkrétní rozšíření rozhraní WMI přidal nainstalovaných aplikací.

> [!NOTE]
> Při použití Get-WmiObject pro připojení ke vzdálenému počítači, vzdáleném počítači musí běžet rozhraní WMI, a v části výchozí konfigurace, musí být účet, který používáte v místní skupiny administrators na vzdáleném počítači. Vzdáleném systému není nutné mít nainstalované prostředí Windows PowerShell. To umožňuje spravovat operační systémy, které nejsou spuštěné prostředí Windows PowerShell, ale jsou k dispozici rozhraní WMI.

Hodnota vlastnosti ComputerName můžete zahrnout i při připojování k místní systém. Můžete použít název místního počítače, jeho IP adresu (nebo adresu zpětné smyčky 127.0.0.1), nebo rozhraní WMI-style '.' jako název počítače. Pokud používáte prostředí Windows PowerShell do počítače s názvem Admin01 s IP adresou 192.168.1.90, následující příkazy všechny vrátí třídu služby WMI výpis pro tento počítač:

```powershell
Get-WmiObject -List
Get-WmiObject -List -ComputerName .
Get-WmiObject -List -ComputerName Admin01
Get-WmiObject -List -ComputerName 192.168.1.90
Get-WmiObject -List -ComputerName 127.0.0.1
Get-WmiObject -List -ComputerName localhost
```

Get-WmiObject používá obor názvů root nebo cimv2 ve výchozím nastavení. Pokud chcete zadat jiný obor názvů rozhraní WMI, použijte **Namespace** parametr a zadejte odpovídající cestě k oboru názvů:

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29 -Namespace root

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
...
```

### <a name="displaying-wmi-class-details"></a>Zobrazení podrobností třídy služby WMI

Pokud znáte název třídy WMI, můžete získat informace o okamžitě. Je třeba jednu z tříd WMI běžně používá pro načtení informací o počítači **Win32_OperatingSystem**.

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName .

SystemDirectory : C:\WINDOWS\system32
Organization    : Global Network Solutions
BuildNumber     : 2600
RegisteredUser  : Oliver W. Jones
SerialNumber    : 12345-678-9012345-67890
Version         : 5.1.2600
```

I když jsme zobrazují všechny parametry, dají se vyjádřit příkaz více stručného způsobem. **ComputerName** parametr není třeba při připojování k místní systém. Ukážeme ho k předvedení nejobecnější případ a zobrazení upozornění na parametr. **Namespace** výchozí nastavení je kořenový/cimv2 a také lze vynechat. Většina rutiny navíc umožňují vypuštění názvu společných parametrů. S Get-WmiObject, pokud není zadán žádný název prvního parametru, prostředí Windows PowerShell považována za **třída** parametr. To znamená, že poslední příkaz může vystavené zadáním:

```powershell
Get-WmiObject Win32_OperatingSystem
```

**Win32_OperatingSystem** třída má mnohem více vlastností než ty, které zobrazí tady. Get-člen můžete zobrazit všechny vlastnosti. Vlastnosti třídy WMI jsou automaticky dostupné jako ostatní vlastnosti objektu:

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

#### <a name="displaying-non-default-properties-with-format-cmdlets"></a>Zobrazení vlastností jiné než výchozí s rutinami formátu

Pokud chcete informace obsažené v **Win32_OperatingSystem** třídy, který je nezobrazí ve výchozím nastavení, můžete ji zobrazit pomocí **formát** rutiny. Například pokud chcete zobrazit data dostupná paměť, zadejte:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-Table -Property TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize TotalVisibleMemory FreePhysicalMemory FreeVirtualMemory FreeSpaceInPagingFiles
---------------------- ---------------    ------------------ -==--------------------- ---------------
               2097024          785904                305808           2056724                1558232
```

> [!NOTE]
> Zástupné znaky pracovat s názvy vlastností v **Format-Table**, takže element konečné kanálu se může snížit na **Format-Table-celkový počet vlastnost*, volnou *

Data paměti může být lépe čitelný, pokud je formátovat jako seznam zadáním:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-List TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize : 2097024
TotalVisibleMemorySize : 785904
FreePhysicalMemory     : 301876
FreeVirtualMemory      : 2056724
FreeSpaceInPagingFiles : 1556644
```