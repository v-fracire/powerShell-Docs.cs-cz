---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Pomocí statické třídy a metody"
ms.assetid: 418ad766-afa6-4b8c-9a44-471889af7fd9
ms.openlocfilehash: fe41c7d6b45564e7b5bc2b922a18587c9745e26d
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="using-static-classes-and-methods"></a><span data-ttu-id="e85ed-103">Pomocí statické třídy a metody</span><span class="sxs-lookup"><span data-stu-id="e85ed-103">Using Static Classes and Methods</span></span>
<span data-ttu-id="e85ed-104">Ne všechny třídy rozhraní .NET Framework lze vytvořit pomocí **New-Object**.</span><span class="sxs-lookup"><span data-stu-id="e85ed-104">Not all .NET Framework classes can be created by using **New-Object**.</span></span> <span data-ttu-id="e85ed-105">Například pokud se pokusíte vytvořit **System.Environment** nebo **System.Math** objektu s **New-Object**, zobrazí se následující chybové zprávy:</span><span class="sxs-lookup"><span data-stu-id="e85ed-105">For example, if you try to create a **System.Environment** or a **System.Math** object with **New-Object**, you will get the following error messages:</span></span>

```
PS> New-Object System.Environment
New-Object : Constructor not found. Cannot find an appropriate constructor for
type System.Environment.
At line:1 char:11
+ New-Object  <<<< System.Environment
PS> New-Object System.Math
New-Object : Constructor not found. Cannot find an appropriate constructor for
type System.Math.
At line:1 char:11
+ New-Object  <<<< System.Math
```

<span data-ttu-id="e85ed-106">Tyto chyby dojít, protože neexistuje žádný způsob, jak vytvořit nový objekt z těchto tříd.</span><span class="sxs-lookup"><span data-stu-id="e85ed-106">These errors occur because there is no way to create a new object from these classes.</span></span> <span data-ttu-id="e85ed-107">Tyto třídy jsou referenční dokumentace knihoven metod a vlastností, které se nemění stavu.</span><span class="sxs-lookup"><span data-stu-id="e85ed-107">These classes are reference libraries of methods and properties that do not change state.</span></span> <span data-ttu-id="e85ed-108">Nemusíte je vytvořit, je jednoduše používat.</span><span class="sxs-lookup"><span data-stu-id="e85ed-108">You don't need to create them, you simply use them.</span></span> <span data-ttu-id="e85ed-109">Třídy a metody, jako jsou ty se nazývají *statické třídy* vzhledem k tomu, že nejsou vytvořeny, zničení nebo změnit.</span><span class="sxs-lookup"><span data-stu-id="e85ed-109">Classes and methods such as these are called *static classes* because they are not created, destroyed, or changed.</span></span> <span data-ttu-id="e85ed-110">Chcete-li to zrušte poskytujeme příklady, které používají statické třídy.</span><span class="sxs-lookup"><span data-stu-id="e85ed-110">To make this clear we will provide examples that use static classes.</span></span>

### <a name="getting-environment-data-with-systemenvironment"></a><span data-ttu-id="e85ed-111">Získávání dat prostředí s System.Environment</span><span class="sxs-lookup"><span data-stu-id="e85ed-111">Getting Environment Data with System.Environment</span></span>
<span data-ttu-id="e85ed-112">Prvním krokem při práci s objektem v prostředí Windows PowerShell je obvykle, použijte Get-člen a zjistěte, jaké členy obsahuje.</span><span class="sxs-lookup"><span data-stu-id="e85ed-112">Usually, the first step in working with an object in Windows PowerShell is to use Get-Member to find out what members it contains.</span></span> <span data-ttu-id="e85ed-113">S statické třídy je trochu jiný proces, protože skutečná třída není objekt.</span><span class="sxs-lookup"><span data-stu-id="e85ed-113">With static classes, the process is a little different because the actual class is not an object.</span></span>

#### <a name="referring-to-the-static-systemenvironment-class"></a><span data-ttu-id="e85ed-114">Odkazy na statická třída System.Environment</span><span class="sxs-lookup"><span data-stu-id="e85ed-114">Referring to the Static System.Environment Class</span></span>
<span data-ttu-id="e85ed-115">Statická třída může být tím, že název třídy do složených závorek.</span><span class="sxs-lookup"><span data-stu-id="e85ed-115">You can refer to a static class by surrounding the class name with square brackets.</span></span> <span data-ttu-id="e85ed-116">Například můžete se podívat do **System.Environment** zadáním názvu v závorkách.</span><span class="sxs-lookup"><span data-stu-id="e85ed-116">For example, you can refer to **System.Environment** by typing the name within brackets.</span></span> <span data-ttu-id="e85ed-117">Díky tomu se zobrazí některé informace obecného typu:</span><span class="sxs-lookup"><span data-stu-id="e85ed-117">Doing so displays some generic type information:</span></span>

```
PS> [System.Environment]

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     False    Environment                              System.Object
```

