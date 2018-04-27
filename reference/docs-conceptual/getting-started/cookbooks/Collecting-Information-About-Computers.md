---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Shromažďování informací o počítačích
ms.assetid: 9e7b6a2d-34f7-4731-a92c-8b3382eb51bb
ms.openlocfilehash: 7f5a5f6accd57a84e2bcb3d20c14640a8e028791
ms.sourcegitcommit: a9aa5e8d0fab0cbb3e4e6cff0e3ca8c0339ab4e6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/27/2018
---
# <a name="collecting-information-about-computers"></a>Shromažďování informací o počítačích

**Get-WmiObject** je nejdůležitější rutina pro obecné systém úlohy správy. Všechna nastavení kritické subsystém se zveřejňují přes rozhraní WMI. Kromě toho WMI data jsou považovány za objekty, které jsou v kolekcích jednu nebo více položek. Protože prostředí Windows PowerShell taky pracuje s objekty a má kanál, který vám umožní zacházet s jednoho nebo více objektů stejným způsobem, obecný přístup WMI umožňuje provádět některé pokročilé úlohy s uživatele příliš mnoho zásahů.

Následující příklady ukazují, jak shromažďovat konkrétní informace pomocí **Get-WmiObject** libovolný počítač. Určíme **ComputerName** parametr s hodnotou tečkou (**.**), který představuje místní počítač. Můžete zadat název nebo IP adresu přidruženou libovolného počítače, které lze získat přístup pomocí rozhraní WMI. Pokud chcete načíst informace o místním počítači, může vynechat **- ComputerName.**

### <a name="listing-desktop-settings"></a>Výpis nastavení plochy

Začneme příkaz, který shromažďuje informace o stolní počítače v místním počítači.

```powershell
Get-WmiObject -Class Win32_Desktop -ComputerName .
```

Tento příkaz vrátí informace pro všechny pracovní plochy, zda jsou právě používány, nebo ne.

> [!NOTE]
> Informace o vrácené některé třídy WMI může být velmi podrobné a často obsahují metadata o třídu služby WMI. Vzhledem k tomu, že většina těchto metadat vlastností názvy, které začínají dvojité podtržítko, můžete filtrovat pomocí Select-Object vlastnosti. Zadejte pouze vlastnosti, které začínají s abecední znaky pomocí **[-z]*** jako hodnota vlastnosti. Příklad:

```powershell
Get-WmiObject -Class Win32_Desktop -ComputerName . | Select-Object -Property [a-z]*
```

Filtrovat metadata, použijte operátor kanálu (|) k odeslání výsledky příkazu Get-WmiObject k `Select-Object -Property [a-z]*`.

### <a name="listing-bios-information"></a>Výpis informace o systému BIOS

Vlastnost rozhraní WMI Win32_BIOS vrátí poměrně compact a úplné informace o systému BIOS v místním počítači:

```powershell
Get-WmiObject -Class Win32_BIOS -ComputerName .
```

### <a name="listing-processor-information"></a>Výpis informace o procesoru

Informace o obecné procesoru můžete načíst pomocí rozhraní WMI na **Win32_Processor** třídy, i když budete pravděpodobně chtít filtrování informací:

```powershell
Get-WmiObject -Class Win32_Processor -ComputerName . | Select-Object -Property [a-z]*
```

Obecný popis řetězce třídu procesoru, může jen vrátit **typ SystemType** vlastnost:

```
PS> Get-WmiObject -Class Win32_ComputerSystem -ComputerName . | Select-Object -Property SystemType

SystemType
----------
X86-based PC
```

### <a name="listing-computer-manufacturer-and-model"></a>Výpis Model a výrobce počítače

Informace o modelu počítače je také dostupná z **Win32_ComputerSystem**. Ve standardním výstupu zobrazeného nebudete potřebovat jakéhokoli filtrování poskytující OEM data:

```
PS> Get-WmiObject -Class Win32_ComputerSystem

Domain              : WORKGROUP
Manufacturer        : Compaq Presario 06
Model               : DA243A-ABA 6415cl NA910
Name                : MyPC
PrimaryOwnerName    : Jane Doe
TotalPhysicalMemory : 804765696
```

Výstup z příkazy jako to, které vrací informace přímo z některé hardwaru, je pouze jako vhodný jako data, která máte. Některé informace není správně nakonfigurováno podle výrobců hardwaru a proto pravděpodobně není k dispozici.

### <a name="listing-installed-hotfixes"></a>Výpis nainstalovaných oprav hotfix

Můžete vytvořit seznam všech nainstalovaných oprav hotfix s použitím **Win32_QuickFixEngineering**:

```powershell
Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName .
```

Tato třída vrátí seznam oprav hotfix, které vypadá takto:

```output
Description         : Update for Windows XP (KB910437)
FixComments         : Update
HotFixID            : KB910437
Install Date        :
InstalledBy         : Administrator
InstalledOn         : 12/16/2005
Name                :
ServicePackInEffect : SP3
Status              :
```

Pro více stručného výstup můžete chtít vyloučit některé vlastnosti. Přestože je možné použít **vlastnost Get-WmiObject** parametr zvolit pouze **HotFixID**, to tak, budou vracet další informace, protože je ve výchozím nastavení zobrazí všechna metadata:

```
PS> Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName . -Property HotFixID

HotFixID         : KB910437
__GENUS          : 2
__CLASS          : Win32_QuickFixEngineering
__SUPERCLASS     :
__DYNASTY        :
__RELPATH        :
__PROPERTY_COUNT : 1
__DERIVATION     : {}
__SERVER         :
__NAMESPACE      :
__PATH           :
```

