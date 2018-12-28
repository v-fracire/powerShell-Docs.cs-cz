---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Složené prostředky – pomocí konfigurace DSC jako prostředek
ms.openlocfilehash: 2823d05e0c8feb2933ca691f9ab5149ace2f7ee3
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403653"
---
# <a name="composite-resources-using-a-dsc-configuration-as-a-resource"></a><span data-ttu-id="4130d-103">Složené prostředky: Pomocí konfigurace DSC jako prostředek</span><span class="sxs-lookup"><span data-stu-id="4130d-103">Composite resources: Using a DSC configuration as a resource</span></span>

> <span data-ttu-id="4130d-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="4130d-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="4130d-105">V reálných situacích může být konfigurace dlouhá a složitá, volání mnoho různých prostředků a nastavení rozsáhlé počet vlastností.</span><span class="sxs-lookup"><span data-stu-id="4130d-105">In real-world situations, configurations can become long and complex, calling many different resources and setting a vast number of properties.</span></span> <span data-ttu-id="4130d-106">Pomáhají řešit Tato složitost, můžete použít Windows PowerShell Desired State Configuration (DSC) konfigurace jako prostředek pro další konfigurace.</span><span class="sxs-lookup"><span data-stu-id="4130d-106">To help address this complexity, you can use a Windows PowerShell Desired State Configuration (DSC) configuration as a resource for other configurations.</span></span> <span data-ttu-id="4130d-107">To označujeme složený prostředek.</span><span class="sxs-lookup"><span data-stu-id="4130d-107">We call this a composite resource.</span></span> <span data-ttu-id="4130d-108">Složený prostředek je konfigurace DSC, která přebírá parametry.</span><span class="sxs-lookup"><span data-stu-id="4130d-108">A composite resource is a DSC configuration that takes parameters.</span></span> <span data-ttu-id="4130d-109">Parametry konfigurace fungovat jako vlastností prostředku.</span><span class="sxs-lookup"><span data-stu-id="4130d-109">The parameters of the configuration act as the properties of the resource.</span></span> <span data-ttu-id="4130d-110">Konfigurace je uložen jako soubor s **. schema.psm1** rozšíření a přijímá místo schématu MOF a prostředek skriptu v typické prostředku DSC (Další informace o prostředcích DSC najdete v tématu [Windows Prostředí PowerShell Desired State Configuration prostředky](resources.md).</span><span class="sxs-lookup"><span data-stu-id="4130d-110">The configuration is saved as a file with a **.schema.psm1** extension, and takes the place of both the MOF schema and the resource script in a typical DSC resource (for more information about DSC resources, see [Windows PowerShell Desired State Configuration Resources](resources.md).</span></span>

## <a name="creating-the-composite-resource"></a><span data-ttu-id="4130d-111">Vytváření složených prostředků</span><span class="sxs-lookup"><span data-stu-id="4130d-111">Creating the composite resource</span></span>

<span data-ttu-id="4130d-112">V našem příkladu jsme vytvořit konfiguraci, která volá počet stávajících prostředků, abyste konfiguraci virtuálních počítačů.</span><span class="sxs-lookup"><span data-stu-id="4130d-112">In our example, we create a configuration that invokes a number of existing resources to configure virtual machines.</span></span> <span data-ttu-id="4130d-113">Místo určení hodnoty, které mají být nastavené v blocích konfigurace, konfigurace přijímá několik parametrů, které se následně použijí v blocích konfigurace.</span><span class="sxs-lookup"><span data-stu-id="4130d-113">Instead of specifying the values to be set in configuration blocks, the configuration takes a number of parameters that are then used in the configuration blocks.</span></span>

```powershell
Configuration xVirtualMachine
{
    param
    (
        # Name of VMs
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String[]] $VMName,

        # Name of Switch to create
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $SwitchName,

        # Type of Switch to create
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $SwitchType,

        # Source Path for VHD
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VHDParentPath,

        # Destination path for diff VHD
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VHDPath,

        # Startup Memory for VM
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VMStartupMemory,

        # State of the VM
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VMState
    )

    # Import the module that defines custom resources
    Import-DscResource -Module xComputerManagement,xHyper-V

    # Install the Hyper-V role
    WindowsFeature HyperV
    {
        Ensure = "Present"
        Name = "Hyper-V"
    }

    # Create the virtual switch
    xVMSwitch $SwitchName
    {
        Ensure = "Present"
        Name = $SwitchName
        Type = $SwitchType
        DependsOn = "[WindowsFeature]HyperV"
    }

    # Check for Parent VHD file
    File ParentVHDFile
    {
        Ensure = "Present"
        DestinationPath = $VHDParentPath
        Type = "File"
        DependsOn = "[WindowsFeature]HyperV"
    }

    # Check the destination VHD folder
    File VHDFolder
    {
        Ensure = "Present"
        DestinationPath = $VHDPath
        Type = "Directory"
        DependsOn = "[File]ParentVHDFile"
    }

    # Create VM specific diff VHD
    foreach ($Name in $VMName)
    {
        xVHD "VHD$Name"
        {
            Ensure = "Present"
            Name = $Name
            Path = $VHDPath
            ParentPath = $VHDParentPath
            DependsOn = @("[WindowsFeature]HyperV",
                          "[File]VHDFolder")
        }
    }

    # Create VM using the above VHD
    foreach($Name in $VMName)
    {
        xVMHyperV "VMachine$Name"
        {
            Ensure = "Present"
            Name = $Name
            VhDPath = (Join-Path -Path $VHDPath -ChildPath $Name)
            SwitchName = $SwitchName
            StartupMemory = $VMStartupMemory
            State = $VMState
            MACAddress = $MACAddress
            WaitForIP = $true
            DependsOn = @("[WindowsFeature]HyperV",
                          "[xVHD]VHD$Name")
        }
    }
}
```

### <a name="saving-the-configuration-as-a-composite-resource"></a><span data-ttu-id="4130d-114">Ukládání konfigurace jako složený prostředek</span><span class="sxs-lookup"><span data-stu-id="4130d-114">Saving the configuration as a composite resource</span></span>

<span data-ttu-id="4130d-115">Použití parametrizovaného konfigurace jako prostředek DSC, uložte ho do struktury adresářů stejně jako u jakéhokoli jiného prostředku založený na souboru MOF a pojmenujte ho s **. schema.psm1** rozšíření.</span><span class="sxs-lookup"><span data-stu-id="4130d-115">To use the parameterized configuration as a DSC resource, save it in a directory structure like that of any other MOF-based resource, and name it with a **.schema.psm1** extension.</span></span> <span data-ttu-id="4130d-116">V tomto příkladu jsme vám název souboru **xVirtualMachine.schema.psm1**.</span><span class="sxs-lookup"><span data-stu-id="4130d-116">For this example, we’ll name the file **xVirtualMachine.schema.psm1**.</span></span> <span data-ttu-id="4130d-117">Budete potřebovat k vytvoření manifestu s názvem **xVirtualMachine.psd1** , který obsahuje následující řádek.</span><span class="sxs-lookup"><span data-stu-id="4130d-117">You also need to create a manifest named **xVirtualMachine.psd1** that contains the following line.</span></span> <span data-ttu-id="4130d-118">Všimněte si, že to je navíc k **MyDscResources.psd1**, manifestu modulu pro všechny prostředky v rámci **MyDscResources** složky.</span><span class="sxs-lookup"><span data-stu-id="4130d-118">Note that this is in addition to **MyDscResources.psd1**, the module manifest for all resources under the **MyDscResources** folder.</span></span>

```powershell
RootModule = 'xVirtualMachine.schema.psm1'
```

<span data-ttu-id="4130d-119">Jakmile budete hotovi, struktura složek by měl vypadat takto.</span><span class="sxs-lookup"><span data-stu-id="4130d-119">When you are done, the folder structure should be as follows.</span></span>

```
$env: psmodulepath
    |- MyDscResources
           MyDscResources.psd1
        |- DSCResources
            |- xVirtualMachine
                |- xVirtualMachine.psd1
                |- xVirtualMachine.schema.psm1
```

<span data-ttu-id="4130d-120">Prostředek je nyní zjistitelné pomocí rutiny Get-DscResource a její vlastnosti jsou zjistitelné buď rutinu nebo pomocí **kombinace kláves Ctrl + mezerník** automatického dokončování v prostředí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="4130d-120">The resource is now discoverable by using the Get-DscResource cmdlet, and its properties are discoverable by either that cmdlet or by using **Ctrl+Space** auto-complete in the Windows PowerShell ISE.</span></span>

## <a name="using-the-composite-resource"></a><span data-ttu-id="4130d-121">Pomocí složených prostředků</span><span class="sxs-lookup"><span data-stu-id="4130d-121">Using the composite resource</span></span>

<span data-ttu-id="4130d-122">Vytvoříme další konfiguraci, která volá složený prostředek.</span><span class="sxs-lookup"><span data-stu-id="4130d-122">Next we create a configuration that calls the composite resource.</span></span> <span data-ttu-id="4130d-123">Tato konfigurace volá xVirtualMachine složený prostředek pro vytvoření virtuálního počítače a pak zavolá **xComputer** prostředků ji budete chtít přejmenovat.</span><span class="sxs-lookup"><span data-stu-id="4130d-123">This configuration calls the xVirtualMachine composite resource to create a virtual machine, and then calls the **xComputer** resource to rename it.</span></span>

```powershell

configuration RenameVM
{

    Import-DscResource -Module xVirtualMachine
    Node localhost
    {
        xVirtualMachine VM
        {
            VMName = "Test"
            SwitchName = "Internal"
            SwitchType = "Internal"
            VhdParentPath = "C:\Demo\VHD\RTM.vhd"
            VHDPath = "C:\Demo\VHD"
            VMStartupMemory = 1024MB
            VMState = "Running"
        }
    }

    Node "192.168.10.1"
    {
        xComputer Name
        {
            Name = "SQL01"
            DomainName = "fourthcoffee.com"
        }
    }
}
```

## <a name="supporting-psdscrunascredential"></a><span data-ttu-id="4130d-124">Podpora PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="4130d-124">Supporting PsDscRunAsCredential</span></span>

><span data-ttu-id="4130d-125">**Poznámka:** **PsDscRunAsCredential** je podporován v Powershellu 5.0 a novějším.</span><span class="sxs-lookup"><span data-stu-id="4130d-125">**Note:** **PsDscRunAsCredential** is supported in PowerShell 5.0 and later.</span></span>

<span data-ttu-id="4130d-126">**PsDscRunAsCredential** vlastnost lze použít v [konfigurací DSC](../configurations/configurations.md) prostředků bloku k určení, prostředku by měl být spuštěny pod zadanou sadu přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="4130d-126">The **PsDscRunAsCredential** property can be used in [DSC configurations](../configurations/configurations.md) resource block to specify that the resource should be run under a specified set of credentials.</span></span>
<span data-ttu-id="4130d-127">Další informace najdete v tématu [DSC spuštěná s pověřeními uživatele](../configurations/runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="4130d-127">For more information, see [Running DSC with user credentials](../configurations/runAsUser.md).</span></span>

<span data-ttu-id="4130d-128">Pro přístup k uživatelský kontext z v rámci vlastní prostředek, můžete použít automatické proměnné `$PsDscContext`.</span><span class="sxs-lookup"><span data-stu-id="4130d-128">To access the user context from within a custom resource, you can use the automatic variable `$PsDscContext`.</span></span>

<span data-ttu-id="4130d-129">Například následující kód by zápisu uživatelský kontext, ve kterém prostředek běží podrobné výstupního datového proudu:</span><span class="sxs-lookup"><span data-stu-id="4130d-129">For example the following code would write the user context under which the resource is running to the verbose output stream:</span></span>

```powershell
if ($PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a><span data-ttu-id="4130d-130">Viz také</span><span class="sxs-lookup"><span data-stu-id="4130d-130">See Also</span></span>
### <a name="concepts"></a><span data-ttu-id="4130d-131">Koncepty</span><span class="sxs-lookup"><span data-stu-id="4130d-131">Concepts</span></span>
* [<span data-ttu-id="4130d-132">Psaní vlastních prostředků DSC s MOF</span><span class="sxs-lookup"><span data-stu-id="4130d-132">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
* [<span data-ttu-id="4130d-133">Začínáme s Windows PowerShell Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="4130d-133">Get Started with Windows PowerShell Desired State Configuration</span></span>](../overview/overview.md)