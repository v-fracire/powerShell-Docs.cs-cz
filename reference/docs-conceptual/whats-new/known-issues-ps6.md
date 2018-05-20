---
ms.date: 05/17/2018
keywords: prostředí PowerShell, jádra
title: Známé problémy pro prostředí PowerShell 6.0
ms.openlocfilehash: 6ad1bcaf1de06f204b57eb8ce23b3053ba4a5b38
ms.sourcegitcommit: 2d9cf1ccb9a653db7726a408ebcb65530dcb1522
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/19/2018
---
# <a name="known-issues-for-powershell-60"></a>Známé problémy pro prostředí PowerShell 6.0

## <a name="known-issues-for-powershell-on-non-windows-platforms"></a>Známé problémy pro prostředí PowerShell na jiných platforem než Windows

Alfa verze prostředí PowerShell v systému macOS systémy Linux a jsou většinou funkční, ale mají některé důležité omezení a problémech s použitelností. Beta verze prostředí PowerShell v systému Linux a systému macOS jsou funkční a stabilní než alfa verze, ale stále může být postrádá některé sadu funkcí a může obsahovat chyby. V některých případech se tyto problémy jsou jednoduše chyby, které nebyly byl opraven. V ostatních případech (jako výchozí aliasy pro ls, cp atd.), jsme hledáte zpětnou vazbu od komunity týkající se možnosti uděláme.

Poznámka: Z důvodu podobnosti základní subsystémů, prostředí PowerShell v systému Linux a systému macOS zpravidla na stejné úrovni vyspělosti v funkcí a chyby. S výjimkou toho, jak je uvedeno níže, problémy v této části se uplatní na obou operačních systémů.

### <a name="case-sensitivity-in-powershell"></a>Rozlišování v prostředí PowerShell

Prostředí PowerShell v minulosti byl jednotně velká a malá písmena, s několika výjimkami. V operačních systémech UNIX jako systém souborů je převážně velká a malá písmena a prostředí PowerShell dodržuje standard systému souborů. Toto jsou dostupné prostřednictvím mnoha způsoby, zjevnější a není zřejmé.

#### <a name="directly"></a>přímo

- Při zadání soubor v prostředí PowerShell, se musí použít správnou velikost.

#### <a name="indirectly"></a>Nepřímo

- Pokud se skript pokusí načíst modul a na název modulu není použita správně, pak se nezdaří načtení modulu. Pokud název, podle kterého se odkazuje v modulu neshoduje s názvem skutečný soubor může dojít k potížím s existující skripty.
- Karta dokončení není automatické dokončování Pokud případ název souboru je nesprávný. Fragment k dokončení musí být použita správně. (Dokončení je velká a malá písmena pro název typu a typ člena dokončených.)

### <a name="ps1-file-extensions"></a>. PS1. přípony souborů

Skripty prostředí PowerShell musí končit `.ps1` pro překladač pochopit, jak načíst a spustit v aktuálním procesu. Spouštění skriptů v aktuálním procesu je očekávané obvyklé chování pro prostředí PowerShell. `#!` Magické číslo mohou být přidány do skript, který nemá `.ps1` rozšíření, ale to způsobí, že skript, který chcete spustit v nové instanci prostředí PowerShell brání skript pracovní správně při zaměnitelnosti objekty. (Poznámka: může to být žádoucí chování při provádění skriptu prostředí PowerShell z `bash` nebo jiné prostředí.)

### <a name="missing-command-aliases"></a>Chybějící aliasy příkazů

V systému Linux nebo systému macOS, "aliasy pohodlí" pro základní příkazy `ls`, `cp`, `mv`, `rm`, `cat`, `man`, `mount`, `ps` byly odebrány. V systému Windows prostředí PowerShell poskytuje sadu aliasy, které jsou mapovány na názvy příkazů Linux ke zvýšení pohodlí uživatelů. Tyto aliasy byly odebrány z výchozí prostředí PowerShell v systému Linux nebo macOS distribuce, povolení nativní spustitelný soubor běžela bez zadání cesty.

Existují výhody a nevýhody na to. Odebrání zástupci zpřístupní nativní příkaz prostředí PowerShell uživateli, ale snižuje funkčnost v prostředí, protože nativní příkazy vracet řetězce místo objekty.

