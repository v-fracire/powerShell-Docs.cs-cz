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
# <a name="new-language-features-in-powershell-50"></a><span data-ttu-id="41596-102">Nové funkce jazyků v Powershellu 5.0</span><span class="sxs-lookup"><span data-stu-id="41596-102">New language features in PowerShell 5.0</span></span>

<span data-ttu-id="41596-103">PowerShell 5.0 zavádí následující nové prvky jazyka v prostředí Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="41596-103">PowerShell 5.0 introduces the following new language elements in Windows PowerShell:</span></span>

## <a name="class-keyword"></a><span data-ttu-id="41596-104">Class – klíčové slovo</span><span class="sxs-lookup"><span data-stu-id="41596-104">Class keyword</span></span>

<span data-ttu-id="41596-105">**Třídy** – klíčové slovo definuje novou třídu.</span><span class="sxs-lookup"><span data-stu-id="41596-105">The **class** keyword defines a new class.</span></span> <span data-ttu-id="41596-106">To je PRAVDA typ rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="41596-106">This is a true .NET Framework type.</span></span>
<span data-ttu-id="41596-107">Členy třídy jsou veřejné, ale pouze veřejné v rámci oboru modul.</span><span class="sxs-lookup"><span data-stu-id="41596-107">Class members are public, but only public within the module scope.</span></span>
<span data-ttu-id="41596-108">Nemůže odkazovat na název typu jako řetězec (například `New-Object` nefunguje), a v této verzi nelze použít typ literál (například `[MyClass]`) mimo modul skriptu nebo soubor, ve kterém je třída definovaná.</span><span class="sxs-lookup"><span data-stu-id="41596-108">You can't refer to the type name as a string (for example, `New-Object` doesn't work), and in this release, you can't use a type literal (for example, `[MyClass]`) outside the script/module file in which the class is defined.</span></span>

```powershell
class MyClass
{
    ...
}
```

## <a name="enum-keyword-and-enumerations"></a><span data-ttu-id="41596-109">Enum – klíčové slovo a výčty</span><span class="sxs-lookup"><span data-stu-id="41596-109">Enum keyword and enumerations</span></span>

<span data-ttu-id="41596-110">Podpora **výčtu** – klíčové slovo se přidala, který používá jako oddělovač znaku nového řádku.</span><span class="sxs-lookup"><span data-stu-id="41596-110">Support for the **enum** keyword has been added, which uses newline as the delimiter.</span></span>
<span data-ttu-id="41596-111">Aktuální omezení: nelze definovat enumerátor z hlediska samotný, ale můžete inicializovat výčet z hlediska jiného výčtu, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="41596-111">Current limitations: you cannot define an enumerator in terms of itself, but you can initialize an enum in terms of another enum, as shown in the following example.</span></span>
<span data-ttu-id="41596-112">Kromě toho nelze aktuálně zadané základní typ; Ten je vždy [int].</span><span class="sxs-lookup"><span data-stu-id="41596-112">Also, the base type cannot currently be specified; it is always [int].</span></span>

```powershell
enum Color2
{
    Yellow = [Color]::Blue
}
```

<span data-ttu-id="41596-113">Hodnotou výčtu musí být časovou konstantou analýzy; nelze ho nastavíte na výsledek volaný příkaz.</span><span class="sxs-lookup"><span data-stu-id="41596-113">An enumerator value must be a parse time constant; you cannot set it to the result of an invoked command.</span></span>

```powershell
enum MyEnum
{
    Enum1
    Enum2
    Enum3 = 42
    Enum4 = [int]::MaxValue
}
```

<span data-ttu-id="41596-114">Výčty podporují aritmetické operace, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="41596-114">Enums support arithmetic operations, as shown in the following example.</span></span>

```powershell
enum SomeEnum { Max = 42 }
enum OtherEnum { Max = [SomeEnum]::Max + 1 }
```

## <a name="import-dscresource"></a><span data-ttu-id="41596-115">Import-DscResource</span><span class="sxs-lookup"><span data-stu-id="41596-115">Import-DscResource</span></span>

