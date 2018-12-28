---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Get-Test-Set
ms.openlocfilehash: e46710954679bf20f4536c6efbcbd4dafd9e629e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403730"
---
# <a name="get-test-set"></a><span data-ttu-id="95a59-103">Get-Test-Set</span><span class="sxs-lookup"><span data-stu-id="95a59-103">Get-Test-Set</span></span>

><span data-ttu-id="95a59-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="95a59-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

![Získání, testu a nastavení](/media/get-test-set.png)

<span data-ttu-id="95a59-106">Je postavena na PowerShell Desired State Configuration **získat**, **testovací**, a **nastavit** procesu.</span><span class="sxs-lookup"><span data-stu-id="95a59-106">PowerShell Desired State Configuration is constructed around a **Get**, **Test**, and **Set** process.</span></span> <span data-ttu-id="95a59-107">DSC [prostředky](resources.md) každý obsahuje metody pro dokončení každé z těchto operací.</span><span class="sxs-lookup"><span data-stu-id="95a59-107">DSC [resources](resources.md) each contains methods to complete each of these operations.</span></span> <span data-ttu-id="95a59-108">V [konfigurace](../configurations/configurations.md), definujete prostředek bloky vyplnit klíče, které se stanou parametry pro určitý prostředek **získat**, **testovací**, a **nastavit** metody.</span><span class="sxs-lookup"><span data-stu-id="95a59-108">In a [Configuration](../configurations/configurations.md), you define resource blocks to fill in keys that become parameters for a resource's **Get**, **Test**, and **Set** methods.</span></span>

<span data-ttu-id="95a59-109">Toto je syntaxe **služby** prostředků bloku.</span><span class="sxs-lookup"><span data-stu-id="95a59-109">This is the syntax for a **Service** resource block.</span></span> <span data-ttu-id="95a59-110">**Služby** nakonfiguruje prostředku služby Windows.</span><span class="sxs-lookup"><span data-stu-id="95a59-110">The **Service** resource configures Windows services.</span></span>

```syntax
Service [String] #ResourceName
{
    Name = [string]
    [BuiltInAccount = [string]{ LocalService | LocalSystem | NetworkService }]
    [Credential = [PSCredential]]
    [Dependencies = [string[]]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [DisplayName = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Path = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [StartupType = [string]{ Automatic | Disabled | Manual }]
    [State = [string]{ Running | Stopped }]
}
```

<span data-ttu-id="95a59-111">**Získat**, **testovací**, a **nastavit** metody **služby** prostředků bude mít parametr bloků, které tyto hodnoty.</span><span class="sxs-lookup"><span data-stu-id="95a59-111">The **Get**, **Test**, and **Set** methods of the **Service** resource will have parameter blocks that accept these values.</span></span>

```powershell
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [System.String]
        $Name,

        [System.String]
        [ValidateSet("Automatic", "Manual", "Disabled")]
        $StartupType,

        [System.String]
        [ValidateSet("LocalSystem", "LocalService", "NetworkService")]
        $BuiltInAccount,

        [System.Management.Automation.PSCredential]
        [ValidateNotNull()]
        $Credential,

        [System.String]
        [ValidateSet("Running", "Stopped")]
        $State="Running",

        [System.String]
        [ValidateNotNullOrEmpty()]
        $DisplayName,

        [System.String]
        [ValidateNotNullOrEmpty()]
        $Description,

        [System.String]
        [ValidateNotNullOrEmpty()]
        $Path,

        [System.String[]]
        [ValidateNotNullOrEmpty()]
        $Dependencies,

        [System.String]
        [ValidateSet("Present", "Absent")]
        $Ensure="Present"
    )
```

> [!NOTE]
> <span data-ttu-id="95a59-112">Jazyk a metodu používanou k definování zdroje určuje, jak **získat**, **testovací**, a **nastavit** bude obsahovat definici metody.</span><span class="sxs-lookup"><span data-stu-id="95a59-112">The language and method used to define the resource determines how the **Get**, **Test**, and **Set** methods will be defined.</span></span>

<span data-ttu-id="95a59-113">Protože **služby** prostředků má jenom jeden klíč požadované (`Name`), **služby** bloku prostředek může být stejně jednoduché jako tato:</span><span class="sxs-lookup"><span data-stu-id="95a59-113">Because the **Service** resource only has one required key (`Name`), a **Service** block resource could be as simple as this:</span></span>

```powershell
Configuration TestConfig
{
    Import-DSCResource -Name Service
    Node localhost
    {
        Service "MyService"
        {
            Name = "Spooler"
        }
    }
}
```

