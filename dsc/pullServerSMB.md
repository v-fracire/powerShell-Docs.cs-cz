---
ms.date: 04/11/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Nastavení serveru vyžádané replikace SMB pro DSC
ms.openlocfilehash: 1eac6c51aeca3ed573ba8fa27188103436004920
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892861"
---
# <a name="setting-up-a-dsc-smb-pull-server"></a>Nastavení serveru vyžádané replikace SMB pro DSC

Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

> [!IMPORTANT]
> Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce. Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).

DSC [SMB](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831795(v=ws.11)) serveru vyžádané replikace je počítač hostující sdílené složky SMB, které zpřístupnit DSC konfigurační soubory a prostředky DSC cílové uzly při těchto uzlů požádat o nich.

Chcete-li použít serveru vyžádané replikace SMB pro DSC, budete muset:

- Nastavení sdílené složky protokolu SMB na serveru se systémem Powershellu 4.0 nebo vyšší
- Konfigurace klienta, spouštění prostředí PowerShell 4.0 nebo vyšší na vyžádání z této sdílené složky SMB

## <a name="using-the-xsmbshare-resource-to-create-an-smb-file-share"></a>Použití xSmbShare prostředků k vytvoření sdílené složky protokolu SMB

Existuje mnoho způsobů, jak nastavit sdílenou složku SMB, ale podívejme se na tom, jak to provést pomocí DSC.

### <a name="install-the-xsmbshare-resource"></a>Nainstalujte xSmbShare prostředků

Volání [Install-Module](/powershell/module/PowershellGet/Install-Module) rutinu instalace **xSmbShare** modulu.

> [!NOTE]
> `Install-Module` je součástí **PowerShellGet** modulu, která je obsažena v Powershellu 5.0. Můžete stáhnout **PowerShellGet** modulu pro PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).
> **XSmbShare** obsahuje prostředek DSC **xSmbShare**, který slouží k vytvoření sdílené složky SMB.

### <a name="create-the-directory-and-file-share"></a>Vytvoření sdílené složky adresáře a souboru

Následující konfigurace se používá [souboru](fileResource.md) prostředek pro vytvoření sdílené složky v adresáři a **xSmbShare** prostředků nastavení sdílené složky SMB:

```powershell
Configuration SmbShare
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Import-DscResource -ModuleName xSmbShare

    Node localhost
    {

        File CreateFolder
        {
            DestinationPath = 'C:\DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'
        }

        xSMBShare CreateShare
        {
            Name = 'DscSmbShare'
            Path = 'C:\DscSmbShare'
            FullAccess = 'admininstrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'
        }
    }
}
```

Konfigurace vytvoří adresář `C:\DscSmbShare` Pokud zatím již existuje a použije tento adresář jako sdílené složky protokolu SMB. **FullAccess** by měla být věnována libovolný účet, který se musí zapisovat nebo odstranit ze sdílené složky a **oprávnění ke čtení** musí předávat žádné uzly klienta, které si mohli služby konfigurace a prostředky DSC ze sdílené složky (totiž DSC jako systémový účet ve výchozím nastavení spustí, takže přímo počítač musí mít přístup ke sdílené složce).

### <a name="give-file-system-access-to-the-pull-client"></a>Poskytnout přístup systému souborů k načítacího klienta

Poskytuje **oprávnění ke čtení** klientovi uzel umožňuje přístup ke sdílené složce protokolu SMB, ale ne na soubory nebo složky, které sdílejí tento uzel. Je nutné explicitně udělit klienta uzlům přístup do sdílené složky protokolu SMB a podsložky. Můžeme to udělat pomocí DSC tak, že přidáte pomocí **cNtfsPermissionEntry** prostředek, který je součástí [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) modulu. V následující konfiguraci přidáte **cNtfsPermissionEntry** blok, který uděluje přístup ReadAndExecute načítacího klienta:

```powershell
Configuration DSCSMB
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Import-DscResource -ModuleName xSmbShare
    Import-DscResource -ModuleName cNtfsAccessControl

    Node localhost
    {

        File CreateFolder
        {
            DestinationPath = 'DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'
        }

        xSMBShare CreateShare
        {
            Name = 'DscSmbShare'
            Path = 'DscSmbShare'
            FullAccess = 'administrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'
        }

        cNtfsPermissionEntry PermissionSet1
        {
            Ensure = 'Present'
            Path = 'C:\DSCSMB'
            Principal = 'myDomain\Contoso-Server$'
            AccessControlInformation = @(
                cNtfsAccessControlInformation
                {
                    AccessControlType = 'Allow'
                    FileSystemRights = 'ReadAndExecute'
                    Inheritance = 'ThisFolderSubfoldersAndFiles'
                    NoPropagateInherit = $false
                }
            )
            DependsOn = '[File]CreateFolder'
        }
    }
}
```

## <a name="placing-configurations-and-resources"></a>Uvedení konfigurací a prostředků

Uložte konfigurační soubory MOF a/nebo prostředky DSC, které mají klienta uzly, aby se načetla sdílenou složku SMB.

Musí mít název konfiguračního souboru MOF *ConfigurationID*.mof, kde *ConfigurationID* je hodnota **ConfigurationID** vlastnost LCM cílový uzel. Další informace o nastavení klientů o přijetí změn najdete v tématu [nastavení načítacího klienta použití konfiguračních identifikátorů](pullClientConfigID.md).

