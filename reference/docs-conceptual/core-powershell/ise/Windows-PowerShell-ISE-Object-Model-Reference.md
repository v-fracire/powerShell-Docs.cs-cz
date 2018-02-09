---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Referenční informace o objektovém modelu prostředí Windows PowerShell ISE"
ms.assetid: e1a9e7d1-0fd5-47de-8d9b-f1be1ed13b0c
ms.openlocfilehash: 624ddca3895ba3e24bf52a27babdb07e8714baae
ms.sourcegitcommit: 18e3bfae83ffe282d3fd1a45f5386f3b7250f0c0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/08/2018
---
# <a name="windows-powershell-ise-object-model-reference"></a>Referenční informace o objektovém modelu prostředí Windows PowerShell ISE
  
## <a name="object-model-reference"></a>Odkaz na objekt modelu
 Tato část obsahuje odkaz na základní třídy, která definují různé objekty inWindows PowerShell® Integrované skriptovací prostředí (ISE). Objekty, které jsou uspořádány do jejich hierarchie najdete v sekci [hierarchie ISE objektového modelu](The-ISE-Object-Model-Hierarchy.md).

 [Objekt ISEAddOnTool](The-ISEAddOnTool-Object.md) příklady: $psISE.CurrentVisibleHorizontalTool, $psISE.CurrentVisibleVerticalTool.

 [Objekt ISEAddOnTool](The-ISEAddOnTool-Object.md) [objekt ISEEditor](The-ISEEditor-Object.md) příklady: $psISE.CurrentFile.Editor, $psISE.CurrentPowerShellTab.Output, $psISE.CurrentPowerShellTab.CommandPane.

 [Objekt ISEFile](The-ISEFile-Object.md) příklady: $psISE.CurrentFile, $psISE.PowerShellTabs.Files\[0\].

 [Objekt ISEFileCollection](The-ISEFileCollection-Object.md) příklady: $psISE.PowerShellTabs.Files.

 [Objekt ISEMenuItem](The-ISEMenuItem-Object.md) příklady: $psISE.CurrentPowerShellTab.AddOnsMenu, $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus\[0\].

 [Objekt ISEMenuItemCollection](The-ISEMenuItemCollection-Object.md) příklad: $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.

 [Objekt ISEOptions](The-ISEOptions-Object.md) příklady: $psISE.Options, $psISE.Options.DefaultOptions.

 [Objekt ObjectModelRoot](The-ObjectModelRoot-Object.md) příklad: kořenový $psISE objekt.

 [Objekt PowerShellTab](The-PowerShellTab-Object.md) příklady: $psISE.CurrentPowerShellTab, $psISE.PowerShellTabs\[0\].

 [Objekt PowerShellTabCollection](The-PowerShellTabCollection-Object.md) příklad: $psISE.PowerShellTabs.

## <a name="see-also"></a>Viz také
- [ISE Windows PowerShell skriptování objektový Model](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
