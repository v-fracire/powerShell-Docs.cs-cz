---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC File
ms.openlocfilehash: e5f7a91e5f19c8c7bbada090804d8f29a7cfedd5
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048186"
---
# <a name="dsc-file-resource"></a>Prostředek DSC File

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Prostředek File ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě souborů a složek na cílový uzel.

>**Poznámka:** Pokud **MatchSource** je nastavena na **$false** (což je výchozí hodnota), obsahu, které se mají zkopírovat jsou uložené v mezipaměti při prvním tato konfigurace používá.
>Následné žádosti z konfigurace nebude kontrolovat aktualizované soubory nebo složky v cestě určené **SourcePath**. Pokud chcete vyhledat aktualizace pro soubory a složky v **SourcePath** pokaždé, když se tato konfigurace používá, nastavte **MatchSource** k **$true**.

## <a name="syntax"></a>Syntaxe
```
File [string] #ResourceName
{
    DestinationPath = [string]
    [ Attributes = [string[]] { Archive | Hidden | ReadOnly | System }]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ Contents = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Force = [bool] ]
    [ Recurse = [bool] ]
    [ DependsOn = [string[]] ]
    [ SourcePath = [string] ]
    [ Type = [string] { Directory | File } ]
    [ MatchSource = [bool] ]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| DestinationPath| Označuje umístění, kam chcete zajistit stavu pro soubor nebo adresář.|
| Atributy| Určuje požadovaný stav atributy pro cílový soubor nebo adresář.|
| Kontrolní součet| Určuje typ kontrolního součtu pro zjištění, zda dva soubory jsou stejné. Pokud __kontrolního součtu__ není zadán, pouze název souboru nebo složky se používá pro porovnání. Platné hodnoty jsou: SHA-1, SHA-256, SHA-512, datum vytvoření, modifiedDate.|
| Obsah| Určuje obsah souboru, jako je například konkrétní řetězec.|
| Přihlašovací údaje| Určuje přihlašovací údaje, které jsou požadovány pro přístup k prostředkům, jako je například zdrojové soubory, pokud takový přístup je povinný.|
| Zkontrolujte| Určuje, jestli existuje soubor nebo adresář. Nastavte tuto vlastnost na "Chybí" Ujistěte se, že soubor nebo adresář neexistuje. Nastavte ho na "Obsahuje" Ujistěte se, že soubor nebo adresář neexistuje. Výchozí hodnota je "K dispozici".|
| Force| Určité operace se soubory (například soubor přepsání nebo odstranění adresáře, který není prázdný) dojde chybě. Pomocí vlastnosti vynucení přepsání tyto chyby. Výchozí hodnota je __$false__.|
| Recurse| Uvádí, jestli jsou zahrnuté podadresářů. Tuto vlastnost nastavte na __$true__ k označení, že chcete, aby podadresářů, které mají být zahrnuty. Výchozí hodnota je __$false__. **Poznámka:**: Tato vlastnost je platná pouze v případě vlastnost Type je nastavená na adresář.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
| SourcePath| Označuje cestu, ze kterého chcete kopírovat zdroje souboru nebo složky.|
| Type| Určuje, zda je nakonfigurován prostředek je adresář nebo soubor. Nastavte tuto vlastnost na "Directory" k označení, že je prostředek adresáře. Nastavte ho na "File" označuje, že soubor prostředku. Výchozí hodnota je "File".|
| MatchSource| Pokud nastavena na výchozí hodnotu __$false__, pak všechny soubory ve zdroji (například soubory A, B a C) budou přidány do cílového umístění poprvé, tato konfigurace používá. Pokud nový soubor (D) je přidán ke zdroji, nebude přidána do umístění, i když tato konfigurace používá znovu později. Pokud je hodnota __$true__, pak pokaždé, když tato konfigurace používá, do cíle jsou přidávány nové soubory, které jsou následně nalezena ve zdroji (například D soubor v tomto příkladu). Výchozí hodnota je **$false**.|

## <a name="example"></a>Příklad

Následující příklad ukazuje způsob použití souborů prostředků a zkontrolujte, že adresář s cestou `C:\Users\Public\Documents\DSCDemo\DemoSource` zdroje počítače (třeba server "o přijetí změn") je také k dispozici (spolu s všechny podadresáře) na cílovém uzlu. Také zapíše potvrzovací zprávu do protokolu po dokončení a obsahuje prohlášení, ujistěte se, že operace kontroly souborů předchází operace protokolování.

```powershell
Configuration FileResourceDemo
{
    Node "localhost"
    {
        File DirectoryCopy
        {
            Ensure = "Present"  # You can also set Ensure to "Absent"
            Type = "Directory" # Default is "File".
            Recurse = $true # Ensure presence of subdirectories, too
            SourcePath = "C:\Users\Public\Documents\DSCDemo\DemoSource"
            DestinationPath = "C:\Users\Public\Documents\DSCDemo\DemoDestination"
        }

        Log AfterDirectoryCopy
        {
            # The message below gets written to the Microsoft-Windows-Desired State Configuration/Analytic log
            Message = "Finished running the file resource with ID DirectoryCopy"
            DependsOn = "[File]DirectoryCopy" # This means run "DirectoryCopy" first.
        }
    }
}
```