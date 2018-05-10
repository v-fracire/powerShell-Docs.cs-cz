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
# <a name="collecting-information-about-computers"></a>Shromažďování informací o počítačích

Rutiny z **CimCmdlets** modulu jsou nejdůležitější rutiny pro úlohy správy obecného systému.
Všechna nastavení kritické subsystém se zveřejňují přes rozhraní WMI.
Kromě toho WMI data jsou považovány za objekty, které jsou v kolekcích jednu nebo více položek.
Protože prostředí Windows PowerShell taky pracuje s objekty a má kanál, který vám umožní zacházet s jednoho nebo více objektů stejným způsobem, obecný přístup WMI umožňuje provádět některé pokročilé úlohy s uživatele příliš mnoho zásahů.

Následující příklady ukazují, jak shromažďovat konkrétní informace pomocí `Get-CimInstance` libovolný počítač.
Určíme **ComputerName** parametr s hodnotou tečkou (**.**), který představuje místní počítač.
Můžete zadat název nebo IP adresu přidruženou libovolného počítače, které lze získat přístup pomocí rozhraní WMI.
Pokud chcete načíst informace o místním počítači, může vynechat **ComputerName** parametr.

### <a name="listing-desktop-settings"></a>Výpis nastavení plochy

Začneme příkaz, který shromažďuje informace o stolní počítače v místním počítači.

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName .
```

Tento příkaz vrátí informace pro všechny pracovní plochy, zda jsou právě používány, nebo ne.

> [!NOTE]
> Informace o vrácené některé třídy WMI může být velmi podrobné a často obsahují metadata o třídu služby WMI.
Protože většina těchto metadat vlastností názvy, které začínají **Cim**, můžete filtrovat pomocí vlastností `Select-Object`.
Zadejte **- ExcludeProperty** parametr s "Cim *" jako hodnotu.
Příklad:

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

Filtrovat metadata, použijte operátor kanálu (|) k odeslání výsledky `Get-CimInstance` příkaz `Select-Object -ExcludeProperty "CIM*"`.

### <a name="listing-bios-information"></a>Výpis informace o systému BIOS

Služba WMI **Win32_BIOS** třída vrátí poměrně compact a úplné informace o systému BIOS v místním počítači:

```powershell
Get-CimInstance -ClassName Win32_BIOS -ComputerName .
```

### <a name="listing-processor-information"></a>Výpis informace o procesoru

Informace o obecné procesoru můžete načíst pomocí rozhraní WMI na **Win32_Processor** třídy, i když budete pravděpodobně chtít filtrování informací:

```powershell
Get-CimInstance -ClassName Win32_Processor -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

Obecný popis řetězce třídu procesoru, může jen vrátit **typ SystemType** vlastnost:

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -ComputerName . | Select-Object -Property SystemType

SystemType
----------
X86-based PC
```

### <a name="listing-computer-manufacturer-and-model"></a>Výpis Model a výrobce počítače

Informace o modelu počítače je také dostupná z **Win32_ComputerSystem**.
Ve standardním výstupu zobrazeného nebudete potřebovat jakéhokoli filtrování poskytující OEM data:

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem
```

```output
Name PrimaryOwnerName Domain    TotalPhysicalMemory Model                   Manufacturer
---- ---------------- ------    ------------------- -----                   ------------
MyPC Jane Doe         WORKGROUP 804765696           DA243A-ABA 6415cl NA910 Compaq Presario 06
```

Výstup z příkazy jako to, které vrací informace přímo z některé hardwaru, je pouze jako vhodný jako data, která máte.
Některé informace není správně nakonfigurováno podle výrobců hardwaru a proto pravděpodobně není k dispozici.

### <a name="listing-installed-hotfixes"></a>Výpis nainstalovaných oprav hotfix

Můžete vytvořit seznam všech nainstalovaných oprav hotfix s použitím **Win32_QuickFixEngineering**:

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName .
```

Tato třída vrátí seznam oprav hotfix, které vypadá takto:

```output
Source Description     HotFixID  InstalledBy   InstalledOn PSComputerName
------ -----------     --------  -----------   ----------- --------------
       Security Update KB4048951 Administrator 12/16/2017  .
