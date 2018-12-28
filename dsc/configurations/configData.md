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
# <a name="using-configuration-data-in-dsc"></a><span data-ttu-id="5fdff-103">Použití konfiguračních dat v DSC</span><span class="sxs-lookup"><span data-stu-id="5fdff-103">Using configuration data in DSC</span></span>

> <span data-ttu-id="5fdff-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="5fdff-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="5fdff-105">Pomocí předdefinovaných DSC **ConfigurationData** parametr, můžete definovat data, která je možné v rámci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="5fdff-105">By using the built-in DSC **ConfigurationData** parameter, you can define data that can be used within a configuration.</span></span>
<span data-ttu-id="5fdff-106">To umožňuje vytvoření jedné konfigurace, který lze použít pro více uzlů nebo pro různá prostředí.</span><span class="sxs-lookup"><span data-stu-id="5fdff-106">This allows you to create a single configuration that can be used for multiple nodes or for different environments.</span></span>
<span data-ttu-id="5fdff-107">Například pokud vyvíjíte aplikaci, můžete použít jednu konfiguraci pro vývoj a provoz prostředí a konfigurační data můžete zadat data pro každé prostředí.</span><span class="sxs-lookup"><span data-stu-id="5fdff-107">For example, if you are developing an application, you can use one configuration for both development and production environments, and use configuration data to specify data for each environment.</span></span>

<span data-ttu-id="5fdff-108">Toto téma popisuje strukturu **ConfigurationData** zatřiďovací tabulku.</span><span class="sxs-lookup"><span data-stu-id="5fdff-108">This topic describes the structure of the **ConfigurationData** hashtable.</span></span>
<span data-ttu-id="5fdff-109">Příklady toho, jak použít konfigurační data, najdete v článku [oddělení dat konfigurace a prostředí](separatingEnvData.md).</span><span class="sxs-lookup"><span data-stu-id="5fdff-109">For examples of how to use configuration data, see [Separating configuration and environment data](separatingEnvData.md).</span></span>

## <a name="the-configurationdata-common-parameter"></a><span data-ttu-id="5fdff-110">Společný parametr jsou konfigurační data</span><span class="sxs-lookup"><span data-stu-id="5fdff-110">The ConfigurationData common parameter</span></span>

