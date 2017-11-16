---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Glosář služby Windows PowerShell"
ms.assetid: b0f88cbe-cb83-4912-a301-184534cb35c7
ms.openlocfilehash: 48e5d832ead720c8bc7753c94f757ddb21846fc9
ms.sourcegitcommit: ced46469e064736eeb1f5608abbc792ec69bdc92
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/08/2017
---
# <a name="windows-powershell-glossary"></a>Glosář služby Windows PowerShell


|Termín|Definice|
|--------|--------------|
|binární modulu|Modul prostředí Windows PowerShell, jejichž kořenové modul je modul binární soubor (.dll). Modul binární může nebo nemusí obsahovat modul manifestu.|
|společný parametr|Parametr, který je přidán do rutiny, pokročilé funkce a pracovní postupy modul prostředí Windows PowerShell.|
|Zdroj tečku|V prostředí Windows PowerShell, spusťte příkaz zadáním tečkou a místo před příkaz. Příkazy, které jsou tečkou Source spustit v aktuálním oboru místo v nového oboru. Všechny proměnné, aliasy, funkce nebo jednotky které příkaz vytvoří jsou vytvořené v aktuálním oboru a jsou k dispozici uživatelům při dokončení příkazu.|
|dynamické modulu|Modul, který existuje pouze v paměti. Rutiny New-Module a Import-PSSession vytvořit dynamické moduly.|
|dynamický parametr|Parametr, který se přidá do rutiny prostředí Windows PowerShell, funkce nebo skriptu za určitých podmínek. Dynamické parametry můžete přidat rutin, funkcí, zprostředkovatele a skripty.|
|formátování souboru|Soubor Windows PowerShell XML, který má. format.ps1xml rozšíření, která definuje, jak Windows PowerShell zobrazí objekt na základě jeho typu rozhraní .NET Framework.|
|Stav globální relace|Stav relace, který obsahuje data, která je přístupné pro uživatele relaci prostředí Windows PowerShell.|
|hostitele|Rozhraní, které modul prostředí Windows PowerShell používá ke komunikaci s uživatelem. Například hostitele určuje způsob zpracování výzvy mezi prostředí Windows PowerShell a uživatelem.|
|hostitelskou aplikaci|Program, který načte modul prostředí Windows PowerShell do zpracování a používá k provádění operací.|
|vstup zpracování metody|Metoda, která rutiny můžete použít ke zpracování záznamů, které přijímá jako vstup. Vstupní zpracování metody zahrnují metodu BeginProcessing, metoda ProcessRecord, metoda EndProcessing a metodu StopProcessing.|
|modul manifestu|Modul prostředí Windows PowerShell, který má manifestu a jejichž ModulesToProcess klíč je prázdný.|
|modul manifestu|Prostředí Windows PowerShell datový soubor (.psd1), který popisuje obsah modulu a která řídí zpracování modulu.|
|Stav relace modulu|Stav relace, který obsahuje data veřejné a privátní modulu prostředí Windows PowerShell. Privátní data v tomto stavu relace nejsou k dispozici pro uživatele relaci prostředí Windows PowerShell.|
|neukončující chybu|K chybě, která nezastaví pokračovat ke zpracování tohoto příkazu prostředí Windows PowerShell.|
|podstatné jméno|Slovo následující pomlčka v názvu rutiny prostředí Windows PowerShell. Podstatným jménem popisuje prostředky, na kterých rutina funguje.|
|Sada parametrů|Skupina parametry, které lze použít v jednom příkazu k provedení určité akce.|
|kanálu|V prostředí Windows PowerShell k odesílání výsledky předchozí příkaz jako vstup na další příkaz v kanálu.|
|Kanál|Řadu příkazů pomocí operátorů kanálů (&#124;) (ASCII 124). Každý operátor kanálu odesílá výsledky předchozí příkaz jako vstup dalšího příkazu.|
|PSSession|Typ relace prostředí Windows PowerShell, který je vytvořen, spravované a uzavřené uživatele.|
|kořenové modulu|Zadaný v klíči ModuleToProcess v manifestu modulu modul.|
|Prostředí runspace|V prostředí Windows PowerShell, je pracovní prostředí, ve kterém se spustí každý příkaz v kanálu.|
|blok skriptu|V prostředí Windows PowerShell programovací jazyk, kolekci příkazy nebo výrazy, které lze použít jako na jednu jednotku. Blok skriptu můžete přijímají argumenty a návratové hodnoty.|
|modulu skriptu|Modul prostředí Windows PowerShell, jejichž kořenové modul je soubor modulu skriptu (.psm1). Modulu skriptu může nebo nemusí obsahovat modul manifestu.|
|soubor skriptu modulu|Soubor, který obsahuje skript prostředí Windows PowerShell. Skript definuje členy, kteří exportuje modulu skriptu. Soubory modulu skriptu mít příponu názvu souboru .psm1.|
|prostředí shell|Překladač příkazů, který slouží k předávání příkazů v operačním systému.|
|přepínacího parametru|Parametr, který nevyžaduje argument.|
|ukončující chyba|K chybě, která ukončí zpracování příkazu prostředí Windows PowerShell.|
|Transakce|Atomické jednotky práce. Práce v transakci musí být dokončena jako celek; Pokud jakékoliv části transakce selže, selže celá transakce.|
|typy souborů|Windows PowerShell XML soubor obsahující .ps1xml rozšíření, která rozšiřuje vlastnosti typů rozhraní Microsoft .NET Framework v prostředí Windows PowerShell.|
|Příkaz|Slovo, které předchází spojovník v názvu rutiny prostředí Windows PowerShell. Příkaz popisuje akce, která provádí rutina.|
|Windows PowerShell|Prostředí shell příkazového řádku a skriptovací technologie založený na úlohách, která poskytuje komplexní řízení správci IT a automatizaci systému úlohy správy.|
|Příkaz prostředí Windows PowerShell|Prvky v kanálu, které způsobí akci, která má být provedeny. Příkazy prostředí Windows PowerShell jsou zadané na klávesnici nebo vyvolat prostřednictvím kódu programu.|
|Prostředí Windows PowerShell datového souboru|Textový soubor, který má příponu názvu souboru .psd1. Prostředí Windows PowerShell používá datové soubory pro různé účely, například ukládání dat v manifestu modulu a ukládání přeložených řetězců pro internacionalizace skriptu.|
|Jednotku prostředí Windows PowerShell|Virtuální jednotka, která poskytuje přímý přístup k úložišti dat. Můžete být definované poskytovatele prostředí Windows PowerShell nebo vytvořit na příkazovém řádku. Jednotky vytvořili na příkazovém řádku jsou specifické pro relaci jednotky a budou ztraceny při zavření relace.|
|Integrované skriptovací prostředí (ISE) v prostředí Windows PowerShell|Hostitelskou aplikaci pro Windows PowerShell, která umožňuje spouštět příkazy a zápis, testování a ladění skriptů v prostředí popisné a syntaxe stejné barvy, kompatibilní se standardem Unicode.|
|Modul prostředí Windows PowerShell|Samostatná opakovaně použitelné jednotkou, která umožňuje oddílu, organizovat a abstraktní kód prostředí Windows PowerShell. Modul může obsahovat rutiny, zprostředkovatelé, funkce, proměnné a dalších typů prostředků, které lze importovat jako jeden celek.|
|Zprostředkovatel Windows PowerShellu|Microsoft založené na rozhraní .NET Framework program, který zpřístupní data v úložišti specializované data v prostředí Windows PowerShell, aby mohli zobrazit a spravovat.|
|Skript prostředí Windows PowerShell|Skript, který je napsán v jazyce prostředí Windows PowerShell.|
|Soubor skriptu prostředí Windows PowerShell|Soubor s příponou .ps1 a který obsahuje skript, který je napsán v jazyce prostředí Windows PowerShell.|
|Modul snap-in prostředí Windows PowerShell|Prostředek, který definuje sadu rutin, zprostředkovatelů a typy rozhraní Microsoft .NET Framework, které mohou být přidány do prostředí Windows PowerShell.|
|Pracovní postup prostředí Windows PowerShell|Pracovní postup je pořadí naprogramovaných, propojených kroků, které provádějí dlouhodobé úlohy nebo vyžadují koordinaci více kroků v rámci více zařízení nebo spravovaných uzlů. Pracovní postup prostředí Windows PowerShell umožňuje odborníkům IT a vývojářům vytvářet sekvence aktivit správy více zařízení nebo jeden úloh v rámci pracovního postupu jako pracovních postupů. Pracovní postup prostředí Windows PowerShell umožňuje přizpůsobit a spouštění skriptů prostředí Windows PowerShell a soubory XAML jako pracovních postupů.|

