---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Vlastní Windows PowerShell Desired State Configuration prostředky sestavení
ms.openlocfilehash: 882b6efed4564d2354183d7472b301e1e1758335
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403655"
---
# <a name="build-custom-windows-powershell-desired-state-configuration-resources"></a>Vlastní Windows PowerShell Desired State Configuration prostředky sestavení

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Windows PowerShell Desired State Configuration (DSC) má integrované prostředky, které můžete použít ke konfiguraci prostředí. Toto téma obsahuje základní informace o vývoji zdroje a odkazy na témata s konkrétní informace a příklady.

## <a name="dsc-resource-components"></a>Součásti prostředků DSC

Prostředek DSC je modul prostředí Windows PowerShell. Modul obsahuje schéma (definice konfigurovatelné vlastnosti) a implementace (kód, který ve skutečnosti zajišťuje zpracování určené konfigurace) pro prostředek. Schéma prostředků DSC lze definovat v souboru MOF a implementaci se provádí pomocí modulu skriptu. Počínaje podporu tříd Powershellu ve verzi 5, schéma a provádění oba určeny ve třídě. Následující témata popisují podrobně, jak vytvořit prostředky DSC.

* [Psaní vlastních prostředků DSC s MOF](authoringResourceMOF.md)
* [Implementace prostředek DSC vC#](authoringResourceMofCS.md)
* [Psaní vlastních prostředků DSC pomocí tříd Powershellu](authoringResourceClass.md)
* [Složené prostředky: Pomocí konfigurace DSC jako prostředek](authoringResourceComposite.md)
* [Pomocí nástroje Návrhář prostředků](../authoringResourceMofDesigner.md)
