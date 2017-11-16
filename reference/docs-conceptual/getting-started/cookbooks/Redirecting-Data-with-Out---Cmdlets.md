---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Přesměrování Data pomocí rutiny"
ms.assetid: 2a4acd33-041d-43a5-a3e9-9608a4c52b0c
ms.openlocfilehash: e570ca1c2c665a4a5d23abb50d4102a012b160e9
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="redirecting-data-with-out--cmdlets"></a>Přesměrování dat s Out-* rutiny
Prostředí Windows PowerShell poskytuje několik rutiny, která umožňují řídit přímo výstupní data. Tyto rutiny sdílet dvě důležité charakteristiky.

Nejprve se obecně transformovat data na určitou formu text. Je to proto, že výstupní data do komponent systému, které vyžadují zadávání textu. To znamená, že potřebují k reprezentaci objektů jako text. Text je proto naformátován, jak můžete vidět v okně konzoly prostředí Windows PowerShell.

Druhý, tyto rutiny použít příkaz prostředí Windows PowerShell **Out** protože odesílají informace z prostředí Windows PowerShell do jiné oblasti. **Odesílací hostitele** rutiny není žádná výjimka: zobrazení okna hostitele je mimo prostředí Windows PowerShell. To je důležité, protože při odesílání dat mimo prostředí Windows PowerShell je ve skutečnosti odstraněna. To můžete vidět, pokud se pokusíte vytvořit kanál data stránek do okna hostitele a pak se pokusíte formátovat jako seznam, jak je vidět tady:

```
PS> Get-Process | Out-Host -Paging | Format-List
```

Příkaz k zobrazení stránky informace o procesu ve formátu seznamu můžou očekávat. Místo toho zobrazí výchozí tabulkového seznamu:

```
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    101       5     1076       3316    32     0.05   2888 alg
...
    618      18    39348      51108   143   211.20    740 explorer
    257       8     9752      16828    79     3.02   2560 explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

**Odesílací hostitele** rutiny odešle data přímo do konzoly, proto **Format-List** příkaz nikdy obdrží nic k formátování.

Správný způsob struktury tento příkaz je uvést **odesílací hostitele** rutinu na konci kanálu, jak je uvedeno níže. To způsobí, že proces data, která mají být ve formátu v seznamu před je stránkovaného fondu a zobrazí.

```
PS> Get-Process | Format-List | Out-Host -Paging

Id      : 2888
Handles : 101
CPU     : 0.046875
Name    : alg
...

Id      : 740
Handles : 612
CPU     : 211.703125
Name    : explorer

Id      : 2560
Handles : 257
CPU     : 3.015625
Name    : explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

To platí pro všechny **Out** rutiny. **Out** rutiny se vždy zobrazí na konci kanálu.

> [!NOTE]
> Všechny **Out** rutiny vykreslení výstupu jako text použití formátování, které platí pro v okně konzoly, včetně omezení délky řádku.

#### <a name="paging-console-output-out-host"></a>Stránkování výstupu konzoly (odesílací hostitele)
Ve výchozím nastavení, prostředí Windows PowerShell, odešle data do okna hostitele, který je co odesílací hostitele rutiny nepodporuje. Primárním použitím pro odesílací hostitele rutina je stránkování dat, jak již bylo zmíněno dříve. Například následující příkaz používá odesílací hostitele na stránku výstup rutiny Get-Command:

```
PS> Get-Command | Out-Host -Paging
```

Můžete také **Další** funkce k datům stránky. V prostředí Windows PowerShell **Další** je funkce, která volá **odesílací hostitel-stránkování**. Následující příkaz ukazuje, jak pomocí **Další** funkce na stránku výstup Get-Command:

```
PS> Get-Command | more
```

Pokud jeden nebo více názvů souborů zahrnete jako argumenty pro další funkce, funkce přečte zadané soubory a stránka jejich obsah na hostitele:

```
PS> more c:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
...
```