<span data-ttu-id="95a59-114">Při kompilaci konfigurace výše uvedené hodnoty, které zadáte pro klíč jsou uložené v souboru ".mof", který je generován.</span><span class="sxs-lookup"><span data-stu-id="95a59-114">When you compile the Configuration above, the values you specify for a key are stored in the ".mof" file that is generated.</span></span> <span data-ttu-id="95a59-115">Další informace najdete v tématu [MOF](/windows/desktop/wmisdk/managed-object-format--mof-).</span><span class="sxs-lookup"><span data-stu-id="95a59-115">For more information, see [MOF](/windows/desktop/wmisdk/managed-object-format--mof-).</span></span>

```
instance of MSFT_ServiceResource as $MSFT_ServiceResource1ref
{
SourceInfo = "::5::1::Service";
 ModuleName = "PsDesiredStateConfiguration";
 ResourceID = "[Service]MyService";
 Name = "Spooler";

ModuleVersion = "1.0";

 ConfigurationName = "Test";

};
```

<span data-ttu-id="95a59-116">Při použití [Local Configuration Manageru](../managing-nodes/metaConfig.md) čtení ze souboru ".mof" hodnota "Zařazování" a předat ho metodě `-Name` parametr **získat**, **Test**, a **nastavit** metody pro instanci "Moje_služba" **služby** prostředků.</span><span class="sxs-lookup"><span data-stu-id="95a59-116">When applied, the [Local Configuration Manager](../managing-nodes/metaConfig.md) will read the value "Spooler" from the ".mof" file, and pass it to the `-Name` parameter of the **Get**, **Test**, and **Set** methods for the "MyService" instance of the **Service** resource.</span></span>

## <a name="get"></a><span data-ttu-id="95a59-117">Get</span><span class="sxs-lookup"><span data-stu-id="95a59-117">Get</span></span>

<span data-ttu-id="95a59-118">**Získat** metoda prostředku, načte stav prostředku, protože je nakonfigurovaná na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="95a59-118">The **Get** method of a resource, retrieves the state of the resource as it is configured on the target Node.</span></span> <span data-ttu-id="95a59-119">Tento stav se vrátí jako [zatřiďovací tabulky](/powershell/module/microsoft.powershell.core/about/about_hash_tables).</span><span class="sxs-lookup"><span data-stu-id="95a59-119">This state is returned as a [hashtable](/powershell/module/microsoft.powershell.core/about/about_hash_tables).</span></span> <span data-ttu-id="95a59-120">Klíče **zatřiďovací tabulky** bude konfigurovatelných hodnot nebo parametry přijímá prostředku.</span><span class="sxs-lookup"><span data-stu-id="95a59-120">The keys of the **hashtable** will be the configurable values, or parameters, the resource accepts.</span></span>

