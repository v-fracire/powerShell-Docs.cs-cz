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
# <a name="convert-string"></a>Rutina Convert-String
**Převod řetězce** zpřístupňuje funkci, "nahradit pomocí magic". Zadejte před a po příklady, jak chcete text, který se podíváte, a **převést řetězec** automaticky formátování textu. Tady je ukázkový - někdo na pořízení křestní jméno a příjmení a nahraďte ji své příjmení, čárku, první počáteční své příjmení a tečku. Opakujte s regex a najdete v části jak dlouho trvalo můžete.

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```