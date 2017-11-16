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
# <a name="new-temporaryfile"></a><span data-ttu-id="04b86-102">Nové TemporaryFile</span><span class="sxs-lookup"><span data-stu-id="04b86-102">New-TemporaryFile</span></span>
<span data-ttu-id="04b86-103">Někdy ve skriptech, musíte vytvořit dočasný soubor.</span><span class="sxs-lookup"><span data-stu-id="04b86-103">Sometimes in your scripts, you must create a temporary file.</span></span> <span data-ttu-id="04b86-104">Můžete snadno to provést pomocí **New-TemporaryFile** rutiny:</span><span class="sxs-lookup"><span data-stu-id="04b86-104">You can easily do this with the **New-TemporaryFile** cmdlet:</span></span>

<span data-ttu-id="04b86-105">PS C:\\ &gt; $tempFile = New-TemporaryFile</span><span class="sxs-lookup"><span data-stu-id="04b86-105">PS C:\\&gt; $tempFile = New-TemporaryFile</span></span>

<span data-ttu-id="04b86-106">PS C:\\ &gt; $tempFile.FullName</span><span class="sxs-lookup"><span data-stu-id="04b86-106">PS C:\\&gt; $tempFile.FullName</span></span>

<span data-ttu-id="04b86-107">C:\\uživatelé\\slee\\data aplikací\\místní\\Temp\\tmp375.tmp</span><span class="sxs-lookup"><span data-stu-id="04b86-107">C:\\Users\\slee\\AppData\\Local\\Temp\\tmp375.tmp</span></span>

