---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: ada4fcc0beb3eb74b099f221762341abbf2c3b4c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="new-temporaryfile"></a>Rutina New-TemporaryFile
Někdy ve skriptech, musíte vytvořit dočasný soubor. Můžete snadno to provést pomocí **New-TemporaryFile** rutiny:

PS C:\\ &gt; $tempFile = New-TemporaryFile

PS C:\\ &gt; $tempFile.FullName

C:\\Users\\slee\\AppData\\Local\\Temp\\tmp375.tmp