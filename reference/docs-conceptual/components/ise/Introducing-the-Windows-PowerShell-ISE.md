---
ms.date: 08/14/2018
keywords: rutiny prostředí PowerShell
title: Úvod do prostředí PowerShell ISE
ms.openlocfilehash: 09a28b295855fd2a3c62bba8a681399dae3454f8
ms.sourcegitcommit: 3402a478cf118c11a5642038eb117bc76553e3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53411578"
---
# <a name="the-windows-powershell-ise"></a>Windows PowerShell ISE

Windows Powershellu integrovaném skriptovacím prostředí (ISE) je hostitelskou aplikaci pro Windows PowerShell. V prostředí ISE můžete spouštět příkazy a zápis, testování a ladění skriptů v jedné založené na Windows grafické uživatelské rozhraní. ISE poskytuje víceřádkové úpravy, tab k dokončování příkazů, barevné zvýrazňování syntaxe, selektivní spouštění, kontextové nápovědy a podpory pro jazyky zprava doleva. Položky nabídky a klávesové zkratky se mapují na řadu stejných úkolů, které by se v konzole Windows Powershellu. Například při ladění skriptu v prostředí ISE, kliknete pravým tlačítkem na řádek kódu do podokna úprav nastavení zarážky.

## <a name="support"></a>Podpora

ISE byla poprvé zavedena v systémech Windows PowerShell verze 2 a byla znovu navržena s PowerShell verze 3. ISE je podporované ve všech podporovaných verzích Windows Powershellu až a včetně verze 5.1 Windows Powershellu. ISE, ale je v režimu maintennce a které můžete chtít přidat žádné nové funkce.
Kromě toho se nepodporuje pro ISE Powershellu v6 a nad rámec. Uživatelé se chce grafický nástroj pro správu Powershellu scrips atd., zvažte [Visual Studio Code](https://code.visualstudio.com/).

## <a name="key-features"></a>Klíčové funkce

Mezi hlavní funkce v prostředí Windows PowerShell ISE patří:

- Víceřádkové úpravy: V příkazovém podokně Vložit prázdný řádek pod aktuálním řádkem, stisknutím klávesy SHIFT + ENTER.
- Výběrové spuštění: Spustit část skriptu, vyberte text, který chcete spustit a pak klikněte na tlačítko **spustit skript** tlačítko. Nebo stisknutím klávesy F5.
- Kontextová nápověda: Typ **Invoke-Item**, a potom stiskněte klávesu F1. V souboru nápovědy se otevře v článku **Invoke-Item** rutiny.

Windows PowerShell ISE umožňuje přizpůsobit některé aspekty její vzhled. Má také svůj vlastní profil skript prostředí Windows PowerShell.

## <a name="to-start-the-windows-powershell-ise"></a>Spusťte Windows PowerShell ISE

Klikněte na tlačítko **Start**vyberte **prostředí Windows PowerShell**a potom klikněte na tlačítko **Windows PowerShell ISE**.
Alternativně můžete zadat `powershell_ise.exe` libovolného příkazového řádku nebo v poli Spustit.

## <a name="to-get-help-in-the-windows-powershell-ise"></a>Chcete-li získat nápovědu v prostředí Windows PowerShell ISE

Na **pomáhají** nabídky, klikněte na tlačítko **nápovědu k prostředí Windows PowerShell**. Nebo stisknutím klávesy F1. Soubor, který otevře popisuje Windows PowerShell ISE a prostředí Windows PowerShell, včetně všech objektů v nápovědě k dispozici z rutiny Get-Help.