<span data-ttu-id="5fdff-111">Konfigurace DSC používá společný parametr **ConfigurationData**, zadejte při kompilaci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="5fdff-111">A DSC configuration takes a common parameter, **ConfigurationData**, that you specify when you compile the configuration.</span></span>
<span data-ttu-id="5fdff-112">Informace o kompilaci konfigurace najdete v tématu [konfigurací DSC](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="5fdff-112">For information about compiling configurations, see [DSC configurations](configurations.md).</span></span>

<span data-ttu-id="5fdff-113">**ConfigurationData** parametr je zatřiďovací tabulku, kterou musí mít alespoň jeden klíč s názvem **AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="5fdff-113">The **ConfigurationData** parameter is a hashtable that must have at least one key named **AllNodes**.</span></span>
<span data-ttu-id="5fdff-114">Také může mít jeden nebo více klíčů.</span><span class="sxs-lookup"><span data-stu-id="5fdff-114">It can also have one or more other keys.</span></span>

> [!NOTE]
> <span data-ttu-id="5fdff-115">V příkladech v tomto tématu se používá jeden další klíč (jiné než pojmenované **AllNodes** klíč) s názvem `NonNodeData`, ale může obsahovat libovolný počet dalších klíčů a pojmenujte je cokoliv, co chcete.</span><span class="sxs-lookup"><span data-stu-id="5fdff-115">The examples in this topic use a single additional key (other than the named **AllNodes** key) named `NonNodeData`, but you can include any number of additional keys, and name them whatever you want.</span></span>

```powershell
$MyData =
@{
    AllNodes = @()
    NonNodeData = ""
}
```

<span data-ttu-id="5fdff-116">Hodnota **AllNodes** klíč je pole.</span><span class="sxs-lookup"><span data-stu-id="5fdff-116">The value of the **AllNodes** key is an array.</span></span> <span data-ttu-id="5fdff-117">Každý prvek toto pole je také zatřiďovací tabulku, kterou musí mít alespoň jeden klíč s názvem **NodeName**:</span><span class="sxs-lookup"><span data-stu-id="5fdff-117">Each element of this array is also a hash table that must have at least one key named **NodeName**:</span></span>

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

<span data-ttu-id="5fdff-118">Můžete přidat další klíče pro každou zatřiďovací tabulku:</span><span class="sxs-lookup"><span data-stu-id="5fdff-118">You can add other keys to each hash table as well:</span></span>

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

<span data-ttu-id="5fdff-119">Vlastnost použít pro všechny uzly, můžete vytvořit člena **AllNodes** pole, které má **NodeName** z `*`.</span><span class="sxs-lookup"><span data-stu-id="5fdff-119">To apply a property to all nodes, you can create a member of the **AllNodes** array that has a **NodeName** of `*`.</span></span>
<span data-ttu-id="5fdff-120">Například, aby každý uzel `LogPath` vlastnost, můžete to udělat:</span><span class="sxs-lookup"><span data-stu-id="5fdff-120">For example, to give every node a `LogPath` property, you could do this:</span></span>

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

<span data-ttu-id="5fdff-121">Jedná se o ekvivalent přidávání vlastnost s názvem `LogPath` s hodnotou `"C:\Logs"` ke každé z jiných bloků (`VM-1`, `VM-2`, a `VM-3`).</span><span class="sxs-lookup"><span data-stu-id="5fdff-121">This is the equivalent of adding a property with a name of `LogPath` with a value of `"C:\Logs"` to each of the other blocks (`VM-1`, `VM-2`, and `VM-3`).</span></span>

## <a name="defining-the-configurationdata-hashtable"></a><span data-ttu-id="5fdff-122">Definování zatřiďovací tabulky jsou konfigurační data</span><span class="sxs-lookup"><span data-stu-id="5fdff-122">Defining the ConfigurationData hashtable</span></span>

<span data-ttu-id="5fdff-123">Můžete definovat **ConfigurationData** buď jako proměnné v rámci souboru skriptu jako konfigurace (podobně jako v našich příkladech předchozí) nebo v samostatném `.psd1` souboru.</span><span class="sxs-lookup"><span data-stu-id="5fdff-123">You can define **ConfigurationData** either as a variable within the same script file as a configuration (as in our previous examples) or in a separate `.psd1` file.</span></span>
<span data-ttu-id="5fdff-124">Chcete-li definovat **ConfigurationData** v `.psd1` soubor, vytvořit soubor, který obsahuje pouze zatřiďovací tabulky, který představuje konfigurační data.</span><span class="sxs-lookup"><span data-stu-id="5fdff-124">To define **ConfigurationData** in a `.psd1` file, create a file that contains only the hashtable that represents the configuration data.</span></span>

<span data-ttu-id="5fdff-125">Například můžete vytvořit soubor s názvem `MyData.psd1` s následujícím obsahem:</span><span class="sxs-lookup"><span data-stu-id="5fdff-125">For example, you could create a file named `MyData.psd1` with the following contents:</span></span>

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

## <a name="compiling-a-configuration-with-configuration-data"></a><span data-ttu-id="5fdff-126">Kompilace konfigurace s konfiguračními daty</span><span class="sxs-lookup"><span data-stu-id="5fdff-126">Compiling a configuration with configuration data</span></span>

<span data-ttu-id="5fdff-127">Kompilace konfigurace, pro kterou jste definovali konfigurační data, předávat konfigurační data jako hodnotu **ConfigurationData** parametru.</span><span class="sxs-lookup"><span data-stu-id="5fdff-127">To compile a configuration for which you have defined configuration data, you pass the configuration data as the value of the **ConfigurationData** parameter.</span></span>

<span data-ttu-id="5fdff-128">Tím se vytvoří pro každou položku v souboru MOF **AllNodes** pole.</span><span class="sxs-lookup"><span data-stu-id="5fdff-128">This will create a MOF file for each entry in the **AllNodes** array.</span></span>
<span data-ttu-id="5fdff-129">Každý soubor MOF budou mít názvy `NodeName` vlastnost odpovídající položku pole.</span><span class="sxs-lookup"><span data-stu-id="5fdff-129">Each MOF file will be named with the `NodeName` property of the corresponding array entry.</span></span>

<span data-ttu-id="5fdff-130">Například pokud definujete konfigurační data stejně jako v `MyData.psd1` soubor výše, kompilaci konfigurace byste vytvořili oba `VM-1.mof` a `VM-2.mof` soubory.</span><span class="sxs-lookup"><span data-stu-id="5fdff-130">For example, if you define configuration data as in the `MyData.psd1` file above, compiling a configuration would create both `VM-1.mof` and `VM-2.mof` files.</span></span>

### <a name="compiling-a-configuration-with-configuration-data-using-a-variable"></a><span data-ttu-id="5fdff-131">Kompilace konfigurace s konfiguračními daty pomocí proměnné</span><span class="sxs-lookup"><span data-stu-id="5fdff-131">Compiling a configuration with configuration data using a variable</span></span>

<span data-ttu-id="5fdff-132">Použití konfiguračních dat, která je definována jako proměnné ve stejném `.ps1` soubor jako konfiguraci, předejte název proměnné jako hodnotu **ConfigurationData** parametr při kompilaci konfigurace:</span><span class="sxs-lookup"><span data-stu-id="5fdff-132">To use configuration data that is defined as a variable in the same `.ps1` file as the configuration, you pass the variable name as the value of the **ConfigurationData** parameter when compiling the configuration:</span></span>

```powershell
MyDscConfiguration -ConfigurationData $MyData
```

### <a name="compiling-a-configuration-with-configuration-data-using-a-data-file"></a><span data-ttu-id="5fdff-133">Kompilace konfigurace s konfiguračními daty pomocí datového souboru</span><span class="sxs-lookup"><span data-stu-id="5fdff-133">Compiling a configuration with configuration data using a data file</span></span>

<span data-ttu-id="5fdff-134">Pokud chcete použít konfigurační data, která je definována v souboru .psd1, předáte cestu a název tohoto souboru jako hodnotu **ConfigurationData** parametr při kompilaci konfigurace:</span><span class="sxs-lookup"><span data-stu-id="5fdff-134">To use configuration data that is defined in a .psd1 file, you pass the path and name of that file as the value of the **ConfigurationData** parameter when compiling the configuration:</span></span>

```powershell
MyDscConfiguration -ConfigurationData .\MyData.psd1
```

## <a name="using-configurationdata-variables-in-a-configuration"></a><span data-ttu-id="5fdff-135">Použití proměnných jsou konfigurační data v konfiguraci</span><span class="sxs-lookup"><span data-stu-id="5fdff-135">Using ConfigurationData variables in a configuration</span></span>

<span data-ttu-id="5fdff-136">DSC poskytuje následující speciální proměnné, které lze použít v konfigurační skript:</span><span class="sxs-lookup"><span data-stu-id="5fdff-136">DSC provides the following special variables that can be used in a configuration script:</span></span>

- <span data-ttu-id="5fdff-137">**$AllNodes** odkazuje na celou kolekci uzlů, které jsou definovány v **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="5fdff-137">**$AllNodes** refers to the entire collection of nodes defined in **ConfigurationData**.</span></span> <span data-ttu-id="5fdff-138">Můžete filtrovat **AllNodes** kolekce s použitím **. Metody WHERE()** a **. Konstrukce ForEach()**.</span><span class="sxs-lookup"><span data-stu-id="5fdff-138">You can filter the **AllNodes** collection by using **.Where()** and **.ForEach()**.</span></span>
- <span data-ttu-id="5fdff-139">**ConfigurationData** odkazuje na celý zatřiďovací tabulky, který je předán jako parametr při kompilaci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="5fdff-139">**ConfigurationData** refers to the entire hash table that is passed as the parameter when compiling a configuration.</span></span>
- <span data-ttu-id="5fdff-140">**MyTypeName** obsahuje [konfigurace](configurations.md) název proměnné je používán.</span><span class="sxs-lookup"><span data-stu-id="5fdff-140">**MyTypeName** contains the [configuration](configurations.md) name the variable is used in.</span></span> <span data-ttu-id="5fdff-141">Například v konfiguraci `MyDscConfiguration`, `$MyTypeName` bude mít hodnotu `MyDscConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="5fdff-141">For example, in the configuration `MyDscConfiguration`, the `$MyTypeName` will have a value of `MyDscConfiguration`.</span></span>
- <span data-ttu-id="5fdff-142">**Uzel** odkazuje na příslušnou položku v **AllNodes** kolekce po filtrován použitím **. Metody WHERE()** nebo **. Konstrukce ForEach()**.</span><span class="sxs-lookup"><span data-stu-id="5fdff-142">**Node** refers to a particular entry in the **AllNodes** collection after it is filtered by using **.Where()** or **.ForEach()**.</span></span>
  - <span data-ttu-id="5fdff-143">Další informace o těchto metodách v [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)</span><span class="sxs-lookup"><span data-stu-id="5fdff-143">You can read more about these methods in [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)</span></span>

## <a name="using-non-node-data"></a><span data-ttu-id="5fdff-144">Použití dat mimo uzel</span><span class="sxs-lookup"><span data-stu-id="5fdff-144">Using non-node data</span></span>

<span data-ttu-id="5fdff-145">Jak jsme viděli v předchozích příkladech **ConfigurationData** zatřiďovací tabulka může mít jeden nebo více klíčů kromě požadované **AllNodes** klíč.</span><span class="sxs-lookup"><span data-stu-id="5fdff-145">As we've seen in previous examples, the **ConfigurationData** hashtable can have one or more keys in addition to the required **AllNodes** key.</span></span>
<span data-ttu-id="5fdff-146">V příkladech v tomto tématu jsme použít jenom jeden další uzel a s názvem ho `NonNodeData`.</span><span class="sxs-lookup"><span data-stu-id="5fdff-146">In the examples in this topic, we have used only a single additional node, and named it `NonNodeData`.</span></span>
<span data-ttu-id="5fdff-147">Však můžete definovat libovolný počet dalších klíčů a pojmenujte je všechno, co chcete.</span><span class="sxs-lookup"><span data-stu-id="5fdff-147">However, you can define any number of additional keys, and name them anything you want.</span></span>

<span data-ttu-id="5fdff-148">Příklad použití data mimo uzel, naleznete v tématu [oddělení dat konfigurace a prostředí](separatingEnvData.md).</span><span class="sxs-lookup"><span data-stu-id="5fdff-148">For an example of using non-node data, see [Separating configuration and environment data](separatingEnvData.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5fdff-149">Viz také</span><span class="sxs-lookup"><span data-stu-id="5fdff-149">See Also</span></span>

- [<span data-ttu-id="5fdff-150">Možnosti přihlašovacích údajů v konfiguračních datech</span><span class="sxs-lookup"><span data-stu-id="5fdff-150">Credentials Options in Configuration Data</span></span>](configDataCredentials.md)
- [<span data-ttu-id="5fdff-151">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="5fdff-151">DSC Configurations</span></span>](configurations.md)