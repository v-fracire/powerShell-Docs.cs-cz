---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 302a347b0f4c9c322f7701e8d6a721f9ffba9b59
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="convert-string"></a><span data-ttu-id="b2c5a-102">Rutina Convert-String</span><span class="sxs-lookup"><span data-stu-id="b2c5a-102">Convert-String</span></span>
<span data-ttu-id="b2c5a-103">**Převod řetězce** zpřístupňuje funkci, "nahradit pomocí magic".</span><span class="sxs-lookup"><span data-stu-id="b2c5a-103">**Convert-String** exposes "replace by magic" functionality.</span></span> <span data-ttu-id="b2c5a-104">Zadejte před a po příklady, jak chcete text, který se podíváte, a **převést řetězec** automaticky formátování textu.</span><span class="sxs-lookup"><span data-stu-id="b2c5a-104">Provide before and after examples of how you want text to look, and **Convert-String** formats your text automatically.</span></span> <span data-ttu-id="b2c5a-105">Tady je ukázkový - někdo na pořízení křestní jméno a příjmení a nahraďte ji své příjmení, čárku, první počáteční své příjmení a tečku.</span><span class="sxs-lookup"><span data-stu-id="b2c5a-105">Here's a demo - taking somebody's first and last name, and replacing it with their last name, a comma, the first initial of their last name, and a dot.</span></span> <span data-ttu-id="b2c5a-106">Opakujte s regex a najdete v části jak dlouho trvalo můžete.</span><span class="sxs-lookup"><span data-stu-id="b2c5a-106">Try it with a regex, and see how long it takes you.</span></span>

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```