---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Hierarchie objektového modelu prostředí ISE
ms.openlocfilehash: 0159707b1050c412a74da3d3ca02a46cea982556
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30950688"
---
# <a name="the-ise-object-model-hierarchy"></a>Hierarchie objektového modelu prostředí ISE

Toto téma ukazuje hierarchii objektů, které jsou součástí systému Windows PowerShell Integrované skriptovací prostředí (ISE).
Windows PowerShell ISE je součástí prostředí Windows PowerShell 3.0 a v prostředí Windows PowerShell 4.0.
Klikněte na objekt tak, aby vás zavedou na referenční dokumentaci k nástroji pro třídu, která definuje objekt.

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
Jedná se o kolekci všechny aktuálně otevřené prostředí PowerShell karet, které představují spustit prostředí v místním počítači nebo na vzdálených počítačích připojených k dispozici prostředí Windows PowerShell.
Každý člen v kolekci je instance [PowerShellTab](The-PowerShellTab-Object.md) třídy.

## <a name="see-also"></a>Viz také

- [Účelem ISE Windows PowerShell skriptování objektový Model](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)