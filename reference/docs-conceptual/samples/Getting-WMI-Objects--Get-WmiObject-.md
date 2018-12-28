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
# <a name="getting-wmi-objects-get-wmiobject"></a>Získávání objektů WMI (Get-WmiObject)

## <a name="getting-wmi-objects-get-wmiobject"></a>Získávání objektů WMI (Get-WmiObject)

Windows Management Instrumentation (WMI) je základní technologie pro správu systému Windows, protože poskytuje širokou škálu informací jednotným způsobem. Z důvodu kolik WMI umožňují, rutiny prostředí Windows PowerShell pro získání přístupu k objektům služby WMI **Get-WmiObject**, patří mezi nejužitečnější plnit skutečnou práci. Budeme o tom, jak pomocí Get-WmiObject pro přístup k objektům rozhraní WMI a pak použití objektů WMI provádět konkrétní akce.

### <a name="listing-wmi-classes"></a>Třídy služby WMI pro výpis

První problém, ke které dojde k většině uživatelů služby WMI se pokouší zjistit, co se dá dělat s rozhraním WMI. Třídy služby WMI popisují prostředky, které je možné spravovat. Existují stovky třídy služby WMI, z nichž některé obsahovat desítky vlastnosti.

**Get-WmiObject** tento problém řeší tím, že WMI zjistitelné. Seznam tříd WMI, která je k dispozici v místním počítači můžete získat tak, že zadáte:

```
PS> Get-WmiObject -List

__SecurityRelatedClass                  __NTLMUser9X
__PARAMETERS                            __SystemSecurity
__NotifyStatus                          __ExtendedStatus
Win32_PrivilegesStatus                  Win32_TSNetworkAdapterSettingError
Win32_TSRemoteControlSettingError       Win32_TSEnvironmentSettingError
...
```

Stejné informace ze vzdáleného počítače můžete načíst pomocí parametru ComputerName zadání názvu počítače nebo IP adresa:

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
__ProviderRegistration                  __ObjectProviderRegistration
...
```

Třída výpis vrácený vzdálených počítačů se můžou lišit kvůli konkrétní operační systém, který je spuštěna a konkrétní rozšíření služby WMI přidal nainstalovaných aplikací.

> [!NOTE]
> Při použití Get-WmiObject k připojení ke vzdálenému počítači, vzdáleném počítači musí běžet rozhraní WMI a pod výchozí konfiguraci, musí být účet, který používáte ve skupině místních správců na vzdáleném počítači. Vzdálený systém není potřeba mít Windows PowerShell nainstalovaný. To umožňuje spravovat operační systémy, které nejsou spuštěné prostředí Windows PowerShell, ale mají k dispozici rozhraní WMI.

Hodnota vlastnosti ComputerName můžete zahrnout i při připojování k místní systém. Můžete použít název místního počítače, jeho IP adresy (nebo na adresu zpětné smyčky 127.0.0.1), nebo rozhraní WMI-style '.' jako název počítače. Pokud používáte prostředí Windows PowerShell do počítače s názvem Admin01 s IP adresou 192.168.1.90, následující příkazy všechny vrátí třídu služby WMI pro tento počítač:

```powershell
Get-WmiObject -List
Get-WmiObject -List -ComputerName .
Get-WmiObject -List -ComputerName Admin01
Get-WmiObject -List -ComputerName 192.168.1.90
Get-WmiObject -List -ComputerName 127.0.0.1
Get-WmiObject -List -ComputerName localhost
```

Get-WmiObject používá obor názvů root/cimv2 ve výchozím nastavení. Pokud chcete zadat jiný obor názvů rozhraní WMI, použijte **Namespace** parametr a zadejte odpovídající cestě k oboru názvů:

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29 -Namespace root

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
...
```

### <a name="displaying-wmi-class-details"></a>Zobrazení podrobností třídy služby WMI

Pokud již znáte název třídy služby WMI, můžete získat informace o okamžitě. Je třeba jeden z třídy služby WMI pro načtení informací o počítači běžně používá **Win32_OperatingSystem**.

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName .

SystemDirectory : C:\WINDOWS\system32
Organization    : Global Network Solutions
BuildNumber     : 2600
RegisteredUser  : Oliver W. Jones
SerialNumber    : 12345-678-9012345-67890
Version         : 5.1.2600
```

I když jsme se zobrazují všechny parametry, tento příkaz lze vyjádřit stručnější způsobem. **ComputerName** parametr není nezbytné, při připojování k místní systém. Ukážeme ukazují nejobecnější případ a upozorňovat na parametr. **Namespace** výchozí hodnota je root/cimv2 a také lze vynechat. A konečně většina rutin umožňují vynechat název společných parametrů. Pomocí Get-WmiObject, pokud není zadán žádný název pro první parametr, prostředí Windows PowerShell zpracovává **třídy** parametru. To znamená, že poslední příkaz by byl vydán zadáním:

```powershell
Get-WmiObject Win32_OperatingSystem
```

**Win32_OperatingSystem** třída má mnohem více vlastností než ty, které tady zobrazí. Get-Member můžete zobrazit všechny vlastnosti. Vlastnosti třídy WMI jsou automaticky dostupné jako ostatní vlastnosti objektu:

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

Pokud chcete informace obsažené v **Win32_OperatingSystem** třídy, který je ve výchozím nastavení se nezobrazuje, můžete ho zobrazit pomocí **formátu** rutiny. Pokud chcete zobrazit data dostupná paměť, zadejte například:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-Table -Property TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize TotalVisibleMemory FreePhysicalMemory FreeVirtualMemory FreeSpaceInPagingFiles
---------------------- ---------------    ------------------ -==--------------------- ---------------
               2097024          785904                305808           2056724                1558232
```

> [!NOTE]
> Zástupné znaky pracovat s názvy vlastností v **Format-Table**, takže konečný kanálu element může být snížena na `Format-Table -Property Total,Free`

Data paměti může být lépe čitelný, pokud je formátovat jako seznam tak, že zadáte:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-List TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize : 2097024
TotalVisibleMemorySize : 785904
FreePhysicalMemory     : 301876
FreeVirtualMemory      : 2056724
FreeSpaceInPagingFiles : 1556644
```
