---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxUser
ms.openlocfilehash: 1b02be1559957585a2a1733630cb93440e8182f9
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048122"
---
# <a name="dsc-for-linux-nxuser-resource"></a>DSC pro Linux prostředek nxUser

**NxUser** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě místních uživatelů na uzlu systému Linux.

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
| UserName| Určuje umístění, kam chcete zajistit stavu pro soubor nebo adresář.|
| Zkontrolujte| Určuje, jestli účet existuje. Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že existuje účet a nastavte ho na "Chybí" Ujistěte se, že účet neexistuje.|
| Jméno a příjmení| Řetězec obsahující úplný název pro uživatelský účet.|
| Popis| Popis pro uživatelský účet.|
| Heslo| Hodnota hash hesla uživatele ve formuláři vhodná pro počítače s Linuxem. Obvykle je to solené SHA-256 nebo hodnoty hash SHA-512. Debian a Ubuntu Linux tato hodnota dá vygenerovat pomocí příkazu mkpasswd. Pro jiné distribuce Linuxu metoda crypt Crypt knihovny pro Python slouží ke generování hodnoty hash.|
| Zakázáno| Určuje, zda je účet povolený. Tuto vlastnost nastavte na **$true** zajistit, že tento účet je zakázaný a nastavte ho na **$false** ujistěte, že je povolena.|
| PasswordChangeRequired| Určuje, jestli uživatel může změnit heslo. Tuto vlastnost nastavte na **$true** zajistit, že uživatel nemůže změnit heslo a nastavte ho na **$false** aby uživatel mohl změnit heslo. Výchozí hodnota je **$false**. Tato vlastnost je vyhodnocen pouze pokud uživatelský účet dříve neexistoval a se vytváří.|
| Domovský_adresář| Domovský adresář pro uživatele.|
| ID skupiny| ID primární skupiny uživatele.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud je ID bloku skriptu konfigurace prostředků, kterou chcete spustit nejprve "ResourceName" a její typ je "ResourceType", syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|

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