> [!NOTE]
> Pokud používáte serveru vyžádané replikace SMB je nutné použít ID konfigurace. Názvy konfigurace nejsou podporovány pro protokolu SMB.

Každý modul prostředků musí být metoda ZIP a s názvem podle následující vzor `{Module Name}_{Module Version}.zip`. Například modul s názvem xWebAdminstration s verzí modulu 3.1.2.0 by se pojmenoval "xWebAdministration_3.2.1.0.zip". Každá verze modulu musí být součástí jedné zip soubor. Vzhledem k tomu, že existuje pouze jedna verze prostředku v každém souboru zip formát modulu přidáno ve WMF 5.0 s více verzí modulu v jednom adresáři není podporované. To znamená, že před zabalení moduly prostředků DSC pro použití se serverem o přijetí změn je potřeba proveďte malou změnu do struktury adresářů. Je výchozí formát pro moduly obsahující prostředek DSC ve WMF 5.0 `{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\`. Před balení do serveru vyžádané replikace jednoduše odebrat `{Module version}` složku, cesta bude `{Module Folder}\DscResources\{DSC Resource Folder}\`. Díky této změně složky zip, jak je popsáno výše a umístí tyto souboru zip do sdílené složky SMB.

## <a name="creating-the-mof-checksum"></a>Vytváří se kontrolní součet MOF

Konfiguračního souboru MOF musí být párována s typem kontrolního součtu souboru tak, aby LCM na cílový uzel můžete konfiguraci ověřit.
Chcete-li vytvořit kontrolní součet, zavolejte [New-DSCCheckSum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum) rutiny. Přijímá rutina `Path` parametr, který určuje složku, ve kterém se nachází konfigurační soubor MOF. Rutina vytvoří kontrolní součet souboru s názvem `ConfigurationMOFName.mof.checksum`, kde `ConfigurationMOFName` je název konfiguračního souboru mof.
Pokud existuje více než jednu konfiguraci soubory MOF v zadané složce, kontrolní součet se vytvoří pro každou konfiguraci ve složce.

Kontrolní součet souboru musí být ve stejném adresáři jako konfigurační soubor MOF (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` ve výchozím nastavení), a mít stejný název `.checksum` připojenou příponou.

> [!NOTE]
> Pokud změníte konfiguračního souboru MOF žádným způsobem, je nutné znovu vytvořit kontrolní součet souboru.

## <a name="setting-up-a-pull-client-for-smb"></a>Nastavení načítacího klienta pro SMB

Nastavení klienta, který si vyžádá konfigurace a/nebo prostředky z do sdílené složky SMB, můžete nakonfigurovat klienta místní Configuration Manageru (LCM) s **ConfigurationRepositoryShare** a **ResourceRepositoryShare** bloky, které určují sdílenou složku, ze kterého chcete o přijetí změn konfigurace a prostředky DSC.

Další informace týkající se konfigurace LCM v tématu [nastavení načítacího klienta použití konfiguračních identifikátorů](pullClientConfigID.md).

> [!NOTE]
> Pro zjednodušení tento příklad používá **PSDscAllowPlainTextPassword** umožňuje předání hesla ve formátu prostého textu **přihlašovacích údajů** parametru. Informace o předávání přihlašovacích údajů bezpečněji, naleznete v tématu [možnosti přihlašovacích údajů v konfiguračních datech](configDataCredentials.md).
>
> Můžete **musí** zadat **ConfigurationID** v **nastavení** bloku metaconfiguration pro serveru vyžádané replikace SMB, i když jsou pouze souhrnné informace prostředky.

```powershell
$secpasswd = ConvertTo-SecureString “Pass1Word” -AsPlainText -Force
$mycreds = New-Object System.Management.Automation.PSCredential (“TestUser”, $secpasswd)

[DSCLocalConfigurationManager()]
configuration SmbCredTest
{
    Node $AllNodes.NodeName
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
            ConfigurationID    = '16db7357-9083-4806-a80c-ebbaf4acd6c1'
        }

         ConfigurationRepositoryShare SmbConfigShare
        {
            SourcePath = '\\WIN-E0TRU6U11B1\DscSmbShare'
            Credential = $mycreds
        }

        ResourceRepositoryShare SmbResourceShare
        {
            SourcePath = '\\WIN-E0TRU6U11B1\DscSmbShare'
            Credential = $mycreds

        }
    }
}

$ConfigurationData = @{
    AllNodes = @(
        @{
            #the "*" means "all nodes named in ConfigData" so we don't have to repeat ourselves
            NodeName="localhost"
            PSDscAllowPlainTextPassword = $true
        })
}
```

## <a name="acknowledgements"></a>Poděkování

Speciální díky následující:

- Mike F. Robbins, jehož příspěvky na použití protokolu SMB pro DSC pomohla informovat obsah v tomto tématu. Jeho blogu je na [Mike F Robbins](http://mikefrobbins.com/).
- Serge Nikalaichyk, kdo vytvořil **cNtfsAccessControl** modulu. Zdroj pro tento modul je na [cNtfsAccessControl](https://github.com/SNikalaichyk/cNtfsAccessControl).

## <a name="see-also"></a>Viz taky

[Prostředí Windows PowerShell Desired State Configuration – přehled](overview.md)

[Přijetí konfigurace](enactingConfigurations.md)

[Použití konfiguračních identifikátorů k nastavení načítacího klienta](pullClientConfigID.md)