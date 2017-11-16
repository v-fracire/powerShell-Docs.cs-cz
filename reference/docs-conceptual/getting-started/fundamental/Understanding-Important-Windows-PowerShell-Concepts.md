---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Seznámení s koncepty důležité Windows PowerShell"
ms.assetid: 3e601e38-4520-4578-a48d-b6779f1d35ee
ms.openlocfilehash: 1ffcfefcc7ffc7c98ba4d1e3ccc9a59cd9b0baac
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="understanding-important-windows-powershell-concepts"></a>Seznámení s koncepty důležité Windows PowerShell
Prostředí Windows PowerShell návrhu integruje koncepty z mnoha různých prostředích. Několik z nich jsou známé uživatelům s prostředím v součásti pro konkrétní nebo programovací prostředí, ale jen několik lidí věděli o všech z nich. Vyhledávání na některé z těchto pojmech obsahuje užitečné Přehled prostředí.

### <a name="commands-are-not-text-based"></a>Příkazy nejsou založený na textu
Na rozdíl od tradičních rozhraní příkazového řádku příkazy prostředí Windows PowerShell rutiny jsou navrženy tak, jak nakládat s objekty - strukturovaná informace, které je více než jen řetězec znaků, které jsou uvedeny na obrazovce. Vždy výstup příkazu představuje podél doplňující informace, které můžete použít, pokud to potřebujete. Toto téma podrobněji, v tomto dokumentu se budeme zabývat.

Pokud jste použili text zpracování nástroje ke zpracování příkazového řádku data v minulosti, zjistíte, že budou chovat jinak Pokud se pokusíte použít je v prostředí Windows PowerShell. Ve většině případů není nutné nástrojů pro zpracování textu k extrakci konkrétní informace. Dostanete částem dat přímo pomocí standardní příkazy zpracování objektu prostředí Windows PowerShell.

### <a name="the-command-family-is-extensible"></a>Příkaz řada je rozšiřitelný
Rozhraní, jako je například Cmd.exe neposkytují způsob, jak můžete přímo rozšířit sadu předdefinovaných příkazů. Můžete vytvořit externí nástroje příkazového řádku, které běží v Cmd.exe, ale tyto externí nástroje nemají služby, jako je Nápověda integrace a Cmd.exe nezná automaticky, že jsou platné příkazy.

Nativní binární příkazy v prostředí Windows PowerShell, označuje jako *rutiny* (výrazný příkaz – umožňuje), může být rozšířen o rutiny, které vytvoříte a která přidáte do prostředí Windows PowerShell pomocí modulu snap in. Prostředí Windows PowerShell *moduly snap in* kompilovány, stejně jako binární nástroje v jiných rozhraní. Můžete je přidat do prostředí, jakož i nové rutiny prostředí Windows PowerShell poskytovatelů.

Speciální charakter interní příkazy prostředí Windows PowerShell, bude označujeme je jako *rutiny*.

> [!NOTE]
> Prostředí Windows PowerShell můžete spouštět příkazy než rutiny. Jsme nebude možné hovoříte o je podrobně v Průvodci uživatele Windows PowerShell, ale jsou užitečné vědět o jako kategorie typů příkaz. Prostředí Windows PowerShell podporuje skripty, které se podobá skripty prostředí UNIX a Cmd.exe dávkové soubory, ale jsou příponu názvu souboru .ps1. Prostředí Windows PowerShell můžete taky vytvořit interní funkce, které lze použít přímo v rozhraní nebo ve skriptech.

### <a name="windows-powershell-handles-console-input-and-display"></a>Vstup konzoly obslužných rutin prostředí PowerShell systému Windows a zobrazení
Když zadáte příkaz, prostředí Windows PowerShell vždy zpracovává příkazového řádku vstup přímo. Prostředí Windows PowerShell taky formáty výstupu, který se zobrazí na obrazovce. To je důležité, protože snižuje práce potřebné jednotlivých rutin a zajišťuje, že můžete vždy způsobem stejným způsobem, bez ohledu na to, které rutina, kterou používáte. Jedním z příkladů jak tato funkce zjednodušuje životnosti pro nástroj vývojáři a uživatelé je Nápověda příkazového řádku.

Tradiční nástroje příkazového řádku mají své vlastní schémata požaduje a zobrazení nápovědy. Některé nástroje příkazového řádku použijte **/?** k aktivaci zobrazení nápovědy; jiné používají **-?**, **/H**, nebo i  **//** . Některé zobrazí nápovědy v okně grafického uživatelského rozhraní, a nikoli v zobrazení konzoly. Některé komplexní nástroje, například aktualizační aplikace, rozbalte soubory vnitřním před zobrazení jejich nápovědy. Pokud použijete nesprávný parametr, nástroj může ignorovat zadali a zahájit provádění úlohy automaticky.

Když zadáte příkaz v prostředí Windows PowerShell, vše, co zadáte je automaticky analyzovat a předem zpracovány prostředím Windows PowerShell. Pokud použijete **-?** Parametr s rutiny prostředí Windows PowerShell, vždy znamená "Zobrazit mi nápovědy pro tento příkaz". Vývojáři rutiny nemají analyzovat příkaz; Stačí, když se zadat text nápovědy.

Je důležité si uvědomit, že funkce nápovědy prostředí Windows PowerShell jsou k dispozici i v případě, že spustíte tradiční nástroje příkazového řádku v prostředí Windows PowerShell. Prostředí Windows PowerShell zpracuje parametry a předá výsledky externí nástroje.

> [!NOTE]
> Pokud spustíte grafické aplikace v prostředí Windows PowerShell, otevře se okno pro aplikaci. Prostředí Windows PowerShell zasáhla pouze při zpracování příkazového řádku zadejte můžete napájení nebo výstup aplikace do okna konzoly; nemá vliv interně fungování aplikace.

### <a name="windows-powershell-uses-some-c-syntax"></a>Prostředí Windows PowerShell používá některé syntaxe jazyka C#
Prostředí Windows PowerShell má syntaxe funkce a klíčová slova, která jsou velmi podobné těm, které jsou v programovací jazyk, C# použít, protože prostředí Windows PowerShell je založena na rozhraní .NET Framework. Učení prostředí Windows PowerShell budou bylo mnohem snazší výuka C#, pokud vás zajímá v jazyce.

Pokud si nejste programování v C#, není tato podobnosti důležité. Ale pokud jste již obeznámeni s C#, podobnost můžete nastavit učení mnohem jednodušší prostředí Windows PowerShell.

