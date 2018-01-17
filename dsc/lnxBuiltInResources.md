---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Předdefinované Desired State Configuration prostředky pro Linux"
ms.openlocfilehash: e268cb2ee8a246f18216b34e5e2a6d512f15e18c
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="built-in-desired-state-configuration-resources-for-linux"></a>Předdefinované Desired State Configuration prostředky pro Linux

Prostředky jsou stavební bloky, které můžete použít k zápisu skriptu prostředí PowerShell požadovaného stavu konfigurace (DSC). DSC pro Linux obsahuje sadu předdefinovaných funkcí pro konfiguraci prostředků, jako jsou soubory a složky, balíčky, proměnné prostředí a služby a procesy.

## <a name="built-in-resources"></a>Integrované prostředky 

Následující tabulka obsahuje seznam těchto prostředků a odkazy na témata, která je podrobně popisují.

* [nxArchive prostředků](lnxArchiveResource.md)– poskytuje mechanismus rozbalte souborech archivu (.tar, .zip) na konkrétní cesty.
* [nxEnvironment prostředků](lnxEnvironmentResource.md)– spravuje proměnné prostředí v cílové uzly. 
* [nxFile prostředků](lnxFileResource.md)– spravuje Linux souborů a adresářů. 
* [nxFileLine prostředků](lnxFileLineResource.md)– spravuje jednotlivých řádků v souboru Linux. 
* [nxGroup prostředků](lnxGroupResource.md)– spravuje místní skupiny Linux. 
* [nxPackage prostředků](lnxPackageResource.md)– spravuje balíčků na Linuxových uzlů.
* [nxScript prostředků](lnxScriptResource.md)– spustí skripty na cílové uzly.
* [nxService prostředků](lnxServiceResource.md)--služby spravuje Linuxu (démoni).
* [nxSshAuthorizedKeys prostředků](lnxSshAuthorizedKeysResource.md)– spravuje veřejné ssh klíče pro uživatele systému Linux. 
* [nxUser prostředků](lnxUserResource.md)– spravuje místní uživatelé Linux. 
  
