---
ms.date: 2017-10-31
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Zabezpečení souboru MOF"
ms.openlocfilehash: 1bb257f3237344f32c9035f3836dd317b75eef0a
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="securing-the-mof-file"></a>Zabezpečení souboru MOF

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

DSC spravuje konfigurace uzlů serveru pomocí informace uložené v souboru MOF, kde místní Configuration Manager (LCM) implementuje požadované koncové stavu.
Protože tento soubor obsahuje podrobnosti o konfiguraci, je důležité k lepšímu zabezpečení.
Toto téma popisuje, jak na cílový uzel je šifrovaný soubor.

Od verze prostředí PowerShell, verze 5.0, celý soubor MOF je zašifrovaná ve výchozím nastavení při použití na uzlu pomocí **Start-DSCConfiguration** rutiny.
Proces popsaný v tomto článku se vyžaduje jenom v případě, že implementaci řešení pro použití protokolu vyžádání obsahu, pokud nejsou spravovány certifikáty, aby konfigurace stáhne cílový uzel může dešifrovat a číst systému před jejich instalací (například službu vyžádání obsahu k dispozici v systému Windows Server).
Uzly zaregistrované [Azure Automation DSC](https://docs.microsoft.com/azure/automation/automation-dsc-overview) bude automaticky certifikáty instalaci a spravuje službu s žádné režijní náklady na správu požadované.

>**Poznámka:** Toto téma popisuje certifikátů používaných pro šifrování.
>Certifikát podepsaný svým držitelem pro šifrování, stačí, protože privátní klíč je vždy tajný klíč a šifrování neznamená důvěryhodnosti dokumentu.
>Certifikáty podepsané svým držitelem by *není* být použito pro účely ověřování.
>Měli byste použít certifikát od důvěryhodné certifikační autority (CA) k jakýmkoli jiným účelům ověřování.

## <a name="prerequisites"></a>Předpoklady

Chcete-li úspěšně šifrovat přihlašovací údaje používané k zabezpečení konfigurace DSC, ujistěte se, že máte následující:

* **Některé prostředky, vydávání a distribuci certifikátů**. Toto téma a jeho příklady předpokládají, že používáte Active Directory certifikační autority. Pro další základní informace o službě Active Directory Certificate Services naleznete v tématu [přehled Active Directory Certificate Services](https://technet.microsoft.com/library/hh831740.aspx) a [Active Directory Certificate Services v systému Windows Server 2008](https://technet.microsoft.com/windowsserver/dd448615.aspx).
* **Přístup pro správu na cílový uzel nebo uzly**.
* **Každý cílový uzel má certifikát podporující šifrování uložit jeho osobní úložiště**. V prostředí Windows PowerShell je cesta k úložišti Cert: \LocalMachine\My. V příkladech v tomto tématu použijte šablonu "ověřování pracovní stanice", které můžete vyhledat (spolu s další šablony certifikátů) v [výchozí šablony certifikátů](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).
* Pokud budete používat tuto konfiguraci na jiném počítači než cílový uzel **exportujte veřejný klíč certifikátu**a importujte ho do počítače se spustí konfiguraci z. Ujistěte se, že exportujete pouze **veřejné** klíče; zabezpečit privátní klíč.

## <a name="overall-process"></a>Celkový proces

 1. Nastavení klíče, certifikátů a kryptografických otisků, a ujistěte se, že každý cílový uzel má kopie certifikátu a v počítači konfigurace je veřejný klíč a kryptografický otisk.
 2. Vytvořte blok dat konfigurace, který obsahuje cestu a kryptografický otisk veřejný klíč.
 3. Vytvořte konfigurační skript, který definuje požadovanou konfiguraci pro cílový uzel a nastaví dešifrování na cílové uzly podle tvorba příkazů konfiguraci místního správce k dešifrování dat konfigurace pomocí certifikátu a jeho kryptografický otisk.
 4. Spusťte konfigurace, který bude nastavení správce místní konfigurace a spuštění konfigurace DSC.

![Diagram1](images/CredentialEncryptionDiagram1.png)

## <a name="certificate-requirements"></a>Požadavky na certifikát

K uplatní šifrování přihlašovacích údajů, musí být k dispozici na certifikátu veřejného klíče _cílový uzel_ tedy **důvěryhodné** pro počítač používá k vytváření konfigurace DSC.
Certifikát veřejného klíče má specifické požadavky pro něj má být použit pro šifrování přihlašovacích údajů DSC:
 1. **Použití klíče**:
   - Musí obsahovat: 'KeyEncipherment' a 'DataEncipherment'.
   - Měli _není_ obsahovat: 'Digitální podpis'.
 2. **Rozšířené použití klíče**:
   - Musí obsahovat: šifrování dokumentů (1.3.6.1.4.1.311.80.1).
   - Měli _není_ obsahovat: ověření klienta (1.3.6.1.5.5.7.3.2) a ověření serveru (1.3.6.1.5.5.7.3.1).
 3. Soukromý klíč pro certifikát je k dispozici na * Node_ cíl.
 4. **Zprostředkovatele** pro certifikát musí být "Microsoft RSA SChannel Cryptographic Provider".
 
>**Doporučený osvědčený postup:** i když používáte certifikát s obsahující použití klíče, digitální podpis, nebo jednoho z ověřování EKU tím povolíte šifrovacího klíče se snadněji chybná a bude zranitelný vůči útoku. Proto je vhodné používat certifikát vytvořena speciálně pro účely zabezpečení DSC pověření, který vynechá tyto použití klíče a rozšířená použití klíče.
  
Všechny existující certifikát na _cílový uzel_ , že splňuje tyto kritéria slouží k zabezpečené přihlašovací údaje DSC.

## <a name="certificate-creation"></a>Vytvoření certifikátu

Existují dva přístupy, které můžete použít k vytváření a používání požadovaný certifikát šifrování (pár veřejného a privátního klíče).

1. Vytvořte na **cílový uzel** a exportovat pouze veřejný klíč k **vytváření uzlu**
2. Vytvořit na **vytváření uzlu** a celý páru klíčů pro export **cílový uzel.**

Metoda 1 se doporučuje, protože privátní klíč používaný k dešifrování přihlašovací údaje v MOF zůstává na cílový uzel za všech okolností.


### <a name="creating-the-certificate-on-the-target-node"></a>Vytváření certifikátu na cílovém uzlu

Privátní klíč musí být udržovány tajný, protože se používá k dešifrování MOF na **cílový uzel** je nejjednodušší způsob, jak to udělat k vytvoření certifikátu privátního klíče na **cílový uzel**a zkopírujte  **certifikát veřejného klíče** k počítači používá k vytváření konfigurace DSC do souboru MOF.
V následujícím příkladu:
 1. vytvoří certifikát na **cílový uzel.**
 2. Exportuje certifikátu veřejného klíče na **cílový uzel**.
 3. Importuje certifikátu veřejného klíče do **Moje** úložiště certifikátů na **vytváření uzlu**.

#### <a name="on-the-target-node-create-and-export-the-certificate"></a>Na cílovém uzlu: vytvoření a export certifikátu
>Cílový uzel: Windows Server 2016 a Windows 10

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```
Po exportu ```DscPublicKey.cer``` by bylo potřeba kopírovat do **vytváření uzlu**.

>Cílový uzel: Windows Server 2012 R2 nebo Windows 8.1 a starší

Protože rutinu New-SelfSignedCertificate na Windows operačních systémech starších než Windows 10 a Windows Server 2016 nepodporují **typ** parametr, alternativní metodu vytváření tohoto certifikátu je povinný, pokud k nim operační systémy.
V takovém případě můžete použít ```makecert.exe``` nebo ```certutil.exe``` k vytvoření certifikátu.

Je to alternativní metoda [stáhnout z webu Microsoft Script Center skript New-SelfSignedCertificateEx.ps1](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) a použít ho k vytvoření certifikátu místo:
```powershell
# note: These steps need to be performed in an Administrator PowerShell session
# and in the folder that contains New-SelfSignedCertificateEx.ps1
. .\New-SelfSignedCertificateEx.ps1
New-SelfsignedCertificateEx `
    -Subject "CN=${ENV:ComputerName}" `
    -EKU 'Document Encryption' `
    -KeyUsage 'KeyEncipherment, DataEncipherment' `
    -SAN ${ENV:ComputerName} `
    -FriendlyName 'DSC Credential Encryption certificate' `
    -Exportable `
    -StoreLocation 'LocalMachine' `
    -KeyLength 2048 `
    -ProviderName 'Microsoft Enhanced Cryptographic Provider v1.0' `
    -AlgorithmName 'RSA' `
    -SignatureAlgorithm 'SHA256'
# Locate the newly created certificate
$Cert = Get-ChildItem -Path cert:\LocalMachine\My `
    | Where-Object {
        ($_.FriendlyName -eq 'DSC Credential Encryption certificate') `
        -and ($_.Subject -eq "CN=${ENV:ComputerName}")
    } | Select-Object -First 1
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```
Po exportu ```DscPublicKey.cer``` by bylo potřeba kopírovat do **vytváření uzlu**.

#### <a name="on-the-authoring-node-import-the-certs-public-key"></a>Na uzlu vytváření: import veřejného klíče certifikátu
```powershell
# Import to the my store
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

### <a name="creating-the-certificate-on-the-authoring-node"></a>Vytváření certifikátu na uzlu pro tvorbu
Alternativně lze vytvořit šifrovací certifikát na **vytváření uzlu**, exportovaný s **privátní klíč** jako PFX souboru a poté importovat na **cílový uzel**.
Toto je aktuální metoda pro implementaci šifrování přihlašovacích údajů DSC na _Nano Server_.
I když soubor PFX je zabezpečen heslo se musí být zabezpečen během přenosu.
V následujícím příkladu:
 1. vytvoří certifikát na **vytváření uzlu**.
 2. Exportuje certifikát, včetně privátního klíče **vytváření uzlu**.
 3. Odebere privátní klíč z **vytváření uzlu**, ale zachová certifikátu veřejného klíče **Moje** uložit.
 4. Importuje certifikátu privátního klíče do kořenového úložiště certifikátů na **cílový uzel**.
   - musí být přidané do kořenového úložiště tak, aby se důvěřují **cílový uzel**.

#### <a name="on-the-authoring-node-create-and-export-the-certificate"></a>Na uzlu vytváření: vytvoření a export certifikátu
>Cílový uzel: Windows Server 2016 a Windows 10

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the private key certificate
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
$cert | Export-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -Password $mypwd -Force
# remove the private key certificate from the node but keep the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
$cert | Remove-Item -Force
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```
Po exportu ```DscPrivateKey.pfx``` by bylo potřeba kopírovat do **cílový uzel**.

>Cílový uzel: Windows Server 2012 R2 nebo Windows 8.1 a starší

Protože rutinu New-SelfSignedCertificate na Windows operačních systémech starších než Windows 10 a Windows Server 2016 nepodporují **typ** parametr, alternativní metodu vytváření tohoto certifikátu je povinný, pokud k nim operační systémy.
V takovém případě můžete použít ```makecert.exe``` nebo ```certutil.exe``` k vytvoření certifikátu.

Je to alternativní metoda [stáhnout z webu Microsoft Script Center skript New-SelfSignedCertificateEx.ps1](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) a použít ho k vytvoření certifikátu místo:
```powershell
# note: These steps need to be performed in an Administrator PowerShell session
# and in the folder that contains New-SelfSignedCertificateEx.ps1
. .\New-SelfSignedCertificateEx.ps1
New-SelfsignedCertificateEx `
    -Subject "CN=${ENV:ComputerName}" `
    -EKU 'Document Encryption' `
    -KeyUsage 'KeyEncipherment, DataEncipherment' `
    -SAN ${ENV:ComputerName} `
    -FriendlyName 'DSC Credential Encryption certificate' `
    -Exportable `
    -StoreLocation 'LocalMachine' `
    -KeyLength 2048 `
    -ProviderName 'Microsoft Enhanced Cryptographic Provider v1.0' `
    -AlgorithmName 'RSA' `
    -SignatureAlgorithm 'SHA256'
# Locate the newly created certificate
$Cert = Get-ChildItem -Path cert:\LocalMachine\My `
    | Where-Object {
        ($_.FriendlyName -eq 'DSC Credential Encryption certificate') `
        -and ($_.Subject -eq "CN=${ENV:ComputerName}")
    } | Select-Object -First 1
# export the public key certificate
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
$cert | Export-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -Password $mypwd -Force
# remove the private key certificate from the node but keep the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
$cert | Remove-Item -Force
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

#### <a name="on-the-target-node-import-the-certs-private-key-as-a-trusted-root"></a>Na cílovém uzlu: import privátní klíč certifikátu jako důvěryhodné kořenové
```powershell
# Import to the root store so that it is trusted
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
Import-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -CertStoreLocation Cert:\LocalMachine\My -Password $mypwd > $null
```

## <a name="configuration-data"></a>Konfigurační data

Datový blok konfigurace definuje cílový uzlů, které fungují na tom, zda nebo šifrovat přihlašovací údaje, způsob šifrování a další informace. Další informace o konfiguraci datového bloku najdete v tématu [oddělení konfigurace a Data prostředí](configData.md).

Prvky, které lze nastavit pro každý uzel, které se vztahují k šifrování přihlašovacích údajů jsou:
* **NodeName** -název cílového uzlu, který je nakonfigurováno šifrování přihlašovacích údajů.
* **PsDscAllowPlainTextPassword** – ať nezašifrované přihlašovací údaje se bude moct být předána pro tento uzel. Toto je **nedoporučuje**.
* **Kryptografický otisk** -kryptografický otisk certifikátu, který se použije k dešifrování přihlašovací údaje v konfigurace DSC na _cílový uzel_. **Tento certifikát musí existovat v úložišti certifikátů místního počítače na cílovém uzlu.**
* **CertificateFile** – soubor certifikátu (obsahuje pouze veřejný klíč), který slouží k šifrování přihlašovacích údajů pro _cílový uzel_. Tato hodnota musí být buď Binární X.509, kódování DER nebo soubor certifikátu X.509 formátu s kódováním Base-64.

Tento příklad ukazuje blok dat konfigurace, který určuje cílový uzel tak, aby fungoval na pojmenované cílovým uzlem, cestu k souboru certifikátu veřejného klíče (s názvem targetNode.cer) a kryptografický otisk pro veřejný klíč.

```powershell
$ConfigData= @{ 
    AllNodes = @(     
            @{  
                # The name of the node we are describing 
                NodeName = "targetNode" 

                # The path to the .cer file containing the 
                # public key of the Encryption Certificate 
                # used to encrypt credentials for this node 
                CertificateFile = "C:\publicKeys\targetNode.cer" 

         
                # The thumbprint of the Encryption Certificate 
                # used to decrypt the credentials on target node 
                Thumbprint = "AC23EA3A9E291A75757A556D0B71CBBF8C4F6FD8" 
            }; 
        );    
    }
```


## <a name="configuration-script"></a>Konfigurační skript

V samotný skript konfigurace pomocí `PsCredential` parametr zajistit, že přihlašovací údaje jsou uloženy pro co nejdříve. Když spustíte zadaný příklad, bude DSC výzvu k zadání pověření a zašifrování souboru MOF pomocí CertificateFile, který je přidružen k uzlu cíl v bloku dat konfigurace. Tento příklad kódu zkopíruje soubor ze sdílené složky, která je zabezpečená na uživatele.

```
configuration CredentialEncryptionExample 
{ 
    param( 
        [Parameter(Mandatory=$true)] 
        [ValidateNotNullorEmpty()] 
        [PsCredential] $credential 
        ) 
    

    Node $AllNodes.NodeName 
    { 
        File exampleFile 
        { 
            SourcePath = "\\Server\share\path\file.ext" 
            DestinationPath = "C:\destinationPath" 
            Credential = $credential 
        } 
    } 
}
```

## <a name="setting-up-decryption"></a>Nastavení dešifrování

Před [ `Start-DscConfiguration` ](https://technet.microsoft.com/library/dn521623.aspx) můžete pracovat, je nutné zjistit správce místní konfigurace na každý cílový uzel, který certifikát má použít k dešifrování přihlašovacích údajů, pomocí prostředků CertificateID ověření kryptografický otisk certifikátu. Tento příklad funkce se najít odpovídající místní certifikát (bude pravděpodobně nutné přizpůsobit ho tak najde přesný certifikátu, který chcete použít):

```powershell
# Get the certificate that works for encryption 
function Get-LocalEncryptionCertificateThumbprint 
{ 
    (dir Cert:\LocalMachine\my) | %{
        # Verify the certificate is for Encryption and valid 
        if ($_.PrivateKey.KeyExchangeAlgorithm -and $_.Verify()) 
        { 
            return $_.Thumbprint 
        } 
    } 
}
```

Se identifikovanou pomocí jeho kryptografický otisk certifikátu můžete aktualizovat konfigurační skript, a použít hodnotu:

```powershell
configuration CredentialEncryptionExample 
{ 
    param( 
        [Parameter(Mandatory=$true)] 
        [ValidateNotNullorEmpty()] 
        [PsCredential] $credential 
        ) 
    

    Node $AllNodes.NodeName 
    { 
        File exampleFile 
        { 
            SourcePath = "\\Server\share\path\file.ext" 
            DestinationPath = "C:\destinationPath" 
            Credential = $credential 
        } 
        
        LocalConfigurationManager 
        { 
             CertificateId = $node.Thumbprint 
        } 
    } 
}
```

## <a name="running-the-configuration"></a>Spuštění konfigurace

V tomto okamžiku můžete spustit konfigurace, který bude výstup dva soubory:

 * A *. meta.mof soubor, který konfiguruje správce místní konfigurace dešifrovat přihlašovací údaje pomocí certifikátu, který je uložen v úložišti místního počítače a identifikovaný jeho kryptografický otisk. [`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/library/dn521621.aspx) se vztahuje *. meta.mof souboru.
 * Soubor MOF, který ve skutečnosti aplikuje konfiguraci. Spuštění DscConfiguration aplikuje konfiguraci.

Tyto příkazy bude možné provést tyto kroky:

```powershell
Write-Host "Generate DSC Configuration..."
CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample

Write-Host "Setting up LCM to decrypt credentials..."
Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose 
 
Write-Host "Starting Configuration..."
Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose
```

V tomto příkladu by nabízená konfigurace DSC cílový uzel.
Konfigurace DSC můžete použít také pomocí DSC pro vyžádání obsahu serveru, pokud je k dispozici.

V tématu [nastavení klienta vyžádání DSC](pullClient.md) Další informace o použití konfigurace DSC pomocí serveru vyžádané replikace DSC.

## <a name="credential-encryption-module-example"></a>Příklad modulu pro šifrování přihlašovacích údajů

Tady je příklad úplné, která zahrnuje všechny tyto kroky, a dále pomocná rutina, která exportuje a zkopíruje veřejných klíčů:

```powershell
# A simple example of using credentials
configuration CredentialEncryptionExample
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PsCredential] $credential
        )
    

    Node $AllNodes.NodeName
    {
        File exampleFile
        {
            SourcePath = "\\server\share\file.txt"
            DestinationPath = "C:\Users\user"
            Credential = $credential
        }
        
        LocalConfigurationManager
        {
            CertificateId = $node.Thumbprint
        }
    }
}

# A Helper to invoke the configuration, with the correct public key 
# To encrypt the configuration credentials
function Start-CredentialEncryptionExample
{
    [CmdletBinding()]
    param ($computerName)


    [string] $thumbprint = Get-EncryptionCertificate -computerName $computerName -Verbose
    Write-Verbose "using cert: $thumbprint"

    $certificatePath = join-path -Path "$env:SystemDrive\$script:publicKeyFolder" -childPath "$computername.EncryptionCertificate.cer"         

    $ConfigData=    @{
        AllNodes = @(     
                        @{  
                            # The name of the node we are describing
                            NodeName = "$computerName"

                            # The path to the .cer file containing the
                            # public key of the Encryption Certificate
                            CertificateFile = "$certificatePath"

                            # The thumbprint of the Encryption Certificate
                            # used to decrypt the credentials
                            Thumbprint = $thumbprint
                        };
                    );    
    }

    Write-Verbose "Generate DSC Configuration..."
    CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample `
        -credential (Get-Credential -UserName "$env:USERDOMAIN\$env:USERNAME" -Message "Enter credentials for configuration") 

    Write-Verbose "Setting up LCM to decrypt credentials..."
    Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose 

    Write-Verbose "Starting Configuration..."
    Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose

}


#region HelperFunctions

# The folder name for the exported public keys
$script:publicKeyFolder = "publicKeys"

# Get the certificate that works for encryptions
function Get-EncryptionCertificate
{
    [CmdletBinding()]
    param ($computerName)
    $returnValue= Invoke-Command -ComputerName $computerName -ScriptBlock {
            $certificates = dir Cert:\LocalMachine\my

            $certificates | %{
                    # Verify the certificate is for Encryption and valid
                    if ($_.PrivateKey.KeyExchangeAlgorithm -and $_.Verify())
                    {
                        # Create the folder to hold the exported public key
                        $folder= Join-Path -Path $env:SystemDrive\ -ChildPath $using:publicKeyFolder
                        if (! (Test-Path $folder))
                        {
                            md $folder | Out-Null
                        }

                        # Export the public key to a well known location
                        $certPath = Export-Certificate -Cert $_ -FilePath (Join-Path -path $folder -childPath "EncryptionCertificate.cer") 

                        # Return the thumbprint, and exported certificate path
                        return @($_.Thumbprint,$certPath);
                    }
                  }
        }
    Write-Verbose "Identified and exported cert..."
    # Copy the exported certificate locally
    $destinationPath = join-path -Path "$env:SystemDrive\$script:publicKeyFolder" -childPath "$computername.EncryptionCertificate.cer"
    Copy-Item -Path (join-path -path \\$computername -childPath $returnValue[1].FullName.Replace(":","$"))  $destinationPath | Out-Null

    # Return the thumbprint
    return $returnValue[0]
}

Start-CredentialEncryptionExample
```

