---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Spuštění 32bitové verze Windows PowerShellu"
ms.assetid: 12b31890-2609-4a76-8c24-0ebe78084f50
ms.openlocfilehash: d682ce45ebc92cda3a9008ab608bacf9ef8eba57
ms.sourcegitcommit: 18e3bfae83ffe282d3fd1a45f5386f3b7250f0c0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/08/2018
---
# <a name="starting-the-32-bit-version-of-windows-powershell"></a><span data-ttu-id="6b361-103">Spuštění 32bitové verze prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b361-103">Starting the 32-Bit Version of Windows PowerShell</span></span>
<span data-ttu-id="6b361-104">Při instalaci prostředí Windows PowerShell na 64bitovém počítači **prostředí Windows PowerShell (x86)**, 32bitová verze prostředí Windows PowerShell je nainstalovaný kromě 64bitovou verzi.</span><span class="sxs-lookup"><span data-stu-id="6b361-104">When you install Windows PowerShell on a 64-bit computer, **Windows PowerShell (x86)**, a 32-bit version of Windows PowerShell is installed in addition to the 64-bit version.</span></span> <span data-ttu-id="6b361-105">Při spuštění prostředí Windows PowerShell ve výchozím nastavení spustí 64bitovou verzi.</span><span class="sxs-lookup"><span data-stu-id="6b361-105">When you run Windows PowerShell, the 64-bit version runs by default.</span></span>

<span data-ttu-id="6b361-106">Však může někdy musíte spustit **prostředí Windows PowerShell (x86)**, například při použití modulu, který vyžaduje 32bitovou verzi nebo kdy se vzdáleně připojují k 32bitového počítače.</span><span class="sxs-lookup"><span data-stu-id="6b361-106">However, you might occasionally need to run **Windows PowerShell (x86)**, such as when you are using a module that requires the 32-bit version or when you are connecting remotely to a 32-bit computer.</span></span>

<span data-ttu-id="6b361-107">Spusťte 32bitovou verzi prostředí Windows PowerShell, použijte některý z následujících postupů.</span><span class="sxs-lookup"><span data-stu-id="6b361-107">To start a 32-bit version of Windows PowerShell, use any of the following procedures.</span></span>

#### <a name="in-windows-server-2012-r2"></a><span data-ttu-id="6b361-108">In Windows Server® 2012 R2</span><span class="sxs-lookup"><span data-stu-id="6b361-108">In Windows Server® 2012 R2</span></span>

- <span data-ttu-id="6b361-109">Na **spustit** zadejte **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="6b361-109">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="6b361-110">Klikněte **prostředí Windows PowerShell x86** dlaždici.</span><span class="sxs-lookup"><span data-stu-id="6b361-110">Click the **Windows PowerShell x86** tile.</span></span>

- <span data-ttu-id="6b361-111">V **správce serveru**, z **nástroje** nabídce vyberte možnost **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="6b361-111">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="6b361-112">Přesunutí kurzoru do pravého horního rohu klikněte na ploše **vyhledávání**, typ **prostředí PowerShell x86** a pak klikněte na **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="6b361-112">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="6b361-113">Prostřednictvím příkazového řádku zadejte:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="6b361-113">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-server-2012"></a><span data-ttu-id="6b361-114">In Windows Server® 2012</span><span class="sxs-lookup"><span data-stu-id="6b361-114">In Windows Server® 2012</span></span>

- <span data-ttu-id="6b361-115">Na **spustit** zadejte **prostředí PowerShell** a pak klikněte na **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="6b361-115">On the **Start** screen, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="6b361-116">V **správce serveru**, z **nástroje** nabídce vyberte možnost **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="6b361-116">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="6b361-117">Přesunutí kurzoru do pravého horního rohu klikněte na ploše **vyhledávání**, typ **prostředí PowerShell** a pak klikněte na **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="6b361-117">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="6b361-118">Prostřednictvím příkazového řádku zadejte:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="6b361-118">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-81"></a><span data-ttu-id="6b361-119">V Windows® 8.1</span><span class="sxs-lookup"><span data-stu-id="6b361-119">In Windows® 8.1</span></span>

- <span data-ttu-id="6b361-120">Na **spustit** zadejte **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="6b361-120">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="6b361-121">Klikněte **prostředí Windows PowerShell x86** dlaždici.</span><span class="sxs-lookup"><span data-stu-id="6b361-121">Click the **Windows PowerShell x86** tile.</span></span>

- <span data-ttu-id="6b361-122">Pokud používáte [nástrojů pro vzdálenou správu serveru](http://go.microsoft.com/fwlink/?LinkID=304145) pro Windows 8.1, můžete také otevřít prostředí Windows PowerShell x86 z **Server ManagerTools** nabídky.</span><span class="sxs-lookup"><span data-stu-id="6b361-122">If you are running [Remote Server Administration Tools](http://go.microsoft.com/fwlink/?LinkID=304145) for Windows 8.1, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span> <span data-ttu-id="6b361-123">Vyberte **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="6b361-123">Select **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="6b361-124">Přesunutí kurzoru do pravého horního rohu klikněte na ploše **vyhledávání**, typ **prostředí PowerShell x86** a pak klikněte na **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="6b361-124">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
   
- <span data-ttu-id="6b361-125">Prostřednictvím příkazového řádku zadejte:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="6b361-125">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-8"></a><span data-ttu-id="6b361-126">V Windows® 8</span><span class="sxs-lookup"><span data-stu-id="6b361-126">In Windows® 8</span></span>

- <span data-ttu-id="6b361-127">Na **spustit** obrazovky, přesuňte se ukazatelem do pravého horního rohu, klikněte na **nastavení**, klikněte na tlačítko **dlaždice**a poté přesuňte **zobrazit nástroje pro správu** jezdec na Ano.</span><span class="sxs-lookup"><span data-stu-id="6b361-127">On the **Start** screen, move the cursor to the upper right corner, click **Settings**, click **Tiles**, and then move the **Show Administrative Tools** slider to Yes.</span></span> <span data-ttu-id="6b361-128">Poté zadejte **prostředí PowerShell** a klikněte na tlačítko **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="6b361-128">Then, type **PowerShell** and click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="6b361-129">Pokud používáte [nástrojů pro vzdálenou správu serveru](http://www.microsoft.com/download/details.aspx?id=28972) pro systém Windows 8, můžete také otevřít prostředí Windows PowerShell x86 z **Server ManagerTools** nabídky.</span><span class="sxs-lookup"><span data-stu-id="6b361-129">If you are running [Remote Server Administration Tools](http://www.microsoft.com/download/details.aspx?id=28972) for Windows 8, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span> <span data-ttu-id="6b361-130">Vyberte **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="6b361-130">Select **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="6b361-131">Na **spustit** obrazovky nebo plocha, zadejte **prostředí PowerShell (x86)** a pak klikněte na **prostředí Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="6b361-131">On the **Start** screen or the desktop, type **PowerShell (x86)** and then click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="6b361-132">Prostřednictvím příkazového řádku zadejte:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="6b361-132">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

