---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxSshAuthorizedKeys
ms.openlocfilehash: d4cdb727a94a5e89e8401769f24977d49bcf4929
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048208"
---
# <a name="dsc-for-linux-nxsshauthorizedkeys-resource"></a>DSC pro Linux prostředek nxSshAuthorizedKeys

**NxAuthorizedKeys** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě oprávnění ssh klíče pro zadaného uživatele.

## <a name="syntax"></a>Syntaxe

```
nxAuthorizedKeys <string> #ResourceName
{
    KeyComment = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Username = <string> ]
    [ Key = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost |  Popis |
|---|---|
| KeyComment| Komentář jedinečné klíče. Slouží k jednoznačné identifikaci klíče.|
| Zkontrolujte| Určuje, zda je definován klíč. Nastavte tuto vlastnost na "Chybí" Ujistěte se, že klíč v souboru autorizovaných klíčů uživatele neexistuje. Nastavte ho na "Obsahuje" Ujistěte se, že klíč je definována v souboru klíče autorizované uživatele.|
| Uživatelské jméno| Uživatelské jméno ssh spravovat oprávnění klíče. Pokud není definován, je výchozí uživatel "root".|
| Klávesa| Obsah klíče. To je potřeba, pokud **Ujistěte se, že** je nastavena na "K dispozici".|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Příklad

Následující příklad definuje oprávnění ssh veřejné klíče pro uživatele "monuser".

```
Import-DSCResource -Module nx

Node $node {

nxSshAuthorizedKeys myKey{
   KeyComment = "myKey"
   Ensure = "Present"
   Key = 'ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEA0b+0xSd07QXRifm3FXj7Pn/DblA6QI5VAkDm6OivFzj3U6qGD1VJ6AAxWPCyMl/qhtpRtxZJDu/TxD8AyZNgc8aN2CljN1hOMbBRvH2q5QPf/nCnnJRaGsrxIqZjyZdYo9ZEEzjZUuMDM5HI1LA9B99k/K6PK2Bc1NLivpu7nbtVG2tLOQs+GefsnHuetsRMwo/+c3LtwYm9M0XfkGjYVCLO4CoFuSQpvX6AB3TedUy6NZ0iuxC0kRGg1rIQTwSRcw+McLhslF0drs33fw6tYdzlLBnnzimShMuiDWiT37WqCRovRGYrGCaEFGTG2e0CN8Co8nryXkyWc6NSDNpMzw== rsa-key-20150401'
   UserName = "monuser"
}
}
```