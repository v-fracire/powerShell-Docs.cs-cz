---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Nastavení serveru vyžádané replikace SMB pro DSC
ms.openlocfilehash: e9228c050d6f496e30e94404a564ed2e425a5412
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="setting-up-a-dsc-smb-pull-server"></a>Nastavení serveru vyžádané replikace SMB pro DSC

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

DSC [SMB](https://technet.microsoft.com/library/hh831795.aspx) vyžádání obsahu server je počítač hostování sdílených složek SMB, které zpřístupnit DSC konfiguračních souborů a prostředků DSC pro cílové uzly při uzly, zeptejte se pro ně.

Chcete-li použít vyžádání serveru SMB pro DSC, budete muset:
- Nastavení sdílené složky SMB na serveru se systémem prostředí PowerShell 4.0 nebo vyšší
- Konfigurace klienta se systémem prostředí PowerShell 4.0 nebo vyšší načítat z této sdílené složce protokolu SMB

## <a name="using-the-xsmbshare-resource-to-create-an-smb-file-share"></a>Použití xSmbShare prostředků k vytvoření sdílené složky SMB

Existuje několik způsobů, jak nastavit sdílenou složku SMB, ale podíváme, jak můžete to provést pomocí DSC.

### <a name="install-the-xsmbshare-resource"></a>Nainstalujte xSmbShare prostředků

Volání [instalace modulu](https://technet.microsoft.com/library/dn807162.aspx) k instalaci **xSmbShare** modulu.
>**Poznámka:**: **instalace modulu** je součástí **PowerShellGet** modul, který je součástí prostředí PowerShell 5.0. Si můžete stáhnout **PowerShellGet** modul pro prostředí PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186). **XSmbShare** obsahuje prostředek DSC **xSmbShare**, který slouží k vytvoření sdílené složky SMB.

### <a name="create-the-directory-and-file-share"></a>Vytvoření sdílené složky pro adresáře a souboru

Používá následující konfigurace [soubor](fileResource.md) prostředek pro vytvoření adresáře pro sdílenou složku a **xSmbShare** prostředků nastavit sdílenou složku SMB:

```powershell
Configuration SmbShare {

Import-DscResource -ModuleName PSDesiredStateConfiguration
Import-DscResource -ModuleName xSmbShare

    Node localhost {

        File CreateFolder {

            DestinationPath = 'C:\DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'

        }

        xSMBShare CreateShare {

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

Konfigurace vytvoří adresář `C:\DscSmbShare` Pokud tomu tak není již existuje a pak použije tento adresář jako sdílenou složku SMB. **FullAccess** má být poskytnut k nějakému účtu, který potřebuje zapisovat nebo odstranit ze sdílené složky a **oprávnění ke čtení** musí být poskytnut do žádného uzlu klienta, které získají ze sdílené složky (totiž konfigurace nebo prostředky DSC DSC jako systémový účet ve výchozím nastavení spustí, takže přímo počítač musí mít přístup ke sdílené složce).


### <a name="give-file-system-access-to-the-pull-client"></a>Poskytnout přístupu k systému souborů k vyžádání klienta

Poskytnutí **oprávnění ke čtení** klientovi uzel umožňuje tento uzel k přístupu ke sdílené složce protokolu SMB, ale aby se soubory nebo složky, jež se sdílet. Je nutné explicitně udělit klienta uzly přístup k protokolu SMB sdílenou složku a podsložky. Jsme to provést pomocí DSC přidáním pomocí **cNtfsPermissionEntry** prostředku, který je součástí [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) modulu. Přidá následující konfigurace **cNtfsPermissionEntry** blok, který uděluje přístup ReadAndExecute klient pro vyžádání obsahu:

```powershell
Configuration DSCSMB {

Import-DscResource -ModuleName PSDesiredStateConfiguration
Import-DscResource -ModuleName xSmbShare
Import-DscResource -ModuleName cNtfsAccessControl

    Node localhost {

        File CreateFolder {

            DestinationPath = 'DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'

        }

        xSMBShare CreateShare {

            Name = 'DscSmbShare'
            Path = 'DscSmbShare'
            FullAccess = 'administrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'

        }

        cNtfsPermissionEntry PermissionSet1 {

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

## <a name="placing-configurations-and-resources"></a>Umístění konfigurace a prostředky

Uložte všechny soubory MOF konfigurace nebo prostředky DSC, které chcete uzly klienta stáhnout sdílenou složku SMB.

Musí mít název konfiguračního souboru MOF _ConfigurationID_MOF, kde _ConfigurationID_ je hodnota **ConfigurationID** vlastnost LCM cílový uzel. Další informace o nastavení klientů pro vyžádání obsahu najdete v tématu [nastavení vyžadování klienta pomocí ID konfigurace](pullClientConfigID.md).

>**Poznámka:** ID konfigurace musíte použít, pokud používáte vyžádání serveru SMB. Názvy konfigurace nejsou podporovány pro protokol SMB.

Každý modul prostředků musí být ZIP a s názvem podle následující vzor `{Module Name}_{Module Version}.zip`. Například modul s názvem xWebAdminstration verzí modulu 3.1.2.0 by se jmenovala 'xWebAdministration_3.2.1.0.zip'. Každá verze nástroje modul musí být obsažena v souboru zip jeden. Vzhledem k tomu, že existuje jenom jedna verze nástroje prostředků do každého souboru zip modulu formát přidali v WMF 5.0 s není dostupná podpora pro více verze modulu v jednom adresáři. To znamená, že před balení až moduly prostředků DSC pro použití s načítacího serveru je potřeba provést změnu malá strukturu adresáře. Výchozí formát modulů obsahující prostředek DSC v WMF 5.0 je ' {složku modulu}\{verze modulu} \DscResources\{Složka prostředků DSC}\'. Před balení pro vyžádání obsahu server jednoduše odeberte **{verze modulu}** složku, cesta k přestane ' {složku modulu} \DscResources\{Složka prostředků DSC}\'. Díky této změně složky zip, jak je popsáno výše a umístěte tyto soubory zip v sdílenou složku SMB.

## <a name="creating-the-mof-checksum"></a>Vytváření kontrolního součtu MOF
Konfigurační soubor MOF musí být spárována s soubor kontrolního součtu, takže LCM na cílový uzel můžete konfiguraci ověřit.
Chcete-li vytvořit kontrolní součet, zavolejte [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) rutiny. Rutina trvá **cesta** parametr, který určuje složku, kde se nachází v konfiguraci MOF. Rutina vytvoří kontrolní součet souboru s názvem `ConfigurationMOFName.mof.checksum`, kde `ConfigurationMOFName` je název konfiguračního souboru mof.
Pokud existují minimálně jedna konfigurace soubory MOF do určené složky, vytvoří se pro každou konfiguraci ve složce kontrolní součet.

Soubor kontrolního součtu musí být ve stejném adresáři jako konfiguračního souboru MOF (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` ve výchozím nastavení), a mít stejný název `.checksum` příponou.

>**Poznámka:**: Pokud změníte konfigurační soubor MOF žádným způsobem, musíte také znovu vytvořit soubor kontrolního součtu.

## <a name="setting-up-a-pull-client-for-smb"></a>Nastavení klienta vyžádání obsahu pro protokol SMB

Chcete-li nastavení klienta, který vrátí konfigurace nebo prostředky ze složky protokolu SMB, je nakonfigurovat klienta místní Configuration Manager (LCM) s **ConfigurationRepositoryShare** a **ResourceRepositoryShare** bloků, které zadejte sdílenou složku, ze kterého mají být konfigurací a prostředků DSC pro vyžádání obsahu.

Další informace o konfiguraci LCM najdete v tématu [nastavení vyžadování klienta pomocí ID konfigurace](pullClientConfigID.md).

>**Poznámka:** pro jednoduchost, v tomto příkladu **PSDscAllowPlainTextPassword** umožňující předávání heslo jako prostý text k **přihlašovacích údajů** parametr. Informace o předávání pověření bezpečněji najdete v tématu [možností pověření v konfigurační Data](configDataCredentials.md).

>**Poznámka:** je nutné zadat **ConfigurationID** v **nastavení** blok metakonfiguraci pro vyžádání obsahu serveru SMB, i když jsou pouze stahování prostředky.

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

Zvláštní díky následující:

- Jan F. Robbins, jejichž příspěvcích na pomocí protokolu SMB pro DSC pomohl informovat obsah v tomto tématu. Jeho blogu je na [Karel F Robbins](http://mikefrobbins.com/).
- Serge Nikalaichyk, kdo vytvořené **cNtfsAccessControl** modulu. Zdroj pro tento modul je v https://github.com/SNikalaichyk/cNtfsAccessControl.

## <a name="see-also"></a>Viz taky
- [Přehled stavu konfigurace požadovaného prostředí Windows PowerShell](overview.md)
- [Přijetí konfigurace](enactingConfigurations.md)
- [Použití konfiguračních identifikátorů k nastavení načítacího klienta](pullClientConfigID.md)