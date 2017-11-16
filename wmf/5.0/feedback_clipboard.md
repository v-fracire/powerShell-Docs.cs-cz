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
# <a name="clipboard-cmdlets"></a>Rutiny schránky
**Get-schránky** a **schránky sadu** bylo snazší pro vás k přenosu obsahu do a z relace prostředí Windows PowerShell. Například, pokud pomocí Průzkumníka Windows zkopírujte tři soubory do schránky (výběrem je a stisknutím klávesy `ctrl-c`, například), potom můžete snadno přistupovat obsah ze schránky jako seznam souborů:

```powershell 
PS C:\\&gt; Get-Clipboard -Format FileDropList

Directory: C:\\Users\\slee\\Downloads\\Example

Mode LastWriteTime Length Name

---- ------------- ------ ----

-a---- 4/14/2015 1:19 PM 0 File2.txt

-a---- 4/14/2015 1:19 PM 0 File3.txt

-a---- 4/14/2015 1:19 PM 0 File1.txt
```


Rutiny schránky podporovat bitové kopie, zvukové soubory, seznamy souborů a text.

