---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití statických tříd a metod
ms.assetid: 418ad766-afa6-4b8c-9a44-471889af7fd9
ms.openlocfilehash: 0f2b02c3a40365ad0335118b057a4e548c9f6535
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="using-static-classes-and-methods"></a>Použití statických tříd a metod
Ne všechny třídy rozhraní .NET Framework lze vytvořit pomocí **New-Object**. Například pokud se pokusíte vytvořit **System.Environment** nebo **System.Math** objektu s **New-Object**, zobrazí se následující chybové zprávy:

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

Tyto chyby dojít, protože neexistuje žádný způsob, jak vytvořit nový objekt z těchto tříd. Tyto třídy jsou referenční dokumentace knihoven metod a vlastností, které se nemění stavu. Nemusíte je vytvořit, je jednoduše používat. Třídy a metody, jako jsou ty se nazývají *statické třídy* vzhledem k tomu, že nejsou vytvořeny, zničení nebo změnit. Chcete-li to zrušte poskytujeme příklady, které používají statické třídy.

### <a name="getting-environment-data-with-systemenvironment"></a>Získávání dat prostředí s System.Environment
Prvním krokem při práci s objektem v prostředí Windows PowerShell je obvykle, použijte Get-člen a zjistěte, jaké členy obsahuje. S statické třídy je trochu jiný proces, protože skutečná třída není objekt.

#### <a name="referring-to-the-static-systemenvironment-class"></a>Odkazy na statická třída System.Environment
Statická třída může být tím, že název třídy do složených závorek. Například můžete se podívat do **System.Environment** zadáním názvu v závorkách. Díky tomu se zobrazí některé informace obecného typu:

```
PS> [System.Environment]

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     False    Environment                              System.Object
```

> [!NOTE]
> Jak jsme už bylo zmíněno dříve, prostředí Windows PowerShell automaticky přidá '**systému.**' Zadejte názvy při použití **New-Object**. Samé se stane, když pomocí názvu typu v závorkách, takže můžete určit  **\[System.Environment]** jako  **\[prostředí]**.

**System.Environment** třída obsahuje obecné informace o pracovní prostředí aktuální proces, který je powershell.exe při práci v rámci prostředí Windows PowerShell.

Pokud se pokusíte zobrazit podrobnosti o této třídy zadáním  **\[System.Environment] | Get-člen**, typu objektu je oznámil, že je **System.RuntimeType** , nikoli **System.Environment**:

```
PS> [System.Environment] | Get-Member

   TypeName: System.RuntimeType
```

Chcete-li zobrazit statické členy Get-členem, zadejte **statické** parametr:

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

Vlastnosti, které chcete zobrazit z System.Environment jsme teď můžete vybrat.

#### <a name="displaying-static-properties-of-systemenvironment"></a>Statické vlastnosti System.Environment zobrazení

Vlastnosti System.Environment jsou statické a je třeba zadat jiným způsobem než běžné vlastnosti. Používáme **::** označíte, prostředí Windows PowerShell, která by měla spolupracovat s statickou metodu nebo vlastnost. Chcete-li zobrazit příkaz, který byl použitý ke spuštění prostředí Windows PowerShell, jsme zkontrolujte **CommandLine** vlastnost zadáním:

```
PS> [System.Environment]::Commandline
"C:\Program Files\Windows PowerShell\v1.0\powershell.exe"
```

Pokud chcete zkontrolovat verzi operačního systému, zobrazí vlastnost OSVersion zadáním:

```
PS> [System.Environment]::OSVersion

           Platform ServicePack         Version             VersionString
           -------- -----------         -------             -------------
            Win32NT Service Pack 2      5.1.2600.131072     Microsoft Windows...
```

Jsme můžete zkontrolovat, zda je počítač právě vypíná zobrazením **HasShutdownStarted** vlastnost:

```
PS> [System.Environment]::HasShutdownStarted
False
```

### <a name="doing-math-with-systemmath"></a>Provádění matematické s System.Math

Statická třída System.Math je užitečné pro provádění některých matematické operace. Důležité členů **System.Math** jsou většinou metody, které jsme můžete zobrazit pomocí **Get-člen**.

> [!NOTE]
> System.Math má několik metod se stejným názvem, ale jsou rozlišené typ jejich parametrů.

Zadejte následující příkaz k zobrazení seznamu metod **System.Math** třídy.

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

Zobrazí se několik matematickém metod. Tady je seznam příkazů, které ukazují, jak fungují některé běžné metody:

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