> [!NOTE]
> <span data-ttu-id="e85ed-118">Jak jsme už bylo zmíněno dříve, prostředí Windows PowerShell automaticky přidá '**systému.**.</span><span class="sxs-lookup"><span data-stu-id="e85ed-118">As we mentioned previously, Windows PowerShell automatically prepends '**System.**'</span></span> <span data-ttu-id="e85ed-119">Zadejte názvy při použití **New-Object**.</span><span class="sxs-lookup"><span data-stu-id="e85ed-119">to type names when you use **New-Object**.</span></span> <span data-ttu-id="e85ed-120">Samé se stane, když pomocí názvu typu v závorkách, takže můžete určit  **\[System.Environment]** jako  **\[prostředí]**.</span><span class="sxs-lookup"><span data-stu-id="e85ed-120">The same thing happens when using a bracketed type name, so you can specify **\[System.Environment]** as **\[Environment]**.</span></span>

<span data-ttu-id="e85ed-121">**System.Environment** třída obsahuje obecné informace o pracovní prostředí aktuální proces, který je powershell.exe při práci v rámci prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e85ed-121">The **System.Environment** class contains general information about the working environment for the current process, which is powershell.exe when working within Windows PowerShell.</span></span>

<span data-ttu-id="e85ed-122">Pokud se pokusíte zobrazit podrobnosti o této třídy zadáním  **\[System.Environment] | Get-člen**, typu objektu je oznámil, že je **System.RuntimeType** , nikoli **System.Environment**:</span><span class="sxs-lookup"><span data-stu-id="e85ed-122">If you try to view details of this class by typing **\[System.Environment] | Get-Member**, the object type is reported as being **System.RuntimeType** , not **System.Environment**:</span></span>

```
PS> [System.Environment] | Get-Member

   TypeName: System.RuntimeType
```

<span data-ttu-id="e85ed-123">Chcete-li zobrazit statické členy Get-členem, zadejte **statické** parametr:</span><span class="sxs-lookup"><span data-stu-id="e85ed-123">To view static members with Get-Member, specify the **Static** parameter:</span></span>

```
PS> [System.Environment] | Get-Member -Static

   TypeName: System.Environment

Name                       MemberType Definition
----                       ---------- ----------
Equals                     Method     static System.Boolean Equals(Object ob...
Exit                       Method     static System.Void Exit(Int32 exitCode)
...
CommandLine                Property   static System.String CommandLine {get;}
CurrentDirectory           Property   static System.String CurrentDirectory ...
ExitCode                   Property   static System.Int32 ExitCode {get;set;}
HasShutdownStarted         Property   static System.Boolean HasShutdownStart...
MachineName                Property   static System.String MachineName {get;}
NewLine                    Property   static System.String NewLine {get;}
OSVersion                  Property   static System.OperatingSystem OSVersio...
ProcessorCount             Property   static System.Int32 ProcessorCount {get;}
StackTrace                 Property   static System.String StackTrace {get;}
SystemDirectory            Property   static System.String SystemDirectory {...
TickCount                  Property   static System.Int32 TickCount {get;}
UserDomainName             Property   static System.String UserDomainName {g...
UserInteractive            Property   static System.Boolean UserInteractive ...
UserName                   Property   static System.String UserName {get;}
Version                    Property   static System.Version Version {get;}
WorkingSet                 Property   static System.Int64 WorkingSet {get;}
TickCount                               ExitCode
```

<span data-ttu-id="e85ed-124">Vlastnosti, které chcete zobrazit z System.Environment jsme teď můžete vybrat.</span><span class="sxs-lookup"><span data-stu-id="e85ed-124">We can now select properties to view from System.Environment.</span></span>

#### <a name="displaying-static-properties-of-systemenvironment"></a><span data-ttu-id="e85ed-125">Statické vlastnosti System.Environment zobrazení</span><span class="sxs-lookup"><span data-stu-id="e85ed-125">Displaying Static Properties of System.Environment</span></span>
<span data-ttu-id="e85ed-126">Vlastnosti System.Environment jsou statické a je třeba zadat jiným způsobem než běžné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="e85ed-126">The properties of System.Environment are also static, and must be specified in a different way than normal properties.</span></span> <span data-ttu-id="e85ed-127">Používáme **::** označíte, prostředí Windows PowerShell, která by měla spolupracovat s statickou metodu nebo vlastnost.</span><span class="sxs-lookup"><span data-stu-id="e85ed-127">We use **::** to indicate to Windows PowerShell that we want to work with a static method or property.</span></span> <span data-ttu-id="e85ed-128">Chcete-li zobrazit příkaz, který byl použitý ke spuštění prostředí Windows PowerShell, jsme zkontrolujte **CommandLine** vlastnost zadáním:</span><span class="sxs-lookup"><span data-stu-id="e85ed-128">To see the command that was used to launch Windows PowerShell, we check the **CommandLine** property by typing:</span></span>

```
PS> [System.Environment]::Commandline
"C:\Program Files\Windows PowerShell\v1.0\powershell.exe"
```

<span data-ttu-id="e85ed-129">Pokud chcete zkontrolovat verzi operačního systému, zobrazí vlastnost OSVersion zadáním:</span><span class="sxs-lookup"><span data-stu-id="e85ed-129">To check the operating system version, display the OSVersion property by typing:</span></span>

