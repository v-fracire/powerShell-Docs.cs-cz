---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: ad1d19eeb70a19cd3d1493b9a09b115af755feb4
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="desired-state-configuration-dsc-known-issues-and-limitations"></a>Konfigurace požadovaného stavu (DSC) – známé problémy a omezení

<a name="breaking-change-certificates-used-to-encryptdecrypt-passwords-in-dsc-configurations-may-not-work-after-installing-wmf-50-rtm"></a>Narušující změny: Certifikáty používané k šifrování a dešifrování hesla v konfiguracích DSC nemusí fungovat po instalaci WMF 5.0 RTM
--------------------------------------------------------------------------------------------------------------------------------

Ve verzích WMF 4.0 a WMF 5.0 Preview DSC nepovolí hesla v konfiguraci pro o délce maximálně 121 znaků. DSC byla vynucení použít krátký hesla i v případě, že byl potřeby náročná a silné heslo. Tato změna narušující umožňuje hesla, aby se o libovolné délce v konfiguraci DSC.

**Řešení:** znovu vytvořit certifikát s využití šifrování dat nebo šifrování klíče a použití klíče pro rozšířené šifrování dokumentů (1.3.6.1.4.1.311.80.1). Článku na webu TechNet <https://technet.microsoft.com/library/dn807171.aspx> obsahuje další informace.


<a name="dsc-cmdlets-may-fail-after-installing-wmf-50-rtm"></a>Po instalaci WMF 5.0 RTM, může selhat rutiny DSC
------------------------------------------------------------------------------------
Spuštění DscConfiguration a ostatní rutiny DSC může selhat po instalaci WMF 5.0 RTM, s následující chybou:
```powershell
    LCM failed to retrieve the property PendingJobStep from the object of class dscInternalCache .
    + CategoryInfo : ObjectNotFound: (root/Microsoft/...gurationManager:String) [], CimException
    + FullyQualifiedErrorId : MI RESULT 6
    + PSComputerName : localhost
```

**Řešení:** odstranit DSCEngineCache.mof spuštěním následujícího příkazu v relaci prostředí PowerShell zvýšenými oprávněními (Spustit jako správce):
    
```powershell
Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof
```


<a name="dsc-cmdlets-may-not-work-if-wmf-50-rtm-is-installed-on-top-of-wmf-50-production-preview"></a>Rutiny DSC nemusí fungovat, pokud WMF 5.0 RTM již je nainstalován na WMF 5.0 produkční Preview
------------------------------------------------------
**Řešení:** spuštěním následujícího příkazu v relaci prostředí PowerShell zvýšenými oprávněními (Spustit jako správce):
```powershell
    mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof
```


<a name="lcm-can-go-into-an-unstable-state-while-using-get-dscconfiguration-in-debugmode"></a>LCM můžete přejít do nestabilním stavu, při použití Get-DscConfiguration v režim DebugMode
-------------------------------------------------------------------------------

Pokud LCM v režim DebugMode, kombinace kláves CTRL + C zastavit zpracování Get-DscConfiguration může způsobit LCM přejdete do nestabilním stavu takové této většinu rutin DSC nefungují.

**Řešení:** není při ladění rutiny Get-DscConfiguration stisknutím CTRL + C.


<a name="stop-dscconfiguration-may-hang-in-debugmode"></a>Stop-DscConfiguration může přestat reagovat v režim DebugMode
------------------------------------------------------------------------------------------------------------------------
Pokud LCM v režim DebugMode, zastavte DscConfiguration může přestat reagovat při pokusu o zastavení operace pomocí Get-DscConfiguration

**Řešení:** ukončete ladění operaci Get-DscConfiguration spouštěné, jak je uvedeno v části "[prostředky DSC ladění](https://msdn.microsoft.com/powershell/dsc/debugresource)'.


<a name="no-verbose-error-messages-are-shown-in-debugmode"></a>Žádné podrobné chybové zprávy se zobrazují v režim DebugMode
-----------------------------------------------------------------------------------
Pokud LCM v režim DebugMode, zobrazí se žádné podrobné chybové zprávy z prostředků DSC.

**Řešení:** zakázat *režim DebugMode* zobrazíte podrobné zprávy z prostředku


<a name="invoke-dscresource-operations-cannot-be-retrieved-by-get-dscconfigurationstatus-cmdlet"></a>Vyvolání DscResource operace nelze načíst pomocí rutiny Get-DscConfigurationStatus
--------------------------------------------------------------------------------------
Po pomocí rutiny Invoke-DscResource přímo volat metody jakémukoli prostředku, nemohou být načteni prostřednictvím Get-DscConfigurationStatus záznamy takové operaci později.

