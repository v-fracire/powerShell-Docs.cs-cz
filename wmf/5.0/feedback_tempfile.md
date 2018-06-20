---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 08f431c27cd0ee769518b5246af2fa95aa499d54
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34217987"
---
# <a name="new-temporaryfile"></a>Rutina New-TemporaryFile
Někdy ve skriptech, musíte vytvořit dočasný soubor. Můžete snadno to provést pomocí **New-TemporaryFile** rutiny:

PS C:\\ &gt; $tempFile = New-TemporaryFile

PS C:\\ &gt; $tempFile.FullName

C:\\uživatelé\\slee\\data aplikací\\místní\\Temp\\tmp375.tmp
