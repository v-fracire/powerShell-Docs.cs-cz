---
ms.date: 06/12/2017
keywords: jea, powershell, zabezpečení
title: Role funkce JEA
ms.openlocfilehash: bd0a995adc60e50049ff99d6b23e7c2aeb745a18
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522935"
---
# <a name="jea-role-capabilities"></a>Role funkce JEA

> Platí pro: Windows PowerShell 5.0

Při vytváření koncového bodu JEA, budete muset definovat jeden nebo více "funkce rolí" které popisují *co* někdo můžete provést v relaci JEA.
Funkce role je PowerShell datový soubor s příponou .psrc, který obsahuje seznam všech rutin, funkcí, poskytovatelů a externích programů, které by měly být k dispozici připojování uživatelů.

Toto téma popisuje, jak vytvořit soubor prostředí PowerShell role funkce JEA uživatelům.

## <a name="determine-which-commands-to-allow"></a>Určit, které příkazy umožňující

Prvním krokem při vytváření souboru funkce role, je rozmyslet, co uživatelé, kteří mají přiřazenou roli potřebovat přístup k.
Tyto požadavky proces shromažďování může chvíli trvat, ale je velmi důležité proces.
Udělení přístupu uživatelům ke příliš málo rutiny a funkce je můžete zabránit v získání jejich práci.
Povolení přístupu k příliš mnoho funkcí a rutiny může vést k provádění více, než jste chtěli s jejich oprávněními implicitní správce oslabení postoj vaší zabezpečení uživatele.

Jak přejít o tomto procesu bude záviset na vaší organizace a cíle, ale následující tipy mohou pomoci zajistit, že jste na správné cestě.

1. **Identifikujte** příkazy uživatelé používají k dokončení jejich úloh. To může zahrnovat zjištění pracovníky IT, kontrolu skriptů pro automatizaci nebo analýza protokolů nebo záznamy o studiu relace prostředí PowerShell.
2. **Aktualizace** pomocí nástroje příkazového řádku a Powershellu ekvivalenty, kde je to možné, pro nejlepší auditování a možnostmi přizpůsobení JEA. Jako posunutím jako nativní rutin prostředí PowerShell a funkce v sadě nástrojů JEA nemůže omezovat externích programů.
3. **Omezit** oboru rutin, pokud je nutné jenom povolit určité parametry nebo hodnoty parametrů. To je zvlášť důležité, pokud uživatelé by měli být pouze možnost spravovat součástí systému.
4. **Vytvoření** vlastní funkce k nahrazení komplexní příkazy nebo příkazy, které je obtížné zachovat v sadě nástrojů JEA. Jednoduché funkce, která zabalí komplexní příkaz nebo použije další ověřovací logiku můžou nabízet další ovládací prvek pro zjednodušení správci a koncových uživatelů.
5. **Test** s vymezeným oborem seznam povolených příkazů s vaší uživatele a/nebo Automatizace služeb a podle potřeby upravte.

Je dobré si uvědomit, že příkazy v relaci JEA jsou často oprávněními spustit správce (nebo jinak se zvýšenými oprávněními).
Pozor, výběr dostupných příkazech je důležité zajistit, že koncového bodu JEA neumožňuje připojení uživatelů ke zvýšení svých oprávnění.
Níže je několik příkladů příkazů, které můžete použít speciálně Pokud může ve stavu bez omezení.
Všimněte si, že to není vyčerpávající seznam a slouží pouze jako výchozí bod vytvořených.

### <a name="examples-of-potentially-dangerous-commands"></a>Příklady potenciálně nebezpečných příkazů

Riziko | Příklad | Související příkazy
-----|---------|-----------------
Udělení oprávnění správce, aby vynechat JEA je připojující se uživatel | `Add-LocalGroupMember -Member 'CONTOSO\jdoe' -Group 'Administrators'` | `Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`
Spuštění libovolného kódu, jako je například malware, zneužití nebo vlastní skripty pro obejití ochrany | `Start-Process -FilePath '\\san\share\malware.exe'` | `Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`

## <a name="create-a-role-capability-file"></a>Vytvořte soubor funkce rolí

Můžete vytvořit nový soubor funkce role prostředí PowerShell s [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) rutiny.

```powershell
New-PSRoleCapabilityFile -Path .\MyFirstJEARole.psrc
```

Výsledný soubor funkce role můžete otevřít v textovém editoru a upravit tak, aby bylo možné požadované příkazy pro danou roli.
V nápovědě k prostředí PowerShell obsahuje několik příkladů konfigurace souboru.

### <a name="allowing-powershell-cmdlets-and-functions"></a>Povolení funkcí a rutin prostředí PowerShell

