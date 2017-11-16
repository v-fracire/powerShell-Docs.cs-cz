---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC pro Linux nxEnvironment prostředků"
ms.openlocfilehash: 3d09c9642f35627e939460c9c13dfe48d14030c3
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-for-linux-nxenvironment-resource"></a>DSC pro Linux nxEnvironment prostředků

**NxEnvironment** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro ke správě seznamu proměnných prostředí systému Linux uzlu.

## <a name="syntax"></a>Syntaxe

```
nxEnvironment <string> #ResourceName
{
    Name = <string>
    [ Value = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Path = <bool> }
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost |  Popis | 
|---|---|
| Název| Určuje název proměnné prostředí, pro které chcete zajistit určitý stav.| 
| Hodnota| Hodnota pro přiřazení k proměnné prostředí.| 
| Ujistěte se| Určuje, jestli se má zkontrolovat, zda existuje proměnnou. Nastavením této vlastnosti "Přítomen" Ujistěte se, že existuje proměnnou. Nastavte ji na "Chybí" Ujistěte se, že proměnná neexistuje. Výchozí hodnota je "Dispozici".| 
| Cesta| Definuje proměnnou prostředí, který je konfigurován. Tuto vlastnost nastavit na **$true** -li proměnná **cesta** proměnné; v opačném nastavte ji na **$false**. Výchozí hodnota je **$false**. Pokud je proměnná konfigurován **cesta** proměnné, hodnota poskytnutá prostřednictvím **hodnotu** vlastnost bude připojeno k stávající hodnotu.| 
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.| 

## <a name="additional-information"></a>Další informace

* Pokud **cesta** chybí nebo je nastavena na **$false**, proměnné prostředí se spravují v `/etc/environment`. Programy nebo skripty může vyžadovat konfiguraci ke zdroji `/etc/environment` souboru pro přístup k proměnným spravovaném prostředí.
* Pokud **cesta** je nastaven na **$true**, proměnná prostředí je spravován v souboru `/etc/profile.d/DSCenvironment.sh`. Tento soubor bude vytvořen, pokud neexistuje. Pokud **zajistěte, aby** je nastaven na "Chybí" a **cesta** je nastaven na **$true**, existující proměnné prostředí se jenom odeberou z `/etc/profile.d/DSCenvironment.sh` a nikoli z jiné soubory.

## <a name="example"></a>Příklad

Následující příklad ukazuje, jak používat **nxEnvironment** prostředků zajistit, aby **TestEnvironmentVariable** je k dispozici a má hodnotu "Test-hodnota". Pokud **TestEnvironmentVariable** nejsou k dispozici, bude vytvořen.

```
Import-DSCResource -Module nx 


nxEnvironment EnvironmentExample
{
    Ensure = “Present”
    Name = “TestEnvironmentVariable”
    Value = “TestValue”
}
```


