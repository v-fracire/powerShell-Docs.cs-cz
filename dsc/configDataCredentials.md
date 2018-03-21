---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Možnosti přihlašovací údaje v konfiguračních dat"
ms.openlocfilehash: 6ddf82c2b63309255ec3187d650677a6c3c2afb0
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="credentials-options-in-configuration-data"></a>Možnosti přihlašovací údaje v konfiguračních dat
>Platí pro: Prostředí Windows PowerShell 5.0

## <a name="plain-text-passwords-and-domain-users"></a>Hesla ve formátu prostého textu a uživatelé domény

Konfigurace DSC obsahující pověření bez šifrování vygeneruje chybovou zprávu o hesla v prostém textu.
Navíc DSC vygeneruje upozornění při použití přihlašovacích údajů do domény.
Chcete-li potlačit tyto chybové zprávy a upozornění používat klíčová slova, DSC konfigurační data:
* **PsDscAllowPlainTextPassword**
* **PsDscAllowDomainUser**

> [!NOTE]
> Ukládání nebo přenos hesel ve formátu prostého textu bez šifrování není zabezpečený. Doporučuje se zabezpečení přihlašovacích údajů pomocí techniky popsané dál v tomto tématu.
> Služba Azure Automation DSC umožňuje centrálně spravovat pověření k kompilovat v konfiguracích a bezpečně uložit.
> Informace najdete v tématu: [kompilaci konfigurace DSC / prostředků přihlašovacích údajů](/azure/automation/automation-dsc-compile#credential-assets)

Následuje příklad předávání přihlašovací údaje ve formátu prostého textu:

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

## <a name="handling-credentials-in-dsc"></a>Zpracování pověření v DSC

Prostředky konfigurace DSC spustit jako `Local System` ve výchozím nastavení.
Ale některé prostředky je nutné pověření, například když `Package` prostředků je potřeba nainstalovat software v části konkrétní uživatelský účet.

Starší prostředky používá pevně zakódovaným `Credential` název vlastnosti pro toto zpracování.
WMF 5.0 přidat automatické `PsDscRunAsCredential` vlastnost pro všechny prostředky.
Informace o používání `PsDscRunAsCredential`, najdete v části [DSC spuštěná s pověřeními uživatele](runAsUser.md).
Novější a vlastních prostředků pomocí této vlastnosti automatické místo vytvoření vlastní vlastnost pro přihlašovací údaje.

> [!NOTE]
> Návrh některé prostředky se mají používat více přihlašovací údaje pro konkrétní důvod, proč a budou mít vlastní vlastnosti přihlašovacích údajů.

K vyhledání dostupných přihlašovacích údajů vlastnosti prostředku, použijte buď `Get-DscResource -Name ResourceName -Syntax` nebo Intellisense (ISE) v (`CTRL+SPACE`).

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

Tento příklad používá [skupiny](https://msdn.microsoft.com/powershell/dsc/groupresource) prostředek z `PSDesiredStateConfiguration` integrovaného modulu prostředků DSC.
Můžete vytvořit místní skupiny a přidat nebo odebrat členy.
Přijímá i `Credential` vlastnost a automatického `PsDscRunAsCredential` vlastnost.
Ale prostředek používá jenom `Credential` vlastnost.

Další informace o `PsDscRunAsCredential` vlastnost, najdete v části [DSC spuštěná s pověřeními uživatele](runAsUser.md).

## <a name="example-the-group-resource-credential-property"></a>Příklad: Skupina prostředků vlastnost pověření

DSC běží pod `Local System`, takže už má oprávnění ke změně místní uživatelé a skupiny.
Pokud je člen přidat místní účet, se žádné přihlašovací údaje nezbytné.
Pokud `Group` prostředků přidá doménový účet do místní skupiny a pak je nutné pověření.

Anonymní dotazy do služby Active Directory nejsou povoleny.
`Credential` Vlastnost `Group` prostředek je doménový účet použít k dotazu služby Active Directory.
Pro většinu účelů to může být obecné uživatelský účet, ve výchozím nastavení mohou uživatelé *číst* většinu objektů ve službě Active Directory.

## <a name="example-configuration"></a>Příklad konfigurace

Následující příklad kódu používá DSC k naplnění místní skupiny s uživatelem domény:

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

Tento kód se generuje k chybě a upozornění:

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
1. Chybu vysvětluje, že se nedoporučují hesla v prostém textu
2. Upozornění informuje o tom proti pomocí pověření domény

## <a name="psdscallowplaintextpassword"></a>PsDscAllowPlainTextPassword

První chybovou zprávu s adresou URL naleznete v dokumentaci.
Tento odkaz vysvětluje, jak šifrovat pomocí hesla [ConfigurationData](https://msdn.microsoft.com/powershell/dsc/configdata) struktura a certifikát.
Další informace o certifikátech a DSC [si tento příspěvek](http://aka.ms/certs4dsc).

Chcete-li vynutit hesla v podobě prostého textu, prostředku vyžaduje `PsDscAllowPlainTextPassword` – klíčové slovo v konfigurační data části následujícím způsobem:

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
> `NodeName` se nesmí rovnat hvězdičky, konkrétním uzlu jméno je povinné.

**Microsoft informuje o tom, aby se zabránilo hesla v prostém textu z důvodu významné bezpečnostní riziko.**

Výjimku by při použití služby Azure Automation DSC, protože data se vždy ukládají zašifrovaně (na cestě, umístěná ve službě a v klidovém stavu uložených v uzlu).

## <a name="domain-credentials"></a>Domain Credentials

Spuštění skriptu konfigurace příklad opakujte (s nebo bez šifrování), stále generuje upozornění, že používáte doménu účtu pro přihlašovací údaje se nedoporučuje.
Pomocí místního účtu eliminuje potenciální ohrožení pověření domény, které by mohly být použity na jiných serverech.

**Pokud používáte přihlašovací údaje s prostředky DSC, raději místní účet přes účet domény, pokud je to možné.**

Pokud je '\' nebo '@' v `Username` vlastnosti přihlašovacích údajů, pak DSC bude zpracována jako účet domény.
Dojde k výjimce pro "localhost", "127.0.0.1" a ":: 1" v části domény uživatelského jména.

## <a name="psdscallowdomainuser"></a>PSDscAllowDomainUser

V DSC `Group` prostředků příkladu výše, dotazování domény služby Active Directory *vyžaduje* účet domény.
V takovém případě přidejte `PSDscAllowDomainUser` vlastnost, která má `ConfigurationData` blokovat následujícím způsobem:

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

Nyní konfigurační skript vygeneruje soubor MOF se žádné chyby nebo upozornění.
