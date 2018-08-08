---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: a96a4a58dafa01fb43f5bdffb52ef833816148e7
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587291"
---
# <a name="new-language-features-in-powershell-50"></a>Nové funkce jazyků v Powershellu 5.0

PowerShell 5.0 zavádí následující nové prvky jazyka v prostředí Windows PowerShell:

## <a name="class-keyword"></a>Class – klíčové slovo

**Třídy** – klíčové slovo definuje novou třídu. To je PRAVDA typ rozhraní .NET Framework.
Členy třídy jsou veřejné, ale pouze veřejné v rámci oboru modul.
Nemůže odkazovat na název typu jako řetězec (například `New-Object` nefunguje), a v této verzi nelze použít typ literál (například `[MyClass]`) mimo modul skriptu nebo soubor, ve kterém je třída definovaná.

```powershell
class MyClass
{
    ...
}
```

## <a name="enum-keyword-and-enumerations"></a>Enum – klíčové slovo a výčty

Podpora **výčtu** – klíčové slovo se přidala, který používá jako oddělovač znaku nového řádku.
Aktuální omezení: nelze definovat enumerátor z hlediska samotný, ale můžete inicializovat výčet z hlediska jiného výčtu, jak je znázorněno v následujícím příkladu.
Kromě toho nelze aktuálně zadané základní typ; Ten je vždy [int].

```powershell
enum Color2
{
    Yellow = [Color]::Blue
}
```

Hodnotou výčtu musí být časovou konstantou analýzy; nelze ho nastavíte na výsledek volaný příkaz.

```powershell
enum MyEnum
{
    Enum1
    Enum2
    Enum3 = 42
    Enum4 = [int]::MaxValue
}
```

Výčty podporují aritmetické operace, jak je znázorněno v následujícím příkladu.

```powershell
enum SomeEnum { Max = 42 }
enum OtherEnum { Max = [SomeEnum]::Max + 1 }
```

## <a name="import-dscresource"></a>Import-DscResource

**Import-DscResource** je nyní true dynamické – klíčové slovo.
Prostředí PowerShell analyzuje zadaný modul kořenový modul, hledání třídy, které obsahují **DscResource** atribut.

## <a name="implementingassembly"></a>ImplementingAssembly

Nové pole **ImplementingAssembly**, byl přidán do ModuleInfo. Je nastavena na dynamickém sestavení vytvořené pro modul skriptu, pokud skript definuje třídy nebo načíst sestavení pro binární moduly. Není nastavena, když ModuleType = manifestu.

Reflexe v **ImplementingAssembly** pole zjišťuje prostředky v modulu. To znamená, že může zjistit prostředky, které jsou napsané v Powershellu nebo jiných spravovaných jazycích.

Pole s inicializátory:

```powershell
[int] $i = 5
```

Je statická nejsou podporovány. funguje stejně jako atribut, stejně jako omezení typu, takže ho můžete zadat v libovolném pořadí.

```powershell
static [int] $count = 0
```

Typ je volitelné.

```powershell
$s = "hello"
```

Všichni členové jsou veřejné.

## <a name="constructors-and-instantiation"></a>Konstruktory a instance