```
PS> [System.Environment]::OSVersion

           Platform ServicePack         Version             VersionString
           -------- -----------         -------             -------------
            Win32NT Service Pack 2      5.1.2600.131072     Microsoft Windows...
```

<span data-ttu-id="e85ed-130">Jsme můžete zkontrolovat, zda je počítač právě vypíná zobrazením **HasShutdownStarted** vlastnost:</span><span class="sxs-lookup"><span data-stu-id="e85ed-130">We can check whether the computer is in the process of shutting down by displaying the **HasShutdownStarted** property:</span></span>

```
PS> [System.Environment]::HasShutdownStarted
False
```

### <a name="doing-math-with-systemmath"></a><span data-ttu-id="e85ed-131">Provádění matematické s System.Math</span><span class="sxs-lookup"><span data-stu-id="e85ed-131">Doing Math with System.Math</span></span>
<span data-ttu-id="e85ed-132">Statická třída System.Math je užitečné pro provádění některých matematické operace.</span><span class="sxs-lookup"><span data-stu-id="e85ed-132">The System.Math static class is useful for performing some mathematical operations.</span></span> <span data-ttu-id="e85ed-133">Důležité členů **System.Math** jsou většinou metody, které jsme můžete zobrazit pomocí **Get-člen**.</span><span class="sxs-lookup"><span data-stu-id="e85ed-133">The important members of **System.Math** are mostly methods, which we can display by using **Get-Member**.</span></span>

> [!NOTE]
> <span data-ttu-id="e85ed-134">System.Math má několik metod se stejným názvem, ale jsou rozlišené typ jejich parametrů.</span><span class="sxs-lookup"><span data-stu-id="e85ed-134">System.Math has several methods with the same name, but they are distinguished by the type of their parameters.</span></span>

<span data-ttu-id="e85ed-135">Zadejte následující příkaz k zobrazení seznamu metod **System.Math** třídy.</span><span class="sxs-lookup"><span data-stu-id="e85ed-135">Type the following command to list the methods of the **System.Math** class.</span></span>

```
PS> [System.Math] | Get-Member -Static -MemberType Methods

   TypeName: System.Math

Name            MemberType Definition
----            ---------- ----------
Abs             Method     static System.Single Abs(Single value), static Sy...
Acos            Method     static System.Double Acos(Double d)
Asin            Method     static System.Double Asin(Double d)
Atan            Method     static System.Double Atan(Double d)
Atan2           Method     static System.Double Atan2(Double y, Double x)
BigMul          Method     static System.Int64 BigMul(Int32 a, Int32 b)
Ceiling         Method     static System.Double Ceiling(Double a), static Sy...
Cos             Method     static System.Double Cos(Double d)
Cosh            Method     static System.Double Cosh(Double value)
DivRem          Method     static System.Int32 DivRem(Int32 a, Int32 b, Int3...
Equals          Method     static System.Boolean Equals(Object objA, Object ...
Exp             Method     static System.Double Exp(Double d)
Floor           Method     static System.Double Floor(Double d), static Syst...
IEEERemainder   Method     static System.Double IEEERemainder(Double x, Doub...
Log             Method     static System.Double Log(Double d), static System...
Log10           Method     static System.Double Log10(Double d)
Max             Method     static System.SByte Max(SByte val1, SByte val2), ...
Min             Method     static System.SByte Min(SByte val1, SByte val2), ...
Pow             Method     static System.Double Pow(Double x, Double y)
ReferenceEquals Method     static System.Boolean ReferenceEquals(Object objA...
Round           Method     static System.Double Round(Double a), static Syst...
Sign            Method     static System.Int32 Sign(SByte value), static Sys...
Sin             Method     static System.Double Sin(Double a)
Sinh            Method     static System.Double Sinh(Double value)
Sqrt            Method     static System.Double Sqrt(Double d)
Tan             Method     static System.Double Tan(Double a)
Tanh            Method     static System.Double Tanh(Double value)
Truncate        Method     static System.Decimal Truncate(Decimal d), static...
```

<span data-ttu-id="e85ed-136">Zobrazí se několik matematickém metod.</span><span class="sxs-lookup"><span data-stu-id="e85ed-136">This displays several mathematical methods.</span></span> <span data-ttu-id="e85ed-137">Tady je seznam příkazů, které ukazují, jak fungují některé běžné metody:</span><span class="sxs-lookup"><span data-stu-id="e85ed-137">Here is a list of commands that demonstrate how some of the common methods work:</span></span>

```
PS> [System.Math]::Sqrt(9)
3
PS> [System.Math]::Pow(2,3)
8
PS> [System.Math]::Floor(3.3)
3
PS> [System.Math]::Floor(-3.3)
-4
PS> [System.Math]::Ceiling(3.3)
4
PS> [System.Math]::Ceiling(-3.3)
-3
PS> [System.Math]::Max(2,7)
7
PS> [System.Math]::Min(2,7)
2
PS> [System.Math]::Truncate(9.3)
9
PS> [System.Math]::Truncate(-9.3)
-9
```

