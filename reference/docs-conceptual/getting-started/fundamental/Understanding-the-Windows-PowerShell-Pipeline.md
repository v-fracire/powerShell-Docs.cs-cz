---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vysvětlení kanálu Windows PowerShellu
ms.assetid: 6be50926-7943-4ef7-9499-4490d72a63fb
ms.openlocfilehash: c3f1d17432cf3a77c0f5ecae137a4233a28a19d7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30951065"
---
# <a name="understanding-the-windows-powershell-pipeline"></a>Vysvětlení kanálu Windows PowerShellu
Zřetězení prakticky všude, kde funguje v prostředí Windows PowerShell. I když text se zobrazí na obrazovce, nejsou prostřednictvím prostředí Windows PowerShell kanálu text mezi příkazy. Místo toho ji prostřednictvím kanálu předá objekty.

Zápis použitý pro kanály je podobný které byly použity v jiné prostředí shell, takže na první pohled nemusí být zřejmé, že prostředí Windows PowerShell zavádí nové. Například pokud použijete **odesílací hostitele** k vynucení po stránkách zobrazení výstupu z jiného příkazu, výstup vypadá stejně jako běžný text zobrazené na obrazovce, rozdělené stránky:

```
PS> Get-ChildItem -Path C:\WINDOWS\System32 | Out-Host -Paging

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\system32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2005-10-22  11:04 PM        315 $winnt$.inf
-a---        2004-08-04   8:00 AM      68608 access.cpl
-a---        2004-08-04   8:00 AM      64512 acctres.dll
-a---        2004-08-04   8:00 AM     183808 accwiz.exe
-a---        2004-08-04   8:00 AM      61952 acelpdec.ax
-a---        2004-08-04   8:00 AM     129536 acledit.dll
-a---        2004-08-04   8:00 AM     114688 aclui.dll
-a---        2004-08-04   8:00 AM     194048 activeds.dll
-a---        2004-08-04   8:00 AM     111104 activeds.tlb
-a---        2004-08-04   8:00 AM       4096 actmovie.exe
-a---        2004-08-04   8:00 AM     101888 actxprxy.dll
-a---        2003-02-21   6:50 PM     143150 admgmt.msc
-a---        2006-01-25   3:35 PM      53760 admparse.dll
<SPACE> next page; <CR> next line; Q quit
...
```

Out-Host-příkaz stránkování je element užitečné kanálu vždy, když máte zdlouhavé výstupu, který chcete zobrazit pomalu. Je obzvláště užitečná pokud operace je velmi náročná na prostředky procesoru. Protože zpracování se přenese do odesílací hostitele rutiny pokud obsahuje kompletní stránku připravena k zobrazení, rutin, které předcházet v kanálu zastaví operaci, dokud na další stránku výstupu je k dispozici. Pokud použijete Správce úloh systému Windows ke sledování procesoru a paměti pomocí prostředí Windows PowerShell najdete v to.

Spusťte následující příkaz: **C: Get-ChildItem\\Windows-Recurse**. Porovnání využití procesoru a paměti na tento příkaz: **Get-ChildItem C:\\Windows-Recurse | Odesílací Host-stránkování**. Zobrazte na obrazovce je text, ale je to způsobeno je nezbytné k reprezentaci objektů jako text v okně konzoly. To je právě reprezentace co je skutečně probíhající v prostředí Windows PowerShell. Zvažte například rutinu Get-umístění. Pokud zadáte **Get-umístění** sice vaše aktuální umístění kořenové složce jednotky C, zobrazí se následující výstup:

```
PS> Get-Location

Path
----
C:\
```

Pokud prostředí Windows PowerShell zřetězena text, vydání příkazu, jako **Get-umístění | Odesílací hostitele**, by úspěšně prošel zpracováním z **Get-umístění** k **odesílací hostitele** sadu znaků v pořadí, jsou zobrazeny na obrazovce. Jinými slovy, pokud byste chtěli ignorovat informace záhlaví, **odesílací hostitele** nejprve obdrží znak '**C'**, pak znak '**:'**, pak znak ' **\\'**. **Odesílací hostitele** rutiny nelze určit, co znamená přidružit výstup znaků pomocí **Get-umístění** rutiny.

Místo použití text umožníte příkazy v kanálu komunikovat, prostředí Windows PowerShell pomocí objektů. Z hlediska uživatelů objekty balíček související informace do formuláře, který usnadňuje manipulovat s informacemi jako jednotku a extrahovat konkrétní položky, které potřebujete.

**Get-umístění** příkaz nevrací text, který obsahuje aktuální cestě. Vrátí balíček informace nazývané **PathInfo** objekt, který obsahuje aktuální cestě společně s některé další informace. **Odesílací hostitele** rutiny pak odešle tento **PathInfo** objekt, který chcete obrazovky a prostředí Windows PowerShell rozhodne informace k zobrazení a jak ji zobrazit založené na jeho pravidla formátování.

Ve skutečnosti výstupem informace v hlavičce **Get-umístění** rutiny je přidána pouze na konci procesu, jako součást procesu formátování data pro zobrazení na obrazovce. Co se zobrazí na obrazovce je souhrnné informace a úplný reprezentace objektu výstup.

Vzhledem k tomu, že může být další informace o výstupní z prostředí Windows PowerShell příkaz než budeme najdete v okně konzoly zobrazí jak může načtete neviditelné prvky? Jak si zobrazit doplňující data? A co dělat, když chcete zobrazit data ve formátu, liší od jednoho prostředí Windows PowerShell normálně používá?

Zbytek této kapitoly popisuje, jak můžete zjistit struktura konkrétní objektů prostředí Windows PowerShell, vyberete konkrétní položky a formátování je snazší zobrazení a jak odesílat výše uvedené informace, jako alternativní výstupní umístění souborů a tiskárny.