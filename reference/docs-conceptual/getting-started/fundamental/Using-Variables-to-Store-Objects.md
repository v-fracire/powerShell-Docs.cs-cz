---
ms.date: 08/27/2018
keywords: rutiny prostředí PowerShell
title: Použití proměnných k ukládání objektů
ms.assetid: b1688d73-c173-491e-9ba6-6d0c1cc852de
ms.openlocfilehash: 3168b64039a601857f9c684108de5770f88329e3
ms.sourcegitcommit: 59727f71dc204785a1bcdedc02716d8340a77aeb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2018
ms.locfileid: "43134054"
---
# <a name="using-variables-to-store-objects"></a><span data-ttu-id="a28fe-103">Použití proměnných k ukládání objektů</span><span class="sxs-lookup"><span data-stu-id="a28fe-103">Using variables to store objects</span></span>

<span data-ttu-id="a28fe-104">Prostředí PowerShell funguje s objekty.</span><span class="sxs-lookup"><span data-stu-id="a28fe-104">PowerShell works with objects.</span></span> <span data-ttu-id="a28fe-105">Prostředí PowerShell vám umožňuje vytvoření pojmenovaných objektů, které jsou známé jako proměnné.</span><span class="sxs-lookup"><span data-stu-id="a28fe-105">PowerShell lets you create named objects known as variables.</span></span>
<span data-ttu-id="a28fe-106">Názvy proměnných může obsahovat alfanumerické znaky může znak podtržítka.</span><span class="sxs-lookup"><span data-stu-id="a28fe-106">Variables names can include the underscore character can any alphanumeric characters.</span></span> <span data-ttu-id="a28fe-107">Při použití v prostředí PowerShell, proměnná je vždy určena pomocí \$ znak následovaný název proměnné.</span><span class="sxs-lookup"><span data-stu-id="a28fe-107">When used in PowerShell, a variable is always specified using the \$ character followed by variable name.</span></span>

## <a name="creating-a-variable"></a><span data-ttu-id="a28fe-108">Vytváření proměnných</span><span class="sxs-lookup"><span data-stu-id="a28fe-108">Creating a variable</span></span>

<span data-ttu-id="a28fe-109">Zadejte platný název proměnné, můžete vytvořit proměnnou:</span><span class="sxs-lookup"><span data-stu-id="a28fe-109">You can create a variable by typing a valid variable name:</span></span>

```
PS> $loc
PS>
```

<span data-ttu-id="a28fe-110">V tomto příkladu vrátí žádný výsledek, protože `$loc` nemá žádnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="a28fe-110">This example returns no result because `$loc` doesn't have a value.</span></span> <span data-ttu-id="a28fe-111">Můžete vytvořit proměnnou a přiřaďte mu hodnotu do jednoho kroku.</span><span class="sxs-lookup"><span data-stu-id="a28fe-111">You can create a variable and assign it a value in the same step.</span></span> <span data-ttu-id="a28fe-112">Prostředí PowerShell vytvoří pouze proměnné, pokud neexistuje.</span><span class="sxs-lookup"><span data-stu-id="a28fe-112">PowerShell only creates the variable if it doesn't exist.</span></span>
<span data-ttu-id="a28fe-113">V opačném případě přiřazuje zadanou hodnotu existující proměnné.</span><span class="sxs-lookup"><span data-stu-id="a28fe-113">Otherwise, it assigns the specified value to the existing variable.</span></span> <span data-ttu-id="a28fe-114">Následující příklad uloží aktuální umístění do proměnné `$loc`:</span><span class="sxs-lookup"><span data-stu-id="a28fe-114">The following example stores the current location in the variable `$loc`:</span></span>

```powershell
$loc = Get-Location
```

<span data-ttu-id="a28fe-115">Prostředí PowerShell když zadáte tento příkaz nezobrazí se žádný výstup.</span><span class="sxs-lookup"><span data-stu-id="a28fe-115">PowerShell displays no output when you type this command.</span></span> <span data-ttu-id="a28fe-116">Prostředí PowerShell odešle výstup "Get-Location" `$loc`.</span><span class="sxs-lookup"><span data-stu-id="a28fe-116">PowerShell sends the output of 'Get-Location' to `$loc`.</span></span> <span data-ttu-id="a28fe-117">V prostředí PowerShell posílá data, která není přiřazené nebo je přesměrován na obrazovku.</span><span class="sxs-lookup"><span data-stu-id="a28fe-117">In PowerShell, data that isn't assigned or redirected is sent to the screen.</span></span> <span data-ttu-id="a28fe-118">Zadáním `$loc` zobrazuje aktuální umístění:</span><span class="sxs-lookup"><span data-stu-id="a28fe-118">Typing `$loc` shows your current location:</span></span>

```
PS> $loc

Path
----
C:\temp
```

<span data-ttu-id="a28fe-119">Můžete použít `Get-Member` k zobrazení informací o obsahu proměnné.</span><span class="sxs-lookup"><span data-stu-id="a28fe-119">You can use `Get-Member` to display information about the contents of variables.</span></span> <span data-ttu-id="a28fe-120">`Get-Member` ukazuje, že `$loc` je **PathInfo** objektu, stejně jako výstup z `Get-Location`:</span><span class="sxs-lookup"><span data-stu-id="a28fe-120">`Get-Member` shows you that `$loc` is a **PathInfo** object, just like the output from `Get-Location`:</span></span>

