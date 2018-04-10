---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: d34a267bae7e48afe4442256d7f112da3a97eb7d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="clipboard-cmdlets"></a><span data-ttu-id="9c546-102">Rutiny schránky</span><span class="sxs-lookup"><span data-stu-id="9c546-102">Clipboard cmdlets</span></span>
<span data-ttu-id="9c546-103">**Get-schránky** a **schránky sadu** bylo snazší pro vás k přenosu obsahu do a z relace prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9c546-103">**Get-Clipboard** and **Set-Clipboard** make it easier for you to transfer content to and from a Windows PowerShell session.</span></span> <span data-ttu-id="9c546-104">Například, pokud pomocí Průzkumníka Windows zkopírujte tři soubory do schránky (výběrem je a stisknutím klávesy `ctrl-c`, například), potom můžete snadno přistupovat obsah ze schránky jako seznam souborů:</span><span class="sxs-lookup"><span data-stu-id="9c546-104">For example, if you use Windows Explorer to copy three files to the clipboard (by selecting them and pressing `ctrl-c`, for example), you can then easily access the contents of the clipboard as a list of files:</span></span>

```powershell
PS C:\\&gt; Get-Clipboard -Format FileDropList

Directory: C:\\Users\\slee\\Downloads\\Example

Mode LastWriteTime Length Name

---- ------------- ------ ----

-a---- 4/14/2015 1:19 PM 0 File2.txt

-a---- 4/14/2015 1:19 PM 0 File3.txt

-a---- 4/14/2015 1:19 PM 0 File1.txt
```


<span data-ttu-id="9c546-105">Rutiny schránky podporovat bitové kopie, zvukové soubory, seznamy souborů a text.</span><span class="sxs-lookup"><span data-stu-id="9c546-105">The Clipboard cmdlets support images, audio files, file lists, and text.</span></span>