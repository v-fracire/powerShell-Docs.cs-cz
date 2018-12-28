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
# <a name="get-test-set"></a>Get-Test-Set

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

![Získání, testu a nastavení](/media/get-test-set.png)

Je postavena na PowerShell Desired State Configuration **získat**, **testovací**, a **nastavit** procesu. DSC [prostředky](resources.md) každý obsahuje metody pro dokončení každé z těchto operací. V [konfigurace](../configurations/configurations.md), definujete prostředek bloky vyplnit klíče, které se stanou parametry pro určitý prostředek **získat**, **testovací**, a **nastavit** metody.

Toto je syntaxe **služby** prostředků bloku. **Služby** nakonfiguruje prostředku služby Windows.

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

**Získat**, **testovací**, a **nastavit** metody **služby** prostředků bude mít parametr bloků, které tyto hodnoty.

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
> Jazyk a metodu používanou k definování zdroje určuje, jak **získat**, **testovací**, a **nastavit** bude obsahovat definici metody.

Protože **služby** prostředků má jenom jeden klíč požadované (`Name`), **služby** bloku prostředek může být stejně jednoduché jako tato:

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

Při kompilaci konfigurace výše uvedené hodnoty, které zadáte pro klíč jsou uložené v souboru ".mof", který je generován. Další informace najdete v tématu [MOF](/windows/desktop/wmisdk/managed-object-format--mof-).

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

Při použití [Local Configuration Manageru](../managing-nodes/metaConfig.md) čtení ze souboru ".mof" hodnota "Zařazování" a předat ho metodě `-Name` parametr **získat**, **Test**, a **nastavit** metody pro instanci "Moje_služba" **služby** prostředků.

## <a name="get"></a>Get

**Získat** metoda prostředku, načte stav prostředku, protože je nakonfigurovaná na cílový uzel. Tento stav se vrátí jako [zatřiďovací tabulky](/powershell/module/microsoft.powershell.core/about/about_hash_tables). Klíče **zatřiďovací tabulky** bude konfigurovatelných hodnot nebo parametry přijímá prostředku.

**Získat** metoda mapuje přímo [Get-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/get-dscconfiguration) rutiny. Při volání `Get-DSCConfiguration`, spuštění LCM **získat** metoda každého prostředku v současné době použité konfiguraci. LCM používá hodnoty klíče uložené v souboru "MOF" jako parametry pro každý odpovídající instance prostředku.

Toto je ukázkový výstup z **služby** prostředek, který konfiguruje službu architektura "Zařazování".

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

Výstup zobrazuje aktuální hodnota vlastnosti konfigurovatelné podle **služby** prostředků.

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

## <a name="test"></a>Test

**Testovací** metoda prostředku určuje, zda cílový uzel je nyní kompatibilní s prostředku *požadovaného stavu*. **Testovací** vrátí metoda `$True` nebo `$False` pouze k určení, jestli je uzel kompatibilní.
Při volání [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration), volání LCM **Test** metoda každého prostředku v současné době použité konfiguraci. LCM používá hodnoty klíče uložené v souboru "MOF" jako parametry pro každý odpovídající instance prostředku.

Pokud výsledek všechny jednotlivé prostředky **testovací** je `$False`, `Test-DSCConfiguration` vrátí `$False` označující, že uzel není kompatibilní. Pokud všechny prostředky **testovací** metody vrací `$True`, `Test-DSCConfiguration` vrátí `$True` k označení, zda je uzel kompatibilní.

```powershell
Test-DSCConfiguration
```

```output
True
```

V Powershellu 5.0 `-Detailed` parametr byl přidán. Určení `-Detailed` způsobí, že `Test-DSCConfiguration` vrátit objekt, který obsahuje kolekce výsledků pro kompatibilní a nekompatibilní prostředky.

```powershell
Test-DSCConfiguration -Detailed
```

```output
PSComputerName  ResourcesInDesiredState        ResourcesNotInDesiredState     InDesiredState
--------------  -----------------------        --------------------------     --------------
localhost       {[Service]Spooler}                                            True
```

Další informace najdete v tématu [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)

## <a name="set"></a>Nastavit

**Nastavit** metoda prostředku se pokusí vynutit uzel, který má být kompatibilní s prostředku *požadovaného stavu*. **Nastavit** metoda je určena být **idempotentní**, což znamená, že **nastavit** může být spuštění více než jednou a vždy získáte stejný výsledek bez chyb.  Při spuštění [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Start-DSCConfiguration), LCM procházení jednotlivé prostředky v aktuálně použité konfiguraci. LCM načte hodnoty klíče pro aktuální instanci prostředků ze souboru ".mof" a použije je jako parametry pro **Test** metody. Pokud **testovací** metoda vrátí hodnotu `$True`, uzlu je kompatibilní s aktuální prostředek a **nastavit** metoda se přeskočí. Pokud **testovací** vrátí `$False`, uzel se jako nevyhovující.  LCM předává prostředku instance klíčové hodnoty jako parametry na prostředek **nastavit** metoda obnovení uzlu na dodržování předpisů.

Zadáním `-Verbose` a `-Wait` parametry, můžete sledovat průběh `Start-DSCConfiguration` rutiny. V tomto příkladu je již uzel kompatibilní. `Verbose` Výstup označuje, že **nastavit** metoda byla přeskočena.

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

## <a name="see-also"></a>Viz taky

- [Přehled Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)
- [Nastavení serveru vyžádané replikace SMB](../pull-server/pullServerSMB.md)
- [Konfigurace načítacího klienta](../pull-server/pullClientConfigID.md)
