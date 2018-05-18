---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 08f431c27cd0ee769518b5246af2fa95aa499d54
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="new-temporaryfile"></a><span data-ttu-id="5ca76-102">Rutina New-TemporaryFile</span><span class="sxs-lookup"><span data-stu-id="5ca76-102">New-TemporaryFile</span></span>
<span data-ttu-id="5ca76-103">Někdy ve skriptech, musíte vytvořit dočasný soubor.</span><span class="sxs-lookup"><span data-stu-id="5ca76-103">Sometimes in your scripts, you must create a temporary file.</span></span> <span data-ttu-id="5ca76-104">Můžete snadno to provést pomocí **New-TemporaryFile** rutiny:</span><span class="sxs-lookup"><span data-stu-id="5ca76-104">You can easily do this with the **New-TemporaryFile** cmdlet:</span></span>

<span data-ttu-id="5ca76-105">PS C:\\ &gt; $tempFile = New-TemporaryFile</span><span class="sxs-lookup"><span data-stu-id="5ca76-105">PS C:\\&gt; $tempFile = New-TemporaryFile</span></span>

<span data-ttu-id="5ca76-106">PS C:\\ &gt; $tempFile.FullName</span><span class="sxs-lookup"><span data-stu-id="5ca76-106">PS C:\\&gt; $tempFile.FullName</span></span>

<span data-ttu-id="5ca76-107">C:\\uživatelé\\slee\\data aplikací\\místní\\Temp\\tmp375.tmp</span><span class="sxs-lookup"><span data-stu-id="5ca76-107">C:\\Users\\slee\\AppData\\Local\\Temp\\tmp375.tmp</span></span>
