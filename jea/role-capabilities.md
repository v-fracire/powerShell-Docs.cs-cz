---
ms.date: 2017-06-12
author: rpsqrd
ms.topic: conceptual
keywords: "jea, prostředí powershell, zabezpečení"
title: "Možnosti JEA Role"
ms.openlocfilehash: 083cab3b44348168fe20e8355f5076b28be78702
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="jea-role-capabilities"></a>Možnosti JEA Role

> Platí pro: prostředí Windows PowerShell 5.0

Při vytváření koncový bod JEA, budete muset definovat jeden nebo více "role možnosti", které popisují *co* někdo můžete provést v relaci JEA.
Funkce role je prostředí PowerShell datový soubor s příponou .psrc obsahující seznam všech rutin, funkce, zprostředkovatele a externí programy, které má být k dispozici až po připojení uživatelů.

Toto téma popisuje, jak vytvořit soubor prostředí PowerShell role schopnosti pro vaše uživatele JEA.

## <a name="determine-which-commands-to-allow"></a>Určit, které příkazy umožňující

Prvním krokem při vytváření souboru funkce role, je rozmyslet, co budou uživatelé, kteří mají přiřazenou roli potřebují přístup k.
Požadavky na tento proces shromažďování může chvíli trvat, ale je velmi důležité procesu.
Udělení přístupu uživatelům ke příliš málo rutiny a funkce je můžete zabránit v získání své práci.
Povolení přístupu k příliš mnoho rutiny a funkce může vést k provádění více, než jste zamýšleli s jejich oprávněními implicitní správce oslabení vaší potřebujete zabezpečení uživatele.

Jak přejdete o tomto procesu bude záviset na vaší organizace a cíle, ale následující tipy může pomoci zajistit, že jste na správné cestě.

1. **Identifikovat** příkazy uživatelé používají pro své práci. To může zahrnovat průzkumu IT oddělení, kontrola skripty pro automatizaci nebo analýza přepisy relace prostředí PowerShell nebo protokoly.
2. **Aktualizace** pomocí nástroje příkazového řádku pro prostředí PowerShell ekvivalenty, kde je to možné, nejlepší auditování a JEA přizpůsobení prostředí. Externí programy nemůže být omezen jako granularly jako nativní rutiny prostředí PowerShell a funkce v sadě nástrojů JEA.
3. **Omezit** oboru rutin, pokud nezbytné jenom povolit konkrétní parametry nebo hodnoty parametru. To je zvlášť důležité, pokud uživatelé by měli být jenom moct spravovat součást systému.
4. **Vytvoření** nahradit komplexní příkazy nebo příkazy, které je obtížné omezit v sadě nástrojů JEA vlastní funkce. Jednoduché funkci, která zabalí komplexní příkaz nebo vztahuje další ověřovací logiku nabízí další ovládací prvek pro jednoduchost admins a koncového uživatele.
5. **Test** vymezená seznam povolených příkazů s uživatele nebo Automatizace služby a podle potřeby upravte.

Je důležité si pamatovat, že příkazy v relaci JEA jsou často oprávnění spustit s správce (nebo jinak zvýšených oprávnění).
Pozor, výběr dostupné příkazy je důležité zajistit, že koncový bod JEA neumožňuje je připojující se uživatel zvýšit svá oprávnění.
Níže jsou příklady příkazů, které mohou být používány neoprávněnému pokud povolený neomezeným stavu.
Všimněte si, že to není vyčerpávající seznam a musí být použit pouze jako vytvořených počáteční bod.

### <a name="examples-of-potentially-dangerous-commands"></a>Příklady potenciálně nebezpečná příkazy

Riziko | Příklad | Související příkazy
-----|---------|-----------------
Udělení oprávnění správce obejít JEA je připojující se uživatel | `Add-LocalGroupMember -Member 'CONTOSO\jdoe' -Group 'Administrators'` | `Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`
Spuštění libovolné kódu, například malware, zneužití nebo vlastní skripty obejít ochrany | `Start-Process -FilePath '\\san\share\malware.exe'` | `Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`

## <a name="create-a-role-capability-file"></a>Vytvořte soubor schopnosti role

