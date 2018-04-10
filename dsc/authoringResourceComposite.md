---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Složené prostředků – pomocí konfigurace DSC jako prostředek
ms.openlocfilehash: c89293fdbe9bc054a47cc6974b6bd0471f727f46
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="composite-resources-using-a-dsc-configuration-as-a-resource"></a><span data-ttu-id="d6553-103">Složené prostředky: použití konfigurace DSC jako prostředek</span><span class="sxs-lookup"><span data-stu-id="d6553-103">Composite resources: Using a DSC configuration as a resource</span></span>

> <span data-ttu-id="d6553-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="d6553-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="d6553-105">V situacích, reálného může stát konfigurace dlouhá a složitá, volání mnoha různými prostředky a nastavení velká počet vlastností.</span><span class="sxs-lookup"><span data-stu-id="d6553-105">In real-world situations, configurations can become long and complex, calling many different resources and setting a vast number of properties.</span></span> <span data-ttu-id="d6553-106">K vám budou snadněji řešit tento složitost, můžete konfiguraci požadovaného stavu aplikace Windows PowerShell (DSC) jako prostředek pro ostatní konfigurace.</span><span class="sxs-lookup"><span data-stu-id="d6553-106">To help address this complexity, you can use a Windows PowerShell Desired State Configuration (DSC) configuration as a resource for other configurations.</span></span> <span data-ttu-id="d6553-107">Říkáme to složené prostředků.</span><span class="sxs-lookup"><span data-stu-id="d6553-107">We call this a composite resource.</span></span> <span data-ttu-id="d6553-108">Složené prostředek je konfigurace DSC, která přebírá parametry.</span><span class="sxs-lookup"><span data-stu-id="d6553-108">A composite resource is a DSC configuration that takes parameters.</span></span> <span data-ttu-id="d6553-109">Parametry konfigurace fungovat jako vlastnosti prostředku.</span><span class="sxs-lookup"><span data-stu-id="d6553-109">The parameters of the configuration act as the properties of the resource.</span></span> <span data-ttu-id="d6553-110">Konfigurace je uloženo jako soubor s **. schema.psm1** rozšíření a trvá místo schéma MOF a prostředek skript v typické prostředek DSC (Další informace o prostředcích DSC najdete v tématu [Windows Prostředí PowerShell Desired State Configuration prostředky](resources.md).</span><span class="sxs-lookup"><span data-stu-id="d6553-110">The configuration is saved as a file with a **.schema.psm1** extension, and takes the place of both the MOF schema and the resource script in a typical DSC resource (for more information about DSC resources, see [Windows PowerShell Desired State Configuration Resources](resources.md).</span></span>

## <a name="creating-the-composite-resource"></a><span data-ttu-id="d6553-111">Vytváření složených prostředků</span><span class="sxs-lookup"><span data-stu-id="d6553-111">Creating the composite resource</span></span>

<span data-ttu-id="d6553-112">V našem příkladu vytvoříme konfigurace, která volá počet stávajících prostředků ke konfiguraci virtuálních počítačů.</span><span class="sxs-lookup"><span data-stu-id="d6553-112">In our example, we create a configuration that invokes a number of existing resources to configure virtual machines.</span></span> <span data-ttu-id="d6553-113">Místo zadání hodnoty, které mají být nastavena v konfiguraci bloky, konfigurace trvá několik parametrů, které jsou pak použito v blocích konfigurace.</span><span class="sxs-lookup"><span data-stu-id="d6553-113">Instead of specifying the values to be set in configuration blocks, the configuration takes a number of parameters that are then used in the configuration blocks.</span></span>

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

### <a name="saving-the-configuration-as-a-composite-resource"></a><span data-ttu-id="d6553-114">Ukládání konfigurace jako složený prostředek</span><span class="sxs-lookup"><span data-stu-id="d6553-114">Saving the configuration as a composite resource</span></span>

<span data-ttu-id="d6553-115">Použití parametrizovaného konfigurace jako prostředek DSC, uložte ho do struktury adresářů jako u jiných na základě MOF prostředků a pojmenujte ji s **. schema.psm1** rozšíření.</span><span class="sxs-lookup"><span data-stu-id="d6553-115">To use the parameterized configuration as a DSC resource, save it in a directory structure like that of any other MOF-based resource, and name it with a **.schema.psm1** extension.</span></span> <span data-ttu-id="d6553-116">V tomto příkladu jsme budete název souboru **xVirtualMachine.schema.psm1**.</span><span class="sxs-lookup"><span data-stu-id="d6553-116">For this example, we’ll name the file **xVirtualMachine.schema.psm1**.</span></span> <span data-ttu-id="d6553-117">Budete také muset vytvoření manifestu s názvem **xVirtualMachine.psd1** obsahující následující řádek.</span><span class="sxs-lookup"><span data-stu-id="d6553-117">You also need to create a manifest named **xVirtualMachine.psd1** that contains the following line.</span></span> <span data-ttu-id="d6553-118">Všimněte si, že toto je kromě **MyDscResources.psd1**, modul manifestu pro všechny prostředky pod **MyDscResources** složky.</span><span class="sxs-lookup"><span data-stu-id="d6553-118">Note that this is in addition to **MyDscResources.psd1**, the module manifest for all resources under the **MyDscResources** folder.</span></span>

```powershell
RootModule = 'xVirtualMachine.schema.psm1'
```

<span data-ttu-id="d6553-119">Až skončíte, struktura složek by měl vypadat takto.</span><span class="sxs-lookup"><span data-stu-id="d6553-119">When you are done, the folder structure should be as follows.</span></span>

```
$env: psmodulepath
    |- MyDscResources
           MyDscResources.psd1
        |- DSCResources
            |- xVirtualMachine
                |- xVirtualMachine.psd1
                |- xVirtualMachine.schema.psm1
```

<span data-ttu-id="d6553-120">Prostředek je teď zjistitelný pomocí rutiny Get-DscResource a jeho vlastnosti jsou zjistitelný pomocí buď rutinu nebo pomocí **Ctrl + mezerník** automatického dokončování v Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="d6553-120">The resource is now discoverable by using the Get-DscResource cmdlet, and its properties are discoverable by either that cmdlet or by using **Ctrl+Space** auto-complete in the Windows PowerShell ISE.</span></span>

## <a name="using-the-composite-resource"></a><span data-ttu-id="d6553-121">Pomocí složeného prostředků</span><span class="sxs-lookup"><span data-stu-id="d6553-121">Using the composite resource</span></span>

<span data-ttu-id="d6553-122">Dále vytvoříme konfigurace, která volá složené prostředků.</span><span class="sxs-lookup"><span data-stu-id="d6553-122">Next we create a configuration that calls the composite resource.</span></span> <span data-ttu-id="d6553-123">Tato konfigurace volá xVirtualMachine složené prostředek pro vytvoření virtuálního počítače a pak zavolá **xComputer** prostředků, pokud ji chcete přejmenovat.</span><span class="sxs-lookup"><span data-stu-id="d6553-123">This configuration calls the xVirtualMachine composite resource to create a virtual machine, and then calls the **xComputer** resource to rename it.</span></span>

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

## <a name="supporting-psdscrunascredential"></a><span data-ttu-id="d6553-124">Podpora PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="d6553-124">Supporting PsDscRunAsCredential</span></span>

><span data-ttu-id="d6553-125">**Poznámka:** **PsDscRunAsCredential** je podporována v prostředí PowerShell 5.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="d6553-125">**Note:** **PsDscRunAsCredential** is supported in PowerShell 5.0 and later.</span></span>

<span data-ttu-id="d6553-126">**PsDscRunAsCredential** vlastnost lze použít v [konfigurace DSC](configurations.md) prostředků bloku určí prostředek by měl být spuštění pod zadanou sadu přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="d6553-126">The **PsDscRunAsCredential** property can be used in [DSC configurations](configurations.md) resource block to specify that the resource should be run under a specified set of credentials.</span></span>
<span data-ttu-id="d6553-127">Další informace najdete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="d6553-127">For more information, see [Running DSC with user credentials](runAsUser.md).</span></span>

<span data-ttu-id="d6553-128">Pro přístup k kontext uživatele z v rámci vlastní prostředek, můžete použít automatické proměnné `$PsDscContext`.</span><span class="sxs-lookup"><span data-stu-id="d6553-128">To access the user context from within a custom resource, you can use the automatic variable `$PsDscContext`.</span></span>

<span data-ttu-id="d6553-129">Například následující kód zapíše kontextu uživatele, pod kterým běží prostředku do datového proudu podrobný výstup:</span><span class="sxs-lookup"><span data-stu-id="d6553-129">For example the following code would write the user context under which the resource is running to the verbose output stream:</span></span>

```powershell
if ($PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a><span data-ttu-id="d6553-130">Viz také</span><span class="sxs-lookup"><span data-stu-id="d6553-130">See Also</span></span>
### <a name="concepts"></a><span data-ttu-id="d6553-131">Koncepty</span><span class="sxs-lookup"><span data-stu-id="d6553-131">Concepts</span></span>
* [<span data-ttu-id="d6553-132">Psaní vlastních prostředků DSC s MOF</span><span class="sxs-lookup"><span data-stu-id="d6553-132">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
* [<span data-ttu-id="d6553-133">Začínáme s Windows PowerShell Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="d6553-133">Get Started with Windows PowerShell Desired State Configuration</span></span>](overview.md)