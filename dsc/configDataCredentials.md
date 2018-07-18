---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Možnosti přihlašovacích údajů v konfiguračních datech
ms.openlocfilehash: 12bb8d8ce5fc4685e583e74d411b098320ac4fd4
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093673"
---
# <a name="credentials-options-in-configuration-data"></a>Možnosti přihlašovacích údajů v konfiguračních datech
>Platí pro: Windows PowerShell 5.0

## <a name="plain-text-passwords-and-domain-users"></a>Hesla v prostém textu a uživatelé domény

Konfigurace DSC obsahující přihlašovací údaje bez šifrování se vygeneruje chybovou zprávu o hesla v prostém textu.
DSC, vygeneruje upozornění při použití přihlašovacích údajů do domény.
Můžete potlačit pomocí klíčových dat konfigurace DSC tyto chybové zprávy a upozornění:
* **PsDscAllowPlainTextPassword**
* **PsDscAllowDomainUser**

> [!NOTE]
> Ukládání a přenos hesel ve formátu prostého textu nešifrované není obecně bezpečné. Doporučuje se zabezpečení přihlašovacích údajů pomocí techniky popsané dále v tomto tématu.
> Služba Azure Automation DSC umožňuje centrálně spravovat přihlašovací údaje pro kompilaci v konfiguracích a bezpečně uložen.
> Informace najdete v tématu: [kompilaci konfigurace DSC / Assety přihlašovacích údajů](/azure/automation/automation-dsc-compile#credential-assets)

Následuje příklad předá přihlašovací údaje ve formátu prostého textu:

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

## <a name="handling-credentials-in-dsc"></a>Zpracování přihlašovacích údajů v DSC

Prostředky DSC konfigurace spustit jako `Local System` ve výchozím nastavení.
Ale některé prostředky nutné přihlašovací údaje, například při `Package` prostředků je potřeba nainstalovat software v rámci konkrétního uživatelského účtu.

Použít starší prostředky pevně zakódovaná `Credential` název vlastnosti pro toto zpracování.
Automatické přidání WMF 5.0 `PsDscRunAsCredential` vlastnost pro všechny prostředky.
Informace o používání `PsDscRunAsCredential`, naleznete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).
Novější a vlastních prostředků pomocí této vlastnosti automatické místo vytvoření vlastní vlastnost pro přihlašovací údaje.

> [!NOTE]
> Návrh některých prostředků mají používat více přihlašovací údaje pro konkrétní důvod, proč a mají své vlastní vlastnosti přihlašovacích údajů.

Pokud chcete zjistit přihlašovací údaje, které k dispozici vlastnosti prostředku, použijte buď `Get-DscResource -Name ResourceName -Syntax` nebo technologie Intellisense v prostředí ISE (`CTRL+SPACE`).

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

Tento příklad používá [skupiny](https://msdn.microsoft.com/powershell/dsc/groupresource) prostředku z `PSDesiredStateConfiguration` integrovaný modul prostředků DSC.
Můžete vytvořit místní skupiny a přidat nebo odebrat členy.
Přijímá i `Credential` vlastnost a automatické `PsDscRunAsCredential` vlastnost.
Nicméně pouze prostředek používá `Credential` vlastnost.

Další informace o `PsDscRunAsCredential` vlastnost, naleznete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).

## <a name="example-the-group-resource-credential-property"></a>Příklad: Skupina prostředků vlastnost Credential

DSC běží pod `Local System`, takže už má oprávnění ke změně místní uživatelé a skupiny.
Pokud Přidání člena je místní účet, nevyžadují se přihlašovací údaje je nezbytné.
Pokud `Group` zdroj přidá doménový účet do místní skupiny a pak je nutné přihlašovací údaje.

Anonymní dotazy do služby Active Directory nejsou povoleny.
`Credential` Vlastnost `Group` prostředků je účet domény používaný k dotazu služby Active Directory.
Pro většinu účelů příčinou může být obecný uživatelský účet ve výchozím nastavení můžou uživatelé *čtení* většinu objektů ve službě Active Directory.

## <a name="example-configuration"></a>Příklad konfigurace

Následující příklad kódu používá DSC k naplnění místní skupinu jako uživatel domény:

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

Tento kód vygeneruje chyby i upozornění:

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

V tomto příkladu má dva problémy:
1. Chyba vysvětluje, že nedoporučujeme používat hesla v prostém textu
2. Upozornění se nedoporučuje používat přihlašovací údaje domény

## <a name="psdscallowplaintextpassword"></a>PsDscAllowPlainTextPassword

První chybovou zprávu má adresu URL s dokumentací.
Tento odkaz vysvětluje, jak šifrovat pomocí hesla [ConfigurationData](https://msdn.microsoft.com/powershell/dsc/configdata) strukturu a certifikát.
Další informace o certifikátech a DSC [přečtěte si tento příspěvek](http://aka.ms/certs4dsc).

Vynutit heslo jako prostý text, prostředek, vyžaduje `PsDscAllowPlainTextPassword` – klíčové slovo v konfiguračních datech části následujícím způsobem:

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
> `NodeName` se nesmí rovnat hvězdičky, konkrétní uzel název je povinné.

**Microsoft se výzva, aby hesla v prostém textu kvůli významné riziko zabezpečení.**

## <a name="domain-credentials"></a>Přihlašovací údaje domény

Spuštění skriptu konfigurace příklad znovu (s nebo bez šifrování), stále generuje upozornění, že používáte doménu účtu zadání přihlašovacích údajů se nedoporučuje.
Pomocí místního účtu eliminuje potenciální riziko pověření domény, které lze použít na jiných serverech.

**Při použití přihlašovacích údajů pomocí prostředků DSC, dáváte přednost místní účet kontrolu nad účtem domény, pokud je to možné.**

Pokud je '\' nebo '\@' v `Username` vlastnosti přihlašovacích údajů, pak DSC bude zpracována jako účet domény.
Dojde k výjimce pro "localhost", "127.0.0.1" a ":: 1" v části domény uživatelské jméno.

## <a name="psdscallowdomainuser"></a>PSDscAllowDomainUser

V DSC `Group` prostředků příklad výše, dotazování domény služby Active Directory *vyžaduje* účet domény.
V takovém případě přidejte `PSDscAllowDomainUser` vlastnost `ConfigurationData` blokovat následujícím způsobem:

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

Konfigurační skript nyní vygeneruje soubor MOF bez jakýchkoli chyb nebo upozornění.
