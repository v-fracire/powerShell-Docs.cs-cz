---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Použití přihlašovacích údajů pomocí prostředků DSC
ms.openlocfilehash: af54c286ce744cd7db0b0e2d05087f60cdf1a33c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403811"
---
# <a name="use-credentials-with-dsc-resources"></a>Použití přihlašovacích údajů pomocí prostředků DSC

> Platí pro: Prostředí Windows PowerShell 5.0, prostředí Windows PowerShell 5.1

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
**Registru** prostředků se používá ke změně klíče registru, který určuje barvu pozadí okna příkazového řádku Windows.

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
> Informace o šifrování přihlašovacích údajů v konfiguračních souborech MOF na DSC najdete v tématu [zabezpečení souboru MOF](../pull-server/secureMOF.md).
