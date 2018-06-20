---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 9ead27fd5d4f146e9062488c1c8cc22a073b922e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187098"
---
# <a name="improvements-in-powershell-script-debugging"></a><span data-ttu-id="3b129-102">Vylepšené ladění powershellového skriptu</span><span class="sxs-lookup"><span data-stu-id="3b129-102">Improvements in PowerShell Script Debugging</span></span>

<span data-ttu-id="3b129-103">Množství vylepšení byly provedeny v prostředí PowerShell 5.0 zdokonalování ladění:</span><span class="sxs-lookup"><span data-stu-id="3b129-103">A number of improvements were made in PowerShell 5.0 to enhance the debugging experience:</span></span>

## <a name="break-all"></a><span data-ttu-id="3b129-104">Rozdělit všechny</span><span class="sxs-lookup"><span data-stu-id="3b129-104">Break All</span></span>

<span data-ttu-id="3b129-105">Konzole PowerShell a Windows PowerShell ISE teď umožňují rozdělit na ladicí program ke spouštění skriptů.</span><span class="sxs-lookup"><span data-stu-id="3b129-105">The PowerShell console and Windows PowerShell ISE now allow you to break into the debugger for running scripts.</span></span> <span data-ttu-id="3b129-106">Toto funguje ve místních i vzdálených relací.</span><span class="sxs-lookup"><span data-stu-id="3b129-106">This works in both local and remote sessions.</span></span>

<span data-ttu-id="3b129-107">V konzole, stiskněte klávesu **Ctrl + Break**.</span><span class="sxs-lookup"><span data-stu-id="3b129-107">In the console, press **Ctrl+Break**.</span></span>

<span data-ttu-id="3b129-108">V integrovaném Skriptovacím, stiskněte klávesu **Ctrl + B**, nebo použijte **ladění -> Rozdělit všechny** příkazu nabídky.</span><span class="sxs-lookup"><span data-stu-id="3b129-108">In ISE, press **Ctrl+B**, or use the **Debug -> Break All** menu command.</span></span>

## <a name="remote-debugging-and-remote-file-editing-in-windows-powershell-ise"></a><span data-ttu-id="3b129-109">Vzdálené ladění a vzdálené úpravy souborů v systému Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="3b129-109">Remote debugging and remote file editing in Windows PowerShell ISE</span></span>

<span data-ttu-id="3b129-110">Windows PowerShell ISE nyní umožňuje otevírat a upravovat soubory ve vzdálené relaci spuštěním příkazu PSEdit.</span><span class="sxs-lookup"><span data-stu-id="3b129-110">Windows PowerShell ISE now lets you open and edit files in a remote session by running the PSEdit command.</span></span>
<span data-ttu-id="3b129-111">Například můžete otevřít soubor pro úpravy z příkazového řádku v relaci vzdálené následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="3b129-111">For example, you can open a file for editing from the command line in a remote session as follows:</span></span>

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

<span data-ttu-id="3b129-112">Kromě toho teď můžete upravit a uložit změny v ke vzdálenému souboru, který se automaticky otevře v systému Windows PowerShell ISE při průchodu zarážky.</span><span class="sxs-lookup"><span data-stu-id="3b129-112">In addition, you can now edit and save changes in a remote file that is automatically opened in Windows PowerShell ISE when you hit a breakpoint.</span></span>
<span data-ttu-id="3b129-113">Nyní můžete ladění soubor skriptu, který běží na vzdáleném počítači, upravte soubor opravte chybu a pak znovu spusťte upravené skriptu.</span><span class="sxs-lookup"><span data-stu-id="3b129-113">Now, you can debug a script file that is running on a remote computer, edit the file to fix an error, and then rerun the modified script.</span></span>

## <a name="advanced-script-debugging"></a><span data-ttu-id="3b129-114">Ladění pokročilé skriptů</span><span class="sxs-lookup"><span data-stu-id="3b129-114">Advanced Script Debugging</span></span>

<span data-ttu-id="3b129-115">Existují nové, pokročilé funkce ladění, které umožňují připojení k libovolnému procesu místního počítače, který načetl prostředí Windows PowerShell a ladění libovolný prostředí runspace v tomto procesu.</span><span class="sxs-lookup"><span data-stu-id="3b129-115">There are new, advanced debugging features that let you attach to any local computer process that has loaded Windows PowerShell, and debug arbitrary runspaces in that process.</span></span>

### <a name="runspace-debugging"></a><span data-ttu-id="3b129-116">Ladění prostředí runspace</span><span class="sxs-lookup"><span data-stu-id="3b129-116">Runspace Debugging</span></span>

<span data-ttu-id="3b129-117">Byly přidané nové rutiny, které umožňují seznamu aktuální prostředí runspace v procesu a připojení v konzole pro prostředí Windows PowerShell nebo ISE ladicí program k tohoto prostředí runspace pro ladění skriptů:</span><span class="sxs-lookup"><span data-stu-id="3b129-117">New cmdlets have been added that let you list current runspaces in a process, and attach the Windows PowerShell console or ISE debugger to that runspace for script debugging:</span></span>

-   <span data-ttu-id="3b129-118">Get-prostředí Runspace</span><span class="sxs-lookup"><span data-stu-id="3b129-118">Get-Runspace</span></span>
-   <span data-ttu-id="3b129-119">Ladění Runspace</span><span class="sxs-lookup"><span data-stu-id="3b129-119">Debug-Runspace</span></span>
-   <span data-ttu-id="3b129-120">Povolit RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="3b129-120">Enable-RunspaceDebug</span></span>
-   <span data-ttu-id="3b129-121">Zakázat RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="3b129-121">Disable-RunspaceDebug</span></span>
-   <span data-ttu-id="3b129-122">Get-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="3b129-122">Get-RunspaceDebug</span></span>

### <a name="attach-to-process-hosting-powershell"></a><span data-ttu-id="3b129-123">Připojit k procesu hostování prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b129-123">Attach to Process hosting PowerShell</span></span>

<span data-ttu-id="3b129-124">Nyní můžete připojit k libovolnému počítače procesu, který má prostředí Windows PowerShell načíst.</span><span class="sxs-lookup"><span data-stu-id="3b129-124">You can now attach to any computer process that has Windows PowerShell loaded.</span></span> <span data-ttu-id="3b129-125">To uděláte tak, že zadáte do interaktivní relace v procesu, podobně jako na tom, jak zadat do interaktivní vzdálené relace spuštěním rutiny Enter-PSSession:</span><span class="sxs-lookup"><span data-stu-id="3b129-125">You do this by entering into an interactive session with the process, similarly to how you enter into an interactive remote session by running the Enter-PSSession cmdlet:</span></span>

-   <span data-ttu-id="3b129-126">Zadejte PSHostProcess</span><span class="sxs-lookup"><span data-stu-id="3b129-126">Enter-PSHostProcess</span></span>
-   <span data-ttu-id="3b129-127">Ukončení PSHostProcess</span><span class="sxs-lookup"><span data-stu-id="3b129-127">Exit-PSHostProcess</span></span>
