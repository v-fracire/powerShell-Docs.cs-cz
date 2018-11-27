---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Díky tomu druhé směrování vzdálené komunikace Powershellu
ms.openlocfilehash: 06ca43e3e0524d89ec6f66f6553c4c75072beaf3
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320699"
---
# <a name="making-the-second-hop-in-powershell-remoting"></a><span data-ttu-id="5dfe5-103">Díky tomu druhé směrování vzdálené komunikace Powershellu</span><span class="sxs-lookup"><span data-stu-id="5dfe5-103">Making the second hop in PowerShell Remoting</span></span>

<span data-ttu-id="5dfe5-104">"Druhý segment směrování problém" odkazuje na situace nějak takto:</span><span class="sxs-lookup"><span data-stu-id="5dfe5-104">The "second hop problem" refers to a situation like the following:</span></span>

1. <span data-ttu-id="5dfe5-105">Jste přihlášeni k _Server_a_.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-105">You are logged in to _ServerA_.</span></span>
2. <span data-ttu-id="5dfe5-106">Z _Server_a_, spouští vzdálenou relaci prostředí PowerShell pro připojení k _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-106">From _ServerA_, you start a remote PowerShell session to connect to _ServerB_.</span></span>
3. <span data-ttu-id="5dfe5-107">Příkaz můžete spustit na _ServerB_ prostřednictvím vaší vzdálené komunikace Powershellu relace pokusí získat přístup k prostředku na _ServerC_.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-107">A command you run on _ServerB_ via your PowerShell Remoting session attempts to access a resource on _ServerC_.</span></span>
4. <span data-ttu-id="5dfe5-108">Přístup k prostředku na _ServerC_ byl odepřen, protože nejsou přihlašovací údaje, které jste použili k vytvoření relace vzdálené komunikace Powershellu předat z _ServerB_ k _ServerC_.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-108">Access to the resource on _ServerC_ is denied, because the credentials you used to create the PowerShell Remoting session are not passed from _ServerB_ to _ServerC_.</span></span>

<span data-ttu-id="5dfe5-109">Existuje několik způsobů, jak tento problém vyřešit.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-109">There are several ways to address this problem.</span></span> <span data-ttu-id="5dfe5-110">V tomto tématu se podíváme na některé z nejoblíbenějších řešení problému druhý segment směrování.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-110">In this topic, we'll look at several of the most popular solutions to the second hop problem.</span></span>

## <a name="credssp"></a><span data-ttu-id="5dfe5-111">CredSSP</span><span class="sxs-lookup"><span data-stu-id="5dfe5-111">CredSSP</span></span>

