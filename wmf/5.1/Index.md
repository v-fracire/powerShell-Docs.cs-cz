---
ms.date: 2017-08-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
title: "Poznámky k verzi WMF 5.1"
ms.openlocfilehash: 3a6b7fb84d679d9bbe7a89e30c8c769e26f7381a
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2017
---
# <a name="windows-management-framework-wmf-51"></a>Windows Management Framework (WMF) 5.1 #

WMF umožňuje uživatelům aktualizovat ve stávajících systémech Windows verze komponent PowerShell, WMI, WinRM a Protokolování softwarového inventáře (SIL), které byly vydané ve Windows Serveru 2016. 

WMF 5.1 můžete instalovat na Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 a 2012 R2. Verze WMF 5.1 nabízí oproti WMF 5.0 RTM celou řadu vylepšení. Například:

- Nové rutiny pro místní uživatelé a skupiny, Get-ComputerInfo
- Vylepšení PowerShellGet zahrnuje vynucení podepsaných modulů a instalaci modulů JEA
- Přidaná podpora funkce PackageManagement pro kontejnery, nastavení CBS, nastavení založené na souboru EXE a balíčky CAB
- Vylepšené ladění pro třídy DSC a PowerShellu
- Vylepšené zabezpečení, včetně vynucení modulů podepsaných v katalogu, které pocházejí ze serveru vyžádané replikace při používání rutin PowerShellGet
- Odpovědi na celou řadu požadavků a problémů uživatelů

Další informace o novinkách této verze najdete v tématech, kterými se zabývá článek [Nové scénáře a funkce](https://docs.microsoft.com/en-us/powershell/wmf/5.1/scenarios-features). 

V tématu [Instalace a konfigurace](https://docs.microsoft.com/en-us/powershell/wmf/5.1/install-configure) je seznam požadavků a pokyny k instalaci WMF. 

V tématu [Kompatibilita](https://docs.microsoft.com/en-us/powershell/wmf/5.1/compatibility) je seznam verzí WMF, které je možné nainstalovat do určité verze Windows. 

Téma [Kompatibilita produktu](https://docs.microsoft.com/en-us/powershell/wmf/5.1/productincompat) obsahuje seznam aplikací Microsoftu, které v této chvíli neschválily používání WMF 5.1. 

Podrobnosti o komponentách WMF najdete v dokumentaci MSDN:

- [PowerShell 5.1](https://docs.microsoft.com/en-us/powershell/) 
- [WMI](https://msdn.microsoft.com/en-us/library/jj152383(v=vs.85).aspx)
- [WinRM](https://msdn.microsoft.com/en-us/library/aa384426(v=vs.85).aspx)
- [Protokolování inventáře softwaru](https://technet.microsoft.com/en-us/library/dn383584(v=ws.11).aspx)

