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
# <a name="securing-the-mof-file"></a><span data-ttu-id="84981-103">Zabezpečení souboru MOF</span><span class="sxs-lookup"><span data-stu-id="84981-103">Securing the MOF File</span></span>

> <span data-ttu-id="84981-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="84981-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="84981-105">DSC spravuje konfiguraci uzlů serveru s použitím informací uložených v souboru MOF, kde místní Configuration Manageru (LCM) implementuje požadované koncový stav.</span><span class="sxs-lookup"><span data-stu-id="84981-105">DSC manages the configuration of server nodes by applying information stored in a MOF file, where the Local Configuration Manager (LCM) implements the desired end state.</span></span>
<span data-ttu-id="84981-106">Tento soubor obsahuje podrobnosti o konfiguraci, proto je důležité, abyste zajistili jeho zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="84981-106">Because this file contains the details of the configuration, it’s important to keep it secure.</span></span>
<span data-ttu-id="84981-107">Toto téma popisuje, jak zajistit cílový uzel má šifrování souboru.</span><span class="sxs-lookup"><span data-stu-id="84981-107">This topic describes how to ensure the target node has encrypted the file.</span></span>

<span data-ttu-id="84981-108">Od verze prostředí PowerShell verze 5.0, celý soubor MOF zašifrují ve výchozím nastavení při použití na uzlu pomocí `Start-DSCConfiguration` rutiny.</span><span class="sxs-lookup"><span data-stu-id="84981-108">Beginning with PowerShell version 5.0, the entire MOF file is encrypted by default when it is applied to the node using the `Start-DSCConfiguration` cmdlet.</span></span>
<span data-ttu-id="84981-109">Proces popsaný v tomto článku se vyžaduje jenom při implementaci řešení, které využívá službu protokolu o přijetí změn, pokud nejsou spravované certifikáty, aby konfigurace stáhl cílový uzel je možné dešifrovat a čtení systém předtím, než se použijí (například službu přijetí změn ve Windows serveru k dispozici).</span><span class="sxs-lookup"><span data-stu-id="84981-109">The process described in this article is required only when implementing a solution using the pull service protocol if certificates are not managed, to ensure configurations downloaded by the target node can be decrypted and read by the system before they are applied (for example, the pull service available in Windows Server).</span></span>
<span data-ttu-id="84981-110">Uzly zaregistrovaný [Azure Automation DSC](https://docs.microsoft.com/azure/automation/automation-dsc-overview) bude automaticky certifikáty instalaci a spravovaná služba s žádné administrativní režii vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="84981-110">Nodes registered to [Azure Automation DSC](https://docs.microsoft.com/azure/automation/automation-dsc-overview) will automatically have certificates installed and managed by the service with no administrative overhead required.</span></span>

> [!NOTE]
> <span data-ttu-id="84981-111">Toto téma popisuje certifikáty používané k šifrování.</span><span class="sxs-lookup"><span data-stu-id="84981-111">This topic discusses certificates used for encryption.</span></span>
> <span data-ttu-id="84981-112">Pro šifrování certifikát podepsaný svým držitelem je dostačující, protože privátní klíč zůstane vždy tajný klíč a šifrování neznamená důvěryhodnosti dokumentu.</span><span class="sxs-lookup"><span data-stu-id="84981-112">For encryption, a self-signed certificate is sufficient, because the private key is always kept secret and encryption does not imply trust of the document.</span></span>
> <span data-ttu-id="84981-113">Certifikáty podepsané svým držitelem by *není* slouží k jeho ověřování.</span><span class="sxs-lookup"><span data-stu-id="84981-113">Self-signed certificates should *not* be used for authentication purposes.</span></span>
> <span data-ttu-id="84981-114">Pro účely ověřování používejte certifikát od důvěryhodné certifikační autority (CA).</span><span class="sxs-lookup"><span data-stu-id="84981-114">You should use a certificate from a trusted Certification Authority (CA) for any authentication purposes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84981-115">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="84981-115">Prerequisites</span></span>

<span data-ttu-id="84981-116">Chcete-li úspěšně šifrovat přihlašovací údaje používané k zabezpečení konfiguraci DSC, ujistěte se, že máte následující:</span><span class="sxs-lookup"><span data-stu-id="84981-116">To successfully encrypt the credentials used to secure a DSC configuration, make sure you have the following:</span></span>

- <span data-ttu-id="84981-117">**Některé prostředky, vydávání a distribuci certifikátů**.</span><span class="sxs-lookup"><span data-stu-id="84981-117">**Some means of issuing and distributing certificates**.</span></span> <span data-ttu-id="84981-118">Toto téma a jeho příklady předpokládají, že používáte Active Directory certifikační autority.</span><span class="sxs-lookup"><span data-stu-id="84981-118">This topic and its examples assume you are using Active Directory Certification Authority.</span></span> <span data-ttu-id="84981-119">Další informace na pozadí v Active Directory Certificate Services najdete v tématu [přehled Active Directory Certificate Services](https://technet.microsoft.com/library/hh831740.aspx) a [Active Directory Certificate Services ve Windows serveru 2008](https://technet.microsoft.com/windowsserver/dd448615.aspx).</span><span class="sxs-lookup"><span data-stu-id="84981-119">For more background information on Active Directory Certificate Services, see [Active Directory Certificate Services Overview](https://technet.microsoft.com/library/hh831740.aspx) and [Active Directory Certificate Services in Windows Server 2008](https://technet.microsoft.com/windowsserver/dd448615.aspx).</span></span>
- <span data-ttu-id="84981-120">**Přístup pro správu na cílový uzel nebo uzly**.</span><span class="sxs-lookup"><span data-stu-id="84981-120">**Administrative access to the target node or nodes**.</span></span>
- <span data-ttu-id="84981-121">**Každý cílový uzel má certifikát podporující šifrování, uložit své osobní Store**.</span><span class="sxs-lookup"><span data-stu-id="84981-121">**Each target node has an encryption-capable certificate saved its Personal Store**.</span></span> <span data-ttu-id="84981-122">V prostředí Windows PowerShell je cesta k úložišti certifikátů: \LocalMachine\My.</span><span class="sxs-lookup"><span data-stu-id="84981-122">In Windows PowerShell, the path to the store is Cert:\LocalMachine\My.</span></span> <span data-ttu-id="84981-123">Příklady v tomto tématu použijte šablonu "ověřování pracovní stanice", která můžete najít (společně s další šablony certifikátů) v [výchozí šablony certifikátů](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="84981-123">The examples in this topic use the “workstation authentication” template, which you can find (along with other certificate templates) at [Default Certificate Templates](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).</span></span>
- <span data-ttu-id="84981-124">Pokud budete používat tuto konfiguraci na jiném počítači než cílový uzel **export veřejného klíče certifikátu**a importovat ho do počítače se spustí konfiguraci z.</span><span class="sxs-lookup"><span data-stu-id="84981-124">If you will be running this configuration on a computer other than the target node, **export the public key of the certificate**, and then import it to the computer you will run the configuration from.</span></span> <span data-ttu-id="84981-125">Ujistěte se, že je exportovat pouze **veřejné** klíče; zabezpečit privátní klíč.</span><span class="sxs-lookup"><span data-stu-id="84981-125">Make sure that you export only the **public** key; keep the private key secure.</span></span>

## <a name="overall-process"></a><span data-ttu-id="84981-126">Celkový proces</span><span class="sxs-lookup"><span data-stu-id="84981-126">Overall process</span></span>

 1. <span data-ttu-id="84981-127">Nastavte certifikáty, klíče a kryptografických otisků, ujistěte se, že každý cílový uzel má kopie certifikátu a konfigurace počítače veřejným klíčem a kryptografického otisku.</span><span class="sxs-lookup"><span data-stu-id="84981-127">Set up the certificates, keys, and thumbprints, making sure that each target node has copies of the certificate and the configuration computer has the public key and thumbprint.</span></span>
 2. <span data-ttu-id="84981-128">Vytvoří blok dat konfigurace, který obsahuje cestu a kryptografický otisk veřejný klíč.</span><span class="sxs-lookup"><span data-stu-id="84981-128">Create a configuration data block that contains the path and thumbprint of the public key.</span></span>
 3. <span data-ttu-id="84981-129">Vytvořte konfigurační skript, který definuje požadovanou konfiguraci pro cílový uzel a nastaví dešifrování cílové uzly podle příkazů místní konfiguraci správce dešifrovat konfigurační data pomocí certifikátu a jeho kryptografický otisk.</span><span class="sxs-lookup"><span data-stu-id="84981-129">Create a configuration script that defines your desired configuration for the target node and sets up decryption on the target nodes by commanding the Local Configuration manager to decrypt the configuration data using the certificate and its thumbprint.</span></span>
 4. <span data-ttu-id="84981-130">Spusťte konfiguraci, která bude nastavení Local Configuration Manageru a spustit konfiguraci DSC.</span><span class="sxs-lookup"><span data-stu-id="84981-130">Run the configuration, which will set the Local Configuration Manager settings and start the DSC configuration.</span></span>

![Diagram1](../images/CredentialEncryptionDiagram1.png)

## <a name="certificate-requirements"></a><span data-ttu-id="84981-132">Požadavky na certifikát</span><span class="sxs-lookup"><span data-stu-id="84981-132">Certificate Requirements</span></span>

<span data-ttu-id="84981-133">K uplatní šifrování přihlašovacích údajů, certifikát veřejného klíče musí být k dispozici na _cílový uzel_ , který je **důvěryhodné** počítač používá pro vytvoření konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="84981-133">To enact credential encryption, a public key certificate must be available on the _Target Node_ that is **trusted** by the computer being used to author the DSC configuration.</span></span>
<span data-ttu-id="84981-134">Tento certifikát veřejného klíče má specifické požadavky, aby se používá pro šifrování přihlašovacích údajů DSC:</span><span class="sxs-lookup"><span data-stu-id="84981-134">This public key certificate has specific requirements for it to be used for DSC credential encryption:</span></span>

1. <span data-ttu-id="84981-135">**Použití klíče**:</span><span class="sxs-lookup"><span data-stu-id="84981-135">**Key Usage**:</span></span>
   - <span data-ttu-id="84981-136">Musí obsahovat: "KeyEncipherment" a "DataEncipherment".</span><span class="sxs-lookup"><span data-stu-id="84981-136">Must contain: 'KeyEncipherment' and 'DataEncipherment'.</span></span>
   - <span data-ttu-id="84981-137">By měl _není_ obsahovat: Digitální podpis.</span><span class="sxs-lookup"><span data-stu-id="84981-137">Should _not_ contain: 'Digital Signature'.</span></span>
2. <span data-ttu-id="84981-138">**Rozšířené použití klíče**:</span><span class="sxs-lookup"><span data-stu-id="84981-138">**Enhanced Key Usage**:</span></span>
   - <span data-ttu-id="84981-139">Musí obsahovat: Šifrování dokumentů (1.3.6.1.4.1.311.80.1).</span><span class="sxs-lookup"><span data-stu-id="84981-139">Must contain: Document Encryption (1.3.6.1.4.1.311.80.1).</span></span>
   - <span data-ttu-id="84981-140">By měl _není_ obsahovat: Ověření klienta (1.3.6.1.5.5.7.3.2) a ověření serveru (1.3.6.1.5.5.7.3.1).</span><span class="sxs-lookup"><span data-stu-id="84981-140">Should _not_ contain: Client Authentication (1.3.6.1.5.5.7.3.2) and Server Authentication (1.3.6.1.5.5.7.3.1).</span></span>
3. <span data-ttu-id="84981-141">Privátní klíč certifikátu je k dispozici na \* Node_ cíl.</span><span class="sxs-lookup"><span data-stu-id="84981-141">The Private Key for the certificate is available on the \*Target Node_.</span></span>
4. <span data-ttu-id="84981-142">**Poskytovatele** pro tento certifikát musí být "Microsoft RSA SChannel Cryptographic Provider".</span><span class="sxs-lookup"><span data-stu-id="84981-142">The **Provider** for the certificate must be "Microsoft RSA SChannel Cryptographic Provider".</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84981-143">I když používáte certifikát s obsahující použití klíče 'Digitální podpis' nebo některou z použití klíče ověřování, tím povolíte šifrovacího klíče na možné snadněji chybná a zranitelný vůči útoku.</span><span class="sxs-lookup"><span data-stu-id="84981-143">Although you can use a certificate with containing a Key Usage of 'Digital Signature' or one of the Authentication EKU's, this will enable the encryption key to be more easily misused and vulnerable to attack.</span></span> <span data-ttu-id="84981-144">Proto je osvědčeným postupem je použití certifikátu vytvořené speciálně pro účely zabezpečení přihlašovacích údajů DSC, která vynechává tyto použití klíče a rozšířená použití klíče.</span><span class="sxs-lookup"><span data-stu-id="84981-144">So it is best practice to use a certificate created specifically for the purpose of securing DSC credentials that omits these Key Usage and EKUs.</span></span>

<span data-ttu-id="84981-145">Všechny existující certifikát na _cílový uzel_ , že splňuje tyto kritéria lze použít na zabezpečené přihlašovací údaje DSC.</span><span class="sxs-lookup"><span data-stu-id="84981-145">Any existing certificate on the _Target Node_ that meets these criteria can be used to secure DSC credentials.</span></span>

## <a name="certificate-creation"></a><span data-ttu-id="84981-146">Vytvoření certifikátu</span><span class="sxs-lookup"><span data-stu-id="84981-146">Certificate creation</span></span>

<span data-ttu-id="84981-147">Existují dva přístupy, které si můžete vytvořit a použít požadované šifrovací certifikát (pár veřejného a privátního klíče).</span><span class="sxs-lookup"><span data-stu-id="84981-147">There are two approaches you can take to create and use the required Encryption Certificate (public-private key pair).</span></span>

1. <span data-ttu-id="84981-148">Vytvořit v **cílový uzel** a exportovat pouze veřejný klíč, který **vytváření uzlu**</span><span class="sxs-lookup"><span data-stu-id="84981-148">Create it on the **Target Node** and export just the public key to the **Authoring Node**</span></span>
2. <span data-ttu-id="84981-149">Vytvořit v **vytváření uzel** a exportovat celé dvojici klíčů k **cílový uzel**</span><span class="sxs-lookup"><span data-stu-id="84981-149">Create it on the **Authoring Node** and export the entire key pair to the **Target Node**</span></span>

<span data-ttu-id="84981-150">Metoda 1 se doporučuje, protože privátní klíč používaný k dešifrování přihlašovacích údajů v soubor MOF táhnou za jeden cílový uzel za všech okolností.</span><span class="sxs-lookup"><span data-stu-id="84981-150">Method 1 is recommended because the private key used to decrypt credentials in the MOF stays on the Target Node at all times.</span></span>

### <a name="creating-the-certificate-on-the-target-node"></a><span data-ttu-id="84981-151">Vytvoření certifikátu na cílový uzel</span><span class="sxs-lookup"><span data-stu-id="84981-151">Creating the Certificate on the Target Node</span></span>

<span data-ttu-id="84981-152">Privátní klíč musí být udržen v tajnosti, protože se používá k dešifrování soubor MOF v **cílový uzel** je nejjednodušší způsob, jak to udělat k vytvoření certifikátu privátního klíče na **cílový uzel**a zkopírujte  **certifikát veřejného klíče** do počítače se použije k vytvoření konfigurace DSC do souboru MOF.</span><span class="sxs-lookup"><span data-stu-id="84981-152">The private key must be kept secret, because is used to decrypt the MOF on the **Target Node** The easiest way to do that is to create the private key certificate on the **Target Node**, and copy the **public key certificate** to the computer being used to author the DSC configuration into a MOF file.</span></span>
<span data-ttu-id="84981-153">V následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="84981-153">The following example:</span></span>

1. <span data-ttu-id="84981-154">vytvoří certifikát na **cílový uzel**</span><span class="sxs-lookup"><span data-stu-id="84981-154">creates a certificate on the **Target node**</span></span>
2. <span data-ttu-id="84981-155">Exportuje certifikátu veřejného klíče na **cílový uzel**.</span><span class="sxs-lookup"><span data-stu-id="84981-155">exports the public key certificate on the **Target node**.</span></span>
3. <span data-ttu-id="84981-156">Importuje certifikát veřejného klíče do **Moje** úložiště certifikátů na **vytváření obsahu uzlu**.</span><span class="sxs-lookup"><span data-stu-id="84981-156">imports the public key certificate into the **my** certificate store on the **Authoring node**.</span></span>

#### <a name="on-the-target-node-create-and-export-the-certificate"></a><span data-ttu-id="84981-157">Na cílovém uzlu: vytvoření a export certifikátu</span><span class="sxs-lookup"><span data-stu-id="84981-157">On the Target Node: create and export the certificate</span></span>

> <span data-ttu-id="84981-158">Cílový uzel: Windows Server 2016 a Windows 10</span><span class="sxs-lookup"><span data-stu-id="84981-158">Target Node: Windows Server 2016 and Windows 10</span></span>

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```

<span data-ttu-id="84981-159">Jednou exportovat `DscPublicKey.cer` by bylo potřeba zkopírovat do **vytváření uzel**.</span><span class="sxs-lookup"><span data-stu-id="84981-159">Once exported, the `DscPublicKey.cer` would need to be copied to the **Authoring Node**.</span></span>

> <span data-ttu-id="84981-160">Cílový uzel: Windows Server 2012 R2 nebo Windows 8.1 a starší</span><span class="sxs-lookup"><span data-stu-id="84981-160">Target Node: Windows Server 2012 R2/Windows 8.1 and earlier</span></span>
> [!WARNING]
> <span data-ttu-id="84981-161">Protože `New-SelfSignedCertificate` rutiny ve Windows operačních systémech starších než Windows 10 a Windows Server 2016 nepodporuje **typ** parametr, alternativní způsob vytváření tento certifikát je nutný v těchto operačních systémech.</span><span class="sxs-lookup"><span data-stu-id="84981-161">Because the `New-SelfSignedCertificate` cmdlet on Windows Operating Systems prior to Windows 10 and Windows Server 2016 do not support the **Type** parameter, an alternate method of creating this certificate is required on these operating systems.</span></span>
>
> <span data-ttu-id="84981-162">V tomto případě můžete použít `makecert.exe` nebo `certutil.exe` k vytvoření certifikátu.</span><span class="sxs-lookup"><span data-stu-id="84981-162">In this case you can use `makecert.exe` or `certutil.exe` to create the certificate.</span></span>
>
><span data-ttu-id="84981-163">Alternativní způsob je [stáhnout skript New-SelfSignedCertificateEx.ps1 z webu Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) a použít ho k vytvoření certifikátu místo toho:</span><span class="sxs-lookup"><span data-stu-id="84981-163">An alternate method is to [download the New-SelfSignedCertificateEx.ps1 script from Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) and use it to create the certificate instead:</span></span>

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

<span data-ttu-id="84981-164">Jednou exportovat ```DscPublicKey.cer``` by bylo potřeba zkopírovat do **vytváření uzel**.</span><span class="sxs-lookup"><span data-stu-id="84981-164">Once exported, the ```DscPublicKey.cer``` would need to be copied to the **Authoring Node**.</span></span>

#### <a name="on-the-authoring-node-import-the-certs-public-key"></a><span data-ttu-id="84981-165">V uzlu pro tvorbu: Importovat veřejný klíč certifikátu</span><span class="sxs-lookup"><span data-stu-id="84981-165">On the Authoring Node: import the cert’s public key</span></span>

```powershell
# Import to the my store
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

### <a name="creating-the-certificate-on-the-authoring-node"></a><span data-ttu-id="84981-166">Vytvoření certifikátu pro vytváření obsahu uzlu</span><span class="sxs-lookup"><span data-stu-id="84981-166">Creating the Certificate on the Authoring Node</span></span>

<span data-ttu-id="84981-167">Alternativně se dají vytvořit šifrovací certifikát na **vytváření uzel**, exportovaný s **privátní klíč** jako PFX soubor a potom naimportovat **cílový uzel**.</span><span class="sxs-lookup"><span data-stu-id="84981-167">Alternately, the encryption certificate can be created on the **Authoring Node**, exported with the **private key** as a PFX file and then imported on the **Target Node**.</span></span>
<span data-ttu-id="84981-168">Toto je aktuální metody pro implementaci šifrování přihlašovacích údajů DSC v _Nano Server_.</span><span class="sxs-lookup"><span data-stu-id="84981-168">This is the current method for implementing DSC credential encryption on _Nano Server_.</span></span>
<span data-ttu-id="84981-169">I když soubor PFX je zabezpečený pomocí hesla by měla být ukázal jako nedocenitelný zabezpečené během přenosu.</span><span class="sxs-lookup"><span data-stu-id="84981-169">Although the PFX is secured with a password it should be kept secure during transit.</span></span>
<span data-ttu-id="84981-170">V následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="84981-170">The following example:</span></span>

1. <span data-ttu-id="84981-171">vytvoří certifikát na **vytváření obsahu uzlu**.</span><span class="sxs-lookup"><span data-stu-id="84981-171">creates a certificate on the **Authoring node**.</span></span>
2. <span data-ttu-id="84981-172">Exportuje včetně soukromého klíče v certifikátu **vytváření obsahu uzlu**.</span><span class="sxs-lookup"><span data-stu-id="84981-172">exports the certificate including the private key on the **Authoring node**.</span></span>
3. <span data-ttu-id="84981-173">Odstraní privátní klíč z **vytváření obsahu uzlu**, uchová certifikátu veřejného klíče, ale **Moje** ukládat.</span><span class="sxs-lookup"><span data-stu-id="84981-173">removes the private key from the **Authoring node**, but keeps the public key certificate in the **my** store.</span></span>
4. <span data-ttu-id="84981-174">provede import certifikátu privátního klíče do úložiště certifikátů My(Personal) na **cílový uzel**.</span><span class="sxs-lookup"><span data-stu-id="84981-174">imports the private key certificate into the My(Personal) certificate store on the **Target node**.</span></span>
   - <span data-ttu-id="84981-175">musí být přidán do kořenového úložiště tak, aby se důvěryhodná **cílový uzel**.</span><span class="sxs-lookup"><span data-stu-id="84981-175">it must be added to the root store so that it will be trusted by the **Target node**.</span></span>

#### <a name="on-the-authoring-node-create-and-export-the-certificate"></a><span data-ttu-id="84981-176">V uzlu pro tvorbu: vytvoření a export certifikátu</span><span class="sxs-lookup"><span data-stu-id="84981-176">On the Authoring Node: create and export the certificate</span></span>

> <span data-ttu-id="84981-177">Cílový uzel: Windows Server 2016 a Windows 10</span><span class="sxs-lookup"><span data-stu-id="84981-177">Target Node: Windows Server 2016 and Windows 10</span></span>

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

<span data-ttu-id="84981-178">Po exportu `DscPrivateKey.pfx` by bylo potřeba zkopírovat do **cílový uzel**.</span><span class="sxs-lookup"><span data-stu-id="84981-178">Once exported, the `DscPrivateKey.pfx` would need to be copied to the **Target Node**.</span></span>

> <span data-ttu-id="84981-179">Cílový uzel: Windows Server 2012 R2 nebo Windows 8.1 a starší</span><span class="sxs-lookup"><span data-stu-id="84981-179">Target Node: Windows Server 2012 R2/Windows 8.1 and earlier</span></span>
> [!WARNING]
> <span data-ttu-id="84981-180">Protože `New-SelfSignedCertificate` rutiny ve Windows operačních systémech starších než Windows 10 a Windows Server 2016 nepodporuje **typ** parametr, alternativní způsob vytváření tento certifikát je nutný v těchto operačních systémech.</span><span class="sxs-lookup"><span data-stu-id="84981-180">Because the `New-SelfSignedCertificate` cmdlet on Windows Operating Systems prior to Windows 10 and Windows Server 2016 do not support the **Type** parameter, an alternate method of creating this certificate is required on these operating systems.</span></span>
>
> <span data-ttu-id="84981-181">V tomto případě můžete použít `makecert.exe` nebo `certutil.exe` k vytvoření certifikátu.</span><span class="sxs-lookup"><span data-stu-id="84981-181">In this case you can use `makecert.exe` or `certutil.exe` to create the certificate.</span></span>
>
> <span data-ttu-id="84981-182">Alternativní způsob je [stáhnout skript New-SelfSignedCertificateEx.ps1 z webu Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) a použít ho k vytvoření certifikátu místo toho:</span><span class="sxs-lookup"><span data-stu-id="84981-182">An alternate method is to [download the New-SelfSignedCertificateEx.ps1 script from Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) and use it to create the certificate instead:</span></span>

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

#### <a name="on-the-target-node-import-the-certs-private-key-as-a-trusted-root"></a><span data-ttu-id="84981-183">Na cílovém uzlu: import certifikátu privátní klíč jako důvěryhodné kořenové</span><span class="sxs-lookup"><span data-stu-id="84981-183">On the Target Node: import the cert’s private key as a trusted root</span></span>

```powershell
# Import to the root store so that it is trusted
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
Import-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -CertStoreLocation Cert:\LocalMachine\My -Password $mypwd > $null
```

## <a name="configuration-data"></a><span data-ttu-id="84981-184">Konfigurační data</span><span class="sxs-lookup"><span data-stu-id="84981-184">Configuration data</span></span>

<span data-ttu-id="84981-185">Blok dat konfigurace definuje cílové uzly, na kterých pracují na tom, zda nebo šifrovat přihlašovací údaje, znamená, že šifrování a dalších informací.</span><span class="sxs-lookup"><span data-stu-id="84981-185">The configuration data block defines which target nodes to operate on, whether or not to encrypt the credentials, the means of encryption, and other information.</span></span> <span data-ttu-id="84981-186">Další informace o konfiguraci datového bloku, naleznete v tématu [oddělení konfiguraci a Data prostředí](../configurations/configData.md).</span><span class="sxs-lookup"><span data-stu-id="84981-186">For more information on the configuration data block, see [Separating Configuration and Environment Data](../configurations/configData.md).</span></span>

<span data-ttu-id="84981-187">Prvky, které je možné nakonfigurovat pro každý uzel, ke které se vztahují k šifrování přihlašovacích údajů jsou:</span><span class="sxs-lookup"><span data-stu-id="84981-187">The elements that can be configured for each node that are related to credential encryption are:</span></span>

- <span data-ttu-id="84981-188">**NodeName** – název nakonfigurované šifrování přihlašovacích údajů pro cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="84981-188">**NodeName** - the name of the target node that the credential encryption is being configured for.</span></span>
- <span data-ttu-id="84981-189">**PsDscAllowPlainTextPassword** – ať už se bude moct nezašifrované přihlašovací údaje předávat do tohoto uzlu.</span><span class="sxs-lookup"><span data-stu-id="84981-189">**PsDscAllowPlainTextPassword** - whether unencrypted credentials will be allowed to be passed to this node.</span></span> <span data-ttu-id="84981-190">Toto je **ale nedoporučený krok**.</span><span class="sxs-lookup"><span data-stu-id="84981-190">This is **not recommended**.</span></span>
- <span data-ttu-id="84981-191">**Kryptografický otisk** – kryptografický otisk certifikátu, který se použije k dešifrování přihlašovacích údajů v konfiguraci DSC na _cílový uzel_.</span><span class="sxs-lookup"><span data-stu-id="84981-191">**Thumbprint** - the thumbprint of the certificate that will be used to decrypt the credentials in the DSC Configuration on the _Target Node_.</span></span> <span data-ttu-id="84981-192">**Tento certifikát musí existovat v úložišti certifikátů místního počítače na cílový uzel.**</span><span class="sxs-lookup"><span data-stu-id="84981-192">**This certificate must exist in the Local Machine certificate store on the Target Node.**</span></span>
- <span data-ttu-id="84981-193">**CertificateFile** – soubor certifikátu (který obsahuje pouze veřejný klíč), který má použít k šifrování přihlašovacích údajů pro _cílový uzel_.</span><span class="sxs-lookup"><span data-stu-id="84981-193">**CertificateFile** - the certificate file (containing the public key only) that should be used to encrypt the credentials for the _Target Node_.</span></span> <span data-ttu-id="84981-194">Musí se jednat buď Binární X.509, kódování DER nebo soubor certifikátu formátu X.509 s kódováním Base-64.</span><span class="sxs-lookup"><span data-stu-id="84981-194">This must be either a DER encoded binary X.509 or Base-64 encoded X.509 format certificate file.</span></span>

<span data-ttu-id="84981-195">Tento příklad ukazuje blok dat konfigurace, který určuje cílový uzel tak, aby fungoval na pojmenované targetNode, cestu k souboru certifikátu veřejného klíče (s názvem targetNode.cer) a kryptografický otisk pro veřejný klíč.</span><span class="sxs-lookup"><span data-stu-id="84981-195">This example shows a configuration data block that specifies a target node to act on named targetNode, the path to the public key certificate file (named targetNode.cer), and the thumbprint for the public key.</span></span>

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

## <a name="configuration-script"></a><span data-ttu-id="84981-196">Konfigurační skript</span><span class="sxs-lookup"><span data-stu-id="84981-196">Configuration script</span></span>

<span data-ttu-id="84981-197">V samotný skript konfigurace, použijte `PsCredential` parametr Ujistěte se, že přihlašovací údaje jsou uložené pro nejkratší možné době.</span><span class="sxs-lookup"><span data-stu-id="84981-197">In the configuration script itself, use the `PsCredential` parameter to ensure that credentials are stored for the shortest possible time.</span></span> <span data-ttu-id="84981-198">Při spuštění zadaný příklad DSC bude vyzve k zadání přihlašovacích údajů a zašifrování souboru MOF pomocí CertificateFile, který je přidružený cílový uzel v bloku dat konfigurace.</span><span class="sxs-lookup"><span data-stu-id="84981-198">When you run the supplied example, DSC will prompt you for credentials and then encrypt the MOF file using the CertificateFile that is associated with the target node in the configuration data block.</span></span> <span data-ttu-id="84981-199">Tento příklad kódu ze sdílené složky, která je zabezpečena zkopíruje soubor na uživatele.</span><span class="sxs-lookup"><span data-stu-id="84981-199">This code example copies a file from a share that is secured to a user.</span></span>

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

## <a name="setting-up-decryption"></a><span data-ttu-id="84981-200">Nastavení dešifrování</span><span class="sxs-lookup"><span data-stu-id="84981-200">Setting up decryption</span></span>

<span data-ttu-id="84981-201">Před [ `Start-DscConfiguration` ](https://technet.microsoft.com/library/dn521623.aspx) můžete pracovat, je nutné zjistit Local Configuration Manageru na každém cílovém uzlu, který certifikát se má použít k dešifrování přihlašovacích údajů, pomocí prostředků CertificateID ověřit kryptografický otisk certifikátu.</span><span class="sxs-lookup"><span data-stu-id="84981-201">Before [`Start-DscConfiguration`](https://technet.microsoft.com/library/dn521623.aspx) can work, you have to tell the Local Configuration Manager on each target node which certificate to use to decrypt the credentials, using the CertificateID resource to verify the certificate’s thumbprint.</span></span> <span data-ttu-id="84981-202">Tuto ukázkovou funkci najdete příslušné místní certifikát (může mít vlastní nastavení, takže se přesně certifikát, který chcete použít):</span><span class="sxs-lookup"><span data-stu-id="84981-202">This example function will find the appropriate local certificate (you might have to customize it so it will find the exact certificate you want to use):</span></span>

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

<span data-ttu-id="84981-203">S certifikátem identifikován jeho kryptografický otisk konfigurační skript aktualizovat tak, použijte hodnotu:</span><span class="sxs-lookup"><span data-stu-id="84981-203">With the certificate identified by its thumbprint, the configuration script can be updated to use the value:</span></span>

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

## <a name="running-the-configuration"></a><span data-ttu-id="84981-204">Konfigurace spuštění</span><span class="sxs-lookup"><span data-stu-id="84981-204">Running the configuration</span></span>

<span data-ttu-id="84981-205">V tomto okamžiku spustíte konfiguraci, která bude výstup dva soubory:</span><span class="sxs-lookup"><span data-stu-id="84981-205">At this point, you can run the configuration, which will output two files:</span></span>

- <span data-ttu-id="84981-206">A \*. meta.mof soubor, který konfiguruje Local Configuration Manageru k dešifrování přihlašovacích údajů pomocí certifikátu, který je uložen v úložišti místního počítače a identifikován jeho kryptografický otisk.</span><span class="sxs-lookup"><span data-stu-id="84981-206">A \*.meta.mof file that configures the Local Configuration Manager to decrypt the credentials using the certificate that is stored on the local machine store and identified by its thumbprint.</span></span> <span data-ttu-id="84981-207">[`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/library/dn521621.aspx) se vztahuje \*. meta.mof souboru.</span><span class="sxs-lookup"><span data-stu-id="84981-207">[`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/library/dn521621.aspx) applies the \*.meta.mof file.</span></span>
- <span data-ttu-id="84981-208">Soubor MOF, který ve skutečnosti aplikuje konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="84981-208">A MOF file that actually applies the configuration.</span></span> <span data-ttu-id="84981-209">Start-DscConfiguration aplikuje konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="84981-209">Start-DscConfiguration applies the configuration.</span></span>

<span data-ttu-id="84981-210">Tyto příkazy bude provádět tyto kroky:</span><span class="sxs-lookup"><span data-stu-id="84981-210">These commands will accomplish those steps:</span></span>

```powershell
Write-Host "Generate DSC Configuration..."
CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample

Write-Host "Setting up LCM to decrypt credentials..."
Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose

Write-Host "Starting Configuration..."
Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose
```

<span data-ttu-id="84981-211">V tomto příkladu by nabízená konfigurace DSC na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="84981-211">This example would push the DSC configuration to the target node.</span></span>
<span data-ttu-id="84981-212">Konfigurace DSC můžete použít také pomocí serveru vyžádané replikace DSC, pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="84981-212">The DSC configuration can also be applied using a DSC Pull Server if one is available.</span></span>

<span data-ttu-id="84981-213">Zobrazit [nastavení načítacího klienta DSC](pullClient.md) Další informace o použití konfigurací DSC pomocí serveru vyžádané replikace DSC.</span><span class="sxs-lookup"><span data-stu-id="84981-213">See [Setting up a DSC pull client](pullClient.md) for more information on applying DSC configurations using a DSC Pull Server.</span></span>

## <a name="credential-encryption-module-example"></a><span data-ttu-id="84981-214">Příklad modulu šifrování přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="84981-214">Credential Encryption Module Example</span></span>

<span data-ttu-id="84981-215">Tady je úplný příklad, který zahrnuje všechny tyto kroky a pomocné rutiny, který exportuje a zkopíruje veřejných klíčů:</span><span class="sxs-lookup"><span data-stu-id="84981-215">Here is a full example that incorporates all of these steps, plus a helper cmdlet that exports and copies the public keys:</span></span>

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
