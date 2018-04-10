---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
title: Poznámky k verzi WMF 5.1
ms.openlocfilehash: eb22267c1af28a9fcdd049c76d363fff687f6167
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="windows-management-framework-wmf-51-release-notes"></a>Poznámky k verzi Windows Management Framework (WMF) 5.1 #

WMF 5.1 zahrnuje komponenty prostředí PowerShell, rozhraní WMI, WinRM a protokolování inventáře softwaru (SIL), které byly zveřejněny v systému Windows Server 2016.
WMF 5.1 můžete instalovat na Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 a 2012 R2. Verze WMF 5.1 nabízí oproti WMF 5.0 RTM celou řadu vylepšení. Například:

- Nové rutiny pro místní uživatelé a skupiny, Get-ComputerInfo
- Vylepšení PowerShellGet zahrnuje vynucení podepsaných modulů a instalaci modulů JEA
- Přidaná podpora funkce PackageManagement pro kontejnery, nastavení CBS, nastavení založené na souboru EXE a balíčky CAB
- Vylepšené ladění pro třídy DSC a PowerShellu
- Vylepšené zabezpečení, včetně vynucení modulů podepsaných v katalogu, které pocházejí ze serveru vyžádané replikace při používání rutin PowerShellGet
- Odpovědi na celou řadu požadavků a problémů uživatelů

**Důležité poznámky:**

- **WMF 5.1 vyžaduje rozhraní .NET Framework 4.5.2** (nebo novější). Instalace proběhne úspěšně, ale jsou některé klíčové funkce se nezdaří, pokud rozhraní .NET 4.5.2 (nebo novější) není nainstalována. Pokyny jsou k dispozici v [instalace a konfigurace 5.1 WMF ](https://msdn.microsoft.com/powershell/wmf/5.1/install-configure) tématu.
- WMF 5.1 náhled je nutné odinstalovat před instalací WMF 5.1 RTM.
- WMF 5.1 může být nainstalovaná přímo přes WMF 5.0 nebo WMF 4.0.
- Je __nevyžaduje__ k instalaci WMF 4.0 před instalací WMF 5.1 v systému Windows 7 a Windows Server 2008 R2. Zda byl problém ve verzi WMF 5.1 Preview a byl vyřešen.