---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Přihlašovací údaje uživatele s DSC"
ms.openlocfilehash: 7b57732679e4fb29112a3ca7fe64cba2bda67207
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="running-dsc-with-user-credentials"></a><span data-ttu-id="15058-103">Přihlašovací údaje uživatele s DSC</span><span class="sxs-lookup"><span data-stu-id="15058-103">Running DSC with user credentials</span></span> 

> <span data-ttu-id="15058-104">Platí pro: Prostředí Windows PowerShell 5.0, 5.1 prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="15058-104">Applies To: Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="15058-105">Prostředek DSC pod zadanou sadu přihlašovacích údajů můžete spustit pomocí automatického **PsDscRunAsCredential** vlastnosti v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="15058-105">You can run a DSC resource under a specified set of credentials by using the automatic **PsDscRunAsCredential** property in the configuration.</span></span> <span data-ttu-id="15058-106">Ve výchozím nastavení spouští DSC každý prostředek, jako systémový účet.</span><span class="sxs-lookup"><span data-stu-id="15058-106">By default, DSC runs each resource as the system account.</span></span>
<span data-ttu-id="15058-107">Existují situace, kdy spuštěná jako uživatel je nezbytné, například instalaci balíčky MSI v kontextu konkrétního uživatele, nastavení klíče registru uživatele, přístup k určité místní adresáře uživatele nebo přístup k síti sdílet.</span><span class="sxs-lookup"><span data-stu-id="15058-107">There are times when running as a user is necessary, such as installing MSI packages in a specific user context, setting a user's registry keys, accessing a user's specific local directory, or accessing a network share.</span></span>

<span data-ttu-id="15058-108">Má každý prostředek DSC **PsDscRunAsCredential** vlastnost, která může být nastaven na všechny přihlašovací údaje uživatele ( [PSCredential](https://msdn.microsoft.com/en-us/library/ms572524(v=VS.85).aspx) objekt).</span><span class="sxs-lookup"><span data-stu-id="15058-108">Every DSC resource has a **PsDscRunAsCredential** property that can be set to any user credentials (a [PSCredential](https://msdn.microsoft.com/en-us/library/ms572524(v=VS.85).aspx) object).</span></span>
<span data-ttu-id="15058-109">Přihlašovací údaje mohou být pevně zakódované jako hodnota vlastnosti v konfiguraci, nebo nastavte hodnotu na [Get-Credential](https://technet.microsoft.com/en-us/library/hh849815.aspx), který se zobrazí výzva pro pověření při kompilaci (pro informace o konfiguraci kompilování konfigurace, najdete v části [konfigurace](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="15058-109">The credential can be hard-coded as the value of the property in the configuration, or you can set the value to [Get-Credential](https://technet.microsoft.com/en-us/library/hh849815.aspx), which will prompt the user for a credential when the configuration is compiled (for information about compiling configurations, see [Configurations](configurations.md).</span></span>

><span data-ttu-id="15058-110">**Poznámka:** v prostředí PowerShell 5.0, pomocí **PsDscRunAsCredential** vlastnost v konfiguracích volání složené prostředků nebyla podporována.</span><span class="sxs-lookup"><span data-stu-id="15058-110">**Note:** In PowerShell 5.0, using the **PsDscRunAsCredential** property in configurations calling composite resources was not supported.</span></span> 
><span data-ttu-id="15058-111">V prostředí PowerShell 5.1 **PsDscRunAsCredential** vlastnost je podporována v konfiguracích volání složené prostředky.</span><span class="sxs-lookup"><span data-stu-id="15058-111">In PowerShell 5.1, the **PsDscRunAsCredential** property is supported in configurations calling composite resources.</span></span>

><span data-ttu-id="15058-112">**Poznámka:** **PsDscRunAsCredential** vlastnost není k dispozici v prostředí PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="15058-112">**Note:** The **PsDscRunAsCredential** property is not available in PowerShell 4.0.</span></span>

<span data-ttu-id="15058-113">V následujícím příkladu **Get-Credential** se používá k vyzvat uživatele k zadání přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="15058-113">In the following example, **Get-Credential** is used to prompt the user for credentials.</span></span> <span data-ttu-id="15058-114">[Registru](registryResource.md) prostředků se používá ke změně klíč registru, který určuje barvu pozadí pro okno příkazového řádku systému Windows.</span><span class="sxs-lookup"><span data-stu-id="15058-114">The [Registry](registryResource.md) resource is used to change the registry key that specifies the background color for the Windows command prompt window.</span></span>

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
><span data-ttu-id="15058-115">**Poznámka:** tento příklad předpokládá, že máte platný certifikát v `C:\publicKeys\targetNode.cer`, a že kryptografický otisk certifikátu je hodnota použitá.</span><span class="sxs-lookup"><span data-stu-id="15058-115">**Note:** This example assumes that you have a valid certificate at `C:\publicKeys\targetNode.cer`, and that the thumbprint of that certificate is the value shown.</span></span>
><span data-ttu-id="15058-116">Informace o šifrování pověření v souborech MOF konfigurace DSC najdete v tématu [zabezpečení souboru MOF](secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="15058-116">For information about encrypting credentials in DSC configuration MOF files, see [Securing the MOF file](secureMOF.md).</span></span>

