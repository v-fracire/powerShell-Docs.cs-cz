---
ms.date: 08/27/2018
keywords: rutiny prostředí PowerShell
title: Skriptování v prostředí PowerShell
ms.openlocfilehash: 07925ce8dcafd33970a703c9b241bf6f76f88d10
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403810"
---
# <a name="powershell"></a>PowerShell

PowerShell je prostředí příkazového řádku založeného na úlohách a skriptovací jazyk založená na rozhraní .NET.
PowerShell umožňuje správcům systému a zkušení uživatelé rychle automatizace úloh, které spravovat operační systémy (Linux, macOS a Windows) a procesy.

Příkazy prostředí PowerShell umožňují spravovat počítače z příkazového řádku. Zprostředkovatelé prostředí PowerShell vám umožní přistupovat k úložištím dat, jako je například registr a úložiště certifikátů, stejně snadno, jako je přístup k systému souborů. PowerShell zahrnuje analyzátor výrazů a propracovaný skriptovací jazyk.

## <a name="powershell-is-open-source"></a>PowerShell je open source

Prostředí PowerShell základní zdrojový kód je nyní k dispozici na webu GitHub a otevřít příspěvky vytvořené komunitou.
Zobrazit [Powershellu source na Githubu](https://github.com/powershell/powershell).

Můžete začít s bity, je potřeba mít [získat PowerShell](https://github.com/PowerShell/PowerShell#get-powershell).
Nebo možná s rychlou prohlídku u [Začínáme](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell).

## <a name="powershell-design-goals"></a>Cíle návrhu prostředí PowerShell

PowerShell slouží ke zlepšení prostředí příkazového řádku a skriptovací odstraňuje dlouhotrvající problémy a přidáním nových funkcí.

### <a name="discoverability"></a>Zjistitelnost

PowerShell umožňuje snadno zjistit jeho funkcí. Například najdete seznam rutin, které zobrazení a změna služby Windows, zadejte:

```powershell
Get-Command *-Service
```

Po zjištění, které rutina provede úlohu, můžete další informace o rutině pomocí `Get-Help` rutiny. Například pro zobrazení nápovědy o `Get-Service` rutiny, typ:

```powershell
Get-Help Get-Service
```

Většina rutin návratových objektů, které mohou manipulovat a pak se vykresluje jako text k zobrazení. Abyste úplně pochopili výstupu rutiny, přesměrujte výstup do `Get-Member` rutiny. Například následující příkaz zobrazí informace o členech výstup objektu podle `Get-Service` rutiny.

```powershell
Get-Service | Get-Member
```

### <a name="consistency"></a>Konzistence

Správa systémů může být složitý úkol. Nástroje, které mají nápovědu jednotné rozhraní pro řízení zákonitou složitost. Bohužel nástrojů příkazového řádku a skriptovatelný objektů COM nejsou známy jejich konzistence.

Konzistence Powershellu je jedním z jeho primární prostředky. Například, pokud se dozvíte, jak používat `Sort-Object` rutiny, vám pomůže dané znalosti seřadit výstup všechny rutiny. Není nutné další různé rutiny řazení jednotlivých rutin.

Kromě toho rutina vývojáři nemuseli navrhnout řazení funkce pro jejich rutiny. PowerShell nabízí rozhraní se základními funkcemi, které vynutí konzistence. Rozhraní framework eliminuje některé možnosti, které jsou ponechána pro vývojáře. Ale naopak to vývoj rutin značně zjednodušuje.

### <a name="interactive-and-scripting-environments"></a>Interaktivní a skriptovací prostředí

Příkazový řádek Windows poskytuje interaktivní prostředí s přístupem k nástroji příkazového řádku a skriptování základní. Windows Script Host (WSH) je možné používat skripty příkazového řádku nástroje a objekty automatizace COM, ale neposkytuje interaktivní prostředí.

Prostředí PowerShell spojuje interaktivní prostředí a skriptovací prostředí. Prostředí PowerShell můžete přistupovat k nástroje příkazového řádku, objekty COM a knihovny tříd .NET. Tato kombinace funkcí rozšiřuje možnosti interaktivního uživatele, skripty a správce systému.

### <a name="object-orientation"></a>Objekt orientace

PowerShell je založená na objekt není text. Výstup příkazu je objekt. Výstupní objekt, prostřednictvím kanálu, můžete odeslat k jinému příkazu jako vstup.

Tento kanál obsahuje známému rozhraní pro osoby zkušenosti s další prostředí. Prostředí PowerShell rozšiřuje tento koncept odesláním objekty namísto textu.

### <a name="easy-transition-to-scripting"></a>Snadný přechod do skriptů

Díky možnosti rozpoznání příkazu Powershellu usnadňuje přechod od psaní příkazů interaktivně k vytváření a spouštění skriptů. Záznamy o studiu prostředí PowerShell a historie usnadňují kopírování příkazů do souboru pro použití jako skript.
