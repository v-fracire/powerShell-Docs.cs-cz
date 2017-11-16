---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: c7318552969c44f3b79f82efd71e6a72bfabef6b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="new-language-features-in-powershell-50"></a>Nové jazykové funkce v prostředí PowerShell 5.0 

Prostředí PowerShell 5.0 zavádí následující nové jazykové elementy v prostředí Windows PowerShell:

## <a name="class-keyword"></a>Class – klíčové slovo

**Třída** – klíčové slovo definuje novou třídu. Toto je true typ rozhraní .NET Framework. Členy třídy jsou veřejné, ale pouze veřejné v rámci oboru modulu.
Nemůže odkazovat na název typu jako řetězec (například `New-Object` nefunguje), a v této verzi nelze použít typ literál (například `[MyClass]`) mimo modulu skriptu nebo soubor, ve kterém je třída definovaná.

```powershell
class MyClass
{
    ...
}
```

## <a name="enum-keyword-and-enumerations"></a>Enum – klíčové slovo a výčty

Podpora pro **výčtu** byla přidána – klíčové slovo, které používá nový řádek jako oddělovač.
Aktuální omezení: nelze definovat enumerátor z hlediska sám sebe, ale bude možné inicializovat výčet z hlediska jiné výčtu, jak je znázorněno v následujícím příkladu.
Navíc nelze momentálně zadaný základní typ; je vždy [int].

```powershell
enum Color2
{
    Yellow = [Color]::Blue
}
```

Hodnotu výčtu musí být konstanta doba analýzy; Nelze nastavit ho na výsledek vyvolaná příkazu.

```powershell
enum MyEnum
{
    Enum1
    Enum2
    Enum3 = 42
    Enum4 = [int]::MaxValue
}
```

Výčty podporovat aritmetické operace, jak je znázorněno v následujícím příkladu.

```powershell
enum SomeEnum { Max = 42 }
enum OtherEnum { Max = [SomeEnum]::Max + 1 }
```

## <a name="import-dscresource"></a>Import DscResource

**Import DscResource** je nyní true dynamické – klíčové slovo.
Prostředí PowerShell analyzuje zadaný modul modul kořenové, hledání tříd, které obsahují **DscResource** atribut.

## <a name="implementingassembly"></a>ImplementingAssembly

Nové pole **ImplementingAssembly**, byl přidán do ModuleInfo. Jinak je nastavená na dynamické sestavení vytvoří modulu skriptu, pokud skript definuje třídy nebo načíst sestavení pro binární moduly. Není nastavena, když ModuleType = manifestu. 

Reflexe na **ImplementingAssembly** pole vyhledá prostředky v modulu. To znamená, že může zjistit prostředky, které jsou napsané v prostředí PowerShell nebo jiné spravované jazyky.

Pole s inicializátory:      

```powershell
[int] $i = 5
```

Je podporován statické; funguje jako atribut, stejně jako omezení typu, můžete zadat v libovolném pořadí.

```powershell
static [int] $count = 0
```

Typ je volitelný.

```powershell
$s = "hello"
```

Veřejné se všichni její členové. 

## <a name="constructors-and-instantiation"></a>Konstruktory a vytváření instancí

