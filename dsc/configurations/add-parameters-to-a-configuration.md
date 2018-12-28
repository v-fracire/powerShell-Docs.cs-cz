---
ms.date: 12/12/2018
keywords: DSC, powershell, zdroj, galerie, instalační program
title: Přidání parametrů ke konfiguraci
ms.openlocfilehash: 15213404f0cdd6416baf1f83af91b8f5279cc97f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403725"
---
# <a name="add-parameters-to-a-configuration"></a><span data-ttu-id="a138e-103">Přidání parametrů ke konfiguraci</span><span class="sxs-lookup"><span data-stu-id="a138e-103">Add Parameters to a Configuration</span></span>

<span data-ttu-id="a138e-104">Funkce, jako jsou [konfigurace](configurations.md) může být parametrizován umožňující dynamičtějších konfigurace na základě uživatelského zadání.</span><span class="sxs-lookup"><span data-stu-id="a138e-104">Like Functions, [Configurations](configurations.md) can be parameterized to allow more dynamic configurations based on user input.</span></span> <span data-ttu-id="a138e-105">Postup je podobný jako postup popsaný v [funkce s parametry](/powershell/module/microsoft.powershell.core/about/about_functions).</span><span class="sxs-lookup"><span data-stu-id="a138e-105">The steps are similar to those described in [Functions with Parameters](/powershell/module/microsoft.powershell.core/about/about_functions).</span></span>

<span data-ttu-id="a138e-106">Tento příklad začíná základní konfigurace, který konfiguruje službu "Zařazování" k "Spuštěna".</span><span class="sxs-lookup"><span data-stu-id="a138e-106">This example starts with a basic Configuration that configures the "Spooler" service to be "Running".</span></span>

```powershell
Configuration TestConfig
{
    # It is best practice to implicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node localhost
    {
        Service 'Spooler'
        {
            Name = 'Spooler'
            State = 'Running'
        }
    }
}
```

## <a name="built-in-configuration-parameters"></a><span data-ttu-id="a138e-107">Integrované parametry konfigurace</span><span class="sxs-lookup"><span data-stu-id="a138e-107">Built-in Configuration parameters</span></span>

<span data-ttu-id="a138e-108">Na rozdíl od funkce však [CmdletBinding](/powershell/module/microsoft.powershell.core/about/about_functions_cmdletbindingattribute) atribut přidá žádné funkce.</span><span class="sxs-lookup"><span data-stu-id="a138e-108">Unlike a Function though, the [CmdletBinding](/powershell/module/microsoft.powershell.core/about/about_functions_cmdletbindingattribute) attribute adds no functionality.</span></span> <span data-ttu-id="a138e-109">Kromě [společné parametry](/powershell/module/microsoft.powershell.core/about/about_commonparameters), konfigurace můžete použít také následující předdefinované parametrů, aniž by bylo potřeba jejich definování.</span><span class="sxs-lookup"><span data-stu-id="a138e-109">In addition to [Common Parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters), Configurations can also use the following built in parameters, without requiring you to define them.</span></span>

|<span data-ttu-id="a138e-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="a138e-110">Parameter</span></span>  |<span data-ttu-id="a138e-111">Popis</span><span class="sxs-lookup"><span data-stu-id="a138e-111">Description</span></span>  |
|---------|---------|
|`-InstanceName`|<span data-ttu-id="a138e-112">Použít při definování [složené konfigurace](compositeconfigs.md)</span><span class="sxs-lookup"><span data-stu-id="a138e-112">Used in defining [Composite Configurations](compositeconfigs.md)</span></span>|
|`-DependsOn`|<span data-ttu-id="a138e-113">Použít při definování [složené konfigurace](compositeconfigs.md)</span><span class="sxs-lookup"><span data-stu-id="a138e-113">Used in defining [Composite Configurations](compositeconfigs.md)</span></span>|
|`-PSDSCRunAsCredential`|<span data-ttu-id="a138e-114">Použít při definování [složené konfigurace](compositeconfigs.md)</span><span class="sxs-lookup"><span data-stu-id="a138e-114">Used in defining [Composite Configurations](compositeconfigs.md)</span></span>|
|`-ConfigurationData`|<span data-ttu-id="a138e-115">Sloužící k předávání v strukturované [konfigurační Data](configData.md) pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="a138e-115">Used to pass in structured [Configuration Data](configData.md) for use in the Configuration.</span></span>|
|`-OutputPath`|<span data-ttu-id="a138e-116">Umožňuje určit, kde vaše "\<computername\>MOF" soubor bude zkompilována.</span><span class="sxs-lookup"><span data-stu-id="a138e-116">Used to specify where your "\<computername\>.mof" file will be compiled</span></span>|

