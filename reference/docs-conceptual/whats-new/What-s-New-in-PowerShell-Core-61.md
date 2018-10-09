---
title: Co je nového v Powershellu Core 6.1
description: Nové funkce a změny v prostředí PowerShell Core 6.1
ms.date: 09/13/2018
ms.openlocfilehash: 4e39780a0ff446993005bba6284741f3b4b02549
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851303"
---
# <a name="whats-new-in-powershell-core-61"></a>Co je nového v Powershellu Core 6.1

Níže je výběr některé hlavní nové funkce a změny, které byly zavedeny v prostředí PowerShell Core 6.1.

K dispozici je také **tuny** z "nudné", která usnadňují rychlejší a stabilnější (plus velké a spoustu chyb) PowerShell!
Úplný seznam změn, podívejte se na naše [protokolu změn na Githubu](https://github.com/PowerShell/PowerShell/blob/master/CHANGELOG.md).

A při říkáme si některé názvy, Děkujeme, že vám [všechny přispěvatelé komunit](https://github.com/PowerShell/PowerShell/graphs/contributors) , provedli tato verze je to možné.

## <a name="net-core-21"></a>.NET core 2.1

PowerShell Core 6.1 přesunuta do .NET Core 2.1 poté, co byla [vydáno v květnu](https://blogs.msdn.microsoft.com/dotnet/2018/05/30/announcing-net-core-2-1/), což celou řadou vylepšení prostředí PowerShell, včetně:

- vylepšení výkonu (viz [níže](#performance-improvements))
- Podpora Alpine Linuxu (preview)
- [Podpora globálních nástroje .NET](/dotnet/core/tools/global-tools) – nadcházejících brzy do prostředí PowerShell
- [`Span<T>`](/dotnet/api/system.span-1?view=netcore-2.1)

## <a name="windows-compatibility-pack-for-net-core"></a>Windows Compatibility Pack for .NET Core

Na Windows, dodávané týmu .NET [Windows Compatibility Pack for .NET Core](https://blogs.msdn.microsoft.com/dotnet/2017/11/16/announcing-the-windows-compatibility-pack-for-net-core/), odebrat sadu sestavení, které přidají několik rozhraní API zpět do .NET Core ve Windows.

Přidali jsme Windows Compatibility Pack na verzi prostředí PowerShell Core 6.1 tak, aby všechny moduly nebo skripty, které pomocí těchto rozhraní API můžete spolehnout na nich nebudou dostupné.

PowerShell Core používat umožňuje Windows Compatibility Pack **více než 1900 rutiny, které se dodávají s Windows 10. října 2018 Update a Windows Server 2019**.

## <a name="support-for-application-whitelisting"></a>Podpora pro přidávání na seznam povolených aplikací

PowerShell Core 6.1 má se podporuje Windows PowerShell 5.1 [Applockeru](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/applocker/applocker-overview) a [Device Guard](https://docs.microsoft.com/en-us/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control) seznamu povolených aplikací.
Přidávání na seznam povolených aplikací umožňuje podrobnou kontrolu nad jaké binární soubory jsou mohou být provedeny pomocí prostředí PowerShell použít [režim omezené jazyka](https://blogs.msdn.microsoft.com/powershell/2017/11/02/powershell-constrained-language-mode/).

## <a name="performance-improvements"></a>Vylepšení výkonu

Windows Powershellu 6.0 provedli několik vylepšení výkonu.
PowerShell Core 6.1 neustále zlepšuje rychlost určité operace.

Například `Group-Object` byla urychlí 66 %:

```powershell
Measure-Command { 1..100000 | % {Get-Random -Minimum 1 -Maximum 10000} | Group-Object }
```

|              | Prostředí Windows PowerShell 5.1 | PowerShell Core 6.0 | PowerShell Core 6.1 |
|--------------|------------------------|---------------------|---------------------|
| Doba (sek)   | 25.178                 | 19.653              | 6.641               |
| Zrychlení (%) | Neužívá se.                    | % 21,9               | 66.2 %               |

Obdobně řazení scénáře, jako je tato vylepšili o více než 15 %:

```powershell
Measure-Command { 1..100000 | % {Get-Random -Minimum 1 -Maximum 10000} | Sort-Object }
```

|              | Prostředí Windows PowerShell 5.1 | PowerShell Core 6.0 | PowerShell Core 6.1 |
|--------------|------------------------|---------------------|---------------------|
| Doba (sek)   | 12.170                 | 8.493               | 7.08                |
| Zrychlení (%) | Neužívá se.                    | 30.2 %               | 16.6 %               |

`Import-Csv` má také byla urychlí výrazně po regrese z prostředí Windows PowerShell.
Test sdíleného svazku clusteru s 26,616 řádky a šest sloupců v následujícím příkladu:

```powershell
Measure-Command {$a = Import-Csv foo.csv}
```

|              | Prostředí Windows PowerShell 5.1 | PowerShell Core 6.0 | PowerShell Core 6.1    |
|--------------|------------------------|---------------------|------------------------|
| Doba (sek)   | 0.441                  | 1.069               | 0.268                  |
| Zrychlení (%) | Neužívá se.                    | -142.4 %             | 74.9 % (39.2 % WPS) |

A konečně, převodu z formátu JSON do `PSObject` má byla urychlí více než 50 % od prostředí Windows PowerShell.
Následující příklad používá soubor JSON ~ 2MB testu:

```powershell
Measure-Command {Get-Content .\foo.json | ConvertFrom-Json}
```

|              | Prostředí Windows PowerShell 5.1 | PowerShell Core 6.0 | PowerShell Core 6.1    |
|--------------|------------------------|---------------------|------------------------|
| Doba (sek)   | 0.259                  | 0.577               | 0,125                  |
| Zrychlení (%) | Neužívá se.                    | -122.8 %             | 78.3 % (51.7 % WPS) |

## <a name="check-system32-for-compatible-in-box-modules-on-windows"></a>Zkontrolujte `system32` kompatibilní modulů integrované ve Windows

V aktualizaci Windows 10 1809 a Windows Server 2019 jsme aktualizovali několik moduly Powershellu dodávané označit jako kompatibilní s PowerShell Core.

Při spuštění PowerShell Core 6.1, bude automaticky obsahovat `$windir\System32` jako součást `PSModulePath` proměnné prostředí.
Ale to zpřístupňuje pouze moduly, které `Get-Module` a `Import-Module` pokud jeho `CompatiblePSEdition` je označen jako kompatibilní se `Core`.


```powershell
Get-Module -ListAvailable
```

> [!NOTE]
> Může se zobrazit různé dostupné moduly v závislosti na tom, jaké role a funkce jsou nainstalovány.

```Output
...
    Directory: C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules

ModuleType Version    Name                                PSEdition ExportedCommands
---------- -------    ----                                --------- ----------------
Manifest   2.0.1.0    Appx                                Core,Desk {Add-AppxPackage, Get-AppxPackage, Get-AppxPacka...
Manifest   1.0.0.0    BitLocker                           Core,Desk {Unlock-BitLocker, Suspend-BitLocker, Resume-Bit...
Manifest   1.0.0.0    DnsClient                           Core,Desk {Resolve-DnsName, Clear-DnsClientCache, Get-DnsC...
Manifest   1.0.0.0    HgsDiagnostics                      Core,Desk {New-HgsTraceTarget, Get-HgsTrace, Get-HgsTraceF...
Binary     2.0.0.0    Hyper-V                             Core,Desk {Add-VMAssignableDevice, Add-VMDvdDrive, Add-VMF...
Binary     1.1        Hyper-V                             Core,Desk {Add-VMDvdDrive, Add-VMFibreChannelHba, Add-VMHa...
Manifest   2.0.0.0    NetAdapter                          Core,Desk {Disable-NetAdapter, Disable-NetAdapterBinding, ...
Manifest   1.0.0.0    NetEventPacketCapture               Core,Desk {New-NetEventSession, Remove-NetEventSession, Ge...
Manifest   2.0.0.0    NetLbfo                             Core,Desk {Add-NetLbfoTeamMember, Add-NetLbfoTeamNic, Get-...
Manifest   1.0.0.0    NetNat                              Core,Desk {Get-NetNat, Get-NetNatExternalAddress, Get-NetN...
Manifest   2.0.0.0    NetQos                              Core,Desk {Get-NetQosPolicy, Set-NetQosPolicy, Remove-NetQ...
Manifest   2.0.0.0    NetSecurity                         Core,Desk {Get-DAPolicyChange, New-NetIPsecAuthProposal, N...
Manifest   1.0.0.0    NetSwitchTeam                       Core,Desk {New-NetSwitchTeam, Remove-NetSwitchTeam, Get-Ne...
Manifest   1.0.0.0    NetWNV                              Core,Desk {Get-NetVirtualizationProviderAddress, Get-NetVi...
Manifest   2.0.0.0    TrustedPlatformModule               Core,Desk {Get-Tpm, Initialize-Tpm, Clear-Tpm, Unblock-Tpm...
...
```

K zobrazení všech modulů pomocí toto chování můžete přepsat `-SkipEditionCheck` přepnout parametru.
Přidali jsme také `PSEdition` vlastnost do tabulkového výstupu.

```powershell
Get-Module Net* -ListAvailable -SkipEditionCheck
```

```Output
    Directory: C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules

ModuleType Version    Name                        PSEdition ExportedCommands
---------- -------    ----                        --------- ----------------
Manifest   2.0.0.0    NetAdapter                  Core,Desk {Disable-NetAdapter, Disable-NetAdapterBinding, ...
Manifest   1.0.0.0    NetConnection               Core,Desk {Get-NetConnectionProfile, Set-NetConnectionProf...
Manifest   1.0.0.0    NetDiagnostics              Desk      Get-NetView
Manifest   1.0.0.0    NetEventPacketCapture       Core,Desk {New-NetEventSession, Remove-NetEventSession, Ge...
Manifest   2.0.0.0    NetLbfo                     Core,Desk {Add-NetLbfoTeamMember, Add-NetLbfoTeamNic, Get-...
Manifest   1.0.0.0    NetNat                      Core,Desk {Get-NetNat, Get-NetNatExternalAddress, Get-NetN...
Manifest   2.0.0.0    NetQos                      Core,Desk {Get-NetQosPolicy, Set-NetQosPolicy, Remove-NetQ...
Manifest   2.0.0.0    NetSecurity                 Core,Desk {Get-DAPolicyChange, New-NetIPsecAuthProposal, N...
Manifest   1.0.0.0    NetSwitchTeam               Core,Desk {New-NetSwitchTeam, Remove-NetSwitchTeam, Get-Ne...
Manifest   1.0.0.0    NetTCPIP                    Core,Desk {Get-NetIPAddress, Get-NetIPInterface, Get-NetIP...
Manifest   1.0.0.0    NetWNV                      Core,Desk {Get-NetVirtualizationProviderAddress, Get-NetVi...
Manifest   1.0.0.0    NetworkConnectivityStatus   Core,Desk {Get-DAConnectionStatus, Get-NCSIPolicyConfigura...
Manifest   1.0.0.0    NetworkSwitchManager        Core,Desk {Disable-NetworkSwitchEthernetPort, Enable-Netwo...
Manifest   1.0.0.0    NetworkTransition           Core,Desk {Add-NetIPHttpsCertBinding, Disable-NetDnsTransi...
```

Další informace o tomto chování najdete [PowerShell RFC0025](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0025-PSCore6-and-Windows-Modules.md).

## <a name="markdown-cmdlets-and-rendering"></a>Rutiny markdown a vykreslování

Markdown je standardní způsob vytváření dokumentů čitelné ve formátu prostého textu se základní formátování, které lze vykreslit do kódu HTML.

Přidali jsme některé rutiny v 6.1, která vám umožní převést a vykreslování Markdownu dokumentů v konzole, včetně:

- `ConvertFrom-Markdown`
- `Get-MarkdownOption`
- `Set-MarkdownOption`
- `Show-Markdown`

Například `Show-Markdown` vykreslí souboru Markdownu v konzole:

![Příklad Markdownu show](./images/markdown_example.png)

Další informace o tom, jak tyto rutiny fungují, přečtěte si [tento dokument RFC](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0025-Native-Markdown-Rendering.md).

## <a name="experimental-feature-flags"></a>Příznaky experimentální funkce

Příznaky experimentální funkce povolit uživatele, aby na funkce, které nebyly byla dokončena.
Tyto experimentální funkce nejsou podporované a může obsahovat chyby.

Další informace o této funkci v [PowerShell RFC0029](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0029-Support-Experimental-Features.md).

## <a name="web-cmdlet-improvements"></a>Vylepšení webového rutiny

K [ @markekraus ](https://github.com/markekraus), celý slew vylepšení byly provedeny na náš web rutiny: [`Invoke-WebRequest`](/powershell/module/microsoft.powershell.utility/invoke-webrequest)
a [ `Invoke-RestMethod` ](/powershell/module/microsoft.powershell.utility/invoke-restmethod).

- [Žádost o přijetí změn #6109](https://github.com/PowerShell/PowerShell/pull/6109) – výchozí kódování sady na UTF-8 pro `application-json` odpovědi
- [Žádost o přijetí změn #6018](https://github.com/PowerShell/PowerShell/pull/6018)  -  `-SkipHeaderValidation` parametr umožňující `Content-Type` hlavičky, které nejsou kompatibilní se standardy
- [Žádosti o přijetí změn #5972](https://github.com/PowerShell/PowerShell/pull/5972)  -  `Form` parametr pro podporu zjednodušená `multipart/form-data` podpory
- [Žádost o přijetí změn #6338](https://github.com/PowerShell/PowerShell/pull/6338) – vyhovují řadě požadavků a velkých a malých písmen zpracování klíčů relace
- [Žádost o přijetí změn #6447](https://github.com/PowerShell/PowerShell/pull/6447) – přidání `-Resume` parametr pro rutiny webových

## <a name="remoting-improvements"></a>Vylepšení vzdálené komunikace

### <a name="powershell-direct-for-containers-tries-to-use-powershell-core-first"></a>Přímou službu PowerShell for Containers se pokusí nejprve použít PowerShell Core

[Přímou službu PowerShell](/virtualization/hyper-v-on-windows/user-guide/powershell-direct) funkce je součástí prostředí PowerShell a technologie Hyper-V, který umožňuje připojení k virtuálnímu počítači Hyper-V nebo kontejneru bez připojení k síti nebo jiné služby pro vzdálenou správu.

V minulosti přímou službu PowerShell připojené pomocí prostředí Windows PowerShell instance doručené pošty v kontejneru.
Nyní, přímou službu PowerShell se nejprve pokusí připojit pomocí všechny dostupné `pwsh.exe` na `PATH` proměnné prostředí.
Pokud `pwsh.exe` není k dispozici, přímou službu PowerShell spadne zpět na použití `powershell.exe`.

### <a name="enable-psremoting-now-creates-separate-remoting-endpoints-for-preview-versions"></a>`Enable-PSRemoting` nyní vytvoří samostatné vzdálené komunikace koncové body pro verze preview

`Enable-PSRemoting` nyní vytvoří dvě konfigurace vzdálené komunikace relace:

- Jeden pro hlavní verzi prostředí PowerShell. Například`PowerShell.6`. Tento koncový bod, který lze dovolávat napříč vedlejší verze aktualizace jako konfiguraci relace prostředí PowerShell 6 "celosystémovým"
- Jednu konfiguraci relace specifické pro verzi, například: `PowerShell.6.1.0`

Toto chování je užitečné, pokud chcete mít více verzí Powershellu 6 nainstalovaná a přístupná na stejném počítači.

Kromě toho ve verzi preview verzí Powershellu teď mít své vlastní vzdálené komunikace konfiguracím relací po spuštění `Enable-PSRemoting` rutiny:

```powershell
C:\WINDOWS\system32> Enable-PSRemoting
```

Výstup může lišit, pokud jste nenastavili WinRM před.

```Output
WinRM is already set up to receive requests on this computer.
WinRM is already set up for remote management on this computer.
```

Pak můžete zobrazit samostatné konfigurace relace Powershellu ve verzi Preview a stabilní verze sestavení Powershellu 6 a u každé konkrétní verze.

```powershell
Get-PSSessionConfiguration
```

```Output
Name          : PowerShell.6.2-preview.1
PSVersion     : 6.2
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : PowerShell.6-preview
PSVersion     : 6.2
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : powershell.6
PSVersion     : 6.1
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : powershell.6.1.0
PSVersion     : 6.1
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed
```

### <a name="userhostport-syntax-supported-for-ssh"></a>`user@host:port` Syntaxe podporovaných pro SSH

SSH klienti obvykle podporují připojovací řetězec ve formátu `user@host:port`.
Přidání SSH jako protokol pro vzdálenou komunikaci prostředí PowerShell přidali jsme podporu pro tento formát připojovacího řetězce:

`Enter-PSSession -HostName fooUser@ssh.contoso.com:2222`

## <a name="msi-option-to-add-explorer-shell-context-menu-on-windows"></a>Možnost Instalační služby MSI pro přidání místní nabídky prostředí Průzkumníka Windows

K [ @bergmeister ](https://github.com/bergmeister), teď můžete povolit kontextovou nabídku Windows. Nyní můžete otevřít 6.1 prostředí PowerShell pro vaši instalaci systémová z libovolné složky v Průzkumníku Windows:

![Místní nabídka Shell pro PowerShell 6](./images/shell_context_menu.png)

## <a name="goodies"></a>Užitečné nástroje

### <a name="run-as-administrator-in-the-windows-shortcut-jump-list"></a>"Spustit jako správce" v seznamu odkazů místní Windows

K [ @bergmeister ](https://github.com/bergmeister), seznam odkazů na zástupce Powershellu Core teď obsahuje "Spustit jako správce":

![Spustit jako správce v seznamu skok PowerShell 6](./images/jumplist.png)

### <a name="cd---returns-to-previous-directory"></a>`cd -` Vrátí předchozí adresář

```powershell
C:\Windows\System32> cd C:\
C:\> cd -
C:\Windows\System32>
```

Nebo v Linuxu:

```ShellSession
PS /etc> cd /usr/bin
PS /usr/bin> cd -
PS /etc>
```

Navíc `cd` a `cd --` změnit na `$HOME`.

### `Test-Connection`

K [ @iSazonov ](https://github.com/iSazonov), [ `Test-Connection` ](/powershell/module/microsoft.powershell.management/test-connection) rutiny má byla přenést do prostředí PowerShell Core.

### <a name="update-help-as-non-admin"></a>`Update-Help` jako bez oprávnění správce.

Zabývajících `Update-Help` už nebude potřeba spustit jako správce.
`Update-Help` Teď výchozí ukládání nápovědy do složky s rozsahem uživatele.

### <a name="new-methodsproperties-on-pscustomobject"></a>Nové metody/vlastnosti `PSCustomObject`

K [ @iSazonov ](https://github.com/iSazonov), přidali jsme nové metody a vlastnosti, které chcete `PSCustomObject`.
`PSCustomObject` nyní zahrnuje `Count` / `Length` vlastnost jako u jiných objektů.

```powershell
$PSCustomObject = [pscustomobject]@{foo = 1}

$PSCustomObject.Length
```

```Output
1
```

```powershell
$PSCustomObject.Count
```

```Output
1
```

Tato práce zahrnuje také `ForEach` a `Where` metody, která umožňují jeho provoz a vyfiltrujte `PSCustomObject` položky:

```powershell
$PSCustomObject.ForEach({$_.foo + 1})
```

```Output
2
```

```powershell
$PSCustomObject.Where({$_.foo -gt 0})
```

```Output
foo
---
  1
```

### `Where-Object -Not`

K @SimonWahlin, přidali jsme `-Not` parametr `Where-Object`.
Teď můžete filtrovat objektu na kanál bez existuje, nebo hodnotu vlastnosti null nebo je prázdný.

Tento příkaz například vrátí všechny služby, které nemají definované všechny závislé služby:

```powershell
Get-Service | Where-Object -Not DependentServices
```

### <a name="new-modulemanifest-creates-a-bom-less-utf-8-document"></a>`New-ModuleManifest` Vytvoří dokument bez BOM kódování UTF-8

Přesun věnovat bez BOM kódování UTF-8 v Powershellu 6.0, jsme aktualizovali `New-ModuleManifest` rutina pro vytvoření dokumentu bez BOM kódování UTF-8 namísto UTF-16, jeden.

### <a name="conversions-from-psmethod-to-delegate"></a>Převody z PSMethod delegáta

K [ @powercode ](https://github.com/powercode), teď podporujeme převodu `PSMethod` delegátovi.
Díky tomu můžete provést třeba k předávání `PSMethod` `[M]::DoubleStrLen` jako hodnotu delegáta do `[M]::AggregateString`:

```powershell
class M {
    static [int] DoubleStrLen([string] $value) { return 2 * $value.Length }

    static [long] AggregateString([string[]] $values, [func[string, int]] $selector) {
        [long] $res = 0
        foreach($s in $values){
            $res += $selector.Invoke($s)
        }
        return $res
    }
}

[M]::AggregateString((gci).Name, [M]::DoubleStrLen)
```

Další informace o této změně, projděte si [žádosti o přijetí změn #5287](https://github.com/PowerShell/PowerShell/pull/5287).

### <a name="standard-deviation-in-measure-object"></a>Směrodatná odchylka `Measure-Object`

K [ @CloudyDino ](https://github.com/CloudyDino), přidali jsme `StandardDeviation` vlastnost `Measure-Object`:

```powershell
Get-Process | Measure-Object -Property CPU -AllStats
```

```Output
Count             : 308
Average           : 31.3720576298701
Sum               : 9662.59375
Maximum           : 4416.046875
Minimum           :
StandardDeviation : 264.389544720926
Property          : CPU
```

### `GetPfxCertificate -Password`

K [ @maybe-hello-world ](https://github.com/maybe-hello-world), `Get-PfxCertificate` má teď `Password` parametr, který přijímá `SecureString`. To umožňuje používat neinteraktivně:

```powershell
$certFile = '\\server\share\pwd-protected.pfx'
$certPass = Read-Host -AsSecureString -Prompt 'Enter the password for certificate: '

$certThumbPrint = (Get-PfxCertificate -FilePath $certFile -Password $certPass ).ThumbPrint
```

### <a name="removal-of-the-more-function"></a>Odebrání `more` – funkce

V minulosti, prostředí PowerShell dodané funkci v Windows volá `more` , která zabalena `more.com`.
Tato funkce se odebralo.

Také `help` funkce změněn, aby používal `more.com` na Windows nebo v systému výchozí operátor určené `$env:PAGER` na platformách než Windows.

### <a name="cd-drivename-now-returns-users-to-the-current-working-directory-in-that-drive"></a>`cd DriveName:` nyní vrátí uživatele do aktuálního pracovního adresáře na tomto disku

Dříve, pomocí `Set-Location` nebo `cd` se vraťte do PSDrive uživatelům odesílat výchozí umístění pro tuto jednotku.

K [ @mcbobke ](https://github.com/mcbobke), uživatelům se nyní odesílají na poslední známé aktuální pracovní adresář pro danou relaci.

### <a name="windows-powershell-type-accelerators"></a>Akcelerátory typ prostředí Windows PowerShell

V prostředí Windows PowerShell jsme zahrnuli následující typ akcelerátory usnadnit práci s jejich odpovídající typy:

- `[adsi]`: `System.DirectoryServices.DirectoryEntry`
- `[adsisearcher]`: `System.DirectoryServices.DirectorySearcher`
- `[wmi]`: `System.Management.ManagementObject`
- `[wmiclass]`: `System.Management.ManagementClass`
- `[wmisearcher]`: `System.Management.ManagementObjectSearcher`

Tyto klávesové zkratky typu nejsou zahrnuty v Powershellu 6, ale byly přidány do prostředí PowerShell 6.1 a systémem Windows.

Tyto typy jsou užitečné pro snadné vytváření AD a objekty rozhraní WMI.

Například můžete zadávat dotazy pomocí protokolu LDAP:

```powershell
[adsi]'LDAP://CN=FooUse,OU=People,DC=contoso,DC=com'
```

Následující příklad vytvoří objekt Win32_OperatingSystem CIM:

```powershell
[wmi]"Win32_OperatingSystem=@"
```

```Output
SystemDirectory : C:\WINDOWS\system32
Organization    : Contoso IT
BuildNumber     : 18234
RegisteredUser  : Contoso Corp.
SerialNumber    : 12345-67890-ABCDE-F0123
Version         : 10.0.18234
```

V tomto příkladu vrátí objekt ManagementClass Win32_OperatingSystem třídy.

```powershell
[wmiclass]"Win32_OperatingSystem"
```

```Output
   NameSpace: ROOT\cimv2

Name                                Methods              Properties
----                                -------              ----------
Win32_OperatingSystem               {Reboot, Shutdown... {BootDevice, BuildNumber, BuildType, Caption...}
```

### <a name="-lp-alias-for-all--literalpath-parameters"></a>`-lp` alias pro všechny `-LiteralPath` parametry

K [ @kvprasoon ](https://github.com/kvprasoon), nyní je k dispozici alias parametru `-lp` pro všechny integrované rutiny Powershellu, které mají `-LiteralPath` parametru.

## <a name="breaking-changes"></a>Rozbíjející změny v

### <a name="msi-based-installation-paths-on-windows"></a>Instalace pomocí MSI cesty ve Windows

Na Windows nyní balíček MSI instaluje do následujícího umístění:

- `$env:ProgramFiles\PowerShell\6\` pro stabilní instalaci 6.x
- `$env:ProgramFiles\PowerShell\6-preview\` pro instalaci preview 6.x

Tato změna zajišťuje PowerShell Core může být aktualizován/obsluhovány pomocí Microsoft Update.

Další informace, podívejte se na [PowerShell RFC0026](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0026-MSI-Installation-Path.md).

### <a name="telemetry-can-only-be-disabled-with-an-environment-variable"></a>Telemetrie se dá deaktivovat jenom s proměnnou prostředí

PowerShell Core odesílá základní telemetrická data do Microsoftu při jeho spuštění. Data obsahují název operačního systému, verze operačního systému a verze prostředí PowerShell. Tato data umožňují nám lépe pochopit prostředí, ve kterém se používá prostředí PowerShell a umožňuje nám to určit prioritu nových funkcí a oprav.

Odhlásit z této telemetrická data, nastavte proměnnou prostředí `POWERSHELL_TELEMETRY_OPTOUT` k `true`, `yes`, nebo `1`. Odstranění souboru už nadále nepodporujeme `DELETE_ME_TO_DISABLE_CONSOLEHOST_TELEMETRY` zakázat telemetrii.

### <a name="disallowed-basic-auth-over-http-in-powershell-remoting-on-unix-platforms"></a>Zakázané základního ověřování prostřednictvím protokolu HTTP při vzdálené komunikaci Powershellu na platformách systému Unix

Zabránit používání nešifrované přenosy, vzdálené komunikace Powershellu na platformy Unix nyní vyžaduje použití protokolu NTLM nebo Negotiate, nebo HTTPS.

Další informace o těchto změnách, přečtěte si [problém #6779](https://github.com/PowerShell/PowerShell/issues/6779).

### <a name="removed-visualbasic-as-a-supported-language-in-add-type"></a>Odebrat `VisualBasic` jako podporovaný jazyk v Add-Type

V minulosti by mohla kompilaci kódu pomocí jazyka Visual Basic `Add-Type` rutiny.
Jen zřídka se používá jazyka Visual Basic s `Add-Type`. Odebrali jsme tato změna povede ke zmenšení velikosti prostředí PowerShell.

### <a name="cleaned-up-uses-of-commandtypesworkflow-and-workflowinfocleaned"></a>Vyčištění použití `CommandTypes.Workflow` a `WorkflowInfoCleaned`

Další informace o těchto změnách, přečtěte si [žádosti o přijetí změn #6708](https://github.com/PowerShell/PowerShell/pull/6708).
