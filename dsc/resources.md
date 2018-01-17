---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředky DSC"
ms.openlocfilehash: 0994616673b5e447c69c09154bfdb9b9126a88c8
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-resources"></a><span data-ttu-id="f4a55-103">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="f4a55-103">DSC Resources</span></span>

><span data-ttu-id="f4a55-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f4a55-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="f4a55-105">Požadované prostředky konfigurace stavu (DSC) poskytují stavební bloky pro konfiguraci DSC.</span><span class="sxs-lookup"><span data-stu-id="f4a55-105">Desired State Configuration (DSC) Resources provide the building blocks for a DSC configuration.</span></span> <span data-ttu-id="f4a55-106">Prostředek zpřístupní vlastnosti, které může být nakonfigurované (schéma) a obsahuje funkce skriptu prostředí PowerShell, které místní Configuration Manager (LCM) žádostí na "jej tak".</span><span class="sxs-lookup"><span data-stu-id="f4a55-106">A resource exposes properties that can be configured (schema) and contains the PowerShell script functions that the Local Configuration Manager (LCM) calls to "make it so".</span></span>

<span data-ttu-id="f4a55-107">Prostředek může model něco jako obecný jako soubor nebo co nastavení serveru služby IIS.</span><span class="sxs-lookup"><span data-stu-id="f4a55-107">A resource can model something as generic as a file or as specific as an IIS server setting.</span></span>  <span data-ttu-id="f4a55-108">Skupiny jako prostředky společně na modul DSC, který slouží k uspořádání všechny požadované soubory v strukturu, která je přenosný a zahrnuje metadata k identifikaci, jak jsou prostředky určena k použití.</span><span class="sxs-lookup"><span data-stu-id="f4a55-108">Groups of like resources are combined in to a DSC Module, which organizes all the required files in to a structure that is portable and includes metadata to identify how the resources are intended to be used.</span></span>  

<span data-ttu-id="f4a55-109">Následující témata popisují prostředky DSC:</span><span class="sxs-lookup"><span data-stu-id="f4a55-109">The following topics describe DSC resources:</span></span>

- [<span data-ttu-id="f4a55-110">Předdefinované prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="f4a55-110">Built-In DSC resources</span></span>](builtInResource.md)
- [<span data-ttu-id="f4a55-111">Sestavení vlastní prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="f4a55-111">Build custom DSC resources</span></span>](authoringResource.md)
- [<span data-ttu-id="f4a55-112">Předdefinované prostředky DSC pro Linux</span><span class="sxs-lookup"><span data-stu-id="f4a55-112">Built-In DSC resources for Linux</span></span>](lnxBuiltInResources.md)

