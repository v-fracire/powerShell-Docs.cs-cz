---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Sestavení vlastní Windows PowerShell Desired State Configuration prostředky
ms.openlocfilehash: f1ac626c5ef18b7ed14f3754ab39139db2a2a2d7
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="build-custom-windows-powershell-desired-state-configuration-resources"></a>Sestavení vlastní Windows PowerShell Desired State Configuration prostředky

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Požadovaného stavu aplikace Windows PowerShell (DSC) má integrovanou prostředky, které můžete použít ke konfiguraci prostředí. (Další informace najdete v tématu [předdefinované Windows PowerShell požadovaného stavu konfigurace prostředků](builtInResource.md).) Toto téma obsahuje přehled vývoje prostředky a odkazy na témata s konkrétní informace a příklady.

## <a name="dsc-resource-components"></a>Součásti prostředků DSC

Prostředek DSC je modul prostředí Windows PowerShell. Tento modul obsahuje schéma (definice konfigurovatelné vlastnosti) a implementace (kód, který ve skutečnosti zajišťuje zpracování zadané konfigurace) pro daný prostředek. Schéma prostředků DSC lze definovat v souboru MOF a implementaci se provádí pomocí modulu skriptu. Počínaje podpory prostředí PowerShell tříd v verze 5, schéma a implementace obě určeny v třídě. Následující témata popisují postup vytvoření prostředky DSC podrobněji.

* [Psaní vlastních prostředků DSC s MOF](authoringResourceMOF.md)
* [Implementace prostředek DSC v jazyce C#](authoringResourceMofCS.md)
* [Psaní vlastních prostředků DSC s třídami, prostředí PowerShell](authoringResourceClass.md)
* [Složené prostředky: použití konfigurace DSC jako prostředek](authoringResourceComposite.md)
* [V nástroji Návrhář prostředků](authoringResourceMofDesigner.md)