---
ms.date: 06/12/2017
keywords: jea, powershell, zabezpečení
title: Konfigurace registrace funkce JEA
ms.openlocfilehash: 160aa95283da57a10aad5fdd4043adb1354a5db5
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002902"
---
# <a name="registering-jea-configurations"></a>Konfigurace registrace funkce JEA

> Platí pro: Windows PowerShell 5.0

Jakmile budete mít vaše [funkce rolí](role-capabilities.md) a [relace konfigurační soubor](session-configurations.md) vytvořený, poslední krok, abyste mohli používat JEA je registrace koncového bodu JEA.
Registrace koncového bodu JEA systémem zpřístupňuje koncový bod pro uživatele a moduly služby automation.

## <a name="single-machine-configuration"></a>Konfigurace jednoho počítače

Pro malá prostředí, můžete nasadit JEA tak, že zaregistrujete pomocí souboru konfigurace relace [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) rutiny.

Než začnete, ujistěte se, že jsou splněné následující požadavky:
- Jeden nebo více rolí byla vytvořena a umístěny ve složce "RoleCapabilities" platný modulu prostředí PowerShell.
- Soubor konfigurace relace byla vytvořena a testování.
- Uživatel registruje JEA konfigurace má práva správce na systémy.

Musíte také zvolit název vašeho koncového bodu JEA.
Název koncového bodu JEA je povinný, pokud uživatelé chtějí pro připojení k systému prostřednictvím JEA.
Můžete použít [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) rutiny zkontrolovat názvy stávající koncové body v systému.
Koncové body, které začínají znakem "microsoft" je obvykle součástí Windows.
Koncový bod 'microsoft.powershell' je použit při připojování ke koncovému bodu vzdáleného prostředí PowerShell výchozí koncový bod.

```powershell
PS C:\> Get-PSSessionConfiguration | Select-Object Name

Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

Vyhodnoceného vhodný název vašeho koncového bodu JEA spuštěním následujícího příkazu zaregistrujte koncový bod.

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> Výše uvedený příkaz, restartuje službu WinRM v systému.
> To se ukončí všechny relace vzdálené komunikace prostředí PowerShell, jakož i všechny probíhající konfigurace DSC.
> Doporučuje se provést jakékoli produkčního počítače do offline režimu před spuštěním příkazu, aby se zabránilo přerušení provozu firmy.

Pokud je úspěšné registrace, budete chtít [použít JEA](using-jea.md).
Kdykoli; může odstranit soubor konfigurace relace Po registraci koncového bodu není použit.

## <a name="multi-machine-configuration-with-dsc"></a>Konfiguraci více počítačů s DSC

Pokud nasazujete JEA ve více počítačích, je nejjednodušší model nasazení použít JEA [Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) prostředek, který se rychle a konzistentně nasazujte JEA na každém počítači.

Nasazení funkce JEA s DSC, je potřeba zajistit, že jsou splněné následující požadavky:
- Jeden nebo více funkcí role byly vytvořené a přidali na platný modul prostředí PowerShell.
- Modul prostředí PowerShell, který obsahuje role se ukládá ve sdílené složce souboru (jen pro čtení), která je přístupná pomocí každý počítač.
- Nastavení pro konfiguraci relace byla určena. Není nutné k vytvoření souboru konfigurace relace, při použití DSC JEA prostředků.
- Mít přihlašovací údaje, které umožňují provádět akce správy na každém počítači, nebo mají přístup k serveru vyžádané replikace DSC používá ke správě počítačů.
- Jste si stáhli [prostředků DSC JEA](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)

Do cílového počítače (nebo serveru vyžádané replikace, pokud použijete jeden) vytvořte konfiguraci DSC pro vašeho koncového bodu JEA.
V této konfiguraci používáte prostředků DSC JustEnoughAdministration k nastavení relace konfigurační soubor a soubor prostředek, který chcete zkopírovat role funkce ze sdílené složky.

Následující vlastnosti lze konfigurovat pomocí prostředků DSC:
- Definice rolí
- Virtuální účet skupiny
- Název účtu spravované služby skupiny
- Adresář přepisu
- Jednotka uživatele
- Pravidla podmíněného přístupu
- Spouštěcí skripty pro relaci JEA

Syntaxe pro každý z těchto vlastností v konfiguraci DSC je konzistentní se konfigurační soubor pro relaci Powershellu.

Následuje ukázka konfigurace DSC pro obecný server modul údržby.

Předpokládá, že platný modulu prostředí PowerShell, který obsahuje funkce rolí v podsložce "RoleCapabilities" se nachází na "\\\\myfileshare\\JEA" sdílení souborů.


```powershell
Configuration JEAMaintenance
{
    Import-DscResource -Module JustEnoughAdministration, PSDesiredStateConfiguration

    File MaintenanceModule
    {
        SourcePath = "\\myfileshare\JEA\ContosoMaintenance"
        DestinationPath = "C:\Program Files\WindowsPowerShell\Modules\ContosoMaintenance"
        Checksum = "SHA-256"
        Ensure = "Present"
        Type = "Directory"
        Recurse = $true
    }

    JeaEndpoint JEAMaintenanceEndpoint
    {
        EndpointName = "JEAMaintenance"
        RoleDefinitions = "@{ 'CONTOSO\JEAMaintenanceAuditors' = @{ RoleCapabilities = 'GeneralServerMaintenance-Audit' }; 'CONTOSO\JEAMaintenanceAdmins' = @{ RoleCapabilities = 'GeneralServerMaintenance-Audit', 'GeneralServerMaintenance-Admin' } }"
        TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
        DependsOn = '[File]MaintenanceModule'
    }
}
```

Potom tuto konfiguraci můžete použít v systému podle [přímo vyvoláním Local Configuration Manageru](https://msdn.microsoft.com/powershell/dsc/metaconfig) nebo aktualizaci [o přijetí změn konfigurace serveru](https://msdn.microsoft.com/powershell/dsc/pullserver).

Prostředek DSC také umožňuje nahradit výchozí koncový bod vzdálené komunikace Microsoft.PowerShell.
Pokud to uděláte, prostředek automaticky zaregistruje koncový bod unconstrainted zálohování s názvem "Microsoft.PowerShell.Restricted", který má výchozí seznam ACL WinRM (povoluje Remote Management Users a místní správci členy skupiny pro přístup k ní).

## <a name="unregistering-jea-configurations"></a>Ruší se registrace funkce JEA konfigurace

Chcete-li odebrat koncový bod JEA v systému, použijte [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) rutiny.
Zrušení registrace koncového bodu JEA zabrání novým uživatelům vytváření nových relací JEA v systému.
Také vám umožňuje aktualizovat tak, že znovu zaregistrujete soubor konfigurace relace aktualizované pomocí stejného názvu koncového bodu JEA konfigurace.

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> Odregistrace JEA koncový bod způsobí, že Služba WinRM k restartování.
> Přeruší se nejvíce vzdálené správy operace probíhá, včetně jiných relacích Powershellu, rozhraní WMI volání a některé nástroje pro správu.
> Pouze zrušte registraci prostředí PowerShell koncové body během plánované údržby windows.

## <a name="next-steps"></a>Další kroky

- [Testování koncového bodu JEA](using-jea.md)
