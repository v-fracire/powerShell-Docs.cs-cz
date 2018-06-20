---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: d9f1ca10c948b06b234e17f688b8f899ed41c5d6
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34221897"
---
# <a name="get-childitem-has--depth-parameter"></a>Get-ChildItem má – hloubka parametr
**Get-ChildItem** má teď **– hloubka** parametr použijete s **– Recurse** omezit rekurze:

PS C:\\uživatelé\\slee\\stáhne\\příklad&gt; Get-ChildItem-Recurse - hloubka 0

Adresář: C:\\uživatelé\\slee\\stáhne\\příklad

Název režimu LastWriteTime délka

---- ------------- ------ ----

d---Depth0 17:36:00 4 14. prosince 2015

-a---4/14. prosince 2015 1:19 PM 0 File1.txt

-a---4/14. prosince 2015 1:19 PM 0 Soubor2.txt

-a---4/14. prosince 2015 1:19 PM 0 File3.txt

PS C:\\uživatelé\\slee\\stáhne\\příklad&gt; Get-ChildItem-Recurse - hloubku 1

Adresář: C:\\uživatelé\\slee\\stáhne\\příklad

Název režimu LastWriteTime délka

---- ------------- ------ ----

d---Depth0 17:36:00 4 14. prosince 2015

-a---4/14. prosince 2015 1:19 PM 0 File1.txt

-a---4/14. prosince 2015 1:19 PM 0 Soubor2.txt

-a---4/14. prosince 2015 1:19 PM 0 File3.txt

Adresář: C:\\uživatelé\\slee\\stáhne\\příklad\\Depth0

Název režimu LastWriteTime délka

---- ------------- ------ ----

d---Depth1 5:33 odp 4 14. prosince 2015
