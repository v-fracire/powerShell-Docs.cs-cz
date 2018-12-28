---
ms.date: 08/27/2018
keywords: rutiny prostředí PowerShell
title: Použití proměnných k ukládání objektů
ms.assetid: b1688d73-c173-491e-9ba6-6d0c1cc852de
ms.openlocfilehash: d166ec58dc658c1b134030c9a9592249ee40d4f5
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403705"
---
# <a name="using-variables-to-store-objects"></a><span data-ttu-id="86496-103">Použití proměnných k ukládání objektů</span><span class="sxs-lookup"><span data-stu-id="86496-103">Using variables to store objects</span></span>

<span data-ttu-id="86496-104">Prostředí PowerShell funguje s objekty.</span><span class="sxs-lookup"><span data-stu-id="86496-104">PowerShell works with objects.</span></span> <span data-ttu-id="86496-105">Prostředí PowerShell vám umožňuje vytvoření pojmenovaných objektů, které jsou známé jako proměnné.</span><span class="sxs-lookup"><span data-stu-id="86496-105">PowerShell lets you create named objects known as variables.</span></span>
<span data-ttu-id="86496-106">Názvy proměnných může obsahovat znak podtržítka a alfanumerické znaky.</span><span class="sxs-lookup"><span data-stu-id="86496-106">Variable names can include the underscore character and any alphanumeric characters.</span></span> <span data-ttu-id="86496-107">Při použití v prostředí PowerShell, proměnná je vždy určena pomocí \$ znak následovaný název proměnné.</span><span class="sxs-lookup"><span data-stu-id="86496-107">When used in PowerShell, a variable is always specified using the \$ character followed by variable name.</span></span>

## <a name="creating-a-variable"></a><span data-ttu-id="86496-108">Vytváření proměnných</span><span class="sxs-lookup"><span data-stu-id="86496-108">Creating a variable</span></span>

<span data-ttu-id="86496-109">Zadejte platný název proměnné, můžete vytvořit proměnnou:</span><span class="sxs-lookup"><span data-stu-id="86496-109">You can create a variable by typing a valid variable name:</span></span>

```
PS> $loc
PS>
```

<span data-ttu-id="86496-110">V tomto příkladu vrátí žádný výsledek, protože `$loc` nemá žádnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="86496-110">This example returns no result because `$loc` doesn't have a value.</span></span> <span data-ttu-id="86496-111">Můžete vytvořit proměnnou a přiřaďte mu hodnotu do jednoho kroku.</span><span class="sxs-lookup"><span data-stu-id="86496-111">You can create a variable and assign it a value in the same step.</span></span> <span data-ttu-id="86496-112">Prostředí PowerShell vytvoří pouze proměnné, pokud neexistuje.</span><span class="sxs-lookup"><span data-stu-id="86496-112">PowerShell only creates the variable if it doesn't exist.</span></span>
<span data-ttu-id="86496-113">V opačném případě přiřazuje zadanou hodnotu existující proměnné.</span><span class="sxs-lookup"><span data-stu-id="86496-113">Otherwise, it assigns the specified value to the existing variable.</span></span> <span data-ttu-id="86496-114">Následující příklad uloží aktuální umístění do proměnné `$loc`:</span><span class="sxs-lookup"><span data-stu-id="86496-114">The following example stores the current location in the variable `$loc`:</span></span>

```powershell
$loc = Get-Location
```

<span data-ttu-id="86496-115">Prostředí PowerShell když zadáte tento příkaz nezobrazí se žádný výstup.</span><span class="sxs-lookup"><span data-stu-id="86496-115">PowerShell displays no output when you type this command.</span></span> <span data-ttu-id="86496-116">Prostředí PowerShell odešle výstup "Get-Location" `$loc`.</span><span class="sxs-lookup"><span data-stu-id="86496-116">PowerShell sends the output of 'Get-Location' to `$loc`.</span></span> <span data-ttu-id="86496-117">V prostředí PowerShell posílá data, která není přiřazené nebo je přesměrován na obrazovku.</span><span class="sxs-lookup"><span data-stu-id="86496-117">In PowerShell, data that isn't assigned or redirected is sent to the screen.</span></span> <span data-ttu-id="86496-118">Zadáním `$loc` zobrazuje aktuální umístění:</span><span class="sxs-lookup"><span data-stu-id="86496-118">Typing `$loc` shows your current location:</span></span>

```
PS> $loc

Path
----
C:\temp
```

<span data-ttu-id="86496-119">Můžete použít `Get-Member` k zobrazení informací o obsahu proměnné.</span><span class="sxs-lookup"><span data-stu-id="86496-119">You can use `Get-Member` to display information about the contents of variables.</span></span> <span data-ttu-id="86496-120">`Get-Member` ukazuje, že `$loc` je **PathInfo** objektu, stejně jako výstup z `Get-Location`:</span><span class="sxs-lookup"><span data-stu-id="86496-120">`Get-Member` shows you that `$loc` is a **PathInfo** object, just like the output from `Get-Location`:</span></span>

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

## <a name="manipulating-variables"></a><span data-ttu-id="86496-121">Manipulace s proměnné</span><span class="sxs-lookup"><span data-stu-id="86496-121">Manipulating variables</span></span>

