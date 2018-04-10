---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 7eaa4dfb68bc299ad31bce81af96b6a760c4fcc5
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="creating-custom-types-using-powershell-classes"></a>Vytváření vlastních typů pomocí tříd PowerShellu

Vylepšili jsme prostředí PowerShell jazyk pro definování třídami a ostatními typy uživatelem definované pomocí syntaxe formální a sémantikou, které jsou podobné jinými objektově orientované programovací jazyky. Cílem je umožnit vývojářům a odborníkům zapojení prostředí PowerShell pro širší škálu případy použití, vývoj artefaktů prostředí PowerShell (jako jsou prostředky DSC) zjednodušit a urychlit pokrytí Správa ploch.

## <a name="supported-scenarios-in-this-release"></a>Podporované scénáře v této verzi

-   Definice prostředků DSC a jejich přidružené typy pomocí prostředí PowerShell jazyka
-   Definování vlastních typů v prostředí PowerShell pomocí známých objektově orientované programovací konstrukce, jako jsou třídy, vlastnosti, metody atd.
-   Podpora dědičnosti s třídou v prostředí PowerShell a třída základní prostředek DSC
-   Ladění typy pomocí prostředí PowerShell jazyka
-   Generování a zpracování výjimek pomocí formální mechanismů a na pravém úrovni