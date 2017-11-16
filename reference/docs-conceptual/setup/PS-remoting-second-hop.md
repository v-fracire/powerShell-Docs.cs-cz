---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Vytváření druhé směrování v vzdálenou komunikaci prostředí PowerShell"
ms.openlocfilehash: f3b8280819e43bd67bd608ffd0ba9484c2bbc26c
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/31/2017
---
# <a name="making-the-second-hop-in-powershell-remoting"></a><span data-ttu-id="b2d3f-103">Vytváření druhé směrování v vzdálenou komunikaci prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2d3f-103">Making the second hop in PowerShell Remoting</span></span>

<span data-ttu-id="b2d3f-104">"Druhý směrování problém" odkazuje na situaci takto:</span><span class="sxs-lookup"><span data-stu-id="b2d3f-104">The "second hop problem" refers to a situation like the following:</span></span>

1. <span data-ttu-id="b2d3f-105">Jste přihlášeni k _Server_a_.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-105">You are logged in to _ServerA_.</span></span>
2. <span data-ttu-id="b2d3f-106">Z _Server_a_, spouští vzdálenou relaci prostředí PowerShell pro připojení k _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-106">From _ServerA_, you start a remote PowerShell session to connect to _ServerB_.</span></span>
3. <span data-ttu-id="b2d3f-107">Příkaz spustíte v _ServerB_ prostřednictvím vaší vzdálenou komunikaci prostředí PowerShell relace pokusí o přístup k prostředku na _ServerC_.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-107">A command you run on _ServerB_ via your PowerShell Remoting session attempts to access a resource on _ServerC_.</span></span>
4. <span data-ttu-id="b2d3f-108">Přístup k danému prostředku na _ServerC_ byl odepřen, protože jste použili k vytvoření relace vzdálenou komunikaci prostředí PowerShell přihlašovací údaje nejsou předat z _ServerB_ k _ServerC_.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-108">Access to the resource on _ServerC_ is denied, because the credentials you used to create the PowerShell Remoting session are not passed from _ServerB_ to _ServerC_.</span></span>

<span data-ttu-id="b2d3f-109">Chcete-li vyřešit tento problém několika způsoby.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-109">There are several ways to address this problem.</span></span> <span data-ttu-id="b2d3f-110">V tomto tématu se podíváme řadu nejoblíbenější řešení druhý problém směrování.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-110">In this topic, we'll look at several of the most popular solutions to the second hop problem.</span></span>

## <a name="credssp"></a><span data-ttu-id="b2d3f-111">CredSSP</span><span class="sxs-lookup"><span data-stu-id="b2d3f-111">CredSSP</span></span>

