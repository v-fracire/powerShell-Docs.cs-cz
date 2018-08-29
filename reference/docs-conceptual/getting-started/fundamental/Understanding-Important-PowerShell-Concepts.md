---
ms.date: 08/23/2018
keywords: rutiny prostředí PowerShell
title: Vysvětlení důležitých pojmů Powershellu
ms.assetid: 3e601e38-4520-4578-a48d-b6779f1d35ee
ms.openlocfilehash: 5f8192f962cebb8ee5e5384e39b48de811b11003
ms.sourcegitcommit: 59727f71dc204785a1bcdedc02716d8340a77aeb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2018
ms.locfileid: "43134239"
---
# <a name="understanding-important-powershell-concepts"></a>Vysvětlení důležitých pojmů Powershellu

Návrh Powershellu integruje koncepty z mnoha různých prostředích. Několik konceptů bude znát lidem prostředí v prostředí nebo programovací prostředí. Ale několik lidí vědět o všechny z nich. Hledání v některé z těchto konceptů obsahuje užitečné Přehled prostředí.

## <a name="output-is-object-based"></a>Výstup je založený na objektech

Na rozdíl od tradičních rozhraní příkazového řádku rutin prostředí PowerShell mají zacházet s objekty.
Objekt je strukturovaných informací, která je více než jen řetězce znaky uvedené na obrazovce. Příkaz výstupu vždy provede další informace, které můžete použít, pokud ji budete potřebovat.

Pokud ke zpracování dat v minulosti jste použili nástrojů pro zpracování textu, zjistíte, chovají se odlišně při použití v prostředí PowerShell. Ve většině případů není nutné nástrojů pro zpracování textu k extrakci konkrétní informace. Přímý přístup k částem dat pomocí standardní syntaxe objekt prostředí PowerShell.

## <a name="the-command-family-is-extensible"></a>Řada příkaz je možné rozšířit

Rozhraní, jako je například Cmd.exe neposkytuje způsob, jak přímo rozšířit sadu předdefinovaných příkazů.
Můžete vytvořit externí nástroje příkazového řádku, které běží v Cmd.exe. Ale tyto externí nástroje nemáte služby, jako je integrace nápovědy. Cmd.exe automaticky neví, že tyto externí nástroje jsou platné příkazy.

Nativní příkazy v prostředí PowerShell jsou označovány jako *rutiny* (vyslovováno příkaz umožňuje). Můžete vytvořit vlastní moduly rutin a funkcí pomocí kompilaci kódu nebo skriptech. Moduly můžete přidat rutiny a zprostředkovatelé prostředí. PowerShell podporuje také skripty, které jsou obdobou skripty prostředí UNIX a Cmd.exe dávkové soubory.

## <a name="powershell-handles-console-input-and-display"></a>Prostředí PowerShell zpracovává vstup konzoly a zobrazení

Po zadání příkazu Powershellu vždy zpracovává vstup příkazového řádku přímo. Prostředí PowerShell také formáty výstupu, který se zobrazí na obrazovce. Tento rozdíl je důležité, protože snižuje práci potřebnou jednotlivých rutin. Zajišťuje, že můžete vždy dělat něco stejně jako všechny rutiny. Vývojáři rutiny není potřeba napsat kód, který analyzovat argumenty příkazového řádku nebo formátování výstupu.

Tradiční nástroje příkazového řádku mají své vlastní schémata pro požadování a zobrazení nápovědy. Některé nástroje příkazového řádku použijte **/?** k aktivaci zobrazení nápovědy; ostatní používat **-?**, **/H**, nebo dokonce **//**. Některé zobrazí nápovědy v okně grafického uživatelského rozhraní, nikoli v zobrazení konzoly. Pokud použijete chybný parametr, může nástroj ignorovat zadali a spusťte skript úkolu automaticky.
Vzhledem k tomu, že automaticky analyzuje a zpracuje příkazového řádku Powershellu **-?** Parametr vždy znamená "zobrazit nápovědu pro tento příkaz".

> [!NOTE]
> Pokud spustíte grafické aplikace v prostředí PowerShell, otevře se okno pro aplikaci.
> Prostředí PowerShell zasáhla pouze při zpracování příkazového řádku zadejte vám napájení nebo výstup aplikace vrátit do okna konzoly. To nemá vliv na fungování aplikace interně.

## <a name="powershell-uses-some-c-syntax"></a>PowerShell používá syntaxe jazyka C#

PowerShell je postaveno na .NET Framework. Některé funkce syntaxe a klíčová slova sdílí s programovací jazyk C#. Výuku Powershellu můžete usnadnit mnohem snazší naučit se C#. Pokud jste již obeznámeni s jazykem C#, mohli tyto podobnosti výuku Powershellu jednodušší.