<span data-ttu-id="5dfe5-112">Můžete použít [Credential Security Support Provider (CredSSP Credential)](https://msdn.microsoft.com/library/windows/desktop/bb931352.aspx) pro ověřování.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-112">You can use the [Credential Security Support Provider (CredSSP)](https://msdn.microsoft.com/library/windows/desktop/bb931352.aspx) for authentication.</span></span> <span data-ttu-id="5dfe5-113">CredSSP ukládá do mezipaměti přihlašovací údaje na vzdáleném serveru (_ServerB_), takže ho pomocí otevře až útoků využívajících krádež přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-113">CredSSP caches credentials on the remote server (_ServerB_), so using it opens you up to credential theft attacks.</span></span> <span data-ttu-id="5dfe5-114">Pokud je vzdálený počítač v ohrožení, útočník má přístup k přihlašovacím údajům uživatele.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-114">If the remote computer is compromised, the attacker has access to the user's credentials.</span></span> <span data-ttu-id="5dfe5-115">CredSSP je ve výchozím nastavení na klientských i serverových počítačích zakázána.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-115">CredSSP is disabled by default on both client and server computers.</span></span> <span data-ttu-id="5dfe5-116">Pouze v nejdůvěryhodnějším prostředí byste měli povolit zprostředkovatele CredSSP.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-116">You should enable CredSSP only in the most trusted environments.</span></span> <span data-ttu-id="5dfe5-117">Například správce domény připojení k řadiči domény, protože řadič domény je vysoce důvěryhodných.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-117">For example, a domain administrator connecting to a domain controller because the domain controller is highly trusted.</span></span>

<span data-ttu-id="5dfe5-118">Další informace o zajištění zabezpečení při použití ověřování CredSSP pro vzdálenou komunikaci prostředí PowerShell najdete v tématu [náhodného napadení zařízení: Mějte na paměti, CredSSP](https://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-118">For more information about security concerns when using CredSSP for PowerShell Remoting, see [Accidental Sabotage: Beware of CredSSP](https://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).</span></span>

<span data-ttu-id="5dfe5-119">Další informace o útoků využívajících krádež přihlašovacích údajů najdete v tématu [útoky obrana proti útokům Pass-the-Hash (PtH) a dalším metodám krádeže přihlašovacích údajů](https://www.microsoft.com/en-us/download/details.aspx?id=36036).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-119">For more information about credential theft attacks, see [Mitigating Pass-the-Hash (PtH) Attacks and Other Credential Theft](https://www.microsoft.com/en-us/download/details.aspx?id=36036).</span></span>

<span data-ttu-id="5dfe5-120">Příklad toho, jak povolit a používat CredSSP pro vzdálenou komunikaci prostředí PowerShell, najdete v části [pomocí zprostředkovatele CredSSP pro vyřešení problému druhé směrování](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-120">For an example of how to enable and use CredSSP for PowerShell remoting, see [Using CredSSP to solve the second-hop problem](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).</span></span>

### <a name="pros"></a><span data-ttu-id="5dfe5-121">Výhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-121">Pros</span></span>

- <span data-ttu-id="5dfe5-122">Funguje to pro všechny servery s Windows serverem 2008 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-122">It works for all servers with Windows Server 2008 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="5dfe5-123">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-123">Cons</span></span>

- <span data-ttu-id="5dfe5-124">Má ohrožení zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-124">Has security vulnerabilities.</span></span>
- <span data-ttu-id="5dfe5-125">Vyžaduje konfiguraci rolí klienta a serveru.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-125">Requires configuration of both client and server roles.</span></span>

## <a name="kerberos-delegation-unconstrained"></a><span data-ttu-id="5dfe5-126">Delegování protokolu Kerberos (vstupy bez omezení)</span><span class="sxs-lookup"><span data-stu-id="5dfe5-126">Kerberos delegation (unconstrained)</span></span>

<span data-ttu-id="5dfe5-127">Delegování protokolu Kerberos neomezeného lze také vytvořit druhý segment směrování.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-127">You can also used Kerberos unconstrained delegation to make the second hop.</span></span> <span data-ttu-id="5dfe5-128">Tato metoda však poskytuje žádnou kontrolu, ve kterém se používají delegovaná pověření.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-128">However, this method provides no control of where delegated credentials are used.</span></span>

><span data-ttu-id="5dfe5-129">**Poznámka:** účtů služby Active Directory, které mají **účet je citlivý a nelze jej delegovat** nastavenou vlastnost není možné delegovat.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-129">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="5dfe5-130">Další informace najdete v tématu [fokus zabezpečení: analyzování "Účet je citlivý a nelze jej delegovat" pro privilegované účty](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) a [nástroje pro ověřování protokolu Kerberos a nastavení](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="5dfe5-130">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="5dfe5-131">Výhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-131">Pros</span></span>

- <span data-ttu-id="5dfe5-132">Vyžaduje žádné speciální kódování.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-132">Requires no special coding.</span></span>

### <a name="cons"></a><span data-ttu-id="5dfe5-133">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-133">Cons</span></span>

- <span data-ttu-id="5dfe5-134">Druhé směrování pro WinRM nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-134">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="5dfe5-135">Poskytuje žádnou kontrolu nad tím, kde se používají přihlašovací údaje, vytváření ohrožení zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-135">Provides no control over where credentials are used, creating a security vulnerability.</span></span>

## <a name="kerberos-constrained-delegation"></a><span data-ttu-id="5dfe5-136">Omezené delegování protokolu Kerberos</span><span class="sxs-lookup"><span data-stu-id="5dfe5-136">Kerberos constrained delegation</span></span>

<span data-ttu-id="5dfe5-137">Chcete-li druhý segment směrování můžete použít starší verzi omezené delegování (ne založené na prostředcích).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-137">You can use legacy constrained delegation (not resource-based) to make the second hop.</span></span>

><span data-ttu-id="5dfe5-138">**Poznámka:** účtů služby Active Directory, které mají **účet je citlivý a nelze jej delegovat** nastavenou vlastnost není možné delegovat.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-138">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="5dfe5-139">Další informace najdete v tématu [fokus zabezpečení: analyzování "Účet je citlivý a nelze jej delegovat" pro privilegované účty](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) a [nástroje pro ověřování protokolu Kerberos a nastavení](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="5dfe5-139">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="5dfe5-140">Výhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-140">Pros</span></span>

- <span data-ttu-id="5dfe5-141">Vyžaduje žádné speciální kódování</span><span class="sxs-lookup"><span data-stu-id="5dfe5-141">Requires no special coding</span></span>

### <a name="cons"></a><span data-ttu-id="5dfe5-142">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-142">Cons</span></span>

- <span data-ttu-id="5dfe5-143">Druhé směrování pro WinRM nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-143">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="5dfe5-144">Musí být nakonfigurovaná na objektu služby Active Directory vzdáleného serveru (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-144">Must be configured on the Active Directory object of the remote server (_ServerB_).</span></span>
- <span data-ttu-id="5dfe5-145">Je omezená na jednu doménu.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-145">Limited to one domain.</span></span> <span data-ttu-id="5dfe5-146">Nelze napříč doménami nebo doménovými strukturami.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-146">Cannot cross domains or forests.</span></span>
- <span data-ttu-id="5dfe5-147">Vyžaduje oprávnění aktualizovat objekty a hlavní názvy služby (SPN).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-147">Requires rights to update objects and Service Principal Names (SPNs).</span></span>

## <a name="resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="5dfe5-148">Založené na prostředcích omezené delegování protokolu Kerberos</span><span class="sxs-lookup"><span data-stu-id="5dfe5-148">Resource-based Kerberos constrained delegation</span></span>

<span data-ttu-id="5dfe5-149">Pomocí protokolu Kerberos založené na prostředcích, omezené delegování (zavedená ve Windows serveru 2012), konfigurace delegování přihlašovacích údajů na objekt serveru, kde jsou umístěny prostředky.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-149">Using resource-based Kerberos constrained delegation (introduced in Windows Server 2012), you configure credential delegation on the server object where resources reside.</span></span>
<span data-ttu-id="5dfe5-150">V druhém scénáři segment směrování je popsáno výše, nakonfigurujete _ServerC_ určit, kde bude přijímat delegovaný přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-150">In the second hop scenario described above, you configure _ServerC_ to specify from where it will accept delegated credentials.</span></span>

><span data-ttu-id="5dfe5-151">**Poznámka:** účtů služby Active Directory, které mají **účet je citlivý a nelze jej delegovat** nastavenou vlastnost není možné delegovat.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-151">**Note:** Active Directory accounts that have the **Account is sensitive and cannot be delegated** property set cannot be delegated.</span></span> <span data-ttu-id="5dfe5-152">Další informace najdete v tématu [fokus zabezpečení: analyzování "Účet je citlivý a nelze jej delegovat" pro privilegované účty](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) a [nástroje pro ověřování protokolu Kerberos a nastavení](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="5dfe5-152">For more information, see [Security Focus: Analysing 'Account is sensitive and cannot be delegated' for Privileged Accounts](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) and [Kerberos Authentication Tools and Settings](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)</span></span>

### <a name="pros"></a><span data-ttu-id="5dfe5-153">Výhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-153">Pros</span></span>

- <span data-ttu-id="5dfe5-154">Přihlašovací údaje se neukládají.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-154">Credentials are not stored.</span></span>
- <span data-ttu-id="5dfe5-155">Relativně jednoduchá konfigurace pomocí rutin prostředí PowerShell – žádné speciální kódování vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-155">Relatively easy to configure by using PowerShell cmdlets--no special coding required.</span></span>
- <span data-ttu-id="5dfe5-156">Je vyžadován přístup žádné speciální domény.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-156">No special domain access is required.</span></span>
- <span data-ttu-id="5dfe5-157">Funguje napříč doménami a doménovými strukturami.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-157">Works across domains and forests.</span></span>
- <span data-ttu-id="5dfe5-158">Kód Powershellu.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-158">PowerShell code.</span></span>

### <a name="cons"></a><span data-ttu-id="5dfe5-159">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-159">Cons</span></span>

- <span data-ttu-id="5dfe5-160">Vyžaduje systém Windows Server 2012 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-160">Requires Windows Server 2012 or later.</span></span>
- <span data-ttu-id="5dfe5-161">Druhé směrování pro WinRM nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-161">Does not support the second hop for WinRM.</span></span>
- <span data-ttu-id="5dfe5-162">Vyžaduje oprávnění aktualizovat objekty a hlavní názvy služby (SPN).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-162">Requires rights to update objects and Service Principal Names (SPNs).</span></span>

### <a name="example"></a><span data-ttu-id="5dfe5-163">Příklad</span><span class="sxs-lookup"><span data-stu-id="5dfe5-163">Example</span></span>

<span data-ttu-id="5dfe5-164">Podívejme se na příklad, který konfiguruje prostředků na základě omezené delegování Powershellu _ServerC_ umožňující delegovaná pověření z _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-164">Let's look at a PowerShell example that configures resource based constrained delegation on _ServerC_ to allow delegated credentials from a _ServerB_.</span></span>
<span data-ttu-id="5dfe5-165">Tento příklad předpokládá, že všechny servery se systémem Windows Server 2012 nebo novější, a aby existovala aspoň jeden řadič domény systému Windows Server 2012 každou doménu, pro kterou žádný ze serverů patří.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-165">This example assumes that all servers are running Windows Server 2012 or later, and that there is at least one Windows Server 2012 domain controller each domain to which any of the servers belong.</span></span>

<span data-ttu-id="5dfe5-166">Než budete moct nakonfigurovat omezené delegování, je nutné přidat `RSAT-AD-PowerShell` funkcí k instalaci modulu Powershellu pro Active Directory a následným importem tohoto modulu do relace:</span><span class="sxs-lookup"><span data-stu-id="5dfe5-166">Before you can configure constrained delegation, you must add the `RSAT-AD-PowerShell` feature to install the Active Directory PowerShell module, and then import that module into your session:</span></span>

```powershell
PS C:\> Add-WindowsFeature RSAT-AD-PowerShell

PS C:\> Import-Module ActiveDirectory
```
<span data-ttu-id="5dfe5-167">Teď máte několik dostupných rutin **PrincipalsAllowedToDelegateToAccount** parametr:</span><span class="sxs-lookup"><span data-stu-id="5dfe5-167">Several available cmdlets now have a **PrincipalsAllowedToDelegateToAccount** parameter:</span></span>

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

<span data-ttu-id="5dfe5-168">**PrincipalsAllowedToDelegateToAccount** parametr nastaví atributu objektu služby Active Directory **msDS-AllowedToActOnBehalfOfOtherIdentity**, který obsahuje seznam řízení přístupu (ACL), který Určuje, účty, které mají oprávnění k delegování přihlašovacích údajů k souvisejícímu účtu (v našem příkladu bude účet počítače pro _Server_).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-168">The **PrincipalsAllowedToDelegateToAccount** parameter sets the Active Directory object attribute **msDS-AllowedToActOnBehalfOfOtherIdentity**, which contains an access control list (ACL) that specifies which accounts have permission to delegate credentials to the associated account (in our example, it will be the machine account for _Server_).</span></span>

<span data-ttu-id="5dfe5-169">Nyní Pojďme vytvořit proměnné, použijeme k reprezentaci servery:</span><span class="sxs-lookup"><span data-stu-id="5dfe5-169">Now let's set up the variables we'll use to represent the servers:</span></span>

```powershell
# Set up variables for reuse
$ServerA = $env:COMPUTERNAME
$ServerB = Get-ADComputer -Identity ServerB
$ServerC = Get-ADComputer -Identity ServerC
```

<span data-ttu-id="5dfe5-170">Služba WinRM (a tedy vzdálené komunikace Powershellu) ve výchozím nastavení spustí jako účet počítače.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-170">WinRM (and therefore PowerShell remoting) runs as the computer account by default.</span></span> <span data-ttu-id="5dfe5-171">Tohle je vidět pohledem **%{StartName/** vlastnost `winrm` služby:</span><span class="sxs-lookup"><span data-stu-id="5dfe5-171">You can see this by looking at the **StartName** property of the `winrm` service:</span></span>

```powershell
PS C:\> Get-WmiObject win32_service -filter 'name="winrm"' | Format-List StartName

StartName : NT AUTHORITY\NetworkService
```

<span data-ttu-id="5dfe5-172">Pro _ServerC_ povolit delegování v relaci vzdálené komunikace Powershellu na _ServerB_, jsme udělí přístup tak, že nastavíte **PrincipalsAllowedToDelegateToAccount** parametr na _ServerC_ objekt počítače _ServerB_:</span><span class="sxs-lookup"><span data-stu-id="5dfe5-172">For _ServerC_ to allow delegation from a PowerShell remoting session on _ServerB_, we will grant access by setting the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to the computer object of _ServerB_:</span></span>

```powershell
# Grant resource-based Kerberos constrained delegation
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB

# Check the value of the attribute directly
$x = Get-ADComputer -Identity $ServerC -Properties msDS-AllowedToActOnBehalfOfOtherIdentity
$x.'msDS-AllowedToActOnBehalfOfOtherIdentity'.Access

# Check the value of the attribute indirectly
Get-ADComputer -Identity $ServerC -Properties PrincipalsAllowedToDelegateToAccount
```

<span data-ttu-id="5dfe5-173">Kerberos [Key Distribution Center (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) mezipaměti byl odepřen přístup pokusů (negativní mezipaměť) po dobu 15 minut.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-173">The Kerberos [Key Distribution Center (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) caches denied access attempts (negative cache) for 15 minutes.</span></span> <span data-ttu-id="5dfe5-174">Pokud _ServerB_ dříve pokusil o přístup k _ServerC_, budete muset vymazat mezipaměť na _ServerB_ zavoláním následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="5dfe5-174">If _ServerB_ has previously attempted to access _ServerC_, you will need to clear the cache on _ServerB_ by invoking the following command:</span></span>

```powershell
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {
    klist purge -li 0x3e7
}
```

<span data-ttu-id="5dfe5-175">Může také restartování počítače, nebo počkejte aspoň 15 minut a vymažte mezipaměť.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-175">You could also restart the computer, or wait at least 15 minutes to clear the cache.</span></span>

<span data-ttu-id="5dfe5-176">Po vymazání mezipaměti můžete úspěšně spustit kód z _Server_a_ prostřednictvím _ServerB_ k _ServerC_:</span><span class="sxs-lookup"><span data-stu-id="5dfe5-176">After clearing the cache, you can successfully run code from _ServerA_ through _ServerB_ to _ServerC_:</span></span>

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

<span data-ttu-id="5dfe5-177">V tomto příkladu `$using` proměnná slouží k Ujistěte se, `$ServerC` proměnná viditelná pro _ServerB_.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-177">In this example, the `$using` variable is used to make the `$ServerC` variable visible to _ServerB_.</span></span> <span data-ttu-id="5dfe5-178">Další informace o `$using` proměnné, viz [about_Remote_Variables](https://technet.microsoft.com/library/jj149005.aspx).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-178">For more information about the `$using` variable, see [about_Remote_Variables](https://technet.microsoft.com/library/jj149005.aspx).</span></span>

<span data-ttu-id="5dfe5-179">Povolit více serverů pro delegování přihlašovacích údajů k _ServerC_, nastavte hodnotu **PrincipalsAllowedToDelegateToAccount** parametru u _ServerC_ na pole:</span><span class="sxs-lookup"><span data-stu-id="5dfe5-179">To allow multiple servers to delegate credentials to _ServerC_, set the value of the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to an array:</span></span>

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

<span data-ttu-id="5dfe5-180">Pokud chcete, aby druhý segment směrování mezi doménami, přidejte plně kvalifikovaný název domény (FQDN) řadiče domény, domény, ke kterému _ServerB_ patří:</span><span class="sxs-lookup"><span data-stu-id="5dfe5-180">If you want to make the second hop across domains, add fully-qualified domain name (FQDN) of the domain controller of the domain to which _ServerB_ belongs:</span></span>

```powershell
# For ServerC in Contoso domain and ServerB in other domain
$ServerB = Get-ADComputer -Identity ServerB -Server dc1.alpineskihouse.com
$ServerC = Get-ADComputer -Identity ServerC
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB
```

<span data-ttu-id="5dfe5-181">Možnost delegování přihlašovacích údajů k ServerC odebrat, nastavte hodnotu **PrincipalsAllowedToDelegateToAccount** parametru u _ServerC_ k `$null`:</span><span class="sxs-lookup"><span data-stu-id="5dfe5-181">To remove the ability to delegate credentials to ServerC, set the value of the **PrincipalsAllowedToDelegateToAccount** parameter on _ServerC_ to `$null`:</span></span>

```powershell
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $null
```

### <a name="information-on-resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="5dfe5-182">Informace o založené na prostředcích omezené delegování protokolu Kerberos</span><span class="sxs-lookup"><span data-stu-id="5dfe5-182">Information on resource-based Kerberos constrained delegation</span></span>

- [<span data-ttu-id="5dfe5-183">Co je nového v ověřování protokolem Kerberos</span><span class="sxs-lookup"><span data-stu-id="5dfe5-183">What's New in Kerberos Authentication</span></span>](https://technet.microsoft.com/library/hh831747.aspx)
- [<span data-ttu-id="5dfe5-184">Jak Windows serveru 2012 usnadňuje bolest Kerberos omezeného delegování, část 1</span><span class="sxs-lookup"><span data-stu-id="5dfe5-184">How Windows Server 2012 Eases the Pain of Kerberos Constrained Delegation, Part 1</span></span>](https://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1)
- [<span data-ttu-id="5dfe5-185">Jak Windows serveru 2012 usnadňuje bolest Kerberos omezeného delegování, část 2</span><span class="sxs-lookup"><span data-stu-id="5dfe5-185">How Windows Server 2012 Eases the Pain of Kerberos Constrained Delegation, Part 2</span></span>](https://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-2)
- [<span data-ttu-id="5dfe5-186">Principy Kerberos omezeného delegování pro nasazení Proxy aplikací Azure Active Directory s ověřováním Windows integrované</span><span class="sxs-lookup"><span data-stu-id="5dfe5-186">Understanding Kerberos Constrained Delegation for Azure Active Directory Application Proxy Deployments with Integrated Windows Authentication</span></span>](https://aka.ms/kcdpaper)
- <span data-ttu-id="5dfe5-187">[[MS-ADA2]: Active Directory schématu atributů M2.210 atribut msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/library/hh554126.aspx)</span><span class="sxs-lookup"><span data-stu-id="5dfe5-187">[[MS-ADA2]: Active Directory Schema Attributes M2.210 Attribute msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/library/hh554126.aspx)</span></span>
- <span data-ttu-id="5dfe5-188">[[MS-SFU]: rozšíření protokolu Kerberos: Service for User a protokolu 1.3.2 S4U2proxy omezeného delegování](https://msdn.microsoft.com/library/cc246079.aspx)</span><span class="sxs-lookup"><span data-stu-id="5dfe5-188">[[MS-SFU]: Kerberos Protocol Extensions: Service for User and Constrained Delegation Protocol 1.3.2 S4U2proxy](https://msdn.microsoft.com/library/cc246079.aspx)</span></span>
- [<span data-ttu-id="5dfe5-189">Prostředek na základě protokolu Kerberos omezeného delegování</span><span class="sxs-lookup"><span data-stu-id="5dfe5-189">Resource Based Kerberos Constrained Delegation</span></span>](https://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)
- [<span data-ttu-id="5dfe5-190">Vzdálená správa bez použití PrincipalsAllowedToDelegateToAccount omezeného delegování</span><span class="sxs-lookup"><span data-stu-id="5dfe5-190">Remote Administration Without Constrained Delegation Using PrincipalsAllowedToDelegateToAccount</span></span>](https://blogs.msdn.microsoft.com/taylorb/2012/11/06/remote-administration-without-constrained-delegation-using-principalsallowedtodelegatetoaccount/)

## <a name="pssessionconfiguration-using-runas"></a><span data-ttu-id="5dfe5-191">PSSessionConfiguration pomocí RunAs</span><span class="sxs-lookup"><span data-stu-id="5dfe5-191">PSSessionConfiguration using RunAs</span></span>

<span data-ttu-id="5dfe5-192">Konfigurace relace můžete vytvořit na _ServerB_ a nastavte jeho **RunAsCredential** parametru.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-192">You can create a session configuration on _ServerB_ and set its **RunAsCredential** parameter.</span></span>

<span data-ttu-id="5dfe5-193">Informace o používání PSSessionConfiguration a spustit jako druhý segment směrování problém vyřešit, najdete v tématu [další řešení s více segmenty směrování vzdálené komunikace Powershellu](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-193">For information about using PSSessionConfiguration and RunAs to solve the second hop problem, see [Another solution to multi-hop PowerShell remoting](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).</span></span>

### <a name="pros"></a><span data-ttu-id="5dfe5-194">Výhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-194">Pros</span></span>

- <span data-ttu-id="5dfe5-195">Funguje s jakýmkoli serverem s WMF 3.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-195">Works with any server with WMF 3.0 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="5dfe5-196">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-196">Cons</span></span>

- <span data-ttu-id="5dfe5-197">Vyžaduje konfiguraci **PSSessionConfiguration** a **RunAs** na každém serveru zprostředkující (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-197">Requires configuration of **PSSessionConfiguration** and **RunAs** on every intermediate server (_ServerB_).</span></span>
- <span data-ttu-id="5dfe5-198">Vyžaduje heslo údržby, pokud používáte doménu **RunAs** účtu</span><span class="sxs-lookup"><span data-stu-id="5dfe5-198">Requires password maintenance when using a domain **RunAs** account</span></span>

## <a name="just-enough-administration-jea"></a><span data-ttu-id="5dfe5-199">Funkce Just Enough Administration (JEA)</span><span class="sxs-lookup"><span data-stu-id="5dfe5-199">Just Enough Administration (JEA)</span></span>

<span data-ttu-id="5dfe5-200">JEA umožňuje omezit, jaké příkazy můžete spustit správce během relace Powershellu.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-200">JEA allows you to restrict what commands an administrator can run during a PowerShell session.</span></span> <span data-ttu-id="5dfe5-201">Slouží k jejich vyřešení druhý segment směrování.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-201">It can be used to solve the second hop problem.</span></span>

<span data-ttu-id="5dfe5-202">Informace o JEA najdete v tématu [Just Enough Administration](https://docs.microsoft.com/powershell/jea/overview).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-202">For information about JEA, see [Just Enough Administration](https://docs.microsoft.com/powershell/jea/overview).</span></span>

### <a name="pros"></a><span data-ttu-id="5dfe5-203">Výhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-203">Pros</span></span>

- <span data-ttu-id="5dfe5-204">Žádná Údržba heslo při používání virtuální účet.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-204">No password maintenance when using a virtual account.</span></span>

### <a name="cons"></a><span data-ttu-id="5dfe5-205">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-205">Cons</span></span>

- <span data-ttu-id="5dfe5-206">Vyžaduje WMF 5.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-206">Requires WMF 5.0 or later.</span></span>
- <span data-ttu-id="5dfe5-207">Vyžaduje konfiguraci na každém serveru zprostředkující (_ServerB_).</span><span class="sxs-lookup"><span data-stu-id="5dfe5-207">Requires configuration on every intermediate server (_ServerB_).</span></span>

## <a name="pass-credentials-inside-an-invoke-command-script-block"></a><span data-ttu-id="5dfe5-208">Předávat přihlašovací údaje uvnitř bloku skriptu Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="5dfe5-208">Pass credentials inside an Invoke-Command script block</span></span>

<span data-ttu-id="5dfe5-209">Můžete předat pověření uvnitř **ScriptBlock** parametr volání [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) rutiny.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-209">You can pass credentials inside the **ScriptBlock** parameter of a call to the [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) cmdlet.</span></span>

### <a name="pros"></a><span data-ttu-id="5dfe5-210">Výhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-210">Pros</span></span>

- <span data-ttu-id="5dfe5-211">Nevyžaduje server zvláštní konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-211">Does not require special server configuration.</span></span>
- <span data-ttu-id="5dfe5-212">Funguje na jakémkoli serveru s WMF 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-212">Works on any server running WMF 2.0 or later.</span></span>

### <a name="cons"></a><span data-ttu-id="5dfe5-213">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="5dfe5-213">Cons</span></span>

- <span data-ttu-id="5dfe5-214">Vyžaduje techniku nevhodnou kódu.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-214">Requires an awkward code technique.</span></span>
- <span data-ttu-id="5dfe5-215">Pokud používáte WMF 2.0, vyžaduje jinou syntaxi pro předávání argumentů do vzdálené relace.</span><span class="sxs-lookup"><span data-stu-id="5dfe5-215">If running WMF 2.0, requires different syntax for passing arguments to a remote session.</span></span>

### <a name="example"></a><span data-ttu-id="5dfe5-216">Příklad</span><span class="sxs-lookup"><span data-stu-id="5dfe5-216">Example</span></span>

<span data-ttu-id="5dfe5-217">Následující příklad ukazuje, jak předávat přihlašovací údaje v **Invoke-Command** bloku skriptu:</span><span class="sxs-lookup"><span data-stu-id="5dfe5-217">The following example shows how to pass credentials in an **Invoke-Command** script block:</span></span>

```powershell
# This works without delegation, passing fresh creds
# Note $Using:Cred in nested request
$cred = Get-Credential Contoso\Administrator
Invoke-Command -ComputerName ServerB -Credential $cred -ScriptBlock {
    hostname
    Invoke-Command -ComputerName ServerC -Credential $Using:cred -ScriptBlock {hostname}
}
```

## <a name="see-also"></a><span data-ttu-id="5dfe5-218">Viz taky</span><span class="sxs-lookup"><span data-stu-id="5dfe5-218">See also</span></span>

[<span data-ttu-id="5dfe5-219">Aspekty zabezpečení vzdálené komunikace PowerShellu</span><span class="sxs-lookup"><span data-stu-id="5dfe5-219">PowerShell Remoting Security Considerations</span></span>](WinRMSecurity.md)