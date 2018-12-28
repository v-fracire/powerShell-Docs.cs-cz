---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: 'Příloha 1: Kompatibilní aliasy'
ms.assetid: 96ad921e-1a57-463e-8e60-424faf8b6ef8
ms.openlocfilehash: 113bbee1af185f98777df5767022d54accb69447
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404093"
---
# <a name="appendix-1---compatibility-aliases"></a>Příloha 1 – kompatibilní aliasy

Prostředí Windows PowerShell obsahuje několik přechod aliasy, které umožňují uživatelům se systémem UNIX a Cmd použití známých názvů příkazů v prostředí Windows PowerShell. Nejběžnější aliasy jsou uvedeny v následující tabulce, spolu s Windows Powershellu příkaz alias a standardní prostředí Windows PowerShell alias, pokud existuje.

Můžete najít příkazu prostředí Windows PowerShell, který jakýkoli alias odkazuje na z v rámci prostředí Windows PowerShell pomocí rutiny Get-Alias. Zadejte například **get-alias kompatibilní se specifikací**.

```
CommandType     Name                            Definition
-----------     ----                            ----------
Alias           cls                             Clear-Host
```

|Příkaz CMD|Příkaz systému UNIX|PS Příkaz|PS Alias|
|---------------|----------------|--------------|------------|
|**adresář**|**Ls**|**Rutina Get-ChildItem**|**CGI**|
|**specifikace CLS**|**Vymazat**|**Clear-Host** (function)|**specifikace CLS**|
|**DEL, vymazání, rmdir**|**Správce prostředků**|**Odebrat položku**|**rezervované instance**|
|**Kopírování**|**prohlášení CP**|**Kopírovat položku**|**průběžná integrace**|
|**Přesunutí**|**MV**|**Přesunout položku**|**mi**|
|**Přejmenovat**|**MV**|**Přejmenovat položku**|**rni**|
|**Typ**|**CAT**|**Get obsah**|**uvolňování paměti**|
|**CD**|**CD**|**Nastavení umístění**|**SL**|
|**MD**|**mkdir**|**Nová položka**|**ni**|
|**pushd**|**pushd**|**Umístění nabízených oznámení**|**pushd**|
|**popd**|**popd**|**Umístění POP**|**popd**|