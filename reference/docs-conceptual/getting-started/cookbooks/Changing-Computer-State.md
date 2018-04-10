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
# <a name="changing-computer-state"></a><span data-ttu-id="1e4a0-103">Změna stavu počítače</span><span class="sxs-lookup"><span data-stu-id="1e4a0-103">Changing Computer State</span></span>

<span data-ttu-id="1e4a0-104">Pokud chcete resetovat počítač v prostředí Windows PowerShell, použijte standardní nástroj příkazového řádku nebo třídu služby WMI.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-104">To reset a computer in Windows PowerShell, use either a standard command-line tool or a WMI class.</span></span> <span data-ttu-id="1e4a0-105">I když používáte prostředí Windows PowerShell pouze ke spuštění nástroje, naučit, jak změnit stav napájení počítače v prostředí Windows PowerShell ukazuje některé důležité podrobnosti o práci s externích nástrojů v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-105">Although you are using Windows PowerShell only to run the tool, learning how to change a computer's power state in Windows PowerShell illustrates some of the important details about working with external tools in Windows PowerShell.</span></span>

### <a name="locking-a-computer"></a><span data-ttu-id="1e4a0-106">Uzamčení počítače</span><span class="sxs-lookup"><span data-stu-id="1e4a0-106">Locking a Computer</span></span>

<span data-ttu-id="1e4a0-107">Jediný způsob, jak uzamčení počítače přímo pomocí standardních nástrojů k dispozici je volání **LockWorkstation()** fungovat v **user32.dll**:</span><span class="sxs-lookup"><span data-stu-id="1e4a0-107">The only way to lock a computer directly with the standard available tools is to call the **LockWorkstation()** function in **user32.dll**:</span></span>

```
rundll32.exe user32.dll,LockWorkStation
```

<span data-ttu-id="1e4a0-108">Tento příkaz okamžitě uzamkne pracovní stanici.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-108">This command immediately locks the workstation.</span></span> <span data-ttu-id="1e4a0-109">Používá *rundll32.exe*, který spouští knihovny DLL systému Windows (a uloží jejich knihovny pro opakované použití) ke spuštění user32.dll knihovnu funkce správy Windows.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-109">It uses *rundll32.exe*, which runs Windows DLLs (and saves their libraries for repeated use) to run user32.dll, a library of Windows management functions.</span></span>

<span data-ttu-id="1e4a0-110">Když zamknete pracovní stanice funkcí Rychlé přepínání uživatelů je povolen, program, jako je v systému Windows XP, počítač zobrazí na obrazovce přihlášení uživatele místo spuštění šetřič aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-110">When you lock a workstation while Fast User Switching is enabled, such as on Windows XP, the computer displays the user logon screen rather than starting the current user's screensaver.</span></span>

<span data-ttu-id="1e4a0-111">Chcete-li vypnout konkrétní relace terminálového serveru, použijte **tsshutdn.exe** nástroj příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-111">To shut down particular sessions on a Terminal Server, use the **tsshutdn.exe** command-line tool.</span></span>

### <a name="logging-off-the-current-session"></a><span data-ttu-id="1e4a0-112">Odhlášení aktuální relaci</span><span class="sxs-lookup"><span data-stu-id="1e4a0-112">Logging Off the Current Session</span></span>

<span data-ttu-id="1e4a0-113">Můžete použít několik různých technik odhlášení relace v místním systému.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-113">You can use several different techniques to log off of a session on the local system.</span></span> <span data-ttu-id="1e4a0-114">Nejjednodušší způsob je pomocí nástroje příkazového řádku služby Vzdálená plocha a Terminálové **logoff.exe** (podrobnosti najdete v řádku prostředí Windows PowerShell zadejte **odhlášení nebo?**).</span><span class="sxs-lookup"><span data-stu-id="1e4a0-114">The simplest way is to use the Remote Desktop/Terminal Services command-line tool, **logoff.exe** (For details, at the Windows PowerShell prompt, type **logoff /?**).</span></span> <span data-ttu-id="1e4a0-115">Chcete-li odhlásit aktuální aktivní relace, zadejte **odhlášení** bez argumentů.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-115">To log off the current active session, type **logoff** with no arguments.</span></span>

