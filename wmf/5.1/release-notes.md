---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
title: "Poznámky k verzi WMF 5.1"
ms.openlocfilehash: ce9bc7791facfcc2cce9468689e88a26154bda7d
ms.sourcegitcommit: 3f49bd2e0b786e69c71393c00ad85d05a8466753
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/04/2017
---
# <a name="windows-management-framework-wmf-51-release-notes"></a>Poznámky k verzi Windows Management Framework (WMF) 5.1 #

WMF 5.1 zahrnuje komponenty prostředí PowerShell, rozhraní WMI, WinRM a protokolování inventáře softwaru (SIL), které byly zveřejněny v systému Windows Server 2016.
WMF 5.1 se dá nainstalovat na Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 a 2012 R2 a nabízí několik vylepšení v porovnání s WMF 5.0 RTM, včetně:

- Nové rutiny: místní uživatelé a skupiny; Get-ComputerInfo
- PowerShellGet vylepšení patří vynucování podepsané moduly a instalace JEA moduly
- PackageManagement přidaná podpora pro instalační program na základě EXE kontejnery, CBS instalace, soubor CAB balíčky
- Ladění vylepšení pro třídy DSC a prostředí PowerShell
- Vylepšení zabezpečení, včetně vynucení katalogu podepsané moduly přichází ze serveru vyžádaných replikací a při použití rutiny PowerShellGet
- Odpovědi na počet uživatelských požadavků a problémů

**Důležité poznámky:**

- **WMF 5.1 vyžaduje rozhraní .NET Framework 4.5.2** (nebo novější). Instalace proběhne úspěšně, ale jsou některé klíčové funkce se nezdaří, pokud rozhraní .NET 4.5.2 (nebo novější) není nainstalována. Pokyny jsou k dispozici v [instalace a konfigurace 5.1 WMF ](https://msdn.microsoft.com/en-us/powershell/wmf/5.1/install-configure) tématu.
- WMF 5.1 náhled je nutné odinstalovat před instalací WMF 5.1 RTM.
- WMF 5.1 může být nainstalovaná přímo přes WMF 5.0 nebo WMF 4.0.
- Je __nevyžaduje__ k instalaci WMF 4.0 před instalací WMF 5.1 v systému Windows 7 a Windows Server 2008 R2. Zda byl problém ve verzi WMF 5.1 Preview a byl vyřešen.  


