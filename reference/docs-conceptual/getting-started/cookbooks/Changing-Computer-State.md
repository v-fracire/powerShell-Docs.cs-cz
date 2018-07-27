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
# <a name="changing-computer-state"></a><span data-ttu-id="94574-103">Změna stavu počítače</span><span class="sxs-lookup"><span data-stu-id="94574-103">Changing Computer State</span></span>

<span data-ttu-id="94574-104">Pokud chcete resetovat počítače v prostředí Windows PowerShell, použijte standardní nástroj příkazového řádku nebo třída služby WMI.</span><span class="sxs-lookup"><span data-stu-id="94574-104">To reset a computer in Windows PowerShell, use either a standard command-line tool or a WMI class.</span></span> <span data-ttu-id="94574-105">I když používáte jenom ke spuštění nástroje Windows Powershellu, naučit, jak se změna stavu napájení počítače v prostředí Windows PowerShell ukazuje některé důležité podrobnosti o práci s externí nástroje v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94574-105">Although you are using Windows PowerShell only to run the tool, learning how to change a computer's power state in Windows PowerShell illustrates some of the important details about working with external tools in Windows PowerShell.</span></span>

### <a name="locking-a-computer"></a><span data-ttu-id="94574-106">Uzamčení počítače</span><span class="sxs-lookup"><span data-stu-id="94574-106">Locking a Computer</span></span>

<span data-ttu-id="94574-107">Je jediný způsob, jak uzamknout počítače přímo pomocí standardních nástrojů k dispozici k volání **LockWorkstation()** fungovat v **user32.dll**:</span><span class="sxs-lookup"><span data-stu-id="94574-107">The only way to lock a computer directly with the standard available tools is to call the **LockWorkstation()** function in **user32.dll**:</span></span>

```
rundll32.exe user32.dll,LockWorkStation
```

<span data-ttu-id="94574-108">Tento příkaz okamžitě zamkne pracovní stanici.</span><span class="sxs-lookup"><span data-stu-id="94574-108">This command immediately locks the workstation.</span></span> <span data-ttu-id="94574-109">Používá *rundll32.exe*, které běží Windows knihovny DLL (a uloží jejich knihovny pro opakované použití) ke spuštění user32.dll, knihovnu funkce správy Windows.</span><span class="sxs-lookup"><span data-stu-id="94574-109">It uses *rundll32.exe*, which runs Windows DLLs (and saves their libraries for repeated use) to run user32.dll, a library of Windows management functions.</span></span>

<span data-ttu-id="94574-110">Když Uzamknout pracovní stanice rychlé přepínání uživatelů je povolen, jako je Windows XP, počítač zobrazí přihlašovací obrazovka uživatele spíše než počáteční spořič obrazovky aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="94574-110">When you lock a workstation while Fast User Switching is enabled, such as on Windows XP, the computer displays the user logon screen rather than starting the current user's screensaver.</span></span>

<span data-ttu-id="94574-111">Chcete-li vypnout konkrétní relace terminálového serveru, použijte **tsshutdn.exe** nástroj příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="94574-111">To shut down particular sessions on a Terminal Server, use the **tsshutdn.exe** command-line tool.</span></span>

### <a name="logging-off-the-current-session"></a><span data-ttu-id="94574-112">Odhlášení se od aktuální relace</span><span class="sxs-lookup"><span data-stu-id="94574-112">Logging Off the Current Session</span></span>

<span data-ttu-id="94574-113">Odhlášení relace v místním systému můžete použít několik různých technik.</span><span class="sxs-lookup"><span data-stu-id="94574-113">You can use several different techniques to log off of a session on the local system.</span></span> <span data-ttu-id="94574-114">Nejjednodušší způsob je pomocí nástroje příkazového řádku vzdálené plochy/Terminálové služby **logoff.exe** (podrobnosti najdete v příkazovém řádku Windows Powershellu, zadejte **odhlášení /?**).</span><span class="sxs-lookup"><span data-stu-id="94574-114">The simplest way is to use the Remote Desktop/Terminal Services command-line tool, **logoff.exe** (For details, at the Windows PowerShell prompt, type **logoff /?**).</span></span> <span data-ttu-id="94574-115">Chcete-li odhlásit aktuální aktivní relace, zadejte **odhlášení** bez argumentů.</span><span class="sxs-lookup"><span data-stu-id="94574-115">To log off the current active session, type **logoff** with no arguments.</span></span>

