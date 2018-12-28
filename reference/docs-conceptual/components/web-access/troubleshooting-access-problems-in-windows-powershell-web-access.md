---
ms.date: 08/23/2017
keywords: rutiny prostředí PowerShell
title: řešení problémů s přístupem ve windows powershell web Accessu
ms.openlocfilehash: c9b98c7a1685679eb88b718de0351154cb84e92e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403719"
---
# <a name="troubleshooting-access-problems-in-windows-powershell-web-access"></a>Řešení problémů s přístupem ve Windows PowerShell Web Accessu

Aktualizováno: 24 červen 2013 (revize 23. srpna 2017)

Platí pro: Windows Server 2012 R2, Windows Server 2012

Následující části identifikovat některé běžné problémy při pokusu o připojení ke vzdálenému počítači pomocí Windows PowerShell Web Accessu a zahrnuje návrhy na řešení problémů.

## <a name="sign-in-failure"></a>Chyba při přihlášení

Chyba může mít několik příčin.

- Autorizační pravidlo, které uživateli umožňuje přístup k počítači, nebo určitá konfigurace relace na vzdáleném počítači, která neexistuje.

  Zabezpečení Windows PowerShell Web Accessu je omezující; Uživatelé musí udělit přístup ke vzdáleným počítačům pomocí autorizačních pravidel.

  Další informace o vytváření autorizačních pravidel najdete v tématu [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Accessu](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

- Uživatel nemá autorizovaný přístup k cílovému počítači. Ten je daný seznamy řízení přístupu (ACL).

  Další informace najdete v tématu [přihlášení k Windows PowerShell Web Accessu](use-the-web-based-windows-powershell-console.md#signing-in-to-windows-powershell-web-access), nebo Blog týmu Windows PowerShell.

- V cílovém počítači nemusí být povolená Vzdálená správa prostředí Windows PowerShell.

  Ověřte, zda je Vzdálená správa povolená na počítači, ke kterému se uživatel pokouší připojit.

  Další informace najdete v tématu [konfigurace počítače pro vzdálenou komunikaci](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_remote_requirements#how-to-configure-your-computer-for-remoting).

## <a name="internal-server-error"></a>Vnitřní chyba serveru

Co uživatelé vyzkouší pro přihlášení k Windows PowerShell Web Access v okně aplikace Internet Explorer, zobrazí se **vnitřní chyba serveru** stránky, nebo *aplikace Internet Explorer* přestane reagovat.

Jde o specifický problém Internet Exploreru.

### <a name="possible-cause"></a>Možná příčina

Problém se může stát uživatelům, kteří se přihlašují pod názvem domény obsahujícím čínské znaky, nebo když je jeden nebo několik čínských znaků v názvu serveru brány.

#### <a name="workaround"></a>Alternativní řešení

1. [Nainstalujte a spusťte Internet Explorer 10](https://ie.microsoft.com/testdrive/info/downloads/Default.html)
1. Změna aplikace Internet Explorer **režim dokumentu** nastavení *aplikace Internet Explorer 10* standardy.
   1. Stisknutím klávesy **F12** otevřete konzolu nástroje pro vývojáře
   1. V Internet Exploreru 10 klikněte na tlačítko **režim prohlížeče**a pak vyberte *aplikace Internet Explorer 10*.
   1. Klikněte na tlačítko **režim dokumentu**a potom klikněte na tlačítko *aplikace Internet Explorer 10* standardy.
   1. Stisknutím klávesy **F12** zavřete konzolu nástroje pro vývojáře.
1. Zakažte automatickou konfiguraci serveru proxy v Internet Exploreru 10.
   1. Klikněte na tlačítko **nástroje**a potom klikněte na tlačítko **Možnosti Internetu**.
   1. V **Možnosti Internetu** dialogovém okně **připojení** klikněte na tlačítko **nastavení místní sítě**.
   1. Zrušte **automaticky zjišťovat nastavení** zaškrtávací políčko. Klikněte na tlačítko **OK**a potom klikněte na tlačítko **OK** zavřete *Možnosti Internetu* dialogové okno.

## <a name="cannot-connect-to-a-remote-workgroup-computer"></a>Nejde se připojit ke vzdálenému počítači pracovní skupiny.

Pokud cílový počítač je členem pracovní skupiny, zadejte uživatelské jméno a přihlaste se k počítači, použijte následující syntaxi: `<workgroup_name>\<user_name>`

## <a name="cannot-find-web-server-iis-management-tools-even-though-the-role-was-installed"></a>Nejdou najít nástroje na správu Webového serveru (IIS), i když je role nainstalovaná.

Pokud jste nainstalovali Windows PowerShell Web Accessu pomocí `Install-WindowsFeature` rutiny, správy, pokud nejsou nainstalované nástroje `-IncludeManagementTools` parametru se přidá do rutiny.

Příklad najdete v tématu [instalace Windows PowerShell Web Accessu pomocí rutin prostředí Windows PowerShell](install-and-use-windows-powershell-web-access.md#to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets).

Můžete přidat konzoly Správce služby IIS a nástroje pro správu jiných služby IIS, že potřebujete vybráním možnosti nástroje v **Průvodce přidání rolí a funkcí** relace, která je cílená na server brány.
Přidat role a funkce Průvodce je otevřena z v rámci správce serveru.

## <a name="windows-powershell-web-access-website-is-not-accessible"></a>Windows PowerShell Web Accessu webu není dostupný

Pokud je povolená konfigurace rozšířeného zabezpečení aplikace Internet Explorer (IE ESC), můžete přidat na web Windows PowerShell Web Accessu do seznamu důvěryhodných webů.

Méně doporučený postup, kvůli ohrožení zabezpečení, je k zakázání IE ESC.
Zakázání IE ESC na dlaždici vlastnosti na stránce místního serveru ve Správci serveru.

## <a name="an-authorization-failure-occurred-verify-that-you-are-authorized-to-connect-to-the-destination-computer"></a>Došlo k chybě autorizace. Ověřte, že máte oprávnění pro připojení k cílovému počítači.

Při pokusu o připojení, pokud server brány je cílový počítač a je taky v pracovní skupině se zobrazí nad chybová zpráva.

Pokud je server brány taky na cílový server a je v pracovní skupině, zadejte uživatelské jméno, název počítače a název skupiny uživatelů.
Nepoužívejte tečku (.) samostatně k skutečného názvu počítače.

### <a name="scenarios-and-proper-values"></a>Scénáře a odpovídajícími hodnotami

#### <a name="all-cases"></a>Všechny případy

Parametr | Hodnota
-- | --
UserName | Server\_name\\user\_name<br/>Localhost\\user\_name<br/>. \\uživatele\_název
UserGroup | Server\_název\\uživatele\_skupiny<br/>Localhost\\user\_group<br/>. \\uživatele\_skupiny
ComputerGroup | Server\_název\\počítače\_skupiny<br/>Localhost\\computer\_group<br/>. \\počítače\_skupiny

#### <a name="gateway-server-is-in-a-domain"></a>Server brány je v doméně.

Parametr | Hodnota
-- | --
ComputerName | Plně kvalifikovaný název serveru brány nebo Localhost

#### <a name="gateway-server-is-in-a-workgroup"></a>Server brány je v pracovní skupině.

Parametr | Hodnota
-- | --
ComputerName | Název serveru

### <a name="gateway-credentials"></a>Přihlašovací údaje brány

Přihlaste se k serveru brány jako cílový počítač. Použijte přihlašovací údaje v jednom z následujících formátů.

- Server\_name\\user\_name
- Localhost\\user\_name
- . \\uživatele\_název

## <a name="a-security-identifier-sid-is-displayed-in-an-authorization-rule"></a>Zobrazí se v autorizačním pravidle identifikátor zabezpečení (SID)

Identifikátor zabezpečení (SID) se zobrazí v autorizačním pravidle místo na uživatele, syntaxe\_název nebo počítač platí následující\_název.

Buď pravidlo už neplatí,nebo selhal dotaz do služby Active Directory Domain Services.
Autorizační pravidlo není obvykle ve scénářích, kdy server brány se v jednu chvíli v pracovní skupině, ale později byl připojený k doméně

## <a name="cannot-sign-in-with-rule-as-an-ipv6-address-with-a-domain"></a>Nemůžete se přihlásit pomocí pravidla jako adresu IPv6 s doménou

Nejde se přihlásit k cílovému počítači, který byl v autorizačních pravidlech zadaný pomocí adresy IPv6 s doménou.

Autorizační pravidla nepodporují adresu IPv6, která má tvar názvu domény.

Pokud chcete k zadání cílového počítače použít adresu IPv6, použijte v autorizačním pravidle původní adresu IPv6 (která obsahuje dvojtečky).
Jako název cílového počítače, na přihlašovací stránce Windows PowerShell Web Accessu, ale ne v autorizační pravidla jsou podporované tvaru doménové i číselné (s dvojtečkami) adresy IPv6.

Další informace o adresách IPv6 najdete v tématu [jak funguje IPv6](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx).

## <a name="see-also"></a>Viz také

- [Autorizační pravidla a funkce zabezpečení Windows PowerShell Web Accessu](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)
- [Použití konzole založeného na webu Windows Powershellu](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)
- [about_Remote_Requirements](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_remote_requirements)