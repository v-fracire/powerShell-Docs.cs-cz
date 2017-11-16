---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Pomocí konfigurační data"
ms.openlocfilehash: a70cd8f0f6c24eb02743b02d198cebcc3d775756
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="using-configuration-data-in-dsc"></a><span data-ttu-id="e689c-103">Pomocí konfigurační data v DSC</span><span class="sxs-lookup"><span data-stu-id="e689c-103">Using configuration data in DSC</span></span>

><span data-ttu-id="e689c-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e689c-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="e689c-105">Pomocí předdefinovaných DSC **ConfigurationData** parametr, můžete definovat data, která lze použít v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e689c-105">By using the built-in DSC **ConfigurationData** parameter, you can define data that can be used within a configuration.</span></span> <span data-ttu-id="e689c-106">To umožňuje vytvoření jedné konfigurace, které lze použít pro více uzly nebo v různých prostředích.</span><span class="sxs-lookup"><span data-stu-id="e689c-106">This allows you to create a single configuration that can be used for multiple nodes or for different environments.</span></span> <span data-ttu-id="e689c-107">Například pokud vyvíjíte aplikaci, můžete použít jednu konfiguraci pro vývoj a produkční prostředí a konfigurační data použijte k určení dat pro každé prostředí.</span><span class="sxs-lookup"><span data-stu-id="e689c-107">For example, if you are developing an application, you can use one configuration for both development and production environments, and use configuration data to specify data for each environment.</span></span>

<span data-ttu-id="e689c-108">Toto téma popisuje strukturu **ConfigurationData** zatřiďovací tabulky.</span><span class="sxs-lookup"><span data-stu-id="e689c-108">This topic describes the structure of the **ConfigurationData** hashtable.</span></span> <span data-ttu-id="e689c-109">Příklady použití konfiguračních dat najdete v tématu [oddělení dat konfigurace a prostředí](separatingEnvData.md).</span><span class="sxs-lookup"><span data-stu-id="e689c-109">For examples of how to use configuration data, see [Separating configuration and environment data](separatingEnvData.md).</span></span>

## <a name="the-configurationdata-common-parameter"></a><span data-ttu-id="e689c-110">Společný parametr ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="e689c-110">The ConfigurationData common parameter</span></span>

