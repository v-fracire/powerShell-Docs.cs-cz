---
ms.date: 05/17/2018
keywords: prostředí PowerShell, core
title: Známé problémy pro Powershellu 6.0
ms.openlocfilehash: e3e718be903ff2223064d5790d3d0fe554ef04cd
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39267996"
---
# <a name="known-issues-for-powershell-60"></a>Známé problémy pro Powershellu 6.0

## <a name="known-issues-for-powershell-on-non-windows-platforms"></a>Známé problémy pro prostředí PowerShell na platformách než Windows

Alfa verze prostředí PowerShell v systému Linux a macOS se většinou funkční, ale jsou některé důležité omezení a problémů použitelnosti. Beta verzí powershellu v Linuxu a macOS je funkční a stabilní než alfa verze, ale stále může být chybí některé sadu funkcí a může obsahovat chyby. V některých případech se tyto problémy jsou jednoduše chyby, které nebyly byla opravena. V ostatních případech (jako výchozí aliasy pro ls, cp atd.), hledáme zpětnou vazbu od komunity týkající se možností neposkytujeme.

Poznámka: Obarvené mnoha podkladových subsystémy, prostředí PowerShell v systému Linux a macOS mají tendenci na stejné úrovni vyspělosti ve funkcích a chyby. S výjimkou toho, jak je uvedeno níže, problémů v této části se bude vztahovat na obou operačních systémech.

### <a name="case-sensitivity-in-powershell"></a>Rozlišování v prostředí PowerShell

Prostředí PowerShell v minulosti bylo rovnoměrně velkých a malých písmen, s několika výjimkami. Na bázi systému UNIX operačních systémů systém souborů je převážně malá a velká písmena a prostředí PowerShell dodržuje standardní systému souborů. To je přístupný prostřednictvím několika způsoby, jasné a není zřejmé.

#### <a name="directly"></a>Přímo

- Při zadávání souboru v prostředí PowerShell, musíte použít správnou velikost.

#### <a name="indirectly"></a>Nepřímo

- Pokud se skript pokusí se načíst modul a modul není správně formátováno název, se nezdaří načtení modulu. Pokud název, podle kterého se odkazuje v modulu neodpovídá skutečného názvu souboru, to může způsobit potíže s existujícími skripty.
- Dokončování pomocí tabulátoru – není automatické dokončování Pokud případě název souboru je nesprávný. Fragment pro dokončení musí být správně notaci. (Dokončení je velká a malá písmena pro název typu a dokončování členů typu.)

### <a name="ps1-file-extensions"></a>. PS1 Přípony souborů

Skripty prostředí PowerShell musí končit `.ps1` pro interpret pochopit, jak načíst a spustit v aktuálním procesu. Spouštění skriptů v aktuálním procesu je očekávané obvyklé chování pro prostředí PowerShell. `#!` Magické číslo může být přidán do skriptu, který nemá `.ps1` rozšíření, ale to způsobí, že skript ke spuštění v nové instanci prostředí PowerShell brání skript pracovní správně při zaměnitelnosti objekty. (Poznámka: to může být žádoucí, chování při spouštění skriptu PowerShell z `bash` nebo jiné prostředí.)

### <a name="missing-command-aliases"></a>Chybějící aliasy příkazů

V systému Linux, macOS, "aliasy pohodlí" pro základní příkazy `ls`, `cp`, `mv`, `rm`, `cat`, `man`, `mount`, `ps` byly odebrány. Prostředí PowerShell na Windows, poskytuje sadu aliasy, které mapují na názvy příkazů Linux ke zvýšení pohodlí uživatelů. Tyto aliasy byly odebrány z výchozího prostředí PowerShell v distribucích systému Linux, macOS, umožňuje nativní spustitelný soubor běžet bez zadání cesty.

Existují výhody a nevýhody to. Odebrání aliasy zpřístupní nativní příkaz prostředí PowerShell uživateli, ale zmenšuje funkce v prostředí, protože nativní příkazy vracet řetězce namísto objektů.

