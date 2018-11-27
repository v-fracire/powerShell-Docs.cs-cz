---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Přesměrování dat rutinami Out
ms.assetid: 2a4acd33-041d-43a5-a3e9-9608a4c52b0c
ms.openlocfilehash: f08879f436ce751b176af020aba21e90f09aa61f
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52321005"
---
# <a name="redirecting-data-with-out--cmdlets"></a>Přesměrování dat Out-* rutiny

Prostředí Windows PowerShell poskytuje několik rutin, které umožňují řídit přímo výstupní data. Tyto rutiny sdílet dvě důležité charakteristiky.

Nejprve se obecně transformovat data na nějakou formu text. Je to proto, že výstupní data do systémových komponent, které vyžadují vaše zadání textu. To znamená, že potřebují k reprezentaci objektů jako text. Proto se text formátovaný jako se zobrazí v okně konzoly Windows Powershellu.

Za druhé, tyto rutiny použít příkaz prostředí Windows PowerShell **si** vzhledem k tomu, že odesílat informace z prostředí Windows PowerShell někde jinde. **Out-Buffer: hostování** rutina není žádná výjimka: zobrazení okna hostitele je mimo prostředí Windows PowerShell. To je důležité, protože když se data odesílají z prostředí Windows PowerShell, ve skutečnosti se odebere. To můžete vidět, pokud při pokusu o vytvoření kanálu data stránek do okna hostitele a pak se pokusíte naformátovat jako seznam, jak je znázorněno zde:

```powershell
Get-Process | Out-Host -Paging | Format-List
```

Očekáváte příkaz pro zobrazování stránek informace o procesu ve formátu seznamu. Místo toho zobrazí výchozí tabulkového seznamu:

```output
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

**Out-Buffer: hostování** rutiny odešle data přímo do konzoly, proto **Format-List** příkaz nikdy obdrží nic k formátování.

Správný způsob strukturování tento příkaz je umístit **out-Buffer: hostování** rutiny na konci kanálu, jak je znázorněno níže. To způsobí, že zpracování dat, který má být formátována v seznamu před se stránkováním a zobrazí.

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

To platí pro všechny **si** rutiny. **Si** rutiny by se měla vždy zobrazit na konci kanálu.

> [!NOTE]
> Všechny **si** rutiny vykreslení výstupu jako text, použití v platnosti formátování okna konzoly, včetně omezení délky řádku.

#### <a name="paging-console-output-out-host"></a>Stránkování výstupu konzoly (out-Buffer: hostitelské)

Ve výchozím nastavení, prostředí Windows PowerShell, odesílá data do okna hostitele, což je přesně to, co hostování odesílací rutina nemá. Primárně používají k hostování odesílací rutina je stránkování dat, jak jsme probírali výše. Například následující použití příkazu out-Buffer: hostovat na stránce výstupem rutiny Get-– příkaz:

```powershell
Get-Command | Out-Host -Paging
```

Můžete také použít **Další** funkce k datům stránky. V prostředí Windows PowerShell **Další** je funkce, která volá **out-Buffer: hostování-stránkování**. Následující příkaz ukazuje použití **Další** funkce na stránce výstup Get-– příkaz:

```powershell
Get-Command | more
```

Zadáte-li jeden nebo více názvů souborů jako argumenty, které mají další funkce, funkce se načíst zadané soubory a stránek jejich obsah na hostitele:

```
PS> more c:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
...
```

#### <a name="discarding-output-out-null"></a>Zahazuje se výstup (out-Buffer: Null)

**Out-Buffer: Null** rutina slouží k okamžitě zrušit všechny vstupní přijme. To je užitečné pro nepotřebná data, abyste získali jako vedlejší efekt spuštění příkazu se zahodí. Když zadáte následující příkaz, se nezobrazí nic zpět z tohoto příkazu:

```powershell
Get-Command | Out-Null
```

**Out-Buffer: Null** rutina není zahodit chybový výstup. Například pokud zadáte následující příkaz, zobrazí se zpráva oznamující, že prostředí Windows PowerShell nerozpozná "Je NotACommand":

```
PS> Get-Command Is-NotACommand | Out-Null
Get-Command : 'Is-NotACommand' is not recognized as a cmdlet, function, operabl
e program, or script file.
At line:1 char:12
+ Get-Command  <<<< Is-NotACommand | Out-Null
```

#### <a name="printing-data-out-printer"></a>Tisk Data (domáčtí tiskárny)

Data lze vytisknout pomocí **domáčtí tiskárny** rutiny. **Domáčtí tiskárny** rutiny použije výchozí tiskárna, pokud nezadáte název tiskárny. Tiskárny založené na Windows můžete použít tak, že zadáte jeho zobrazované jméno. Není nutné pro jakýkoli druh mapování portů tiskáren nebo dokonce skutečné fyzické tiskárny. Například pokud máte nástroje pro vytváření bitových kopií dokumentu aplikace Microsoft Office nainstalovaný, můžete odeslat data na soubor obrázku tak, že zadáte:

```powershell
Get-Command Get-Command | Out-Printer -Name 'Microsoft Office Document Image Writer'
```

#### <a name="saving-data-out-file"></a>Ukládání dat (out-File)

S použitím může odeslat výstup do souboru místo v okně konzoly **out-File** rutiny. Následující příkazový řádek odešle seznam procesů k souboru **C:\\temp\\processlist.txt**:

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt
```

Výsledky použití **out-File** rutiny nemusí být co očekáváte, že pokud se používají k přesměrování tradiční výstupu. Informace o tom své chování, musí mít přehled o kontextu, ve kterém **out-File** rutina funguje.

Ve výchozím nastavení **out-File** rutina vytvoří soubor Unicode. Toto je doporučené výchozí dlouhodobě, ale znamená, že nástroje, které očekávají soubory ASCII nebudou fungovat správně s výchozí formát výstupu. Můžete změnit výchozí formát výstupu na ASCII pomocí **kódování** parametr:

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt -Encoding ASCII
```

**Out-File** formátů souboru obsahu, aby vypadala jako výstup na konzole. To způsobí, že výstupní má být zkráceno stejně, jako je v okně konzoly ve většině případů. Například pokud spustíte následující příkaz:

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt
```

Výstup bude vypadat takto:

```output
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
...
```

Chcete-li získat výstup, který se nevynutí zalomení řádků tak, aby odpovídaly šířka obrazovky, můžete použít **šířka** parametr k určení tloušťka čáry. Protože **šířka** je parametr 32bitové celé číslo, může mít maximální hodnota je 2147483647. Zadejte následující příkaz pro nastavení tloušťka čáry této maximální hodnotě:

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt -Width 2147483647
```

**Out-File** rutina je nejužitečnější, pokud chcete uložit výstup, který bude mít zobrazí v konzole. Pro lepší kontrolu nad formátem výstupu budete potřebovat další pokročilé nástroje. Podíváme se na ty v následující kapitole spolu s některé podrobnosti o manipulaci s objekty.