Prostředí Windows PowerShell třídy mohou mít konstruktory; mají stejný název jako jejich třídy. Konstruktory může být přetížený. Statické konstruktory jsou podporovány. Vlastnosti inicializace výrazy se inicializují před spuštěním jakékoli kódu v konstruktoru. Statické vlastnosti se inicializují před text statického konstruktoru a vlastnosti instance se inicializují před text nestatické konstruktoru. V současné době není žádné syntaxi pro volání konstruktoru z jiného konstruktoru (C jako\# syntaxe ": this()"). Alternativní řešení je definovat běžné metody Init. 

Následující způsoby konkretizujete tříd v této verzi.

Vytváření instancí pomocí výchozí konstruktor. Všimněte si, že není v této verzi podporovány New-Object.

```powershell
$a = [MyClass]::new()
```

Volání metody konstruktor s parametrem

```powershell
$b = [MyClass]::new(42)
```

Předávání pole do konstruktoru s více parametrů
```powershell
$c = [MyClass]::new(@(42,43,44), "Hello")
```

V této verzi nefunguje New-Object s třídami definovanými v prostředí Windows PowerShell. Také pro tuto verzi, název typu je jenom viditelné lexikálně, což znamená, že se nezobrazuje jinde než v modulu nebo skript, který definuje třídu. Funkce může vrátit instance třídy definované v prostředí Windows PowerShell a instancí fungovat i jinde než v modulu nebo skriptu.

`Get-Member -Static`uvádí konstruktory, aby se dala Zobrazit přetížení jako jakékoliv jiné metody. Výkon této syntaxe je také výrazně rychlejší než New-Object.

Částečně statickou metodu s názvem **nové** funguje s typy .NET, jak je znázorněno v následujícím příkladu.

```powershell
[hashtable]::new()
```

Nyní můžete vidět konstruktor přetížení Get-členovi, nebo jak je uvedené v tomto příkladu:

```powershell
PS> [hashtable]::new
OverloadDefinitions
-------------------
hashtable new()
hashtable new(int capacity)
hashtable new(int capacity, float loadFactor)
```

## <a name="methods"></a>Metody

Metoda třídy prostředí Windows PowerShell je implementovaný jako blok skriptu, který má jenom koncový blok. Všechny metody jsou veřejné. Ukazuje následující příklad definování metodu s názvem **DoSomething**.

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

Přetížení metody – to znamená, ty, které jsou se stejným názvem jako stávající metodu, ale rozlišené pomocí jejich zadaných hodnot – jsou také podporovány.

## <a name="properties"></a>Properties 

Všechny vlastnosti jsou veřejné. Vlastnosti vyžadují buď nového řádku nebo středníkem. Pokud není zadaný žádný typ objektu, typ vlastnosti je objekt.

Vlastnosti, které pomocí atributů ověření nebo atributy transformaci argumentu (například `[ValidateSet("aaa")]`) fungovat podle očekávání.

## <a name="hidden"></a>Skryté

New – klíčové slovo **Hidden**, byla přidána. **Skrytý** lze použít k vlastnosti a metody (včetně konstruktory).

Skryté členy jsou veřejné, ale pokud se nezobrazí ve výstupu člena Get-Force přidat parametr.

Skryté členy nejsou zahrnuty při kartě dokončení nebo pomocí Intellisense nenastane dokončení ve třídě definování člen skrytý.

Nový atribut **System.Management.Automation.HiddenAttribute** byla přidána tak, aby kód C# může mít stejnou sémantiku v rámci prostředí Windows PowerShell.

## <a name="return-types"></a>Návratové typy

Návratový typ je kontraktu; Návratová hodnota je převést na očekávaný typ. Pokud není zadaný žádný návratový typ, je návratový typ void. Neexistuje žádné streamování objekty; objekty nelze zapsat do kanálu, ať už úmyslně nebo omylem odstraněný.

## <a name="attributes"></a>Atributy

Dvou nových atributů **DscResource** a **DscProperty** byly přidány.

## <a name="lexical-scoping-of-variables"></a>Lexikální rozsahu proměnné

Následující ukazuje příklad jak lexikální oboru funguje v této verzi.

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

Následující příklad vytvoří několik nových, vlastních třídy k implementaci list jazyce dynamické stylu HTML (DSL). V příkladu potom přidá podpůrné funkce vytvořit specifické typy elementů v rámci elementu třídy, jako je záhlaví styly a tabulek, protože typů nelze použít mimo obor modulu.

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
        TR (-join $Properties.Foreach{ TD ($row.$\_) } )
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