> [!NOTE]
> Toto je oblast, ve kterém hledá týmu prostředí PowerShell pro zpětnou vazbu.
> Co je preferovaným řešením? Nechte jsme to tak je, nebo přidejte aliasy pohodlí zpět? Zobrazit [vydat #929](https://github.com/PowerShell/PowerShell/issues/929).

### <a name="missing-wildcard-globbing-support"></a>Chybí zástupný znak (podpory zástupných znaků) podpory

Prostředí PowerShell v současné době pouze se rozšíření zástupného znaku (podpory zástupných znaků) pro integrované rutiny ve Windows a pro externí příkazy nebo binární soubory, jakož i rutiny v Linuxu. To znamená, že příkaz jako `ls
*.txt` selže, protože tak, aby odpovídaly názvy souborů nebudou rozbaleny hvězdičku. Můžete alternativně vyřešit pomocí tím `ls (gci *.txt | % name)` nebo jednoduše řečeno `gci *.txt` pomocí prostředí PowerShell předdefinované ekvivalent `ls`.

Zobrazit [#954](https://github.com/PowerShell/PowerShell/issues/954) říct nám zpětnou vazbu o tom, jak zlepšit možnosti podpory zástupných znaků v systému Linux/macOS.

### <a name="net-framework-vs-net-core-framework"></a>Rozhraní .NET framework a .NET Core Framework

Prostředí PowerShell v systému Linux nebo macOS pomocí .NET Core, který je podmnožinou úplné rozhraní .NET Framework na Microsoft Windows. To je důležité, protože PowerShell poskytuje přímý přístup k podkladové framework typy, metody atd. V důsledku toho skripty, které běží na Windows nebude fungovat na platformách než Windows vzhledem k rozdílům v rozhraní. Další informace o .NET Core Framework najdete v tématu <https://dotnetfoundation.org/net-core>

S nástupem [.NET Standard2.0](https://blogs.msdn.microsoft.com/dotnet/2016/09/26/introducing-net-standard/), .NET Core 2.0 přinese back řadu tradiční typy a metody k dispozici v plné verzi rozhraní .NET. To znamená, že PowerShell Core budete moct načíst mnoho tradiční moduly Windows Powershellu bez jakýchkoli úprav. Můžete postupovat podle našich .NET Standard 2.0 související pracovní [tady](https://github.com/PowerShell/PowerShell/projects/4).

### <a name="redirection-issues"></a>Problémům s přesměrováním

Přesměrování vstupu není podporována v prostředí PowerShell na libovolné platformě.
[Problém #1629](https://github.com/PowerShell/PowerShell/issues/1629)

Použití `Get-Content` k zápisu obsahu souboru do kanálu.

Přesměrovaný výstup bude obsahovat značku pořadí bajtů kódování Unicode (BOM), při použití výchozího kódování UTF-8. BOM způsobí problémy při práci s nástroji, které není pravděpodobné, že ho nebo při připojení k souboru. Použití `-Encoding Ascii` zapsat text ASCII (který, přičemž kódování Unicode, nebude mít BOM).

> [!Note]
> Zobrazit [RFC0020](https://github.com/PowerShell/PowerShell-RFC/issues/71) říct nám svůj názor na vylepšování kódování prostředí PowerShell Core na všech platformách. Snažíme se práce pro podporu UTF-8 bez BOM a potenciálně Změna kódování výchozí hodnoty pro různé rutiny napříč platformami.

### <a name="job-control"></a>Řízení projektu

Není dostupná podpora úlohy správy v prostředí PowerShell v systému Linux/macOS.
`fg` a `bg` příkazy nejsou k dispozici.

Prozatím, můžete použít [úloh Powershellu](/powershell/module/microsoft.powershell.core/about/about_jobs) které fungují na všech platformách.

### <a name="remoting-support"></a>Dokonalejší podpora vzdálené komunikace

V současné době PowerShell Core podporuje vzdálené komunikace prostředí PowerShell (PSRP) prostřednictvím služby WSMan se základním ověřováním v systémech macOS a Linux a pomocí ověřování protokolem NTLM v Linuxu. (Ověřování pomocí protokolu Kerberos se nepodporuje.)

Práce pro vzdálené komunikace založená na službě WSMan se provádí [psl omi zprostředkovatele](https://github.com/PowerShell/psl-omi-provider) úložiště.

PowerShell Core podporuje také vzdálené komunikace prostředí PowerShell (PSRP) přes protokol SSH na všech platformách (Windows, macOS a Linux). Zatímco aktuálně to není podporováno v produkčním prostředí, můžete další informace o nastavování [tady](../core-powershell/ssh-remoting-in-powershell-core.md).

### <a name="just-enough-administration-jea-support"></a>Podpora just dostatečně Administration (JEA)

Schopnost vytvářet omezené správu vzdálené komunikace (JEA) koncových bodů není aktuálně k dispozici v prostředí PowerShell v systému Linux/macOS. Tato funkce momentálně není v oboru pro 6.0 a něco posoudíme příspěvek 6.0 vyžaduje pracovní významné návrhu.

### <a name="sudo-exec-and-powershell"></a>`sudo`, `exec`a prostředí PowerShell

Protože prostředí PowerShell spouští většinu příkazů v paměti (jako je Python nebo Ruby), nelze použít sudo přímo pomocí prostředí PowerShell předdefinované. (Můžete samozřejmě spustit `powershell` z sudo.) Pokud je potřeba spustit rutinu prostředí PowerShell z v rámci prostředí PowerShell s příkazem sudo, například `sudo `Set-datum` 8/18/2016`, pak byste udělali `sudo powershell `Set-datum` 8/18/2016`. Podobně nelze exec Powershellu integrované přímo. Místo toho je nutné provést `exec powershell item_to_exec`.

Tento problém je právě sledován jako součást #3232.

### <a name="missing-cmdlets"></a>Chybějící rutiny

Velký počet příkazů (rutiny) běžně k dispozici v prostředí PowerShell nejsou k dispozici v systému Linux/macOS. V mnoha případech se tyto příkazy žádný smysl na těchto platformách (třeba Windows specifické funkce jako registru). Další příkazy, jako jsou příkazy pro řízení služby (Get/Start/Stop-Service) jsou k dispozici, ale není funkční. Budoucí verze bude opravte tyto problémy opravit porušení rutiny a přidání nové značky v čase.

### <a name="command-availability"></a>Dostupnost příkazu

Následující tabulka uvádí příkazy, které se ví, že fungují v prostředí PowerShell v systému Linux/macOS.

|Příkazy|Provozní stav|Poznámky|
|--------|-----------------|-----|
|`Get-Service`, `New-Service`, `Restart-Service`, `Resume-Service`, `Set-Service`, `Start-Service`, `Stop-Service`, `Suspend-Service`|Není k dispozici.|Tyto příkazy nebude rozpoznán. Tento problém by měl vyřešen v budoucí verzi.|
|`Get-Acl`, `Set-Acl`|Tato možnost není dostupná.|Tyto příkazy nebude rozpoznán. Tento problém by měl vyřešen v budoucí verzi.|
|`Get-AuthenticodeSignature`, `Set-AuthenticodeSignature`|Tato možnost není dostupná.|Tyto příkazy nebude rozpoznán. Tento problém by měl vyřešen v budoucí verzi.|
|`Wait-Process`|K dispozici, nebude fungovat správně. |Například "spustit proces gvim - PassThru | Wait – procesu nefunguje; Čekání na proces selže.|
|`Register-PSSessionConfiguration`, `Unregister-PSSessionConfiguration`, `Get-PSSessionConfiguration`|K dispozici ale nebude fungovat.|Zapisuje se chybová zpráva oznamující, že příkazy nefungují. Ty je třeba stanovit v budoucí verzi.|
|`Get-Event`, `New-Event`, `Register-EngineEvent`, `Register-WmiEvent`, `Remove-Event`, `Unregister-Event`|K dispozici, ale žádné zdroje událostí jsou k dispozici.|Zpracování událostí příkazy prostředí PowerShell jsou k dispozici, ale většina zdroje událostí používat s příkazy (například System.Timers.Timer) nejsou k dispozici v Linuxu, aby příkazy zbytečné ve verzi alfa.|
|`Set-ExecutionPolicy`|K dispozici ale nebude fungovat.|Vrátí zpráva není na této platformě podporována. Zásady spouštění jsou zaměřené na uživatele "bezpečnostního pásu", která pomáhá zabránit uživateli v provádění nákladné chyby. Není hranice zabezpečení.|
|`New-PSSessionOption`, `New-PSTransportOption`|K dispozici ale `New-PSSession` nebude fungovat.|`New-PSSessionOption` a `New-PSTransportOption` se k činnosti, které aktuálně neověřují `New-PSSession` funguje.|