---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 4185d9395f2f3e5ba1c8daa0c365cb2bf322936b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
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

