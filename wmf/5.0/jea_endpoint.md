---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 66db78cfb136f22cad9078d7113dad085ee667a5
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188424"
---
# <a name="creating-and-connecting-to-a-jea-endpoint"></a><span data-ttu-id="95611-102">Vytvoření koncového bodu JEA a připojení k tomuto bodu</span><span class="sxs-lookup"><span data-stu-id="95611-102">Creating and Connecting to a JEA Endpoint</span></span>
<span data-ttu-id="95611-103">Chcete-li vytvořit koncový bod JEA, je potřeba vytvořit a registrovat souboru speciálně nakonfigurované konfiguraci relace prostředí PowerShell, který se dá vygenerovat pomocí **New-PSSessionConfigurationFile** rutiny.</span><span class="sxs-lookup"><span data-stu-id="95611-103">To create a JEA endpoint, you need to create and register a specially-configured PowerShell Session Configuration file, which can be generated with the **New-PSSessionConfigurationFile** cmdlet.</span></span>

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -TranscriptDirectory "C:\ProgramData\JEATranscripts" -RunAsVirtualAccount -RoleDefinitions @{ 'CONTOSO\NonAdmin_Operators' = @{ RoleCapabilities = 'Maintenance' }} -Path "$env:ProgramData\JEAConfiguration\Demo.pssc"
```

<span data-ttu-id="95611-104">Tím se vytvoří soubor konfigurace relace, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="95611-104">This will create a session configuration file that looks like this:</span></span>
```powershell
@{

# Version number of the schema used for this document
SchemaVersion = '2.0.0.0'

# ID used to uniquely identify this document
GUID = 'a384fdd3-5830-4a2c-ac86-cdd1822c3afd'

# Author of this document
Author = 'Administrator'

# Description of the functionality provided by these settings
# Description = ''

# Session type defaults to apply for this session configuration. Can be 'RestrictedRemoteServer' (recommended), 'Empty', or 'Default'
SessionType = 'RestrictedRemoteServer'

# Directory to place session transcripts for this session configuration
TranscriptDirectory = 'C:\ProgramData\JEATranscripts'

# Whether to run this session configuration as the machine's (virtual) administrator account
RunAsVirtualAccount = $true

# Groups associated with machine's (virtual) administrator account
# RunAsVirtualAccountGroups = 'Remote Desktop Users', 'Remote Management Users'

# Scripts to run when applied to a session
# ScriptsToProcess = 'C:\ConfigData\InitScript1.ps1', 'C:\ConfigData\InitScript2.ps1'

# User roles (security groups), and the Role Capabilities that should be applied to them when applied to a session
RoleDefinitions = @{
    'CONTOSO\NonAdmin_Operators' = @{
        'RoleCapabilities' = 'Maintenance' } }

}
```
<span data-ttu-id="95611-105">Při vytváření koncový bod JEA, musíte nastavit následující parametry příkazu (a odpovídající klíče v souboru):</span><span class="sxs-lookup"><span data-stu-id="95611-105">When creating a JEA endpoint, the following parameters of the command (and corresponding keys in the file) must be set:</span></span>
1.  <span data-ttu-id="95611-106">SessionType k RestrictedRemoteServer</span><span class="sxs-lookup"><span data-stu-id="95611-106">SessionType to RestrictedRemoteServer</span></span>
2.  <span data-ttu-id="95611-107">RunAsVirtualAccount k **$true**</span><span class="sxs-lookup"><span data-stu-id="95611-107">RunAsVirtualAccount to **$true**</span></span>
3.  <span data-ttu-id="95611-108">TranscriptPath k adresáři, kde "přes rameno" přepisy se uloží po každé relaci</span><span class="sxs-lookup"><span data-stu-id="95611-108">TranscriptPath to the directory where “over the shoulder” transcripts will be saved after each session</span></span>
4.  <span data-ttu-id="95611-109">RoleDefinitions do zatřiďovací tabulky, která definuje, které skupiny mají přístup k jaké "funkce Role."</span><span class="sxs-lookup"><span data-stu-id="95611-109">RoleDefinitions to a hashtable that defines which groups have access to which “Role Capabilities.”</span></span>  <span data-ttu-id="95611-110">Toto pole definuje **kdo** můžete provést **co** na tento koncový bod.</span><span class="sxs-lookup"><span data-stu-id="95611-110">This field defines **who** can do **what** on this endpoint.</span></span>   <span data-ttu-id="95611-111">Funkce role jsou speciální soubory, které bude za chvíli vysvětlit.</span><span class="sxs-lookup"><span data-stu-id="95611-111">Role Capabilities are special files that will be explained shortly.</span></span>


<span data-ttu-id="95611-112">Pole RoleDefinitions definuje, které skupiny mají přístup k jaké funkce Role.</span><span class="sxs-lookup"><span data-stu-id="95611-112">The RoleDefinitions field defines which groups had access to which Role Capabilities.</span></span>  <span data-ttu-id="95611-113">Funkce Role je soubor, který definuje sadu funkcí, které se zveřejní pro připojení uživatelů.</span><span class="sxs-lookup"><span data-stu-id="95611-113">A Role Capability is a file that defines a set of capabilities that will be exposed to connecting users.</span></span>  <span data-ttu-id="95611-114">Můžete vytvořit Role funkce **New-PSRoleCapabilityFile** příkaz.</span><span class="sxs-lookup"><span data-stu-id="95611-114">You can create Role Capabilities with the **New-PSRoleCapabilityFile** command.</span></span>

```powershell
New-PSRoleCapabilityFile -Path "$env:ProgramFiles\WindowsPowerShell\Modules\DemoModule\RoleCapabilities\Maintenance.psrc"
```

<span data-ttu-id="95611-115">Tím se vygeneruje funkci role šablony, která vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="95611-115">This will generate a template role capability that looks like this:</span></span>
```
@{

# ID used to uniquely identify this document
GUID = '9287a34f-3f0e-4fbe-9dd7-f1361ba9fd65'

# Author of this document
Author = 'Administrator'

# Description of the functionality provided by these settings
# Description = ''

# Company associated with this document
CompanyName = 'Unknown'

# Copyright statement for this document
Copyright = '(c) 2015 Administrator. All rights reserved.'

# Modules to import when applied to a session
# ModulesToImport = 'MyCustomModule', @{ ModuleName = 'MyCustomModule'; ModuleVersion = '1.0.0.0'; GUID = '4d30d5f0-cb16-4898-812d-f20a6c596bdf' }

# Aliases to make visible when applied to a session
# VisibleAliases = 'Item1', 'Item2'

# Cmdlets to make visible when applied to a session
# VisibleCmdlets = 'Invoke-Cmdlet1', @{ Name = 'Invoke-Cmdlet2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }

# Functions to make visible when applied to a session
# VisibleFunctions = 'Invoke-Function1', @{ Name = 'Invoke-Function2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }

# External commands (scripts and applications) to make visible when applied to a session
# VisibleExternalCommands = 'Item1', 'Item2'

# Providers to make visible when applied to a session
# VisibleProviders = 'Item1', 'Item2'

# Scripts to run when applied to a session
# ScriptsToProcess = 'C:\ConfigData\InitScript1.ps1', 'C:\ConfigData\InitScript2.ps1'

# Aliases to be defined when applied to a session
# AliasDefinitions = @{ Name = 'Alias1'; Value = 'Invoke-Alias1'}, @{ Name = 'Alias2'; Value = 'Invoke-Alias2'}

# Functions to define when applied to a session
# FunctionDefinitions = @{ Name = 'MyFunction'; ScriptBlock = { param($MyInput) $MyInput } }

# Variables to define when applied to a session
# VariableDefinitions = @{ Name = 'Variable1'; Value = { 'Dynamic' + 'InitialValue' } }, @{ Name = 'Variable2'; Value = 'StaticInitialValue' }

# Environment variables to define when applied to a session
# EnvironmentVariables = @{ Variable1 = 'Value1'; Variable2 = 'Value2' }

# Type files (.ps1xml) to load when applied to a session
# TypesToProcess = 'C:\ConfigData\MyTypes.ps1xml', 'C:\ConfigData\OtherTypes.ps1xml'

# Format files (.ps1xml) to load when applied to a session
# FormatsToProcess = 'C:\ConfigData\MyFormats.ps1xml', 'C:\ConfigData\OtherFormats.ps1xml'

# Assemblies to load when applied to a session
# AssembliesToLoad = 'System.Web', 'System.OtherAssembly, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'

}

