---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 62cccabd7c63c6ba928fc2bf8addd3d11483e90f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
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