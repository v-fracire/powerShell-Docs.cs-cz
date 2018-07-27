---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Změna stavu počítače
ms.assetid: 8093268b-27f8-4a49-8871-142c5cc33f01
ms.openlocfilehash: 4b5b4adb349dd8036117c364ed2ebb1ffaf8c88f
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39267881"
---
# <a name="changing-computer-state"></a>Změna stavu počítače

Pokud chcete resetovat počítače v prostředí Windows PowerShell, použijte standardní nástroj příkazového řádku nebo třída služby WMI. I když používáte jenom ke spuštění nástroje Windows Powershellu, naučit, jak se změna stavu napájení počítače v prostředí Windows PowerShell ukazuje některé důležité podrobnosti o práci s externí nástroje v prostředí Windows PowerShell.

### <a name="locking-a-computer"></a>Uzamčení počítače

Je jediný způsob, jak uzamknout počítače přímo pomocí standardních nástrojů k dispozici k volání **LockWorkstation()** fungovat v **user32.dll**:

```
rundll32.exe user32.dll,LockWorkStation
```

Tento příkaz okamžitě zamkne pracovní stanici. Používá *rundll32.exe*, které běží Windows knihovny DLL (a uloží jejich knihovny pro opakované použití) ke spuštění user32.dll, knihovnu funkce správy Windows.

Když Uzamknout pracovní stanice rychlé přepínání uživatelů je povolen, jako je Windows XP, počítač zobrazí přihlašovací obrazovka uživatele spíše než počáteční spořič obrazovky aktuálního uživatele.

Chcete-li vypnout konkrétní relace terminálového serveru, použijte **tsshutdn.exe** nástroj příkazového řádku.

### <a name="logging-off-the-current-session"></a>Odhlášení se od aktuální relace

Odhlášení relace v místním systému můžete použít několik různých technik. Nejjednodušší způsob je pomocí nástroje příkazového řádku vzdálené plochy/Terminálové služby **logoff.exe** (podrobnosti najdete v příkazovém řádku Windows Powershellu, zadejte **odhlášení /?**). Chcete-li odhlásit aktuální aktivní relace, zadejte **odhlášení** bez argumentů.

Můžete také použít **shutdown.exe** nástroje s možností jeho odhlášení:

```
shutdown.exe -l
```

Třetí možností je použít rozhraní WMI. Třídy Win32_OperatingSystem má metody Win32Shutdown metodu. Vyvolání metody s 0 příznak zahájí odhlášení:

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(0)
```

Další informace a najít další funkce Win32Shutdown obsahuje všechny metody naleznete v tématu "Metody Win32Shutdown metoda z Win32_OperatingSystem třída" na webu MSDN.

### <a name="shutting-down-or-restarting-a-computer"></a>Vypnutí nebo restartování počítače

Vypnutí a restartování počítačů jsou obvykle stejné typy úloh. Nástroje, které vypnout počítač obecně restartuje ho také – a naopak. Existují dvě jednoduché možnosti pro restartování počítače z prostředí Windows PowerShell. Použijte Tsshutdn.exe nebo Shutdown.exe s příslušnými argumenty. Můžete získat podrobné informace o použití z **tsshutdn.exe /?** nebo **shutdown.exe /?**.

Můžete také provést vypnutí a restartování operace přímo z prostředí Windows PowerShell a.

Vypnutí počítače, použijte příkaz stop-computer

```powershell
stop-computer
```

Chcete-li restartovat operační systém, použijte příkaz restart-computer

```powershell
restart-computer
```
