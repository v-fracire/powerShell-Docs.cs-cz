---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Sestavení vlastní Windows PowerShell Desired State Configuration prostředky"
ms.openlocfilehash: 75b494db4ee6e381491decb11d35b60105217a0f
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
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