Můžete vytvořit nový soubor schopnosti role prostředí PowerShell s [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) rutiny.

```powershell
New-PSRoleCapabilityFile -Path .\MyFirstJEARole.psrc
```

Výsledný soubor schopnosti role lze otevřít v textovém editoru a upravit tak, aby povolit požadované příkazy pro roli.
V nápovědě k prostředí PowerShell obsahuje několik příkladů, jak nakonfigurovat soubor.

### <a name="allowing-powershell-cmdlets-and-functions"></a>Povolení funkcí a rutiny prostředí PowerShell

Povolit uživatelům spustit rutiny prostředí PowerShell nebo funkce, přidejte název rutiny nebo funkce na VisbibleCmdlets nebo VisibleFunctions pole.
Pokud si nejste jisti, zda je příkaz rutiny nebo funkce, můžete spustit `Get-Command <name>` a zkontrolujte vlastnost "CommandType" ve výstupu.

```powershell
VisibleCmdlets = 'Restart-Computer', 'Get-NetIPAddress'
```

Někdy rozsah konkrétní rutiny nebo funkce je příliš široké potřebám vašich uživatelů.
Správce DNS, například pravděpodobně pouze potřebám přístup k restartování služby DNS.
Prostředí s více klientů, kde klienti mají přístup k nástroje pro správu samoobslužné služby musí být klienti omezená Správa s vlastní prostředky.
U těchto případech můžete omezit, parametry, které jsou zveřejněné z rutiny nebo funkce.

```powershell

VisibleCmdlets = @{ Name = 'Restart-Computer'; Parameters = @{ Name = 'Name' }}

```

V pokročilejších scénářích může také muset omezení hodnot, které můžete zadat někdo na tyto parametry.
Funkce role umožňují definovat sadu povolených hodnot nebo vzor regulárního výrazu, který se vyhodnotí pro určení, zda daný vstup povolen.

```powershell
VisibleCmdlets = @{ Name = 'Restart-Service'; Parameters = @{ Name = 'Name'; ValidateSet = 'Dns', 'Spooler' }},
                 @{ Name = 'Start-Website'; Parameters = @{ Name = 'Name'; ValidatePattern = 'HR_*' }}
```

> [!NOTE]
> [Společné parametry prostředí PowerShell](https://technet.microsoft.com/library/hh847884.aspx) jsou vždy povoleny, i v případě, že omezíte dostupné parametry.
> Můžete neměl by obsahovat explicitně je v poli parametrů.

Následující tabulka popisuje různé způsoby, kterými můžete přizpůsobit viditelné rutiny nebo funkce.
Můžete kombinovat a párovat některé z níže VisibleCmdlets pole.

Příklad                                                                                      | Případ použití
---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------
`'My-Func'` nebo `@{ Name = 'My-Func' }`                                                       | Umožňuje uživateli spustit `My-Func` bez jakýchkoli omezení na parametry.
`'MyModule\My-Func'`                                                                         | Umožňuje uživateli spustit `My-Func` z modulu `MyModule` bez jakýchkoli omezení na parametry.
`'My-*'`                                                                                     | Umožňuje uživateli spustit všechny rutiny nebo funkce s příkazem `My`.
`'*-Func'`                                                                                   | Umožňuje uživateli spustit všechny rutiny nebo funkce s podstatným jménem `Func`.
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'}, @{ Name = 'Param2' }}`               | Umožňuje uživateli spustit `My-Func` s `Param1` nebo `Param2` parametry. Na parametry můžete zadat libovolnou hodnotu.
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidateSet = 'Value1', 'Value2' }}`  | Umožňuje uživateli spustit `My-Func` s `Param1` parametr. Pro parametr lze zadat pouze "Hodnota1" a "Hodnota2".
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidatePattern = 'contoso.*' }}`     | Umožňuje uživateli spustit `My-Func` s `Param1` parametr. Parametru můžete zadat libovolnou hodnotu od "contoso".


> [!WARNING]
> Osvědčené postupy zabezpečení nedoporučujeme používat zástupné znaky při definování viditelné rutiny nebo funkce.
> Místo toho byste měli explicitně uvést každého důvěryhodné příkazu k zajištění, že žádné další příkazy, které sdílejí stejné schéma pojmenování jsou neúmyslně oprávnění.

