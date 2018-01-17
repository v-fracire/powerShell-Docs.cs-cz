---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC pro Linux nxUser prostředků"
ms.openlocfilehash: 93e2b12af076fce687e045e3043c94fa82d61861
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-for-linux-nxuser-resource"></a>DSC pro Linux nxUser prostředků

**NxUser** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro ke správě místních uživatelů na uzlu Linux.

## <a name="syntax"></a>Syntaxe

```
nxUser <string> #ResourceName
{
    UserName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ FullName = <string> ]
    [ Description = <string> ]
    [ Password = <string> ]
    [ Disabled = <bool> ]
    [ PasswordChangeRequired = <bool> ]
    [ HomeDirectory = <string> ]
    [ GroupID = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost |  Určuje název účtu, pro které chcete zajistit určitý stav. | 
|---|---|
| UserName| Určuje umístění, kde chcete zajistit stav pro soubor nebo adresář.| 
| Ujistěte se| Určuje, jestli účet existuje. Nastavením této vlastnosti "Přítomen" zajistit, že existuje účet a nastavte ji na "Chybí" zajistit, že účet neexistuje.| 
| FullName| Řetězec, který obsahuje úplný název pro uživatelský účet.| 
| Popis| Popis pro uživatelský účet.| 
| Heslo| Hodnota hash hesla uživatele v příslušný formulář pro počítače se systémem Linux. Obvykle je to solené SHA-256, nebo hodnotu hash SHA-512. Na Debian a Ubuntu Linux tato hodnota může být generována pomocí příkazu mkpasswd. Pro ostatní distribucích systému Linux metodu crypt knihovny jazyka Python Crypt slouží ke generování hodnoty hash.| 
| Zakázáno| Určuje, zda je povolen. Tuto vlastnost nastavit na **$true** zajistit, že tento účet je zakázané a nastavte ji na **$false** zajistit, že je povolena.| 
| PasswordChangeRequired| Určuje, zda může uživatel změnit heslo. Tuto vlastnost nastavit na **$true** zajistit, že uživatel nemůže změnit heslo a nastavte ji na **$false** umožňuje uživatelům změnit heslo. Výchozí hodnota je **$false**. Tato vlastnost je Vyhodnocená jenom Pokud uživatelský účet dříve neexistoval a je vytvářena.| 
| Domovský_adresář| Domovský adresář pro uživatele.| 
| GroupID| Identifikátor primární skupiny uživatele.| 
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud ID bloku skriptu konfigurace prostředků, který chcete spustit nejprve je "ResourceName" a "Typ prostředku" je její typ, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.| 

## <a name="example"></a>Příklad

Následující příklad zajistí, že uživatel "monuser" existuje a je členem skupiny "DBusers".

```
Import-DSCResource -Module nx 

Node $node {
nxUser UserExample{
   UserName = "monuser"
   Description = "Monitoring user"
   Password  =    '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
   Ensure = "Present"
   HomeDirectory = "/home/monuser"
}
 
nxGroup GroupExample{
   GroupName = "DBusers"
   Ensure = "Present"
   MembersToInclude = "monuser"
   DependsOn = "[nxUser]UserExample"            
}
}
```

