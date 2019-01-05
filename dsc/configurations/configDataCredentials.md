---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Možnosti přihlašovacích údajů v konfiguračních datech
ms.openlocfilehash: 10cf3456fcc7104b7dd779db30aebace54ba087a
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046637"
---
# <a name="credentials-options-in-configuration-data"></a><span data-ttu-id="1239a-103">Možnosti přihlašovacích údajů v konfiguračních datech</span><span class="sxs-lookup"><span data-stu-id="1239a-103">Credentials Options in Configuration Data</span></span>
><span data-ttu-id="1239a-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1239a-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="plain-text-passwords-and-domain-users"></a><span data-ttu-id="1239a-105">Hesla v prostém textu a uživatelé domény</span><span class="sxs-lookup"><span data-stu-id="1239a-105">Plain Text Passwords and Domain Users</span></span>

<span data-ttu-id="1239a-106">Konfigurace DSC obsahující přihlašovací údaje bez šifrování se vygeneruje chybovou zprávu o hesla v prostém textu.</span><span class="sxs-lookup"><span data-stu-id="1239a-106">DSC configurations containing a credential without encryption will generate an error message about plain text passwords.</span></span>
<span data-ttu-id="1239a-107">DSC, vygeneruje upozornění při použití přihlašovacích údajů do domény.</span><span class="sxs-lookup"><span data-stu-id="1239a-107">Also, DSC will generate a warning when using domain credentials.</span></span>
<span data-ttu-id="1239a-108">Můžete potlačit pomocí klíčových dat konfigurace DSC tyto chybové zprávy a upozornění:</span><span class="sxs-lookup"><span data-stu-id="1239a-108">To suppress these error and warning messages use the DSC configuration data keywords:</span></span>
* <span data-ttu-id="1239a-109">**PsDscAllowPlainTextPassword**</span><span class="sxs-lookup"><span data-stu-id="1239a-109">**PsDscAllowPlainTextPassword**</span></span>
* <span data-ttu-id="1239a-110">**PsDscAllowDomainUser**</span><span class="sxs-lookup"><span data-stu-id="1239a-110">**PsDscAllowDomainUser**</span></span>

> [!NOTE]
> <span data-ttu-id="1239a-111">Ukládání a přenos hesel ve formátu prostého textu nešifrované není obecně bezpečné.</span><span class="sxs-lookup"><span data-stu-id="1239a-111">Storing/transmitting plaintext passwords unencrypted is generally not secure.</span></span> <span data-ttu-id="1239a-112">Doporučuje se zabezpečení přihlašovacích údajů pomocí techniky popsané dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="1239a-112">Securing credentials by using the techniques covered later in this topic is recommended.</span></span>
> <span data-ttu-id="1239a-113">Služba Azure Automation DSC umožňuje centrálně spravovat přihlašovací údaje pro kompilaci v konfiguracích a bezpečně uložen.</span><span class="sxs-lookup"><span data-stu-id="1239a-113">The Azure Automation DSC service allows you to centrally manage credentials to be compiled in configurations and stored securely.</span></span>
> <span data-ttu-id="1239a-114">Informace najdete v tématu: [Kompilace konfigurací DSC / Assety přihlašovacích údajů](/azure/automation/automation-dsc-compile#credential-assets)</span><span class="sxs-lookup"><span data-stu-id="1239a-114">For information, see: [Compiling DSC Configurations / Credential Assets](/azure/automation/automation-dsc-compile#credential-assets)</span></span>

<span data-ttu-id="1239a-115">Následuje příklad předá přihlašovací údaje ve formátu prostého textu:</span><span class="sxs-lookup"><span data-stu-id="1239a-115">The following is an example of passing plain text credentials:</span></span>

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
        $password = $Node.LocalPassword | ConvertTo-SecureString -asPlainText -Force
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
            Credential = $promptedCreds
            GroupName = "Administrators"
            DependsOn = "[User]User2"
            Ensure = "Present"
            MembersToInclude = "User2"
        }
    }
}