ValidatePattern i ValidateSet nelze použít na stejné rutiny nebo funkce.

Pokud ano, přepíše ValidatePattern ValidateSet.

Další informace o ValidatePattern, podívejte se na [to *blogu Hey, Scripting Guy!* post](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) a [prostředí PowerShell regulární výrazy](https://technet.microsoft.com/library/hh847880.aspx) odkazovat na obsah.

### <a name="allowing-external-commands-and-powershell-scripts"></a>Povolení externí příkazy a skripty prostředí PowerShell

Povolit uživatelům spouštět spustitelné soubory a skripty prostředí PowerShell (.ps1) v relaci JEA, budete muset přidat úplnou cestu pro každý program v poli VisibleExternalCommands.

```powershell
VisibleExternalCommands = 'C:\Windows\System32\whoami.exe', 'C:\Program Files\Contoso\Scripts\UpdateITSoftware.ps1'
```

Doporučujeme, kde je to možné, používat ekvivalenty rutiny nebo funkce prostředí PowerShell externí spustitelné soubory, které autorizujete vzhledem k tomu, že budete mít kontrolu nad niž jsou povolené parametry pomocí rutin prostředí PowerShell nebo funkce.

Mnoho spustitelných souborů umožňují číst aktuální stav a pak ji změňte právě tím, že poskytuje různé parametry.

Představte si třeba roli správce na serveru soubor, který chce zkontrolujte, které síťové sdílené složky jsou hostované v místním počítači.
Jeden způsob kontroly je použití `net share`.
Však umožňuje net.exe je velmi nebezpečné, protože správce stejným způsobem použít příkaz k získání oprávnění správce s `net group Administrators unprivilegedjeauser /add`.
Lepším řešením je povolit [Get-SmbShare](https://technet.microsoft.com/library/jj635704.aspx) která dosáhne stejného výsledku, ale má mnohem omezenější obor.

Při provádění externích příkazů k dispozici uživatelům v relaci JEA, vždycky zadejte úplnou cestu ke spustitelnému souboru, aby nebudou program s podobným názvem (a potenciálně malicous) umístěny jinde v systému místo provedeny.

### <a name="allowing-access-to-powershell-providers"></a>Povolení přístupu k zprostředkovatelé prostředí PowerShell

Ve výchozím nastavení jsou k dispozici v relacích JEA žádní zprostředkovatelé prostředí PowerShell.

Toto je primárně pro snížení rizika citlivé informace a nastavení konfigurace, které se budou mít přístup k připojování uživatelů.

Pokud je to nezbytné, můžete povolit přístup k poskytovateli prostředí PowerShell pomocí `VisibleProviders` příkaz.
Úplný seznam poskytovatelů, spouštění `Get-PSProvider`.

```powershell
VisibleProviders = 'Registry'
```

Jednoduché úlohy, které vyžadují přístup k systému souborů, registru, úložiště certifikátů nebo jiných citlivých poskytovatelů byste také zvážit, zápis vlastní funkci, která funguje s poskytovatelem jménem uživatele.
Funkce, rutiny a externí programy, které jsou k dispozici v relaci JEA nejsou stejné omezující jako JEA – získají přístup k libovolného zprostředkovatele ve výchozím nastavení.
Také zvažte použití [uživatele jednotky](session-configurations.md#user-drive) při kopírování souborů do nebo z koncového bodu JEA je požadovaná.

### <a name="creating-custom-functions"></a>Vytvoření vlastní funkce

Můžete vytvářet vlastní funkce v souboru schopnosti role ke zjednodušení složité úlohy pro koncové uživatele.
Vlastní funkce jsou také užitečné, pokud požadujete pokročilé ověřovací logiku pro hodnoty parametru rutiny.
Psát jednoduché funkce **FunctionDefinitions** pole:

```powershell
VisibleFunctions = 'Get-TopProcess'

FunctionDefinitions = @{
    Name = 'Get-TopProcess'

    ScriptBlock = {
        param($Count = 10)

        Get-Process | Sort-Object -Property CPU -Descending | Microsoft.PowerShell.Utility\Select-Object -First $Count
    }
}
```

> [!IMPORTANT]
> Nezapomeňte přidat název své vlastní funkce pro **VisibleFunctions** pole proto může být spuštěna uživatelem JEA.


Text (bloku skriptu) vlastní funkce se spustí v režimu výchozí jazyk pro systém a nevztahují na JEA jazyková omezení.
To znamená, že funkce můžete přístup k systému souborů a registr a spustit příkazy, které nebyly v souboru schopnosti role dostupná.
Ujistěte se, aby se zabránilo povolení libovolný kód ke spuštění při použití parametrů a vyhnout se vstup uživatele zřetězení přímo do rutiny jako `Invoke-Expression`.

Ve výše uvedeném příkladu bude zjistíte, že název plně kvalifikovaného modulu (FQMN) `Microsoft.PowerShell.Utility\Select-Object` byl použit místo zkrácený `Select-Object`.
Funkce definované v souborech schopnosti role se stále vztahují oboru JEA relace, která zahrnuje funkce proxy JEA vytvoří omezit existující příkazy.

Select-Object je výchozí, omezené rutinu v všechny JEA relace, která neumožňuje můžete vybrat libovolný vlastnosti u objektů.
Pokud chcete používat funkce neomezeným Select-Object, musíte explicitně požádat o úplnou implementaci, zadáním FQMN.
Všechny rutiny omezené v relaci JEA bude mít květy stejné chování při vyvolání z funkce, souladu Powershellu [příkaz přednost před](https://msdn.microsoft.com/en-us/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).

Pokud píšete spoustu vlastní funkce, může být snazší jejich umístění [modulu skriptu prostředí PowerShell](https://msdn.microsoft.com/en-us/library/dd878340(v=vs.85).aspx).
Pak můžete provést tyto funkce viditelné v relaci JEA pomocí pole VisibleFunctions jako s moduly předdefinované a třetích stran.

## <a name="place-role-capabilities-in-a-module"></a>Umístěte role funkce v modulu

Aby PowerShell najít soubor funkce role musí být uložen ve složce "RoleCapabilities" v modulu prostředí PowerShell.
Modul můžou být uložená v libovolné složky součástí `$env:PSModulePath` proměnné prostředí, ale neměli umístěte do System32 (vyhrazené pro integrované moduly) nebo do složky kde nedůvěryhodná, připojení uživatelů může upravit soubory.
Dole je příklad vytvoření základní modul skriptu prostředí PowerShell s názvem *ContosoJEA* v cestě "Program Files".

```powershell
# Create a folder for the module
$modulePath = Join-Path $env:ProgramFiles "WindowsPowerShell\Modules\ContosoJEA"
New-Item -ItemType Directory -Path $modulePath

# Create an empty script module and module manifest. At least one file in the module folder must have the same name as the folder itself.
New-Item -ItemType File -Path (Join-Path $modulePath "ContosoJEAFunctions.psm1")
New-ModuleManifest -Path (Join-Path $modulePath "ContosoJEA.psd1") -RootModule "ContosoJEAFunctions.psm1"

# Create the RoleCapabilities folder and copy in the PSRC file
$rcFolder = Join-Path $modulePath "RoleCapabilities"
New-Item -ItemType Directory $rcFolder
Copy-Item -Path .\MyFirstJEARole.psrc -Destination $rcFolder
```

V tématu [pochopení modul PowerShell](https://msdn.microsoft.com/en-us/library/dd878324.aspx) Další informace o moduly, modul manifesty a proměnnou prostředí PSModulePath prostředí PowerShell.

## <a name="updating-role-capabilities"></a>Aktualizace role možnosti


Soubor schopnosti role můžete kdykoli aktualizovat jednoduše ukládání změn do souboru funkce role.
Všechny nové relace JEA spustit po aktualizaci schopnosti role se projeví revidovaný možnosti.

Z tohoto důvodu řízení přístupu ke složce Možnosti role je tak důležité.
Pouze vysoce důvěryhodných správců, byste měli mít měnit soubory funkce role.
Pokud nedůvěryhodné uživatel může změnit soubory funkce role, můžete snadno uvedou sami přístup do rutin, které mohly zvýšit jejich oprávnění.


Pro správce chtějí uzamčení přístup k funkcím role zajistěte, aby že místní systém má přístup pro čtení k souborům schopnosti role a obsahující moduly.

## <a name="how-role-capabilities-are-merged"></a>Způsob role možnosti sloučení

Uživatele můžete mít udělen přístup k více možností role při jejich zadejte JEA relaci v závislosti na roli mapování na [relace konfigurační soubor](session-configurations.md).
V takovém případě se pokusí uživateli přidělit JEA *nejvíce projektovou* sadu příkazů, které jsou povolené žádné role.

**VisibleCmdlets a VisibleFunctions**

Většina komplexní logiku sloučení ovlivňuje rutiny a funkce, což může mít jejich parametrů a hodnoty parametrů v sadě nástrojů JEA omezené.

Pravidla jsou následující:

1. Pokud rutiny jsou dostupná pouze v jedné role, bude viditelné pro uživatele s omezeními použít parametr.
2. Pokud rutiny jsou dostupná ve více než jedné role, a Každá role má stejné omezení u rutinu, bude rutina viditelné pro uživatele s těmito omezeními.
3. Pokud rutiny jsou dostupná ve více než jedné role, a každou roli umožňuje jinou sadu parametrů, rutiny a všechny parametry definované v každé role budou viditelné pro uživatele. Pokud jednu roli nemá omezení pro parametry, budou mít povolený všechny parametry.
4. Pokud jedna role definuje sadu ověřením nebo ověřením vzor pro parametr rutiny, a jinou roli umožňuje parametr, ale neuvádělo hodnoty parametrů, ověřit sady nebo vzor se budou ignorovat.
5. Pokud sadu ověřením definovaná pro parametr rutiny ve více než jedné role, všechny hodnoty ze všech sad ověřením bude možné.
6. Pokud vzor ověřením definovaná pro parametr rutiny ve více než jedné role, všechny hodnoty, které odpovídají některé vzory bude možné.
7. Pokud sadu ověřením je definována v jedné nebo více rolí, a ověřit vzor je definována v jiné role pro parametr stejné rutiny, je ignorován sadu ověřením a pravidlo (6) se vztahuje na zbývající vzory ověřením.

Dole je příklad způsob sloučení rolí podle těchto pravidel:

```powershell
# Role A Visible Cmdlets
$roleA = @{
    VisibleCmdlets = 'Get-Service',
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Client' } }
}

# Role B Visible Cmdlets
$roleB = @{
    VisibleCmdlets = @{ Name = 'Get-Service'; Parameters = @{ Name = 'DisplayName'; ValidatePattern = 'DNS.*' } },
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Server' } }
}

# Resulting permisisons for a user who belongs to both role A and B
# - The constraint in role B for the DisplayName parameter on Get-Service is ignored becuase of rule #4
# - The ValidateSets for Restart-Service are merged because both roles use ValidateSet on the same parameter per rule #5
$mergedAandB = @{
    VisibleCmdlets = 'Get-Service',
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Client', 'DNS Server' } }
}
```



**VisibleExternalCommands ScriptsToProcess VisibleAliases, VisibleProviders,**

Všechna pole v souboru schopnosti role jsou jednoduše přidat do kumulativní sadu povolených externích příkazů, aliasy, poskytovatelů a spouštění skriptů.
Příkaz, alias, zprostředkovatele nebo skriptu, které jsou k dispozici v jedné role funkce bude k dispozici pro uživatele JEA.

Dávejte pozor, abyste ověřili, že kombinovanou sadu zprostředkovatelů z jednoho schopnosti role a rutiny nebo funkce nebo příkazy z jiné neumožňuje, aby uživatelé připojující neúmyslnému přístupu k systémovým prostředkům.
Například, pokud umožňuje jednu roli `Remove-Item` rutina a jiné umožňuje `FileSystem` poskytovatele, jsou hrozí JEA uživatel odstraní libovolné soubory ve vašem počítači.
Další informace o identifikaci skutečná oprávnění uživatelů lze najít v [auditování JEA tématu](audit-and-report.md).

## <a name="next-steps"></a>Další kroky

- [Vytvoření konfiguračního souboru relace](session-configurations.md)

