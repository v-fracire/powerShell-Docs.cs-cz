---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Příprava na použití Windows PowerShellu
ms.assetid: 6dc7052d-cc5a-4220-950f-98f963a2b587
ms.openlocfilehash: 5e095984286ff89958dc0a4e3d27e40eae5b2c5e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30950963"
---
# <a name="getting-ready-to-use-windows-powershell"></a>Příprava na použití Windows PowerShellu
Pokud prostředí Windows PowerShell je nainstalován a spuštěn, zvažte následující možnosti instalace. Kdykoli můžete provádět tyto úlohy.

- **Instalaci souborů nápovědy.** Rutiny, které jsou zahrnuty v prostředí Windows PowerShell 3.0 není součástí soubory nápovědy. Můžete však použít [Update-Help](/powershell/module/microsoft.powershell.core/update-help) rutiny stáhnout a nainstalovat nejnovější soubory nápovědy ve vašem počítači. Pokud je nainstalován, můžete použít [Get-Help](/powershell/module/microsoft.powershell.core/get-help) rutiny zobrazit přímo na příkazovém řádku. Další informace najdete v tématu [about_Updatable_Help](/powershell/module/microsoft.powershell.core/about/about_updatable_help).

    Pokud se rozhodnete, že není instalaci souborů nápovědy, můžete stále přečíst témata nápovědy online. Chcete-li najít online verzi tématu nápovědy všechny rutiny, zadejte: `Get-Help <CmdletName> -Online`. Procházet viz témata nápovědy prostředí Windows PowerShell [prostředí PowerShell dokumentaci](/powershell/scripting).

- **Spouštění skriptů.** K zabezpečení prostředí Windows PowerShell se výchozí zásady provádění na prostředí Windows PowerShell je **s omezeným přístupem**. Tato zásada umožňuje spouštět rutiny, ale ne skripty. Chcete-li spustit skripty, použijte [Set-ExecutionPolicy](/powershell/module/microsoft.powershell.security/set-executionpolicy) rutiny změňte zásadu spouštění na **AllSigned** nebo **RemoteSigned**. Tuto rutinu můžete spustit pouze členové skupiny Administrators v počítači. Další informace najdete v tématu [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

- **Povolte vzdálenou komunikaci.** V systému je již nakonfigurován pro můžete spouštět vzdálené příkazy na jiných počítačích. Na Windows Server 2012 R2 a Windows Server 2012 systém je také nakonfigurován pro příjem vzdálených příkazů, který je, aby ostatní počítače spouštět vzdálené příkazy na místním počítači. Chcete-li povolit počítačích s jinými verzemi systému Windows pro příjem vzdálených příkazů, spusťte [Enable-PSRemoting](/powershell/module/microsoft.powershell.core/enable-psremoting) rutiny v počítači, který chcete vzdáleně spravovat. Tuto rutinu můžete spustit pouze členové skupiny Administrators v počítači. Další informace najdete v tématu [about_Remote](/powershell/module/microsoft.powershell.core/about/about_remote).

    Poznámka: Pokud je povolena vzdálená komunikace na počítači se systémem Windows PowerShell 2.0, je povolena vzdálená komunikace stále po instalaci Windows Management Framework 3.0. Ale v systému Windows Server 2008 (není Windows Server 2008 R2), je nutné znovu povolit vzdálenou komunikaci po instalaci Windows Management Framework 3.0.

## <a name="see-also"></a>Viz také
- [Instalace prostředí Windows PowerShell](../setup/Installing-Windows-PowerShell.md)
- [Spuštění prostředí Windows PowerShell](/powershell/scripting/setup/starting-windows-powershell)