```
<span data-ttu-id="95611-116">Konfigurace relace JEA se má používat, musíte ho uložit možnosti Role jako platný modul prostředí PowerShell v adresáři s názvem "RoleCapabilities".</span><span class="sxs-lookup"><span data-stu-id="95611-116">To be used by a JEA session configuration, Role Capabilities must be saved as a valid PowerShell module in a directory named “RoleCapabilities”.</span></span> <span data-ttu-id="95611-117">Modul může obsahovat několik souborů funkce role, v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="95611-117">A module may have multiple role capability files, if desired.</span></span>

<span data-ttu-id="95611-118">Pro spuštění konfigurace rutin, funkcí, aliasy a skripty, které uživatel může přistupovat k při připojování k relaci JEA, přidejte do souboru schopnosti Role následující komentáři se šablony svých vlastních pravidel.</span><span class="sxs-lookup"><span data-stu-id="95611-118">To start configuring which cmdlets, functions, aliases, and scripts a user may access when connecting to a JEA session, add your own rules to the Role Capability file following the commented out templates.</span></span> <span data-ttu-id="95611-119">Pro hlubší podívejte se na tom, jak můžete konfigurovat Role schopnosti, podívejte se na celý [prostředí průvodce](http://aka.ms/JEA).</span><span class="sxs-lookup"><span data-stu-id="95611-119">For a deeper look into how you can configure Role Capabilities, check out the full [experience guide](http://aka.ms/JEA).</span></span>

<span data-ttu-id="95611-120">Nakonec po dokončení přizpůsobení konfigurace relace a související možnosti Role zaregistrovat tuto konfiguraci relace a vytvořit koncový bod spuštěním **Register-PSSessionConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="95611-120">Finally, once you have finished customizing your session configuration and related Role Capabilities, register this session configuration and create the endpoint by running **Register-PSSessionConfiguration**.</span></span>

```powershell
Register-PSSessionConfiguration -Name Maintenance -Path "C:\ProgramData\JEAConfiguration\Demo.pssc"
```

## <a name="connect-to-a-jea-endpoint"></a><span data-ttu-id="95611-121">Připojení ke koncovému bodu JEA</span><span class="sxs-lookup"><span data-stu-id="95611-121">Connect to a JEA Endpoint</span></span>
<span data-ttu-id="95611-122">Připojení ke koncovému bodu JEA funguje stejným způsobem připojení k jakékoli jiné výtvory koncový bod prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="95611-122">Connecting to a JEA Endpoint works the same way connecting to any other PowerShell endpoint works.</span></span>  <span data-ttu-id="95611-123">Jednoduše muset poskytnout název koncového bodu JEA jako parametr "ConfigurationName" pro **New-PSSession**, **Invoke-Command**, nebo **Enter-PSSession**.</span><span class="sxs-lookup"><span data-stu-id="95611-123">You simply have to give your JEA endpoint name as the “ConfigurationName” parameter for **New-PSSession**, **Invoke-Command**, or **Enter-PSSession**.</span></span>

```powershell
Enter-PSSession -ConfigurationName Maintenance -ComputerName localhost
```
<span data-ttu-id="95611-124">Jakmile se připojíte k relaci JEA, bude omezena na seznam povolených adres příkazy spuštěné v roli možnosti, které máte přístup k.</span><span class="sxs-lookup"><span data-stu-id="95611-124">Once you have connected to the JEA session, you will be limited to running the commands whitelisted in the Role Capabilities that you have access to.</span></span> <span data-ttu-id="95611-125">Pokud se pokusíte spustit libovolný příkaz není povolen pro vaši roli, bude dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="95611-125">If you try to run any command not allowed for your role, you will encounter an error.</span></span>
