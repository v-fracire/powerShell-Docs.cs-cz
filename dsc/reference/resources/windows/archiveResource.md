---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC Archive
ms.openlocfilehash: d5ccd242d000a0907c6768f30923764be6bf20a3
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048141"
---
# <a name="dsc-archive-resource"></a>Prostředek DSC Archive

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Prostředek Archive ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus k rozbalení archivu (ZIP) soubory do konkrétní cesty.

## <a name="syntax"></a>Syntaxe
```MOF
Archive [string] #ResourceName
{
    Destination = [string]
    Path = [string]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Force = [bool] ]
    [ Validate = [bool] ]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Cíl| Určuje umístění, ve které chcete zajistit, aby že extrahování obsahu archivu.|
| Cesta| Určuje zdrojovou cestu souboru archivu.|
| __Kontrolní součet__| Definuje typ, který má použít při určování, zda dva soubory jsou stejné. Pokud __kontrolního součtu__ není zadán, pouze název souboru nebo složky se používá pro porovnání. Platné hodnoty jsou: SHA-1, SHA-256, SHA-512, datum vytvoření, modifiedDate, none (výchozí). Pokud zadáte __kontrolního součtu__ bez __ověřit__, konfigurace se nezdaří.|
| Zkontrolujte| Určuje, jestli se má zkontrolovat, zda obsah archivu existuje na __cílové__. Tuto vlastnost nastavte na __k dispozici__ zajistit obsah neexistuje. Nastavte ho na __chybí__ zajistit ještě neexistují. Výchozí hodnota je __k dispozici__.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud první je ID bloku skriptu konfigurace prostředků, kterou chcete spustit ResourceName a její typ je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
| Ověření| Vlastnost kontrolní součet se používá k určení, pokud archiv odpovídá podpisu. Pokud chcete zadat kontrolního součtu bez ověřením, konfigurace se nezdaří. Pokud chcete zadat ověřit bez kontrolního součtu, se standardně používá kontrolního součtu SHA-256.|
| Force| Určité operace se soubory (například soubor přepsání nebo odstranění adresáře, který není prázdný) dojde chybě. Pomocí vlastnosti vynucení přepsání tyto chyby. Výchozí hodnota je False.|

## <a name="example"></a>Příklad

Následující příklad ukazuje, jak použít prostředek Archive zajistíte, že obsah souboru archivu, s názvem Test.zip existují a jsou extrahovány na určitého cíle.

```
Archive ArchiveExample {
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Path = "C:\Users\Public\Documents\Test.zip"
    Destination = "C:\Users\Public\Documents\ExtractionPath"
}
```