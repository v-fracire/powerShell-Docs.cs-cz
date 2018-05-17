---
ms.date: 06/12/2017
keywords: jea, prostředí powershell, zabezpečení
title: Registrace JEA konfigurace
ms.openlocfilehash: cda899b20378b0183a3d88ecfd593aaf7356e967
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="registering-jea-configurations"></a>Registrace JEA konfigurace

> Platí pro: prostředí Windows PowerShell 5.0

Poslední krok, abyste mohli používat JEA, až budete mít vaše [role možnosti](role-capabilities.md) a [relace konfigurační soubor](session-configurations.md) vytvořený a zaregistrujte koncový bod JEA je.
Tento proces informace o konfiguraci relace se vztahuje na systém a zpřístupní koncový bod pro uživatele a automatizace moduly.

## <a name="single-machine-configuration"></a>Konfigurace jednoho počítače

Pro malá prostředí, můžete nasadit JEA registrace pomocí souboru konfigurace relace [Register-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/register-pssessionconfiguration) rutiny.

Než začnete, ujistěte se, že byly splněny následující požadavky:
- Jeden nebo více rolí byla vytvořena a umístěný ve složce 'RoleCapabilities' platný modulu prostředí PowerShell.
- Konfigurační soubor relace byla vytvořena a otestovat.
- Uživatel registruje konfigurace JEA má práva správce na systémy.

Musíte také vyberte název pro svůj koncový bod JEA.
Název koncového bodu JEA se bude vyžadovat, když uživatelé se chcete připojit k systému prostřednictvím JEA.
Můžete použít [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) rutiny Zkontrolujte názvy stávající koncové body v systému.
Koncové body, které začínají "microsoft", jsou obvykle dodávané se systémem Windows.
Koncový bod, microsoft.powershell, je výchozí koncový bod používat při připojování ke vzdálený koncový bod prostředí PowerShell.

```powershell
PS C:\> Get-PSSessionConfiguration | Select-Object Name

Name
----
microsoft.powershell
microsoft.powershell.workflow
microsoft.powershell32
```

Pokud zjistíte, vhodný název pro svůj koncový bod JEA, spusťte následující příkaz k registraci koncového bodu.

```powershell
Register-PSSessionConfiguration -Path .\MyJEAConfig.pssc -Name 'JEAMaintenance' -Force
```

> [!WARNING]
> Výše uvedený příkaz restartuje službu WinRM na serveru.
> To, přeruší se všechny relace vzdálenou komunikaci prostředí PowerShell a také všechny probíhající konfigurace DSC.
> Doporučujeme je provést všechny produkčního počítače do offline režimu před spuštěním příkazu, aby se zabránilo přerušení provoz firmy.

Pokud byla registrace úspěšná, jste připraveni k [použít JEA](using-jea.md).
Kdykoli; může odstranit konfiguračního souboru relace Po registraci se nepoužívá.

## <a name="multi-machine-configuration-with-dsc"></a>Víc počítačů konfigurace s DSC

Pokud nasazujete JEA ve více počítačích, je nejjednodušší model nasazení použít JEA [konfigurace požadovaného stavu](https://msdn.microsoft.com/en-us/powershell/dsc/overview) prostředek pro rychle a konzistentně nasazujte JEA na každém počítači.

Pokud chcete nasadit JEA s DSC, budete muset Ujistěte se, že jsou splněny následující požadavky:
- Jeden nebo více možností role byly vytvořené a přidat na platný modul prostředí PowerShell.
- Modul prostředí PowerShell, který obsahuje role je uložená na sdílené složce souborů (jen pro čtení), která je přístupný pomocí každý počítač.
- Nastavení pro konfiguraci relace byly určeny. Není nutné vytvořit konfigurační soubor relace při používání JEA DSC prostředků.
- Máte přihlašovací údaje, které vám umožní provádět akce správy na každém počítači, nebo mají přístup k serveru vyžádané replikace DSC používat ke správě těchto počítačů.
- Jste si stáhli [prostředek JEA DSC](https://github.com/PowerShell/JEA/tree/master/DSC%20Resource)

Do cílového počítače (nebo načítacího serveru, pokud ji používáte) vytvořte konfiguraci DSC pro koncový bod služby JEA.
V této konfiguraci použijete prostředek JustEnoughAdministration DSC nastavit relace konfigurační soubor a soubor prostředků pro kopírování prostřednictvím možnosti role ze sdílené složky.

Následující vlastnosti se dá konfigurovat pomocí prostředek DSC:
- Definice rolí
- Virtuální účet skupiny
- Název účtu spravované služby skupiny
- Přepis adresáře
- Jednotka uživatele
- Pravidla podmíněného přístupu
- Spouštěcí skripty pro relaci JEA

Syntaxe pro každou z těchto vlastností v konfiguraci DSC je konzistentní s konfiguračního souboru relace prostředí PowerShell.

Níže je ukázka konfigurace DSC pro modul obecný server údržby.

Předpokládá, že platný modul PowerShell obsahující možnosti role v podsložce 'RoleCapabilities' se nachází na '\\\\myfileshare\\JEA se sdílené složky.


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

Tato konfigurace lze potom použít v systému podle [přímo vyvolání správce místní konfigurace](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) nebo aktualizaci [konfigurace serveru vyžádané](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver).

Prostředek DSC umožňuje nahradit Microsoft.PowerShell vzdálenou komunikaci výchozí koncový bod.
Pokud to uděláte, bude prostředek automaticky zaregistrovat koncový bod zálohování unconstrainted s názvem "Microsoft.PowerShell.Restricted", který má výchozí seznam ACL WinRM (povolení Remote Management Users a místní správci členy skupiny pro přístup k ní).

## <a name="unregistering-jea-configurations"></a>Zrušení registrace JEA konfigurace

Pokud chcete odstranit koncový bod JEA v systému, použijte [Unregister-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Unregister-PSSessionConfiguration) rutiny.
Zrušení registrace koncový bod JEA zabrání novým uživatelům ve vytváření nových JEA relací v systému.
Také vám umožňuje aktualizovat konfiguraci JEA opakováním registrace konfigurační soubor aktualizované relace pomocí stejného názvu koncového bodu.

```powershell
# Unregister the JEA endpoint called "ContosoMaintenance"
Unregister-PSSessionConfiguration -Name 'ContosoMaintenance' -Force
```

> [!WARNING]
> Zrušení registrace JEA koncový bod způsobí, že Služba WinRM restartovat.
> To přeruší vzdálený operace správy v průběhu, včetně jiných relací prostředí PowerShell, volání rozhraní WMI a některé nástroje pro správu.
> Pouze zrušte registraci prostředí PowerShell koncové body během plánované údržby windows.

## <a name="next-steps"></a>Další kroky

- [Testování JEA koncový bod](using-jea.md)