```

Pro více stručného výstup můžete chtít vyloučit některé vlastnosti.
Přestože je možné použít `Get-CimInstance`na **vlastnost** parametr zvolit pouze **HotFixID**, to tak, budou vracet další informace, protože je ve výchozím nastavení zobrazí všechna metadata:

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

Vrátí další data, protože parametr vlastností v `Get-CimInstance` omezuje vlastnosti vrácená z instancí třídy služby WMI, není objekt byl vrácen do prostředí Windows PowerShell.
Chcete-li snížit výstup, použijte `Select-Object`:

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName . -Property HotFixId | Select-Object -Property HotFixId
```

```output
HotFixId
--------
KB4048951
```

### <a name="listing-operating-system-version-information"></a>Výpis informace o verzi operačního systému

**Win32_OperatingSystem** vlastnosti třídy zahrnují informace o verzi a service pack.
Můžete vybrat explicitně pouze tyto vlastnosti k získání informací o verzi shrnutí z **Win32_OperatingSystem**:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property BuildNumber,BuildType,OSType,ServicePackMajorVersion,ServicePackMinorVersion
```

Můžete také použít zástupné znaky s `Select-Object`na **vlastnost** parametr.
Protože všechny vlastnosti počínaje buď **sestavení** nebo **aktualizace Service Pack** jsou důležité pro použití Zde jsme zkrátit to pro následující tvar:

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

### <a name="listing-local-users-and-owner"></a>Výpis místní uživatelé a vlastníka

Místní obecné informace o uživateli – počet oprávněných uživatelů, aktuální počet uživatelů a jméno vlastníka – lze najít pomocí výběr **Win32_OperatingSystem** vlastnosti třídy se.
Můžete vybrat explicitně vlastnosti zobrazíte takto:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property NumberOfLicensedUsers,NumberOfUsers,RegisteredUser
```

Použití zástupných znaků více stručného verze je:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property *user*
```

### <a name="getting-available-disk-space"></a>Získávání volného místa na disku

Pokud chcete zobrazit místa na disku a volné místo pro místní disky, můžete použít třídu služby WMI Win32_LogicalDisk.
Je třeba zobrazit pouze instance s DriveType 3 – hodnota WMI používá pro pevné disky.

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

### <a name="getting-logon-session-information"></a>Získávání informací o relaci přihlášení

Obecné informace o přidružená k uživatelům prostřednictvím relace přihlášení můžete získat **Win32_LogonSession** třídu služby WMI:

```powershell
Get-CimInstance -ClassName Win32_LogonSession -ComputerName .
```

### <a name="getting-the-user-logged-on-to-a-computer"></a>Získávání uživateli přihlášenému k počítači

Můžete zobrazit uživateli přihlášenému k určitému počítači systému pomocí Win32_ComputerSystem.
Tento příkaz vrátí jenom uživateli přihlášení k ploše systému:

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -Property UserName -ComputerName .
```

### <a name="getting-local-time-from-a-computer"></a>Získávání z počítače, na místní čas

Aktuální místní čas v určitém počítači můžete načíst pomocí **Win32_LocalTime** třídu služby WMI.

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

### <a name="displaying-service-status"></a>Zobrazení stavu služby

Chcete-li zobrazit stav všech služeb v určitém počítači, místně můžete `Get-Service` rutiny.
Pro vzdálené systémy, můžete použít **Win32_Service** třídu služby WMI.
Pokud používáte také `Select-Object` filtrování výsledků na **stav**, **název**, a **DisplayName**, formát výstupu bude skoro stejná jako z `Get-Service`:

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Select-Object -Property Status,Name,DisplayName
```

Pokud chcete povolit úplný zobrazovaný názvů pro příležitostně služby s velmi dlouhé názvy, můžete chtít použít `Format-Table` s **AutoSize** a **zabalení** parametry za účelem optimalizace šířka sloupce a Povolit dlouhé názvy zabalit místo ke zkrácení:

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Format-Table -Property Status,Name,DisplayName -AutoSize -Wrap
```
