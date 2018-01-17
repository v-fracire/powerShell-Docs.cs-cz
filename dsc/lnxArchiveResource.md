---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC pro Linux nxArchive prostředků"
ms.openlocfilehash: e91ef5bcf4bdf413844c23d1d3bd823a535b536f
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-for-linux-nxarchive-resource"></a>DSC pro Linux nxArchive prostředků

**NxArchive** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus rozbalte soubory archivu (.tar, .zip) v určité cesty na uzlu Linux.

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
| SourcePath| Určuje zdroj cestu k souboru archivu. Měl by být .tar, .zip, nebo. tar.gz souboru. | 
| DestinationPath| Určuje umístění, kam chcete zajistit, aby že se extrahují obsah archivu.| 
| Kontrolní součet| Definuje typ, který má použít při určování, zda byly aktualizovány archivu zdroje. Hodnoty: "ctime", "mtime" nebo "md5". Výchozí hodnota je "md5".| 
| Force| Některé operace souboru (například přepsání souboru nebo odstranění adresáře, který není prázdný) bude výsledkem chyba. Pomocí **Force** vlastnost má přednost před takové chyby. Výchozí hodnota je **$false**.| 
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.| 
| Ujistěte se| Určuje, jestli se má zkontrolovat, zda existuje obsah archivu v **cílový**. Nastavením této vlastnosti "Přítomen" Ujistěte se, že existuje obsah. Nastavte ji na "Chybí" Ujistěte se, že neexistují. Výchozí hodnota je "Dispozici".| 

## <a name="example"></a>Příklad

Následující příklad ukazuje, jak používat **nxArchive** prostředek se má zajistit, aby obsah souboru archivu volána `website.tar` existují a jsou extrahovány na daný cíl.

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