> [!NOTE]
> Toto je oblast, kde týmem prostředí PowerShell hledá zpětnou vazbu.
> Co je upřednostňovaný řešení? Měli jsme necháte nebo přidat zpět zástupci pohodlí? V tématu [vydání #929](https://github.com/PowerShell/PowerShell/issues/929).

### <a name="missing-wildcard-globbing-support"></a>Chybí zástupný znak (expanze názvů) podpory

Prostředí PowerShell v současné době pouze se rozšíření zástupného znaku (expanze názvů) pro integrované rutiny ve Windows a externích příkazů nebo binární soubory, jakož i rutiny v systému Linux. To znamená, že příkaz jako `ls
*.txt` selže, protože tak, aby odpovídaly názvy souborů nebudou rozbaleny hvězdičku. Můžete obejít tím nástrojem `ls (gci *.txt | % name)` nebo více jednoduše `gci *.txt` pomocí předdefinovaných ekvivalent prostředí PowerShell k `ls`.

V tématu [#954](https://github.com/PowerShell/PowerShell/issues/954) poskytněte nám o tom, jak vylepšit expanze názvů v systému Linux nebo macOS zpětnou vazbu.

### <a name="net-framework-vs-net-core-framework"></a>Rozhraní .NET framework vs rozhraní .NET Framework Core

Prostředí PowerShell v systému Linux nebo macOS používá .NET Core, který je podmnožinou úplné rozhraní .NET Framework na Microsoft Windows. To je důležité, protože prostředí PowerShell poskytuje přímý přístup k podkladové typy framework, metody atd. V důsledku toho nemusí skripty, které běží v systému Windows spustit na jiných platforem než Windows vzhledem k rozdílům v rozhraní. Další informace o rozhraní .NET Framework Core najdete v tématu <https://dotnetfoundation.org/net-core>

S nástupem [standardní rozhraní .NET 2.0](https://blogs.msdn.microsoft.com/dotnet/2016/09/26/introducing-net-standard/), rozhraní .NET Core 2.0 se otevře zpět řadu tradiční typy a metody k dispozici v úplné rozhraní .NET Framework. To znamená, že základní prostředí PowerShell bude moci načítat mnoho tradiční moduly prostředí Windows PowerShell bez úprav. Můžete postupovat podle našich .NET standardní 2.0 související pracovní [zde](https://github.com/PowerShell/PowerShell/projects/4).

### <a name="redirection-issues"></a>Přesměrování problémy

Přesměrování vstupu není podporována v prostředí PowerShell na jakékoli platformě.
[Problém #1629](https://github.com/PowerShell/PowerShell/issues/1629)

Použití `Get-Content` k zápisu obsahu souboru do kanálu.

Přesměrovaného výstup bude obsahovat značka pořadí bajtů kódování Unicode (BOM), když bude použito výchozí kódování UTF-8. Kusovníku způsobí problémy při práci s nástroje, které není jeho očekávat, nebo při připojování k souboru. Použití `-Encoding Ascii` k zapsání textu ASCII, (a které vrácení kódování Unicode, nebude mít Kusovníku). (Poznámka: v tématu [RFC0020](https://github.com/PowerShell/PowerShell-RFC/issues/71) k sdělte nám svůj názor na vylepšení kódování prostředí pro základní prostředí PowerShell pro všechny platformy. Jsme se práce na podporu znakové sady UTF-8 bez Kusovník a potenciálně Změna kódování výchozí hodnoty pro různé rutiny napříč platformami.)

### <a name="job-control"></a>Ovládací prvek úlohy

Neexistuje žádná podpora řízení úlohy v prostředí PowerShell v systému Linux nebo macOS.
`fg` a `bg` nejsou příkazy k dispozici.

Prozatím, můžete použít [prostředí PowerShell úlohy](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_jobs) které fungují na všech platformách.

### <a name="remoting-support"></a>Dokonalejší podpora vzdálené komunikace

V současné době základní prostředí PowerShell podporuje vzdálenou komunikaci prostředí PowerShell (PSRP) prostřednictvím služby WSMan s základní ověřování v systému macOS a Linux a se ověření protokolem NTLM v systému Linux. (Pomocí protokolu Kerberos není podporována.)

Pro vzdálenou komunikaci založená na službě WSMan práce [psl. omi zprostředkovatele](https://github.com/PowerShell/psl-omi-provider) úložišti.

Základní prostředí PowerShell také podporuje vzdálenou komunikaci prostředí PowerShell (PSRP) přes protokol SSH na všechny platformy (Windows, systému macOS a Linux). Když to není podporováno aktuálně v produkčním prostředí, můžete další informace o nastavování [zde](../core-powershell/ssh-remoting-in-powershell-core.md).

### <a name="just-enough-administration-jea-support"></a>Podpora právě dostatečně správy (JEA)

Schopnost vytvářet omezené Správa koncových bodů (JEA) Vzdálená komunikace není aktuálně k dispozici v prostředí PowerShell v systému Linux nebo macOS. Tato funkce není aktuálně v oboru pro 6.0 a něco jsme zvažovat post 6.0 jak to vyžaduje pracovní významné návrhu.

### <a name="sudo-exec-and-powershell"></a>`sudo`, `exec`a prostředí PowerShell

Vzhledem k prostředí PowerShell běží většina příkazů v paměti (například Python nebo Ruby), nemůžete použít sudo přímo s built-ins prostředí PowerShell. (Samozřejmě můžete spustit `powershell` z sudo.) Pokud je nutné spustit rutiny prostředí PowerShell z prostředí PowerShell pomocí příkazu "sudo", například `sudo Set-Date 8/18/2016`, a poté by proveďte `sudo powershell Set-Date 8/18/2016`. Stejně tak nemůžete exec integrované prostředí PowerShell přímo. Místo toho je nutné provést `exec powershell item_to_exec`.

Tento problém je aktuálně sledován jako součást #3232.

### <a name="missing-cmdlets"></a>Chybí rutiny

Nejsou k dispozici v systému Linux nebo macOS velký počet příkazů (rutiny) obvykle dostupné v prostředí PowerShell. V mnoha případech tyto příkazy smysl žádné na těchto platforem (například specifické pro systém Windows funkcí, jako je registru). Další příkazy, jako jsou příkazy řízení služby (Get/počáteční/Stop-Service) existuje, ale není funkční. Budoucích verzích se vyřešit tyto problémy opravit poškozená rutiny a přidání nové v čase.

### <a name="command-availability"></a>Příkaz dostupnosti

Následující tabulka uvádí příkazy, které jsou známé není pro práci v prostředí PowerShell v systému Linux nebo macOS.

<table>
<th>Příkazy</th><th>Provozní stav</th><th>Poznámky</th>
<tr>
<td>Get-Service, nové služby, Restart-Service, Resume-Service, nastavení služby, Start-Service, Stop-Service, pozastavení služby
<td>Tato možnost není dostupná.
<td>Tyto příkazy nebude rozpoznána. Tento problém by měl vyřešen v budoucí verzi.
</tr>
<tr>
<td>Get-seznamu Acl, Set-Acl
<td>Tato možnost není dostupná.
<td>Tyto příkazy nebude rozpoznána. Tento problém by měl vyřešen v budoucí verzi.
</tr>
<tr>
<td>Get-AuthenticodeSignature, Set-AuthenticodeSignature
<td>Tato možnost není dostupná.
<td>Tyto příkazy nebude rozpoznána. Tento problém by měl vyřešen v budoucí verzi.
</tr>
<tr>
<td>Proces čekání
<td>K dispozici, nebude fungovat správně. <td>Například `Start-Process gvim -PassThru | Wait-Process` nefunguje; se nepodaří počkejte procesu.
</tr>
<tr>
<td>Register-PSSessionConfiguration, Unregister-PSSessionConfiguration, Get-PSSessionConfiguration
<td>K dispozici ale nefunguje.
<td>Zapíše chybová zpráva oznamující, že příkazy nefungují. Toto je třeba stanovit v budoucí verzi.
</tr>
<tr>
<td>Get událost novou událost, Register-EngineEvent, Register-WmiEvent, událost odebrání zrušit registraci události
<td>K dispozici, ale žádné zdroje událostí jsou k dispozici.
<td>Příkazy prostředí PowerShell eventing existují, ale většina zdroje událostí používat s příkazy (například System.Timers.Timer) nejsou k dispozici v systému Linux provedení nemá ve verzi Alpha příkazy.
</tr>
<tr>
<td>Set-ExecutionPolicy
<td>K dispozici ale nefunguje.
<td>Vrátí zpráva na této platformě není podporován. Zásady spouštění jsou zaměřené na uživatele "bezpečnostním pásem" která pomáhá zabránit uživateli v dělat nákladné chyby. Není hranice zabezpečení.
</tr>
<tr>
<td>Nový PSSessionOption, nové PSTransportOption
<td>K dispozici, ale New-PSSession nefunguje.
<td>New-PSSessionOption a New-PSTransportOption nejsou ověřeny aktuálně pracovat nyní, New-PSSession funguje.
</tr>
</table>
