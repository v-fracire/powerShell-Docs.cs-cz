---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxArchive
ms.openlocfilehash: 800954478f149e29c22d1a88304c3be9950f109a
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048155"
---
# <a name="dsc-for-linux-nxarchive-resource"></a>DSC pro Linux prostředek nxArchive

**NxArchive** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus pro rozbalení souborech archivu (.tar, .zip) v určité cestě na uzlu systému Linux.

## <a name="syntax"></a>Syntaxe

```
nxArchive <string> #ResourceName
{
    SourcePath = <string>
    DestinationPath = <string>
    [ Checksum = <string> { ctime | mtime | md5 }  ]
    [ Force = <bool> ]
    [ DependsOn = <string[]> ]
    [ Ensure = <string> { Absent | Present }  ]
}
```

## <a name="properties"></a>Properties

|  Vlastnost |  Popis |
|---|---|
| SourcePath| Určuje zdrojovou cestu souboru archivu. Mělo by se jednat .tar ZIP, nebo. tar.gz souboru. |
| DestinationPath| Určuje umístění, ve které chcete zajistit, aby že extrahování obsahu archivu.|
| Kontrolní součet| Definuje typ, který má použít při určování, zda byl aktualizován archivu zdroje. Hodnoty jsou: "ctime", "mtime" nebo "md5". Výchozí hodnota je "md5".|
| Force| Určité operace se soubory (například soubor přepsání nebo odstranění adresáře, který není prázdný) dojde chybě. Použití **platnost** vlastnost potlačuje tyto chyby. Výchozí hodnota je **$false**.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.|
| Zkontrolujte| Určuje, jestli se má zkontrolovat, zda obsah archivu existuje na **cílové**. Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že existuje obsah. Nastavte ho na "Chybí" Ujistěte se, že neexistují. Výchozí hodnota je "K dispozici".|

## <a name="example"></a>Příklad

Následující příklad ukazuje způsob použití **nxArchive** prostředků k zajištění, že obsah souboru archivu volat `website.tar` existují a jsou extrahovány na určitého cíle.

```
Import-DSCResource -Module nx

nxFile SyncArchiveFromWeb
{
   Ensure = "Present"
   SourcePath = “http://release.contoso.com/releases/website.tar”
   DestinationPath = "/usr/release/staging/website.tar"
   Type = "File"
   Checksum = “mtime”
}

nxArchive SyncWebDir
{
   SourcePath = “/usr/release/staging/website.tar”
   DestinationPath = “/usr/local/apache2/htdocs/”
   Force = $false
   DependsOn = "[nxFile]SyncArchiveFromWeb"
}
```