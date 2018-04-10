---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Prostředek DSC souboru
ms.openlocfilehash: 7964eabe5f4585600ae80f3e5ff7439c0d954769
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-file-resource"></a>Prostředek DSC souboru

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Prostředek souboru v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě souborů a složek na cílovém uzlu.

>**Poznámka:** Pokud **MatchSource** je nastavena na **$false** (což je výchozí hodnota), obsah, který se má zkopírovat jsou uložené v mezipaměti při prvním se konfigurace použije.
>Konfigurace dalších aplikací nebudou kontrolovat aktualizované soubory nebo složky v cestě určeného **SourcePath**. Pokud chcete vyhledat aktualizace na soubory nebo složky v **SourcePath** pokaždé, když se konfigurace použije, nastavte **MatchSource** k **$true**.

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
| DestinationPath| Určuje umístění, kde chcete zajistit stav pro soubor nebo adresář.|
| Atributy| Určuje požadovaný stav atributy pro cílový soubor nebo adresář.|
| Kontrolní součet| Označuje typ kontrolního součtu použít při určování, zda dva soubory jsou stejné. Pokud __kontrolního součtu__ není zadán, pro porovnání se používá pouze název souboru nebo adresáře. Platné hodnoty patří: SHA-1, SHA-256, SHA-512, datum vytvoření, modifiedDate.|
| Obsah| Určuje obsah souboru, například konkrétní řetězec.|
| přihlašovací údaje| Označuje přihlašovací údaje, které jsou požadovány pro přístup k prostředkům, jako je například zdrojové soubory, pokud je nutný takový přístup.|
| Ujistěte se| Určuje, jestli existuje soubor nebo adresář. Nastavením této vlastnosti "Chybí" zajistit, že soubor nebo adresář neexistuje. Nastavte ji na "Přítomen" zajistit, že soubor nebo adresář neexistuje. Výchozí hodnota je "Dispozici".|
| Force| Některé operace souboru (například přepsání souboru nebo odstranění adresáře, který není prázdný) bude výsledkem chyba. Pomocí vlastnosti Vynucené přepsání takové chyby. Výchozí hodnota je __$false__.|
| Recurse| Uvádí, jestli jsou zahrnuté podadresářů. Tuto vlastnost nastavit na __$true__ k označení, že chcete podadresáře, které mají být zahrnuty. Výchozí hodnota je __$false__. **Poznámka:**: Tato vlastnost je platná pouze pokud je vlastnost Typ nastavena na adresář.|
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
| SourcePath| Určuje cestu, ze které kopírování prostředků souboru nebo složky.|
| Typ| Určuje, zda je prostředek konfigurován adresář nebo soubor. Nastavením této vlastnosti "Adresář" označuje, že prostředek adresáře. Nastavte ji na File (soubor) znamenat, že prostředek soubor. Výchozí hodnota je "Soubor".|
| MatchSource| Pokud se nastaví na výchozí hodnotu z __$false__, pak všechny soubory ve zdroji (například, soubory A, B a C) budou přidány do cílového umístění poprvé se konfigurace použije. Pokud nový soubor (D) je přidán ke zdroji, nebude přidáno do cílového umístění, i v případě, že konfigurace se použije znovu později. Pokud je hodnota __$true__, potom pokaždé, když se konfigurace použije, do cílového umístění jsou přidávány nové soubory, které následně nalezena ve zdroji (například soubor D v tomto příkladu). Výchozí hodnota je **$false**.|

## <a name="example"></a>Příklad

Následující příklad ukazuje, jak použít soubor prostředků zajistit, aby adresáře s cestou `C:\Users\Public\Documents\DSCDemo\DemoSource` ve zdroji (například server "vyžádání") počítače nachází také (spolu s všechny podadresáře) na cílovém uzlu. Také potvrzující zpráva, zapíše do protokolu, po dokončení a obsahuje příkaz k zajištění, že operaci kontrola soubor spouští před operaci protokolování.

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