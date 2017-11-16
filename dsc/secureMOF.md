---
ms.date: 2017-10-31
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Zabezpečení souboru MOF"
ms.openlocfilehash: f4ef2962710c7458ac947bf33270175a09de643c
ms.sourcegitcommit: 4807ab554d55fdee499980835bcc279368b1df68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2017
---
# <a name="securing-the-mof-file"></a><span data-ttu-id="400f6-103">Zabezpečení souboru MOF</span><span class="sxs-lookup"><span data-stu-id="400f6-103">Securing the MOF File</span></span>

><span data-ttu-id="400f6-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="400f6-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="400f6-105">DSC spravuje konfigurace uzlů serveru pomocí informace uložené v souboru MOF, kde místní Configuration Manager (LCM) implementuje požadované koncové stavu.</span><span class="sxs-lookup"><span data-stu-id="400f6-105">DSC manages the configuration of server nodes by applying information stored in a MOF file, where the Local Configuration Manager (LCM) implements the desired end state.</span></span>
<span data-ttu-id="400f6-106">Protože tento soubor obsahuje podrobnosti o konfiguraci, je důležité k lepšímu zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="400f6-106">Because this file contains the details of the configuration, it’s important to keep it secure.</span></span>
<span data-ttu-id="400f6-107">Toto téma popisuje, jak na cílový uzel je šifrovaný soubor.</span><span class="sxs-lookup"><span data-stu-id="400f6-107">This topic describes how to ensure the target node has encrypted the file.</span></span>

<span data-ttu-id="400f6-108">Od verze prostředí PowerShell, verze 5.0, celý soubor MOF je zašifrovaná ve výchozím nastavení při použití na uzlu pomocí **Start-DSCConfiguration** rutiny.</span><span class="sxs-lookup"><span data-stu-id="400f6-108">Beginning with PowerShell version 5.0, the entire MOF file is encrypted by default when it is applied to the node using the **Start-DSCConfiguration** cmdlet.</span></span>
<span data-ttu-id="400f6-109">Proces popsaný v tomto článku se vyžaduje jenom v případě, že implementaci řešení pro použití protokolu vyžádání obsahu, pokud nejsou spravovány certifikáty, aby konfigurace stáhne cílový uzel může dešifrovat a číst systému před jejich instalací (například službu vyžádání obsahu k dispozici v systému Windows Server).</span><span class="sxs-lookup"><span data-stu-id="400f6-109">The process described in this article is required only when implementing a solution using the pull service protocol if certificates are not managed, to ensure configurations downloaded by the target node can be decrypted and read by the system before they are applied (for example, the pull service available in Windows Server).</span></span>
<span data-ttu-id="400f6-110">Uzly zaregistrované [Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview) bude automaticky certifikáty instalaci a spravuje službu s žádné režijní náklady na správu požadované.</span><span class="sxs-lookup"><span data-stu-id="400f6-110">Nodes registered to [Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview) will automatically have certificates installed and managed by the service with no administrative overhead required.</span></span>

><span data-ttu-id="400f6-111">**Poznámka:** Toto téma popisuje certifikátů používaných pro šifrování.</span><span class="sxs-lookup"><span data-stu-id="400f6-111">**Note:** This topic discusses certificates used for encryption.</span></span>
><span data-ttu-id="400f6-112">Certifikát podepsaný svým držitelem pro šifrování, stačí, protože privátní klíč je vždy tajný klíč a šifrování neznamená důvěryhodnosti dokumentu.</span><span class="sxs-lookup"><span data-stu-id="400f6-112">For encryption, a self-signed certificate is sufficient, because the private key is always kept secret and encryption does not imply trust of the document.</span></span>
><span data-ttu-id="400f6-113">Certifikáty podepsané svým držitelem by *není* být použito pro účely ověřování.</span><span class="sxs-lookup"><span data-stu-id="400f6-113">Self-signed certificates should *not* be used for authentication purposes.</span></span>
><span data-ttu-id="400f6-114">Měli byste použít certifikát od důvěryhodné certifikační autority (CA) k jakýmkoli jiným účelům ověřování.</span><span class="sxs-lookup"><span data-stu-id="400f6-114">You should use a certificate from a trusted Certification Authority (CA) for any authentication purposes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="400f6-115">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="400f6-115">Prerequisites</span></span>

<span data-ttu-id="400f6-116">Chcete-li úspěšně šifrovat přihlašovací údaje používané k zabezpečení konfigurace DSC, ujistěte se, že máte následující:</span><span class="sxs-lookup"><span data-stu-id="400f6-116">To successfully encrypt the credentials used to secure a DSC configuration, make sure you have the following:</span></span>

