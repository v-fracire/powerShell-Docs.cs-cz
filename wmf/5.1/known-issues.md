---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Známé problémy v WMF 5.1
ms.openlocfilehash: d53031bea978087c68fcb22989c7cd2e2cf2d9fa
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="known-issues-in-wmf-51"></a>Známé problémy v WMF 5.1 #

> Poznámka: Tyto informace se mohou změnit.

## <a name="starting-powershell-shortcut-as-administrator"></a>Počáteční zástupce prostředí PowerShell jako správce
Po instalaci WMF, pokud se pokusíte spustit PowerShell jako správce pomocí zástupce, můžete obdržet zprávu "Nespecifikovaná chyba".
Otevřete zástupce jako bez oprávnění správce a zástupce teď funguje i jako správce.

## <a name="pester"></a>Pester
V této verzi existují dva problémy, které byste měli vědět, když používáte Pester na Nano Server:

* Spouštění testů proti Pester samotné může způsobit některé selhání kvůli rozdíly mezi úplné CLR a základní CLR. Na konkrétní metodu Validate není k dispozici na typ dokumentu XML. Šest testy, které se pokoušejí o ověření schématu NUnit výstupní protokoly jsou známé selhání.
* Jeden pokrytí kódu test nezdaří aktuálně, protože *WindowsFeature* prostředek DSC v Nano Server neexistuje. Ale tyto chyby jsou obvykle neškodný a můžete bezpečně ignorovat.

## <a name="operation-validation"></a>Ověření operace

* Update-Help selže pro modul Microsoft.PowerShell.Operation.Validation z důvodu mimo pracovní Nápověda identifikátor URI

## <a name="dsc-after-uninstall-wmf"></a>DSC po odinstalaci WMF
* Odinstalace WMF neodstraní DSC MOF dokumenty ve složce Konfigurace. DSC nebude pracovat správně, pokud MOF dokumenty obsahují novější vlastností, které nejsou k dispozici na starších systémů. V takovém případě spusťte následující skript zvýšenými konzole PowerShell vyčistěte stavy DSC.
 ```powershell
    $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
            "$env:windir\system32\configuration\*.mof.checksum",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
           )

    $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
 ```

## <a name="jea-virtual-accounts"></a>JEA virtuální účty
JEA koncových bodů a konfigurace relace, které jsou nakonfigurované na používání virtuální účty v WMF 5.0 nebude nakonfigurovaný na používání virtuálních účtu po upgradu na WMF 5.1.
To znamená, že příkazy běží v relacích JEA budou spouštěny pod identitu připojování uživatelů místo dočasný správce účtu, potenciálně bránit uživateli v příkazů, které vyžadují zvýšená oprávnění.
Pokud chcete obnovit virtuální účty, musíte zrušit registraci a znovu zaregistrovat všechny konfigurace relace, které používají virtuální účty.

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