<span data-ttu-id="b2d3f-112">Můžete použít [Credential Security Support Provider (CredSSP)](https://msdn.microsoft.com/en-us/library/windows/desktop/bb931352.aspx) pro ověřování.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-112">You can use the [Credential Security Support Provider (CredSSP)](https://msdn.microsoft.com/en-us/library/windows/desktop/bb931352.aspx) for authentication.</span></span> <span data-ttu-id="b2d3f-113">Zprostředkovatel CredSSP ukládá do mezipaměti přihlašovací údaje na vzdáleném serveru (_ServerB_), takže ho pomocí otevře až útoku krádeží přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-113">CredSSP caches credentials on the remote server (_ServerB_), so using it opens you up to credential theft attacks.</span></span> <span data-ttu-id="b2d3f-114">Pokud vzdálený počítač v ohrožení, útočník má přístup k přihlašovacím údajům uživatele.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-114">If the remote computer is compromised, the attacker has access to the user's credentials.</span></span> <span data-ttu-id="b2d3f-115">Ve výchozím nastavení v počítačích klient i server vypnutá CredSSP.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-115">CredSSP is disabled by default on both client and server computers.</span></span> <span data-ttu-id="b2d3f-116">Měli byste povolit zprostředkovatele CredSSP pouze v nejdůvěryhodnější prostředích.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-116">You should enable CredSSP only in the most trusted environments.</span></span> <span data-ttu-id="b2d3f-117">Například správce domény připojení k řadiči domény, protože řadič domény je vysoce důvěryhodný.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-117">For example, a domain administrator connecting to a domain controller because the domain controller is highly trusted.</span></span>

<span data-ttu-id="b2d3f-118">Další informace o potížích se zabezpečením při použití ověřování CredSSP pro vzdálenou komunikaci prostředí PowerShell najdete v tématu [náhodnému napadení: Pozor CredSSP](http://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-118">For more information about security concerns when using CredSSP for PowerShell Remoting, see [Accidental Sabotage: Beware of CredSSP](http://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).</span></span>

<span data-ttu-id="b2d3f-119">Další informace o útoku krádeží přihlašovacích údajů najdete v tématu [útoky omezení dopadu útoků Pass-the-Hash (PtH) a ostatní krádeží přihlašovacích údajů](https://www.microsoft.com/en-us/download/details.aspx?id=36036).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-119">For more information about credential theft attacks, see [Mitigating Pass-the-Hash (PtH) Attacks and Other Credential Theft](https://www.microsoft.com/en-us/download/details.aspx?id=36036).</span></span>

<span data-ttu-id="b2d3f-120">Příklad toho, jak povolit a používat ověřování CredSSP pro vzdálenou komunikaci prostředí PowerShell naleznete v části [pomocí zprostředkovatele CredSSP sekundu směrování problém vyřešit](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-120">For an example of how to enable and use CredSSP for PowerShell remoting, see [Using CredSSP to solve the second-hop problem](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).</span></span>

### <a name="pros"></a><span data-ttu-id="b2d3f-121">Výhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-121">Pros</span></span>

- <span data-ttu-id="b2d3f-122">Funguje pro všechny servery se systémem Windows Server 2008 nebo novějším.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-122">It works for all servers with Windows Server 2008 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="b2d3f-123">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-123">Cons</span></span>

- <span data-ttu-id="b2d3f-124">Má slabší zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-124">Has security vulnerabilities.</span></span>
- <span data-ttu-id="b2d3f-125">Vyžaduje konfiguraci rolí klient i server.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-125">Requires configuration of both client and server roles.</span></span>

## <a name="kerberos-delegation-unconstrained"></a><span data-ttu-id="b2d3f-126">Delegování protokolu Kerberos (neomezeného)</span><span class="sxs-lookup"><span data-stu-id="b2d3f-126">Kerberos delegation (unconstrained)</span></span>

<span data-ttu-id="b2d3f-127">Delegování protokolu Kerberos neomezeného můžete také použít k nastavení připojení přes další počítač.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-127">You can also used Kerberos unconstrained delegation to make the second hop.</span></span> <span data-ttu-id="b2d3f-128">Tato metoda poskytuje však žádné řízení použití delegovanými přihlašovacími údaji.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-128">However, this method provides no control of where delegated credentials are used.</span></span>

><span data-ttu-id="b2d3f-129">**Poznámka:** účtů služby Active Directory, které mají **účet je citlivý a nelze jej delegovat** sada vlastností není možné delegovat.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-129">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="b2d3f-130">Další informace najdete v tématu [fokus zabezpečení: analýzy 'Účet je citlivý a nelze jej delegovat' k privilegovaným účtům](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) a [nástroje ověřování protokolu Kerberos a nastavení](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="b2d3f-130">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="b2d3f-131">Výhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-131">Pros</span></span>

- <span data-ttu-id="b2d3f-132">Vyžaduje žádné speciální kódování.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-132">Requires no special coding.</span></span>

### <a name="cons"></a><span data-ttu-id="b2d3f-133">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-133">Cons</span></span>

- <span data-ttu-id="b2d3f-134">Pro WinRM nepodporuje připojení přes další počítač.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-134">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="b2d3f-135">Poskytuje žádnou kontrolu nad použití přihlašovacích údajů, vytváření ohrožení zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-135">Provides no control over where credentials are used, creating a security vulnerability.</span></span>

## <a name="kerberos-constrained-delegation"></a><span data-ttu-id="b2d3f-136">Omezené delegování protokolu Kerberos</span><span class="sxs-lookup"><span data-stu-id="b2d3f-136">Kerberos constrained delegation</span></span>

<span data-ttu-id="b2d3f-137">Chcete-li druhé směrování můžete starší verze omezené delegování (není založené na prostředcích).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-137">You can use legacy constrained delegation (not resource-based) to make the second hop.</span></span> 

><span data-ttu-id="b2d3f-138">**Poznámka:** účtů služby Active Directory, které mají **účet je citlivý a nelze jej delegovat** sada vlastností není možné delegovat.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-138">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="b2d3f-139">Další informace najdete v tématu [fokus zabezpečení: analýzy 'Účet je citlivý a nelze jej delegovat' k privilegovaným účtům](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) a [nástroje ověřování protokolu Kerberos a nastavení](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="b2d3f-139">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="b2d3f-140">Výhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-140">Pros</span></span>

- <span data-ttu-id="b2d3f-141">Vyžaduje žádné speciální kódování</span><span class="sxs-lookup"><span data-stu-id="b2d3f-141">Requires no special coding</span></span>

### <a name="cons"></a><span data-ttu-id="b2d3f-142">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-142">Cons</span></span>

- <span data-ttu-id="b2d3f-143">Pro WinRM nepodporuje připojení přes další počítač.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-143">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="b2d3f-144">Musí být nakonfigurované na objektu služby Active Directory vzdáleného serveru (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-144">Must be configured on the Active Directory object of the remote server (_ServerB_).</span></span>
- <span data-ttu-id="b2d3f-145">Omezeno na jednu doménu.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-145">Limited to one domain.</span></span> <span data-ttu-id="b2d3f-146">Nelze napříč doménami nebo doménovými strukturami.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-146">Cannot cross domains or forests.</span></span>
- <span data-ttu-id="b2d3f-147">Vyžaduje práva k aktualizaci objekty a hlavní názvy služby (SPN).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-147">Requires rights to update objects and Service Principal Names (SPNs).</span></span>

## <a name="resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="b2d3f-148">Na základě prostředků omezené delegování protokolu Kerberos</span><span class="sxs-lookup"><span data-stu-id="b2d3f-148">Resource-based Kerberos constrained delegation</span></span>

<span data-ttu-id="b2d3f-149">Pomocí protokolu Kerberos založené na prostředcích omezeného delegování (zavedená v systému Windows Server 2012), konfigurace delegování přihlašovacích údajů na objekt serveru, kde jsou umístěny prostředky.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-149">Using resource-based Kerberos constrained delegation (introduced in Windows Server 2012), you configure credential delegation on the server object where resources reside.</span></span>
<span data-ttu-id="b2d3f-150">Druhý scénář směrování popsané výše, nakonfigurujete _ServerC_ zadejte, kde bude přijímat delegované přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-150">In the second hop scenario described above, you configure _ServerC_ to specify from where it will accept delegated credentials.</span></span>

><span data-ttu-id="b2d3f-151">**Poznámka:** účtů služby Active Directory, které mají **účet je citlivý a nelze jej delegovat** sada vlastností není možné delegovat.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-151">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="b2d3f-152">Další informace najdete v tématu [fokus zabezpečení: analýzy 'Účet je citlivý a nelze jej delegovat' k privilegovaným účtům](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) a [nástroje ověřování protokolu Kerberos a nastavení](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="b2d3f-152">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="b2d3f-153">Výhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-153">Pros</span></span>

- <span data-ttu-id="b2d3f-154">Přihlašovací údaje se neukládají.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-154">Credentials are not stored.</span></span>
- <span data-ttu-id="b2d3f-155">Relativně jednoduchá konfigurace pomocí rutin prostředí PowerShell – žádné speciální kódování vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-155">Relatively easy to configure by using PowerShell cmdlets--no special coding required.</span></span>
- <span data-ttu-id="b2d3f-156">Je vyžadován přístup žádné speciální domény.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-156">No special domain access is required.</span></span>
- <span data-ttu-id="b2d3f-157">Funguje napříč doménami a doménovými strukturami.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-157">Works across domains and forests.</span></span>
- <span data-ttu-id="b2d3f-158">Kód prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-158">PowerShell code.</span></span>

### <a name="cons"></a><span data-ttu-id="b2d3f-159">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-159">Cons</span></span>

- <span data-ttu-id="b2d3f-160">Vyžaduje systém Windows Server 2012 nebo novějším.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-160">Requires Windows Server 2012 or later.</span></span>
- <span data-ttu-id="b2d3f-161">Pro WinRM nepodporuje připojení přes další počítač.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-161">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="b2d3f-162">Vyžaduje práva k aktualizaci objekty a hlavní názvy služby (SPN).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-162">Requires rights to update objects and Service Principal Names (SPNs).</span></span> 

### <a name="example"></a><span data-ttu-id="b2d3f-163">Příklad</span><span class="sxs-lookup"><span data-stu-id="b2d3f-163">Example</span></span>

<span data-ttu-id="b2d3f-164">Podívejme se na příklad, který konfiguruje prostředků na základě omezené delegování prostředí PowerShell _ServerC_ umožňující delegovanými přihlašovacími údaji ze _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-164">Let's look at a PowerShell example that configures resource based constrained delegation on _ServerC_ to allow delegated credentials from a _ServerB_.</span></span>
<span data-ttu-id="b2d3f-165">Tento příklad předpokládá, že všechny servery se systémem Windows Server 2012 nebo novější, a jestli je aspoň jeden řadič domény systému Windows Server 2012 každou doménu, do které žádné servery patří.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-165">This example assumes that all servers are running Windows Server 2012 or later, and that there is at least one Windows Server 2012 domain controller each domain to which any of the servers belong.</span></span>

<span data-ttu-id="b2d3f-166">Než budete moct nakonfigurovat omezené delegování, je nutné přidat `RSAT-AD-PowerShell` funkci nainstalovat modul prostředí PowerShell služby Active Directory a potom tento modul importovat do relace:</span><span class="sxs-lookup"><span data-stu-id="b2d3f-166">Before you can configure constrained delegation, you must add the `RSAT-AD-PowerShell` feature to install the Active Directory PowerShell module, and then import that module into your session:</span></span>

```powershell
PS C:\> Add-WindowsFeature RSAT-AD-PowerShell

PS C:\> Import-Module ActiveDirector
```
<span data-ttu-id="b2d3f-167">Teď máte několik dostupných rutin **PrincipalsAllowedToDelegateToAccount** parametr:</span><span class="sxs-lookup"><span data-stu-id="b2d3f-167">Several available cmdlets now have a **PrincipalsAllowedToDelegateToAccount** parameter:</span></span>

```powershell
PS C:\> Get-Command -ParameterName PrincipalsAllowedToDelegateToAccount

CommandType Name                 ModuleName     
----------- ----                 ----------     
Cmdlet      New-ADComputer       ActiveDirectory
Cmdlet      New-ADServiceAccount ActiveDirectory
Cmdlet      New-ADUser           ActiveDirectory
Cmdlet      Set-ADComputer       ActiveDirectory
Cmdlet      Set-ADServiceAccount ActiveDirectory
Cmdlet      Set-ADUser           ActiveDirectory
```

<span data-ttu-id="b2d3f-168">**PrincipalsAllowedToDelegateToAccount** parametr nastaví atributu objektu služby Active Directory **msDS-AllowedToActOnBehalfOfOtherIdentity**, který obsahuje seznam řízení přístupu (ACL), Určuje, které účty mají oprávnění delegovat přihlašovací údaje pro přidružený účet (v našem příkladu bude účet počítače pro _Server_).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-168">The **PrincipalsAllowedToDelegateToAccount** parameter sets the Active Directory object attribute **msDS-AllowedToActOnBehalfOfOtherIdentity**, which contains an access control list (ACL) that specifies which accounts have permission to delegate credentials to the associated account (in our example, it will be the machine account for _Server_).</span></span>

<span data-ttu-id="b2d3f-169">Nyní nastavíme proměnné použijeme představují servery:</span><span class="sxs-lookup"><span data-stu-id="b2d3f-169">Now let's set up the variables we'll use to represent the servers:</span></span>

```powershell
# Set up variables for reuse            
$ServerA = $env:COMPUTERNAME            
$ServerB = Get-ADComputer -Identity ServerB            
$ServerC = Get-ADComputer -Identity ServerC            
```

<span data-ttu-id="b2d3f-170">WinRM (a proto vzdálenou komunikaci prostředí PowerShell) ve výchozím nastavení spustí jako účet počítače.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-170">WinRM (and therefore PowerShell remoting) runs as the computer account by default.</span></span> <span data-ttu-id="b2d3f-171">Můžete to vidět prohlížením **%{StartName/** vlastnost `winrm` služby:</span><span class="sxs-lookup"><span data-stu-id="b2d3f-171">You can see this by looking at the **StartName** property of the `winrm` service:</span></span>

```powershell
PS C:\> Get-WmiObject win32_service -filter 'name="winrm"' | Format-List StartName

StartName : NT AUTHORITY\NetworkService
```

<span data-ttu-id="b2d3f-172">Pro _ServerC_ na povolit delegování z relace vzdálenou komunikaci prostředí PowerShell _ServerB_, jsme udělí přístup nastavením **PrincipalsAllowedToDelegateToAccount** parametr na _ServerC_ na objekt počítače z _ServerB_:</span><span class="sxs-lookup"><span data-stu-id="b2d3f-172">For _ServerC_ to allow delegation from a PowerShell remoting session on _ServerB_, we will grant access by setting the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to the computer object of _ServerB_:</span></span>

```powershell
# Grant resource-based Kerberos constrained delegation            
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB            
            
# Check the value of the attribute directly            
$x = Get-ADComputer -Identity $ServerC -Properties msDS-AllowedToActOnBehalfOfOtherIdentity            
$x.'msDS-AllowedToActOnBehalfOfOtherIdentity'.Access            
            
# Check the value of the attribute indirectly            
Get-ADComputer -Identity $ServerC -Properties PrincipalsAllowedToDelegateToAccount
```

<span data-ttu-id="b2d3f-173">Protokolu Kerberos [Key Distribution (Center KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) mezipamětí odepřen pokusů o přístup (negativní mezipaměť) 15 minut.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-173">The Kerberos [Key Distribution Center (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) caches denied access attempts (negative cache) for 15 minutes.</span></span> <span data-ttu-id="b2d3f-174">Pokud _ServerB_ dříve pokusil o přístup k _ServerC_, budete muset vymazat mezipaměť na _ServerB_ vyvoláním následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="b2d3f-174">If _ServerB_ has previously attempted to access _ServerC_, you will need to clear the cache on _ServerB_ by invoking the following command:</span></span>

```powershell
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {            
    klist purge -li 0x3e7            
}
```

<span data-ttu-id="b2d3f-175">Můžete také restartovat počítač, nebo počkejte alespoň 15 minut a vymažte mezipaměť.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-175">You could also restart the computer, or wait at least 15 minutes to clear the cache.</span></span>

<span data-ttu-id="b2d3f-176">Po vymazání mezipaměti, je možné úspěšně spustit kód z _Server_a_ prostřednictvím _ServerB_ k _ServerC_:</span><span class="sxs-lookup"><span data-stu-id="b2d3f-176">After clearing the cache, you can successfully run code from _ServerA_ through _ServerB_ to _ServerC_:</span></span>

```powershell
# Capture a credential            
$cred = Get-Credential Contoso\Alice            
            
# Test kerberos double hop            
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {            
    Test-Path \\$($using:ServerC.Name)\C$            
    Get-Process lsass -ComputerName $($using:ServerC.Name)            
    Get-EventLog -LogName System -Newest 3 -ComputerName $($using:ServerC.Name)            
}
```

<span data-ttu-id="b2d3f-177">V tomto příkladu `$using` proměnná se používá k zajištění `$ServerC` proměnné, které jsou viditelné pro _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-177">In this example, the `$using` variable is used to make the `$ServerC` variable visible to _ServerB_.</span></span> <span data-ttu-id="b2d3f-178">Další informace o `$using` proměnné, viz [about_Remote_Variables](https://technet.microsoft.com/en-us/library/jj149005.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-178">For more information about the `$using` variable, see [about_Remote_Variables](https://technet.microsoft.com/en-us/library/jj149005.aspx).</span></span>

<span data-ttu-id="b2d3f-179">Povolit více serverů pro přihlašovací údaje pro delegování _ServerC_, nastavte hodnotu **PrincipalsAllowedToDelegateToAccount** parametr na _ServerC_ do pole:</span><span class="sxs-lookup"><span data-stu-id="b2d3f-179">To allow multiple servers to delegate credentials to _ServerC_, set the value of the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to an array:</span></span>

```powershell
# Set up variables for each server            
$ServerB1 = Get-ADComputer -Identity ServerB1            
$ServerB2 = Get-ADComputer -Identity ServerB2            
$ServerB3 = Get-ADComputer -Identity ServerB3            
$ServerC  = Get-ADComputer -Identity ServerC            
            
# Grant resource-based Kerberos constrained delegation            
Set-ADComputer -Identity $ServerC `
    -PrincipalsAllowedToDelegateToAccount @($ServerB1,$ServerB2,$ServerB3)
```

<span data-ttu-id="b2d3f-180">Pokud chcete, aby druhé směrování mezi doménami, přidejte plně kvalifikovaný název domény (FQDN) řadiče domény, domény, ke kterému _ServerB_ patří:</span><span class="sxs-lookup"><span data-stu-id="b2d3f-180">If you want to make the second hop across domains, add fully-qualified domain name (FQDN) of the domain controller of the domain to which _ServerB_ belongs:</span></span>

```powershell
# For ServerC in Contoso domain and ServerB in other domain            
$ServerB = Get-ADComputer -Identity ServerB -Server dc1.alpineskihouse.com            
$ServerC = Get-ADComputer -Identity ServerC            
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB
```

<span data-ttu-id="b2d3f-181">Chcete-li odebrat možnost delegovat přihlašovací údaje pro ServerC, nastavte hodnotu **PrincipalsAllowedToDelegateToAccount** parametr na _ServerC_ k `$null`:</span><span class="sxs-lookup"><span data-stu-id="b2d3f-181">To remove the ability to delegate credentials to ServerC, set the value of the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to `$null`:</span></span>

```powershell
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $null
```

### <a name="information-on-resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="b2d3f-182">Informace o založené na prostředcích omezené delegování protokolu Kerberos</span><span class="sxs-lookup"><span data-stu-id="b2d3f-182">Information on resource-based Kerberos constrained delegation</span></span>

- [<span data-ttu-id="b2d3f-183">Co je nového v ověřování protokolem Kerberos</span><span class="sxs-lookup"><span data-stu-id="b2d3f-183">What's New in Kerberos Authentication</span></span>](https://technet.microsoft.com/library/hh831747.aspx)
- [<span data-ttu-id="b2d3f-184">Jak Windows Server 2012 usnadňuje problémové Kerberos omezeného delegování, část 1</span><span class="sxs-lookup"><span data-stu-id="b2d3f-184">How Windows Server 2012 Eases the Pain of Kerberos Constrained Delegation, Part 1</span></span>](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1)
- [<span data-ttu-id="b2d3f-185">Jak Windows Server 2012 usnadňuje problémové Kerberos omezeného delegování, část 2</span><span class="sxs-lookup"><span data-stu-id="b2d3f-185">How Windows Server 2012 Eases the Pain of Kerberos Constrained Delegation, Part 2</span></span>](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-2)
- [<span data-ttu-id="b2d3f-186">Principy protokolu Kerberos omezeného delegování pro nasazení Proxy aplikace služby Azure Active Directory pomocí integrovaného ověřování systému Windows</span><span class="sxs-lookup"><span data-stu-id="b2d3f-186">Understanding Kerberos Constrained Delegation for Azure Active Directory Application Proxy Deployments with Integrated Windows Authentication</span></span>](http://aka.ms/kcdpaper)
- <span data-ttu-id="b2d3f-187">[[MS-ADA2]: Active Directory schématu atributů M2.210 atribut msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/en-us/library/hh554126.aspx)</span><span class="sxs-lookup"><span data-stu-id="b2d3f-187">[[MS-ADA2]: Active Directory Schema Attributes M2.210 Attribute msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/en-us/library/hh554126.aspx)</span></span>
- <span data-ttu-id="b2d3f-188">[[MS-SFU]: rozšíření protokolu Kerberos: Service for User a protokolu 1.3.2 S4U2proxy omezeného delegování](https://msdn.microsoft.com/en-us/library/cc246079.aspx)</span><span class="sxs-lookup"><span data-stu-id="b2d3f-188">[[MS-SFU]: Kerberos Protocol Extensions: Service for User and Constrained Delegation Protocol 1.3.2 S4U2proxy](https://msdn.microsoft.com/en-us/library/cc246079.aspx)</span></span>
- [<span data-ttu-id="b2d3f-189">Prostředků na základě protokolu Kerberos omezeného delegování</span><span class="sxs-lookup"><span data-stu-id="b2d3f-189">Resource Based Kerberos Constrained Delegation</span></span>](https://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)
- [<span data-ttu-id="b2d3f-190">Vzdálená správa bez použití PrincipalsAllowedToDelegateToAccount omezeného delegování</span><span class="sxs-lookup"><span data-stu-id="b2d3f-190">Remote Administration Without Constrained Delegation Using PrincipalsAllowedToDelegateToAccount</span></span>](https://blogs.msdn.microsoft.com/taylorb/2012/11/06/remote-administration-without-constrained-delegation-using-principalsallowedtodelegatetoaccount/)

## <a name="pssessionconfiguration-using-runas"></a><span data-ttu-id="b2d3f-191">PSSessionConfiguration použitím RunAs</span><span class="sxs-lookup"><span data-stu-id="b2d3f-191">PSSessionConfiguration using RunAs</span></span>

<span data-ttu-id="b2d3f-192">Konfigurace relace můžete vytvořit na _ServerB_ a nastavit jeho **RunAsCredential** parametr.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-192">You can create a session configuration on _ServerB_ and set its **RunAsCredential** parameter.</span></span>

<span data-ttu-id="b2d3f-193">Informace o používání PSSessionConfiguration a RunAs druhý směrování problém vyřešit, najdete v článku [jiné řešení pro vzdálenou komunikaci prostředí PowerShell vícenásobného předávání](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-193">For information about using PSSessionConfiguration and RunAs to solve the second hop problem, see [Another solution to multi-hop PowerShell remoting](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).</span></span>

### <a name="pros"></a><span data-ttu-id="b2d3f-194">Výhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-194">Pros</span></span>

- <span data-ttu-id="b2d3f-195">Funguje s jakýmkoli serverem s WMF 3.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-195">Works with any server with WMF 3.0 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="b2d3f-196">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-196">Cons</span></span>

- <span data-ttu-id="b2d3f-197">Vyžaduje konfiguraci **PSSessionConfiguration** a **RunAs** na každém serveru, zprostředkující (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-197">Requires configuration of **PSSessionConfiguration** and **RunAs** on every intermediate server (_ServerB_).</span></span>
- <span data-ttu-id="b2d3f-198">Vyžaduje heslo údržby, pokud používáte doménu **RunAs** účtu</span><span class="sxs-lookup"><span data-stu-id="b2d3f-198">Requires password maintenance when using a domain **RunAs** account</span></span>

## <a name="just-enough-administration-jea"></a><span data-ttu-id="b2d3f-199">Akorát správy (JEA)</span><span class="sxs-lookup"><span data-stu-id="b2d3f-199">Just Enough Administration (JEA)</span></span>

<span data-ttu-id="b2d3f-200">JEA umožňuje omezit jaké příkazy můžete spustit správce během relace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-200">JEA allows you to restrict what commands an administrator can run during a PowerShell session.</span></span> <span data-ttu-id="b2d3f-201">Může sloužit k jejich vyřešení druhý směrování.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-201">It can be used to solve the second hop problem.</span></span>

<span data-ttu-id="b2d3f-202">Informace o JEA najdete v tématu [právě dostatečně správy](https://docs.microsoft.com/en-us/powershell/jea/overview).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-202">For information about JEA, see [Just Enough Administration](https://docs.microsoft.com/en-us/powershell/jea/overview).</span></span>

### <a name="pros"></a><span data-ttu-id="b2d3f-203">Výhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-203">Pros</span></span>

- <span data-ttu-id="b2d3f-204">Žádná Údržba heslo při použití virtuální účet.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-204">No password maintenance when using a virtual account.</span></span>

### <a name="cons"></a><span data-ttu-id="b2d3f-205">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-205">Cons</span></span>

- <span data-ttu-id="b2d3f-206">Vyžaduje WMF 5.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-206">Requires WMF 5.0 or later.</span></span>
- <span data-ttu-id="b2d3f-207">Vyžaduje konfiguraci na každém serveru, zprostředkující (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="b2d3f-207">Requires configuration on every intermediate server (_ServerB_).</span></span>

## <a name="pass-credentials-inside-an-invoke-command-script-block"></a><span data-ttu-id="b2d3f-208">Předávat přihlašovací údaje uvnitř bloku skriptu Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="b2d3f-208">Pass credentials inside an Invoke-Command script block</span></span>

<span data-ttu-id="b2d3f-209">Můžete předat pověření uvnitř **ScriptBlock** parametr volání [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command) rutiny.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-209">You can pass credentials inside the **ScriptBlock** parameter of a call to the [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command) cmdlet.</span></span>

### <a name="pros"></a><span data-ttu-id="b2d3f-210">Výhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-210">Pros</span></span>

- <span data-ttu-id="b2d3f-211">Nevyžaduje konfiguraci speciální serveru.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-211">Does not require special server configuration.</span></span>
- <span data-ttu-id="b2d3f-212">Funguje na všechny servery se spuštěným WMF 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-212">Works on any server running WMF 2.0 or later.</span></span>

## <a name="cons"></a><span data-ttu-id="b2d3f-213">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="b2d3f-213">Cons</span></span>

- <span data-ttu-id="b2d3f-214">Vyžaduje technika nevhodných kódu.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-214">Requires an awkward code technique.</span></span>
- <span data-ttu-id="b2d3f-215">Pokud systém WMF 2.0, vyžaduje jinou syntaxi pro předání argumentů ke vzdálené relaci.</span><span class="sxs-lookup"><span data-stu-id="b2d3f-215">If running WMF 2.0, requires different syntax for passing arguments to a remote session.</span></span>

## <a name="example"></a><span data-ttu-id="b2d3f-216">Příklad</span><span class="sxs-lookup"><span data-stu-id="b2d3f-216">Example</span></span>

<span data-ttu-id="b2d3f-217">Následující příklad ukazuje, jak předat přihlašovací údaje v **Invoke-Command** bloku skriptu:</span><span class="sxs-lookup"><span data-stu-id="b2d3f-217">The following example shows how to pass credentials in an **Invoke-Command** script block:</span></span>

```powershell
# This works without delegation, passing fresh creds            
# Note $Using:Cred in nested request            
$cred = Get-Credential Contoso\Administrator            
Invoke-Command -ComputerName ServerB -Credential $cred -ScriptBlock {            
    hostname            
    Invoke-Command -ComputerName ServerC -Credential $Using:cred -ScriptBlock {hostname}            
}
```

## <a name="see-also"></a><span data-ttu-id="b2d3f-218">Viz taky</span><span class="sxs-lookup"><span data-stu-id="b2d3f-218">See also</span></span>

[<span data-ttu-id="b2d3f-219">Důležité informace o zabezpečení pro vzdálenou komunikaci prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2d3f-219">PowerShell Remoting Security Considerations</span></span>](WinRMSecurity.md)








 