```powershell
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

## <a name="manipulating-variables"></a><span data-ttu-id="a28fe-121">Manipulace s proměnné</span><span class="sxs-lookup"><span data-stu-id="a28fe-121">Manipulating variables</span></span>

<span data-ttu-id="a28fe-122">PowerShell nabízí několik příkazy pro manipulaci s proměnné.</span><span class="sxs-lookup"><span data-stu-id="a28fe-122">PowerShell provides several commands to manipulate variables.</span></span> <span data-ttu-id="a28fe-123">Úplný seznam ve formě čitelné zobrazíte zadáním příkazu:</span><span class="sxs-lookup"><span data-stu-id="a28fe-123">You can see a complete listing in a readable form by typing:</span></span>

```powershell
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

<span data-ttu-id="a28fe-124">Prostředí PowerShell také vytvoří několik proměnných definovaných systémem.</span><span class="sxs-lookup"><span data-stu-id="a28fe-124">PowerShell also creates several system-defined variables.</span></span> <span data-ttu-id="a28fe-125">Můžete použít `Remove-Variable` rutina pro odebrání proměnné, které nejsou řízeny pomocí prostředí PowerShell, z aktuální relace.</span><span class="sxs-lookup"><span data-stu-id="a28fe-125">You can use the `Remove-Variable` cmdlet to remove variables, which are not controlled by PowerShell, from the current session.</span></span> <span data-ttu-id="a28fe-126">Zadejte následující příkaz pro vymazání všech proměnných:</span><span class="sxs-lookup"><span data-stu-id="a28fe-126">Type the following command to clear all variables:</span></span>

```powershell
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

<span data-ttu-id="a28fe-127">Po spuštění předchozího příkazu `Get-Variable` rutina ukazuje systémové proměnné prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a28fe-127">After running the previous command, the `Get-Variable` cmdlet shows the PowerShell system variables.</span></span>

<span data-ttu-id="a28fe-128">Prostředí PowerShell také vytvoří proměnné jednotku.</span><span class="sxs-lookup"><span data-stu-id="a28fe-128">PowerShell also creates a variable drive.</span></span> <span data-ttu-id="a28fe-129">Chcete-li zobrazit všechny proměnné prostředí PowerShell pomocí proměnné jednotky použijte následující příklad:</span><span class="sxs-lookup"><span data-stu-id="a28fe-129">Use the following example to display all PowerShell variables using the variable drive:</span></span>

```powershell
Get-ChildItem variable:
```

## <a name="using-cmdexe-variables"></a><span data-ttu-id="a28fe-130">Použití proměnných Cmd.exe</span><span class="sxs-lookup"><span data-stu-id="a28fe-130">Using Cmd.exe variables</span></span>

<span data-ttu-id="a28fe-131">Prostředí PowerShell můžete použít stejné proměnné prostředí, která je k dispozici pro jakýkoli proces Windows, včetně Cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="a28fe-131">PowerShell can use the same environment variables available to any Windows process, including Cmd.exe.</span></span> <span data-ttu-id="a28fe-132">Tyto proměnné jsou vystaveny prostřednictvím jednotku s názvem `env:`.</span><span class="sxs-lookup"><span data-stu-id="a28fe-132">These variables are exposed through a drive named `env:`.</span></span> <span data-ttu-id="a28fe-133">Tyto proměnné můžete zobrazit zadáním následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="a28fe-133">You can view these variables by typing the following command:</span></span>

```powershell
Get-ChildItem env:
```

<span data-ttu-id="a28fe-134">Standardní `*-Variable` rutin nejsou navržené pro práci s proměnnými prostředí.</span><span class="sxs-lookup"><span data-stu-id="a28fe-134">The standard `*-Variable` cmdlets aren't designed to work with environment variables.</span></span> <span data-ttu-id="a28fe-135">Proměnné prostředí jsou přístupné pomocí `env:` předponu jednotky.</span><span class="sxs-lookup"><span data-stu-id="a28fe-135">Environment variables are accessed using the `env:` drive prefix.</span></span> <span data-ttu-id="a28fe-136">Například **adresáře % SystemRoot %** proměnné v Cmd.exe obsahuje název kořenového adresáře operačního systému.</span><span class="sxs-lookup"><span data-stu-id="a28fe-136">For example, the **%SystemRoot%** variable in Cmd.exe contains the operating system's root directory name.</span></span> <span data-ttu-id="a28fe-137">V Powershellu, použijte `$env:SystemRoot` pro přístup k stejnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="a28fe-137">In PowerShell, you use `$env:SystemRoot` to access the same value.</span></span>

```
PS> $env:SystemRoot
C:\WINDOWS
```

<span data-ttu-id="a28fe-138">Můžete také vytvořit a upravit proměnné prostředí z v rámci prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a28fe-138">You can also create and modify environment variables from within PowerShell.</span></span> <span data-ttu-id="a28fe-139">Proměnné prostředí v Powershellu použijte stejná pravidla pro proměnné prostředí použít jinde v operačním systému.</span><span class="sxs-lookup"><span data-stu-id="a28fe-139">Environment variables in PowerShell follow the same rules for environment variables used elsewhere in the operating system.</span></span> <span data-ttu-id="a28fe-140">Následující příklad vytvoří novou proměnnou prostředí:</span><span class="sxs-lookup"><span data-stu-id="a28fe-140">The following example creates a new environment variable:</span></span>

```powershell
$env:LIB_PATH='/usr/local/lib'
```

<span data-ttu-id="a28fe-141">I když není vyžadována, je běžné, že názvy proměnných prostředí použít všechna velká písmena.</span><span class="sxs-lookup"><span data-stu-id="a28fe-141">Though not required, is it common for environment variable names to use all uppercase letters.</span></span>