---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 6caff8c06174a1dcb990ed8e5062ccca5848dbb8
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="convert-string"></a><span data-ttu-id="2d4c6-102">Převod řetězce</span><span class="sxs-lookup"><span data-stu-id="2d4c6-102">Convert-String</span></span>
<span data-ttu-id="2d4c6-103">**Převod řetězce** zpřístupňuje funkci, "nahradit pomocí magic".</span><span class="sxs-lookup"><span data-stu-id="2d4c6-103">**Convert-String** exposes "replace by magic" functionality.</span></span> <span data-ttu-id="2d4c6-104">Zadejte před a po příklady, jak chcete text, který se podíváte, a **převést řetězec** automaticky formátování textu.</span><span class="sxs-lookup"><span data-stu-id="2d4c6-104">Provide before and after examples of how you want text to look, and **Convert-String** formats your text automatically.</span></span> <span data-ttu-id="2d4c6-105">Tady je ukázkový - někdo na pořízení křestní jméno a příjmení a nahraďte ji své příjmení, čárku, první počáteční své příjmení a tečku.</span><span class="sxs-lookup"><span data-stu-id="2d4c6-105">Here's a demo - taking somebody's first and last name, and replacing it with their last name, a comma, the first initial of their last name, and a dot.</span></span> <span data-ttu-id="2d4c6-106">Opakujte s regex a najdete v části jak dlouho trvalo můžete.</span><span class="sxs-lookup"><span data-stu-id="2d4c6-106">Try it with a regex, and see how long it takes you.</span></span>

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```