<span data-ttu-id="95a59-121">**Získat** metoda mapuje přímo [Get-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/get-dscconfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="95a59-121">The **Get** method maps directly to the [Get-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/get-dscconfiguration) cmdlet.</span></span> <span data-ttu-id="95a59-122">Při volání `Get-DSCConfiguration`, spuštění LCM **získat** metoda každého prostředku v současné době použité konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="95a59-122">When you call `Get-DSCConfiguration`, the LCM runs the **Get** method of each resource in the currently applied configuration.</span></span> <span data-ttu-id="95a59-123">LCM používá hodnoty klíče uložené v souboru "MOF" jako parametry pro každý odpovídající instance prostředku.</span><span class="sxs-lookup"><span data-stu-id="95a59-123">The LCM uses the key values stored in the ".mof" file as parameters to each corresponding resource instance.</span></span>

<span data-ttu-id="95a59-124">Toto je ukázkový výstup z **služby** prostředek, který konfiguruje službu architektura "Zařazování".</span><span class="sxs-lookup"><span data-stu-id="95a59-124">This is sample output from a **Service** resource that configures the "Spooler" service.</span></span>

```output
ConfigurationName    : Test
DependsOn            :
ModuleName           : PsDesiredStateConfiguration
ModuleVersion        : 1.1
PsDscRunAsCredential :
ResourceId           : [Service]Spooler
SourceInfo           :
BuiltInAccount       : LocalSystem
Credential           :
Dependencies         : {RPCSS, http}
Description          : This service spools print jobs and handles interaction with the printer.  If you turn off
                       this service, you won’t be able to print or see your printers.
DisplayName          : Print Spooler
Ensure               :
Name                 : Spooler
Path                 : C:\WINDOWS\System32\spoolsv.exe
StartupType          : Automatic
State                : Running
Status               :
PSComputerName       :
CimClassName         : MSFT_ServiceResource
```

<span data-ttu-id="95a59-125">Výstup zobrazuje aktuální hodnota vlastnosti konfigurovatelné podle **služby** prostředků.</span><span class="sxs-lookup"><span data-stu-id="95a59-125">The output shows the current value properties configurable by the **Service** resource.</span></span>

```syntax
Service [String] #ResourceName
{
    Name = [string]
    [BuiltInAccount = [string]{ LocalService | LocalSystem | NetworkService }]
    [Credential = [PSCredential]]
    [Dependencies = [string[]]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [DisplayName = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Path = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [StartupType = [string]{ Automatic | Disabled | Manual }]
    [State = [string]{ Running | Stopped }]
}
```

## <a name="test"></a><span data-ttu-id="95a59-126">Test</span><span class="sxs-lookup"><span data-stu-id="95a59-126">Test</span></span>

<span data-ttu-id="95a59-127">**Testovací** metoda prostředku určuje, zda cílový uzel je nyní kompatibilní s prostředku *požadovaného stavu*.</span><span class="sxs-lookup"><span data-stu-id="95a59-127">The **Test** method of a resource determines if the target node is currently compliant with the resource's *desired state*.</span></span> <span data-ttu-id="95a59-128">**Testovací** vrátí metoda `$True` nebo `$False` pouze k určení, jestli je uzel kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="95a59-128">The **Test** method returns `$True` or `$False` only to indicate whether the Node is compliant.</span></span>
<span data-ttu-id="95a59-129">Při volání [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration), volání LCM **Test** metoda každého prostředku v současné době použité konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="95a59-129">When you call [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration), the LCM calls the **Test** method of each resource in the currently applied configuration.</span></span> <span data-ttu-id="95a59-130">LCM používá hodnoty klíče uložené v souboru "MOF" jako parametry pro každý odpovídající instance prostředku.</span><span class="sxs-lookup"><span data-stu-id="95a59-130">The LCM uses the key values stored in the ".mof" file as parameters to each corresponding resource instance.</span></span>

<span data-ttu-id="95a59-131">Pokud výsledek všechny jednotlivé prostředky **testovací** je `$False`, `Test-DSCConfiguration` vrátí `$False` označující, že uzel není kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="95a59-131">If the result of any individual resource's **Test** is `$False`, `Test-DSCConfiguration` returns `$False` indicating that the Node is not compliant.</span></span> <span data-ttu-id="95a59-132">Pokud všechny prostředky **testovací** metody vrací `$True`, `Test-DSCConfiguration` vrátí `$True` k označení, zda je uzel kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="95a59-132">If all resource's **Test** methods return `$True`, `Test-DSCConfiguration` returns `$True` to indicate that the Node is compliant.</span></span>

```powershell
Test-DSCConfiguration
```

```output
True
```

<span data-ttu-id="95a59-133">V Powershellu 5.0 `-Detailed` parametr byl přidán.</span><span class="sxs-lookup"><span data-stu-id="95a59-133">Beginning in PowerShell 5.0, the `-Detailed` parameter was added.</span></span> <span data-ttu-id="95a59-134">Určení `-Detailed` způsobí, že `Test-DSCConfiguration` vrátit objekt, který obsahuje kolekce výsledků pro kompatibilní a nekompatibilní prostředky.</span><span class="sxs-lookup"><span data-stu-id="95a59-134">Specifying `-Detailed` causes `Test-DSCConfiguration` to return an object containing collections of results for compliant, and non-compliant resources.</span></span>

```powershell
Test-DSCConfiguration -Detailed
```

```output
PSComputerName  ResourcesInDesiredState        ResourcesNotInDesiredState     InDesiredState
--------------  -----------------------        --------------------------     --------------
localhost       {[Service]Spooler}                                            True
```

<span data-ttu-id="95a59-135">Další informace najdete v tématu [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)</span><span class="sxs-lookup"><span data-stu-id="95a59-135">For more information, see [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)</span></span>

## <a name="set"></a><span data-ttu-id="95a59-136">Nastavit</span><span class="sxs-lookup"><span data-stu-id="95a59-136">Set</span></span>

<span data-ttu-id="95a59-137">**Nastavit** metoda prostředku se pokusí vynutit uzel, který má být kompatibilní s prostředku *požadovaného stavu*.</span><span class="sxs-lookup"><span data-stu-id="95a59-137">The **Set** method of a resource attempts to force the Node to become compliant with the resource's *desired state*.</span></span> <span data-ttu-id="95a59-138">**Nastavit** metoda je určena být **idempotentní**, což znamená, že **nastavit** může být spuštění více než jednou a vždy získáte stejný výsledek bez chyb.</span><span class="sxs-lookup"><span data-stu-id="95a59-138">The **Set** method is meant to be **idempotent**, which means that **Set** could be run multiple times and always get the same result without errors.</span></span>  <span data-ttu-id="95a59-139">Při spuštění [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Start-DSCConfiguration), LCM procházení jednotlivé prostředky v aktuálně použité konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="95a59-139">When you run [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Start-DSCConfiguration), the LCM cycles through each resource in the currently applied configuration.</span></span> <span data-ttu-id="95a59-140">LCM načte hodnoty klíče pro aktuální instanci prostředků ze souboru ".mof" a použije je jako parametry pro **Test** metody.</span><span class="sxs-lookup"><span data-stu-id="95a59-140">The LCM retrieves key values for the current resource instance from the ".mof" file and uses them as parameters for the **Test** method.</span></span> <span data-ttu-id="95a59-141">Pokud **testovací** metoda vrátí hodnotu `$True`, uzlu je kompatibilní s aktuální prostředek a **nastavit** metoda se přeskočí.</span><span class="sxs-lookup"><span data-stu-id="95a59-141">If the **Test** method returns `$True`, the Node is compliant with the current resource, and the **Set** method is skipped.</span></span> <span data-ttu-id="95a59-142">Pokud **testovací** vrátí `$False`, uzel se jako nevyhovující.</span><span class="sxs-lookup"><span data-stu-id="95a59-142">If the **Test** returns `$False`, the Node is non-compliant.</span></span>  <span data-ttu-id="95a59-143">LCM předává prostředku instance klíčové hodnoty jako parametry na prostředek **nastavit** metoda obnovení uzlu na dodržování předpisů.</span><span class="sxs-lookup"><span data-stu-id="95a59-143">The LCM passes the resource instance's key values as parameters to the resource's **Set** method, restoring the Node to compliance.</span></span>

<span data-ttu-id="95a59-144">Zadáním `-Verbose` a `-Wait` parametry, můžete sledovat průběh `Start-DSCConfiguration` rutiny.</span><span class="sxs-lookup"><span data-stu-id="95a59-144">By specifying the `-Verbose` and `-Wait` parameters, you can watch the progress of the `Start-DSCConfiguration` cmdlet.</span></span> <span data-ttu-id="95a59-145">V tomto příkladu je již uzel kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="95a59-145">In this example, the Node is already compliant.</span></span> <span data-ttu-id="95a59-146">`Verbose` Výstup označuje, že **nastavit** metoda byla přeskočena.</span><span class="sxs-lookup"><span data-stu-id="95a59-146">The `Verbose` output indicates that the **Set** method was skipped.</span></span>

```
PS> Start-DSCConfiguration -Verbose -Wait -UseExisting

VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' =
ApplyConfiguration,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' =
root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer SERVER01 with user sid
S-1-5-21-124525095-708259637-1543119021-1282804.
VERBOSE: [SERVER01]:                            [] Starting consistency engine.
VERBOSE: [SERVER01]:                            [] Checking consistency for current configuration.
VERBOSE: [SERVER01]:                            [DSCEngine] Importing the module
C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\DscResources\MSFT_ServiceResource\MSFT
_ServiceResource.psm1 in force mode.
VERBOSE: [SERVER01]: LCM:  [ Start  Resource ]  [[Service]Spooler]
VERBOSE: [SERVER01]: LCM:  [ Start  Test     ]  [[Service]Spooler]
VERBOSE: [SERVER01]:                            [[Service]Spooler] Importing the module MSFT_ServiceResource in
force mode.
VERBOSE: [SERVER01]: LCM:  [ End    Test     ]  [[Service]Spooler]  in 0.2540 seconds.
VERBOSE: [SERVER01]: LCM:  [ Skip   Set      ]  [[Service]Spooler]
VERBOSE: [SERVER01]: LCM:  [ End    Resource ]  [[Service]Spooler]
VERBOSE: [SERVER01]:                            [] Consistency check completed.
VERBOSE: Operation 'Invoke CimMethod' complete.
VERBOSE: Time taken for configuration job to complete is 1.379 seconds
```

## <a name="see-also"></a><span data-ttu-id="95a59-147">Viz taky</span><span class="sxs-lookup"><span data-stu-id="95a59-147">See also</span></span>

- [<span data-ttu-id="95a59-148">Přehled Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="95a59-148">Azure Automation DSC Overview</span></span>](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="95a59-149">Nastavení serveru vyžádané replikace SMB</span><span class="sxs-lookup"><span data-stu-id="95a59-149">Setting up an SMB pull server</span></span>](../pull-server/pullServerSMB.md)
- [<span data-ttu-id="95a59-150">Konfigurace načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="95a59-150">Configuring a pull client</span></span>](../pull-server/pullClientConfigID.md)
