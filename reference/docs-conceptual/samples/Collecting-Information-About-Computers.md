---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Shromažďování informací o počítačích
ms.assetid: 9e7b6a2d-34f7-4731-a92c-8b3382eb51bb
ms.openlocfilehash: 99125ef701705c20d4e955c79eaa3469ce4d58fb
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403676"
---
# <a name="collecting-information-about-computers"></a>Shromažďování informací o počítačích

Rutiny z **CimCmdlets** modulu jsou nejdůležitější rutiny pro úlohy správy obecné systému.
Všechna nastavení subsystém jsou přístupné prostřednictvím rozhraní WMI.
Kromě toho služby WMI považuje za data objekty, které jsou v kolekcích jednu nebo více položek.
Protože prostředí Windows PowerShell taky funguje s objekty a má kanál, který umožňuje zpracovávat jeden nebo více objektů stejným způsobem, obecný přístup pomocí rozhraní WMI umožňuje provádět některé pokročilé úlohy s příliš mnoho zásahů.

Následující příklady ukazují, jak shromažďovat konkrétní informace s použitím `Get-CimInstance` proti libovolného počítače.
Můžeme zadat **ComputerName** parametr s hodnotou tečka (**.**), který představuje místní počítač.
Můžete zadat název nebo IP adresa přidružená k každý počítač, který můžete oslovit prostřednictvím rozhraní WMI.
Pokud chcete načíst informace o místním počítači, může vynechat **ComputerName** parametru.

### <a name="listing-desktop-settings"></a>Výpis nastavení pracovní plochy

Začneme příkaz, který shromažďuje informace o stolních počítačích v místním počítači.

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName .
```

Informace pro všechny pracovní plochy, vrátí se, zda jsou právě používány, nebo ne.

> [!NOTE]
> Informace o vrácené některé třídy služby WMI může být velmi podrobné a často zahrnují metadata o třída služby WMI.
Protože většina těchto vlastností metadata mají názvy, které začínají **Cim**, můžete filtrovat pomocí vlastností `Select-Object`.
Zadejte **- ExcludeProperty** parametr "Cim *" jako hodnotu.
Příklad:

```powershell
Get-CimInstance -ClassName Win32_Desktop -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

Pokud chcete vyfiltrovat metadata, použijte operátor kanálu (|) odeslat výsledky `Get-CimInstance` příkaz `Select-Object -ExcludeProperty "CIM*"`.

### <a name="listing-bios-information"></a>Výpis informace o systému BIOS

WMI **Win32_BIOS** třída vrací poměrně kompaktní a kompletní informace o systému BIOS na místním počítači:

```powershell
Get-CimInstance -ClassName Win32_BIOS -ComputerName .
```

### <a name="listing-processor-information"></a>Informace o procesoru výpis

Informace o obecných procesoru můžete načíst pomocí služby WMI **Win32_Processor** třídy, i když budete pravděpodobně chtít filtrování informací:

```powershell
Get-CimInstance -ClassName Win32_Processor -ComputerName . | Select-Object -ExcludeProperty "CIM*"
```

Pro řetězec obecný popis procesorů může právě vrátit **typ SystemType** vlastnost:

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -ComputerName . | Select-Object -Property SystemType

SystemType
----------
X86-based PC
```

### <a name="listing-computer-manufacturer-and-model"></a>Výpis modelu a výrobce počítače

Informace o počítači modelu je také k dispozici z **Win32_ComputerSystem**.
Ve standardním výstupu zobrazeného nebudete potřebovat, filtrování poskytující OEM data:

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem
```

```output
Name PrimaryOwnerName Domain    TotalPhysicalMemory Model                   Manufacturer
---- ---------------- ------    ------------------- -----                   ------------
MyPC Jane Doe         WORKGROUP 804765696           DA243A-ABA 6415cl NA910 Compaq Presario 06
```

Výstup z příkazů takovou situaci, které vracejí informace přímo z některý hardware, je jenom tak dobré jako data, ke kterým máte.
Některé informace o výrobci hardwaru není správně nakonfigurován a proto možná není k dispozici.

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

