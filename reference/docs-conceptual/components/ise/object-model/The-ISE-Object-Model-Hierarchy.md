---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Hierarchie objektového modelu prostředí ISE
ms.openlocfilehash: 0159707b1050c412a74da3d3ca02a46cea982556
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403869"
---
# <a name="the-ise-object-model-hierarchy"></a>Hierarchie objektového modelu prostředí ISE

Toto téma ukazuje hierarchii objektů, které jsou součástí sady Windows Powershellu integrovaném skriptovacím prostředí (ISE).
Windows PowerShell ISE je součástí Windows PowerShell 3.0 a ve Windows Powershellu 4.0.
Klikněte na objekt, které vás přesměrují na referenční dokumentaci pro třídy, která definuje objekt.

## <a name="psise-object"></a>objekt $psISE

**$PsISE** je objekt [kořenový objekt](The-ObjectModelRoot-Object.md) hierarchie objektů prostředí PowerShell ISE Windows.
Umístěné na nejvyšší úrovni, díky němu následující objekty dostupné pro skriptování:

## <a name="psisecurrentfilethe-isefile-objectmd"></a>[$psISE.CurrentFile](The-ISEFile-Object.md)

**$PsISE.CurrentFile** objekt je instancí [ISEFile](The-ISEFile-Object.md) třídy.

## <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a>[$psISE.CurrentPowerShellTab](The-PowerShellTab-Object.md)

**$PsISE.CurrentPowerShellTab** objekt je instancí [PowerShellTab](The-PowerShellTab-Object.md) třídy.

## <a name="psisecurrentvisiblehorizontaltool"></a>$psISE.CurrentVisibleHorizontalTool

**$PsISE.CurrentVisibleHorizontalTool** objekt je instancí [ISEAddOnTool](The-ISEAddOnTool-Object.md) třídy.
Představuje nástroj nainstalovaný doplněk, který je aktuálně ukotven na horním okraji okna Windows PowerShell ISE.

## <a name="psisecurrentvisibleverticaltool"></a>$psISE.CurrentVisibleVerticalTool

**$PsISE.CurrentVisibleHorizontalTool** objekt je instancí [ISEAddOnTool](The-ISEAddOnTool-Object.md) třídy.
Představuje nástroj nainstalovaný doplněk, který je aktuálně ukotven na pravém okraji okna Windows PowerShell ISE.

## <a name="psiseoptionsthe-iseoptions-objectmd"></a>[$psISE.Options](The-ISEOptions-Object.md)

**$PsISE.Options** objekt je instancí [ISEOptions](The-ISEOptions-Object.md) třídy.
Objekt ISEOptions představuje různá nastavení pro Windows PowerShell ISE.
Je instancí třídy Microsoft.PowerShell.Host.ISE.ISEOptions.

## <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a>[$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md)

**$PsISE.PowerShellTabs** objekt je instancí [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) třídy.
Jde o kolekci všechny aktuálně otevřené Powershellu karty, které představují k dispozici Windows Powershellu spusťte prostředí v místním počítači nebo na připojených vzdálených počítačích.
Každý člen v kolekci je instance [PowerShellTab](The-PowerShellTab-Object.md) třídy.

## <a name="see-also"></a>Viz také

- [Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)