<span data-ttu-id="94574-116">Můžete také použít **shutdown.exe** nástroje s možností jeho odhlášení:</span><span class="sxs-lookup"><span data-stu-id="94574-116">You can also use the **shutdown.exe** tool with its logoff option:</span></span>

```
shutdown.exe -l
```

<span data-ttu-id="94574-117">Třetí možností je použít rozhraní WMI.</span><span class="sxs-lookup"><span data-stu-id="94574-117">A third option is to use WMI.</span></span> <span data-ttu-id="94574-118">Třídy Win32_OperatingSystem má metody Win32Shutdown metodu.</span><span class="sxs-lookup"><span data-stu-id="94574-118">The Win32_OperatingSystem class has a Win32Shutdown method.</span></span> <span data-ttu-id="94574-119">Vyvolání metody s 0 příznak zahájí odhlášení:</span><span class="sxs-lookup"><span data-stu-id="94574-119">Invoking the method with the 0 flag initiates logoff:</span></span>

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(0)
```

<span data-ttu-id="94574-120">Další informace a najít další funkce Win32Shutdown obsahuje všechny metody naleznete v tématu "Metody Win32Shutdown metoda z Win32_OperatingSystem třída" na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="94574-120">For more information, and to find other features of the Win32Shutdown method, see "Win32Shutdown Method of the Win32_OperatingSystem Class" in MSDN.</span></span>

### <a name="shutting-down-or-restarting-a-computer"></a><span data-ttu-id="94574-121">Vypnutí nebo restartování počítače</span><span class="sxs-lookup"><span data-stu-id="94574-121">Shutting Down or Restarting a Computer</span></span>

<span data-ttu-id="94574-122">Vypnutí a restartování počítačů jsou obvykle stejné typy úloh.</span><span class="sxs-lookup"><span data-stu-id="94574-122">Shutting down and restarting computers are generally the same types of task.</span></span> <span data-ttu-id="94574-123">Nástroje, které vypnout počítač obecně restartuje ho také – a naopak.</span><span class="sxs-lookup"><span data-stu-id="94574-123">Tools that shut down a computer will generally restart it as well—and vice versa.</span></span> <span data-ttu-id="94574-124">Existují dvě jednoduché možnosti pro restartování počítače z prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94574-124">There are two straightforward options for restarting a computer from Windows PowerShell.</span></span> <span data-ttu-id="94574-125">Použijte Tsshutdn.exe nebo Shutdown.exe s příslušnými argumenty.</span><span class="sxs-lookup"><span data-stu-id="94574-125">Use either Tsshutdn.exe or Shutdown.exe with appropriate arguments.</span></span> <span data-ttu-id="94574-126">Můžete získat podrobné informace o použití z **tsshutdn.exe /?**</span><span class="sxs-lookup"><span data-stu-id="94574-126">You can get detailed usage information from **tsshutdn.exe /?**</span></span> <span data-ttu-id="94574-127">nebo **shutdown.exe /?**.</span><span class="sxs-lookup"><span data-stu-id="94574-127">or **shutdown.exe /?**.</span></span>

<span data-ttu-id="94574-128">Můžete také provést vypnutí a restartování operace přímo z prostředí Windows PowerShell a.</span><span class="sxs-lookup"><span data-stu-id="94574-128">You can also perform shutdown and restart operations directly from Windows PowerShell as well.</span></span>

<span data-ttu-id="94574-129">Vypnutí počítače, použijte příkaz stop-computer</span><span class="sxs-lookup"><span data-stu-id="94574-129">To shut down the computer, use the stop-computer command</span></span>

```powershell
stop-computer
```

<span data-ttu-id="94574-130">Chcete-li restartovat operační systém, použijte příkaz restart-computer</span><span class="sxs-lookup"><span data-stu-id="94574-130">To restart the operating system, use the restart-computer command</span></span>

```powershell
restart-computer
```