<span data-ttu-id="41596-116">**Import-DscResource** je nyní true dynamické – klíčové slovo.</span><span class="sxs-lookup"><span data-stu-id="41596-116">**Import-DscResource** is now a true dynamic keyword.</span></span>
<span data-ttu-id="41596-117">Prostředí PowerShell analyzuje zadaný modul kořenový modul, hledání třídy, které obsahují **DscResource** atribut.</span><span class="sxs-lookup"><span data-stu-id="41596-117">PowerShell parses the specified module’s root module, searching for classes that contain the **DscResource** attribute.</span></span>

## <a name="implementingassembly"></a><span data-ttu-id="41596-118">ImplementingAssembly</span><span class="sxs-lookup"><span data-stu-id="41596-118">ImplementingAssembly</span></span>

<span data-ttu-id="41596-119">Nové pole **ImplementingAssembly**, byl přidán do ModuleInfo.</span><span class="sxs-lookup"><span data-stu-id="41596-119">A new field, **ImplementingAssembly**, has been added to ModuleInfo.</span></span> <span data-ttu-id="41596-120">Je nastavena na dynamickém sestavení vytvořené pro modul skriptu, pokud skript definuje třídy nebo načíst sestavení pro binární moduly.</span><span class="sxs-lookup"><span data-stu-id="41596-120">It is set to the dynamic assembly created for a script module if the script defines classes, or the loaded assembly for binary modules.</span></span> <span data-ttu-id="41596-121">Není nastavena, když ModuleType = manifestu.</span><span class="sxs-lookup"><span data-stu-id="41596-121">It is not set when ModuleType = Manifest.</span></span>

<span data-ttu-id="41596-122">Reflexe v **ImplementingAssembly** pole zjišťuje prostředky v modulu.</span><span class="sxs-lookup"><span data-stu-id="41596-122">Reflection on the **ImplementingAssembly** field discovers resources in a module.</span></span> <span data-ttu-id="41596-123">To znamená, že může zjistit prostředky, které jsou napsané v Powershellu nebo jiných spravovaných jazycích.</span><span class="sxs-lookup"><span data-stu-id="41596-123">This means you can discover resources written in either PowerShell or other managed languages.</span></span>

<span data-ttu-id="41596-124">Pole s inicializátory:</span><span class="sxs-lookup"><span data-stu-id="41596-124">Fields with initializers:</span></span>

```powershell
[int] $i = 5
```

<span data-ttu-id="41596-125">Je statická nejsou podporovány. funguje stejně jako atribut, stejně jako omezení typu, takže ho můžete zadat v libovolném pořadí.</span><span class="sxs-lookup"><span data-stu-id="41596-125">Static is supported; it works like an attribute, as do the type constraints, so it can be specified in any order.</span></span>

```powershell
static [int] $count = 0
```

<span data-ttu-id="41596-126">Typ je volitelné.</span><span class="sxs-lookup"><span data-stu-id="41596-126">A type is optional.</span></span>

```powershell
$s = "hello"
```

<span data-ttu-id="41596-127">Všichni členové jsou veřejné.</span><span class="sxs-lookup"><span data-stu-id="41596-127">All members are public.</span></span>

## <a name="constructors-and-instantiation"></a><span data-ttu-id="41596-128">Konstruktory a instance</span><span class="sxs-lookup"><span data-stu-id="41596-128">Constructors and instantiation</span></span>

