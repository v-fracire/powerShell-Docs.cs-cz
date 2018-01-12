# <a name="ws-management-wsman-remoting-in-powershell-core"></a><span data-ttu-id="d9cfa-101">Vzdálenou komunikaci služby WS-Management (WSMan) v prostředí PowerShell jádra</span><span class="sxs-lookup"><span data-stu-id="d9cfa-101">WS-Management (WSMan) Remoting in PowerShell Core</span></span> 

## <a name="instructions-to-create-a-remoting-endpoint"></a><span data-ttu-id="d9cfa-102">Pokyny k vytvoření koncového bodu vzdálené komunikace</span><span class="sxs-lookup"><span data-stu-id="d9cfa-102">Instructions to Create a Remoting Endpoint</span></span>

<span data-ttu-id="d9cfa-103">Balíček základní prostředí PowerShell pro systém Windows obsahuje WinRM modulu plug-in (`pwrshplugin.dll`) a také instalační skript (`Install-PowerShellRemoting.ps1`) v `$PSHome`.</span><span class="sxs-lookup"><span data-stu-id="d9cfa-103">The PowerShell Core package for Windows includes a WinRM plug-in (`pwrshplugin.dll`) and an installation script (`Install-PowerShellRemoting.ps1`) in `$PSHome`.</span></span>
<span data-ttu-id="d9cfa-104">Tyto soubory povolení přijímat příchozí připojení vzdáleného prostředí PowerShell v případě, že její koncový bod je zadán prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9cfa-104">These files enable PowerShell to accept incoming PowerShell remote connections when its endpoint is specified.</span></span>

### <a name="motivation"></a><span data-ttu-id="d9cfa-105">Motivace</span><span class="sxs-lookup"><span data-stu-id="d9cfa-105">Motivation</span></span>