K autorizaci uživatelů ke spouštění rutin prostředí PowerShell nebo funkce, přidejte do polí VisbibleCmdlets nebo VisibleFunctions název rutiny nebo funkce.
Pokud si nejste jisti, zda je příkazu rutiny nebo funkce, můžete spustit `Get-Command <name>` a zkontrolujte vlastnost "CommandType" ve výstupu.

```powershell
VisibleCmdlets = 'Restart-Computer', 'Get-NetIPAddress'
```

Obor konkrétní rutiny nebo funkce je někdy příliš široké pro potřeby vašich uživatelů.
Správce DNS, například požaduje pravděpodobně pouze k restartování služby DNS.
V prostředí s více tenanty, kde jsou tenanti udělen přístup k samoobslužné správy nástroje třeba tenantů omezit na správu pomocí svoje vlastní prostředky.
Pro tyto případy můžete omezit, jaké parametry jsou přístupné z rutiny nebo funkce.

```powershell

VisibleCmdlets = @{ Name = 'Restart-Computer'; Parameters = @{ Name = 'Name' }}

```

V pokročilejších scénářích budete také muset omezení hodnot, které někdo můžete zadat tyto parametry.
Funkce rolí umožňují definovat sadu povolených hodnot nebo vzor regulárního výrazu, který je vyhodnocován pro určení, jestli je povolený daný vstup.

```powershell
VisibleCmdlets = @{ Name = 'Restart-Service'; Parameters = @{ Name = 'Name'; ValidateSet = 'Dns', 'Spooler' }},
                 @{ Name = 'Start-Website'; Parameters = @{ Name = 'Name'; ValidatePattern = 'HR_*' }}
```

> [!NOTE]
> [Společné parametry prostředí PowerShell](https://technet.microsoft.com/library/hh847884.aspx) jsou vždy povoleny, i když můžete omezit dostupné parametry.
> Neměli uvedete explicitně je v poli parametrů.

Následující tabulka popisuje různé způsoby, jak můžete přizpůsobit viditelné rutiny nebo funkce.
Můžete kombinovat a párovat některý níže VisibleCmdlets pole.

Příklad                                                                                      | Případ použití
---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------
`'My-Func'` nebo `@{ Name = 'My-Func' }`                                                       | Umožňuje uživateli spustit `My-Func` bez jakýchkoli omezení na parametry.
`'MyModule\My-Func'`                                                                         | Umožňuje uživateli spustit `My-Func` z modulu `MyModule` bez jakýchkoli omezení na parametry.
`'My-*'`                                                                                     | Umožňuje uživateli spustit libovolné rutiny nebo funkce s příkaz `My`.
`'*-Func'`                                                                                   | Umožňuje uživateli spustit libovolné rutiny nebo funkce s podstatným jménem `Func`.
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'}, @{ Name = 'Param2' }}`               | Umožňuje uživateli spustit `My-Func` s `Param1` a/nebo `Param2` parametry. Libovolná hodnota mohou být poskytnuty parametry.
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidateSet = 'Value1', 'Value2' }}`  | Umožňuje uživateli spustit `My-Func` s `Param1` parametru. Parametr lze zadat pouze "Hodnota1" a "Hodnota2".
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidatePattern = 'contoso.*' }}`     | Umožňuje uživateli spustit `My-Func` s `Param1` parametru. Předat parametru můžete zadat libovolnou hodnotu od "contoso".


> [!WARNING]
> Osvědčené postupy zabezpečení nedoporučujeme používat zástupné znaky, při definování viditelné rutiny nebo funkce.
> Místo toho by měly explicitně uvádět každé důvěryhodné příkaz, kterým zajistíte, že žádné další příkazy, které sdílejí stejné schéma pojmenování neúmyslně oprávnění.

ValidatePattern i ValidateSet nelze použít stejnou rutinu nebo funkce.

Pokud ano, přepíše ValidatePattern ValidateSet.