Vrátí další data, protože parametr vlastností v **Get-WmiObject** omezuje vlastnosti vrácená z instancí třídy služby WMI, není objekt byl vrácen do prostředí Windows PowerShell. Chcete-li snížit výstup, použijte **Select-Object**:

```
PS> Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName . -Property HotFixId | Select-Object -Property HotFixId

HotFixId
--------
KB910437
```

### <a name="listing-operating-system-version-information"></a>Výpis informace o verzi operačního systému

**Win32_OperatingSystem** vlastnosti třídy zahrnují informace o verzi a service pack. Můžete vybrat explicitně pouze tyto vlastnosti k získání informací o verzi shrnutí z **Win32_OperatingSystem**:

```powershell
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property BuildNumber,BuildType,OSType,ServicePackMajorVersion,ServicePackMinorVersion
```

Můžete také použít zástupné znaky s **vlastnost Select-Object** parametr. Protože všechny vlastnosti počínaje buď **sestavení** nebo **aktualizace Service Pack** jsou důležité pro použití Zde jsme zkrátit to pro následující tvar:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property Build*,OSType,ServicePack*

BuildNumber             : 2600
BuildType               : Uniprocessor Free
OSType                  : 18
ServicePackMajorVersion : 2
ServicePackMinorVersion : 0
```

### <a name="listing-local-users-and-owner"></a>Výpis místní uživatelé a vlastníka

Místní obecné informace o uživateli – počet oprávněných uživatelů, aktuální počet uživatelů a jméno vlastníka – lze najít pomocí výběr **Win32_OperatingSystem** vlastnosti. Můžete vybrat explicitně vlastnosti zobrazíte takto:

```powershell
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property NumberOfLicensedUsers,NumberOfUsers,RegisteredUser
```

Použití zástupných znaků více stručného verze je:

```powershell
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property *user*
```

### <a name="getting-available-disk-space"></a>Získávání volného místa na disku

Pokud chcete zobrazit místa na disku a volné místo pro místní disky, můžete použít třídy Win32_LogicalDisk rozhraní WMI. Je třeba zobrazit pouze instance s DriveType 3 – hodnota WMI používá pro pevné disky.

```
PS> Get-WmiObject -Class Win32_LogicalDisk -Filter "DriveType=3" -ComputerName .

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 65541357568
Size         : 203912880128
VolumeName   : Local Disk

DeviceID     : Q:
DriveType    : 3
ProviderName :
FreeSpace    : 44298250240
Size         : 122934034432
VolumeName   : New Volume

PS> Get-WmiObject -Class Win32_LogicalDisk -Filter "DriveType=3" -ComputerName . | Measure-Object -Property FreeSpace,Size -Sum | Select-Object -Property Property,Sum

Property           Sum
--------           ---
FreeSpace 109839607808
Size      326846914560
```

### <a name="getting-logon-session-information"></a>Získávání informací o relaci přihlášení

Můžete získat obecné informace o relacích přihlášení přidružená k uživatelům prostřednictvím rozhraní WMI Win32_LogonSession třídy:

```powershell
Get-WmiObject -Class Win32_LogonSession -ComputerName .
```

### <a name="getting-the-user-logged-on-to-a-computer"></a>Získávání uživateli přihlášenému k počítači

Můžete zobrazit uživateli přihlášenému k určitému počítači systému pomocí Win32_ComputerSystem. Tento příkaz vrátí jenom uživateli přihlášení k ploše systému:

```powershell
Get-WmiObject -Class Win32_ComputerSystem -Property UserName -ComputerName .
```

### <a name="getting-local-time-from-a-computer"></a>Získávání z počítače, na místní čas

Pomocí třídy služby WMI Win32_LocalTime můžete načíst aktuálním místním časem v určitém počítači. Vzhledem k tomu, že tato třída ve výchozím nastavení zobrazí veškerá metadata, můžete filtrovat pomocí **Select-Object**:

```
PS> Get-WmiObject -Class Win32_LocalTime -ComputerName . | Select-Object -Property [a-z]*

Day          : 15
DayOfWeek    : 4
Hour         : 12
Milliseconds :
Minute       : 11
Month        : 6
Quarter      : 2
Second       : 52
WeekInMonth  : 3
Year         : 2006
```

### <a name="displaying-service-status"></a>Zobrazení stavu služby

Chcete-li zobrazit stav všech služeb v určitém počítači, místně můžete **Get-Service** rutiny, jak je uvedeno výše. Pro vzdálené systémy můžete použít třídu Win32_Service rozhraní WMI. Pokud používáte také **Select-Object** filtrování výsledků na **stav**, **název**, a **DisplayName**, formát výstupu bude téměř stejná jako z **Get-Service**:

```powershell
Get-WmiObject -Class Win32_Service -ComputerName . | Select-Object -Property Status,Name,DisplayName
```

Pokud chcete povolit úplný zobrazovaný názvů pro příležitostně služby s velmi dlouhé názvy, můžete chtít použít **Format-Table** s **AutoSize** a **zabalení** parametry , optimalizace šířka sloupce a povolit dlouhé názvy zabalit místo ke zkrácení:

```powershell
Get-WmiObject -Class Win32_Service -ComputerName . | Format-Table -Property Status,Name,DisplayName -AutoSize -Wrap
```