# We declared the ConfigurationData in a local variable, but we need to pass it
# in to our configuration function
# We need to invoke the configuration function we created to generate a MOF
unencryptedPasswordDemo -ConfigurationData $ConfigurationData

# We need to pass the MOF to the machines we named.
#-wait: doesn't use jobs so we get blocked at the prompt until the configuration is done
#-verbose: so we can see what's going on and catch any errors
#-force: for testing purposes, I run start-dscconfiguration frequently + want to make sure i'm
#        not blocked by previous configurations that are still running
Start-DscConfiguration ./unencryptedPasswordDemo -verbose -wait -force
```

<span data-ttu-id="1239a-116">Toto je výňatek ze souboru ".mof" vygenerované konfigurace pro "TestMachine1".</span><span class="sxs-lookup"><span data-stu-id="1239a-116">This is an excerpt from the ".mof" file generated by the configuration for "TestMachine1".</span></span> <span data-ttu-id="1239a-117">`System.Security.SecureString` Používá v konfiguraci byl převeden na prostý text a uloženy v souboru "MOF" jako `MSF_Credential`.</span><span class="sxs-lookup"><span data-stu-id="1239a-117">The `System.Security.SecureString` used in the configuration was converted to plain text and stored in the ".mof" file as a `MSF_Credential`.</span></span> <span data-ttu-id="1239a-118">A `SecureString` je zašifrovaný pomocí aktuálního profilu uživatele.</span><span class="sxs-lookup"><span data-stu-id="1239a-118">A `SecureString` is encrypted with the current users profile.</span></span> <span data-ttu-id="1239a-119">Tento postup funguje dobře s všechny formy Vzdálená správa prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1239a-119">This works well with all forms of PowerShell remote management.</span></span> <span data-ttu-id="1239a-120">Soubor ".mof" byla navržena jako samotný konfigurační mechanizmus stojanu.</span><span class="sxs-lookup"><span data-stu-id="1239a-120">A ".mof" file is designed to be a stand alone configuration mechanism.</span></span> <span data-ttu-id="1239a-121">Od v Powershellu 5.0, jsou ".mof" soubory v uzlu šifrované v klidovém stavu, ale ne v cestě k uzlu.</span><span class="sxs-lookup"><span data-stu-id="1239a-121">Beginning in PowerShell 5.0, ".mof" files on a Node are encrypted at rest, but not in transit to the Node.</span></span> <span data-ttu-id="1239a-122">To znamená, že v souboru ".mof" hesel jako nešifrovaný text při použití na uzlu.</span><span class="sxs-lookup"><span data-stu-id="1239a-122">This means that passwords in a ".mof" file are exposed as clear text when you apply them to a Node.</span></span> <span data-ttu-id="1239a-123">K šifrování přihlašovacích údajů, budete muset použít **serveru vyžádané replikace**.</span><span class="sxs-lookup"><span data-stu-id="1239a-123">To encrypt credentials, you need to use a **Pull Server**.</span></span> <span data-ttu-id="1239a-124">Další informace najdete v tématu [soubory MOF zabezpečení pomocí certifikátů](../pull-server/secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="1239a-124">For more information, see [Securing MOF files with Certificates](../pull-server/secureMOF.md).</span></span>

```syntax
instance of MSFT_Credential as $MSFT_Credential1ref
{
Password = "ThisIsYetAnotherPlaintextPassword";
 UserName = "User2";

};

