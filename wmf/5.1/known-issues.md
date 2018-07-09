---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Známé problémy ve WMF 5.1
ms.openlocfilehash: 74e5a6763a8a780000bf876f34caa9646a2a416a
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892133"
---
# <a name="known-issues-in-wmf-51"></a>Známé problémy ve WMF 5.1

> [!Note]
> Tyto informace se mohou změnit.

## <a name="starting-powershell-shortcut-as-administrator"></a>Spouští se místní prostředí PowerShell jako správce

Po instalaci WMF, pokud se pokusíte spustit PowerShell jako správce z místní, může zobrazit zpráva "Nespecifikovaná chyba".
Znovu otevřít místní jako bez oprávnění správce a zástupce teď funguje i jako správce.

## <a name="pester"></a>Pester

V této verzi jsou dva problémy, které byste měli vědět, když používáte Pester na Nano serveru:

- Spouštění testů proti Pester sám může způsobit nějaké chyby kvůli rozdílům mezi úplné CLR a CORE CLR. Zejména není k dispozici u typu třídou XMLDocument nastavenou na metodu Validate. Šest testů, které k pokusu o ověření schématu NUnit výstupní protokoly se ví nezdaří.
- Jeden test pokrytí kódu nezdaří aktuálně, protože *WindowsFeature* prostředek DSC na Nano serveru neexistuje. Ale tyto chyby jsou obvykle neškodné a můžete bezpečně ignorovat.

## <a name="operation-validation"></a>Ověření operace

- `Update-Help` pro modul Microsoft.PowerShell.Operation.Validation kvůli nefunkční pomocný identifikátor URI se nezdaří

## <a name="dsc-after-uninstall-wmf"></a>DSC po odinstalaci WMF

- Odinstalace WMF nedojde k odstranění dokumentů DSC MOF ve složce Konfigurace. DSC nebude fungovat správně, pokud MOF dokumenty obsahují novější vlastnosti, které nejsou k dispozici na starších systémů. V takovém případě spusťte následující skript z se zvýšenými oprávněními konzole Powershellu k vyčištění stavy DSC.

  ```powershell
    $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
            "$env:windir\system32\configuration\*.mof.checksum",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
           )
    $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
  ```

## <a name="jea-virtual-accounts"></a>JEA virtuální účty

Použití virtuální účet po upgradu na WMF 5.1 nenakonfigurují koncových bodů JEA a konfigurace relace, které umožňují použít virtuální účty ve WMF 5.0.
To znamená, že příkazy se spouští v relacích JEA spustí pod identitou uživatele připojujícího ne s účtem správce dočasné potenciálně s příkazy, které vyžadují zvýšená oprávnění spustit uživatel.
Pokud chcete obnovit virtuální účty, budete muset zrušit registraci a přeregistrovat konfigurace relace, které používají virtuální účty.

```powershell
# Find the JEA endpoint by its name
$jea = Get-PSSessionConfiguration -Name MyJeaEndpoint

# Copy the cached PSSC file so it can be re-registered
$pssc = Copy-Item $jea.ConfigFilePath $env:temp -PassThru

# Unregister the current PSSC
Unregister-PSSessionConfiguration -Name $jea.Name

# Re-register the PSSC
Register-PSSessionConfiguration -Name $jea.Name -Path $pssc.FullName -Force

# Ensure the access policies remain the same
Set-PSSessionConfiguration -Name $newjea.Name -SecurityDescriptorSddl $jea.SecurityDescriptorSddl
```