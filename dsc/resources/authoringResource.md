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
# <a name="build-custom-windows-powershell-desired-state-configuration-resources"></a><span data-ttu-id="e0fee-103">Vlastní Windows PowerShell Desired State Configuration prostředky sestavení</span><span class="sxs-lookup"><span data-stu-id="e0fee-103">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>

> <span data-ttu-id="e0fee-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e0fee-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="e0fee-105">Windows PowerShell Desired State Configuration (DSC) má integrované prostředky, které můžete použít ke konfiguraci prostředí.</span><span class="sxs-lookup"><span data-stu-id="e0fee-105">Windows PowerShell Desired State Configuration (DSC) has built-in resources that you can use to configure your environment.</span></span> <span data-ttu-id="e0fee-106">Toto téma obsahuje základní informace o vývoji zdroje a odkazy na témata s konkrétní informace a příklady.</span><span class="sxs-lookup"><span data-stu-id="e0fee-106">This topic provides an overview of developing resources and links to topics with specific information and examples.</span></span>

## <a name="dsc-resource-components"></a><span data-ttu-id="e0fee-107">Součásti prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="e0fee-107">DSC resource components</span></span>

<span data-ttu-id="e0fee-108">Prostředek DSC je modul prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0fee-108">A DSC resource is a Windows PowerShell module.</span></span> <span data-ttu-id="e0fee-109">Modul obsahuje schéma (definice konfigurovatelné vlastnosti) a implementace (kód, který ve skutečnosti zajišťuje zpracování určené konfigurace) pro prostředek.</span><span class="sxs-lookup"><span data-stu-id="e0fee-109">The module contains both the schema (the definition of the configurable properties) and the implementation (the code that does the actual work specified by a configuration) for the resource.</span></span> <span data-ttu-id="e0fee-110">Schéma prostředků DSC lze definovat v souboru MOF a implementaci se provádí pomocí modulu skriptu.</span><span class="sxs-lookup"><span data-stu-id="e0fee-110">A DSC resource schema can be defined in a MOF file, and the implementation is performed by a script module.</span></span> <span data-ttu-id="e0fee-111">Počínaje podporu tříd Powershellu ve verzi 5, schéma a provádění oba určeny ve třídě.</span><span class="sxs-lookup"><span data-stu-id="e0fee-111">Beginning with the support of PowerShell classes in version 5, the schema and implementation can both be defined in a class.</span></span> <span data-ttu-id="e0fee-112">Následující témata popisují podrobně, jak vytvořit prostředky DSC.</span><span class="sxs-lookup"><span data-stu-id="e0fee-112">The following topics describe in more detail how to create DSC resources.</span></span>

* [<span data-ttu-id="e0fee-113">Psaní vlastních prostředků DSC s MOF</span><span class="sxs-lookup"><span data-stu-id="e0fee-113">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
* [<span data-ttu-id="e0fee-114">Implementace prostředek DSC vC#</span><span class="sxs-lookup"><span data-stu-id="e0fee-114">Implementing a DSC resource in C#</span></span>](authoringResourceMofCS.md)
* [<span data-ttu-id="e0fee-115">Psaní vlastních prostředků DSC pomocí tříd Powershellu</span><span class="sxs-lookup"><span data-stu-id="e0fee-115">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)
* [<span data-ttu-id="e0fee-116">Složené prostředky: Pomocí konfigurace DSC jako prostředek</span><span class="sxs-lookup"><span data-stu-id="e0fee-116">Composite resources: Using a DSC configuration as a resource</span></span>](authoringResourceComposite.md)
* [<span data-ttu-id="e0fee-117">Pomocí nástroje Návrhář prostředků</span><span class="sxs-lookup"><span data-stu-id="e0fee-117">Using the Resource Designer tool</span></span>](../authoringResourceMofDesigner.md)
