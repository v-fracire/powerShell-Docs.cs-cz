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
# <a name="creating-custom-types-using-powershell-classes"></a><span data-ttu-id="6dcd4-102">Vytváření vlastních typů pomocí tříd PowerShellu</span><span class="sxs-lookup"><span data-stu-id="6dcd4-102">Creating Custom Types using PowerShell Classes</span></span>

<span data-ttu-id="6dcd4-103">Vylepšili jsme prostředí PowerShell jazyk pro definování třídami a ostatními typy uživatelem definované pomocí syntaxe formální a sémantikou, které jsou podobné jinými objektově orientované programovací jazyky.</span><span class="sxs-lookup"><span data-stu-id="6dcd4-103">We’ve improved the PowerShell language for defining classes and other user-defined types by using formal syntax and semantics that are similar to other object-oriented programming languages.</span></span> <span data-ttu-id="6dcd4-104">Cílem je umožnit vývojářům a odborníkům zapojení prostředí PowerShell pro širší škálu případy použití, vývoj artefaktů prostředí PowerShell (jako jsou prostředky DSC) zjednodušit a urychlit pokrytí Správa ploch.</span><span class="sxs-lookup"><span data-stu-id="6dcd4-104">The goal is to enable developers and IT professionals to embrace PowerShell for a wider range of use cases, simplify development of PowerShell artifacts (such as DSC resources), and accelerate coverage of management surfaces.</span></span>

## <a name="supported-scenarios-in-this-release"></a><span data-ttu-id="6dcd4-105">Podporované scénáře v této verzi</span><span class="sxs-lookup"><span data-stu-id="6dcd4-105">Supported scenarios in this release</span></span>

-   <span data-ttu-id="6dcd4-106">Definice prostředků DSC a jejich přidružené typy pomocí prostředí PowerShell jazyka</span><span class="sxs-lookup"><span data-stu-id="6dcd4-106">Define DSC resources and their associated types by using the PowerShell language</span></span>
-   <span data-ttu-id="6dcd4-107">Definování vlastních typů v prostředí PowerShell pomocí známých objektově orientované programovací konstrukce, jako jsou třídy, vlastnosti, metody atd.</span><span class="sxs-lookup"><span data-stu-id="6dcd4-107">Define custom types in PowerShell by using familiar object-oriented programming constructs, such as classes, properties, methods, etc.</span></span>
-   <span data-ttu-id="6dcd4-108">Podpora dědičnosti s třídou v prostředí PowerShell a třída základní prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="6dcd4-108">Inheritance support with class in PowerShell and class base DSC resource</span></span>
-   <span data-ttu-id="6dcd4-109">Ladění typy pomocí prostředí PowerShell jazyka</span><span class="sxs-lookup"><span data-stu-id="6dcd4-109">Debug types by using the PowerShell language</span></span>
-   <span data-ttu-id="6dcd4-110">Generování a zpracování výjimek pomocí formální mechanismů a na pravém úrovni</span><span class="sxs-lookup"><span data-stu-id="6dcd4-110">Generate and handle exceptions by using formal mechanisms, and at the right level</span></span>