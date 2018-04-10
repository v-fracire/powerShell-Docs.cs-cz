---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Možnosti přihlašovací údaje v konfiguračních dat
ms.openlocfilehash: 3f1c75c65b357220856dd8e50694eb77808dee41
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="credentials-options-in-configuration-data"></a><span data-ttu-id="d0f2a-103">Možnosti přihlašovací údaje v konfiguračních dat</span><span class="sxs-lookup"><span data-stu-id="d0f2a-103">Credentials Options in Configuration Data</span></span>
><span data-ttu-id="d0f2a-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="d0f2a-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="plain-text-passwords-and-domain-users"></a><span data-ttu-id="d0f2a-105">Hesla ve formátu prostého textu a uživatelé domény</span><span class="sxs-lookup"><span data-stu-id="d0f2a-105">Plain Text Passwords and Domain Users</span></span>

<span data-ttu-id="d0f2a-106">Konfigurace DSC obsahující pověření bez šifrování vygeneruje chybovou zprávu o hesla v prostém textu.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-106">DSC configurations containing a credential without encryption will generate an error message about plain text passwords.</span></span>
<span data-ttu-id="d0f2a-107">Navíc DSC vygeneruje upozornění při použití přihlašovacích údajů do domény.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-107">Also, DSC will generate a warning when using domain credentials.</span></span>
<span data-ttu-id="d0f2a-108">Chcete-li potlačit tyto chybové zprávy a upozornění používat klíčová slova, DSC konfigurační data:</span><span class="sxs-lookup"><span data-stu-id="d0f2a-108">To suppress these error and warning messages use the DSC configuration data keywords:</span></span>
* <span data-ttu-id="d0f2a-109">**PsDscAllowPlainTextPassword**</span><span class="sxs-lookup"><span data-stu-id="d0f2a-109">**PsDscAllowPlainTextPassword**</span></span>
* <span data-ttu-id="d0f2a-110">**PsDscAllowDomainUser**</span><span class="sxs-lookup"><span data-stu-id="d0f2a-110">**PsDscAllowDomainUser**</span></span>