Pro stručnější výstup můžete chtít vyloučit některé vlastnosti.
Přestože lze použít `Get-CimInstance`společnosti **vlastnost** parametr zvolit pouze **HotFixID**, to uděláte tak, budou vracet další informace, protože je ve výchozím nastavení zobrazí všechna metadata:

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

Vrátí další data, protože vlastnost parametru v `Get-CimInstance` omezuje vlastnosti vrácená z instancí třídy služby WMI, není objekt se vrátil do prostředí Windows PowerShell.
Chcete-li snížit výstup, použijte `Select-Object`:

```powershell
Get-CimInstance -ClassName Win32_QuickFixEngineering -ComputerName . -Property HotFixId | Select-Object -Property HotFixId
```

```output
HotFixId
--------
KB4048951
```

### <a name="listing-operating-system-version-information"></a>Výpis informací o verzi operačního systému

**Win32_OperatingSystem** vlastnosti třídy zahrnují informace o balíčku verze a služeb.
Můžete explicitně vybrat pouze tyto vlastnosti se získat informace o verzi Souhrn **Win32_OperatingSystem**:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property BuildNumber,BuildType,OSType,ServicePackMajorVersion,ServicePackMinorVersion
```

Můžete také použít zástupné znaky `Select-Object`společnosti **vlastnost** parametr.
Protože všechny vlastnosti začínající buď **sestavení** nebo **aktualizace Service Pack** jsou důležité pro použití tady jsme můžete zkrátit to pro následující tvar:

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

### <a name="listing-local-users-and-owner"></a>Seznam místních uživatelů a vlastníka

Místní obecné informace o uživateli – počet licencovaných uživatelů, aktuální počet uživatelů a jméno vlastníka – lze nalézt pomocí výběru **Win32_OperatingSystem** vlastnosti třídy.
Můžete explicitně vybrat vlastnosti, které chcete zobrazit takto:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property NumberOfLicensedUsers,NumberOfUsers,RegisteredUser
```

Použití zástupných znaků Stručnější verze je:

```powershell
Get-CimInstance -ClassName Win32_OperatingSystem -ComputerName . | Select-Object -Property *user*
```

### <a name="getting-available-disk-space"></a>Získávání volného místa na disku

Pokud chcete zobrazit místa na disku a volné místo pro místní jednotky pevných disků, můžete použít třídu služby WMI Win32_LogicalDisk.
Je třeba zobrazit pouze instance s DriveType 3 – hodnotu používá rozhraní WMI pro pevné disky.

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

Obecné informace o uživatelské relace spojené s uživateli prostřednictvím můžete získat **Win32_LogonSession** třída služby WMI:

```powershell
Get-CimInstance -ClassName Win32_LogonSession -ComputerName .
```

### <a name="getting-the-user-logged-on-to-a-computer"></a>Získávání uživatel přihlášen k počítači

Můžete zobrazit na určitý počítač systému Win32_ComputerSystem přihlášeného uživatele.
Tento příkaz vrátí pouze uživateli přihlášenému k desktopu systému:

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem -Property UserName -ComputerName .
```

### <a name="getting-local-time-from-a-computer"></a>Získávání místní čas z počítače

Aktuální místní čas v určitém počítači můžete načíst pomocí **Win32_LocalTime** třída služby WMI.

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
Pro vzdálené systémy, můžete použít **Win32_Service** třída služby WMI.
Pokud používáte také `Select-Object` pro filtrování výsledků na **stav**, **název**, a **DisplayName**, výstupní formát bude téměř totožný s tím, z `Get-Service`:

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Select-Object -Property Status,Name,DisplayName
```

Povolit úplnou zobrazované názvy pro občasné služby s velmi dlouhé názvy, můžete chtít použít `Format-Table` s **AutoSize** a **zabalení** parametry pro optimalizaci šířku sloupce a Povolit dlouhé názvy zabalit místo vedlo ke zkrácení:

```powershell
Get-CimInstance -ClassName Win32_Service -ComputerName . | Format-Table -Property Status,Name,DisplayName -AutoSize -Wrap
```
