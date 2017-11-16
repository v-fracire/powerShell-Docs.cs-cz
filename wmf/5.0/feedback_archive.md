---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 7ad4a00f7beba0de70696d88cd5448c7c638c50c
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/27/2017
---
# <a name="archive-cmdlets"></a><span data-ttu-id="5d01f-102">Rutiny archivu</span><span class="sxs-lookup"><span data-stu-id="5d01f-102">Archive cmdlets</span></span>

<span data-ttu-id="5d01f-103">Dvě nové rutiny, **Compress archivu** a **rozbalte archivu**, umožňují komprimovat a rozbalte soubory ZIP.</span><span class="sxs-lookup"><span data-stu-id="5d01f-103">Two new cmdlets, **Compress-Archive** and **Expand-Archive**, let you compress and expand ZIP files.</span></span>

## <a name="compress-archive"></a><span data-ttu-id="5d01f-104">Komprimovat archivu</span><span class="sxs-lookup"><span data-stu-id="5d01f-104">Compress-Archive</span></span>
<span data-ttu-id="5d01f-105">**Compress archivu** rutina vytvoří nový soubor archivu ze zadané soubory.</span><span class="sxs-lookup"><span data-stu-id="5d01f-105">The **Compress-Archive** cmdlet creates a new archive file from specified files.</span></span> <span data-ttu-id="5d01f-106">Soubor archivu umožňuje soubory, které mají být zabalené a volitelně komprimované do jednoho souboru pro snadnější zpracování a úložiště.</span><span class="sxs-lookup"><span data-stu-id="5d01f-106">An archive file allows multiple files to be packaged and optionally compressed into a single file for easier handling and storage.</span></span> <span data-ttu-id="5d01f-107">Pomocí zadané v algoritmus komprese lze komprimovat soubor archivu **- CompressionLevel** parametr.</span><span class="sxs-lookup"><span data-stu-id="5d01f-107">An archive file can be compressed by using a compression algorithm specified in the **-CompressionLevel** parameter.</span></span>
```powershell
Compress-Archive -LiteralPath <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>] 
Compress-Archive [-Path] <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
```

## <a name="expand-archive"></a><span data-ttu-id="5d01f-108">Rozbalte archivu</span><span class="sxs-lookup"><span data-stu-id="5d01f-108">Expand-Archive</span></span>
<span data-ttu-id="5d01f-109">**Rozbalte archivu** rutiny extrahuje soubory z archivu zadaný soubor.</span><span class="sxs-lookup"><span data-stu-id="5d01f-109">The **Expand-Archive** cmdlet extracts files from a specified archive file.</span></span> <span data-ttu-id="5d01f-110">Soubor archivu umožňuje soubory, které mají být zabalené a volitelně komprimované do jednoho souboru pro snadnější zpracování a úložiště.</span><span class="sxs-lookup"><span data-stu-id="5d01f-110">An archive file allows multiple files to be packaged and optionally compressed into a single file for easier handling and storage.</span></span>
```powershell
Expand-Archive -LiteralPath <String> [-DestinationPath] <String>
Expand-Archive [-Path] <String> [-DestinationPath] <String>
```

