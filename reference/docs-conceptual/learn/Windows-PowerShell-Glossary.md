---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Glosář Windows Powershellu
ms.assetid: b0f88cbe-cb83-4912-a301-184534cb35c7
ms.openlocfilehash: fd15667939fd9b3ea705806686b626645519588a
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404055"
---
# <a name="windows-powershell-glossary"></a>Glosář Windows Powershellu


|Termín|Definice|
|--------|--------------|
|binárního modulu|Modul prostředí Windows PowerShell, jejichž kořenový modul je soubor binárního modulu (.dll). Binárního modulu může nebo nemusí obsahovat manifestu modulu.|
|společný parametr|Parametr, který se přidá do rutin, pokročilé funkce a pracovní postupy pomocí modulu Windows PowerShell.|
|tečka zdroje|Ve Windows Powershellu, spusťte příkaz tak, že zadáte tečka a mezera před příkazem. Příkazy, které jsou zdrojem tečkou spustit v aktuálním oboru místo v nového oboru. Všechny proměnné, aliasy, funkce nebo disky, které vytvoří příkaz se vytvoří v aktuálním oboru a jsou dostupné pro uživatele, když se příkaz dokončí.|
|dynamický modul|Modul, který existuje pouze v paměti. Rutiny New-Module a Import-PSSession vytvářet dynamické moduly.|
|dynamický parametr|Parametr, který je přidán do rutiny Windows Powershellu, funkce nebo skriptu za určitých podmínek. Rutiny, funkce, zprostředkovatele a skripty můžete přidat dynamické parametry.|
|Formát souboru|Soubor XML Windows Powershellu, který má. rozšíření format.ps1xml a, který definuje, jak prostředí Windows PowerShell zobrazí objekt na základě jeho typu rozhraní .NET Framework.|
|globální stav relace|Stav relace, který obsahuje data, která je přístupné pro uživatele relaci Windows Powershellu.|
|Hostitel|Rozhraní, které modul prostředí Windows PowerShell používá ke komunikaci s uživateli. Například hostitele určuje způsob zpracování pokynů mezi prostředí Windows PowerShell a uživatele.|
|hostitelské aplikace|Program, který načte modul prostředí Windows PowerShell do svého procesu a používá k provádění operací.|
|vstup zpracování – metoda|Metoda, která rutiny můžete použít ke zpracování záznamů, který přijímá jako vstup. Metody vstupní zpracování patří BeginProcessing metody, metoda ProcessRecord, EndProcessing – metoda a StopProcessing – metoda.|
|modul manifestu|Modul Windows Powershellu, který má manifest a jejichž RootModule klíč je prázdný.|
|manifestu modulu|Prostředí Windows PowerShell datový soubor (.psd1), který popisuje obsah modulu a, která určuje, jak se zpracovávají modulu.|
|modul stavu relace|Stav relace, který obsahuje data veřejných a privátních modulu Windows PowerShell. Soukromým datům v tomto stavu relace není k dispozici pro uživatele relaci Windows Powershellu.|
|neukončující chyba|Chybu, která nezastaví pokračování pro zpracování příkazu prostředí Windows PowerShell.|
|podstatné jméno|Aplikace word, který následuje spojovník název rutiny prostředí Windows PowerShell. Podstatným jménem popisuje prostředky, na kterých funguje rutinu.|
|Sada parametrů|Skupina parametrů, které je možné v jednom příkazu k provedení konkrétní akce.|
|kanál|Ve Windows Powershellu pro odeslání výsledků z předchozího příkazu jako vstup pro další příkaz v rámci kanálu.|
|Kanál|Řadu příkazů, které jsou propojené pomocí operátorů kanálů (&#124;) (ASCII 124). Každý operátor kanálu odešle výsledky ve výstupu předchozího příkazu jako vstup pro další příkaz.|
|Relace PSSession|Typ relace prostředí Windows PowerShell, který je vytvořen, spravovat a zavřít uživatel.|
|kořenový modul|Modul je určená v klíči RootModule v manifestu modulu.|
|prostředí runspace|V prostředí Windows PowerShell, provozní prostředí, ve kterém je spuštěn každý příkaz v kanálu.|
|blok skriptu|V prostředí Windows PowerShell programovací jazyk, kolekce příkazy nebo výrazy, které lze použít jako jeden celek. Blok skriptu můžete přijímat argumenty a návratové hodnoty.|
|modul skriptu|Modul prostředí Windows PowerShell, jejichž kořenový modul je soubor modulu skriptu (.psm1). Modul skriptu může nebo nemusí obsahovat manifestu modulu.|
|soubor modulu skriptu|Soubor, který obsahuje skript prostředí Windows PowerShell. Skript definuje členy, kteří exportuje modulu skriptu. Soubory modulu skriptu mají příponu názvu souboru .psm1.|
|Prostředí shell|Příkaz interpret, který slouží k předání příkazy v operačním systému.|
|Parametr|Parametr, který nevyužívá argument.|
|ukončující chyba|Chybu, která zabraňuje zpracování příkazu prostředí Windows PowerShell.|
|Transakce|Atomickou jednotku práce. Práce v rámci transakce musí dokončit jako celek; Pokud žádnou část transakce selže, selže celá transakce.|
|typy souborů|Soubor XML Windows Powershellu, který má příponu .ps1xml a, který rozšiřuje vlastnosti typů rozhraní Microsoft .NET Framework v prostředí Windows PowerShell.|
|Příkaz|Slovo, které předchází spojovník název rutiny prostředí Windows PowerShell. Příkaz popisuje akci prováděnou rutinu.|
|Windows PowerShell|Prostředí příkazového řádku a úkolově orientovanou skriptovací technologii, která poskytuje komplexní kontroly správce IT a automatizaci systému úlohy správy.|
|Příkaz prostředí Windows PowerShell|Prvky v kanálu, které způsobují akci, která provádí. Příkazy Windows Powershellu jsou zadané na klávesnici nebo vyvolat prostřednictvím kódu programu.|
|Prostředí Windows PowerShell datového souboru|Textový soubor, který má příponu názvu souboru .psd1. Prostředí Windows PowerShell používá datových souborů pro různé účely, jako je ukládání dat manifestu modulu a ukládání přeložené řetězce pro internacionalizaci skriptu.|
|Jednotku prostředí Windows PowerShell|Virtuální jednotka, která poskytuje přímý přístup k úložišti dat. Může být definován ve zprostředkovateli Windows Powershellu nebo vytvořili na příkazovém řádku. Disky vytvořené na příkazovém řádku jsou specifické pro relaci jednotky a budou ztraceny, pokud není zavřena relace.|
|Integrované skriptovací prostředí (ISE) v prostředí Windows PowerShell|Hostitelskou aplikaci Windows PowerShell, která vám umožní spouštět příkazy a psaní, testování a ladění skriptů v prostředí kompatibilní se standardem Unicode popisný a barvy syntaxe.|
|Modul prostředí Windows PowerShell|Samostatná opakovaně použitelných částí, která umožňuje rozdělit, uspořádání a abstrahování kódu prostředí Windows PowerShell. Modul může obsahovat rutiny, poskytovatelů, funkce, proměnné a dalších typů prostředků, které lze importovat jako jeden celek.|
|Zprostředkovatel Windows PowerShellu|Microsoft založené na rozhraní .NET Framework program, který zpřístupňuje data v úložišti specializované dat v prostředí Windows PowerShell tak, že můžete zobrazit a spravovat ho.|
|Skript prostředí Windows PowerShell|Skript, který je napsán v jazyce prostředí Windows PowerShell.|
|Soubor skriptu Windows Powershellu|Soubor, který má příponu .ps1, který obsahuje skript, který je napsán v jazyce prostředí Windows PowerShell.|
|Modul snap-in prostředí Windows PowerShell|Prostředek, který definuje sadu rutin, poskytovatelé a typy rozhraní Microsoft .NET Framework, které mohou být přidány do prostředí Windows PowerShell.|
|Pracovní postup prostředí Windows PowerShell|Pracovní postup je pořadí naprogramovaných, propojených kroků, které provádějí dlouhodobé úlohy nebo vyžadují koordinaci více kroků v rámci více zařízení nebo spravovaných uzlů. Pracovní postup prostředí Windows PowerShell umožňuje odborníkům IT a vývojářům vytvářet sekvence aktivit správy více zařízení nebo jedné úlohy v rámci pracovního postupu jako pracovních postupů. Pracovní postup prostředí Windows PowerShell umožňuje přizpůsobit a spustit skripty prostředí Windows PowerShell a soubory XAML jako pracovní postupy.|