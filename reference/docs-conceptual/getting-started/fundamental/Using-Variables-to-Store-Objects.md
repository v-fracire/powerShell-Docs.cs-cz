---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití proměnných k ukládání objektů
ms.assetid: b1688d73-c173-491e-9ba6-6d0c1cc852de
ms.openlocfilehash: e52f0a344d0ad13db42b34bed912d584c99b0e30
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="using-variables-to-store-objects"></a><span data-ttu-id="bc605-103">Použití proměnných k ukládání objektů</span><span class="sxs-lookup"><span data-stu-id="bc605-103">Using Variables to Store Objects</span></span>
<span data-ttu-id="bc605-104">PowerShell funguje s objekty.</span><span class="sxs-lookup"><span data-stu-id="bc605-104">PowerShell works with objects.</span></span> <span data-ttu-id="bc605-105">Prostředí PowerShell umožňuje vytvářet proměnné, které jsou v podstatě s názvem objektů, aby byla zachována výstup pro pozdější použití.</span><span class="sxs-lookup"><span data-stu-id="bc605-105">PowerShell lets you create variables, essentially named objects, to preserve output for later use.</span></span> <span data-ttu-id="bc605-106">Pokud se používají k práci s proměnné v jiných nutný Pamatujte, že proměnné prostředí PowerShell jsou objekty, nikoli textu.</span><span class="sxs-lookup"><span data-stu-id="bc605-106">If you are used to working with variables in other shells remember that PowerShell variables are objects, not text.</span></span>

<span data-ttu-id="bc605-107">Proměnné jsou vždy zadaný počáteční znak $ a může obsahovat alfanumerické znaky nebo podtržítko jejich názvy.</span><span class="sxs-lookup"><span data-stu-id="bc605-107">Variables are always specified with the initial character $, and can include any alphanumeric characters or the underscore in their names.</span></span>

### <a name="creating-a-variable"></a><span data-ttu-id="bc605-108">Vytvoření proměnné</span><span class="sxs-lookup"><span data-stu-id="bc605-108">Creating a Variable</span></span>
<span data-ttu-id="bc605-109">Zadejte platný název proměnné, můžete vytvořit proměnnou:</span><span class="sxs-lookup"><span data-stu-id="bc605-109">You can create a variable by typing a valid variable name:</span></span>

```
PS> $loc
PS>
```

<span data-ttu-id="bc605-110">Tento příkaz vrátí žádný výsledek protože **$loc** nemá hodnotu.</span><span class="sxs-lookup"><span data-stu-id="bc605-110">This returns no result because **$loc** does not have a value.</span></span> <span data-ttu-id="bc605-111">Můžete vytvořit proměnnou a přiřaďte mu hodnotu do jednoho kroku.</span><span class="sxs-lookup"><span data-stu-id="bc605-111">You can create a variable and assign it a value in the same step.</span></span> <span data-ttu-id="bc605-112">Prostředí PowerShell vytvoří proměnnou pouze, pokud neexistuje; jinak přiřadí zadanou hodnotu existující proměnné.</span><span class="sxs-lookup"><span data-stu-id="bc605-112">PowerShell only creates the variable if it does not exist; otherwise, it assigns the specified value to the existing variable.</span></span> <span data-ttu-id="bc605-113">K uložení vaše aktuální umístění v proměnné **$loc**, zadejte:</span><span class="sxs-lookup"><span data-stu-id="bc605-113">To store your current location in the variable **$loc**, type:</span></span>

```
$loc = Get-Location
```

<span data-ttu-id="bc605-114">Neexistuje žádný výstup se zobrazí, když zadáte tento příkaz, protože výstup posílá místní $</span><span class="sxs-lookup"><span data-stu-id="bc605-114">There is no output displayed when you type this command because the output is sent to $loc.</span></span> <span data-ttu-id="bc605-115">V prostředí PowerShell je zobrazený výstup vedlejším účinkem skutečnost, že data, která není jinak směrované, vždy se odešlou do obrazovky.</span><span class="sxs-lookup"><span data-stu-id="bc605-115">In PowerShell, displayed output is a side effect of the fact that data, which is not otherwise directed, always gets sent to the screen.</span></span> <span data-ttu-id="bc605-116">Zadáním $loc zobrazí vaše aktuální umístění:</span><span class="sxs-lookup"><span data-stu-id="bc605-116">Typing $loc will show your current location:</span></span>

```
PS> $loc

Path
----
C:\temp
```

<span data-ttu-id="bc605-117">Můžete použít **Get-člen** zobrazíte informace o obsahu proměnných.</span><span class="sxs-lookup"><span data-stu-id="bc605-117">You can use **Get-Member** to display information about the contents of variables.</span></span> <span data-ttu-id="bc605-118">Potrubí $loc členovi Get vám ukáže, že je **PathInfo** objekt, stejně jako výstup z Get-umístění:</span><span class="sxs-lookup"><span data-stu-id="bc605-118">Piping $loc to Get-Member will show you that it is a **PathInfo** object, just like the output from Get-Location:</span></span>

