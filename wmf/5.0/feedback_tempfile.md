---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 90e0ab3579e1840598cc3050c27db0b73ba6f69d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="new-temporaryfile"></a>Nové TemporaryFile
Někdy ve skriptech, musíte vytvořit dočasný soubor. Můžete snadno to provést pomocí **New-TemporaryFile** rutiny:

PS C:\\ &gt; $tempFile = New-TemporaryFile

PS C:\\ &gt; $tempFile.FullName

C:\\uživatelé\\slee\\data aplikací\\místní\\Temp\\tmp375.tmp

