---
ms.date: 10/31/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Zabezpečení souboru MOF
ms.openlocfilehash: 6c2aadb75ac617d9b845ef387f292b8156bb8889
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403791"
---
# <a name="securing-the-mof-file"></a>Zabezpečení souboru MOF

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

DSC spravuje konfiguraci uzlů serveru s použitím informací uložených v souboru MOF, kde místní Configuration Manageru (LCM) implementuje požadované koncový stav.
Tento soubor obsahuje podrobnosti o konfiguraci, proto je důležité, abyste zajistili jeho zabezpečení.
Toto téma popisuje, jak zajistit cílový uzel má šifrování souboru.

Od verze prostředí PowerShell verze 5.0, celý soubor MOF zašifrují ve výchozím nastavení při použití na uzlu pomocí `Start-DSCConfiguration` rutiny.
Proces popsaný v tomto článku se vyžaduje jenom při implementaci řešení, které využívá službu protokolu o přijetí změn, pokud nejsou spravované certifikáty, aby konfigurace stáhl cílový uzel je možné dešifrovat a čtení systém předtím, než se použijí (například službu přijetí změn ve Windows serveru k dispozici).
Uzly zaregistrovaný [Azure Automation DSC](https://docs.microsoft.com/azure/automation/automation-dsc-overview) bude automaticky certifikáty instalaci a spravovaná služba s žádné administrativní režii vyžaduje.

> [!NOTE]
> Toto téma popisuje certifikáty používané k šifrování.
> Pro šifrování certifikát podepsaný svým držitelem je dostačující, protože privátní klíč zůstane vždy tajný klíč a šifrování neznamená důvěryhodnosti dokumentu.
> Certifikáty podepsané svým držitelem by *není* slouží k jeho ověřování.
> Pro účely ověřování používejte certifikát od důvěryhodné certifikační autority (CA).

## <a name="prerequisites"></a>Předpoklady

Chcete-li úspěšně šifrovat přihlašovací údaje používané k zabezpečení konfiguraci DSC, ujistěte se, že máte následující:

- **Některé prostředky, vydávání a distribuci certifikátů**. Toto téma a jeho příklady předpokládají, že používáte Active Directory certifikační autority. Další informace na pozadí v Active Directory Certificate Services najdete v tématu [přehled Active Directory Certificate Services](https://technet.microsoft.com/library/hh831740.aspx) a [Active Directory Certificate Services ve Windows serveru 2008](https://technet.microsoft.com/windowsserver/dd448615.aspx).
- **Přístup pro správu na cílový uzel nebo uzly**.
- **Každý cílový uzel má certifikát podporující šifrování, uložit své osobní Store**. V prostředí Windows PowerShell je cesta k úložišti certifikátů: \LocalMachine\My. Příklady v tomto tématu použijte šablonu "ověřování pracovní stanice", která můžete najít (společně s další šablony certifikátů) v [výchozí šablony certifikátů](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).
- Pokud budete používat tuto konfiguraci na jiném počítači než cílový uzel **export veřejného klíče certifikátu**a importovat ho do počítače se spustí konfiguraci z. Ujistěte se, že je exportovat pouze **veřejné** klíče; zabezpečit privátní klíč.

## <a name="overall-process"></a>Celkový proces

 1. Nastavte certifikáty, klíče a kryptografických otisků, ujistěte se, že každý cílový uzel má kopie certifikátu a konfigurace počítače veřejným klíčem a kryptografického otisku.
 2. Vytvoří blok dat konfigurace, který obsahuje cestu a kryptografický otisk veřejný klíč.
 3. Vytvořte konfigurační skript, který definuje požadovanou konfiguraci pro cílový uzel a nastaví dešifrování cílové uzly podle příkazů místní konfiguraci správce dešifrovat konfigurační data pomocí certifikátu a jeho kryptografický otisk.
 4. Spusťte konfiguraci, která bude nastavení Local Configuration Manageru a spustit konfiguraci DSC.

![Diagram1](../images/CredentialEncryptionDiagram1.png)

## <a name="certificate-requirements"></a>Požadavky na certifikát

K uplatní šifrování přihlašovacích údajů, certifikát veřejného klíče musí být k dispozici na _cílový uzel_ , který je **důvěryhodné** počítač používá pro vytvoření konfigurace DSC.
Tento certifikát veřejného klíče má specifické požadavky, aby se používá pro šifrování přihlašovacích údajů DSC:

1. **Použití klíče**:
   - Musí obsahovat: "KeyEncipherment" a "DataEncipherment".
   - By měl _není_ obsahovat: Digitální podpis.
2. **Rozšířené použití klíče**:
   - Musí obsahovat: Šifrování dokumentů (1.3.6.1.4.1.311.80.1).
   - By měl _není_ obsahovat: Ověření klienta (1.3.6.1.5.5.7.3.2) a ověření serveru (1.3.6.1.5.5.7.3.1).
3. Privátní klíč certifikátu je k dispozici na * Node_ cíl.
4. **Poskytovatele** pro tento certifikát musí být "Microsoft RSA SChannel Cryptographic Provider".

> [!IMPORTANT]
> I když používáte certifikát s obsahující použití klíče 'Digitální podpis' nebo některou z použití klíče ověřování, tím povolíte šifrovacího klíče na možné snadněji chybná a zranitelný vůči útoku. Proto je osvědčeným postupem je použití certifikátu vytvořené speciálně pro účely zabezpečení přihlašovacích údajů DSC, která vynechává tyto použití klíče a rozšířená použití klíče.

Všechny existující certifikát na _cílový uzel_ , že splňuje tyto kritéria lze použít na zabezpečené přihlašovací údaje DSC.

## <a name="certificate-creation"></a>Vytvoření certifikátu

Existují dva přístupy, které si můžete vytvořit a použít požadované šifrovací certifikát (pár veřejného a privátního klíče).

1. Vytvořit v **cílový uzel** a exportovat pouze veřejný klíč, který **vytváření uzlu**
2. Vytvořit v **vytváření uzel** a exportovat celé dvojici klíčů k **cílový uzel**

Metoda 1 se doporučuje, protože privátní klíč používaný k dešifrování přihlašovacích údajů v soubor MOF táhnou za jeden cílový uzel za všech okolností.

### <a name="creating-the-certificate-on-the-target-node"></a>Vytvoření certifikátu na cílový uzel

Privátní klíč musí být udržen v tajnosti, protože se používá k dešifrování soubor MOF v **cílový uzel** je nejjednodušší způsob, jak to udělat k vytvoření certifikátu privátního klíče na **cílový uzel**a zkopírujte  **certifikát veřejného klíče** do počítače se použije k vytvoření konfigurace DSC do souboru MOF.
V následujícím příkladu:

1. vytvoří certifikát na **cílový uzel**
2. Exportuje certifikátu veřejného klíče na **cílový uzel**.
3. Importuje certifikát veřejného klíče do **Moje** úložiště certifikátů na **vytváření obsahu uzlu**.

#### <a name="on-the-target-node-create-and-export-the-certificate"></a>Na cílovém uzlu: vytvoření a export certifikátu

> Cílový uzel: Windows Server 2016 a Windows 10

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```

Jednou exportovat `DscPublicKey.cer` by bylo potřeba zkopírovat do **vytváření uzel**.

> Cílový uzel: Windows Server 2012 R2 nebo Windows 8.1 a starší
> [!WARNING]
> Protože `New-SelfSignedCertificate` rutiny ve Windows operačních systémech starších než Windows 10 a Windows Server 2016 nepodporuje **typ** parametr, alternativní způsob vytváření tento certifikát je nutný v těchto operačních systémech.
>
> V tomto případě můžete použít `makecert.exe` nebo `certutil.exe` k vytvoření certifikátu.
>
>Alternativní způsob je [stáhnout skript New-SelfSignedCertificateEx.ps1 z webu Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) a použít ho k vytvoření certifikátu místo toho:

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
$Cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object {
        ($_.FriendlyName -eq 'DSC Credential Encryption certificate') -and ($_.Subject -eq "CN=${ENV:ComputerName}")
    } | Select-Object -First 1
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```

Jednou exportovat ```DscPublicKey.cer``` by bylo potřeba zkopírovat do **vytváření uzel**.

#### <a name="on-the-authoring-node-import-the-certs-public-key"></a>V uzlu pro tvorbu: Importovat veřejný klíč certifikátu

```powershell
# Import to the my store
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

### <a name="creating-the-certificate-on-the-authoring-node"></a>Vytvoření certifikátu pro vytváření obsahu uzlu

Alternativně se dají vytvořit šifrovací certifikát na **vytváření uzel**, exportovaný s **privátní klíč** jako PFX soubor a potom naimportovat **cílový uzel**.
Toto je aktuální metody pro implementaci šifrování přihlašovacích údajů DSC v _Nano Server_.
I když soubor PFX je zabezpečený pomocí hesla by měla být ukázal jako nedocenitelný zabezpečené během přenosu.
V následujícím příkladu:

1. vytvoří certifikát na **vytváření obsahu uzlu**.
2. Exportuje včetně soukromého klíče v certifikátu **vytváření obsahu uzlu**.
3. Odstraní privátní klíč z **vytváření obsahu uzlu**, uchová certifikátu veřejného klíče, ale **Moje** ukládat.
4. provede import certifikátu privátního klíče do úložiště certifikátů My(Personal) na **cílový uzel**.
   - musí být přidán do kořenového úložiště tak, aby se důvěryhodná **cílový uzel**.

#### <a name="on-the-authoring-node-create-and-export-the-certificate"></a>V uzlu pro tvorbu: vytvoření a export certifikátu

> Cílový uzel: Windows Server 2016 a Windows 10

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

Po exportu `DscPrivateKey.pfx` by bylo potřeba zkopírovat do **cílový uzel**.

> Cílový uzel: Windows Server 2012 R2 nebo Windows 8.1 a starší
> [!WARNING]
> Protože `New-SelfSignedCertificate` rutiny ve Windows operačních systémech starších než Windows 10 a Windows Server 2016 nepodporuje **typ** parametr, alternativní způsob vytváření tento certifikát je nutný v těchto operačních systémech.
>
> V tomto případě můžete použít `makecert.exe` nebo `certutil.exe` k vytvoření certifikátu.
>
> Alternativní způsob je [stáhnout skript New-SelfSignedCertificateEx.ps1 z webu Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) a použít ho k vytvoření certifikátu místo toho:

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
$Cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object {
        ($_.FriendlyName -eq 'DSC Credential Encryption certificate') -and ($_.Subject -eq "CN=${ENV:ComputerName}")
    } | Select-Object -First 1
# export the public key certificate
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
$cert | Export-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -Password $mypwd -Force
# remove the private key certificate from the node but keep the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
$cert | Remove-Item -Force
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

#### <a name="on-the-target-node-import-the-certs-private-key-as-a-trusted-root"></a>Na cílovém uzlu: import certifikátu privátní klíč jako důvěryhodné kořenové

```powershell
# Import to the root store so that it is trusted
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
Import-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -CertStoreLocation Cert:\LocalMachine\My -Password $mypwd > $null
```

## <a name="configuration-data"></a>Konfigurační data

Blok dat konfigurace definuje cílové uzly, na kterých pracují na tom, zda nebo šifrovat přihlašovací údaje, znamená, že šifrování a dalších informací. Další informace o konfiguraci datového bloku, naleznete v tématu [oddělení konfiguraci a Data prostředí](../configurations/configData.md).

Prvky, které je možné nakonfigurovat pro každý uzel, ke které se vztahují k šifrování přihlašovacích údajů jsou:

- **NodeName** – název nakonfigurované šifrování přihlašovacích údajů pro cílový uzel.
- **PsDscAllowPlainTextPassword** – ať už se bude moct nezašifrované přihlašovací údaje předávat do tohoto uzlu. Toto je **ale nedoporučený krok**.
- **Kryptografický otisk** – kryptografický otisk certifikátu, který se použije k dešifrování přihlašovacích údajů v konfiguraci DSC na _cílový uzel_. **Tento certifikát musí existovat v úložišti certifikátů místního počítače na cílový uzel.**
- **CertificateFile** – soubor certifikátu (který obsahuje pouze veřejný klíč), který má použít k šifrování přihlašovacích údajů pro _cílový uzel_. Musí se jednat buď Binární X.509, kódování DER nebo soubor certifikátu formátu X.509 s kódováním Base-64.

Tento příklad ukazuje blok dat konfigurace, který určuje cílový uzel tak, aby fungoval na pojmenované targetNode, cestu k souboru certifikátu veřejného klíče (s názvem targetNode.cer) a kryptografický otisk pro veřejný klíč.

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

V samotný skript konfigurace, použijte `PsCredential` parametr Ujistěte se, že přihlašovací údaje jsou uložené pro nejkratší možné době. Při spuštění zadaný příklad DSC bude vyzve k zadání přihlašovacích údajů a zašifrování souboru MOF pomocí CertificateFile, který je přidružený cílový uzel v bloku dat konfigurace. Tento příklad kódu ze sdílené složky, která je zabezpečena zkopíruje soubor na uživatele.

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
    }
}
```

## <a name="setting-up-decryption"></a>Nastavení dešifrování

Před [ `Start-DscConfiguration` ](https://technet.microsoft.com/library/dn521623.aspx) můžete pracovat, je nutné zjistit Local Configuration Manageru na každém cílovém uzlu, který certifikát se má použít k dešifrování přihlašovacích údajů, pomocí prostředků CertificateID ověřit kryptografický otisk certifikátu. Tuto ukázkovou funkci najdete příslušné místní certifikát (může mít vlastní nastavení, takže se přesně certifikát, který chcete použít):

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

S certifikátem identifikován jeho kryptografický otisk konfigurační skript aktualizovat tak, použijte hodnotu:

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

## <a name="running-the-configuration"></a>Konfigurace spuštění

V tomto okamžiku spustíte konfiguraci, která bude výstup dva soubory:

- A *. meta.mof soubor, který konfiguruje Local Configuration Manageru k dešifrování přihlašovacích údajů pomocí certifikátu, který je uložen v úložišti místního počítače a identifikován jeho kryptografický otisk. [`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/library/dn521621.aspx) se vztahuje *. meta.mof souboru.
- Soubor MOF, který ve skutečnosti aplikuje konfiguraci. Start-DscConfiguration aplikuje konfiguraci.

Tyto příkazy bude provádět tyto kroky:

```powershell
Write-Host "Generate DSC Configuration..."
CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample

Write-Host "Setting up LCM to decrypt credentials..."
Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose

Write-Host "Starting Configuration..."
Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose
```

V tomto příkladu by nabízená konfigurace DSC na cílový uzel.
Konfigurace DSC můžete použít také pomocí serveru vyžádané replikace DSC, pokud je k dispozici.

Zobrazit [nastavení načítacího klienta DSC](pullClient.md) Další informace o použití konfigurací DSC pomocí serveru vyžádané replikace DSC.

## <a name="credential-encryption-module-example"></a>Příklad modulu šifrování přihlašovacích údajů

Tady je úplný příklad, který zahrnuje všechny tyto kroky a pomocné rutiny, který exportuje a zkopíruje veřejných klíčů:

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