```
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

### <a name="manipulating-variables"></a><span data-ttu-id="bc605-119">Manipulace s proměnné</span><span class="sxs-lookup"><span data-stu-id="bc605-119">Manipulating Variables</span></span>
<span data-ttu-id="bc605-120">Prostředí PowerShell obsahuje několik příkazů k manipulaci s proměnné.</span><span class="sxs-lookup"><span data-stu-id="bc605-120">PowerShell provides several commands to manipulate variables.</span></span> <span data-ttu-id="bc605-121">Úplný seznam v čitelné podoby zobrazíte zadáním příkazu:</span><span class="sxs-lookup"><span data-stu-id="bc605-121">You can see a complete listing in a readable form by typing:</span></span>

```
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

<span data-ttu-id="bc605-122">Kromě proměnné, které vytvoříte v aktuální relaci prostředí PowerShell existuje několik proměnné definované v systému.</span><span class="sxs-lookup"><span data-stu-id="bc605-122">In addition to the variables you create in your current PowerShell session, there are several system-defined variables.</span></span> <span data-ttu-id="bc605-123">Můžete použít **Remove-Variable** rutiny vyčistit všechny proměnné, které nejsou řízené prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc605-123">You can use the **Remove-Variable** cmdlet to clear out all of the variables which are not controlled by PowerShell.</span></span> <span data-ttu-id="bc605-124">Zadejte následující příkaz k vymazání všech proměnných:</span><span class="sxs-lookup"><span data-stu-id="bc605-124">Type the following command to clear all variables:</span></span>

```
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

<span data-ttu-id="bc605-125">Vznikne tak výzvu k potvrzení, které vidíte níže.</span><span class="sxs-lookup"><span data-stu-id="bc605-125">This will produce the confirmation prompt you see below.</span></span>

```
Confirm
Are you sure you want to perform this action?
Performing operation "Remove Variable" on Target "Name: Error".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):A
```

<span data-ttu-id="bc605-126">Pokud pak spustíte **Get-Variable** rutiny, zobrazí se zbývající proměnné prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc605-126">If you then run the **Get-Variable** cmdlet, you will see the remaining PowerShell variables.</span></span> <span data-ttu-id="bc605-127">Vzhledem k tomu, že je také proměnná jednotku prostředí PowerShell, můžete také zobrazit všechny proměnné prostředí PowerShell zadáním:</span><span class="sxs-lookup"><span data-stu-id="bc605-127">Since there is also a variable PowerShell drive, you can also display all PowerShell variables by typing:</span></span>

```
Get-ChildItem variable:
```

### <a name="using-cmdexe-variables"></a><span data-ttu-id="bc605-128">Použití proměnných Cmd.exe</span><span class="sxs-lookup"><span data-stu-id="bc605-128">Using Cmd.exe Variables</span></span>
<span data-ttu-id="bc605-129">I když prostředí PowerShell není Cmd.exe, běží v prostředí shell příkazového a stejné proměnné, které jsou k dispozici v jakémkoli prostředí, můžete použít v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="bc605-129">Although PowerShell is not Cmd.exe, it runs in a command shell environment and can use the same variables available in any environment in Windows.</span></span> <span data-ttu-id="bc605-130">Tyto proměnné se zveřejňují přes jednotku s názvem **env**:.</span><span class="sxs-lookup"><span data-stu-id="bc605-130">These variables are exposed through a drive named **env**:.</span></span> <span data-ttu-id="bc605-131">Tyto proměnné můžete zobrazit zadáním:</span><span class="sxs-lookup"><span data-stu-id="bc605-131">You can view these variables by typing:</span></span>

```
Get-ChildItem env:
```

<span data-ttu-id="bc605-132">I když standardní rutiny proměnné nejsou navrženy pro práci s **env:** proměnné, stále můžete například vytvořit zadáním **env:** předponu.</span><span class="sxs-lookup"><span data-stu-id="bc605-132">Although the standard variable cmdlets are not designed to work with **env:** variables, you can still use them by specifying the **env:** prefix.</span></span> <span data-ttu-id="bc605-133">Například informace o kořenový adresář operačního systému, můžete použít příkazového prostředí **% SystemRoot %** proměnnou z prostředí PowerShell zadáním:</span><span class="sxs-lookup"><span data-stu-id="bc605-133">For example, to see the operating system root directory, you can use the command-shell **%SystemRoot%** variable from within PowerShell by typing:</span></span>

```
PS> $env:SystemRoot
C:\WINDOWS
```

<span data-ttu-id="bc605-134">Můžete také vytvořit a upravit proměnné prostředí z prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc605-134">You can also create and modify environment variables from within PowerShell.</span></span> <span data-ttu-id="bc605-135">Proměnné prostředí, které jsou k němu přistupovat z prostředí Windows PowerShell požadavkům normální pravidla pro proměnné prostředí jinde v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="bc605-135">Environment variables accessed from Windows PowerShell conform to the normal rules for environment variables elsewhere in Windows.</span></span>