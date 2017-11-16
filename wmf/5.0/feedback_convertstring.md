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
# <a name="convert-string"></a>Převod řetězce
**Převod řetězce** zpřístupňuje funkci, "nahradit pomocí magic". Zadejte před a po příklady, jak chcete text, který se podíváte, a **převést řetězec** automaticky formátování textu. Tady je ukázkový - někdo na pořízení křestní jméno a příjmení a nahraďte ji své příjmení, čárku, první počáteční své příjmení a tečku. Opakujte s regex a najdete v části jak dlouho trvalo můžete.

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```

