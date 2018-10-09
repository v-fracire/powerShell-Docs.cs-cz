---
ms.date: 06/12/2017
keywords: jea, powershell, zabezpečení
title: Auditování a vytváření sestav funkce jea
ms.openlocfilehash: 2388c735840d8d3683aa8bc9869b9fb0371e5902
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851216"
---
# <a name="auditing-and-reporting-on-jea"></a>Auditování a vytváření sestav funkce jea

> Platí pro: Windows PowerShell 5.0

Po nasazení funkce JEA, budete pravidelně auditujte konfigurace JEA.
To vám pomůže vyhodnotit správných lidí máte přístup ke koncovému bodu JEA a pokud jsou stále vhodné jejich přiřazených rolí.

Toto téma popisuje různé způsoby, jak je můžete auditovat koncového bodu JEA.

## <a name="find-registered-jea-sessions-on-a-machine"></a>Najít registrovaný JEA relace na počítači

Chcete-li zkontrolovat, které JEA relací jsou registrované na počítači, použijte [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) rutiny.

```powershell
# Filter for sessions that are configured as 'RestrictedRemoteServer' to find JEA-like session configurations
PS C:\> Get-PSSessionConfiguration | Where-Object { $_.SessionType -eq 'RestrictedRemoteServer' }


Name          : JEAMaintenance
PSVersion     : 5.1
StartupScript :
RunAsUser     :
Permission    : CONTOSO\JEA_DNS_ADMINS AccessAllowed, CONTOSO\JEA_DNS_OPERATORS AccessAllowed, CONTOSO\JEA_DNS_AUDITORS AccessAllowed
```

Efektivní oprávnění pro koncový bod služby jsou uvedeny ve vlastnosti "Oprávnění".
Tito uživatelé mají práva k připojení ke koncovému bodu JEA, ale které role (a při rozšíření i pro příkazy) ke kterým mají přístup se určuje podle pole "RoleDefinitions" v [relace konfigurační soubor](session-configurations.md) , která byla použita k registraci koncový bod.