#### <a name="discarding-output-out-null"></a>Výstupních zahození (odesílací Null)
**Odesílací Null** rutina umožňuje okamžitě zahodit žádný vstup obdrží. To je užitečné pro zahození nepotřebná data, který jste získali v vedlejším účinkem spuštění příkazu. Když zadáte následující příkaz, obdržíte nic zpět z tohoto příkazu:

```
PS> Get-Command | Out-Null
```

**Odesílací Null** rutiny není zahodit výstupní chybě. Například pokud zadáte následující příkaz, zobrazí se zpráva oznamující, že prostředí Windows PowerShell nebyl rozpoznán 'Je NotACommand':

```
PS> Get-Command Is-NotACommand | Out-Null
Get-Command : 'Is-NotACommand' is not recognized as a cmdlet, function, operabl
e program, or script file.
At line:1 char:12
+ Get-Command  <<<< Is-NotACommand | Out-Null
```

#### <a name="printing-data-out-printer"></a>Tisk dat (domáčtí tiskárny)
Data můžete vytisknout pomocí **domáčtí tiskárny** rutiny. **Domáčtí tiskárny** rutiny bude používat výchozí tiskárny, pokud nezadáte název tiskárny. Všechny tiskárny systému Windows můžete použít zadáním jeho zobrazovaný název. Není nutné pro jakýkoli druh mapování portů tiskáren nebo i skutečných fyzické tiskárny. Například pokud máte nástroje pro vytváření bitových kopií dokumentu aplikace Microsoft Office nainstalované, může posílat data do souboru bitové kopie zadáním:

```
PS> Get-Command Get-Command | Out-Printer -Name "Microsoft Office Document Image Writer"
```

#### <a name="saving-data-out-file"></a>Ukládání dat (out-File)
Můžete odesílat výstup do souboru místo v okně konzoly pomocí **out-File** rutiny. Následující příkazový řádek odešle seznam procesů do souboru **C:\\temp\\processlist.txt**:

```
PS> Get-Process | Out-File -FilePath C:\temp\processlist.txt
```

Výsledky pomocí **out-File** rutiny nemusí být toho, co očekáváte, pokud se používají k přesměrování tradiční výstupu. Pochopit své chování, musí mít přehled o kontextu, ve kterém **out-File** rutiny funguje.

Ve výchozím nastavení **out-File** rutina vytvoří soubor kódování Unicode. Toto je nejlepší výchozí dlouhodobě, ale znamená, že nástroje, které očekávají soubory ASCII nebude správně fungovat s výchozí formát výstupu. Výchozí formát výstupu do ASCII můžete změnit pomocí **kódování** parametr:

```
PS> Get-Process | Out-File -FilePath C:\temp\processlist.txt -Encoding ASCII
```

**Out-File** formátů souboru obsahu, aby vypadala jako výstup konzoly. To způsobí, že výstup k oříznutí stejně, jako je v okně konzoly ve většině případů. Například pokud spustíte následující příkaz:

```
PS> Get-Command | Out-File -FilePath c:\temp\output.txt
```

Výstup bude vypadat takto:

```
CommandType     Name                            Definition                     
-----------     ----                            ----------                     
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
...
```

Chcete-li získat výstup, který bez vynucení zalomení řádků tak, aby odpovídaly šířku obrazovky, můžete použít **šířka** parametr k určení šířka čáry. Protože **šířka** je parametr 32bitové celé číslo, může mít maximální hodnota je 2147483647. Zadejte následující příkaz a nastavte šířku čáry na tuto maximální hodnotu:

```
Get-Command | Out-File -FilePath c:\temp\output.txt -Width 2147483647
```

**Out-File** rutina je velmi užitečné, pokud chcete uložit výstup, který by mají zobrazovat v konzole. Pro lepší kontrolu nad výstupní formát budete potřebovat pokročilejší nástroje. Podíváme se na těch, které v další kapitoly, společně s některé podrobnosti o manipulaci s objektu.

