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
# <a name="composite-resources-using-a-dsc-configuration-as-a-resource"></a>Složené prostředky: Pomocí konfigurace DSC jako prostředek

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

V reálných situacích může být konfigurace dlouhá a složitá, volání mnoho různých prostředků a nastavení rozsáhlé počet vlastností. Pomáhají řešit Tato složitost, můžete použít Windows PowerShell Desired State Configuration (DSC) konfigurace jako prostředek pro další konfigurace. To označujeme složený prostředek. Složený prostředek je konfigurace DSC, která přebírá parametry. Parametry konfigurace fungovat jako vlastností prostředku. Konfigurace je uložen jako soubor s **. schema.psm1** rozšíření a přijímá místo schématu MOF a prostředek skriptu v typické prostředku DSC (Další informace o prostředcích DSC najdete v tématu [Windows Prostředí PowerShell Desired State Configuration prostředky](resources.md).

## <a name="creating-the-composite-resource"></a>Vytváření složených prostředků

V našem příkladu jsme vytvořit konfiguraci, která volá počet stávajících prostředků, abyste konfiguraci virtuálních počítačů. Místo určení hodnoty, které mají být nastavené v blocích konfigurace, konfigurace přijímá několik parametrů, které se následně použijí v blocích konfigurace.

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

Použití parametrizovaného konfigurace jako prostředek DSC, uložte ho do struktury adresářů stejně jako u jakéhokoli jiného prostředku založený na souboru MOF a pojmenujte ho s **. schema.psm1** rozšíření. V tomto příkladu jsme vám název souboru **xVirtualMachine.schema.psm1**. Budete potřebovat k vytvoření manifestu s názvem **xVirtualMachine.psd1** , který obsahuje následující řádek. Všimněte si, že to je navíc k **MyDscResources.psd1**, manifestu modulu pro všechny prostředky v rámci **MyDscResources** složky.

```powershell
RootModule = 'xVirtualMachine.schema.psm1'
```

Jakmile budete hotovi, struktura složek by měl vypadat takto.

```
$env: psmodulepath
    |- MyDscResources
           MyDscResources.psd1
        |- DSCResources
            |- xVirtualMachine
                |- xVirtualMachine.psd1
                |- xVirtualMachine.schema.psm1
```

Prostředek je nyní zjistitelné pomocí rutiny Get-DscResource a její vlastnosti jsou zjistitelné buď rutinu nebo pomocí **kombinace kláves Ctrl + mezerník** automatického dokončování v prostředí Windows PowerShell ISE.

## <a name="using-the-composite-resource"></a>Pomocí složených prostředků

Vytvoříme další konfiguraci, která volá složený prostředek. Tato konfigurace volá xVirtualMachine složený prostředek pro vytvoření virtuálního počítače a pak zavolá **xComputer** prostředků ji budete chtít přejmenovat.

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

>**Poznámka:** **PsDscRunAsCredential** je podporován v Powershellu 5.0 a novějším.

**PsDscRunAsCredential** vlastnost lze použít v [konfigurací DSC](../configurations/configurations.md) prostředků bloku k určení, prostředku by měl být spuštěny pod zadanou sadu přihlašovacích údajů.
Další informace najdete v tématu [DSC spuštěná s pověřeními uživatele](../configurations/runAsUser.md).

Pro přístup k uživatelský kontext z v rámci vlastní prostředek, můžete použít automatické proměnné `$PsDscContext`.

Například následující kód by zápisu uživatelský kontext, ve kterém prostředek běží podrobné výstupního datového proudu:

```powershell
if ($PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a>Viz také
### <a name="concepts"></a>Koncepty
* [Psaní vlastních prostředků DSC s MOF](authoringResourceMOF.md)
* [Začínáme s Windows PowerShell Desired State Configuration](../overview/overview.md)