Můžete si vyzkoušet mapování role v registrovaných koncového bodu JEA tak, že rozbalíte data ve vlastnosti "RoleDefinitions".

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{ Name = 'Role Capabilities'; Expression = { $_.Value.RoleCapabilities } }
```

## <a name="find-available-role-capabilities-on-the-machine"></a>Hledání funkcí role k dispozici na počítači

Soubory pro funkce role pouze použije JEA v případě jsou uložené ve složce "RoleCapabilities" na platný modul prostředí PowerShell.
Všechny role funkce k dispozici v počítači najdete tak, že seznam dostupných modulů.

```powershell
function Find-LocalRoleCapability {
    $results = @()

    # Find modules with a "RoleCapabilities" subfolder and add any PSRC files to the result set
    Get-Module -ListAvailable | ForEach-Object {
        $psrcpath = Join-Path -Path $_.ModuleBase -ChildPath 'RoleCapabilities'
        if (Test-Path $psrcpath) {
            $results += Get-ChildItem -Path $psrcpath -Filter *.psrc
        }
    }

    # Format the results nicely to make it easier to read
    $results | Select-Object @{ Name = 'Name'; Expression = { $_.Name.TrimEnd('.psrc') }}, @{ Name = 'Path'; Expression = { $_.FullName }} | Sort-Object Name
}
```

> [!NOTE]
> Pořadí výsledky z této funkce není nutně pořadí, ve kterém bude vybrána funkce rolí, pokud více funkcí role sdílely stejný název.

## <a name="check-effective-rights-for-a-specific-user"></a>Zkontrolujte efektivní oprávnění pro konkrétního uživatele

Po nastavení koncového bodu JEA můžete chtít zkontrolovat, které příkazy v relaci JEA jsou k dispozici pro konkrétního uživatele.
Můžete použít [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) výčet všech příkazů pro uživatele by šlo spustit relaci JEA s jejich aktuální členství ve skupinách.
Výstup `Get-PSSessionCapability` stejná jako zadaný uživatel spustí `Get-Command -CommandType All` v relaci JEA.

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

Pokud uživatelé nejsou trvalé členy skupin, které by jim udělit další práva JEA, tuto rutinu nemusí odrážet tato další oprávnění.
To je obvykle tak při použití systémů správy privilegovaného přístupu just-in-time umožníte uživatelům dočasně patřit do skupiny zabezpečení.
Vždy pečlivě vyhodnoťte mapování uživatelů k rolím a obsah rolí, které se ujistěte se, že uživatelé jsou pouze získal přístup k minimální množství potřeba úspěšně vykonávat svoji práci.

## <a name="powershell-event-logs"></a>Protokoly událostí prostředí PowerShell

Pokud jste povolili modul a/nebo skript blokování protokolování v systému, budete moci vyhledat události v protokolu událostí Windows pro každý příkaz, který uživatel spustili v jejich JEA relace.
K vyhledání těchto událostí, otevřete Prohlížeč událostí Windows, přejděte na **Microsoft-Windows-PowerShell/Operational** protokolu událostí a vyhledejte události s ID události **4104**.

Každá položka protokolu událostí budou zahrnovat informace o relaci, ve kterém jste příkaz spustili.
JEA relacích, to obsahuje důležité informace o **ConnectedUser**, což je skutečné uživatele, který vytvořil JEA relace, stejně jako **Spustit_jako_uživatel** který identifikuje účet používaný JEA k Spusťte příkaz.
Protokoly událostí aplikace se zobrazí změny podle Spustit_jako_uživatel, takže nutnosti přepisů nebo povoleno protokolování modulu/script je důležité mít možnost vysledovat vyvolání konkrétní příkaz zpět na uživatele.

## <a name="application-event-logs"></a>Protokoly událostí aplikace

Při spuštění příkazu v relaci JEA vstupující do interakce s externí aplikace nebo služba může tyto aplikace protokolování událostí ve službě vlastní protokoly událostí.
Na rozdíl od Powershellu protokoly a záznamy o studiu jiné mechanismy protokolování nebude zachytávat připojeného uživatele relace JEA a místo toho pouze zaznamená virtuálního uživatele spustit jako nebo účet skupiny spravované služby.
Aby bylo možné zjistit, kdo spustil příkaz, musíte poradit [relace přepisu](#session-transcripts) nebo prostředí PowerShell protokoly událostí je možné korelovat s čas a prostředky uživatele zobrazeného v protokolu událostí aplikace.

Služba WinRM protokol také vám může pomoci sladit spustit jako uživatele v protokolu událostí aplikace s připojující se uživatel.
ID události **193** v **vzdálené správy Microsoft-Windows-Windows/Operational** protokolování záznamů identifikátor zabezpečení (SID) a účet název připojení na uživatele a spusťte jako uživatel pokaždé, když JEA je vytvořena relace.

## <a name="session-transcripts"></a>Záznamy o studiu relace

Pokud jste nakonfigurovali JEA řádné záznamy o studiu vytvořit pro každou relaci uživatele, text kopie každé uživatelské akce se uloží do zadané složky.

Chcete-li najít všechny adresáře přepisu, spusťte následující příkaz jako správce na počítači nakonfigurované JEA:

```powershell
Get-PSSessionConfiguration | Where-Object { $_.TranscriptDirectory -ne $null } | Format-Table Name, TranscriptDirectory
```

Každý přepisu se spustí s informacemi o čas spuštění relace, který uživatel připojený k relaci a která identita JEA byl přiřazen k nim.

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

V těle přepisu zaznamenaných informací o jednotlivých příkazech, které uživatel vyvolat.
Syntaxe příkazu, který spustil uživatel není k dispozici v relacích JEA kvůli způsobu, jakým jsou transformovány příkazy pro vzdálenou komunikaci prostředí PowerShell, ale stále můžete určit, účinný příkaz, který se spustil.
Níže je přepisu příklad fragmentu kódu od uživatele s `Get-Service Dns` v relaci JEA:

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

Pro každý příkaz, který uživatel spustí "CommandInvocation" řádku, bude napsán, popisující rutina nebo funkce uživatel vyvolat.
ParameterBindings postupujte podle jednotlivých CommandInvocation oznámením o každý parametr a hodnotu, která byla zadána pomocí příkazu.
V příkladu výše uvidíte, že zadaný parametr, který byl "Name" hodnota "Dns" pro rutinu "Get-Service".

Výstupní každý příkaz, spustí se tím taky CommandInvocation, obvykle na out-Buffer: výchozí.
InputObject Out-Default je vrácenou příkazem Objekt prostředí PowerShell.
Podrobnosti tohoto objektu jsou zobrazeny po zadání několika řádků níže, úzce tak napodobuje co byste viděli uživatele.

## <a name="see-also"></a>Viz taky

- [*Prostředí PowerShell ♥ modrý tým* blogový příspěvek o zabezpečení](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)