<span data-ttu-id="d9cfa-106">Instalace prostředí PowerShell můžete vytvořit relace prostředí PowerShell vzdálených počítačů pomocí `New-PSSession` a `Enter-PSSession`.</span><span class="sxs-lookup"><span data-stu-id="d9cfa-106">An installation of PowerShell can establish PowerShell sessions to remote computers using `New-PSSession` and `Enter-PSSession`.</span></span>
<span data-ttu-id="d9cfa-107">Povolit příjem příchozích připojení vzdáleného prostředí PowerShell, musí uživatel vytvoření koncového bodu vzdálenou komunikaci služby WinRM.</span><span class="sxs-lookup"><span data-stu-id="d9cfa-107">To enable it to accept incoming PowerShell remote connections, the user must create a WinRM remoting endpoint.</span></span>
<span data-ttu-id="d9cfa-108">Jedná se o explicitní výslovný souhlas scénář kde uživatel spustí instalaci PowerShellRemoting.ps1 se vytvořit koncový bod služby WinRM.</span><span class="sxs-lookup"><span data-stu-id="d9cfa-108">This is an explicit opt-in scenario where the user runs Install-PowerShellRemoting.ps1 to create the WinRM endpoint.</span></span>
<span data-ttu-id="d9cfa-109">Instalační skript je krátkodobé řešení než přidáme další funkce `Enable-PSRemoting` provádět stejné akce.</span><span class="sxs-lookup"><span data-stu-id="d9cfa-109">The installation script is a short-term solution until we add additional functionality to `Enable-PSRemoting` to perform the same action.</span></span>
<span data-ttu-id="d9cfa-110">Další podrobnosti najdete v tématu problém [#1193](https://github.com/PowerShell/PowerShell/issues/1193).</span><span class="sxs-lookup"><span data-stu-id="d9cfa-110">For more details, please see issue [#1193](https://github.com/PowerShell/PowerShell/issues/1193).</span></span>

### <a name="script-actions"></a><span data-ttu-id="d9cfa-111">Akce skriptu</span><span class="sxs-lookup"><span data-stu-id="d9cfa-111">Script Actions</span></span>

<span data-ttu-id="d9cfa-112">Skript</span><span class="sxs-lookup"><span data-stu-id="d9cfa-112">The script</span></span>

1. <span data-ttu-id="d9cfa-113">Vytvoří adresář modulu plug-in v rámci %windir%\System32\PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9cfa-113">Creates a directory for the plug-in within %windir%\System32\PowerShell</span></span>
1. <span data-ttu-id="d9cfa-114">Zkopíruje pwrshplugin.dll do tohoto umístění</span><span class="sxs-lookup"><span data-stu-id="d9cfa-114">Copies pwrshplugin.dll to that location</span></span>
1. <span data-ttu-id="d9cfa-115">Generuje konfiguračního souboru</span><span class="sxs-lookup"><span data-stu-id="d9cfa-115">Generates a configuration file</span></span>
1. <span data-ttu-id="d9cfa-116">Zaregistruje, který modul plug-in s WinRM</span><span class="sxs-lookup"><span data-stu-id="d9cfa-116">Registers that plug-in with WinRM</span></span>

### <a name="registration"></a><span data-ttu-id="d9cfa-117">Registrace</span><span class="sxs-lookup"><span data-stu-id="d9cfa-117">Registration</span></span>

<span data-ttu-id="d9cfa-118">Skript je třeba spustit v relaci prostředí PowerShell na úrovni správce a běží ve dvou režimech.</span><span class="sxs-lookup"><span data-stu-id="d9cfa-118">The script must be executed within an Administrator-level PowerShell session and runs in two modes.</span></span>

#### <a name="executed-by-the-instance-of-powershell-that-it-will-register"></a><span data-ttu-id="d9cfa-119">Provedený instance prostředí PowerShell, které se budou registrovat</span><span class="sxs-lookup"><span data-stu-id="d9cfa-119">Executed by the instance of PowerShell that it will register</span></span>

``` powershell
Install-PowerShellRemoting.ps1
```

#### <a name="executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register"></a><span data-ttu-id="d9cfa-120">Provedený jiná instance prostředí PowerShell jménem instanci, která se budou registrovat</span><span class="sxs-lookup"><span data-stu-id="d9cfa-120">Executed by another instance of PowerShell on behalf of the instance that it will register</span></span>

``` powershell
<path to powershell>\Install-PowerShellRemoting.ps1 -PowerShellHome "<absolute path to the instance's $PSHOME>"
```

<span data-ttu-id="d9cfa-121">Například:</span><span class="sxs-lookup"><span data-stu-id="d9cfa-121">For Example:</span></span>

``` powershell
Set-Location -Path 'C:\Program Files\PowerShell\6.0.0\'
.\Install-PowerShellRemoting.ps1 -PowerShellHome "C:\Program Files\PowerShell\6.0.0\"
```

<span data-ttu-id="d9cfa-122">**Poznámka:** skript registrace vzdálené komunikace restartuje WinRM, tak všechny existující relace PSRP přeruší okamžitě po spuštění skriptu.</span><span class="sxs-lookup"><span data-stu-id="d9cfa-122">**NOTE:** The remoting registration script will restart WinRM, so all existing PSRP sessions will terminate immediately after the script is run.</span></span> <span data-ttu-id="d9cfa-123">Je-li spustit v průběhu vzdálené relace, to se ukončí připojení.</span><span class="sxs-lookup"><span data-stu-id="d9cfa-123">If run during a remote session, this will terminate the connection.</span></span>

## <a name="how-to-connect-to-the-new-endpoint"></a><span data-ttu-id="d9cfa-124">Jak se připojit k nový koncový bod</span><span class="sxs-lookup"><span data-stu-id="d9cfa-124">How to Connect to the New Endpoint</span></span>

<span data-ttu-id="d9cfa-125">Vytvořte relaci prostředí PowerShell na nový koncový bod prostředí PowerShell zadáním `-ConfigurationName "some endpoint name"`.</span><span class="sxs-lookup"><span data-stu-id="d9cfa-125">Create a PowerShell session to the new PowerShell endpoint by specifying `-ConfigurationName "some endpoint name"`.</span></span> <span data-ttu-id="d9cfa-126">Připojit k instanci prostředí PowerShell z v předchozím příkladu, použijte buď:</span><span class="sxs-lookup"><span data-stu-id="d9cfa-126">To connect to the PowerShell instance from the example above, use either:</span></span>

``` powershell
New-PSSession ... -ConfigurationName "powershell.6.0.0"
Enter-PSSession ... -ConfigurationName "powershell.6.0.0"
```

<span data-ttu-id="d9cfa-127">Všimněte si, že `New-PSSession` a `Enter-PSSession` volání, které neurčují `-ConfigurationName` se zaměří na výchozí koncový bod prostředí PowerShell, `microsoft.powershell`.</span><span class="sxs-lookup"><span data-stu-id="d9cfa-127">Note that `New-PSSession` and `Enter-PSSession` invocations that do not specify `-ConfigurationName` will target the default PowerShell endpoint, `microsoft.powershell`.</span></span>
