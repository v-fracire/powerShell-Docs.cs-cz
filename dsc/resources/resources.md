---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředky DSC
ms.openlocfilehash: 02e1b9856942cf28e77d83dac89681a08cf6bb74
ms.sourcegitcommit: 9df29dfc637191b62ca591893c251c1e02d4eb4c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54012445"
---
# <a name="dsc-resources"></a><span data-ttu-id="2a3f8-103">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="2a3f8-103">DSC Resources</span></span>

><span data-ttu-id="2a3f8-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="2a3f8-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="2a3f8-105">Desired State Configuration (DSC) prostředky poskytují stavební bloky pro konfiguraci DSC.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-105">Desired State Configuration (DSC) Resources provide the building blocks for a DSC configuration.</span></span> <span data-ttu-id="2a3f8-106">Prostředek zveřejňuje vlastnosti, které může být nakonfigurovaný (schéma) a obsahuje funkce skript Powershellu, která volá místní Configuration Manageru (LCM) aby ",".</span><span class="sxs-lookup"><span data-stu-id="2a3f8-106">A resource exposes properties that can be configured (schema) and contains the PowerShell script functions that the Local Configuration Manager (LCM) calls to "make it so".</span></span>

<span data-ttu-id="2a3f8-107">Zdroj lze modelovat něco jako obecné jako soubor, nebo co nastavení serveru služby IIS.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-107">A resource can model something as generic as a file or as specific as an IIS server setting.</span></span>  <span data-ttu-id="2a3f8-108">Skupiny jako prostředky jsou zkombinované v modulu DSC, která slouží k uspořádání všechny požadované soubory v strukturu, která je přenosná a zahrnuje jejich metadata k určení, jak jsou prostředky určena pro použití.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-108">Groups of like resources are combined in to a DSC Module, which organizes all the required files in to a structure that is portable and includes metadata to identify how the resources are intended to be used.</span></span>

<span data-ttu-id="2a3f8-109">Každý prostředek má \* schéma, které určuje nutné k využití prostředků v syntaxi [konfigurace](../configurations/configurations.md).</span><span class="sxs-lookup"><span data-stu-id="2a3f8-109">Each resource has a \*schema that determines the syntax needed to use the resource in a [Configuration](../configurations/configurations.md).</span></span> <span data-ttu-id="2a3f8-110">Schéma zdroje lze definovat takto:</span><span class="sxs-lookup"><span data-stu-id="2a3f8-110">A resource's schema can be defined in the following ways:</span></span>

