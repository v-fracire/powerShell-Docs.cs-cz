---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Předdefinované Desired State Configuration prostředky pro Linux
ms.openlocfilehash: 77617b72584f39c46fc4b9eb67235378bbfc19aa
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="built-in-desired-state-configuration-resources-for-linux"></a><span data-ttu-id="f8c89-103">Předdefinované Desired State Configuration prostředky pro Linux</span><span class="sxs-lookup"><span data-stu-id="f8c89-103">Built-In Desired State Configuration Resources for Linux</span></span>

<span data-ttu-id="f8c89-104">Prostředky jsou stavební bloky, které můžete použít k zápisu skriptu prostředí PowerShell požadovaného stavu konfigurace (DSC).</span><span class="sxs-lookup"><span data-stu-id="f8c89-104">Resources are building blocks that you can use to write a PowerShell Desired State Configuration (DSC) script.</span></span> <span data-ttu-id="f8c89-105">DSC pro Linux obsahuje sadu předdefinovaných funkcí pro konfiguraci prostředků, jako jsou soubory a složky, balíčky, proměnné prostředí a služby a procesy.</span><span class="sxs-lookup"><span data-stu-id="f8c89-105">DSC for Linux comes with a set of built-in functionality for configuring resources such as files and folders, packages, environment variables, and services and processes.</span></span>

## <a name="built-in-resources"></a><span data-ttu-id="f8c89-106">Integrované prostředky</span><span class="sxs-lookup"><span data-stu-id="f8c89-106">Built-in resources</span></span>

<span data-ttu-id="f8c89-107">Následující tabulka obsahuje seznam těchto prostředků a odkazy na témata, která je podrobně popisují.</span><span class="sxs-lookup"><span data-stu-id="f8c89-107">The following table provides a list of these resources and links to topics that describe them in detail.</span></span>

* <span data-ttu-id="f8c89-108">[nxArchive prostředků](lnxArchiveResource.md)– poskytuje mechanismus rozbalte souborech archivu (.tar, .zip) na konkrétní cesty.</span><span class="sxs-lookup"><span data-stu-id="f8c89-108">[nxArchive Resource](lnxArchiveResource.md)--Provides a mechanism to unpack archive (.tar, .zip) files at a specific path.</span></span>
* <span data-ttu-id="f8c89-109">[nxEnvironment prostředků](lnxEnvironmentResource.md)– spravuje proměnné prostředí v cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="f8c89-109">[nxEnvironment Resource](lnxEnvironmentResource.md)--Manages environment variables on target nodes.</span></span>
* <span data-ttu-id="f8c89-110">[nxFile prostředků](lnxFileResource.md)– spravuje Linux souborů a adresářů.</span><span class="sxs-lookup"><span data-stu-id="f8c89-110">[nxFile Resource](lnxFileResource.md)--Manages Linux files and directories.</span></span>
* <span data-ttu-id="f8c89-111">[nxFileLine prostředků](lnxFileLineResource.md)– spravuje jednotlivých řádků v souboru Linux.</span><span class="sxs-lookup"><span data-stu-id="f8c89-111">[nxFileLine Resource](lnxFileLineResource.md)--Manages individual lines in a Linux file.</span></span>
* <span data-ttu-id="f8c89-112">[nxGroup prostředků](lnxGroupResource.md)– spravuje místní skupiny Linux.</span><span class="sxs-lookup"><span data-stu-id="f8c89-112">[nxGroup Resource](lnxGroupResource.md)--Manages local Linux groups.</span></span>
* <span data-ttu-id="f8c89-113">[nxPackage prostředků](lnxPackageResource.md)– spravuje balíčků na Linuxových uzlů.</span><span class="sxs-lookup"><span data-stu-id="f8c89-113">[nxPackage Resource](lnxPackageResource.md)--Manages packages on Linux nodes.</span></span>
* <span data-ttu-id="f8c89-114">[nxScript prostředků](lnxScriptResource.md)– spustí skripty na cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="f8c89-114">[nxScript Resource](lnxScriptResource.md)--Runs scripts on target nodes.</span></span>
* <span data-ttu-id="f8c89-115">[nxService prostředků](lnxServiceResource.md)--služby spravuje Linuxu (démoni).</span><span class="sxs-lookup"><span data-stu-id="f8c89-115">[nxService Resource](lnxServiceResource.md)--Manages Linux services (daemons).</span></span>
* <span data-ttu-id="f8c89-116">[nxSshAuthorizedKeys prostředků](lnxSshAuthorizedKeysResource.md)– spravuje veřejné ssh klíče pro uživatele systému Linux.</span><span class="sxs-lookup"><span data-stu-id="f8c89-116">[nxSshAuthorizedKeys Resource](lnxSshAuthorizedKeysResource.md)--Manages public ssh keys for a Linux user.</span></span>
* <span data-ttu-id="f8c89-117">[nxUser prostředků](lnxUserResource.md)– spravuje místní uživatelé Linux.</span><span class="sxs-lookup"><span data-stu-id="f8c89-117">[nxUser Resource](lnxUserResource.md)--Manages local Linux users.</span></span>