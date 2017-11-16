---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC archivu"
ms.openlocfilehash: 035f7cc1b7f21f7a0df2d72db0ba83bc0688356c
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-archive-resource"></a>Prostředek DSC archivu

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Archiv prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus rozbalte souborech archivu (.zip) na konkrétní cesty.

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
| Cíl| Určuje umístění, kam chcete zajistit, aby že se extrahují obsah archivu.| 
| Cesta| Určuje zdroj cestu k souboru archivu.| 
| __Kontrolní součet__| Definuje typ, který má použít při určování, zda dva soubory jsou stejné. Pokud __kontrolního součtu__ není zadán, pro porovnání se používá pouze název souboru nebo adresáře. Platné hodnoty patří: SHA-1, SHA-256, SHA-512, datum vytvoření, modifiedDate, none (výchozí). Pokud zadáte __kontrolního součtu__ bez __ověřením__, konfigurace se nezdaří.| 
| Ujistěte se| Určuje, jestli se má zkontrolovat, zda existuje obsah archivu v __cílový__. Tuto vlastnost nastavit na __přítomen__ zajistit obsah neexistuje. Nastavte ji na __chybí__ zajistit, že nejsou k dispozici. Výchozí hodnota je __přítomen__.| 
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud ID bloku skriptu konfigurace prostředků, který chcete spustit nejprve je ResourceName a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.| 
| Ověření| Vlastnost kontrolního součtu se používá k určení, jestli odpovídá archivu podpis. Pokud zadáte kontrolního součtu bez ověřením, konfigurace se nezdaří. Pokud zadáte ověřit bez kontrolního součtu, použije se ve výchozím nastavení kontrolního součtu SHA-256.| 
| Force| Některé operace souboru (například přepsání souboru nebo odstranění adresáře, který není prázdný) bude výsledkem chyba. Pomocí vlastnosti Vynucené přepsání takové chyby. Výchozí hodnota je False.| 

## <a name="example"></a>Příklad

Následující příklad ukazuje, jak používat prostředek archivu zajistit, že obsah souboru archivu názvem Test.zip neexistuje a extrahují na daný cíl.

```
Archive ArchiveExample {
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Path = "C:\Users\Public\Documents\Test.zip"
    Destination = "C:\Users\Public\Documents\ExtractionPath"
} 
```

