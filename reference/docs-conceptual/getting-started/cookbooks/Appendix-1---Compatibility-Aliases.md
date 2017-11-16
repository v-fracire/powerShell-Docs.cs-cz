---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Aliasy kompatibility dodatku 1
ms.assetid: 96ad921e-1a57-463e-8e60-424faf8b6ef8
ms.openlocfilehash: d789139ef80d4208b56e0b2930f04f824a00537d
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
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
|**dir**|**ls**|**Get-ChildItem**|**CGI**|
|**specifikací CLS**|**Vymazat**|**Clear-Host** (function)|**specifikací CLS**|
|**DEL, vymazání, rmdir**|**RM**|**Odebrat položky**|**RI**|
|**kopírování**|**prohlášení CP**|**Copy-Item**|**položky konfigurace**|
|**Přesunutí**|**MV**|**Přesun položek**|**mi**|
|**Přejmenování**|**MV**|**Přejmenování položky**|**rni**|
|**Typ**|**CAT**|**Get obsahu**|**uvolňování paměti**|
|**CD**|**CD**|**Nastavení umístění**|**SL**|
|**MD**|**mkdir**|**Nová položka**|**ni**|
|**pushd**|**pushd**|**Push – umístění**|**pushd**|
|**popd**|**popd**|**Umístění POP**|**popd**|