> [!NOTE]
> <span data-ttu-id="d0f2a-111">Ukládání nebo přenos hesel ve formátu prostého textu bez šifrování není zabezpečený.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-111">Storing/transmitting plaintext passwords unencrypted is generally not secure.</span></span> <span data-ttu-id="d0f2a-112">Doporučuje se zabezpečení přihlašovacích údajů pomocí techniky popsané dál v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-112">Securing credentials by using the techniques covered later in this topic is recommended.</span></span>
> <span data-ttu-id="d0f2a-113">Služba Azure Automation DSC umožňuje centrálně spravovat pověření k kompilovat v konfiguracích a bezpečně uložit.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-113">The Azure Automation DSC service allows you to centrally manage credentials to be compiled in configurations and stored securely.</span></span>
> <span data-ttu-id="d0f2a-114">Informace najdete v tématu: [kompilaci konfigurace DSC / prostředků přihlašovacích údajů](/azure/automation/automation-dsc-compile#credential-assets)</span><span class="sxs-lookup"><span data-stu-id="d0f2a-114">For information, see: [Compiling DSC Configurations / Credential Assets](/azure/automation/automation-dsc-compile#credential-assets)</span></span>

<span data-ttu-id="d0f2a-115">Následuje příklad předávání přihlašovací údaje ve formátu prostého textu:</span><span class="sxs-lookup"><span data-stu-id="d0f2a-115">The following is an example of passing plain text credentials:</span></span>

```powershell
#Prompt user for their credentials
#credentials will be unencrypted in the MOF
$promptedCreds = get-credential -Message "Please enter your credentials to generate a DSC MOF:"

# Store passwords in plaintext, in the document itself
# will also be stored in plaintext in the mof
$password = "ThisIsAPlaintextPassword" | ConvertTo-SecureString -asPlainText -Force
$username = "User1"
[PSCredential] $credential = New-Object System.Management.Automation.PSCredential($username,$password)

# DSC requires explicit confirmation before storing passwords insecurely
$ConfigurationData = @{
    AllNodes = @(
        @{
            # The "*" means "all nodes named in ConfigData" so we don't have to repeat ourselves
            NodeName="*"
            PSDscAllowPlainTextPassword = $true
        },
        #however, each node still needs to be explicitly defined for "*" to have meaning
        @{
            NodeName = "TestMachine1"
        },
        #we can also use a property to define node-specific passwords, although this is no more secure
        @{
            NodeName = "TestMachine2";
            UserName = "User2"
            LocalPassword = "ThisIsYetAnotherPlaintextPassword"
        }
        )
}
configuration unencryptedPasswordDemo
{
    Node "TestMachine1"
    {
        # We use the plaintext password to generate a new account
        User User1
        {
            UserName = $username
            Password = $credential
            Description = "local account"
            Ensure = "Present"
            Disabled = $false
            PasswordNeverExpires = $true
            PasswordChangeRequired = $false
        }
        # We use the prompted password to add this account to the local admins group
        Group addToAdmin
        {
            # Ensure the user exists before we add the user to a group
            DependsOn = "[User]User1"
            Credential = $promptedCreds
            GroupName = "Administrators"
            Ensure = "Present"
            MembersToInclude = "User1"
        }
    }

    Node "TestMachine2"
    {
        # Now we'll use a node-specific password to this machine
        $password = $Node.LocalPass | ConvertTo-SecureString -asPlainText -Force
        $username = $node.UserName
        [PSCredential] $nodeCred = New-Object System.Management.Automation.PSCredential($username,$password)

        User User2
        {
            UserName = $username
            Password = $nodeCred
            Description = "local account"
            Ensure = "Present"
            Disabled = $false
            PasswordNeverExpires = $true
            PasswordChangeRequired = $false
        }

        Group addToAdmin
        {
            Credential = $domain
            GroupName = "Administrators"
            DependsOn = "[User]User2"
            Ensure = "Present"
            MembersToInclude = "User2"
        }
    }

}
# We declared the ConfigurationData in a local variable, but we need to pass it in to our configuration function
# We need to invoke the configuration function we created to generate a MOF
unencryptedPasswordDemo -ConfigurationData $ConfigurationData
# We need to pass the MOF to the machines we named.
#-wait: doesn't use jobs so we get blocked at the prompt until the configuration is done
#-verbose: so we can see what's going on and catch any errors
#-force: for testing purposes, I run start-dscconfiguration frequently + want to make sure i'm
#        not blocked by previous configurations that are still running
Start-DscConfiguration ./unencryptedPasswordDemo -verbose -wait -force
```

## <a name="handling-credentials-in-dsc"></a><span data-ttu-id="d0f2a-116">Zpracování pověření v DSC</span><span class="sxs-lookup"><span data-stu-id="d0f2a-116">Handling Credentials in DSC</span></span>

<span data-ttu-id="d0f2a-117">Prostředky konfigurace DSC spustit jako `Local System` ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-117">DSC configuration resources run as `Local System` by default.</span></span>
<span data-ttu-id="d0f2a-118">Ale některé prostředky je nutné pověření, například když `Package` prostředků je potřeba nainstalovat software v části konkrétní uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-118">However, some resources need a credential, for example when the `Package` resource needs to install software under a specific user account.</span></span>

<span data-ttu-id="d0f2a-119">Starší prostředky používá pevně zakódovaným `Credential` název vlastnosti pro toto zpracování.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-119">Earlier resources used a hard-coded `Credential` property name to handle this.</span></span>
<span data-ttu-id="d0f2a-120">WMF 5.0 přidat automatické `PsDscRunAsCredential` vlastnost pro všechny prostředky.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-120">WMF 5.0 added an automatic `PsDscRunAsCredential` property for all resources.</span></span>
<span data-ttu-id="d0f2a-121">Informace o používání `PsDscRunAsCredential`, najdete v části [DSC spuštěná s pověřeními uživatele](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="d0f2a-121">For information about using `PsDscRunAsCredential`, see [Running DSC with user credentials](runAsUser.md).</span></span>
<span data-ttu-id="d0f2a-122">Novější a vlastních prostředků pomocí této vlastnosti automatické místo vytvoření vlastní vlastnost pro přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-122">Newer resources and custom resources can use this automatic property instead of creating their own property for credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="d0f2a-123">Návrh některé prostředky se mají používat více přihlašovací údaje pro konkrétní důvod, proč a budou mít vlastní vlastnosti přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-123">The design of some resources are to use multiple credentials for a specific reason, and they will have their own credential properties.</span></span>

<span data-ttu-id="d0f2a-124">K vyhledání dostupných přihlašovacích údajů vlastnosti prostředku, použijte buď `Get-DscResource -Name ResourceName -Syntax` nebo Intellisense (ISE) v (`CTRL+SPACE`).</span><span class="sxs-lookup"><span data-stu-id="d0f2a-124">To find the available credential properties on a resource use either `Get-DscResource -Name ResourceName -Syntax` or the Intellisense in the ISE (`CTRL+SPACE`).</span></span>

```powershell
PS C:\> Get-DscResource -Name Group -Syntax
Group [String] #ResourceName
{
    GroupName = [string]
    [Credential = [PSCredential]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Members = [string[]]]
    [MembersToExclude = [string[]]]
    [MembersToInclude = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
}
```

<span data-ttu-id="d0f2a-125">Tento příklad používá [skupiny](https://msdn.microsoft.com/powershell/dsc/groupresource) prostředek z `PSDesiredStateConfiguration` integrovaného modulu prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-125">This example uses a [Group](https://msdn.microsoft.com/powershell/dsc/groupresource) resource from the `PSDesiredStateConfiguration` built-in DSC resource module.</span></span>
<span data-ttu-id="d0f2a-126">Můžete vytvořit místní skupiny a přidat nebo odebrat členy.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-126">It can create local groups and add or remove members.</span></span>
<span data-ttu-id="d0f2a-127">Přijímá i `Credential` vlastnost a automatického `PsDscRunAsCredential` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-127">It accepts both the `Credential` property and the automatic `PsDscRunAsCredential` property.</span></span>
<span data-ttu-id="d0f2a-128">Ale prostředek používá jenom `Credential` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-128">However, the resource only uses the `Credential` property.</span></span>

<span data-ttu-id="d0f2a-129">Další informace o `PsDscRunAsCredential` vlastnost, najdete v části [DSC spuštěná s pověřeními uživatele](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="d0f2a-129">For more information about the `PsDscRunAsCredential` property, see [Running DSC with user credentials](runAsUser.md).</span></span>

## <a name="example-the-group-resource-credential-property"></a><span data-ttu-id="d0f2a-130">Příklad: Skupina prostředků vlastnost pověření</span><span class="sxs-lookup"><span data-stu-id="d0f2a-130">Example: The Group resource Credential property</span></span>

<span data-ttu-id="d0f2a-131">DSC běží pod `Local System`, takže už má oprávnění ke změně místní uživatelé a skupiny.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-131">DSC runs under `Local System`, so it already has permissions to change local users and groups.</span></span>
<span data-ttu-id="d0f2a-132">Pokud je člen přidat místní účet, se žádné přihlašovací údaje nezbytné.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-132">If the member added is a local account, then no credential is necessary.</span></span>
<span data-ttu-id="d0f2a-133">Pokud `Group` prostředků přidá doménový účet do místní skupiny a pak je nutné pověření.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-133">If the `Group` resource adds a domain account to the local group, then a credential is necessary.</span></span>

<span data-ttu-id="d0f2a-134">Anonymní dotazy do služby Active Directory nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-134">Anonymous queries to Active Directory are not allowed.</span></span>
<span data-ttu-id="d0f2a-135">`Credential` Vlastnost `Group` prostředek je doménový účet použít k dotazu služby Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-135">The `Credential` property of the `Group` resource is the domain account used to query Active Directory.</span></span>
<span data-ttu-id="d0f2a-136">Pro většinu účelů to může být obecné uživatelský účet, ve výchozím nastavení mohou uživatelé *číst* většinu objektů ve službě Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-136">For most purposes this could be a generic user account, because by default users can *read* most of the objects in Active Directory.</span></span>

## <a name="example-configuration"></a><span data-ttu-id="d0f2a-137">Příklad konfigurace</span><span class="sxs-lookup"><span data-stu-id="d0f2a-137">Example Configuration</span></span>

<span data-ttu-id="d0f2a-138">Následující příklad kódu používá DSC k naplnění místní skupiny s uživatelem domény:</span><span class="sxs-lookup"><span data-stu-id="d0f2a-138">The following example code uses DSC to populate a local group with a domain user:</span></span>

```powershell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred
```

<span data-ttu-id="d0f2a-139">Tento kód se generuje k chybě a upozornění:</span><span class="sxs-lookup"><span data-stu-id="d0f2a-139">This code generates both an error and warning message:</span></span>

```
ConvertTo-MOFInstance : System.InvalidOperationException error processing
property 'Credential' OF TYPE 'Group': Converting and storing encrypted
passwords as plain text is not recommended. For more information on securing
credentials in MOF file, please refer to MSDN blog:
http://go.microsoft.com/fwlink/?LinkId=393729

At line:11 char:9
+   Group
At line:297 char:16
+     $aliasId = ConvertTo-MOFInstance $keywordName $canonicalizedValue
+                ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessProperty,ConvertTo-MOFInstance

WARNING: It is not recommended to use domain credential for node 'localhost'.
In order to suppress the warning, you can add a property named
'PSDscAllowDomainUser' with a value of $true to your DSC configuration data
for node 'localhost'.
```

<span data-ttu-id="d0f2a-140">V tomto příkladu má dva problémy:</span><span class="sxs-lookup"><span data-stu-id="d0f2a-140">This example has two issues:</span></span>
1. <span data-ttu-id="d0f2a-141">Chybu vysvětluje, že se nedoporučují hesla v prostém textu</span><span class="sxs-lookup"><span data-stu-id="d0f2a-141">An error explains that plain text passwords are not recommended</span></span>
2. <span data-ttu-id="d0f2a-142">Upozornění informuje o tom proti pomocí pověření domény</span><span class="sxs-lookup"><span data-stu-id="d0f2a-142">A warning advises against using a domain credential</span></span>

## <a name="psdscallowplaintextpassword"></a><span data-ttu-id="d0f2a-143">PsDscAllowPlainTextPassword</span><span class="sxs-lookup"><span data-stu-id="d0f2a-143">PsDscAllowPlainTextPassword</span></span>

<span data-ttu-id="d0f2a-144">První chybovou zprávu s adresou URL naleznete v dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-144">The first error message has a URL with documentation.</span></span>
<span data-ttu-id="d0f2a-145">Tento odkaz vysvětluje, jak šifrovat pomocí hesla [ConfigurationData](https://msdn.microsoft.com/powershell/dsc/configdata) struktura a certifikát.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-145">This link explains how to encrypt passwords using a [ConfigurationData](https://msdn.microsoft.com/powershell/dsc/configdata) structure and a certificate.</span></span>
<span data-ttu-id="d0f2a-146">Další informace o certifikátech a DSC [si tento příspěvek](http://aka.ms/certs4dsc).</span><span class="sxs-lookup"><span data-stu-id="d0f2a-146">For more information on certificates and DSC [read this post](http://aka.ms/certs4dsc).</span></span>

<span data-ttu-id="d0f2a-147">Chcete-li vynutit hesla v podobě prostého textu, prostředku vyžaduje `PsDscAllowPlainTextPassword` – klíčové slovo v konfigurační data části následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="d0f2a-147">To force a plain text password, the resource requires the `PsDscAllowPlainTextPassword` keyword in the configuration data section as follows:</span></span>

```powershell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowPlainTextPassword = $true
        }
    )
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred -ConfigurationData $cd
```

> [!NOTE]
> <span data-ttu-id="d0f2a-148">`NodeName` se nesmí rovnat hvězdičky, konkrétním uzlu jméno je povinné.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-148">`NodeName` cannot equal asterisk, a specific node name is mandatory.</span></span>

<span data-ttu-id="d0f2a-149">**Microsoft informuje o tom, aby se zabránilo hesla v prostém textu z důvodu významné bezpečnostní riziko.**</span><span class="sxs-lookup"><span data-stu-id="d0f2a-149">**Microsoft advises to avoid plain text passwords due to the significant security risk.**</span></span>

<span data-ttu-id="d0f2a-150">Výjimku by při použití služby Azure Automation DSC, protože data se vždy ukládají zašifrovaně (na cestě, umístěná ve službě a v klidovém stavu uložených v uzlu).</span><span class="sxs-lookup"><span data-stu-id="d0f2a-150">An exception would be when using the Azure Automation DSC service, only because the data is always stored encrypted (in transit, at rest in the service, and at rest on the node).</span></span>

## <a name="domain-credentials"></a><span data-ttu-id="d0f2a-151">Domain Credentials</span><span class="sxs-lookup"><span data-stu-id="d0f2a-151">Domain Credentials</span></span>

<span data-ttu-id="d0f2a-152">Spuštění skriptu konfigurace příklad opakujte (s nebo bez šifrování), stále generuje upozornění, že používáte doménu účtu pro přihlašovací údaje se nedoporučuje.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-152">Running the example configuration script again (with or without encryption), still generates the warning that using a domain account for a credential is not recommended.</span></span>
<span data-ttu-id="d0f2a-153">Pomocí místního účtu eliminuje potenciální ohrožení pověření domény, které by mohly být použity na jiných serverech.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-153">Using a local account eliminates potential exposure of domain credentials that could be used on other servers.</span></span>

<span data-ttu-id="d0f2a-154">**Pokud používáte přihlašovací údaje s prostředky DSC, raději místní účet přes účet domény, pokud je to možné.**</span><span class="sxs-lookup"><span data-stu-id="d0f2a-154">**When using credentials with DSC resources, prefer a local account over a domain account when possible.**</span></span>

<span data-ttu-id="d0f2a-155">Pokud je '\' nebo '\@' v `Username` vlastnosti přihlašovacích údajů, pak DSC bude zpracována jako účet domény.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-155">If there is a '\' or '@' in the `Username` property of the credential, then DSC will treat it as a domain account.</span></span>
<span data-ttu-id="d0f2a-156">Dojde k výjimce pro "localhost", "127.0.0.1" a ":: 1" v části domény uživatelského jména.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-156">There is an exception for "localhost", "127.0.0.1", and "::1" in the domain portion of the user name.</span></span>

## <a name="psdscallowdomainuser"></a><span data-ttu-id="d0f2a-157">PSDscAllowDomainUser</span><span class="sxs-lookup"><span data-stu-id="d0f2a-157">PSDscAllowDomainUser</span></span>

<span data-ttu-id="d0f2a-158">V DSC `Group` prostředků příkladu výše, dotazování domény služby Active Directory *vyžaduje* účet domény.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-158">In the DSC `Group` resource example above, querying an Active Directory domain *requires* a domain account.</span></span>
<span data-ttu-id="d0f2a-159">V takovém případě přidejte `PSDscAllowDomainUser` vlastnost, která má `ConfigurationData` blokovat následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="d0f2a-159">In this case add the `PSDscAllowDomainUser` property to the `ConfigurationData` block as follows:</span></span>

```powershell
$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowDomainUser = $true
            # PSDscAllowPlainTextPassword = $true
            CertificateFile = "C:\PublicKeys\server1.cer"
        }
    )
}
```

<span data-ttu-id="d0f2a-160">Nyní konfigurační skript vygeneruje soubor MOF se žádné chyby nebo upozornění.</span><span class="sxs-lookup"><span data-stu-id="d0f2a-160">Now the configuration script will generate the MOF file with no errors or warnings.</span></span>