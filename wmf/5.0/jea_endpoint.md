---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 9065315ef39129e6a28234d972fe350fd5e7e11d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="creating-and-connecting-to-a-jea-endpoint"></a>Vytvoření koncového bodu JEA a připojení k tomuto bodu
Chcete-li vytvořit koncový bod JEA, je potřeba vytvořit a registrovat souboru speciálně nakonfigurované konfiguraci relace prostředí PowerShell, který se dá vygenerovat pomocí **New-PSSessionConfigurationFile** rutiny.

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -TranscriptDirectory "C:\ProgramData\JEATranscripts" -RunAsVirtualAccount -RoleDefinitions @{ 'CONTOSO\NonAdmin_Operators' = @{ RoleCapabilities = 'Maintenance' }} -Path "$env:ProgramData\JEAConfiguration\Demo.pssc"
```

Tím se vytvoří soubor konfigurace relace, který vypadá takto:
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
Při vytváření koncový bod JEA, musíte nastavit následující parametry příkazu (a odpovídající klíče v souboru):
1.  SessionType k RestrictedRemoteServer
2.  RunAsVirtualAccount k **$true**
3.  TranscriptPath k adresáři, kde "přes rameno" přepisy se uloží po každé relaci
4.  RoleDefinitions do zatřiďovací tabulky, která definuje, které skupiny mají přístup k jaké "funkce Role."  Toto pole definuje **kdo** můžete provést **co** na tento koncový bod.   Funkce role jsou speciální soubory, které bude za chvíli vysvětlit.


Pole RoleDefinitions definuje, které skupiny mají přístup k jaké funkce Role.  Funkce Role je soubor, který definuje sadu funkcí, které se zveřejní pro připojení uživatelů.  Můžete vytvořit Role funkce **New-PSRoleCapabilityFile** příkaz.

```powershell
New-PSRoleCapabilityFile -Path "$env:ProgramFiles\WindowsPowerShell\Modules\DemoModule\RoleCapabilities\Maintenance.psrc"
```

Tím se vygeneruje funkci role šablony, která vypadá takto:
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
Konfigurace relace JEA se má používat, musíte ho uložit možnosti Role jako platný modul prostředí PowerShell v adresáři s názvem "RoleCapabilities". Modul může obsahovat několik souborů funkce role, v případě potřeby.

Pro spuštění konfigurace rutin, funkcí, aliasy a skripty, které uživatel může přistupovat k při připojování k relaci JEA, přidejte do souboru schopnosti Role následující komentáři se šablony svých vlastních pravidel. Pro hlubší podívejte se na tom, jak můžete konfigurovat Role schopnosti, podívejte se na celý [prostředí průvodce](http://aka.ms/JEA).

Nakonec po dokončení přizpůsobení konfigurace relace a související možnosti Role zaregistrovat tuto konfiguraci relace a vytvořit koncový bod spuštěním **Register-PSSessionConfiguration**.

```powershell
Register-PSSessionConfiguration -Name Maintenance -Path "C:\ProgramData\JEAConfiguration\Demo.pssc"
```

## <a name="connect-to-a-jea-endpoint"></a>Připojení ke koncovému bodu JEA
Připojení ke koncovému bodu JEA funguje stejným způsobem připojení k jakékoli jiné výtvory koncový bod prostředí PowerShell.  Jednoduše muset poskytnout název koncového bodu JEA jako parametr "ConfigurationName" pro **New-PSSession**, **Invoke-Command**, nebo **Enter-PSSession**.

```powershell
Enter-PSSession -ConfigurationName Maintenance -ComputerName localhost
```
Jakmile se připojíte k relaci JEA, bude omezena na seznam povolených adres příkazy spuštěné v roli možnosti, které máte přístup k. Pokud se pokusíte spustit libovolný příkaz není povolen pro vaši roli, bude dojde k chybě.