* <span data-ttu-id="400f6-117">**Některé prostředky, vydávání a distribuci certifikátů**.</span><span class="sxs-lookup"><span data-stu-id="400f6-117">**Some means of issuing and distributing certificates**.</span></span> <span data-ttu-id="400f6-118">Toto téma a jeho příklady předpokládají, že používáte Active Directory certifikační autority.</span><span class="sxs-lookup"><span data-stu-id="400f6-118">This topic and its examples assume you are using Active Directory Certification Authority.</span></span> <span data-ttu-id="400f6-119">Pro další základní informace o službě Active Directory Certificate Services naleznete v tématu [přehled Active Directory Certificate Services](https://technet.microsoft.com/library/hh831740.aspx) a [Active Directory Certificate Services v systému Windows Server 2008](https://technet.microsoft.com/windowsserver/dd448615.aspx).</span><span class="sxs-lookup"><span data-stu-id="400f6-119">For more background information on Active Directory Certificate Services, see [Active Directory Certificate Services Overview](https://technet.microsoft.com/library/hh831740.aspx) and [Active Directory Certificate Services in Windows Server 2008](https://technet.microsoft.com/windowsserver/dd448615.aspx).</span></span>
* <span data-ttu-id="400f6-120">**Přístup pro správu na cílový uzel nebo uzly**.</span><span class="sxs-lookup"><span data-stu-id="400f6-120">**Administrative access to the target node or nodes**.</span></span>
* <span data-ttu-id="400f6-121">**Každý cílový uzel má certifikát podporující šifrování uložit jeho osobní úložiště**.</span><span class="sxs-lookup"><span data-stu-id="400f6-121">**Each target node has an encryption-capable certificate saved its Personal Store**.</span></span> <span data-ttu-id="400f6-122">V prostředí Windows PowerShell je cesta k úložišti Cert: \LocalMachine\My.</span><span class="sxs-lookup"><span data-stu-id="400f6-122">In Windows PowerShell, the path to the store is Cert:\LocalMachine\My.</span></span> <span data-ttu-id="400f6-123">V příkladech v tomto tématu použijte šablonu "ověřování pracovní stanice", které můžete vyhledat (spolu s další šablony certifikátů) v [výchozí šablony certifikátů](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="400f6-123">The examples in this topic use the “workstation authentication” template, which you can find (along with other certificate templates) at [Default Certificate Templates](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).</span></span>
* <span data-ttu-id="400f6-124">Pokud budete používat tuto konfiguraci na jiném počítači než cílový uzel **exportujte veřejný klíč certifikátu**a importujte ho do počítače se spustí konfiguraci z.</span><span class="sxs-lookup"><span data-stu-id="400f6-124">If you will be running this configuration on a computer other than the target node, **export the public key of the certificate**, and then import it to the computer you will run the configuration from.</span></span> <span data-ttu-id="400f6-125">Ujistěte se, že exportujete pouze **veřejné** klíče; zabezpečit privátní klíč.</span><span class="sxs-lookup"><span data-stu-id="400f6-125">Make sure that you export only the **public** key; keep the private key secure.</span></span>

## <a name="overall-process"></a><span data-ttu-id="400f6-126">Celkový proces</span><span class="sxs-lookup"><span data-stu-id="400f6-126">Overall process</span></span>

 1. <span data-ttu-id="400f6-127">Nastavení klíče, certifikátů a kryptografických otisků, a ujistěte se, že každý cílový uzel má kopie certifikátu a v počítači konfigurace je veřejný klíč a kryptografický otisk.</span><span class="sxs-lookup"><span data-stu-id="400f6-127">Set up the certificates, keys, and thumbprints, making sure that each target node has copies of the certificate and the configuration computer has the public key and thumbprint.</span></span>
 2. <span data-ttu-id="400f6-128">Vytvořte blok dat konfigurace, který obsahuje cestu a kryptografický otisk veřejný klíč.</span><span class="sxs-lookup"><span data-stu-id="400f6-128">Create a configuration data block that contains the path and thumbprint of the public key.</span></span>
 3. <span data-ttu-id="400f6-129">Vytvořte konfigurační skript, který definuje požadovanou konfiguraci pro cílový uzel a nastaví dešifrování na cílové uzly podle tvorba příkazů konfiguraci místního správce k dešifrování dat konfigurace pomocí certifikátu a jeho kryptografický otisk.</span><span class="sxs-lookup"><span data-stu-id="400f6-129">Create a configuration script that defines your desired configuration for the target node and sets up decryption on the target nodes by commanding the Local Configuration manager to decrypt the configuration data using the certificate and its thumbprint.</span></span>
 4. <span data-ttu-id="400f6-130">Spusťte konfigurace, který bude nastavení správce místní konfigurace a spuštění konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="400f6-130">Run the configuration, which will set the Local Configuration Manager settings and start the DSC configuration.</span></span>

![Diagram1](images/CredentialEncryptionDiagram1.png)

## <a name="certificate-requirements"></a><span data-ttu-id="400f6-132">Požadavky na certifikát</span><span class="sxs-lookup"><span data-stu-id="400f6-132">Certificate Requirements</span></span>

<span data-ttu-id="400f6-133">K uplatní šifrování přihlašovacích údajů, musí být k dispozici na certifikátu veřejného klíče _cílový uzel_ tedy **důvěryhodné** pro počítač používá k vytváření konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="400f6-133">To enact credential encryption, a public key certificate must be available on the _Target Node_ that is **trusted** by the computer being used to author the DSC configuration.</span></span>
<span data-ttu-id="400f6-134">Certifikát veřejného klíče má specifické požadavky pro něj má být použit pro šifrování přihlašovacích údajů DSC:</span><span class="sxs-lookup"><span data-stu-id="400f6-134">This public key certificate has specific requirements for it to be used for DSC credential encryption:</span></span>
 1. <span data-ttu-id="400f6-135">**Použití klíče**:</span><span class="sxs-lookup"><span data-stu-id="400f6-135">**Key Usage**:</span></span>
   - <span data-ttu-id="400f6-136">Musí obsahovat: 'KeyEncipherment' a 'DataEncipherment'.</span><span class="sxs-lookup"><span data-stu-id="400f6-136">Must contain: 'KeyEncipherment' and 'DataEncipherment'.</span></span>
   - <span data-ttu-id="400f6-137">Měli _není_ obsahovat: 'Digitální podpis'.</span><span class="sxs-lookup"><span data-stu-id="400f6-137">Should _not_ contain: 'Digital Signature'.</span></span>
 2. <span data-ttu-id="400f6-138">**Rozšířené použití klíče**:</span><span class="sxs-lookup"><span data-stu-id="400f6-138">**Enhanced Key Usage**:</span></span>
   - <span data-ttu-id="400f6-139">Musí obsahovat: šifrování dokumentů (1.3.6.1.4.1.311.80.1).</span><span class="sxs-lookup"><span data-stu-id="400f6-139">Must contain: Document Encryption (1.3.6.1.4.1.311.80.1).</span></span>
   - <span data-ttu-id="400f6-140">Měli _není_ obsahovat: ověření klienta (1.3.6.1.5.5.7.3.2) a ověření serveru (1.3.6.1.5.5.7.3.1).</span><span class="sxs-lookup"><span data-stu-id="400f6-140">Should _not_ contain: Client Authentication (1.3.6.1.5.5.7.3.2) and Server Authentication (1.3.6.1.5.5.7.3.1).</span></span>
 3. <span data-ttu-id="400f6-141">Soukromý klíč pro certifikát je k dispozici na * Node_ cíl.</span><span class="sxs-lookup"><span data-stu-id="400f6-141">The Private Key for the certificate is available on the *Target Node_.</span></span>
 4. <span data-ttu-id="400f6-142">**Zprostředkovatele** pro certifikát musí být "Microsoft RSA SChannel Cryptographic Provider".</span><span class="sxs-lookup"><span data-stu-id="400f6-142">The **Provider** for the certificate must be "Microsoft RSA SChannel Cryptographic Provider".</span></span>
 
><span data-ttu-id="400f6-143">**Doporučený osvědčený postup:** i když používáte certifikát s obsahující použití klíče, digitální podpis, nebo jednoho z ověřování EKU tím povolíte šifrovacího klíče se snadněji chybná a bude zranitelný vůči útoku.</span><span class="sxs-lookup"><span data-stu-id="400f6-143">**Recommended Best Practice:** Although you can use a certificate with containing a Key Usage of 'Digital Signature' or one of the Authentication EKU's, this will enable the encryption key to be more easily misused and vulnerable to attack.</span></span> <span data-ttu-id="400f6-144">Proto je vhodné používat certifikát vytvořena speciálně pro účely zabezpečení DSC pověření, který vynechá tyto použití klíče a rozšířená použití klíče.</span><span class="sxs-lookup"><span data-stu-id="400f6-144">So it is best practice to use a certificate created specifically for the purpose of securing DSC credentials that omits these Key Usage and EKUs.</span></span>
  
<span data-ttu-id="400f6-145">Všechny existující certifikát na _cílový uzel_ , že splňuje tyto kritéria slouží k zabezpečené přihlašovací údaje DSC.</span><span class="sxs-lookup"><span data-stu-id="400f6-145">Any existing certificate on the _Target Node_ that meets these criteria can be used to secure DSC credentials.</span></span>

## <a name="certificate-creation"></a><span data-ttu-id="400f6-146">Vytvoření certifikátu</span><span class="sxs-lookup"><span data-stu-id="400f6-146">Certificate creation</span></span>

<span data-ttu-id="400f6-147">Existují dva přístupy, které můžete použít k vytváření a používání požadovaný certifikát šifrování (pár veřejného a privátního klíče).</span><span class="sxs-lookup"><span data-stu-id="400f6-147">There are two approaches you can take to create and use the required Encryption Certificate (public-private key pair).</span></span>

1. <span data-ttu-id="400f6-148">Vytvořte na **cílový uzel** a exportovat pouze veřejný klíč k **vytváření uzlu**</span><span class="sxs-lookup"><span data-stu-id="400f6-148">Create it on the **Target Node** and export just the public key to the **Authoring Node**</span></span>
2. <span data-ttu-id="400f6-149">Vytvořit na **vytváření uzlu** a celý páru klíčů pro export **cílový uzel.**</span><span class="sxs-lookup"><span data-stu-id="400f6-149">Create it on the **Authoring Node** and export the entire key pair to the **Target Node**</span></span>

<span data-ttu-id="400f6-150">Metoda 1 se doporučuje, protože privátní klíč používaný k dešifrování přihlašovací údaje v MOF zůstává na cílový uzel za všech okolností.</span><span class="sxs-lookup"><span data-stu-id="400f6-150">Method 1 is recommended because the private key used to decrypt credentials in the MOF stays on the Target Node at all times.</span></span>


### <a name="creating-the-certificate-on-the-target-node"></a><span data-ttu-id="400f6-151">Vytváření certifikátu na cílovém uzlu</span><span class="sxs-lookup"><span data-stu-id="400f6-151">Creating the Certificate on the Target Node</span></span>

<span data-ttu-id="400f6-152">Privátní klíč musí být udržovány tajný, protože se používá k dešifrování MOF na **cílový uzel** je nejjednodušší způsob, jak to udělat k vytvoření certifikátu privátního klíče na **cílový uzel**a zkopírujte  **certifikát veřejného klíče** k počítači používá k vytváření konfigurace DSC do souboru MOF.</span><span class="sxs-lookup"><span data-stu-id="400f6-152">The private key must be kept secret, because is used to decrypt the MOF on the **Target Node** The easiest way to do that is to create the private key certificate on the **Target Node**, and copy the **public key certificate** to the computer being used to author the DSC configuration into a MOF file.</span></span>
<span data-ttu-id="400f6-153">V následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="400f6-153">The following example:</span></span>
 1. <span data-ttu-id="400f6-154">vytvoří certifikát na **cílový uzel.**</span><span class="sxs-lookup"><span data-stu-id="400f6-154">creates a certificate on the **Target node**</span></span>
 2. <span data-ttu-id="400f6-155">Exportuje certifikátu veřejného klíče na **cílový uzel**.</span><span class="sxs-lookup"><span data-stu-id="400f6-155">exports the public key certificate on the **Target node**.</span></span>
 3. <span data-ttu-id="400f6-156">Importuje certifikátu veřejného klíče do **Moje** úložiště certifikátů na **vytváření uzlu**.</span><span class="sxs-lookup"><span data-stu-id="400f6-156">imports the public key certificate into the **my** certificate store on the **Authoring node**.</span></span>

#### <a name="on-the-target-node-create-and-export-the-certificate"></a><span data-ttu-id="400f6-157">Na cílovém uzlu: vytvoření a export certifikátu</span><span class="sxs-lookup"><span data-stu-id="400f6-157">On the Target Node: create and export the certificate</span></span>
><span data-ttu-id="400f6-158">Pro tvorbu uzlu: Windows Server 2016 a Windows 10</span><span class="sxs-lookup"><span data-stu-id="400f6-158">Authoring Node: Windows Server 2016 and Windows 10</span></span>

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```
<span data-ttu-id="400f6-159">Po exportu ```DscPublicKey.cer``` by bylo potřeba kopírovat do **vytváření uzlu**.</span><span class="sxs-lookup"><span data-stu-id="400f6-159">Once exported, the ```DscPublicKey.cer``` would need to be copied to the **Authoring Node**.</span></span>

><span data-ttu-id="400f6-160">Vytváření uzel: Windows Server 2012 R2 nebo Windows 8.1 a starší</span><span class="sxs-lookup"><span data-stu-id="400f6-160">Authoring Node: Windows Server 2012 R2/Windows 8.1 and earlier</span></span>

<span data-ttu-id="400f6-161">Protože rutinu New-SelfSignedCertificate na Windows operačních systémech starších než Windows 10 a Windows Server 2016 nepodporují **typ** parametr, alternativní metodu vytváření tohoto certifikátu je povinný, pokud k nim operační systémy.</span><span class="sxs-lookup"><span data-stu-id="400f6-161">Because the New-SelfSignedCertificate cmdlet on Windows Operating Systems prior to Windows 10 and Windows Server 2016 do not support the **Type** parameter, an alternate method of creating this certificate is required on these operating systems.</span></span>
<span data-ttu-id="400f6-162">V takovém případě můžete použít ```makecert.exe``` nebo ```certutil.exe``` k vytvoření certifikátu.</span><span class="sxs-lookup"><span data-stu-id="400f6-162">In this case you can use ```makecert.exe``` or ```certutil.exe``` to create the certificate.</span></span>

<span data-ttu-id="400f6-163">Je to alternativní metoda [stáhnout z webu Microsoft Script Center skript New-SelfSignedCertificateEx.ps1](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) a použít ho k vytvoření certifikátu místo:</span><span class="sxs-lookup"><span data-stu-id="400f6-163">An alternate method is to [download the New-SelfSignedCertificateEx.ps1 script from Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) and use it to create the certificate instead:</span></span>
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
    -StoreName 'My' `
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
<span data-ttu-id="400f6-164">Po exportu ```DscPublicKey.cer``` by bylo potřeba kopírovat do **vytváření uzlu**.</span><span class="sxs-lookup"><span data-stu-id="400f6-164">Once exported, the ```DscPublicKey.cer``` would need to be copied to the **Authoring Node**.</span></span>

#### <a name="on-the-authoring-node-import-the-certs-public-key"></a><span data-ttu-id="400f6-165">Na uzlu vytváření: import veřejného klíče certifikátu</span><span class="sxs-lookup"><span data-stu-id="400f6-165">On the Authoring Node: import the cert’s public key</span></span>
```powershell
# Import to the my store
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

### <a name="creating-the-certificate-on-the-authoring-node"></a><span data-ttu-id="400f6-166">Vytváření certifikátu na uzlu pro tvorbu</span><span class="sxs-lookup"><span data-stu-id="400f6-166">Creating the Certificate on the Authoring Node</span></span>
<span data-ttu-id="400f6-167">Alternativně lze vytvořit šifrovací certifikát na **vytváření uzlu**, exportovaný s **privátní klíč** jako PFX souboru a poté importovat na **cílový uzel**.</span><span class="sxs-lookup"><span data-stu-id="400f6-167">Alternately, the encryption certificate can be created on the **Authoring Node**, exported with the **private key** as a PFX file and then imported on the **Target Node**.</span></span>
<span data-ttu-id="400f6-168">Toto je aktuální metoda pro implementaci šifrování přihlašovacích údajů DSC na _Nano Server_.</span><span class="sxs-lookup"><span data-stu-id="400f6-168">This is the current method for implementing DSC credential encryption on _Nano Server_.</span></span>
<span data-ttu-id="400f6-169">I když soubor PFX je zabezpečen heslo se musí být zabezpečen během přenosu.</span><span class="sxs-lookup"><span data-stu-id="400f6-169">Although the PFX is secured with a password it should be kept secure during transit.</span></span>
<span data-ttu-id="400f6-170">V následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="400f6-170">The following example:</span></span>
 1. <span data-ttu-id="400f6-171">vytvoří certifikát na **vytváření uzlu**.</span><span class="sxs-lookup"><span data-stu-id="400f6-171">creates a certificate on the **Authoring node**.</span></span>
 2. <span data-ttu-id="400f6-172">Exportuje certifikát, včetně privátního klíče **vytváření uzlu**.</span><span class="sxs-lookup"><span data-stu-id="400f6-172">exports the certificate including the private key on the **Authoring node**.</span></span>
 3. <span data-ttu-id="400f6-173">Odebere privátní klíč z **vytváření uzlu**, ale zachová certifikátu veřejného klíče **Moje** uložit.</span><span class="sxs-lookup"><span data-stu-id="400f6-173">removes the private key from the **Authoring node**, but keeps the public key certificate in the **my** store.</span></span>
 4. <span data-ttu-id="400f6-174">Importuje certifikátu privátního klíče do kořenového úložiště certifikátů na **cílový uzel**.</span><span class="sxs-lookup"><span data-stu-id="400f6-174">imports the private key certificate into the root certificate store on the **Target node**.</span></span>
   - <span data-ttu-id="400f6-175">musí být přidané do kořenového úložiště tak, aby se důvěřují **cílový uzel**.</span><span class="sxs-lookup"><span data-stu-id="400f6-175">it must be added to the root store so that it will be trusted by the **Target node**.</span></span>

#### <a name="on-the-authoring-node-create-and-export-the-certificate"></a><span data-ttu-id="400f6-176">Na uzlu vytváření: vytvoření a export certifikátu</span><span class="sxs-lookup"><span data-stu-id="400f6-176">On the Authoring Node: create and export the certificate</span></span>
><span data-ttu-id="400f6-177">Cílový uzel: Windows Server 2016 a Windows 10</span><span class="sxs-lookup"><span data-stu-id="400f6-177">Target Node: Windows Server 2016 and Windows 10</span></span>

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
<span data-ttu-id="400f6-178">Po exportu ```DscPrivateKey.pfx``` by bylo potřeba kopírovat do **cílový uzel**.</span><span class="sxs-lookup"><span data-stu-id="400f6-178">Once exported, the ```DscPrivateKey.pfx``` would need to be copied to the **Target Node**.</span></span>

><span data-ttu-id="400f6-179">Cílový uzel: Windows Server 2012 R2 nebo Windows 8.1 a starší</span><span class="sxs-lookup"><span data-stu-id="400f6-179">Target Node: Windows Server 2012 R2/Windows 8.1 and earlier</span></span>

<span data-ttu-id="400f6-180">Protože rutinu New-SelfSignedCertificate na Windows operačních systémech starších než Windows 10 a Windows Server 2016 nepodporují **typ** parametr, alternativní metodu vytváření tohoto certifikátu je povinný, pokud k nim operační systémy.</span><span class="sxs-lookup"><span data-stu-id="400f6-180">Because the New-SelfSignedCertificate cmdlet on Windows Operating Systems prior to Windows 10 and Windows Server 2016 do not support the **Type** parameter, an alternate method of creating this certificate is required on these operating systems.</span></span>
<span data-ttu-id="400f6-181">V takovém případě můžete použít ```makecert.exe``` nebo ```certutil.exe``` k vytvoření certifikátu.</span><span class="sxs-lookup"><span data-stu-id="400f6-181">In this case you can use ```makecert.exe``` or ```certutil.exe``` to create the certificate.</span></span>

<span data-ttu-id="400f6-182">Je to alternativní metoda [stáhnout z webu Microsoft Script Center skript New-SelfSignedCertificateEx.ps1](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) a použít ho k vytvoření certifikátu místo:</span><span class="sxs-lookup"><span data-stu-id="400f6-182">An alternate method is to [download the New-SelfSignedCertificateEx.ps1 script from Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) and use it to create the certificate instead:</span></span>
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

#### <a name="on-the-target-node-import-the-certs-private-key-as-a-trusted-root"></a><span data-ttu-id="400f6-183">Na cílovém uzlu: import privátní klíč certifikátu jako důvěryhodné kořenové</span><span class="sxs-lookup"><span data-stu-id="400f6-183">On the Target Node: import the cert’s private key as a trusted root</span></span>
```powershell
# Import to the root store so that it is trusted
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
Import-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -CertStoreLocation Cert:\LocalMachine\Root -Password $mypwd > $null
```

## <a name="configuration-data"></a><span data-ttu-id="400f6-184">Konfigurační data</span><span class="sxs-lookup"><span data-stu-id="400f6-184">Configuration data</span></span>

<span data-ttu-id="400f6-185">Datový blok konfigurace definuje cílový uzlů, které fungují na tom, zda nebo šifrovat přihlašovací údaje, způsob šifrování a další informace.</span><span class="sxs-lookup"><span data-stu-id="400f6-185">The configuration data block defines which target nodes to operate on, whether or not to encrypt the credentials, the means of encryption, and other information.</span></span> <span data-ttu-id="400f6-186">Další informace o konfiguraci datového bloku najdete v tématu [oddělení konfigurace a Data prostředí](configData.md).</span><span class="sxs-lookup"><span data-stu-id="400f6-186">For more information on the configuration data block, see [Separating Configuration and Environment Data](configData.md).</span></span>

<span data-ttu-id="400f6-187">Prvky, které lze nastavit pro každý uzel, které se vztahují k šifrování přihlašovacích údajů jsou:</span><span class="sxs-lookup"><span data-stu-id="400f6-187">The elements that can be configured for each node that are related to credential encryption are:</span></span>
* <span data-ttu-id="400f6-188">**NodeName** -název cílového uzlu, který je nakonfigurováno šifrování přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="400f6-188">**NodeName** - the name of the target node that the credential encryption is being configured for.</span></span>
* <span data-ttu-id="400f6-189">**PsDscAllowPlainTextPassword** – ať nezašifrované přihlašovací údaje se bude moct být předána pro tento uzel.</span><span class="sxs-lookup"><span data-stu-id="400f6-189">**PsDscAllowPlainTextPassword** - whether unencrypted credentials will be allowed to be passed to this node.</span></span> <span data-ttu-id="400f6-190">Toto je **nedoporučuje**.</span><span class="sxs-lookup"><span data-stu-id="400f6-190">This is **not recommended**.</span></span>
* <span data-ttu-id="400f6-191">**Kryptografický otisk** -kryptografický otisk certifikátu, který se použije k dešifrování přihlašovací údaje v konfigurace DSC na _cílový uzel_.</span><span class="sxs-lookup"><span data-stu-id="400f6-191">**Thumbprint** - the thumbprint of the certificate that will be used to decrypt the credentials in the DSC Configuration on the _Target Node_.</span></span> <span data-ttu-id="400f6-192">**Tento certifikát musí existovat v úložišti certifikátů místního počítače na cílovém uzlu.**</span><span class="sxs-lookup"><span data-stu-id="400f6-192">**This certificate must exist in the Local Machine certificate store on the Target Node.**</span></span>
* <span data-ttu-id="400f6-193">**CertificateFile** – soubor certifikátu (obsahuje pouze veřejný klíč), který slouží k šifrování přihlašovacích údajů pro _cílový uzel_.</span><span class="sxs-lookup"><span data-stu-id="400f6-193">**CertificateFile** - the certificate file (containing the public key only) that should be used to encrypt the credentials for the _Target Node_.</span></span> <span data-ttu-id="400f6-194">Tato hodnota musí být buď Binární X.509, kódování DER nebo soubor certifikátu X.509 formátu s kódováním Base-64.</span><span class="sxs-lookup"><span data-stu-id="400f6-194">This must be either a DER encoded binary X.509 or Base-64 encoded X.509 format certificate file.</span></span>

<span data-ttu-id="400f6-195">Tento příklad ukazuje blok dat konfigurace, který určuje cílový uzel tak, aby fungoval na pojmenované cílovým uzlem, cestu k souboru certifikátu veřejného klíče (s názvem targetNode.cer) a kryptografický otisk pro veřejný klíč.</span><span class="sxs-lookup"><span data-stu-id="400f6-195">This example shows a configuration data block that specifies a target node to act on named targetNode, the path to the public key certificate file (named targetNode.cer), and the thumbprint for the public key.</span></span>

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


## <a name="configuration-script"></a><span data-ttu-id="400f6-196">Konfigurační skript</span><span class="sxs-lookup"><span data-stu-id="400f6-196">Configuration script</span></span>

<span data-ttu-id="400f6-197">V samotný skript konfigurace pomocí `PsCredential` parametr zajistit, že přihlašovací údaje jsou uloženy pro co nejdříve.</span><span class="sxs-lookup"><span data-stu-id="400f6-197">In the configuration script itself, use the `PsCredential` parameter to ensure that credentials are stored for the shortest possible time.</span></span> <span data-ttu-id="400f6-198">Když spustíte zadaný příklad, bude DSC výzvu k zadání pověření a zašifrování souboru MOF pomocí CertificateFile, který je přidružen k uzlu cíl v bloku dat konfigurace.</span><span class="sxs-lookup"><span data-stu-id="400f6-198">When you run the supplied example, DSC will prompt you for credentials and then encrypt the MOF file using the CertificateFile that is associated with the target node in the configuration data block.</span></span> <span data-ttu-id="400f6-199">Tento příklad kódu zkopíruje soubor ze sdílené složky, která je zabezpečená na uživatele.</span><span class="sxs-lookup"><span data-stu-id="400f6-199">This code example copies a file from a share that is secured to a user.</span></span>

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

## <a name="setting-up-decryption"></a><span data-ttu-id="400f6-200">Nastavení dešifrování</span><span class="sxs-lookup"><span data-stu-id="400f6-200">Setting up decryption</span></span>

<span data-ttu-id="400f6-201">Před [ `Start-DscConfiguration` ](https://technet.microsoft.com/en-us/library/dn521623.aspx) můžete pracovat, je nutné zjistit správce místní konfigurace na každý cílový uzel, který certifikát má použít k dešifrování přihlašovacích údajů, pomocí prostředků CertificateID ověření kryptografický otisk certifikátu.</span><span class="sxs-lookup"><span data-stu-id="400f6-201">Before [`Start-DscConfiguration`](https://technet.microsoft.com/en-us/library/dn521623.aspx) can work, you have to tell the Local Configuration Manager on each target node which certificate to use to decrypt the credentials, using the CertificateID resource to verify the certificate’s thumbprint.</span></span> <span data-ttu-id="400f6-202">Tento příklad funkce se najít odpovídající místní certifikát (bude pravděpodobně nutné přizpůsobit ho tak najde přesný certifikátu, který chcete použít):</span><span class="sxs-lookup"><span data-stu-id="400f6-202">This example function will find the appropriate local certificate (you might have to customize it so it will find the exact certificate you want to use):</span></span>

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

<span data-ttu-id="400f6-203">Se identifikovanou pomocí jeho kryptografický otisk certifikátu můžete aktualizovat konfigurační skript, a použít hodnotu:</span><span class="sxs-lookup"><span data-stu-id="400f6-203">With the certificate identified by its thumbprint, the configuration script can be updated to use the value:</span></span>

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

## <a name="running-the-configuration"></a><span data-ttu-id="400f6-204">Spuštění konfigurace</span><span class="sxs-lookup"><span data-stu-id="400f6-204">Running the configuration</span></span>

<span data-ttu-id="400f6-205">V tomto okamžiku můžete spustit konfigurace, který bude výstup dva soubory:</span><span class="sxs-lookup"><span data-stu-id="400f6-205">At this point, you can run the configuration, which will output two files:</span></span>

 * <span data-ttu-id="400f6-206">A *. meta.mof soubor, který konfiguruje správce místní konfigurace dešifrovat přihlašovací údaje pomocí certifikátu, který je uložen v úložišti místního počítače a identifikovaný jeho kryptografický otisk.</span><span class="sxs-lookup"><span data-stu-id="400f6-206">A *.meta.mof file that configures the Local Configuration Manager to decrypt the credentials using the certificate that is stored on the local machine store and identified by its thumbprint.</span></span> <span data-ttu-id="400f6-207">[`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/en-us/library/dn521621.aspx)se vztahuje *. meta.mof souboru.</span><span class="sxs-lookup"><span data-stu-id="400f6-207">[`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/en-us/library/dn521621.aspx) applies the *.meta.mof file.</span></span>
 * <span data-ttu-id="400f6-208">Soubor MOF, který ve skutečnosti aplikuje konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="400f6-208">A MOF file that actually applies the configuration.</span></span> <span data-ttu-id="400f6-209">Spuštění DscConfiguration aplikuje konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="400f6-209">Start-DscConfiguration applies the configuration.</span></span>

<span data-ttu-id="400f6-210">Tyto příkazy bude možné provést tyto kroky:</span><span class="sxs-lookup"><span data-stu-id="400f6-210">These commands will accomplish those steps:</span></span>

```powershell
Write-Host "Generate DSC Configuration..."
CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample

Write-Host "Setting up LCM to decrypt credentials..."
Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose 
 
Write-Host "Starting Configuration..."
Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose
```

<span data-ttu-id="400f6-211">V tomto příkladu by nabízená konfigurace DSC cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="400f6-211">This example would push the DSC configuration to the target node.</span></span>
<span data-ttu-id="400f6-212">Konfigurace DSC můžete použít také pomocí DSC pro vyžádání obsahu serveru, pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="400f6-212">The DSC configuration can also be applied using a DSC Pull Server if one is available.</span></span>

<span data-ttu-id="400f6-213">V tématu [nastavení klienta vyžádání DSC](pullClient.md) Další informace o použití konfigurace DSC pomocí serveru vyžádané replikace DSC.</span><span class="sxs-lookup"><span data-stu-id="400f6-213">See [Setting up a DSC pull client](pullClient.md) for more information on applying DSC configurations using a DSC Pull Server.</span></span>

## <a name="credential-encryption-module-example"></a><span data-ttu-id="400f6-214">Příklad modulu pro šifrování přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="400f6-214">Credential Encryption Module Example</span></span>

<span data-ttu-id="400f6-215">Tady je příklad úplné, která zahrnuje všechny tyto kroky, a dále pomocná rutina, která exportuje a zkopíruje veřejných klíčů:</span><span class="sxs-lookup"><span data-stu-id="400f6-215">Here is a full example that incorporates all of these steps, plus a helper cmdlet that exports and copies the public keys:</span></span>

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