<span data-ttu-id="e689c-111">Konfigurace DSC trvá společný parametr **ConfigurationData**, zda jste zadali při kompilaci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="e689c-111">A DSC configuration takes a common parameter, **ConfigurationData**, that you specify when you compile the configuration.</span></span> <span data-ttu-id="e689c-112">Informace o kompilování konfigurace najdete v tématu [konfigurace DSC](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="e689c-112">For information about compiling configurations, see [DSC configurations](configurations.md).</span></span>

<span data-ttu-id="e689c-113">**ConfigurationData** parametr je hasthtable, kterou musí mít alespoň jeden klíč s názvem **AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="e689c-113">The **ConfigurationData** parameter is a hasthtable that must have at least one key named **AllNodes**.</span></span> <span data-ttu-id="e689c-114">Může také obsahovat jeden či více klíčů.</span><span class="sxs-lookup"><span data-stu-id="e689c-114">It can also have one or more other keys.</span></span>

><span data-ttu-id="e689c-115">**Poznámka:** v příkladech v tomto tématu použijte jeden další klíč (než pojmenované **AllNodes** klíč) s názvem `NonNodeData`, ale může obsahovat libovolný počet dalších klíčů a název je všechno.</span><span class="sxs-lookup"><span data-stu-id="e689c-115">**Note:** The examples in this topic use a single additional key (other than the named **AllNodes** key) named `NonNodeData`, but you can include any number of additional keys, and name them whatever you want.</span></span>

```powershell
$MyData = 
@{
    AllNodes = @()
    NonNodeData = ""   
}
```

<span data-ttu-id="e689c-116">Hodnota **AllNodes** klíč je pole.</span><span class="sxs-lookup"><span data-stu-id="e689c-116">The value of the **AllNodes** key is an array.</span></span> <span data-ttu-id="e689c-117">Každý prvek toto pole je také zatřiďovací tabulka, která musí mít alespoň jeden klíč s názvem **NodeName**:</span><span class="sxs-lookup"><span data-stu-id="e689c-117">Each element of this array is also a hash table that must have at least one key named **NodeName**:</span></span>

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

<span data-ttu-id="e689c-118">Můžete přidat další klíče pro každou zatřiďovací tabulku:</span><span class="sxs-lookup"><span data-stu-id="e689c-118">You can add other keys to each hash table as well:</span></span>

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

<span data-ttu-id="e689c-119">Použít vlastnosti na všech uzlech, můžete vytvořit členem **AllNodes** pole, které má **NodeName** z `*`.</span><span class="sxs-lookup"><span data-stu-id="e689c-119">To apply a property to all nodes, you can create a member of the **AllNodes** array that has a **NodeName** of `*`.</span></span> <span data-ttu-id="e689c-120">Například pro poskytnutí každý uzel `LogPath` vlastnost, můžete to udělat toto:</span><span class="sxs-lookup"><span data-stu-id="e689c-120">For example, to give every node a `LogPath` property, you could do this:</span></span>

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

<span data-ttu-id="e689c-121">Jedná se o ekvivalent přidávání vlastnost s názvem `LogPath` s hodnotou `"C:\Logs"` všechny ostatní bloky (`VM-1`, `VM-2`, a `VM-3`).</span><span class="sxs-lookup"><span data-stu-id="e689c-121">This is the equivalent of adding a property with a name of `LogPath` with a value of `"C:\Logs"` to each of the other blocks (`VM-1`, `VM-2`, and `VM-3`).</span></span>

## <a name="defining-the-configurationdata-hashtable"></a><span data-ttu-id="e689c-122">Definování ConfigurationData zatřiďovací tabulky</span><span class="sxs-lookup"><span data-stu-id="e689c-122">Defining the ConfigurationData hashtable</span></span>

<span data-ttu-id="e689c-123">Můžete definovat **ConfigurationData** buď jako proměnné v souboru skriptu jako konfigurace (jako v předchozí příklady) nebo v samostatném `.psd1` souboru.</span><span class="sxs-lookup"><span data-stu-id="e689c-123">You can define **ConfigurationData** either as a variable within the same script file as a configuration (as in our previous examples) or in a separate `.psd1` file.</span></span> <span data-ttu-id="e689c-124">Chcete-li definovat **ConfigurationData** v `.psd1` souboru, vytvořte soubor, který obsahuje pouze zatřiďovací tabulky, který představuje konfigurační data.</span><span class="sxs-lookup"><span data-stu-id="e689c-124">To define **ConfigurationData** in a `.psd1` file, create a file that contains only the hashtable that represents the configuration data.</span></span>

<span data-ttu-id="e689c-125">Například můžete vytvořit soubor s názvem `MyData.psd1` s tímto obsahem:</span><span class="sxs-lookup"><span data-stu-id="e689c-125">For example, you could create a file named `MyData.psd1` with the following contents:</span></span>

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

## <a name="compiling-a-configuration-with-configuration-data"></a><span data-ttu-id="e689c-126">Kompilování konfigurace s konfigurační data</span><span class="sxs-lookup"><span data-stu-id="e689c-126">Compiling a configuration with configuration data</span></span>

<span data-ttu-id="e689c-127">Kompilace konfigurace, pro který jste definovali konfigurační data, můžete předat data konfigurace jako hodnotu **ConfigurationData** parametr.</span><span class="sxs-lookup"><span data-stu-id="e689c-127">To compile a configuration for which you have defined configuration data, you pass the cofiguration data as the value of the **ConfigurationData** parameter.</span></span>

<span data-ttu-id="e689c-128">Tím se vytvoří pro každou položku v souboru MOF **AllNodes** pole.</span><span class="sxs-lookup"><span data-stu-id="e689c-128">This will create a MOF file for each entry in the **AllNodes** array.</span></span>
<span data-ttu-id="e689c-129">Každý soubor MOF budou mít názvy `NodeName` vlastnost odpovídající položky pole.</span><span class="sxs-lookup"><span data-stu-id="e689c-129">Each MOF file will be named with the `NodeName` property of the corresponding array entry.</span></span>

<span data-ttu-id="e689c-130">Například pokud definujete konfigurační data jako v `MyData.psd1` souboru výše, kompilace konfigurace by vytvořit i `VM-1.mof` a `VM-2.mof` soubory.</span><span class="sxs-lookup"><span data-stu-id="e689c-130">For example, if you define configuration data as in the `MyData.psd1` file above, compiling a configuration would create both `VM-1.mof` and `VM-2.mof` files.</span></span>

### <a name="compiling-a-configuration-with-configuration-data-using-a-variable"></a><span data-ttu-id="e689c-131">Kompilování konfiguraci pomocí konfiguračních dat pomocí proměnné</span><span class="sxs-lookup"><span data-stu-id="e689c-131">Compiling a configuration with configuration data using a variable</span></span>

<span data-ttu-id="e689c-132">Použít konfigurační data, která je definována jako proměnné ve stejné `.ps1` soubor jako konfiguraci, předáte název proměnné jako hodnotu **ConfigurationData** parametr při kompilaci konfigurace:</span><span class="sxs-lookup"><span data-stu-id="e689c-132">To use configuration data that is defined as a variable in the same `.ps1` file as the configuration, you pass the variable name as the value of the **ConfigurationData** parameter when compiling the configuration:</span></span>

```powershell
MyDscConfiguration -ConfigurationData $MyData
```

### <a name="compiling-a-configuration-with-configuration-data-using-a-data-file"></a><span data-ttu-id="e689c-133">Kompilování konfiguraci pomocí konfiguračních dat pomocí a datový soubor.</span><span class="sxs-lookup"><span data-stu-id="e689c-133">Compiling a configuration with configuration data using a data file</span></span>

<span data-ttu-id="e689c-134">Pokud chcete používat konfigurační data, která je definována v souboru .psd1, předáte cesta a název souboru jako hodnotu **ConfigurationData** parametr při kompilaci konfigurace:</span><span class="sxs-lookup"><span data-stu-id="e689c-134">To use configuration data that is defined in a .psd1 file, you pass the path and name of that file as the value of the **ConfigurationData** parameter when compiling the configuration:</span></span>

```powershell
MyDscConfiguration -ConfigurationData .\MyData.psd1
```

## <a name="using-configurationdata-variables-in-a-configuration"></a><span data-ttu-id="e689c-135">Použití proměnných ConfigurationData v konfiguraci</span><span class="sxs-lookup"><span data-stu-id="e689c-135">Using ConfigurationData variables in a configuration</span></span>

<span data-ttu-id="e689c-136">DSC poskytuje tři speciální proměnné, které lze použít v konfigurační skript: **$AllNodes**, **$Node**, a **$ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="e689c-136">DSC provides three special variables that can be used in a configuration script: **$AllNodes**, **$Node**, and **$ConfigurationData**.</span></span>

- <span data-ttu-id="e689c-137">**$AllNodes** odkazuje na celou kolekci uzlů, které jsou definované v **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="e689c-137">**$AllNodes** refers to the entire collection of nodes defined in **ConfigurationData**.</span></span> <span data-ttu-id="e689c-138">Můžete filtrovat **AllNodes** kolekce pomocí **. WHERE()** a **. ForEach()**.</span><span class="sxs-lookup"><span data-stu-id="e689c-138">You can filter the **AllNodes** collection by using **.Where()** and **.ForEach()**.</span></span>
- <span data-ttu-id="e689c-139">**Uzel** odkazuje na konkrétní položky v **AllNodes** kolekci po je filtrován pomocí **. WHERE()** nebo **. ForEach()**.</span><span class="sxs-lookup"><span data-stu-id="e689c-139">**Node** refers to a particular entry in the **AllNodes** collection after it is filtered by using **.Where()** or **.ForEach()**.</span></span>
- <span data-ttu-id="e689c-140">**ConfigurationData** odkazuje na tabulku celou hodnotu hash, který je předán jako parametr při kompilaci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="e689c-140">**ConfigurationData** refers to the entire hash table that is passed as the parameter when compiling a configuration.</span></span>

## <a name="using-non-node-data"></a><span data-ttu-id="e689c-141">Pomocí data bez uzlu</span><span class="sxs-lookup"><span data-stu-id="e689c-141">Using non-node data</span></span>

<span data-ttu-id="e689c-142">Jak jsme viděli v předchozích příkladech **ConfigurationData** zatřiďovací tabulka může mít jeden či více klíčů kromě požadované **AllNodes** klíč.</span><span class="sxs-lookup"><span data-stu-id="e689c-142">As we've seen in previous examples, the **ConfigurationData** hashtable can have one or more keys in addition to the required **AllNodes** key.</span></span>
<span data-ttu-id="e689c-143">V příkladech v tomto tématu jsme použít pouze jeden addiontal uzel a s názvem ho `NonNodeData`.</span><span class="sxs-lookup"><span data-stu-id="e689c-143">In the examples in this topic, we have used only a single addiontal node, and named it `NonNodeData`.</span></span> <span data-ttu-id="e689c-144">Však můžete definovat libovolný počet addiontal klíče a název je všechno, co chcete.</span><span class="sxs-lookup"><span data-stu-id="e689c-144">However, you can define any number of addiontal keys, and name them anything you want.</span></span>

<span data-ttu-id="e689c-145">Příklad použití dat na jiný uzel, naleznete v části [oddělení dat konfigurace a prostředí](separatingEnvData.md).</span><span class="sxs-lookup"><span data-stu-id="e689c-145">For an example of using non-node data, see [Separating configuration and environment data](separatingEnvData.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e689c-146">Viz také</span><span class="sxs-lookup"><span data-stu-id="e689c-146">See Also</span></span>
- [<span data-ttu-id="e689c-147">Možnosti přihlašovací údaje v konfiguračních dat</span><span class="sxs-lookup"><span data-stu-id="e689c-147">Credentials Options in Configuration Data</span></span>](configDataCredentials.md)
- [<span data-ttu-id="e689c-148">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="e689c-148">DSC Configurations</span></span>](configurations.md)

