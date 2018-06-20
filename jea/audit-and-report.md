---
ms.date: 06/12/2017
keywords: jea, prostředí powershell, zabezpečení
title: Auditování a vytváření sestav na JEA
ms.openlocfilehash: e68206cd6fe94c51507f42ae2c3e6702f6fd4e0f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188848"
---
# <a name="auditing-and-reporting-on-jea"></a>Auditování a vytváření sestav na JEA

> Platí pro: prostředí Windows PowerShell 5.0

Poté, co nasadíte JEA, budete chtít pravidelně audit JEA konfigurace.
To vám pomůže vyhodnotit, pokud oprávnění uživatelé mají přístup ke koncovému bodu JEA a jejich přiřazené role jsou stále vhodné.

Toto téma popisuje různé způsoby, kterými můžete auditovat koncový bod JEA.

## <a name="find-registered-jea-sessions-on-a-machine"></a>Najít registrovaný JEA relací na počítači

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

Efektivní práva pro koncový bod jsou uvedeny ve vlastnosti "Oprávnění".
Tito uživatelé mají práva k připojení k JEA koncového bodu, ale které role (a při rozšíření příkazy) mají přístup je určen v poli "RoleDefinitions" [relace konfigurační soubor](session-configurations.md) která byla použita k registraci koncový bod.

Mapování role na koncový bod registrovaný JEA můžete vyhodnotit rozšířením dat ve vlastnosti "RoleDefinitions".

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{ Name = 'Role Capabilities'; Expression = { $_.Value.RoleCapabilities } }
```

## <a name="find-available-role-capabilities-on-the-machine"></a>Najít možnosti dostupné role na počítači

Soubory schopnosti role se použít pomocí JEA jen v případě, že jsou uložené ve složce "RoleCapabilities" uvnitř platný modul prostředí PowerShell.
Všechny role možnosti dostupné v počítači můžete najít tak, že seznamu dostupných modulů.

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
> Pořadí výsledky z tato funkce není nutně pořadí, ve kterém bude vybrána funkce role, pokud více možností role sdílejí stejný název.

## <a name="check-effective-rights-for-a-specific-user"></a>Zaškrtněte políčko efektivní práva pro konkrétního uživatele

Jakmile nastavíte koncový bod JEA, můžete zkontrolovat, které příkazy v relaci JEA jsou k dispozici pro konkrétního uživatele.
Můžete použít [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) výčet všechny příkazy pro uživatele, pokud by byly spustit relaci JEA s jejich aktuální členství ve skupinách.
Výstup `Get-PSSessionCapability` je shodná s zadaný uživatel, který spouští `Get-Command -CommandType All` v relaci JEA.

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

Pokud vaši uživatelé nejsou členy skupin, které by jim udělit další práva JEA, tato rutina nemusí odrážet tato další oprávnění.
To je obvykle případ, kdy pomocí systémy správy privilegovaného přístupu za běhu, aby uživatelé mohli dočasně patří do skupiny zabezpečení.
Vždycky pečlivě vyhodnoťte mapování uživatelů k rolím a obsah každou roli, aby uživatelé jsou pouze získávají přístup k minimem příkazy potřebné pro svou práci úspěšně.

## <a name="powershell-event-logs"></a>Protokoly událostí prostředí PowerShell

Pokud jste povolili modulu nebo skriptu bloku protokolování v systému, bude možné najít události v protokolech událostí systému Windows pro každý příkaz, který uživatel spustil v jejich JEA relace.
Pokud chcete vyhledat tyto události, otevřete Prohlížeč událostí systému Windows, přejděte na **Microsoft-Windows-PowerShell/Operational** protokol událostí a podívejte se na události s ID události **4104**.

Každá položka protokolu událostí bude obsahovat informace o relaci, ve kterém byl spuštěn příkaz.
Pro relace JEA to zahrnuje důležité informace o **ConnectedUser**, což je skutečný uživatele, který vytvořil JEA relace, společně s **Spustit_jako_uživatel** který identifikuje účet JEA použitý k spustíte příkaz.
Záznamy událostí aplikace se zobrazí změny podle Spustit_jako_uživatel, takže s přepisy nebo skriptování či modulu protokolování je zásadní moct trasování volání konkrétní příkaz zpět na uživatele.

## <a name="application-event-logs"></a>Záznamy událostí aplikace

Při spuštění příkazu v relaci JEA, která interaguje s externí aplikace nebo služba, mohou tyto aplikace protokolování událostí do své vlastní protokoly událostí.
Na rozdíl od protokoly prostředí PowerShell a přepisy jiným mechanismem protokolování nebude zachytávat připojených uživatelů JEA relace a bude místo toho pouze virtuální spustit jako účet uživatele nebo skupiny spravované služby.
Aby bylo možné zjistit, kdo příkaz spustili, budete muset obrátit [relace přepis](#session-transcripts) nebo korelovat protokoly událostí prostředí PowerShell s a uživatel vidět v protokolu událostí aplikace.

WinRM protokolu rovněž umožňuje korelovat spustit jako uživatele v protokolu událostí aplikace s připojující se uživatel.
ID události **193** v **Operational vzdálené správy Microsoft-Windows-Windows** protokolování záznamů identifikátor zabezpečení (SID) a účet name pro připojování uživatele a spustit jako uživatele pokaždé, když JEA relace je vytvořena.

## <a name="session-transcripts"></a>Přepisy relace

Pokud jste nakonfigurovali JEA k vytvoření přepis pro každou relaci uživatele, text kopii každého uživatele akce se uloží v zadané složce.

Pokud chcete najít všechny adresáře přepis, spusťte následující příkaz v počítači jako správce konfigurace JEA:

```powershell
Get-PSSessionConfiguration | Where-Object { $_.TranscriptDirectory -ne $null } | Format-Table Name, TranscriptDirectory
```

Každý přepis začíná informace o čas spuštění relace, které uživatel připojený k relaci a které identity JEA byl přiřazen k nim.

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

V těle zápis je do něj protokolují informace o každém příkazu uživatel vyvolat.
Přesná syntaxe příkazu, který spustil uživatele je k dispozici v relacích JEA z důvodu způsob, jakým jsou transformovány příkazy pro vzdálenou komunikaci prostředí PowerShell, ale stále můžete určit efektivní příkaz, který byl proveden.
Níže je fragment kódu příklad přepis od uživatele s `Get-Service Dns` v relaci JEA:

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

U každého příkazu, který uživatel spustí řádek "CommandInvocation" bude zapsán, popisující rutinu nebo funkce uživatel vyvolat.
ParameterBindings podle jednotlivých CommandInvocation získat informace o jednotlivých parametr a hodnotu, která byla zadaná pomocí příkazu.
V předchozím příkladu uvidíte, že parametr, který byl "Název" poskytnutá hodnota "Dns" pro rutinu "Get-Service".

Výstup každé příkazu se také aktivuje CommandInvocation, obvykle odesílací výchozí.
InputObject Out-Default je objekt prostředí PowerShell vrátí z příkazu.
Podrobnosti tohoto objektu se tisknou pár řádků níže úzce mimicking, co by mohli vidět uživatele.

## <a name="see-also"></a>Viz taky

- [Akce auditování uživatele v relaci JEA](audit-and-report.md)
- [*Prostředí PowerShell ♥ týmem Blue* příspěvku na blogu na zabezpečení](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)