## <a name="adding-your-own-parameters-to-configurations"></a><span data-ttu-id="a138e-117">Přidání vlastní parametry konfigurace</span><span class="sxs-lookup"><span data-stu-id="a138e-117">Adding your own parameters to Configurations</span></span>

<span data-ttu-id="a138e-118">Kromě předdefinovaných parametry můžete také přidat vlastní parametry do vaší konfigurace.</span><span class="sxs-lookup"><span data-stu-id="a138e-118">In addition to the built-in parameters, you can also add your own parameters to your Configurations.</span></span> <span data-ttu-id="a138e-119">Blok parametrů přejde přímo uvnitř deklarace konfigurace, stejně jako funkce.</span><span class="sxs-lookup"><span data-stu-id="a138e-119">The parameter block goes directly inside the Configuration declaration, just like a Function.</span></span> <span data-ttu-id="a138e-120">Blok parametr konfigurace by měla být mimo všechny **uzel** deklarace a výše žádné *importovat* příkazy.</span><span class="sxs-lookup"><span data-stu-id="a138e-120">A Configuration parameter block should be outside any **Node** declarations, and above any *import* statements.</span></span> <span data-ttu-id="a138e-121">Přidáním parametrů můžete provést konfiguraci robustní a dynamické.</span><span class="sxs-lookup"><span data-stu-id="a138e-121">By adding parameters, you can make your Configurations more robust and dynamic.</span></span>

```powershell
Configuration TestConfig
{
    param
    (

    )
```

### <a name="add-a-computername-parameter"></a><span data-ttu-id="a138e-122">Přidat parametr ComputerName</span><span class="sxs-lookup"><span data-stu-id="a138e-122">Add a ComputerName parameter</span></span>

<span data-ttu-id="a138e-123">První parametr, můžete přidat je `-Computername` parametrů, takže můžete dynamicky kompilovat soubor "MOF" pro všechny `-Computername` předáte do vaší konfigurace.</span><span class="sxs-lookup"><span data-stu-id="a138e-123">The first parameter you might add is a `-Computername` parameter so you can dynamically compile a ".mof" file for any `-Computername` you pass to your configuration.</span></span> <span data-ttu-id="a138e-124">Podobně jako funkce můžete také definovat výchozí hodnotu v případě, že uživatel nepředáte hodnotu `-ComputerName`</span><span class="sxs-lookup"><span data-stu-id="a138e-124">Like Functions, you can also define a default value, in case the user does not pass in a value for `-ComputerName`</span></span>

```powershell
param
(
    [String]
    $ComputerName="localhost"
)
```

<span data-ttu-id="a138e-125">V rámci konfigurace, můžete pak určit váš `-ComputerName` parametr při definování vašeho uzlu bloku.</span><span class="sxs-lookup"><span data-stu-id="a138e-125">Within your configuration, you can then specify your `-ComputerName` parameter when defining your Node block.</span></span>

```powershell
Node $ComputerName
{

}
```

### <a name="calling-your-configuration-with-parameters"></a><span data-ttu-id="a138e-126">Konfigurace s parametry volání</span><span class="sxs-lookup"><span data-stu-id="a138e-126">Calling your Configuration with parameters</span></span>

<span data-ttu-id="a138e-127">Po přidání parametrů do vaší konfigurace, můžete je použít stejným způsobem, jako byste to pomocí rutiny.</span><span class="sxs-lookup"><span data-stu-id="a138e-127">After you have added parameters to your Configuration, you can use them just like you would with a cmdlet.</span></span>

```powershell
TestConfig -ComputerName "server01"
```

### <a name="compiling-multiple-mof-files"></a><span data-ttu-id="a138e-128">Kompilování více soubory MOF</span><span class="sxs-lookup"><span data-stu-id="a138e-128">Compiling multiple .mof files</span></span>

<span data-ttu-id="a138e-129">Blok uzel můžete také přijmout čárkou oddělený seznam názvů počítačů a bude generovat soubory ".mof" pro každý.</span><span class="sxs-lookup"><span data-stu-id="a138e-129">The Node block can also accept a comma-separated list of computer names and will generate ".mof" files for each.</span></span> <span data-ttu-id="a138e-130">Spustíte podle následujícího příkladu lze generovat soubory ".mof" pro všechny počítače, které jsou předány `-ComputerName` parametru.</span><span class="sxs-lookup"><span data-stu-id="a138e-130">You can run the following example to generate ".mof" files for all of the computers passed to the `-ComputerName` parameter.</span></span>