<span data-ttu-id="86496-122">PowerShell nabízí několik příkazy pro manipulaci s proměnné.</span><span class="sxs-lookup"><span data-stu-id="86496-122">PowerShell provides several commands to manipulate variables.</span></span> <span data-ttu-id="86496-123">Úplný seznam ve formě čitelné zobrazíte zadáním příkazu:</span><span class="sxs-lookup"><span data-stu-id="86496-123">You can see a complete listing in a readable form by typing:</span></span>

```powershell
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

<span data-ttu-id="86496-124">Prostředí PowerShell také vytvoří několik proměnných definovaných systémem.</span><span class="sxs-lookup"><span data-stu-id="86496-124">PowerShell also creates several system-defined variables.</span></span> <span data-ttu-id="86496-125">Můžete použít `Remove-Variable` rutina pro odebrání proměnné, které nejsou řízeny pomocí prostředí PowerShell, z aktuální relace.</span><span class="sxs-lookup"><span data-stu-id="86496-125">You can use the `Remove-Variable` cmdlet to remove variables, which are not controlled by PowerShell, from the current session.</span></span> <span data-ttu-id="86496-126">Zadejte následující příkaz pro vymazání všech proměnných:</span><span class="sxs-lookup"><span data-stu-id="86496-126">Type the following command to clear all variables:</span></span>

```powershell
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

<span data-ttu-id="86496-127">Po spuštění předchozího příkazu `Get-Variable` rutina ukazuje systémové proměnné prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86496-127">After running the previous command, the `Get-Variable` cmdlet shows the PowerShell system variables.</span></span>

<span data-ttu-id="86496-128">Prostředí PowerShell také vytvoří proměnné jednotku.</span><span class="sxs-lookup"><span data-stu-id="86496-128">PowerShell also creates a variable drive.</span></span> <span data-ttu-id="86496-129">Chcete-li zobrazit všechny proměnné prostředí PowerShell pomocí proměnné jednotky použijte následující příklad:</span><span class="sxs-lookup"><span data-stu-id="86496-129">Use the following example to display all PowerShell variables using the variable drive:</span></span>

```powershell
Get-ChildItem variable:
```

## <a name="using-cmdexe-variables"></a><span data-ttu-id="86496-130">Použití proměnných cmd.exe</span><span class="sxs-lookup"><span data-stu-id="86496-130">Using cmd.exe variables</span></span>

<span data-ttu-id="86496-131">Prostředí PowerShell můžete použít stejné proměnné prostředí, která je k dispozici pro jakýkoli proces Windows, včetně **cmd.exe**.</span><span class="sxs-lookup"><span data-stu-id="86496-131">PowerShell can use the same environment variables available to any Windows process, including **cmd.exe**.</span></span> <span data-ttu-id="86496-132">Tyto proměnné jsou vystaveny prostřednictvím jednotku s názvem `env:`.</span><span class="sxs-lookup"><span data-stu-id="86496-132">These variables are exposed through a drive named `env:`.</span></span> <span data-ttu-id="86496-133">Tyto proměnné můžete zobrazit zadáním následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="86496-133">You can view these variables by typing the following command:</span></span>

```powershell
Get-ChildItem env:
```

<span data-ttu-id="86496-134">Standardní `*-Variable` rutin nejsou navržené pro práci s proměnnými prostředí.</span><span class="sxs-lookup"><span data-stu-id="86496-134">The standard `*-Variable` cmdlets aren't designed to work with environment variables.</span></span> <span data-ttu-id="86496-135">Proměnné prostředí jsou přístupné pomocí `env:` předponu jednotky.</span><span class="sxs-lookup"><span data-stu-id="86496-135">Environment variables are accessed using the `env:` drive prefix.</span></span> <span data-ttu-id="86496-136">Například **adresáře % SystemRoot %** proměnné v **cmd.exe** obsahuje název kořenového adresáře operačního systému.</span><span class="sxs-lookup"><span data-stu-id="86496-136">For example, the **%SystemRoot%** variable in **cmd.exe** contains the operating system's root directory name.</span></span> <span data-ttu-id="86496-137">V Powershellu, použijte `$env:SystemRoot` pro přístup k stejnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="86496-137">In PowerShell, you use `$env:SystemRoot` to access the same value.</span></span>

```
PS> $env:SystemRoot
C:\WINDOWS
```

<span data-ttu-id="86496-138">Můžete také vytvořit a upravit proměnné prostředí z v rámci prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86496-138">You can also create and modify environment variables from within PowerShell.</span></span> <span data-ttu-id="86496-139">Proměnné prostředí v Powershellu použijte stejná pravidla pro proměnné prostředí použít jinde v operačním systému.</span><span class="sxs-lookup"><span data-stu-id="86496-139">Environment variables in PowerShell follow the same rules for environment variables used elsewhere in the operating system.</span></span> <span data-ttu-id="86496-140">Následující příklad vytvoří novou proměnnou prostředí:</span><span class="sxs-lookup"><span data-stu-id="86496-140">The following example creates a new environment variable:</span></span>

```powershell
$env:LIB_PATH='/usr/local/lib'
```

<span data-ttu-id="86496-141">I když není vyžadována, je běžné, že názvy proměnných prostředí použít všechna velká písmena.</span><span class="sxs-lookup"><span data-stu-id="86496-141">Though not required, is it common for environment variable names to use all uppercase letters.</span></span>
