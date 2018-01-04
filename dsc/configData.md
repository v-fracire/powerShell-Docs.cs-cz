---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Pomocí konfigurační data"
ms.openlocfilehash: 60c6c2d5694a03275e1a08522bdcf4b1bc5bb068
ms.sourcegitcommit: 60f06a06c2fce63024f3f4cbd7657b1dfe7fcb1a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/03/2018
---
# <a name="using-configuration-data-in-dsc"></a>Pomocí konfigurační data v DSC

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Pomocí předdefinovaných DSC **ConfigurationData** parametr, můžete definovat data, která lze použít v konfiguraci. To umožňuje vytvoření jedné konfigurace, které lze použít pro více uzly nebo v různých prostředích. Například pokud vyvíjíte aplikaci, můžete použít jednu konfiguraci pro vývoj a produkční prostředí a konfigurační data použijte k určení dat pro každé prostředí.

Toto téma popisuje strukturu **ConfigurationData** zatřiďovací tabulky. Příklady použití konfiguračních dat najdete v tématu [oddělení dat konfigurace a prostředí](separatingEnvData.md).

## <a name="the-configurationdata-common-parameter"></a>Společný parametr ConfigurationData

Konfigurace DSC trvá společný parametr **ConfigurationData**, zda jste zadali při kompilaci konfigurace. Informace o kompilování konfigurace najdete v tématu [konfigurace DSC](configurations.md).

**ConfigurationData** parametr je hasthtable, kterou musí mít alespoň jeden klíč s názvem **AllNodes**. Může také obsahovat jeden či více klíčů.

>**Poznámka:** v příkladech v tomto tématu použijte jeden další klíč (než pojmenované **AllNodes** klíč) s názvem `NonNodeData`, ale může obsahovat libovolný počet dalších klíčů a název je všechno.

```powershell
$MyData = 
@{
    AllNodes = @()
    NonNodeData = ""   
}
```

Hodnota **AllNodes** klíč je pole. Každý prvek toto pole je také zatřiďovací tabulka, která musí mít alespoň jeden klíč s názvem **NodeName**:

```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName = "VM-1"
        },

 
        @{
            NodeName = "VM-2"
        },

 
        @{
            NodeName = "VM-3"
        }
    );

    NonNodeData = ""   
}
```

Můžete přidat další klíče pro každou zatřiďovací tabulku:

```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName = "VM-1"
            Role     = "WebServer"
        },

 
        @{
            NodeName = "VM-2"
            Role     = "SQLServer"
        },

 
        @{
            NodeName = "VM-3"
            Role     = "WebServer"
        }
    );

    NonNodeData = ""   
}
```

Použít vlastnosti na všech uzlech, můžete vytvořit členem **AllNodes** pole, které má **NodeName** z `*`. Například pro poskytnutí každý uzel `LogPath` vlastnost, můžete to udělat toto:

```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName     = "*"
            LogPath      = "C:\Logs"
        },

 
        @{
            NodeName     = "VM-1"
            Role         = "WebServer"
            SiteContents = "C:\Site1"
            SiteName     = "Website1"
        },

 
        @{
            NodeName     = "VM-2"
            Role         = "SQLServer"
        },

 
        @{
            NodeName     = "VM-3"
            Role         = "WebServer"
            SiteContents = "C:\Site2"
            SiteName     = "Website3"
        }
    );
}
```

Jedná se o ekvivalent přidávání vlastnost s názvem `LogPath` s hodnotou `"C:\Logs"` všechny ostatní bloky (`VM-1`, `VM-2`, a `VM-3`).

## <a name="defining-the-configurationdata-hashtable"></a>Definování ConfigurationData zatřiďovací tabulky

Můžete definovat **ConfigurationData** buď jako proměnné v souboru skriptu jako konfigurace (jako v předchozí příklady) nebo v samostatném `.psd1` souboru. Chcete-li definovat **ConfigurationData** v `.psd1` souboru, vytvořte soubor, který obsahuje pouze zatřiďovací tabulky, který představuje konfigurační data.

Například můžete vytvořit soubor s názvem `MyData.psd1` s tímto obsahem:

```powershell
@{
    AllNodes =
    @(
        @{
            NodeName    = 'VM-1'
            FeatureName = 'Web-Server'
        },

        @{
            NodeName    = 'VM-2'
            FeatureName = 'Hyper-V'
        }
    )
}
```

## <a name="compiling-a-configuration-with-configuration-data"></a>Kompilování konfigurace s konfigurační data

Kompilace konfigurace, pro který jste definovali konfigurační data, předáte konfigurační data jako hodnotu **ConfigurationData** parametr.

Tím se vytvoří pro každou položku v souboru MOF **AllNodes** pole.
Každý soubor MOF budou mít názvy `NodeName` vlastnost odpovídající položky pole.

Například pokud definujete konfigurační data jako v `MyData.psd1` souboru výše, kompilace konfigurace by vytvořit i `VM-1.mof` a `VM-2.mof` soubory.

### <a name="compiling-a-configuration-with-configuration-data-using-a-variable"></a>Kompilování konfiguraci pomocí konfiguračních dat pomocí proměnné

Použít konfigurační data, která je definována jako proměnné ve stejné `.ps1` soubor jako konfiguraci, předáte název proměnné jako hodnotu **ConfigurationData** parametr při kompilaci konfigurace:

```powershell
MyDscConfiguration -ConfigurationData $MyData
```

### <a name="compiling-a-configuration-with-configuration-data-using-a-data-file"></a>Kompilování konfiguraci pomocí konfiguračních dat pomocí a datový soubor.

Pokud chcete používat konfigurační data, která je definována v souboru .psd1, předáte cesta a název souboru jako hodnotu **ConfigurationData** parametr při kompilaci konfigurace:

```powershell
MyDscConfiguration -ConfigurationData .\MyData.psd1
```

## <a name="using-configurationdata-variables-in-a-configuration"></a>Použití proměnných ConfigurationData v konfiguraci

DSC poskytuje tři speciální proměnné, které lze použít v konfigurační skript: **$AllNodes**, **$Node**, a **$ConfigurationData**.

- **$AllNodes** odkazuje na celou kolekci uzlů, které jsou definované v **ConfigurationData**. Můžete filtrovat **AllNodes** kolekce pomocí **. WHERE()** a **. ForEach()**.
- **Uzel** odkazuje na konkrétní položky v **AllNodes** kolekci po je filtrován pomocí **. WHERE()** nebo **. ForEach()**.
- **ConfigurationData** odkazuje na tabulku celou hodnotu hash, který je předán jako parametr při kompilaci konfigurace.

## <a name="using-non-node-data"></a>Pomocí data bez uzlu

Jak jsme viděli v předchozích příkladech **ConfigurationData** zatřiďovací tabulka může mít jeden či více klíčů kromě požadované **AllNodes** klíč.
V příkladech v tomto tématu jsme používá jenom jeden další uzel a s názvem ho `NonNodeData`. Však můžete definovat libovolný počet dalších klíčů a název je všechno, co chcete.

Příklad použití dat na jiný uzel, naleznete v části [oddělení dat konfigurace a prostředí](separatingEnvData.md).

## <a name="see-also"></a>Viz také
- [Možnosti přihlašovací údaje v konfiguračních dat](configDataCredentials.md)
- [Konfigurace DSC](configurations.md)

