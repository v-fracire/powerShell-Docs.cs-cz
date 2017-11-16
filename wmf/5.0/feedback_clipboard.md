---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 8d5f8cc8c85d584b195483e464e878857629a78e
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="clipboard-cmdlets"></a><span data-ttu-id="a46eb-102">Rutiny schránky</span><span class="sxs-lookup"><span data-stu-id="a46eb-102">Clipboard cmdlets</span></span>
<span data-ttu-id="a46eb-103">**Get-schránky** a **schránky sadu** bylo snazší pro vás k přenosu obsahu do a z relace prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a46eb-103">**Get-Clipboard** and **Set-Clipboard** make it easier for you to transfer content to and from a Windows PowerShell session.</span></span> <span data-ttu-id="a46eb-104">Například, pokud pomocí Průzkumníka Windows zkopírujte tři soubory do schránky (výběrem je a stisknutím klávesy `ctrl-c`, například), potom můžete snadno přistupovat obsah ze schránky jako seznam souborů:</span><span class="sxs-lookup"><span data-stu-id="a46eb-104">For example, if you use Windows Explorer to copy three files to the clipboard (by selecting them and pressing `ctrl-c`, for example), you can then easily access the contents of the clipboard as a list of files:</span></span>

```powershell 
PS C:\\&gt; Get-Clipboard -Format FileDropList

Directory: C:\\Users\\slee\\Downloads\\Example

Mode LastWriteTime Length Name

---- ------------- ------ ----

-a---- 4/14/2015 1:19 PM 0 File2.txt

-a---- 4/14/2015 1:19 PM 0 File3.txt

-a---- 4/14/2015 1:19 PM 0 File1.txt
```


<span data-ttu-id="a46eb-105">Rutiny schránky podporovat bitové kopie, zvukové soubory, seznamy souborů a text.</span><span class="sxs-lookup"><span data-stu-id="a46eb-105">The Clipboard cmdlets support images, audio files, file lists, and text.</span></span>