<span data-ttu-id="41596-129">Prostředí Windows PowerShell třídy mohou mít konstruktory; mají stejný název jako své třídy.</span><span class="sxs-lookup"><span data-stu-id="41596-129">Windows PowerShell classes can have constructors; they have the same name as their class.</span></span> <span data-ttu-id="41596-130">Konstruktory mohou být přetíženy.</span><span class="sxs-lookup"><span data-stu-id="41596-130">Constructors can be overloaded.</span></span> <span data-ttu-id="41596-131">Statické konstruktory jsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="41596-131">Static constructors are supported.</span></span> <span data-ttu-id="41596-132">Vlastnosti s výrazy inicializace jsou inicializovány před spuštěním jakéhokoli kódu v konstruktoru.</span><span class="sxs-lookup"><span data-stu-id="41596-132">Properties with initialization expressions are initialized before running any code in a constructor.</span></span> <span data-ttu-id="41596-133">Před tělo statického konstruktoru jsou inicializovány statické vlastnosti a vlastnosti instance se inicializuje před tělo konstruktoru nestatické.</span><span class="sxs-lookup"><span data-stu-id="41596-133">Static properties are initialized before the body of a static constructor, and instance properties are initialized before the body of the non-static constructor.</span></span> <span data-ttu-id="41596-134">V současné době neexistuje žádná syntaxe pro volání konstruktoru od jiného konstruktoru (C, jako jsou\# syntaxe ": this()").</span><span class="sxs-lookup"><span data-stu-id="41596-134">Currently, there is no syntax for calling a constructor from another constructor (like the C\# syntax ": this()").</span></span> <span data-ttu-id="41596-135">Alternativním řešením je definovat běžnou metodou Init.</span><span class="sxs-lookup"><span data-stu-id="41596-135">The workaround is to define a common Init method.</span></span>

<span data-ttu-id="41596-136">Tyto způsoby konkretizujete tříd v této verzi.</span><span class="sxs-lookup"><span data-stu-id="41596-136">The following are ways of instantiating classes in this release.</span></span>

<span data-ttu-id="41596-137">Vytvoření instance pomocí výchozího konstruktoru.</span><span class="sxs-lookup"><span data-stu-id="41596-137">Instantiating by using the default constructor.</span></span> <span data-ttu-id="41596-138">Všimněte si, že se v této verzi nepodporuje New-Object.</span><span class="sxs-lookup"><span data-stu-id="41596-138">Note that New-Object is not supported in this release.</span></span>

```powershell
$a = [MyClass]::new()
```

<span data-ttu-id="41596-139">Volání konstruktoru s parametrem</span><span class="sxs-lookup"><span data-stu-id="41596-139">Calling a constructor with a parameter</span></span>

```powershell
$b = [MyClass]::new(42)
```

<span data-ttu-id="41596-140">Předá pole do konstruktoru s více parametry</span><span class="sxs-lookup"><span data-stu-id="41596-140">Passing an array to a constructor with multiple parameters</span></span>
```powershell
$c = [MyClass]::new(@(42,43,44), "Hello")
```

<span data-ttu-id="41596-141">V této verzi nefunguje New-Object s třídami definovanými ve Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="41596-141">In this release, New-Object does not work with classes defined in Windows PowerShell.</span></span> <span data-ttu-id="41596-142">Pro tuto verzi, název typu je také pouze viditelné lexikálně, což znamená, že není viditelný mimo modul nebo skript, který definuje třídu.</span><span class="sxs-lookup"><span data-stu-id="41596-142">Also for this release, the type name is only visible lexically, meaning it is not visible outside of the module or script that defines the class.</span></span> <span data-ttu-id="41596-143">Funkce může vrátit instanci třídy definované v prostředí Windows PowerShell a instance fungovat dobře mimo modul nebo skriptu.</span><span class="sxs-lookup"><span data-stu-id="41596-143">Functions can return instances of a class defined in Windows PowerShell, and instances work well outside of the module or script.</span></span>

<span data-ttu-id="41596-144">`Get-Member -Static` Zobrazí seznam konstruktory, abyste mohli zobrazit přetížení jako jakékoliv jiné metody.</span><span class="sxs-lookup"><span data-stu-id="41596-144">`Get-Member -Static` lists constructors, so you can view overloads like any other method.</span></span> <span data-ttu-id="41596-145">Výkon této syntaxe je také výrazně rychlejší než New-Object.</span><span class="sxs-lookup"><span data-stu-id="41596-145">The performance of this syntax is also considerably faster than New-Object.</span></span>

<span data-ttu-id="41596-146">Částečně statická metoda s názvem **nové** funguje s typy .NET, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="41596-146">The pseudo-static method named **new** works with .NET types, as shown in the following example.</span></span>

```powershell
[hashtable]::new()
```

<span data-ttu-id="41596-147">Nyní je vidět přetížení konstruktoru pomocí Get-Member, nebo jak je znázorněno v tomto příkladu:</span><span class="sxs-lookup"><span data-stu-id="41596-147">You can now see constructor overloads with Get-Member, or as shown in this example:</span></span>

```powershell
PS> [hashtable]::new
OverloadDefinitions
-------------------
hashtable new()
hashtable new(int capacity)
hashtable new(int capacity, float loadFactor)
```

## <a name="methods"></a><span data-ttu-id="41596-148">Metody</span><span class="sxs-lookup"><span data-stu-id="41596-148">Methods</span></span>

<span data-ttu-id="41596-149">Metoda třídy prostředí Windows PowerShell je implementovaný jako hodnota ScriptBlock, který má pouze koncový blok.</span><span class="sxs-lookup"><span data-stu-id="41596-149">A Windows PowerShell class method is implemented as a ScriptBlock that has only an end block.</span></span> <span data-ttu-id="41596-150">Všechny metody jsou veřejné.</span><span class="sxs-lookup"><span data-stu-id="41596-150">All methods are public.</span></span> <span data-ttu-id="41596-151">Následující ukázka definuje metodu s názvem **DoSomething**.</span><span class="sxs-lookup"><span data-stu-id="41596-151">The following shows an example of defining a method named **DoSomething**.</span></span>

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

<span data-ttu-id="41596-152">Volání metody:</span><span class="sxs-lookup"><span data-stu-id="41596-152">Method invocation:</span></span>

```powershell
$b = [MyClass]::new()
$b.DoSomething(42)
```

<span data-ttu-id="41596-153">Přetížené metody – tedy ty, které jsou stejná jako existující metodu s názvem, ale rozlišené pomocí jejich zadaných hodnot – jsou také podporovány.</span><span class="sxs-lookup"><span data-stu-id="41596-153">Overloaded methods--that is, those that are named the same as an existing method, but differentiated by their specified values--are also supported.</span></span>

## <a name="properties"></a><span data-ttu-id="41596-154">Properties</span><span class="sxs-lookup"><span data-stu-id="41596-154">Properties</span></span>

<span data-ttu-id="41596-155">Všechny vlastnosti jsou veřejné.</span><span class="sxs-lookup"><span data-stu-id="41596-155">All properties are public.</span></span> <span data-ttu-id="41596-156">Vlastnosti vyžadují znaku nového řádku nebo středníkem.</span><span class="sxs-lookup"><span data-stu-id="41596-156">Properties require either a newline or semicolon.</span></span> <span data-ttu-id="41596-157">Pokud není zadán žádný typ objektu, je vlastnost typu objektu.</span><span class="sxs-lookup"><span data-stu-id="41596-157">If no object type is specified, the property type is object.</span></span>

<span data-ttu-id="41596-158">Vlastnosti, které používají ověřování atributy nebo transformaci argumentu (třeba `[ValidateSet("aaa")]`) fungovat podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="41596-158">Properties that use validation attributes or argument transformation attributes (e.g. `[ValidateSet("aaa")]`) work as expected.</span></span>

## <a name="hidden"></a><span data-ttu-id="41596-159">Skryté</span><span class="sxs-lookup"><span data-stu-id="41596-159">Hidden</span></span>

<span data-ttu-id="41596-160">New – klíčové slovo **skryté**, byl přidán.</span><span class="sxs-lookup"><span data-stu-id="41596-160">A new keyword, **Hidden**, has been added.</span></span> <span data-ttu-id="41596-161">**Skryté** lze použít u vlastnosti a metody (včetně konstruktory).</span><span class="sxs-lookup"><span data-stu-id="41596-161">**Hidden** can be applied to properties and methods (including constructors).</span></span>

<span data-ttu-id="41596-162">Skryté členy jsou veřejné, ale pokud se nezobrazí ve výstupu příkazu Get-Member-Force přidat parametr.</span><span class="sxs-lookup"><span data-stu-id="41596-162">Hidden members are public, but do not appear in the output of Get-Member unless the -Force parameter is added.</span></span>

<span data-ttu-id="41596-163">Skryté členy nejsou zahrnuty při kartě dokončení nebo pomocí technologie Intellisense, pokud dojde k dokončení ve třídě definovat člen skrytý.</span><span class="sxs-lookup"><span data-stu-id="41596-163">Hidden members are not included when tab completing or using Intellisense unless the completion occurs in the class defining the hidden member.</span></span>

<span data-ttu-id="41596-164">Nový atribut **System.Management.Automation.HiddenAttribute** byl přidán tak, aby kód jazyka C# může mít stejnou sémantiku v rámci prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41596-164">A new attribute, **System.Management.Automation.HiddenAttribute** has been added so that C# code can have the same semantics within Windows PowerShell.</span></span>

## <a name="return-types"></a><span data-ttu-id="41596-165">Návratové typy</span><span class="sxs-lookup"><span data-stu-id="41596-165">Return types</span></span>

<span data-ttu-id="41596-166">Návratový typ je smlouva; Návratová hodnota je převedena na očekávaný typ.</span><span class="sxs-lookup"><span data-stu-id="41596-166">Return type is a contract; the return value is converted to the expected type.</span></span> <span data-ttu-id="41596-167">Pokud není zadán žádný návratový typ, je návratový typ void.</span><span class="sxs-lookup"><span data-stu-id="41596-167">If no return type is specified, the return type is void.</span></span> <span data-ttu-id="41596-168">Neexistuje žádné streamování objekty. objekty nelze zapsat do kanálu, ať už úmyslně nebo náhodná.</span><span class="sxs-lookup"><span data-stu-id="41596-168">There is no streaming of objects; objects cannot be written to the pipeline either intentionally or by accident.</span></span>

## <a name="attributes"></a><span data-ttu-id="41596-169">Atributy</span><span class="sxs-lookup"><span data-stu-id="41596-169">Attributes</span></span>

<span data-ttu-id="41596-170">Dvě nové atributy **DscResource** a **DscProperty** byly přidány.</span><span class="sxs-lookup"><span data-stu-id="41596-170">Two new attributes, **DscResource** and **DscProperty** have been added.</span></span>

## <a name="lexical-scoping-of-variables"></a><span data-ttu-id="41596-171">Lexikální rozsah proměnné</span><span class="sxs-lookup"><span data-stu-id="41596-171">Lexical scoping of variables</span></span>

<span data-ttu-id="41596-172">Následující příklad funguje jak lexikálním oboru v této verzi.</span><span class="sxs-lookup"><span data-stu-id="41596-172">The following shows an example of how lexical scoping works in this release.</span></span>

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

## <a name="end-to-end-example"></a><span data-ttu-id="41596-173">Příklad začátku do konce</span><span class="sxs-lookup"><span data-stu-id="41596-173">End-to-End Example</span></span>

<span data-ttu-id="41596-174">Následující příklad vytvoří několik nových, vlastních tříd pro implementaci HTML dynamické style sheet jazyk (DSL).</span><span class="sxs-lookup"><span data-stu-id="41596-174">The following example creates several new, custom classes to implement an HTML dynamic style sheet language (DSL).</span></span>
<span data-ttu-id="41596-175">Potom příklad přidá pomocné funkce k vytvoření specifické typy elementů v rámci elementu třídy, jako je například stylů a tabulky, protože typy nelze použít mimo obor modulu.</span><span class="sxs-lookup"><span data-stu-id="41596-175">Then, the example adds helper functions to create specific element types as part of the element class, such as heading styles and tables, because types cannot be used outside the scope of a module.</span></span>

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
