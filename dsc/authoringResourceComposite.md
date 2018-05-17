---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Složené prostředků – pomocí konfigurace DSC jako prostředek
ms.openlocfilehash: 246cab3b437546490d650e45be263a43fd0c84c3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="composite-resources-using-a-dsc-configuration-as-a-resource"></a>Složené prostředky: použití konfigurace DSC jako prostředek

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

V situacích, reálného může stát konfigurace dlouhá a složitá, volání mnoha různými prostředky a nastavení velká počet vlastností. K vám budou snadněji řešit tento složitost, můžete konfiguraci požadovaného stavu aplikace Windows PowerShell (DSC) jako prostředek pro ostatní konfigurace. Říkáme to složené prostředků. Složené prostředek je konfigurace DSC, která přebírá parametry. Parametry konfigurace fungovat jako vlastnosti prostředku. Konfigurace je uloženo jako soubor s **. schema.psm1** rozšíření a trvá místo schéma MOF a prostředek skript v typické prostředek DSC (Další informace o prostředcích DSC najdete v tématu [Windows Prostředí PowerShell Desired State Configuration prostředky](resources.md).

## <a name="creating-the-composite-resource"></a>Vytváření složených prostředků

V našem příkladu vytvoříme konfigurace, která volá počet stávajících prostředků ke konfiguraci virtuálních počítačů. Místo zadání hodnoty, které mají být nastavena v konfiguraci bloky, konfigurace trvá několik parametrů, které jsou pak použito v blocích konfigurace.

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

### <a name="saving-the-configuration-as-a-composite-resource"></a>Ukládání konfigurace jako složený prostředek

Použití parametrizovaného konfigurace jako prostředek DSC, uložte ho do struktury adresářů jako u jiných na základě MOF prostředků a pojmenujte ji s **. schema.psm1** rozšíření. V tomto příkladu jsme budete název souboru **xVirtualMachine.schema.psm1**. Budete také muset vytvoření manifestu s názvem **xVirtualMachine.psd1** obsahující následující řádek. Všimněte si, že toto je kromě **MyDscResources.psd1**, modul manifestu pro všechny prostředky pod **MyDscResources** složky.

```powershell
RootModule = 'xVirtualMachine.schema.psm1'
```

Až skončíte, struktura složek by měl vypadat takto.

```
$env: psmodulepath
    |- MyDscResources
           MyDscResources.psd1
        |- DSCResources
            |- xVirtualMachine
                |- xVirtualMachine.psd1
                |- xVirtualMachine.schema.psm1
```

Prostředek je teď zjistitelný pomocí rutiny Get-DscResource a jeho vlastnosti jsou zjistitelný pomocí buď rutinu nebo pomocí **Ctrl + mezerník** automatického dokončování v Windows PowerShell ISE.

## <a name="using-the-composite-resource"></a>Pomocí složeného prostředků

Dále vytvoříme konfigurace, která volá složené prostředků. Tato konfigurace volá xVirtualMachine složené prostředek pro vytvoření virtuálního počítače a pak zavolá **xComputer** prostředků, pokud ji chcete přejmenovat.

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

## <a name="supporting-psdscrunascredential"></a>Podpora PsDscRunAsCredential

>**Poznámka:** **PsDscRunAsCredential** je podporována v prostředí PowerShell 5.0 nebo novější.

**PsDscRunAsCredential** vlastnost lze použít v [konfigurace DSC](configurations.md) prostředků bloku určí prostředek by měl být spuštění pod zadanou sadu přihlašovacích údajů.
Další informace najdete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).

Pro přístup k kontext uživatele z v rámci vlastní prostředek, můžete použít automatické proměnné `$PsDscContext`.

Například následující kód zapíše kontextu uživatele, pod kterým běží prostředku do datového proudu podrobný výstup:

```powershell
if ($PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a>Viz také
### <a name="concepts"></a>Koncepty
* [Psaní vlastních prostředků DSC s MOF](authoringResourceMOF.md)
* [Začínáme s Windows PowerShell Desired State Configuration](overview.md)