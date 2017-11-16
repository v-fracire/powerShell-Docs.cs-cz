---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Hierarchie ISE objektů modelu"
ms.openlocfilehash: 2df6d40f39dbe14bd3f46a6400cde4a6e91052ef
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="the-ise-object-model-hierarchy"></a>Hierarchie ISE objektů modelu
Toto téma ukazuje hierarchii objektů, které jsou součástí systému Windows PowerShell Integrované skriptovací prostředí (ISE). Windows PowerShell ISE je součástí prostředí Windows PowerShell 3.0 a v prostředí Windows PowerShell 4.0. Klikněte na objekt tak, aby vás zavedou na referenční dokumentaci k nástroji pro třídu, která definuje objekt.

## <a name="psise-object"></a>objekt $psISE

**$PsISE** objekt je [kořenový objekt](The-ObjectModelRoot-Object.md) hierarchie objektů Windows PowerShell ISE.
Umístěný na nejvyšší úrovni, se zpřístupní následující objekty pro skriptování:

## <a name="psisecurrentfilethe-isefile-objectmd"></a>[$psISE.CurrentFile](The-ISEFile-Object.md)

**$PsISE.CurrentFile** objekt je instance [ISEFile](The-ISEFile-Object.md) třídy.

## <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a>[$psISE.CurrentPowerShellTab](The-PowerShellTab-Object.md)

**$PsISE.CurrentPowerShellTab** objekt je instance [PowerShellTab](The-PowerShellTab-Object.md) třídy.

## <a name="psisecurrentvisiblehorizontaltool"></a>$psISE.CurrentVisibleHorizontalTool

**$PsISE.CurrentVisibleHorizontalTool** objekt je instance [ISEAddOnTool](The-ISEAddOnTool-Object.md) třídy.
Reprezentuje nástroj nainstalovaný doplněk, který je aktuálně ukotven na horní okraj okna Windows PowerShell ISE.

## <a name="psisecurrentvisibleverticaltool"></a>$psISE.CurrentVisibleVerticalTool

**$PsISE.CurrentVisibleHorizontalTool** objekt je instance [ISEAddOnTool](The-ISEAddOnTool-Object.md) třídy.
Reprezentuje nástroj nainstalovaný doplněk, který je aktuálně ukotven pravé hrany okna Windows PowerShell ISE.

## <a name="psiseoptionsthe-iseoptions-objectmd"></a>[$psISE.Options](The-ISEOptions-Object.md)

**$PsISE.Options** objekt je instance [ISEOptions](The-ISEOptions-Object.md) třídy.
Objekt ISEOptions představuje různá nastavení pro Windows PowerShell ISE.
Je instance třídy Microsoft.PowerShell.Host.ISE.ISEOptions.

## <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a>[$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md)

**$PsISE.PowerShellTabs** objekt je instance [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) třídy.
Jedná se o kolekci všechny aktuálně otevřené prostředí PowerShell karet, které představují spustit prostředí v místním počítači nebo na vzdálených počítačích připojených k dispozici prostředí Windows PowerShell. Každý člen v kolekci je instance [PowerShellTab](The-PowerShellTab-Object.md) třídy.

## <a name="see-also"></a>Viz také
- [ISE Windows PowerShell skriptování objektový Model](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Odkaz na objekt modelu Windows PowerShell ISE](Windows-PowerShell-ISE-Object-Model-Reference.md)