**Řešení:** None.


<a name="get-dscconfigurationstatus-returns-pull-cycle-operations-as-type-consistency"></a>Operace Get-DscConfigurationStatus vrátí stažení cyklus jako typ *konzistence*
---------------------------------------------------------------------------------
Uzel je nastavena na režimu aktualizace vyžádání obsahu, pro každou vyžádanou operaci provést, rutina Get-DscConfigurationStatus sestavy typ operace jako *konzistence* místo *počáteční*

**Řešení:** None.

<a name="invoke-dscresource-cmdlet-does-not-return-message-in-the-order-they-were-produced"></a>Rutina Invoke-DscResource nevrací zprávy v pořadí, ve kterém jejich výroby
---------------------------------------------------------------------------------
Rutina Invoke-DscResource nevrací podrobné nastavení, upozornění, a chybové zprávy v pořadí, ve kterém byly vytvořeny LCM nebo prostředek DSC.

**Řešení:** None.


<a name="dsc-resources-cannot-be-debugged-easily-when-used-with-invoke-dscresource"></a>Prostředky DSC nelze snadno ladit, pokud se používá s Invoke-DscResource
-----------------------------------------------------------------------
Pokud LCM běží v režimu ladění (najdete v části [prostředky DSC ladění](https://msdn.microsoft.com/powershell/dsc/debugresource) podrobnosti), rutiny Invoke-DscResource neposkytuje informace o prostředí runspace pro připojení k pro ladění.
**Řešení:** vyhledat a připojit k pomocí rutin prostředí runspace **Get-PSHostProcessInfo**, **Enter PSHostProcess** , **Get-prostředí Runspace** a **Ladění Runspace** k ladění prostředek DSC.

```powershell
# Find all the processes hosting PowerShell
Get-PSHostProcessInfo

ProcessName ProcessId AppDomainName
----------- --------- -------------
powershell 3932 DefaultAppDomain
powershell_ise 2304 DefaultAppDomain
WmiPrvSE 3396 DscPsPluginWkr_AppDomain

# Enter the process that is hosting DSC engine (WMI process with DscPsPluginWkr_Appdomain)
Enter-PSHostProcess -Id 3396 -AppDomainName DscPsPluginWkr_AppDomain

# Find all the available rusnspaces in that process
Get-Runspace

Id Name ComputerName Type State Availability
-- ---- ------------ ---- ----- ------------
2 Runspace2 localhost Local Opened InBreakpoint
5 RemoteHost localhost Local Opened Busy

# Debug the runspace that is in **InBreakpoint** availability state
Debug-Runspace -Id 2
```


<a name="various-partial-configuration-documents-for-same-node-cannot-have-identical-resource-names"></a>Různé dokumentů částečné konfigurace pro stejný uzel nemůže mít názvy identické prostředků
------------------------------------------------------------------------------------------

Pro několik částečné konfigurace, které jsou nasazeny do jednoho uzlu spusťte identické názvy prostředků příčina chyby čas.

**Řešení:** v různých konfigurací. částečné používat jiné názvy pro i stejné prostředky.


<a name="start-dscconfiguration-useexisting-does-not-work-with--credential"></a>Spuštění DscConfiguration – UseExisting nefunguje s - přihlašovacích údajů
------------------------------------------------------------------

Při použití s parametrem – UseExisting Start-DscConfiguration – přihlašovací údaje parametr je ignorován. DSC používá výchozí identitu procesu pokračovat operaci. To způsobí, že chyby pokračovat na vzdáleném uzlu se potřeby různých přihlašovacích údajů.

**Řešení:** použití CIM relace pro vzdálené operace DSC:
```powershell
$session = New-CimSession -ComputerName $node -Credential $credential
Start-DscConfiguration -UseExisting -CimSession $session
```


<a name="ipv6-addresses-as-node-names-in-dsc-configurations"></a>Adresy IPv6 jako názvy uzlů v konfiguracích DSC
--------------------------------------------------
Adresy IPv6 jako názvy ve skriptech konfigurace DSC nejsou v této verzi podporovány.

**Řešení:** None.


<a name="debugging-of-class-based-dsc-resources"></a>Ladění prostředky založené na třídě DSC
--------------------------------------
V této verzi nepodporuje ladění založené na třídě prostředků DSC.

**Řešení:** None.


<a name="variables--functions-defined-in-script-scope-in-dsc-class-based-resource-are-not-preserved-across-multiple-calls-to-a-dsc-resource"></a>Proměnné & funkcí definovaných v oboru $script v prostředek DSC založené na třídě nejsou zachována napříč více volání prostředek DSC 
-------------------------------------------------------------------------------------------------------------------------------------

Více po sobě jdoucí volání počáteční DSCConfiguration se nezdaří, pokud je konfigurace pomocí jakékoli založené na třídě prostředku, který má proměnné nebo funkce, které jsou definované v oboru $script.

**Řešení:** definovat všechny proměnné a funkce v vlastní třídy prostředek DSC. No $script obor proměnné nebo funkce.


<a name="dsc-resource-debugging-when-a-resource-is-using-psdscrunascredential"></a>Když prostředek používá PSDscRunAsCredential ladění prostředků DSC
----------------------------------------------------------------------
Ladění prostředků DSC, když používá prostředku *PSDscRunAsCredential* vlastnosti v konfiguraci není suported v této verzi.

**Řešení:** None.


<a name="psdscrunascredential-is-not-supported-for-dsc-composite-resources"></a>PsDscRunAsCredential není podporována pro složené prostředky DSC
----------------------------------------------------------------

**Řešení:** vlastnost použití pověření, pokud je k dispozici. Příklad ServiceSet a WindowsFeatureSet


<a name="get-dscresource--syntax-does-not-reflect-psdscrunascredential-correctly"></a>*Get-DscResource-syntaxe* nezohledňuje PsDscRunAsCredential správně
-------------------------------------------------------------------------
Get-DscResource-syntaxe nezohledňuje PsDscRunAsCredential správně při prostředků označí je jako povinné nebo ji nepodporuje.

**Řešení:** None. Ale vytváření konfigurace (ISE) v odráží správných metadat o PsDscRunAsCredential vlastnosti při použití technologie IntelliSense.


<a name="windowsoptionalfeature-is-not-available-in-windows-7"></a>WindowsOptionalFeature není k dispozici v systému Windows 7
-----------------------------------------------------

Prostředek WindowsOptionalFeature DSC není k dispozici v systému Windows 7. Tento prostředek vyžaduje modulu DISM a rutin DISM, které jsou k dispozici od verze Windows 8 a novější verze operačního systému Windows.

<a name="for-class-based-dsc-resources-import-dscresource--moduleversion-may-not-work-as-expected"></a>Pro prostředky založené na třídě DSC Import DscResource - ModuleVersion nemusí fungovat podle očekávání   
------------------------------------------------------------------------------------------
Pokud je uzel kompilace více verze založené na třídě DSC prostředků modulu, `Import-DscResource -ModuleVersion` vyberte není zadaná verze a výsledků v následujících došlo k chybě kompilace.

```
ImportClassResourcesFromModule : Exception calling "ImportClassResourcesFromModule" with "3" argument(s): "Keyword 'MyTestResource' already defined in the configuration."
At C:\Windows\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:2035 char:35
+ ... rcesFound = ImportClassResourcesFromModule -Module $mod -Resources $r ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [ImportClassResourcesFromModule], MethodInvocationException
    + FullyQualifiedErrorId : PSInvalidOperationException,ImportClassResourcesFromModule
```

**Řešení:** importovat požadovaná verze definováním *ModuleSpecification* do objektu `-ModuleName` s `RequiredVersion` klíč zadaný následujícím způsobem:
``` PowerShell  
Import-DscResource -ModuleName @{ModuleName='MyModuleName';RequiredVersion='1.2'}  
```  

<a name="some-dsc-resources-like-registry-resource-may-start-to-take-a-long-time-to-process-the-request"></a>Některé prostředky DSC jako registru prostředku může začít trvat dlouhou dobu zpracování žádosti.
--------------------------------------------------------------------------------------------------------------------------------

**Resolution1:** vytvoření plánu úlohy, která pravidelně vyčistí následující složku.
``` PowerShell 
$env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis 
```

**Resolution2:** změnit konfiguraci DSC vyčistěte *CommandAnalysis* složky na konci konfigurace.
``` PowerShell
Configuration $configName
{

   # User Data
    Registry SetRegisteredOwner
    {
        Ensure = 'Present'
        Force = $True
        Key = $Node.RegisteredKey
        ValueName = $Node.RegisteredOwnerValue
        ValueType = 'String'
        ValueData = $Node.RegisteredOwnerData
    }
    #
    # Script to delete the config 
    #
    script DeleteCommandAnalysisCache
    {
        DependsOn="[Registry]SetRegisteredOwner"
        getscript="@{}"
        testscript = 'Remove-Item -Path $env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis -Force -Recurse -ErrorAction SilentlyContinue -ErrorVariable ev | out-null;$true'
        setscript = '$true'
    }
}
```