Prostředí Windows PowerShell třídy mohou mít konstruktory; mají stejný název jako své třídy. Konstruktory mohou být přetíženy. Statické konstruktory jsou podporovány. Vlastnosti s výrazy inicializace jsou inicializovány před spuštěním jakéhokoli kódu v konstruktoru. Před tělo statického konstruktoru jsou inicializovány statické vlastnosti a vlastnosti instance se inicializuje před tělo konstruktoru nestatické. V současné době neexistuje žádná syntaxe pro volání konstruktoru od jiného konstruktoru (C, jako jsou\# syntaxe ": this()"). Alternativním řešením je definovat běžnou metodou Init.

Tyto způsoby konkretizujete tříd v této verzi.

Vytvoření instance pomocí výchozího konstruktoru. Všimněte si, že se v této verzi nepodporuje New-Object.

```powershell
$a = [MyClass]::new()
```

Volání konstruktoru s parametrem

```powershell
$b = [MyClass]::new(42)
```

Předá pole do konstruktoru s více parametry
```powershell
$c = [MyClass]::new(@(42,43,44), "Hello")
```

V této verzi nefunguje New-Object s třídami definovanými ve Windows Powershellu. Pro tuto verzi, název typu je také pouze viditelné lexikálně, což znamená, že není viditelný mimo modul nebo skript, který definuje třídu. Funkce může vrátit instanci třídy definované v prostředí Windows PowerShell a instance fungovat dobře mimo modul nebo skriptu.

`Get-Member -Static` Zobrazí seznam konstruktory, abyste mohli zobrazit přetížení jako jakékoliv jiné metody. Výkon této syntaxe je také výrazně rychlejší než New-Object.

Částečně statická metoda s názvem **nové** funguje s typy .NET, jak je znázorněno v následujícím příkladu.

```powershell
[hashtable]::new()
```

Nyní je vidět přetížení konstruktoru pomocí Get-Member, nebo jak je znázorněno v tomto příkladu:

```powershell
PS> [hashtable]::new
OverloadDefinitions
-------------------
hashtable new()
hashtable new(int capacity)
hashtable new(int capacity, float loadFactor)
```

## <a name="methods"></a>Metody

Metoda třídy prostředí Windows PowerShell je implementovaný jako hodnota ScriptBlock, který má pouze koncový blok. Všechny metody jsou veřejné. Následující ukázka definuje metodu s názvem **DoSomething**.

```powershell
class MyClass
{
    DoSomething($x)
    {
        $this._doSomething($x) # method syntax
    }
    private _doSomething($a) {}
}
```

Volání metody:

```powershell
$b = [MyClass]::new()
$b.DoSomething(42)
```

Přetížené metody – tedy ty, které jsou stejná jako existující metodu s názvem, ale rozlišené pomocí jejich zadaných hodnot – jsou také podporovány.

## <a name="properties"></a>Properties

Všechny vlastnosti jsou veřejné. Vlastnosti vyžadují znaku nového řádku nebo středníkem. Pokud není zadán žádný typ objektu, je vlastnost typu objektu.

Vlastnosti, které používají ověřování atributy nebo transformaci argumentu (třeba `[ValidateSet("aaa")]`) fungovat podle očekávání.

## <a name="hidden"></a>Skryté

New – klíčové slovo **skryté**, byl přidán. **Skryté** lze použít u vlastnosti a metody (včetně konstruktory).

Skryté členy jsou veřejné, ale pokud se nezobrazí ve výstupu příkazu Get-Member-Force přidat parametr.

Skryté členy nejsou zahrnuty při kartě dokončení nebo pomocí technologie Intellisense, pokud dojde k dokončení ve třídě definovat člen skrytý.

Nový atribut **System.Management.Automation.HiddenAttribute** byl přidán tak, aby kód jazyka C# může mít stejnou sémantiku v rámci prostředí Windows PowerShell.

## <a name="return-types"></a>Návratové typy

Návratový typ je smlouva; Návratová hodnota je převedena na očekávaný typ. Pokud není zadán žádný návratový typ, je návratový typ void. Neexistuje žádné streamování objekty. objekty nelze zapsat do kanálu, ať už úmyslně nebo náhodná.

## <a name="attributes"></a>Atributy

Dvě nové atributy **DscResource** a **DscProperty** byly přidány.

## <a name="lexical-scoping-of-variables"></a>Lexikální rozsah proměnné

Následující příklad funguje jak lexikálním oboru v této verzi.

```powershell
$d = 42 # Script scope

function bar
{
    $d = 0 # Function scope
    [MyClass]::DoSomething()
}

class MyClass
{
    static [object] DoSomething()
    {
        return $d # error, not found dynamically
        return $script:d # no error
        $d = $script:d
        return $d # no error, found lexically
    }
}

$v = bar
$v -eq $d # true
```

## <a name="end-to-end-example"></a>Příklad začátku do konce

Následující příklad vytvoří několik nových, vlastních tříd pro implementaci HTML dynamické style sheet jazyk (DSL).
Potom příklad přidá pomocné funkce k vytvoření specifické typy elementů v rámci elementu třídy, jako je například stylů a tabulky, protože typy nelze použít mimo obor modulu.

```powershell
# Classes that define the structure of the document
#
class Html
{
    [string] $docType
    [HtmlHead] $Head
    [Element[]] $Body

    [string] Render()
    {
        $text = "<html>`n<head>`n"
        $text += $this.Head
        $text += "`n</head>`n<body>`n"
        $text += $this.Body -join "`n" # Render all of the body elements
        $text += "</body>`n</html>"
        return $text
    }
    [string] ToString() { return $this.Render() }
}

