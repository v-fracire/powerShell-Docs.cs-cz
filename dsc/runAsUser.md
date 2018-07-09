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
# <a name="running-dsc-with-user-credentials"></a>Použití uživatelských přihlašovacích údajů ke spuštění DSC

> Platí pro: Windows PowerShell 5.0, prostředí Windows PowerShell 5.1

Prostředek DSC pod zadanou sadu přihlašovacích údajů můžete spustit pomocí automatického **PsDscRunAsCredential** vlastnosti v konfiguraci.
Ve výchozím nastavení spouští DSC jednotlivé prostředky jako systémový účet.
Existují situace, kdy spuštěn jako uživatel je nezbytné, jako je například instalace balíčky MSI v kontextu konkrétní uživatele, nastavení klíče registru, přístup ke konkrétní místní adresář uživatele nebo přístup k síti sdílet.

Má každý prostředek DSC **PsDscRunAsCredential** vlastnost, která může být nastaven na žádné přihlašovací údaje uživatele ( [PSCredential](/dotnet/api/system.management.automation.pscredential) objekt).
Přihlašovací údaje, které mohou být pevně zakódovaný jako hodnota vlastnosti v konfiguraci, nebo nastavte hodnotu na [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential), který se zobrazí výzva pro pověření při kompilaci (informace o konfiguraci kompilace konfigurací, naleznete v tématu [konfigurace](configurations.md).

> [!NOTE] 
> V Powershellu 5.0, pomocí **PsDscRunAsCredential** nepodporuje vlastnost v konfiguracích volání složené prostředky.
> V prostředí PowerShell 5.1 **PsDscRunAsCredential** vlastnost je podporována v konfiguracích volání složené prostředky.
> **PsDscRunAsCredential** vlastnost není k dispozici v Powershellu 4.0.

V následujícím příkladu `Get-Credential` slouží k výzva k zadání přihlašovacích údajů.
[Registru](registryResource.md) prostředků se používá ke změně klíče registru, který určuje barvu pozadí okna příkazového řádku Windows.

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
> Tento příklad předpokládá, že máte platný certifikát na `C:\publicKeys\targetNode.cer`, a se zobrazenou hodnotu kryptografického otisku certifikátu.
> Informace o šifrování přihlašovacích údajů v konfiguračních souborech MOF na DSC najdete v tématu [zabezpečení souboru MOF](secureMOF.md).
