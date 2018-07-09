---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Použití uživatelských přihlašovacích údajů ke spuštění DSC
ms.openlocfilehash: 4a6c3d8b561cd0a27be07a68f1b577f7bf764254
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893901"
---
# <a name="running-dsc-with-user-credentials"></a><span data-ttu-id="574fd-103">Použití uživatelských přihlašovacích údajů ke spuštění DSC</span><span class="sxs-lookup"><span data-stu-id="574fd-103">Running DSC with user credentials</span></span>

> <span data-ttu-id="574fd-104">Platí pro: Windows PowerShell 5.0, prostředí Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="574fd-104">Applies To: Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="574fd-105">Prostředek DSC pod zadanou sadu přihlašovacích údajů můžete spustit pomocí automatického **PsDscRunAsCredential** vlastnosti v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="574fd-105">You can run a DSC resource under a specified set of credentials by using the automatic **PsDscRunAsCredential** property in the configuration.</span></span>
<span data-ttu-id="574fd-106">Ve výchozím nastavení spouští DSC jednotlivé prostředky jako systémový účet.</span><span class="sxs-lookup"><span data-stu-id="574fd-106">By default, DSC runs each resource as the system account.</span></span>
<span data-ttu-id="574fd-107">Existují situace, kdy spuštěn jako uživatel je nezbytné, jako je například instalace balíčky MSI v kontextu konkrétní uživatele, nastavení klíče registru, přístup ke konkrétní místní adresář uživatele nebo přístup k síti sdílet.</span><span class="sxs-lookup"><span data-stu-id="574fd-107">There are times when running as a user is necessary, such as installing MSI packages in a specific user context, setting a user's registry keys, accessing a user's specific local directory, or accessing a network share.</span></span>

<span data-ttu-id="574fd-108">Má každý prostředek DSC **PsDscRunAsCredential** vlastnost, která může být nastaven na žádné přihlašovací údaje uživatele ( [PSCredential](/dotnet/api/system.management.automation.pscredential) objekt).</span><span class="sxs-lookup"><span data-stu-id="574fd-108">Every DSC resource has a **PsDscRunAsCredential** property that can be set to any user credentials (a [PSCredential](/dotnet/api/system.management.automation.pscredential) object).</span></span>
<span data-ttu-id="574fd-109">Přihlašovací údaje, které mohou být pevně zakódovaný jako hodnota vlastnosti v konfiguraci, nebo nastavte hodnotu na [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential), který se zobrazí výzva pro pověření při kompilaci (informace o konfiguraci kompilace konfigurací, naleznete v tématu [konfigurace](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="574fd-109">The credential can be hard-coded as the value of the property in the configuration, or you can set the value to [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential), which will prompt the user for a credential when the configuration is compiled (for information about compiling configurations, see [Configurations](configurations.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="574fd-110">V Powershellu 5.0, pomocí **PsDscRunAsCredential** nepodporuje vlastnost v konfiguracích volání složené prostředky.</span><span class="sxs-lookup"><span data-stu-id="574fd-110">In PowerShell 5.0, using the **PsDscRunAsCredential** property in configurations calling composite resources was not supported.</span></span>
> <span data-ttu-id="574fd-111">V prostředí PowerShell 5.1 **PsDscRunAsCredential** vlastnost je podporována v konfiguracích volání složené prostředky.</span><span class="sxs-lookup"><span data-stu-id="574fd-111">In PowerShell 5.1, the **PsDscRunAsCredential** property is supported in configurations calling composite resources.</span></span>
> <span data-ttu-id="574fd-112">**PsDscRunAsCredential** vlastnost není k dispozici v Powershellu 4.0.</span><span class="sxs-lookup"><span data-stu-id="574fd-112">The **PsDscRunAsCredential** property is not available in PowerShell 4.0.</span></span>

<span data-ttu-id="574fd-113">V následujícím příkladu `Get-Credential` slouží k výzva k zadání přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="574fd-113">In the following example, `Get-Credential` is used to prompt the user for credentials.</span></span>
<span data-ttu-id="574fd-114">[Registru](registryResource.md) prostředků se používá ke změně klíče registru, který určuje barvu pozadí okna příkazového řádku Windows.</span><span class="sxs-lookup"><span data-stu-id="574fd-114">The [Registry](registryResource.md) resource is used to change the registry key that specifies the background color for the Windows command prompt window.</span></span>

```powershell
Configuration ChangeCmdBackGroundColor
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        Registry CmdPath
        {
            Key                  = 'HKEY_CURRENT_USER\SOFTWARE\Microsoft\Command Processor'
            ValueName            = 'DefaultColor'
            ValueData            = '1F'
            ValueType            = 'DWORD'
            Ensure               = 'Present'
            Force                = $true
            Hex                  = $true
            PsDscRunAsCredential = Get-Credential
        }
    }
}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost';
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}

ChangeCmdBackGroundColor -ConfigurationData $configData
```

> [!NOTE]
> <span data-ttu-id="574fd-115">Tento příklad předpokládá, že máte platný certifikát na `C:\publicKeys\targetNode.cer`, a se zobrazenou hodnotu kryptografického otisku certifikátu.</span><span class="sxs-lookup"><span data-stu-id="574fd-115">This example assumes that you have a valid certificate at `C:\publicKeys\targetNode.cer`, and that the thumbprint of that certificate is the value shown.</span></span>
> <span data-ttu-id="574fd-116">Informace o šifrování přihlašovacích údajů v konfiguračních souborech MOF na DSC najdete v tématu [zabezpečení souboru MOF](secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="574fd-116">For information about encrypting credentials in DSC configuration MOF files, see [Securing the MOF file](secureMOF.md).</span></span>
