---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Změna stavu počítače
ms.assetid: 8093268b-27f8-4a49-8871-142c5cc33f01
ms.openlocfilehash: 3d3983c6d9e9b11db62bd71805da51be83331fdb
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="changing-computer-state"></a>Změna stavu počítače

Pokud chcete resetovat počítač v prostředí Windows PowerShell, použijte standardní nástroj příkazového řádku nebo třídu služby WMI. I když používáte prostředí Windows PowerShell pouze ke spuštění nástroje, naučit, jak změnit stav napájení počítače v prostředí Windows PowerShell ukazuje některé důležité podrobnosti o práci s externích nástrojů v prostředí Windows PowerShell.

### <a name="locking-a-computer"></a>Uzamčení počítače

Jediný způsob, jak uzamčení počítače přímo pomocí standardních nástrojů k dispozici je volání **LockWorkstation()** fungovat v **user32.dll**:

```
rundll32.exe user32.dll,LockWorkStation
```

Tento příkaz okamžitě uzamkne pracovní stanici. Používá *rundll32.exe*, který spouští knihovny DLL systému Windows (a uloží jejich knihovny pro opakované použití) ke spuštění user32.dll knihovnu funkce správy Windows.

Když zamknete pracovní stanice funkcí Rychlé přepínání uživatelů je povolen, program, jako je v systému Windows XP, počítač zobrazí na obrazovce přihlášení uživatele místo spuštění šetřič aktuálního uživatele.

Chcete-li vypnout konkrétní relace terminálového serveru, použijte **tsshutdn.exe** nástroj příkazového řádku.

### <a name="logging-off-the-current-session"></a>Odhlášení aktuální relaci

Můžete použít několik různých technik odhlášení relace v místním systému. Nejjednodušší způsob je pomocí nástroje příkazového řádku služby Vzdálená plocha a Terminálové **logoff.exe** (podrobnosti najdete v řádku prostředí Windows PowerShell zadejte **odhlášení nebo?**). Chcete-li odhlásit aktuální aktivní relace, zadejte **odhlášení** bez argumentů.

Můžete také **shutdown.exe** nástroj s jeho možnost odhlášení:

```
shutdown.exe -l
```

Třetí možnost je použít rozhraní WMI. Třídy Win32_OperatingSystem má metody Win32Shutdown metodu. Volání metody s příznakem 0 zahájí odhlášení:

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(0)
```

Další informace a k nalezení dalších funkcí Win32Shutdown obsahuje všechny metody najdete v části "Metody Win32Shutdown metoda the Win32_OperatingSystem třídy" na webu MSDN.

### <a name="shutting-down-or-restarting-a-computer"></a>Vypnutí nebo restartování počítače

Vypínání a restartování počítačů jsou obvykle stejné typy úloh. Nástroje, které vypnout počítač obecně restartuje ho také – a naopak. Existují dvě možnosti přehledné pro restartování počítače z prostředí Windows PowerShell. Pomocí příslušné argumenty Tsshutdn.exe nebo Shutdown.exe. Můžete získat podrobné informace o použití z **tsshutdn.exe /?** nebo **shutdown.exe /?**.

Můžete také provést vypnutí a restartování operace pomocí **Win32_OperatingSystem** přímo z prostředí Windows PowerShell také.

Chcete-li vypnout počítač, použijte metodu metody Win32Shutdown s **1** příznak.

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(1)
```

Chcete-li restartovat operační systém, použijte metodu metody Win32Shutdown s **2** příznak.

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(2)
```