Další informace o ValidatePattern, projděte si [to *Hey, Scripting Guy!!* příspěvku](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) a [regulární výrazy Powershellu](https://technet.microsoft.com/library/hh847880.aspx) referenční obsah.

### <a name="allowing-external-commands-and-powershell-scripts"></a>Povolení externího příkazy a skripty prostředí PowerShell

Umožňuje uživatelům spouštět spustitelné soubory a skripty prostředí PowerShell (.ps1) v relaci JEA budete muset přidat do každého programu v poli VisibleExternalCommands úplnou cestu.

```powershell
VisibleExternalCommands = 'C:\Windows\System32\whoami.exe', 'C:\Program Files\Contoso\Scripts\UpdateITSoftware.ps1'
```

Doporučujeme, kde je to možné, používat PowerShell rutinu/funkce ekvivalenty externí spustitelné soubory, které autorizujete, protože budete mít kontrolu nad tím, které jsou povoleny parametry s functions rutiny prostředí PowerShell.

Mnoho spustitelných souborů bylo možné číst aktuální stav a pak ji změňte právě tím, že poskytuje různé parametry.

Představte si třeba roli správce serveru soubor, který chcete zkontrolovat, které sdílené síťové složky, které jsou hostované v místním počítači.
Zkontrolujte jedním ze způsobů je použít `net share`.
Nicméně umožňuje net.exe je velmi nebezpečné, protože správce stejně snadno použít příkaz získat oprávnění správce s `net group Administrators unprivilegedjeauser /add`.
Lepším řešením je povolit [Get-SmbShare](https://technet.microsoft.com/library/jj635704.aspx) která dosáhne stejného výsledku, ale má mnohem více omezený rozsah.

Při provádění externích příkazů k dispozici uživatelům v relaci JEA, vždy zadejte úplnou cestu ke spustitelnému souboru k zajištění s podobným názvem (a potenciálně malicous) aplikace umístěn jinde v systému nejsou vykonány místo.

### <a name="allowing-access-to-powershell-providers"></a>Povolení přístupu ke zprostředkovatelům prostředí PowerShell

Ve výchozím nastavení nejsou k dispozici v relacích JEA žádní zprostředkovatelé prostředí PowerShell.

To je především pro snížení rizika citlivé informace a nastavení konfigurace se starším připojující se uživatel.

Pokud je to nezbytné, můžete povolit přístup ke zprostředkovatelům Powershellu pomocí `VisibleProviders` příkazu.
Úplný seznam poskytovatelů, spouštění `Get-PSProvider`.

```powershell
VisibleProviders = 'Registry'
```

Pro jednoduché úlohy, které vyžadují přístup k systému souborů, registry, úložiště certifikátů nebo jiných citlivých poskytovatelů může také být vhodné zápis vlastní funkce, který spolupracuje s poskytovateli jménem uživatele.
Funkce, rutiny a externích programů, které jsou k dispozici v relaci JEA nejsou v souladu s stejná omezení jako JEA – jakýkoli poskytovatel přístupem ve výchozím nastavení.
Také zvážit použití [uživatele jednotky](session-configurations.md#user-drive) při kopírování souborů do/z koncového bodu JEA je povinný.

### <a name="creating-custom-functions"></a>Vytvoření vlastní funkce

Můžete vytvářet vlastní funkce v souboru funkce role pro zjednodušení složitých úloh pro koncové uživatele.
Vlastní funkce jsou také užitečné, pokud požadujete pokročilé ověřovací logiku pro hodnoty parametru rutiny.
Můžete psát jednoduché funkce **FunctionDefinitions** pole:

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
> Nezapomeňte si přidat název své vlastní funkce pro **VisibleFunctions** pole, aby mohla být užívána uživateli JEA.


Text (bloku skriptu) vlastní funkce se spustí v režimu výchozí jazyk pro systém a není předmětem omezení JEA na jazyk.
To znamená, že funkce můžete přístup k systému souborů a registru a spouštět příkazy, které nebyly nastavena jako viditelná v souboru funkce role.
Snažte se vyhnout, což libovolný kód ke spuštění, při použití parametrů a vyhnout se vstup uživatele zřetězení příkazů přímo do rutiny jako `Invoke-Expression`.

V předchozím příkladu si povšimněte, který modul plně kvalifikovaný název (FQMN) `Microsoft.PowerShell.Utility\Select-Object` byl použit místo zkrácený `Select-Object`.
Funkce definované v souborech schopností role jsou pořád v souladu s rozsahu JEA relací, což zahrnuje funkce proxy JEA vytvoří omezit stávající příkazy.

Select-Object je výchozím omezením rutiny ve všech relacích JEA, který neumožňuje vyberte libovolné vlastnosti u objektů.
Bez omezení Select-Object používat ve funkcích, musí explicitně vyžádat toto plně implementováno zadáním FQMN.
Všechny rutiny omezené v relaci JEA produkovány stejné chování při vyvolání z funkce, v Powershellu [příkaz prioritu](https://msdn.microsoft.com/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).

Pokud vytváříte velké množství vlastních funkcí, může být jednodušší umístit je do [modul skriptu Powershellu](https://msdn.microsoft.com/library/dd878340(v=vs.85).aspx).
Potom můžete provést tyto funkce viditelné v relaci JEA pomocí pole VisibleFunctions stejně, jako byste s moduly integrované nebo od jiného výrobce.

## <a name="place-role-capabilities-in-a-module"></a>Funkce rolí místo v modulu

Aby Powershellu k vyhledání souboru funkce role musí být uložen ve složce "RoleCapabilities" v modulu prostředí PowerShell.
Modul mohou být uloženy v jakékoli složce součástí `$env:PSModulePath` proměnné prostředí, ale by neměly umístěte do System32 (vyhrazeno pro integrované moduly) nebo složce kde nedůvěryhodném, připojení uživatelů může upravit soubory.
Níže je příklad vytvoření základní modul skriptu Powershellu s názvem *ContosoJEA* v cestě "Program Files".

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

Zobrazit [Principy modul Powershellu](https://msdn.microsoft.com/library/dd878324.aspx) Další informace o moduly Powershellu, modul manifesty a proměnnou prostředí PSModulePath.

## <a name="updating-role-capabilities"></a>Aktualizace funkcí role


Soubor funkce role můžete kdykoli aktualizovat jednoduše ukládají se změny do souboru funkce role.
Všechny nové relace JEA spuštěna po aktualizaci role funkce bude odrážet revidovaná funkce.

To se dělá tak důležitý řízení přístupu ke složce funkce role.
Pouze vysoce důvěryhodných správců měl změnit soubory funkce role.
Pokud je nedůvěryhodný uživatel může změnit soubory funkce role, se můžete snadno sám si udělit přístup do rutin, které zajistí, aby zvýšení svých oprávnění.


Pro správce chtějí uzamčení přístupu k funkcím role zajistěte, aby že Local System má přístup pro čtení souborů funkce role a moduly obsahující.

## <a name="how-role-capabilities-are-merged"></a>Jak jsou sloučeny funkcí role

Uživatelé lze udělit přístup k více funkcí role při zadávání JEA relace v závislosti na roli mapování [relace konfigurační soubor](session-configurations.md).
Pokud k tomu dojde, pokusí se JEA dát uživateli *největšími* sadu příkazů, které jsou povolené všechny role.

**VisibleCmdlets a VisibleFunctions**

Většina komplexní logiku sloučení ovlivňuje rutiny a funkce, které mohou mít své parametry a jejich hodnoty v sadě nástrojů JEA omezené.

Pravidla jsou následující:

1. Pokud rutiny jsou dostupná jenom v jedné roli, bude viditelné pro uživatele s omezeními příslušný parametr.
2. Pokud rutiny jsou dostupná ve více než jednu roli, a Každá role má stejná omezení na rutinu, bude rutina viditelné pro uživatele s těmito omezeními.
3. Pokud rutiny jsou dostupná ve více než jednu roli, a každou roli umožňuje jinou sadu parametrů, rutiny a všechny parametry definovat v rámci každé role budou viditelné pro uživatele. Pokud jedna role nemá omezení pro parametry, povolí se všechny parametry.
4. Pokud jednu roli definuje sadu ověřit nebo ověřit model pro parametr rutiny, a jinou roli umožňuje parametru ale neomezuje hodnoty parametrů, ověřit set nebo vzor se bude ignorovat.
5. Pokud sada validate je definována pro stejný parametr rutiny ve více než jednu roli, povolí se všechny hodnoty ze všech sad ověřit.
6. Je-li ověřit vzor je definován pro stejný parametr rutiny ve více než jednu roli, povolí se všechny hodnoty, které se shodují s některým z tyto vzory se dají.
7. Je-li ověřit sada je definována v jedné nebo více rolím a ověřit vzor je definován v jiné roli pro stejný parametr rutiny, je ignorován sady ověřit a pravidlo (6) se vztahuje na zbývající vzory ověřit.

Níže je příklad, jak jsou sloučeny role podle těchto pravidel:

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



**VisibleExternalCommands ScriptsToProcess VisibleAliases VisibleProviders,**

Všechna ostatní pole v souboru funkce role se jednoduše přidají do kumulativní sadu povolených externích příkazů, aliasy, poskytovatelů a spouštěcí skripty.
Příkaz, alias, zprostředkovatel nebo skriptu, které jsou k dispozici v jedné role funkce bude k dispozici uživateli JEA.

Dejte pozor, abyste Ujistěte se, že kombinovanou sadu poskytovatelů z jedné role, funkce a rutiny/funkce/příkazy z jiného Nepovolit připojujících se uživatelů neúmyslnému přístupu k systémovým prostředkům.
Například pokud jedna role umožňuje `Remove-Item` rutina a další umožňuje `FileSystem` poskytovatele, vystavujete se riziku JEA uživatele odstraní libovolné soubory ve vašem počítači.
Další informace o určení efektivní oprávnění uživatelů najdete v [auditování JEA tématu](audit-and-report.md).

## <a name="next-steps"></a>Další kroky

- [Vytvoření konfiguračního souboru relace](session-configurations.md)