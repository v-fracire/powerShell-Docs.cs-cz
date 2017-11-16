---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředky DSC"
ms.openlocfilehash: 62bf352b929d661e585e145e5aab0f44f13010a1
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-resources"></a><span data-ttu-id="f5d13-103">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="f5d13-103">DSC Resources</span></span>

><span data-ttu-id="f5d13-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f5d13-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="f5d13-105">Požadované prostředky konfigurace stavu (DSC) poskytují stavební bloky pro konfiguraci DSC.</span><span class="sxs-lookup"><span data-stu-id="f5d13-105">Desired State Configuration (DSC) Resources provide the building blocks for a DSC configuration.</span></span> <span data-ttu-id="f5d13-106">Prostředek zpřístupní vlastnosti, které může být nakonfigurované (schéma) a obsahuje funkce skriptu prostředí PowerShell, které místní Configuration Manager (LCM) žádostí na "jej tak".</span><span class="sxs-lookup"><span data-stu-id="f5d13-106">A resource exposes properties that can be configured (schema) and contains the PowerShell script functions that the Local Configuration Manager (LCM) calls to "make it so".</span></span>

<span data-ttu-id="f5d13-107">Prostředek může model něco jako obecný jako soubor nebo co nastavení serveru služby IIS.</span><span class="sxs-lookup"><span data-stu-id="f5d13-107">A resource can model something as generic as a file or as specific as an IIS server setting.</span></span>  <span data-ttu-id="f5d13-108">Skupiny jako prostředky společně na modul DSC, který slouží k uspořádání všechny požadované soubory v strukturu, která je přenosný a zahrnuje metadata k identifikaci, jak jsou prostředky určena k použití.</span><span class="sxs-lookup"><span data-stu-id="f5d13-108">Groups of like resources are combined in to a DSC Module, which organizes all the required files in to a structure that is portable and includes metadata to identify how the resources are intended to be used.</span></span>  

<span data-ttu-id="f5d13-109">Následující témata popisují prostředky DSC:</span><span class="sxs-lookup"><span data-stu-id="f5d13-109">The following topics describe DSC resources:</span></span>

- [<span data-ttu-id="f5d13-110">Předdefinované prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="f5d13-110">Built-In DSC resources</span></span>](builtInResource.md)
- [<span data-ttu-id="f5d13-111">Sestavení vlastní prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="f5d13-111">Build custom DSC resources</span></span>](authoringResource.md)
- [<span data-ttu-id="f5d13-112">Předdefinované prostředky DSC pro Linux</span><span class="sxs-lookup"><span data-stu-id="f5d13-112">Built-In DSC resources for Linux</span></span>](lnxBuiltInResources.md)