```powershell
Configuration TestConfig
{
    param
    (
        [String]
        $ComputerName="localhost"
    )

    # It is best practice to implicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node $ComputerName
    {
        Service 'Spooler'
        {
            Name = 'Spooler'
            State = 'Running'
        }
    }
}

TestConfig -ComputerName "server01", "server02", "server03"
```

## <a name="advanced-parameters-in-configurations"></a><span data-ttu-id="a138e-131">Pokročilé parametry v konfiguracích</span><span class="sxs-lookup"><span data-stu-id="a138e-131">Advanced parameters in Configurations</span></span>

<span data-ttu-id="a138e-132">Kromě `-ComputerName` parametr, můžeme přidat parametry pro název služby a stav.</span><span class="sxs-lookup"><span data-stu-id="a138e-132">In addition to a `-ComputerName` parameter, we can add parameters for the service name and state.</span></span> <span data-ttu-id="a138e-133">Následující příklad přidá parametr blok s `-ServiceName` parametr a použije ho a dynamicky tak definovat **služby** prostředků bloku.</span><span class="sxs-lookup"><span data-stu-id="a138e-133">The following example adds a parameter block with a `-ServiceName` parameter and uses it to dynamically define the **Service** resource block.</span></span> <span data-ttu-id="a138e-134">Přidá také `-State` parametrů a dynamicky tak definovat **stavu** v **služby** prostředků bloku.</span><span class="sxs-lookup"><span data-stu-id="a138e-134">It also adds a `-State` parameter to dynamically define the **State** in the **Service** resource block.</span></span>

