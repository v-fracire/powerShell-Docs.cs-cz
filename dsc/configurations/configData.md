---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Použití konfiguračních dat
ms.openlocfilehash: f2d25b9ced805fb4c91378ebfe840104eb6ce52a
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403694"
---
# <a name="using-configuration-data-in-dsc"></a>Použití konfiguračních dat v DSC

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Pomocí předdefinovaných DSC **ConfigurationData** parametr, můžete definovat data, která je možné v rámci konfigurace.
To umožňuje vytvoření jedné konfigurace, který lze použít pro více uzlů nebo pro různá prostředí.
Například pokud vyvíjíte aplikaci, můžete použít jednu konfiguraci pro vývoj a provoz prostředí a konfigurační data můžete zadat data pro každé prostředí.

Toto téma popisuje strukturu **ConfigurationData** zatřiďovací tabulku.
Příklady toho, jak použít konfigurační data, najdete v článku [oddělení dat konfigurace a prostředí](separatingEnvData.md).

## <a name="the-configurationdata-common-parameter"></a>Společný parametr jsou konfigurační data

Konfigurace DSC používá společný parametr **ConfigurationData**, zadejte při kompilaci konfigurace.
Informace o kompilaci konfigurace najdete v tématu [konfigurací DSC](configurations.md).

**ConfigurationData** parametr je zatřiďovací tabulku, kterou musí mít alespoň jeden klíč s názvem **AllNodes**.
Také může mít jeden nebo více klíčů.

> [!NOTE]
> V příkladech v tomto tématu se používá jeden další klíč (jiné než pojmenované **AllNodes** klíč) s názvem `NonNodeData`, ale může obsahovat libovolný počet dalších klíčů a pojmenujte je cokoliv, co chcete.

```powershell
$MyData =
@{
    AllNodes = @()
    NonNodeData = ""
}
```

Hodnota **AllNodes** klíč je pole. Každý prvek toto pole je také zatřiďovací tabulku, kterou musí mít alespoň jeden klíč s názvem **NodeName**:

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

Vlastnost použít pro všechny uzly, můžete vytvořit člena **AllNodes** pole, které má **NodeName** z `*`.
Například, aby každý uzel `LogPath` vlastnost, můžete to udělat:

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

Jedná se o ekvivalent přidávání vlastnost s názvem `LogPath` s hodnotou `"C:\Logs"` ke každé z jiných bloků (`VM-1`, `VM-2`, a `VM-3`).

## <a name="defining-the-configurationdata-hashtable"></a>Definování zatřiďovací tabulky jsou konfigurační data

Můžete definovat **ConfigurationData** buď jako proměnné v rámci souboru skriptu jako konfigurace (podobně jako v našich příkladech předchozí) nebo v samostatném `.psd1` souboru.
Chcete-li definovat **ConfigurationData** v `.psd1` soubor, vytvořit soubor, který obsahuje pouze zatřiďovací tabulky, který představuje konfigurační data.

Například můžete vytvořit soubor s názvem `MyData.psd1` s následujícím obsahem:

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

## <a name="compiling-a-configuration-with-configuration-data"></a>Kompilace konfigurace s konfiguračními daty

Kompilace konfigurace, pro kterou jste definovali konfigurační data, předávat konfigurační data jako hodnotu **ConfigurationData** parametru.

Tím se vytvoří pro každou položku v souboru MOF **AllNodes** pole.
Každý soubor MOF budou mít názvy `NodeName` vlastnost odpovídající položku pole.

Například pokud definujete konfigurační data stejně jako v `MyData.psd1` soubor výše, kompilaci konfigurace byste vytvořili oba `VM-1.mof` a `VM-2.mof` soubory.

### <a name="compiling-a-configuration-with-configuration-data-using-a-variable"></a>Kompilace konfigurace s konfiguračními daty pomocí proměnné

Použití konfiguračních dat, která je definována jako proměnné ve stejném `.ps1` soubor jako konfiguraci, předejte název proměnné jako hodnotu **ConfigurationData** parametr při kompilaci konfigurace:

```powershell
MyDscConfiguration -ConfigurationData $MyData
```

### <a name="compiling-a-configuration-with-configuration-data-using-a-data-file"></a>Kompilace konfigurace s konfiguračními daty pomocí datového souboru

Pokud chcete použít konfigurační data, která je definována v souboru .psd1, předáte cestu a název tohoto souboru jako hodnotu **ConfigurationData** parametr při kompilaci konfigurace:

```powershell
MyDscConfiguration -ConfigurationData .\MyData.psd1
```

## <a name="using-configurationdata-variables-in-a-configuration"></a>Použití proměnných jsou konfigurační data v konfiguraci

DSC poskytuje následující speciální proměnné, které lze použít v konfigurační skript:

- **$AllNodes** odkazuje na celou kolekci uzlů, které jsou definovány v **ConfigurationData**. Můžete filtrovat **AllNodes** kolekce s použitím **. Metody WHERE()** a **. Konstrukce ForEach()**.
- **ConfigurationData** odkazuje na celý zatřiďovací tabulky, který je předán jako parametr při kompilaci konfigurace.
- **MyTypeName** obsahuje [konfigurace](configurations.md) název proměnné je používán. Například v konfiguraci `MyDscConfiguration`, `$MyTypeName` bude mít hodnotu `MyDscConfiguration`.
- **Uzel** odkazuje na příslušnou položku v **AllNodes** kolekce po filtrován použitím **. Metody WHERE()** nebo **. Konstrukce ForEach()**.
  - Další informace o těchto metodách v [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)

## <a name="using-non-node-data"></a>Použití dat mimo uzel

Jak jsme viděli v předchozích příkladech **ConfigurationData** zatřiďovací tabulka může mít jeden nebo více klíčů kromě požadované **AllNodes** klíč.
V příkladech v tomto tématu jsme použít jenom jeden další uzel a s názvem ho `NonNodeData`.
Však můžete definovat libovolný počet dalších klíčů a pojmenujte je všechno, co chcete.

Příklad použití data mimo uzel, naleznete v tématu [oddělení dat konfigurace a prostředí](separatingEnvData.md).

## <a name="see-also"></a>Viz také

- [Možnosti přihlašovacích údajů v konfiguračních datech](configDataCredentials.md)
- [Konfigurace DSC](configurations.md)