<span data-ttu-id="1e4a0-116">Můžete také **shutdown.exe** nástroj s jeho možnost odhlášení:</span><span class="sxs-lookup"><span data-stu-id="1e4a0-116">You can also use the **shutdown.exe** tool with its logoff option:</span></span>

```
shutdown.exe -l
```

<span data-ttu-id="1e4a0-117">Třetí možnost je použít rozhraní WMI.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-117">A third option is to use WMI.</span></span> <span data-ttu-id="1e4a0-118">Třídy Win32_OperatingSystem má metody Win32Shutdown metodu.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-118">The Win32_OperatingSystem class has a Win32Shutdown method.</span></span> <span data-ttu-id="1e4a0-119">Volání metody s příznakem 0 zahájí odhlášení:</span><span class="sxs-lookup"><span data-stu-id="1e4a0-119">Invoking the method with the 0 flag initiates logoff:</span></span>

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(0)
```

<span data-ttu-id="1e4a0-120">Další informace a k nalezení dalších funkcí Win32Shutdown obsahuje všechny metody najdete v části "Metody Win32Shutdown metoda the Win32_OperatingSystem třídy" na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-120">For more information, and to find other features of the Win32Shutdown method, see "Win32Shutdown Method of the Win32_OperatingSystem Class" in MSDN.</span></span>

### <a name="shutting-down-or-restarting-a-computer"></a><span data-ttu-id="1e4a0-121">Vypnutí nebo restartování počítače</span><span class="sxs-lookup"><span data-stu-id="1e4a0-121">Shutting Down or Restarting a Computer</span></span>

<span data-ttu-id="1e4a0-122">Vypínání a restartování počítačů jsou obvykle stejné typy úloh.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-122">Shutting down and restarting computers are generally the same types of task.</span></span> <span data-ttu-id="1e4a0-123">Nástroje, které vypnout počítač obecně restartuje ho také – a naopak.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-123">Tools that shut down a computer will generally restart it as well—and vice versa.</span></span> <span data-ttu-id="1e4a0-124">Existují dvě možnosti přehledné pro restartování počítače z prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-124">There are two straightforward options for restarting a computer from Windows PowerShell.</span></span> <span data-ttu-id="1e4a0-125">Pomocí příslušné argumenty Tsshutdn.exe nebo Shutdown.exe.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-125">Use either Tsshutdn.exe or Shutdown.exe with appropriate arguments.</span></span> <span data-ttu-id="1e4a0-126">Můžete získat podrobné informace o použití z **tsshutdn.exe /?**</span><span class="sxs-lookup"><span data-stu-id="1e4a0-126">You can get detailed usage information from **tsshutdn.exe /?**</span></span> <span data-ttu-id="1e4a0-127">nebo **shutdown.exe /?**.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-127">or **shutdown.exe /?**.</span></span>

<span data-ttu-id="1e4a0-128">Můžete také provést vypnutí a restartování operace pomocí **Win32_OperatingSystem** přímo z prostředí Windows PowerShell také.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-128">You can also perform shutdown and restart operations by using **Win32_OperatingSystem** directly from Windows PowerShell as well.</span></span>

<span data-ttu-id="1e4a0-129">Chcete-li vypnout počítač, použijte metodu metody Win32Shutdown s **1** příznak.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-129">To shut down the computer, use the Win32Shutdown method with the **1** flag.</span></span>

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(1)
```

<span data-ttu-id="1e4a0-130">Chcete-li restartovat operační systém, použijte metodu metody Win32Shutdown s **2** příznak.</span><span class="sxs-lookup"><span data-stu-id="1e4a0-130">To restart the operating system, use the Win32Shutdown method with the **2** flag.</span></span>

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(2)
```