```powershell
Configuration TestConfig
{
    param
    (
        [String]
        $ServiceName,

        [String]
        $State,

        [String]
        $ComputerName="localhost"
    )

    # It is best practice to implicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node $ComputerName
    {
        Service $ServiceName
        {
            Name = $ServiceName
            State = $State
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="a138e-135">Ve více scénářích advacned, může mít více smysl přesunout dynamických dat do strukturované [konfigurační Data](configData.md).</span><span class="sxs-lookup"><span data-stu-id="a138e-135">In more advacned scenarios, it might make more sense to move your dynamic data into a structured [Configuration Data](configData.md).</span></span>

<span data-ttu-id="a138e-136">Příklad konfigurace nyní přijímá dynamickou `$ServiceName`, ale pokud není zadaná, kompilaci za následek chybu.</span><span class="sxs-lookup"><span data-stu-id="a138e-136">The example Configuration now takes a dynamic `$ServiceName`, but if one is not specified, compiling results in an error.</span></span> <span data-ttu-id="a138e-137">Můžete přidat výchozí hodnotu jako v tomto příkladu.</span><span class="sxs-lookup"><span data-stu-id="a138e-137">You could add a default value like this example.</span></span>

```powershell
[String]
$ServiceName="Spooler"
```

<span data-ttu-id="a138e-138">V tomto případě však smysl další jednoduše nutí uživatele zadat hodnotu `$ServiceName` parametru.</span><span class="sxs-lookup"><span data-stu-id="a138e-138">In this instance though, it makes more sense to simply force the user to specify a value for the `$ServiceName` parameter.</span></span> <span data-ttu-id="a138e-139">`parameter` Atribut umožňuje přidat další ověření a kanál podpory vaší konfigurace parametrů.</span><span class="sxs-lookup"><span data-stu-id="a138e-139">The `parameter` attribute allows you to add further validation and pipeline support to your Configuration's parameters.</span></span>

<span data-ttu-id="a138e-140">Nad všechny deklarace parametru přidejte `parameter` bloku atributu stejně jako v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="a138e-140">Above any parameter declaration, add the `parameter` attribute block as in the example below.</span></span>

```powershell
[parameter()]
[String]
$ServiceName
```

<span data-ttu-id="a138e-141">Lze zadat argumenty u každého `parameter` atribut pro řízení aspektů definovaný parametr.</span><span class="sxs-lookup"><span data-stu-id="a138e-141">You can specify arguments to each `parameter` attribute, to control aspects of the defined parameter.</span></span> <span data-ttu-id="a138e-142">Následující příklad provede `$ServiceName` **povinné** parametru.</span><span class="sxs-lookup"><span data-stu-id="a138e-142">The following example makes the `$ServiceName` a **Mandatory** parameter.</span></span>

```powershell
[parameter(Mandatory)]
[String]
$ServiceName
```

<span data-ttu-id="a138e-143">Pro `$State` parametr, rádi bychom zabrání uživateli v zadávání hodnoty mimo sadu předdefinovaných (jako je spuštění, zastavení) `ValidationSet*`atributu by zabrání uživateli v zadávání hodnoty mimo sadu předdefinovaných (jako je spuštění, Zastavit).</span><span class="sxs-lookup"><span data-stu-id="a138e-143">For the `$State` parameter, we would like to prevent the user from specifying values outside of a predefined set (like Running, Stopped) the `ValidationSet*`attribute would prevent the user from specifying values outside of a predefined set (like Running, Stopped).</span></span> <span data-ttu-id="a138e-144">Následující příklad přidá `ValidationSet` atribut `$State` parametru.</span><span class="sxs-lookup"><span data-stu-id="a138e-144">The following example adds the `ValidationSet` attribute to the `$State` parameter.</span></span> <span data-ttu-id="a138e-145">Protože jsme nechcete, aby `$State` parametr **povinné**, budeme muset přidat výchozí hodnotu pro něj.</span><span class="sxs-lookup"><span data-stu-id="a138e-145">Since we do not want to make the `$State` parameter **Mandatory**, we will need to add a default value for it.</span></span>

```powershell
[ValidateSet("Running", "Stopped")]
[String]
$State="Running"
```

> [!NOTE]
> <span data-ttu-id="a138e-146">Není potřeba zadat `parameter` atribut při použití `validation` atribut.</span><span class="sxs-lookup"><span data-stu-id="a138e-146">You do not need to specify a `parameter` attribute when using a `validation` attribute.</span></span>

<span data-ttu-id="a138e-147">Další informace o `parameter` a atributů ověření v [about_Functions_Advanced_Parameters](/powershell/module/microsoft.powershell.core/about/about_Functions_Advanced_Parameters.md).</span><span class="sxs-lookup"><span data-stu-id="a138e-147">You can read more about the `parameter` and validation attributes in [about_Functions_Advanced_Parameters](/powershell/module/microsoft.powershell.core/about/about_Functions_Advanced_Parameters.md).</span></span>

## <a name="fully-parameterized-configuration"></a><span data-ttu-id="a138e-148">Plně parametry konfigurace</span><span class="sxs-lookup"><span data-stu-id="a138e-148">Fully parameterized Configuration</span></span>

<span data-ttu-id="a138e-149">Teď máme parametry konfigurace, která vynutí, aby uživatel zadal `-InstanceName`, `-ServiceName`a ověří `-State` parametru.</span><span class="sxs-lookup"><span data-stu-id="a138e-149">We now have a parameterized Configuration that forces the user to specify an `-InstanceName`, `-ServiceName`, and validates the `-State` parameter.</span></span>

```powershell
Configuration TestConfig
{
    param
    (
        [parameter(Mandatory)]
        [String]
        $ServiceName,

        [ValidateSet("Running","Stopped")]
        [String]
        $State="Running",

        [String]
        $ComputerName="localhost",
    )

    # It is best practice to implicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node localhost
    {
        Service $ServiceName
        {
            Name = $ServiceName
            State = $State
        }
    }
}
```

## <a name="see-also"></a><span data-ttu-id="a138e-150">Viz taky</span><span class="sxs-lookup"><span data-stu-id="a138e-150">See also</span></span>

- [<span data-ttu-id="a138e-151">Zápis nápovědy ke konfiguracím DSC</span><span class="sxs-lookup"><span data-stu-id="a138e-151">Write help for DSC configurations</span></span>](configHelp.md)
- [<span data-ttu-id="a138e-152">Dynamická konfigurace</span><span class="sxs-lookup"><span data-stu-id="a138e-152">Dynamic Configurations</span></span>](flow-control-in-configurations.md)
- [<span data-ttu-id="a138e-153">Použití konfiguračních dat ve vašich konfiguracích</span><span class="sxs-lookup"><span data-stu-id="a138e-153">Use Configuration Data in your Configurations</span></span>](configData.md)
- [<span data-ttu-id="a138e-154">Samostatná data pro konfiguraci a prostředí</span><span class="sxs-lookup"><span data-stu-id="a138e-154">Separate configuration and environment data</span></span>](separatingEnvData.md)