class HtmlHead
{
    $Title
    $Base
    $Link
    $Style
    $Meta
    $Script
    [string] Render() { return "<title>$($this.Title)</title>" }
    [string] ToString() { return $this.Render() }
}

class Element
{
    [string] $Tag
    [string] $Text
    [hashtable] $Attributes
    [string] Render() {
        $attributesText= ""
        if ($this.Attributes)
        {
            foreach ($attr in $this.Attributes.Keys)
            {
                #BUGBUG - need to validate keys against attribute
                $attributesText += " $attr=`"$($this.Attributes[$attr])\`""
            }
        }
        return "<$($this.tag)${attributesText}>$($this.text)</$($this.tag)>`n"
    }
[string] ToString() { return $this.Render() }
}

#
# Helper functions for creating specific element types on top of the classes.
# These are required because types aren’t visible outside of the module.
#

function H1 { [Element] @{ Tag = "H1" ; Text = $args.foreach{$_} -join " " }}
function H2 { [Element] @{ Tag = "H2" ; Text = $args.foreach{$_} -join " " }}
function H3 { [Element] @{ Tag = "H3" ; Text = $args.foreach{$_} -join " " }}
function P { [Element] @{ Tag = "P" ; Text = $args.foreach{$_} -join " " }}
function B { [Element] @{ Tag = "B" ; Text = $args.foreach{$_} -join " " }}
function I { [Element] @{ Tag = "I" ; Text = $args.foreach{$_} -join " " }}
function HREF
{
    param (
        $Name,
        $Link
    )
    return [Element] @{
        Tag = "A"
        Attributes = @{ HREF = $link }
        Text = $name
    }
}
function Table
{
    param (
    [Parameter(Mandatory)]
    [object[]]
        $Data,
    [Parameter()]
    [string[]]
        $Properties = "*",
    [Parameter()]
    [hashtable]
        $Attributes = @{ border=2; cellpadding=2; cellspacing=2 }
    )
$bodyText = ""
# Add the header tags
$bodyText += $Properties.foreach{TH $_}
# Add the rows
$bodyText += foreach ($row in $Data)
    {
        TR (-join $Properties.Foreach{ TD ($row.$_) } )
    }

    $table = [Element] @{
        Tag = "Table"
        Attributes = $Attributes
        Text = $bodyText
    }
$table
}
function TH { ([Element] @{ Tag = "TH" ; Text = $args.foreach{$_} -join " " }) }
function TR { ([Element] @{ Tag = "TR" ; Text = $args.foreach{$_} -join " " }) }
function TD { ([Element] @{ Tag = "TD" ; Text = $args.foreach{$_} -join " " }) }
function Style

{
    return [Element] @{
        Tag = "style"
        Text = "$args"
    }
}

# Takes a hash table, casts it to and HTML document
# and then returns the resulting type.
#
function Html ([HTML] $doc) { return $doc }
```
