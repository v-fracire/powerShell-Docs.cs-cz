---
ms.date: 08/23/2017
keywords: rutiny prostředí PowerShell
title: řešení problémů s přístupem ve windows powershell web Accessu
ms.openlocfilehash: c9b98c7a1685679eb88b718de0351154cb84e92e
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320988"
---
# <a name="troubleshooting-access-problems-in-windows-powershell-web-access"></a><span data-ttu-id="2224a-103">Řešení problémů s přístupem ve Windows PowerShell Web Accessu</span><span class="sxs-lookup"><span data-stu-id="2224a-103">Troubleshooting Access Problems in Windows PowerShell Web Access</span></span>

<span data-ttu-id="2224a-104">Aktualizace: 24 červen 2013 (revize 23. srpna 2017)</span><span class="sxs-lookup"><span data-stu-id="2224a-104">Updated: June 24, 2013 (revised August 23, 2017)</span></span>

<span data-ttu-id="2224a-105">Platí pro: Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="2224a-105">Applies To: Windows Server 2012 R2, Windows Server 2012</span></span>

<span data-ttu-id="2224a-106">Následující části identifikovat některé běžné problémy při pokusu o připojení ke vzdálenému počítači pomocí Windows PowerShell Web Accessu a zahrnuje návrhy na řešení problémů.</span><span class="sxs-lookup"><span data-stu-id="2224a-106">The following sections identify some common problems when attempting to connect to a remote computer by using Windows PowerShell Web Access, and includes suggestions for resolving the problems.</span></span>

## <a name="sign-in-failure"></a><span data-ttu-id="2224a-107">Chyba při přihlášení</span><span class="sxs-lookup"><span data-stu-id="2224a-107">Sign-in failure</span></span>

<span data-ttu-id="2224a-108">Chyba může mít několik příčin.</span><span class="sxs-lookup"><span data-stu-id="2224a-108">Failure could occur because of any of the following.</span></span>

- <span data-ttu-id="2224a-109">Autorizační pravidlo, které uživateli umožňuje přístup k počítači, nebo určitá konfigurace relace na vzdáleném počítači, která neexistuje.</span><span class="sxs-lookup"><span data-stu-id="2224a-109">An authorization rule that allows the user access to the computer, or a specific session configuration on the remote computer, does not exist.</span></span>

  <span data-ttu-id="2224a-110">Zabezpečení Windows PowerShell Web Accessu je omezující; Uživatelé musí udělit přístup ke vzdáleným počítačům pomocí autorizačních pravidel.</span><span class="sxs-lookup"><span data-stu-id="2224a-110">Windows PowerShell Web Access security is restrictive; users must be granted explicit access to remote computers by using authorization rules.</span></span>

  <span data-ttu-id="2224a-111">Další informace o vytváření autorizačních pravidel najdete v tématu [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Accessu](authorization-rules-and-security-features-of-windows-powershell-web-access.md).</span><span class="sxs-lookup"><span data-stu-id="2224a-111">For more information about creating authorization rules, see [Authorization Rules and Security Features of Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).</span></span>

