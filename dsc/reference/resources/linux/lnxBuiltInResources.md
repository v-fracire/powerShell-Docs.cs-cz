---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Integrované prostředky Desired State Configuration pro Linux
ms.openlocfilehash: ea700d24c7ff4377af671944184abb3f201852e8
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048156"
---
# <a name="built-in-desired-state-configuration-resources-for-linux"></a><span data-ttu-id="7a6dd-103">Integrované prostředky Desired State Configuration pro Linux</span><span class="sxs-lookup"><span data-stu-id="7a6dd-103">Built-In Desired State Configuration Resources for Linux</span></span>

<span data-ttu-id="7a6dd-104">Prostředky jsou stavební bloky, které můžete napsat skript prostředí PowerShell Desired State Configuration (DSC).</span><span class="sxs-lookup"><span data-stu-id="7a6dd-104">Resources are building blocks that you can use to write a PowerShell Desired State Configuration (DSC) script.</span></span> <span data-ttu-id="7a6dd-105">DSC pro Linux se dodává se sadou integrované funkce pro konfiguraci prostředků, jako jsou soubory a složky, balíčky, proměnné prostředí a služeb a procesů.</span><span class="sxs-lookup"><span data-stu-id="7a6dd-105">DSC for Linux comes with a set of built-in functionality for configuring resources such as files and folders, packages, environment variables, and services and processes.</span></span>

## <a name="built-in-resources"></a><span data-ttu-id="7a6dd-106">Integrované prostředky</span><span class="sxs-lookup"><span data-stu-id="7a6dd-106">Built-in resources</span></span>

<span data-ttu-id="7a6dd-107">Následující tabulka obsahuje seznam těchto prostředků a odkazy na témata, které podrobně popisují.</span><span class="sxs-lookup"><span data-stu-id="7a6dd-107">The following table provides a list of these resources and links to topics that describe them in detail.</span></span>

* <span data-ttu-id="7a6dd-108">[prostředek nxArchive](lnxArchiveResource.md)– poskytuje mechanismus k rozbalení archivu (.tar, .zip) soubory do konkrétní cesty.</span><span class="sxs-lookup"><span data-stu-id="7a6dd-108">[nxArchive Resource](lnxArchiveResource.md)--Provides a mechanism to unpack archive (.tar, .zip) files at a specific path.</span></span>
* <span data-ttu-id="7a6dd-109">[prostředek nxEnvironment](lnxEnvironmentResource.md)– spravuje proměnných prostředí na cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="7a6dd-109">[nxEnvironment Resource](lnxEnvironmentResource.md)--Manages environment variables on target nodes.</span></span>
* <span data-ttu-id="7a6dd-110">[prostředek nxFile](lnxFileResource.md)– Linux spravuje soubory a adresáře.</span><span class="sxs-lookup"><span data-stu-id="7a6dd-110">[nxFile Resource](lnxFileResource.md)--Manages Linux files and directories.</span></span>
* <span data-ttu-id="7a6dd-111">[prostředek nxFileLine](lnxFileLineResource.md)– spravuje jednotlivých řádků v souboru systému Linux.</span><span class="sxs-lookup"><span data-stu-id="7a6dd-111">[nxFileLine Resource](lnxFileLineResource.md)--Manages individual lines in a Linux file.</span></span>
* <span data-ttu-id="7a6dd-112">[prostředek nxGroup](lnxGroupResource.md)– spravuje místní skupiny systému Linux.</span><span class="sxs-lookup"><span data-stu-id="7a6dd-112">[nxGroup Resource](lnxGroupResource.md)--Manages local Linux groups.</span></span>
* <span data-ttu-id="7a6dd-113">[prostředek nxPackage](lnxPackageResource.md)– spravuje balíčků na uzly s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="7a6dd-113">[nxPackage Resource](lnxPackageResource.md)--Manages packages on Linux nodes.</span></span>
* <span data-ttu-id="7a6dd-114">[nxScript prostředků](lnxScriptResource.md)– spustí skripty na cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="7a6dd-114">[nxScript Resource](lnxScriptResource.md)--Runs scripts on target nodes.</span></span>
* <span data-ttu-id="7a6dd-115">[prostředek nxService](lnxServiceResource.md)– služby spravuje Linuxu (procesy démon).</span><span class="sxs-lookup"><span data-stu-id="7a6dd-115">[nxService Resource](lnxServiceResource.md)--Manages Linux services (daemons).</span></span>
* <span data-ttu-id="7a6dd-116">[prostředek nxSshAuthorizedKeys](lnxSshAuthorizedKeysResource.md)– spravuje veřejného ssh klíče pro uživatele systému Linux.</span><span class="sxs-lookup"><span data-stu-id="7a6dd-116">[nxSshAuthorizedKeys Resource](lnxSshAuthorizedKeysResource.md)--Manages public ssh keys for a Linux user.</span></span>
* <span data-ttu-id="7a6dd-117">[prostředek nxUser](lnxUserResource.md)– slouží ke správě místních uživatelů Linuxu.</span><span class="sxs-lookup"><span data-stu-id="7a6dd-117">[nxUser Resource](lnxUserResource.md)--Manages local Linux users.</span></span>