- <span data-ttu-id="2a3f8-111">**"Schema.Mof"** souboru: Definujte většinu prostředků jejich *schématu* v "schema.mof soubor, pomocí [Managed Object Format](/windows/desktop/wmisdk/managed-object-format--mof-).</span><span class="sxs-lookup"><span data-stu-id="2a3f8-111">**'Schema.Mof'** file: Most resources define their *schema* in a 'schema.mof' file, using [Managed Object Format](/windows/desktop/wmisdk/managed-object-format--mof-).</span></span>
- <span data-ttu-id="2a3f8-112">**"\<Název prostředku\>. schema.psm1"** souboru: [Složené prostředky](../configurations/compositeConfigs.md) definovat jejich *schématu* v "<ResourceName>. schema.psm1" soubor pomocí [bloku parametrů](/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-6#functions-with-parameters).</span><span class="sxs-lookup"><span data-stu-id="2a3f8-112">**'\<Resource Name\>.schema.psm1'** file: [Composite Resources](../configurations/compositeConfigs.md) define their *schema* in a '<ResourceName>.schema.psm1' file using a [Parameter Block](/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-6#functions-with-parameters).</span></span>
- <span data-ttu-id="2a3f8-113">**"\<Název prostředku\>.psm1"** souboru: Třídy založené na prostředky DSC definovat jejich *schématu* v definici třídy.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-113">**'\<Resource Name\>.psm1'** file: Class based DSC resources define their *schema* in the class definition.</span></span> <span data-ttu-id="2a3f8-114">Syntaxe položky jsou označené jako vlastnosti třídy.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-114">Syntax items are denoted as Class properties.</span></span> <span data-ttu-id="2a3f8-115">Další informace najdete v tématu [about_Classes](/powershell/module/psdesiredstateconfiguration/about/about_classes_and_dsc).</span><span class="sxs-lookup"><span data-stu-id="2a3f8-115">For more information, see [about_Classes](/powershell/module/psdesiredstateconfiguration/about/about_classes_and_dsc).</span></span>

<span data-ttu-id="2a3f8-116">Pokud chcete načíst syntaxe pro prostředek DSC, použijte [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) rutinu s `-Syntax` parametru.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-116">To retrieve the syntax for a DSC resource, use the [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet with the `-Syntax` parameter.</span></span> <span data-ttu-id="2a3f8-117">Toto použití je podobný používání [Get-Command](/powershell/module/microsoft.powershell.core/get-command) s `-Syntax` parametr zobrazíte Syntaxe rutin.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-117">This usage is similar to using [Get-Command](/powershell/module/microsoft.powershell.core/get-command) with the `-Syntax` parameter to get cmdlet syntax.</span></span> <span data-ttu-id="2a3f8-118">Šablona použitá pro blok prostředků pro prostředek, který zadáte se zobrazí výstup, který se zobrazí.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-118">The output you see will show the template used for a resource block for the resource you specify.</span></span>

```powershell
Get-DscResource -Syntax Service
```

<span data-ttu-id="2a3f8-119">Který se zobrazí výstup by měl vypadat přibližně ve výstupu níže, i když tento prostředek syntaxe může v budoucnu změnit.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-119">The output you see should be similar to the output below, though this resource's syntax could change in the future.</span></span> <span data-ttu-id="2a3f8-120">Syntaxe rutin, jako jsou *klíče* viděli v hranatých závorkách jsou volitelné.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-120">Like cmdlet syntax, the *keys* seen in square brackets, are optional.</span></span> <span data-ttu-id="2a3f8-121">Typy určete typ dat, který očekává, že každý klíč.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-121">The types specify the type of data each key expects.</span></span>

> [!NOTE]
> <span data-ttu-id="2a3f8-122">**Ujistěte se, že** klíč je volitelný, protože výchozí hodnota "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="2a3f8-122">The **Ensure** key is optional because it defaults to "Present".</span></span>

```output
Service [String] #ResourceName
{
    Name = [string]
    [BuiltInAccount = [string]{ LocalService | LocalSystem | NetworkService }]
    [Credential = [PSCredential]]
    [Dependencies = [string[]]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [DisplayName = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Path = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [StartupType = [string]{ Automatic | Disabled | Manual }]
    [State = [string]{ Running | Stopped }]
}
```

<span data-ttu-id="2a3f8-123">V konfiguraci **služby** prostředků bloku může vypadat třeba takto k **Ujistěte se, že** , na kterém běží služba zařazování tisku.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-123">Inside a Configuration, a **Service** resource block might look like this to **Ensure** that the Spooler service is running.</span></span>

> [!NOTE]
> <span data-ttu-id="2a3f8-124">Před použitím zdroje v konfiguraci, je nutné naimportovat pomocí [Import-DSCResource](../configurations/import-dscresource.md).</span><span class="sxs-lookup"><span data-stu-id="2a3f8-124">Before using a resource in a Configuration, you must import it using [Import-DSCResource](../configurations/import-dscresource.md).</span></span>

```powershell
Configuration TestConfig
{
    # It is best practice to always directly import resources, even if the resource is a built-in resource.
    Import-DSCResource -Name Service
    Node localhost
    {
        # The name of this resource block, can be anything you choose, as long as it is of type [String] as indicated by the schema.
        Service "Spooler:Running"
        {
            Name = "Spooler"
            State = "Running"
        }
    }
}
```

<span data-ttu-id="2a3f8-125">Konfigurace může obsahovat více instancí stejného typu prostředku.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-125">Configurations can contain multiple instances of the same resource type.</span></span> <span data-ttu-id="2a3f8-126">Každá instance musí mít jedinečné názvy.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-126">Each instance must be uniquely named.</span></span> <span data-ttu-id="2a3f8-127">V následujícím příkladu druhý **služby** prostředků bloku se přidá do konfigurace služby "DHCP".</span><span class="sxs-lookup"><span data-stu-id="2a3f8-127">In the following example, a second **Service** resource block is added to configure the "DHCP" service.</span></span>

```powershell
Configuration TestConfig
{
    # It is best practice to always directly import resources, even if the resource is a built-in resource.
    Import-DSCResource -Name Service
    Node localhost
    {
        # The name of this resource block, can be anything you choose, as long as it is of type [String] as indicated by the schema.
        Service "Spooler:Running"
        {
            Name = "Spooler"
            State = "Running"
        }

        # To configure a second service resource block, add another Service resource block and use a unique name.
        Service "DHCP:Running"
        {
            Name = "DHCP"
            State = "Running"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="2a3f8-128">Od v Powershellu 5.0, byl přidán technologie intellisense pro DSC.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-128">Beginning in PowerShell 5.0, intellisense was added for DSC.</span></span> <span data-ttu-id="2a3f8-129">Tato nová funkce umožňuje používat \<kartu\> a \<kombinace kláves Ctrl + mezerník\> pro automatické dokončování názvů klíčů.</span><span class="sxs-lookup"><span data-stu-id="2a3f8-129">This new feature allows you to use \<TAB\> and \<Ctrl+Space\> to auto-complete key names.</span></span>

![Prostředek Tab k dokončování příkazů](../media/resource-tabcompletion.png)
