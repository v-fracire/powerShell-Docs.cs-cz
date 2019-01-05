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
# <a name="built-in-desired-state-configuration-resources-for-linux"></a>Integrované prostředky Desired State Configuration pro Linux

Prostředky jsou stavební bloky, které můžete napsat skript prostředí PowerShell Desired State Configuration (DSC). DSC pro Linux se dodává se sadou integrované funkce pro konfiguraci prostředků, jako jsou soubory a složky, balíčky, proměnné prostředí a služeb a procesů.

## <a name="built-in-resources"></a>Integrované prostředky

Následující tabulka obsahuje seznam těchto prostředků a odkazy na témata, které podrobně popisují.

* [prostředek nxArchive](lnxArchiveResource.md)– poskytuje mechanismus k rozbalení archivu (.tar, .zip) soubory do konkrétní cesty.
* [prostředek nxEnvironment](lnxEnvironmentResource.md)– spravuje proměnných prostředí na cílové uzly.
* [prostředek nxFile](lnxFileResource.md)– Linux spravuje soubory a adresáře.
* [prostředek nxFileLine](lnxFileLineResource.md)– spravuje jednotlivých řádků v souboru systému Linux.
* [prostředek nxGroup](lnxGroupResource.md)– spravuje místní skupiny systému Linux.
* [prostředek nxPackage](lnxPackageResource.md)– spravuje balíčků na uzly s Linuxem.
* [nxScript prostředků](lnxScriptResource.md)– spustí skripty na cílové uzly.
* [prostředek nxService](lnxServiceResource.md)– služby spravuje Linuxu (procesy démon).
* [prostředek nxSshAuthorizedKeys](lnxSshAuthorizedKeysResource.md)– spravuje veřejného ssh klíče pro uživatele systému Linux.
* [prostředek nxUser](lnxUserResource.md)– slouží ke správě místních uživatelů Linuxu.