instance of MSFT_UserResource as $MSFT_UserResource1ref
{
ResourceID = "[User]User2";
 Description = "local account";
 UserName = "User2";
 Ensure = "Present";
 Password = $MSFT_Credential1ref;
 Disabled = False;
 SourceInfo = "::66::9::User";
 PasswordNeverExpires = True;
 ModuleName = "PsDesiredStateConfiguration";
 PasswordChangeRequired = False;

ModuleVersion = "1.0";

 ConfigurationName = "unencryptedPasswordDemo";

};
```

## <a name="handling-credentials-in-dsc"></a><span data-ttu-id="1239a-125">Zpracování přihlašovacích údajů v DSC</span><span class="sxs-lookup"><span data-stu-id="1239a-125">Handling Credentials in DSC</span></span>

<span data-ttu-id="1239a-126">Prostředky DSC konfigurace spustit jako `Local System` ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="1239a-126">DSC configuration resources run as `Local System` by default.</span></span>
<span data-ttu-id="1239a-127">Ale některé prostředky nutné přihlašovací údaje, například při `Package` prostředků je potřeba nainstalovat software v rámci konkrétního uživatelského účtu.</span><span class="sxs-lookup"><span data-stu-id="1239a-127">However, some resources need a credential, for example when the `Package` resource needs to install software under a specific user account.</span></span>

<span data-ttu-id="1239a-128">Použít starší prostředky pevně zakódovaná `Credential` název vlastnosti pro toto zpracování.</span><span class="sxs-lookup"><span data-stu-id="1239a-128">Earlier resources used a hard-coded `Credential` property name to handle this.</span></span>
<span data-ttu-id="1239a-129">Automatické přidání WMF 5.0 `PsDscRunAsCredential` vlastnost pro všechny prostředky.</span><span class="sxs-lookup"><span data-stu-id="1239a-129">WMF 5.0 added an automatic `PsDscRunAsCredential` property for all resources.</span></span>
<span data-ttu-id="1239a-130">Informace o používání `PsDscRunAsCredential`, naleznete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="1239a-130">For information about using `PsDscRunAsCredential`, see [Running DSC with user credentials](runAsUser.md).</span></span>
<span data-ttu-id="1239a-131">Novější a vlastních prostředků pomocí této vlastnosti automatické místo vytvoření vlastní vlastnost pro přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="1239a-131">Newer resources and custom resources can use this automatic property instead of creating their own property for credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="1239a-132">Návrh některých prostředků mají používat více přihlašovací údaje pro konkrétní důvod, proč a mají své vlastní vlastnosti přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="1239a-132">The design of some resources are to use multiple credentials for a specific reason, and they will have their own credential properties.</span></span>

<span data-ttu-id="1239a-133">Pokud chcete zjistit přihlašovací údaje, které k dispozici vlastnosti prostředku, použijte buď `Get-DscResource -Name ResourceName -Syntax` nebo technologie Intellisense v prostředí ISE (`CTRL+SPACE`).</span><span class="sxs-lookup"><span data-stu-id="1239a-133">To find the available credential properties on a resource use either `Get-DscResource -Name ResourceName -Syntax` or the Intellisense in the ISE (`CTRL+SPACE`).</span></span>

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

<span data-ttu-id="1239a-134">Tento příklad používá [skupiny](../resources/resources.md) prostředku z `PSDesiredStateConfiguration` integrovaný modul prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="1239a-134">This example uses a [Group](../resources/resources.md) resource from the `PSDesiredStateConfiguration` built-in DSC resource module.</span></span>
<span data-ttu-id="1239a-135">Můžete vytvořit místní skupiny a přidat nebo odebrat členy.</span><span class="sxs-lookup"><span data-stu-id="1239a-135">It can create local groups and add or remove members.</span></span>
<span data-ttu-id="1239a-136">Přijímá i `Credential` vlastnost a automatické `PsDscRunAsCredential` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="1239a-136">It accepts both the `Credential` property and the automatic `PsDscRunAsCredential` property.</span></span>
<span data-ttu-id="1239a-137">Nicméně pouze prostředek používá `Credential` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="1239a-137">However, the resource only uses the `Credential` property.</span></span>

<span data-ttu-id="1239a-138">Další informace o `PsDscRunAsCredential` vlastnost, naleznete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="1239a-138">For more information about the `PsDscRunAsCredential` property, see [Running DSC with user credentials](runAsUser.md).</span></span>

## <a name="example-the-group-resource-credential-property"></a><span data-ttu-id="1239a-139">Příklad: Skupina prostředků vlastnost Credential</span><span class="sxs-lookup"><span data-stu-id="1239a-139">Example: The Group resource Credential property</span></span>

<span data-ttu-id="1239a-140">DSC běží pod `Local System`, takže už má oprávnění ke změně místní uživatelé a skupiny.</span><span class="sxs-lookup"><span data-stu-id="1239a-140">DSC runs under `Local System`, so it already has permissions to change local users and groups.</span></span>
<span data-ttu-id="1239a-141">Pokud Přidání člena je místní účet, nevyžadují se přihlašovací údaje je nezbytné.</span><span class="sxs-lookup"><span data-stu-id="1239a-141">If the member added is a local account, then no credential is necessary.</span></span>
<span data-ttu-id="1239a-142">Pokud `Group` zdroj přidá doménový účet do místní skupiny a pak je nutné přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="1239a-142">If the `Group` resource adds a domain account to the local group, then a credential is necessary.</span></span>

<span data-ttu-id="1239a-143">Anonymní dotazy do služby Active Directory nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="1239a-143">Anonymous queries to Active Directory are not allowed.</span></span>
<span data-ttu-id="1239a-144">`Credential` Vlastnost `Group` prostředků je účet domény používaný k dotazu služby Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1239a-144">The `Credential` property of the `Group` resource is the domain account used to query Active Directory.</span></span>
<span data-ttu-id="1239a-145">Pro většinu účelů příčinou může být obecný uživatelský účet ve výchozím nastavení můžou uživatelé *čtení* většinu objektů ve službě Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1239a-145">For most purposes this could be a generic user account, because by default users can *read* most of the objects in Active Directory.</span></span>

## <a name="example-configuration"></a><span data-ttu-id="1239a-146">Příklad konfigurace</span><span class="sxs-lookup"><span data-stu-id="1239a-146">Example Configuration</span></span>

<span data-ttu-id="1239a-147">Následující příklad kódu používá DSC k naplnění místní skupinu jako uživatel domény:</span><span class="sxs-lookup"><span data-stu-id="1239a-147">The following example code uses DSC to populate a local group with a domain user:</span></span>

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

<span data-ttu-id="1239a-148">Tento kód vygeneruje chyby i upozornění:</span><span class="sxs-lookup"><span data-stu-id="1239a-148">This code generates both an error and warning message:</span></span>

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

<span data-ttu-id="1239a-149">V tomto příkladu má dva problémy:</span><span class="sxs-lookup"><span data-stu-id="1239a-149">This example has two issues:</span></span>
1. <span data-ttu-id="1239a-150">Chyba vysvětluje, že nedoporučujeme používat hesla v prostém textu</span><span class="sxs-lookup"><span data-stu-id="1239a-150">An error explains that plain text passwords are not recommended</span></span>
2. <span data-ttu-id="1239a-151">Upozornění se nedoporučuje používat přihlašovací údaje domény</span><span class="sxs-lookup"><span data-stu-id="1239a-151">A warning advises against using a domain credential</span></span>

## <a name="psdscallowplaintextpassword"></a><span data-ttu-id="1239a-152">PsDscAllowPlainTextPassword</span><span class="sxs-lookup"><span data-stu-id="1239a-152">PsDscAllowPlainTextPassword</span></span>

<span data-ttu-id="1239a-153">První chybovou zprávu má adresu URL s dokumentací.</span><span class="sxs-lookup"><span data-stu-id="1239a-153">The first error message has a URL with documentation.</span></span>
<span data-ttu-id="1239a-154">Tento odkaz vysvětluje, jak šifrovat pomocí hesla [ConfigurationData](./configData.md) strukturu a certifikát.</span><span class="sxs-lookup"><span data-stu-id="1239a-154">This link explains how to encrypt passwords using a [ConfigurationData](./configData.md) structure and a certificate.</span></span>
<span data-ttu-id="1239a-155">Další informace o certifikátech a DSC [přečtěte si tento příspěvek](http://aka.ms/certs4dsc).</span><span class="sxs-lookup"><span data-stu-id="1239a-155">For more information on certificates and DSC [read this post](http://aka.ms/certs4dsc).</span></span>

<span data-ttu-id="1239a-156">Vynutit heslo jako prostý text, prostředek, vyžaduje `PsDscAllowPlainTextPassword` – klíčové slovo v konfiguračních datech části následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="1239a-156">To force a plain text password, the resource requires the `PsDscAllowPlainTextPassword` keyword in the configuration data section as follows:</span></span>

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
> <span data-ttu-id="1239a-157">`NodeName` se nesmí rovnat hvězdičky, konkrétní uzel název je povinné.</span><span class="sxs-lookup"><span data-stu-id="1239a-157">`NodeName` cannot equal asterisk, a specific node name is mandatory.</span></span>

<span data-ttu-id="1239a-158">**Microsoft se výzva, aby hesla v prostém textu kvůli významné riziko zabezpečení.**</span><span class="sxs-lookup"><span data-stu-id="1239a-158">**Microsoft advises to avoid plain text passwords due to the significant security risk.**</span></span>

## <a name="domain-credentials"></a><span data-ttu-id="1239a-159">Přihlašovací údaje domény</span><span class="sxs-lookup"><span data-stu-id="1239a-159">Domain Credentials</span></span>

<span data-ttu-id="1239a-160">Spuštění skriptu konfigurace příklad znovu (s nebo bez šifrování), stále generuje upozornění, že používáte doménu účtu zadání přihlašovacích údajů se nedoporučuje.</span><span class="sxs-lookup"><span data-stu-id="1239a-160">Running the example configuration script again (with or without encryption), still generates the warning that using a domain account for a credential is not recommended.</span></span>
<span data-ttu-id="1239a-161">Pomocí místního účtu eliminuje potenciální riziko pověření domény, které lze použít na jiných serverech.</span><span class="sxs-lookup"><span data-stu-id="1239a-161">Using a local account eliminates potential exposure of domain credentials that could be used on other servers.</span></span>

<span data-ttu-id="1239a-162">**Při použití přihlašovacích údajů pomocí prostředků DSC, dáváte přednost místní účet kontrolu nad účtem domény, pokud je to možné.**</span><span class="sxs-lookup"><span data-stu-id="1239a-162">**When using credentials with DSC resources, prefer a local account over a domain account when possible.**</span></span>

<span data-ttu-id="1239a-163">Pokud je '\' nebo '\@' v `Username` vlastnosti přihlašovacích údajů, pak DSC bude zpracována jako účet domény.</span><span class="sxs-lookup"><span data-stu-id="1239a-163">If there is a '\' or '@' in the `Username` property of the credential, then DSC will treat it as a domain account.</span></span>
<span data-ttu-id="1239a-164">Dojde k výjimce pro "localhost", "127.0.0.1" a ":: 1" v části domény uživatelské jméno.</span><span class="sxs-lookup"><span data-stu-id="1239a-164">There is an exception for "localhost", "127.0.0.1", and "::1" in the domain portion of the user name.</span></span>

## <a name="psdscallowdomainuser"></a><span data-ttu-id="1239a-165">PSDscAllowDomainUser</span><span class="sxs-lookup"><span data-stu-id="1239a-165">PSDscAllowDomainUser</span></span>

<span data-ttu-id="1239a-166">V DSC `Group` prostředků příklad výše, dotazování domény služby Active Directory *vyžaduje* účet domény.</span><span class="sxs-lookup"><span data-stu-id="1239a-166">In the DSC `Group` resource example above, querying an Active Directory domain *requires* a domain account.</span></span>
<span data-ttu-id="1239a-167">V takovém případě přidejte `PSDscAllowDomainUser` vlastnost `ConfigurationData` blokovat následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="1239a-167">In this case add the `PSDscAllowDomainUser` property to the `ConfigurationData` block as follows:</span></span>

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

<span data-ttu-id="1239a-168">Konfigurační skript nyní vygeneruje soubor MOF bez jakýchkoli chyb nebo upozornění.</span><span class="sxs-lookup"><span data-stu-id="1239a-168">Now the configuration script will generate the MOF file with no errors or warnings.</span></span>
