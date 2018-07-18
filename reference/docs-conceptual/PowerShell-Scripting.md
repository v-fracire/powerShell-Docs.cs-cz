---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Skriptování v prostředí PowerShell
ms.openlocfilehash: c6ba3abc2544834e2cbec16a524f79399a1d2599
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39094047"
---
# <a name="powershell"></a>PowerShell

Postaveno na rozhraní .NET Framework a prostředí PowerShell je prostředí příkazového řádku založeného na úlohách a skriptovací jazyk; je navržená speciálně pro správce systému a zkušení uživatelé rychle automatizovat správu více operačních systémů (Linux, macOS, Unix a Windows) a procesy, které souvisí s aplikacemi, které běží v těchto operačních systémech.

## <a name="powershell-is-open-source"></a>PowerShell je open source

Prostředí PowerShell základní zdrojový kód je nyní k dispozici na webu GitHub a otevřít příspěvky vytvořené komunitou.
Zobrazit [Powershellu source na Githubu](https://github.com/powershell/powershell).

Můžete začít s bity, je potřeba mít [získat PowerShell](https://github.com/PowerShell/PowerShell#get-powershell).
Nebo možná s rychlou prohlídku u [Začínáme](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell)

## <a name="powershell-design-goals"></a>Cíle návrhu prostředí PowerShell
PowerShell slouží ke zlepšení prostředí příkazového řádku a skriptovací odstraňuje dlouhotrvající problémy a přidáním nových funkcí.

### <a name="discoverability"></a>Zjistitelnost
PowerShell umožňuje snadno zjistit jeho funkcí. Například najdete seznam rutin, které zobrazení a změna služby Windows, zadejte:

```powershell
Get-Command *-Service
```

Po zjištění, které rutina provede úlohu, můžete další informace o rutině pomocí `Get-Help` rutiny.
Například pro zobrazení nápovědy o `Get-Service` rutiny, typ:

```powershell
Get-Help Get-Service
```
Většina rutin generování objektů, které je možné ovládat a pak vykreslí do textu k zobrazení.
Abyste úplně pochopili výstup této rutiny, kanálem jeho výstup `Get-Member` rutiny.
Například následující příkaz zobrazí informace o členech výstup objektu podle `Get-Service` rutiny.

```powershell
Get-Service | Get-Member
```

### <a name="consistency"></a>Konzistence
Správa systémů může být složité zařízeními a nástrojů, které mají konzistentní rozhraní pomáhají řídit zákonitou složitost.
Bohužel byl vědět nástroje příkazového řádku ani skriptovatelný objekty modelu COM pro jejich konzistence.

Konzistence Powershellu je jedním z jeho primární prostředky.
Například, pokud se dozvíte, jak používat `Sort-Object` rutiny, vám pomůže dané znalosti seřadit výstup všechny rutiny.
Není nutné další různé rutiny řazení jednotlivých rutin.

Vývojáři rutiny navíc není potřeba navrhovat funkce řazení pro jejich rutiny.
PowerShell je poskytuje rozhraní, které poskytuje základní funkce a vynutí, aby byla konzistentní o mnoho aspektů rozhraní.
Rozhraní framework eliminuje některé z možností, které jsou obvykle ponechána pro vývojáře, ale na oplátku umožňuje vývoj rutin robustní a snadno použitelné mnohem jednodušší.

### <a name="interactive-and-scripting-environments"></a>Interaktivní a skriptovací prostředí
PowerShell je kombinované skriptování a interaktivní prostředí, které poskytuje přístup k nástroji příkazového řádku a objekty modelu COM a také umožňuje používat napájení z rozhraní .NET Framework třída Library (FCL).

Toto prostředí zlepšuje po Windows příkazového řádku, která poskytuje interaktivní prostředí s více nástrojů příkazového řádku.
Je také dále to vylepšuje skriptů Windows Script Host (WSH), které vám umožní používat více nástrojů pro příkazový řádek a objekty automatizace COM, ale neposkytuje interaktivního prostředí.

Kombinací přístup ke všem z těchto funkcí Powershellu rozšiřuje možnosti interaktivního uživatele a skripty a díky lépe zvládnutelné Správa systému.

### <a name="object-orientation"></a>Objekt orientace
I když pracujete s prostředím PowerShell zadáním příkazů v textu, prostředí PowerShell je založená na objektech, ne text.
Výstup příkazu je objekt.
Můžete odeslat výstupní objekt k jinému příkazu jako vstup.
V důsledku toho prostředí PowerShell poskytuje známému rozhraní lidem se zkušenostmi s jiné prostředí, při Představujeme novou a výkonnou paradigma příkazového řádku.
Rozšiřuje koncept odesílání dat mezi příkazy tím, že povolíte odesílání objektů, spíše než textovém.

### <a name="easy-transition-to-scripting"></a>Snadný přechod do skriptů
Díky Powershellu usnadňuje přechod od psaní příkazů interaktivně k vytváření a spouštění skriptů.
Můžete zadávat příkazy příkazového řádku Powershellu se zjistit příkazy, které provádějí úlohy.
Potom můžete uložit tyto příkazy v řádné záznamy o studiu nebo historii před zkopírováním do souboru pro použití jako skript.
