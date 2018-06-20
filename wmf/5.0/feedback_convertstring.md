---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 7730912707bb14e90a9926b387fb3a859d7ca26d
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219262"
---
# <a name="convert-string"></a><span data-ttu-id="fd617-102">Rutina Convert-String</span><span class="sxs-lookup"><span data-stu-id="fd617-102">Convert-String</span></span>
<span data-ttu-id="fd617-103">**Převod řetězce** zpřístupňuje funkci, "nahradit pomocí magic".</span><span class="sxs-lookup"><span data-stu-id="fd617-103">**Convert-String** exposes "replace by magic" functionality.</span></span> <span data-ttu-id="fd617-104">Zadejte před a po příklady, jak chcete text, který se podíváte, a **převést řetězec** automaticky formátování textu.</span><span class="sxs-lookup"><span data-stu-id="fd617-104">Provide before and after examples of how you want text to look, and **Convert-String** formats your text automatically.</span></span> <span data-ttu-id="fd617-105">Tady je ukázkový - někdo na pořízení křestní jméno a příjmení a nahraďte ji své příjmení, čárku, první počáteční své příjmení a tečku.</span><span class="sxs-lookup"><span data-stu-id="fd617-105">Here's a demo - taking somebody's first and last name, and replacing it with their last name, a comma, the first initial of their last name, and a dot.</span></span> <span data-ttu-id="fd617-106">Opakujte s regex a najdete v části jak dlouho trvalo můžete.</span><span class="sxs-lookup"><span data-stu-id="fd617-106">Try it with a regex, and see how long it takes you.</span></span>

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```
