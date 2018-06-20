---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 9ca12ad3f0729a2e9595d7ca5ccf9041e47658a3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218089"
---
# <a name="archive-cmdlets"></a><span data-ttu-id="ccb1e-102">Rutiny archivu</span><span class="sxs-lookup"><span data-stu-id="ccb1e-102">Archive cmdlets</span></span>

<span data-ttu-id="ccb1e-103">Dvě nové rutiny, **Compress archivu** a **rozbalte archivu**, umožňují komprimovat a rozbalte soubory ZIP.</span><span class="sxs-lookup"><span data-stu-id="ccb1e-103">Two new cmdlets, **Compress-Archive** and **Expand-Archive**, let you compress and expand ZIP files.</span></span>

## <a name="compress-archive"></a><span data-ttu-id="ccb1e-104">Komprimovat archivu</span><span class="sxs-lookup"><span data-stu-id="ccb1e-104">Compress-Archive</span></span>
<span data-ttu-id="ccb1e-105">**Compress archivu** rutina vytvoří nový soubor archivu ze zadané soubory.</span><span class="sxs-lookup"><span data-stu-id="ccb1e-105">The **Compress-Archive** cmdlet creates a new archive file from specified files.</span></span> <span data-ttu-id="ccb1e-106">Soubor archivu umožňuje soubory, které mají být zabalené a volitelně komprimované do jednoho souboru pro snadnější zpracování a úložiště.</span><span class="sxs-lookup"><span data-stu-id="ccb1e-106">An archive file allows multiple files to be packaged and optionally compressed into a single file for easier handling and storage.</span></span> <span data-ttu-id="ccb1e-107">Pomocí zadané v algoritmus komprese lze komprimovat soubor archivu **- CompressionLevel** parametr.</span><span class="sxs-lookup"><span data-stu-id="ccb1e-107">An archive file can be compressed by using a compression algorithm specified in the **-CompressionLevel** parameter.</span></span>
```powershell
Compress-Archive -LiteralPath <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
Compress-Archive [-Path] <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
```

## <a name="expand-archive"></a><span data-ttu-id="ccb1e-108">Rozbalte archivu</span><span class="sxs-lookup"><span data-stu-id="ccb1e-108">Expand-Archive</span></span>
<span data-ttu-id="ccb1e-109">**Rozbalte archivu** rutiny extrahuje soubory z archivu zadaný soubor.</span><span class="sxs-lookup"><span data-stu-id="ccb1e-109">The **Expand-Archive** cmdlet extracts files from a specified archive file.</span></span> <span data-ttu-id="ccb1e-110">Soubor archivu umožňuje soubory, které mají být zabalené a volitelně komprimované do jednoho souboru pro snadnější zpracování a úložiště.</span><span class="sxs-lookup"><span data-stu-id="ccb1e-110">An archive file allows multiple files to be packaged and optionally compressed into a single file for easier handling and storage.</span></span>
```powershell
Expand-Archive -LiteralPath <String> [-DestinationPath] <String>
Expand-Archive [-Path] <String> [-DestinationPath] <String>
```