- <span data-ttu-id="2224a-112">Uživatel nemá autorizovaný přístup k cílovému počítači.</span><span class="sxs-lookup"><span data-stu-id="2224a-112">The user does not have authorized access to the destination computer.</span></span> <span data-ttu-id="2224a-113">Ten je daný seznamy řízení přístupu (ACL).</span><span class="sxs-lookup"><span data-stu-id="2224a-113">This is determined by access control lists (ACLs).</span></span>

  <span data-ttu-id="2224a-114">Další informace najdete v tématu [přihlášení k Windows PowerShell Web Accessu](use-the-web-based-windows-powershell-console.md#signing-in-to-windows-powershell-web-access), nebo Blog týmu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2224a-114">For more information, see [Signing in to Windows PowerShell Web Access](use-the-web-based-windows-powershell-console.md#signing-in-to-windows-powershell-web-access), or the Windows PowerShell Team Blog.</span></span>

- <span data-ttu-id="2224a-115">V cílovém počítači nemusí být povolená Vzdálená správa prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2224a-115">Windows PowerShell remote management might not be enabled on the destination computer.</span></span>

  <span data-ttu-id="2224a-116">Ověřte, zda je Vzdálená správa povolená na počítači, ke kterému se uživatel pokouší připojit.</span><span class="sxs-lookup"><span data-stu-id="2224a-116">Verify remote management is enabled on the computer to which the user is trying to connect.</span></span>

  <span data-ttu-id="2224a-117">Další informace najdete v tématu [konfigurace počítače pro vzdálenou komunikaci](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_remote_requirements#how-to-configure-your-computer-for-remoting).</span><span class="sxs-lookup"><span data-stu-id="2224a-117">For more information, see [How to Configure Your Computer for Remoting](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_remote_requirements#how-to-configure-your-computer-for-remoting).</span></span>

## <a name="internal-server-error"></a><span data-ttu-id="2224a-118">Vnitřní chyba serveru</span><span class="sxs-lookup"><span data-stu-id="2224a-118">Internal Server Error</span></span>

<span data-ttu-id="2224a-119">Co uživatelé vyzkouší pro přihlášení k Windows PowerShell Web Access v okně aplikace Internet Explorer, zobrazí se **vnitřní chyba serveru** stránky, nebo *aplikace Internet Explorer* přestane reagovat.</span><span class="sxs-lookup"><span data-stu-id="2224a-119">When users try to sign in to Windows PowerShell Web Access in an Internet Explorer window, they are shown an **Internal Server Error** page, or *Internet Explorer* stops responding.</span></span>

<span data-ttu-id="2224a-120">Jde o specifický problém Internet Exploreru.</span><span class="sxs-lookup"><span data-stu-id="2224a-120">This issue is specific to Internet Explorer.</span></span>

### <a name="possible-cause"></a><span data-ttu-id="2224a-121">Možná příčina</span><span class="sxs-lookup"><span data-stu-id="2224a-121">Possible cause</span></span>

<span data-ttu-id="2224a-122">Problém se může stát uživatelům, kteří se přihlašují pod názvem domény obsahujícím čínské znaky, nebo když je jeden nebo několik čínských znaků v názvu serveru brány.</span><span class="sxs-lookup"><span data-stu-id="2224a-122">This can occur for users who have signed in with a domain name that contains Chinese characters, or if one or more Chinese characters are part of the gateway server name.</span></span>

#### <a name="workaround"></a><span data-ttu-id="2224a-123">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="2224a-123">Workaround</span></span>

1. [<span data-ttu-id="2224a-124">Nainstalujte a spusťte Internet Explorer 10</span><span class="sxs-lookup"><span data-stu-id="2224a-124">Install and run Internet Explorer 10</span></span>](https://ie.microsoft.com/testdrive/info/downloads/Default.html)
1. <span data-ttu-id="2224a-125">Změna aplikace Internet Explorer **režim dokumentu** nastavení *aplikace Internet Explorer 10* standardy.</span><span class="sxs-lookup"><span data-stu-id="2224a-125">Change Internet Explorer **Document Mode** setting to *IE10* standards.</span></span>
   1. <span data-ttu-id="2224a-126">Stisknutím klávesy **F12** otevřete konzolu nástroje pro vývojáře</span><span class="sxs-lookup"><span data-stu-id="2224a-126">Press **F12** to open the Developer Tools console</span></span>
   1. <span data-ttu-id="2224a-127">V Internet Exploreru 10 klikněte na tlačítko **režim prohlížeče**a pak vyberte *aplikace Internet Explorer 10*.</span><span class="sxs-lookup"><span data-stu-id="2224a-127">In Internet Explorer 10, click **Browser Mode**, and then select *Internet Explorer 10*.</span></span>
   1. <span data-ttu-id="2224a-128">Klikněte na tlačítko **režim dokumentu**a potom klikněte na tlačítko *aplikace Internet Explorer 10* standardy.</span><span class="sxs-lookup"><span data-stu-id="2224a-128">Click **Document Mode**, and then click *IE10* standards.</span></span>
   1. <span data-ttu-id="2224a-129">Stisknutím klávesy **F12** zavřete konzolu nástroje pro vývojáře.</span><span class="sxs-lookup"><span data-stu-id="2224a-129">Press **F12** again to close the Developer Tools console.</span></span>
1. <span data-ttu-id="2224a-130">Zakažte automatickou konfiguraci serveru proxy v Internet Exploreru 10.</span><span class="sxs-lookup"><span data-stu-id="2224a-130">Disable automatic proxy configuration in Internet Explorer 10.</span></span>
   1. <span data-ttu-id="2224a-131">Klikněte na tlačítko **nástroje**a potom klikněte na tlačítko **Možnosti Internetu**.</span><span class="sxs-lookup"><span data-stu-id="2224a-131">Click **Tools**, and then click **Internet Options**.</span></span>
   1. <span data-ttu-id="2224a-132">V **Možnosti Internetu** dialogovém okně **připojení** klikněte na tlačítko **nastavení místní sítě**.</span><span class="sxs-lookup"><span data-stu-id="2224a-132">In the **Internet Options** dialog box, on the **Connections** tab, click **LAN settings**.</span></span>
   1. <span data-ttu-id="2224a-133">Zrušte **automaticky zjišťovat nastavení** zaškrtávací políčko.</span><span class="sxs-lookup"><span data-stu-id="2224a-133">Clear the **Automatically detect settings** check box.</span></span> <span data-ttu-id="2224a-134">Klikněte na tlačítko **OK**a potom klikněte na tlačítko **OK** zavřete *Možnosti Internetu* dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="2224a-134">Click **OK**, and then click **OK** again to close the *Internet Options* dialog box.</span></span>

## <a name="cannot-connect-to-a-remote-workgroup-computer"></a><span data-ttu-id="2224a-135">Nejde se připojit ke vzdálenému počítači pracovní skupiny.</span><span class="sxs-lookup"><span data-stu-id="2224a-135">Cannot connect to a remote workgroup computer</span></span>

<span data-ttu-id="2224a-136">Pokud cílový počítač je členem pracovní skupiny, zadejte uživatelské jméno a přihlaste se k počítači, použijte následující syntaxi: `<workgroup_name>\<user_name>`</span><span class="sxs-lookup"><span data-stu-id="2224a-136">If the destination computer is a member of a workgroup, use the following syntax to provide your user name and sign in to the computer: `<workgroup_name>\<user_name>`</span></span>

## <a name="cannot-find-web-server-iis-management-tools-even-though-the-role-was-installed"></a><span data-ttu-id="2224a-137">Nejdou najít nástroje na správu Webového serveru (IIS), i když je role nainstalovaná.</span><span class="sxs-lookup"><span data-stu-id="2224a-137">Cannot find Web Server (IIS) management tools, even though the role was installed</span></span>

<span data-ttu-id="2224a-138">Pokud jste nainstalovali Windows PowerShell Web Accessu pomocí `Install-WindowsFeature` rutiny, správy, pokud nejsou nainstalované nástroje `-IncludeManagementTools` parametru se přidá do rutiny.</span><span class="sxs-lookup"><span data-stu-id="2224a-138">If you installed Windows PowerShell Web Access by using the `Install-WindowsFeature` cmdlet, management tools are not installed unless the `-IncludeManagementTools` parameter is added to the cmdlet.</span></span>

<span data-ttu-id="2224a-139">Příklad najdete v tématu [instalace Windows PowerShell Web Accessu pomocí rutin prostředí Windows PowerShell](install-and-use-windows-powershell-web-access.md#to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets).</span><span class="sxs-lookup"><span data-stu-id="2224a-139">For an example, see [To install Windows PowerShell Web Access by using Windows PowerShell cmdlets](install-and-use-windows-powershell-web-access.md#to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets).</span></span>

<span data-ttu-id="2224a-140">Můžete přidat konzoly Správce služby IIS a nástroje pro správu jiných služby IIS, že potřebujete vybráním možnosti nástroje v **Průvodce přidání rolí a funkcí** relace, která je cílená na server brány.</span><span class="sxs-lookup"><span data-stu-id="2224a-140">You can add the IIS Manager console, and other IIS management tools that you need, by selecting the tools in an **Add Roles and Features Wizard** session that is targeted at the gateway server.</span></span>
<span data-ttu-id="2224a-141">Přidat role a funkce Průvodce je otevřena z v rámci správce serveru.</span><span class="sxs-lookup"><span data-stu-id="2224a-141">The Add Roles and Features Wizard is opened from within Server Manager.</span></span>

## <a name="windows-powershell-web-access-website-is-not-accessible"></a><span data-ttu-id="2224a-142">Windows PowerShell Web Accessu webu není dostupný</span><span class="sxs-lookup"><span data-stu-id="2224a-142">Windows PowerShell Web Access website is not accessible</span></span>

<span data-ttu-id="2224a-143">Pokud je povolená konfigurace rozšířeného zabezpečení aplikace Internet Explorer (IE ESC), můžete přidat na web Windows PowerShell Web Accessu do seznamu důvěryhodných webů.</span><span class="sxs-lookup"><span data-stu-id="2224a-143">If Enhanced Security Configuration is enabled in Internet Explorer (IE ESC), you can add the Windows PowerShell Web Access website to the list of trusted sites.</span></span>

<span data-ttu-id="2224a-144">Méně doporučený postup, kvůli ohrožení zabezpečení, je k zakázání IE ESC.</span><span class="sxs-lookup"><span data-stu-id="2224a-144">A less recommended approach, due to security risks, is to disable IE ESC.</span></span>
<span data-ttu-id="2224a-145">Zakázání IE ESC na dlaždici vlastnosti na stránce místního serveru ve Správci serveru.</span><span class="sxs-lookup"><span data-stu-id="2224a-145">You can disable IE ESC in the Properties tile on the Local Server page in Server Manager.</span></span>

## <a name="an-authorization-failure-occurred-verify-that-you-are-authorized-to-connect-to-the-destination-computer"></a><span data-ttu-id="2224a-146">Došlo k chybě autorizace.</span><span class="sxs-lookup"><span data-stu-id="2224a-146">An authorization failure occurred.</span></span> <span data-ttu-id="2224a-147">Ověřte, že máte oprávnění pro připojení k cílovému počítači.</span><span class="sxs-lookup"><span data-stu-id="2224a-147">Verify that you are authorized to connect to the destination computer.</span></span>

<span data-ttu-id="2224a-148">Při pokusu o připojení, pokud server brány je cílový počítač a je taky v pracovní skupině se zobrazí nad chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="2224a-148">The above error message is displayed while trying to connect when the gateway server is the destination computer, and is also in a workgroup.</span></span>

<span data-ttu-id="2224a-149">Pokud je server brány taky na cílový server a je v pracovní skupině, zadejte uživatelské jméno, název počítače a název skupiny uživatelů.</span><span class="sxs-lookup"><span data-stu-id="2224a-149">When the gateway server is also the destination server, and it is in a workgroup, specify the user name, computer name, and user group name.</span></span>
<span data-ttu-id="2224a-150">Nepoužívejte tečku (.) samostatně k skutečného názvu počítače.</span><span class="sxs-lookup"><span data-stu-id="2224a-150">Do not use a dot (.) by itself to represent the computer name.</span></span>

### <a name="scenarios-and-proper-values"></a><span data-ttu-id="2224a-151">Scénáře a odpovídajícími hodnotami</span><span class="sxs-lookup"><span data-stu-id="2224a-151">Scenarios and proper values</span></span>

#### <a name="all-cases"></a><span data-ttu-id="2224a-152">Všechny případy</span><span class="sxs-lookup"><span data-stu-id="2224a-152">All cases</span></span>

<span data-ttu-id="2224a-153">Parametr</span><span class="sxs-lookup"><span data-stu-id="2224a-153">Parameter</span></span> | <span data-ttu-id="2224a-154">Hodnota</span><span class="sxs-lookup"><span data-stu-id="2224a-154">Value</span></span>
-- | --
<span data-ttu-id="2224a-155">UserName</span><span class="sxs-lookup"><span data-stu-id="2224a-155">UserName</span></span> | <span data-ttu-id="2224a-156">Server\_name\\user\_name</span><span class="sxs-lookup"><span data-stu-id="2224a-156">Server\_name\\user\_name</span></span><br/><span data-ttu-id="2224a-157">Localhost\\user\_name</span><span class="sxs-lookup"><span data-stu-id="2224a-157">Localhost\\user\_name</span></span><br/><span data-ttu-id="2224a-158">. \\uživatele\_název</span><span class="sxs-lookup"><span data-stu-id="2224a-158">.\\user\_name</span></span>
<span data-ttu-id="2224a-159">UserGroup</span><span class="sxs-lookup"><span data-stu-id="2224a-159">UserGroup</span></span> | <span data-ttu-id="2224a-160">Server\_název\\uživatele\_skupiny</span><span class="sxs-lookup"><span data-stu-id="2224a-160">Server\_name\\user\_group</span></span><br/><span data-ttu-id="2224a-161">Localhost\\user\_group</span><span class="sxs-lookup"><span data-stu-id="2224a-161">Localhost\\user\_group</span></span><br/><span data-ttu-id="2224a-162">. \\uživatele\_skupiny</span><span class="sxs-lookup"><span data-stu-id="2224a-162">.\\user\_group</span></span>
<span data-ttu-id="2224a-163">ComputerGroup</span><span class="sxs-lookup"><span data-stu-id="2224a-163">ComputerGroup</span></span> | <span data-ttu-id="2224a-164">Server\_název\\počítače\_skupiny</span><span class="sxs-lookup"><span data-stu-id="2224a-164">Server\_name\\computer\_group</span></span><br/><span data-ttu-id="2224a-165">Localhost\\computer\_group</span><span class="sxs-lookup"><span data-stu-id="2224a-165">Localhost\\computer\_group</span></span><br/><span data-ttu-id="2224a-166">. \\počítače\_skupiny</span><span class="sxs-lookup"><span data-stu-id="2224a-166">.\\computer\_group</span></span>

#### <a name="gateway-server-is-in-a-domain"></a><span data-ttu-id="2224a-167">Server brány je v doméně.</span><span class="sxs-lookup"><span data-stu-id="2224a-167">Gateway server is in a domain</span></span>

<span data-ttu-id="2224a-168">Parametr</span><span class="sxs-lookup"><span data-stu-id="2224a-168">Parameter</span></span> | <span data-ttu-id="2224a-169">Hodnota</span><span class="sxs-lookup"><span data-stu-id="2224a-169">Value</span></span>
-- | --
<span data-ttu-id="2224a-170">ComputerName</span><span class="sxs-lookup"><span data-stu-id="2224a-170">ComputerName</span></span> | <span data-ttu-id="2224a-171">Plně kvalifikovaný název serveru brány nebo Localhost</span><span class="sxs-lookup"><span data-stu-id="2224a-171">Fully qualified name of gateway server, or Localhost</span></span>

#### <a name="gateway-server-is-in-a-workgroup"></a><span data-ttu-id="2224a-172">Server brány je v pracovní skupině.</span><span class="sxs-lookup"><span data-stu-id="2224a-172">Gateway server is in a workgroup</span></span>

<span data-ttu-id="2224a-173">Parametr</span><span class="sxs-lookup"><span data-stu-id="2224a-173">Parameter</span></span> | <span data-ttu-id="2224a-174">Hodnota</span><span class="sxs-lookup"><span data-stu-id="2224a-174">Value</span></span>
-- | --
<span data-ttu-id="2224a-175">ComputerName</span><span class="sxs-lookup"><span data-stu-id="2224a-175">ComputerName</span></span> | <span data-ttu-id="2224a-176">Název serveru</span><span class="sxs-lookup"><span data-stu-id="2224a-176">Server name</span></span>

### <a name="gateway-credentials"></a><span data-ttu-id="2224a-177">Přihlašovací údaje brány</span><span class="sxs-lookup"><span data-stu-id="2224a-177">Gateway credentials</span></span>

<span data-ttu-id="2224a-178">Přihlaste se k serveru brány jako cílový počítač. Použijte přihlašovací údaje v jednom z následujících formátů.</span><span class="sxs-lookup"><span data-stu-id="2224a-178">Sign in to a gateway server as target computer by using credentials formatted as one of the following.</span></span>

- <span data-ttu-id="2224a-179">Server\_name\\user\_name</span><span class="sxs-lookup"><span data-stu-id="2224a-179">Server\_name\\user\_name</span></span>
- <span data-ttu-id="2224a-180">Localhost\\user\_name</span><span class="sxs-lookup"><span data-stu-id="2224a-180">Localhost\\user\_name</span></span>
- <span data-ttu-id="2224a-181">. \\uživatele\_název</span><span class="sxs-lookup"><span data-stu-id="2224a-181">.\\user\_name</span></span>

## <a name="a-security-identifier-sid-is-displayed-in-an-authorization-rule"></a><span data-ttu-id="2224a-182">Zobrazí se v autorizačním pravidle identifikátor zabezpečení (SID)</span><span class="sxs-lookup"><span data-stu-id="2224a-182">A security identifier (SID) is displayed in an authorization rule</span></span>

<span data-ttu-id="2224a-183">Identifikátor zabezpečení (SID) se zobrazí v autorizačním pravidle místo na uživatele, syntaxe\_název nebo počítač platí následující\_název.</span><span class="sxs-lookup"><span data-stu-id="2224a-183">A security identifier (SID) is displayed in an authorization rule instead of the syntax user\_name/computer\_name.</span></span>

<span data-ttu-id="2224a-184">Buď pravidlo už neplatí,nebo selhal dotaz do služby Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="2224a-184">Either the rule is no longer valid, or the Active Directory Domain Services query failed.</span></span>
<span data-ttu-id="2224a-185">Autorizační pravidlo není obvykle ve scénářích, kdy server brány se v jednu chvíli v pracovní skupině, ale později byl připojený k doméně</span><span class="sxs-lookup"><span data-stu-id="2224a-185">An authorization rule is usually not valid in scenarios where the gateway server was at one time in a workgroup, but was later joined to a domain</span></span>

## <a name="cannot-sign-in-with-rule-as-an-ipv6-address-with-a-domain"></a><span data-ttu-id="2224a-186">Nemůžete se přihlásit pomocí pravidla jako adresu IPv6 s doménou</span><span class="sxs-lookup"><span data-stu-id="2224a-186">Cannot sign in with rule as an IPv6 address with a domain</span></span>

<span data-ttu-id="2224a-187">Nejde se přihlásit k cílovému počítači, který byl v autorizačních pravidlech zadaný pomocí adresy IPv6 s doménou.</span><span class="sxs-lookup"><span data-stu-id="2224a-187">Cannot sign in to a target computer that has been specified in authorization rules as an IPv6 address with a domain.</span></span>

<span data-ttu-id="2224a-188">Autorizační pravidla nepodporují adresu IPv6, která má tvar názvu domény.</span><span class="sxs-lookup"><span data-stu-id="2224a-188">Authorization rules do not support an IPv6 address in form of a domain name.</span></span>

<span data-ttu-id="2224a-189">Pokud chcete k zadání cílového počítače použít adresu IPv6, použijte v autorizačním pravidle původní adresu IPv6 (která obsahuje dvojtečky).</span><span class="sxs-lookup"><span data-stu-id="2224a-189">To specify a destination computer by using an IPv6 address, use the original IPv6 address (that contains colons) in the authorization rule.</span></span>
<span data-ttu-id="2224a-190">Jako název cílového počítače, na přihlašovací stránce Windows PowerShell Web Accessu, ale ne v autorizační pravidla jsou podporované tvaru doménové i číselné (s dvojtečkami) adresy IPv6.</span><span class="sxs-lookup"><span data-stu-id="2224a-190">Both domain and numerical (with colons) IPv6 addresses are supported as the target computer name on the Windows PowerShell Web Access sign-in page, but not in authorization rules.</span></span>

<span data-ttu-id="2224a-191">Další informace o adresách IPv6 najdete v tématu [jak funguje IPv6](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="2224a-191">For more information about IPv6 addresses, see [How IPv6 Works](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="2224a-192">Viz také</span><span class="sxs-lookup"><span data-stu-id="2224a-192">See Also</span></span>

- <span data-ttu-id="2224a-193">[Autorizační pravidla a funkce zabezpečení Windows PowerShell Web Accessu](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)</span><span class="sxs-lookup"><span data-stu-id="2224a-193">[Authorization Rules and Security Features of Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)</span></span>
- <span data-ttu-id="2224a-194">[Použití konzole založeného na webu Windows Powershellu](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)</span><span class="sxs-lookup"><span data-stu-id="2224a-194">[Use the Web-based Windows PowerShell Console](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)</span></span>
- [<span data-ttu-id="2224a-195">about_Remote_Requirements</span><span class="sxs-lookup"><span data-stu-id="2224a-195">about_Remote_Requirements</span></span>](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_remote_requirements)