---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: 'Příloha 1: Kompatibilní aliasy'
ms.assetid: 96ad921e-1a57-463e-8e60-424faf8b6ef8
ms.openlocfilehash: 113bbee1af185f98777df5767022d54accb69447
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954632"
---
# <a name="appendix-1---compatibility-aliases"></a>Příloha 1 - aliasy kompatibility

Prostředí Windows PowerShell obsahuje několik přechod aliasy, které umožňují uživatelům se systémem UNIX a Cmd používat názvy známých příkazů v prostředí Windows PowerShell. Nejběžnější aliasy jsou uvedeny v následující tabulce, společně s příkaz prostředí Windows PowerShell za alias a standardní prostředí Windows PowerShell alias, pokud existuje.

Můžete najít příkaz prostředí Windows PowerShell, který libovolným aliasem odkazuje na z prostředí Windows PowerShell pomocí rutiny Get-Alias. Můžete například zadat **get-alias se specifikací cls**.

```
CommandType     Name                            Definition
-----------     ----                            ----------
Alias           cls                             Clear-Host
```

|Příkaz CMD|Příkaz systému UNIX|PS Příkaz|PS Alias|
|---------------|----------------|--------------|------------|
|**Dir**|**Ls**|**Get-ChildItem**|**gci**|
|**specifikací CLS**|**clear**|**Clear-Host** (function)|**specifikací CLS**|
|**DEL, vymazání, rmdir**|**rm**|**Odebrat položky**|**ri**|
|**Kopírování**|**cp**|**Copy-Item**|**ci**|
|**Přesunutí**|**mv**|**Přesun položek**|**mi**|
|**rename**|**mv**|**Přejmenování položky**|**rni**|
|**Typ**|**cat**|**Get-Content**|**gc**|
|**cd**|**cd**|**Nastavení umístění**|**sl**|
|**md**|**mkdir**|**Nová položka**|**ni**|
|**pushd**|**pushd**|**Push – umístění**|**pushd**|
|**popd**|**popd**|**Umístění POP**|**popd**|