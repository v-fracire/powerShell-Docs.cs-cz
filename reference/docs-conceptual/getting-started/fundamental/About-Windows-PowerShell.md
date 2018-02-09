---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Informace o Windows PowerShellu
ms.assetid: 979654ae-7994-47f8-be43-d79e7a140143
ms.openlocfilehash: 5e6d1bb4d8915ba3c83ba0020b959e444b5211cd
ms.sourcegitcommit: 18e3bfae83ffe282d3fd1a45f5386f3b7250f0c0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/08/2018
---
# <a name="about-windows-powershell"></a>Informace o Windows PowerShellu
Prostředí Windows PowerShell je navržen pro zlepšení je prostředí příkazového řádku a skriptovací odstraňuje problémy, dlouhotrvající a přidáním nové funkce.

## <a name="discoverability"></a>Možnosti rozpoznání
Prostředí Windows PowerShell snadno zjistit její funkce. Například pokud chcete najít seznam rutin, které zobrazení a změna služby systému Windows, zadejte:

```
Get-Command *-Service
```

Po zjištění, které rutina provede úlohu, se více o rutině pomocí rutiny Get-Help. Například pokud chcete zobrazit nápovědu k nástroji rutinu Get-Service, zadejte:

```
Get-Help Get-Service
```
Většina rutiny emitování objekty, které můžete s nimi manipulovat a pak se vykresluje do textu pro zobrazení. Abyste plně porozuměli tomu výstup této rutiny, prostřednictvím kanálu její výstup do rutiny Get-člen. Následující příkaz například zobrazí informace o členů výstupní objekt rutiny Get-Service.

```
Get-Service | Get-Member
```

## <a name="consistency"></a>Konzistence
Správa systémů může být složité omezené úsilí a nástroje, které mají konzistentní rozhraní pomohou řídit vyplývajících složitost. Bohužel nástroje příkazového řádku ani Skriptovatelná COM – objekty mají známo, jejich konzistence.

Konzistence prostředí Windows PowerShell je jedním z jeho primární prostředky. Například pokud zjistíte, jak pomocí rutiny řazení objekt, můžete použít dané znalosti seřadit výstup všechny rutiny. Nemáte další rutiny různých řazení každou rutinu.

Vývojáři rutiny navíc nemusí návrh řazení funkce pro jejich rutiny. Prostředí Windows PowerShell je poskytuje rozhraní, které poskytuje základní funkce a vynutí, aby byl konzistentní o mnoho aspektů rozhraní. Rozhraní framework eliminuje některé z těchto možností, které jsou obvykle zleva vývojář, ale naopak umožňuje vývoj robustní a snadné použití rutin mnohem jednodušší.

## <a name="interactive-and-scripting-environments"></a>Interaktivní a skriptovací prostředí
Prostředí Windows PowerShell je kombinované interaktivní a skriptovací prostředí, který umožňuje přístup nástroje příkazového řádku a objekty modelu COM a také umožňuje používat power z rozhraní .NET Framework – třída Library (FCL).

Toto prostředí zlepšuje při na příkazovém řádku Windows, která poskytuje interaktivní prostředí s více nástroje příkazového řádku. Také zlepšuje při skripty skriptu hostitele prostředí WSH (Windows), které umožňují použít několik nástrojů příkazového řádku a objekty automatizace modelu COM, ale neposkytuje interaktivní prostředí.

Kombinací přístup ke všem z těchto funkcí prostředí Windows PowerShell rozšiřuje možnosti interaktivního uživatele a skripty a umožňuje lepší správu bitlockeru systému správy.

## <a name="object-orientation"></a>Orientace objektu
I když budete používat v prostředí Windows PowerShell zadáním příkazů v textu, prostředí Windows PowerShell je založena na objekty, nikoli textu. Výstup příkazu je objekt. Můžete odeslat objekt výstup do jiného příkazu jako vstup. V důsledku toho prostředí Windows PowerShell poskytuje známé rozhraní osobám s další součásti pro došlo při zavedení nových a výkonné zlepší příkazového řádku. Je nadstavbou konceptu odesílání dat mezi příkazy tím, že vám odeslat objekty, nikoli text.

## <a name="easy-transition-to-scripting"></a>Snadný přechod skriptování
Díky prostředí Windows PowerShell, které usnadňují přechod z zadáním příkazů interaktivně k vytváření a spouštění skriptů. Příkazy můžete zadat na příkazovém řádku prostředí Windows PowerShell ke zjištění příkazy, které provádějí úlohu. Pak můžete uložit tyto příkazy přepis nebo historii před jejich zkopírováním do souboru pro použití jako skript.

