---
ms.date: 08/23/2017
keywords: rutiny prostředí PowerShell
title: řešení problémů s přístupem ve windows powershell web Accessu
ms.openlocfilehash: ef476d8e386e5380cb2c9dda69180dfce8748bf4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953442"
---
# <a name="troubleshooting-access-problems-in-windows-powershell-web-access"></a>Řešení problémů s přístupem ve Windows PowerShell Web Accessu

Aktualizace: 24 červen 2013 (revize 23 srpen 2017)

Platí pro: Windows Server 2012 R2, Windows Server 2012

V následujících částech identifikovat některé běžné problémy při pokusu o připojení ke vzdálenému počítači pomocí Windows PowerShell Web Access i návrhy na řešení problémů.

## <a name="sign-in-failure"></a>Chyba při přihlášení

Chyba může mít několik příčin.

- Autorizační pravidlo, které uživateli umožňuje přístup k počítači, nebo určitá konfigurace relace na vzdáleném počítači, která neexistuje.

  Zabezpečení Windows PowerShell Web Access je omezující; Uživatelé musí být výslovně udělený přístup ke vzdáleným počítačům pomocí autorizačních pravidel.

  Další informace o vytváření autorizačních pravidel najdete v tématu [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

- Uživatel nemá autorizovaný přístup k cílovému počítači. Ten je daný seznamy řízení přístupu (ACL).

  Další informace najdete v tématu [přihlášení k Windows PowerShell Web Access](use-the-web-based-windows-powershell-console.md#signing-in-to-windows-powershell-web-access), nebo Blog týmu Windows PowerShell.

- V cílovém počítači může být vypnutá Vzdálená správa prostředí Windows PowerShell.

  Ověřte, zda je Vzdálená správa povolená na počítači, ke kterému se uživatel pokouší připojit.

  Další informace najdete v tématu [konfigurace počítače pro vzdálenou komunikaci](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_remote_requirements#how-to-configure-your-computer-for-remoting).

## <a name="internal-server-error"></a>Vnitřní chyba serveru

Pokud se uživatelé k přihlášení do Windows PowerShell Web Access v okně Internet Exploreru, jsou uvedené **vnitřní chyba serveru** stránky, nebo *Internet Explorer* přestane reagovat.

Jde o specifický problém Internet Exploreru.

### <a name="possible-cause"></a>Možná příčina

Problém se může stát uživatelům, kteří se přihlašují pod názvem domény obsahujícím čínské znaky, nebo když je jeden nebo několik čínských znaků v názvu serveru brány.

#### <a name="workaround"></a>Alternativní řešení

1. [Nainstalujte a spusťte Internet Explorer 10](http://ie.microsoft.com/testdrive/info/downloads/Default.html)
1. Internet Exploreru změňte **režim dokumentu** nastavení *IE10* standardů.
   1. Stiskněte klávesu **F12** otevřete konzolu nástroje pro vývojáře
   1. V Internet Exploreru 10 klikněte na tlačítko **režim prohlížeče**a potom vyberte *Internet Explorer 10*.
   1. Klikněte na tlačítko **režim dokumentu**a potom klikněte na *IE10* standardů.
   1. Stiskněte klávesu **F12** zavřete konzolu nástroje pro vývojáře.
1. Zakažte automatickou konfiguraci serveru proxy v Internet Exploreru 10.
   1. Klikněte na tlačítko **nástroje**a potom klikněte na **Možnosti Internetu**.
   1. V **Možnosti Internetu** v dialogovém **připojení** , klikněte na **nastavení místní sítě**.
   1. Vymazat **automaticky zjišťovat nastavení** zaškrtávací políčko. Klikněte na tlačítko **OK**a potom klikněte na **OK** zavřete *Možnosti Internetu* dialogové okno.

## <a name="cannot-connect-to-a-remote-workgroup-computer"></a>Nejde se připojit ke vzdálenému počítači pracovní skupiny.

Pokud cílový počítač členem pracovní skupiny, použijte následující syntaxi zadejte uživatelské jméno a přihlaste se k počítači: `<workgroup_name>\<user_name>`

## <a name="cannot-find-web-server-iis-management-tools-even-though-the-role-was-installed"></a>Nejdou najít nástroje na správu Webového serveru (IIS), i když je role nainstalovaná.

Pokud jste nainstalovali pomocí Windows PowerShell Web Access `Install-WindowsFeature` rutiny, pokud nejsou nainstalovány nástroje správy `-IncludeManagementTools` je přidán parametr do rutiny.

Příklad, naleznete v části [instalace Windows PowerShell Web Accessu pomocí rutin prostředí Windows PowerShell](install-and-use-windows-powershell-web-access.md#to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets).

Můžete použít konzolu Správce služby IIS a další správu služby IIS nástroje, že potřebujete vybráním možnosti nástroje v **Průvodce přidáním rolí a funkcí** relace, který je zaměřený na serveru brány.
Přidat role a funkce Průvodce se otevře z ve Správci serveru.

## <a name="windows-powershell-web-access-website-is-not-accessible"></a>Windows PowerShell Web Access webu není dostupný

Pokud je konfigurace rozšířeného zabezpečení aplikace je povoleno v aplikaci Internet Explorer (IE ESC), můžete přidat do seznamu důvěryhodných serverů na webu Windows PowerShell Web Access.

Menší doporučený postup, z důvodu rizika zabezpečení, je IE ESC zakázat.
Můžete IE ESC zakázat na dlaždici vlastnosti na stránce místního serveru ve Správci serveru.

## <a name="an-authorization-failure-occurred-verify-that-you-are-authorized-to-connect-to-the-destination-computer"></a>Došlo k chybě autorizace. Ověřte, že máte oprávnění pro připojení k cílovému počítači.

Výše uvedené chybová zpráva se zobrazí při pokusu o připojení, když server brány je cílový počítač který je taky v pracovní skupině.

Pokud je server brány taky cílovým serverem a je v pracovní skupině, zadejte uživatelské jméno, název počítače a název skupiny uživatelů.
Nepoužívejte tečku (.) sám o sobě skutečného názvu počítače.

### <a name="scenarios-and-proper-values"></a>Scénáře a správné hodnoty

#### <a name="all-cases"></a>Všechny případy

Parametr | Hodnota
-- | --
UserName | Server\_name\\user\_name<br/>Localhost\\user\_name<br/>. \\uživatele\_název
UserGroup | Server\_name\\user\_group<br/>Localhost\\user\_group<br/>.\\user\_group
ComputerGroup | Server\_name\\computer\_group<br/>Localhost\\computer\_group<br/>. \\počítače\_skupiny

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

Identifikátor zabezpečení (SID) se zobrazí v autorizačním pravidle místo uživatele syntax\_název nebo počítače\_název.

Buď pravidlo už neplatí,nebo selhal dotaz do služby Active Directory Domain Services.
Autorizační pravidlo není obvykle ve scénářích, kdy byl v jednu chvíli v pracovní skupině server brány, ale později byl připojený k doméně

## <a name="cannot-sign-in-with-rule-as-an-ipv6-address-with-a-domain"></a>Nemůžete se přihlásit pomocí pravidla pomocí adresy IPv6 s doménou

Nejde se přihlásit k cílovému počítači, který byl v autorizačních pravidlech zadaný pomocí adresy IPv6 s doménou.

Autorizační pravidla nepodporují adresu IPv6, která má tvar názvu domény.

Pokud chcete k zadání cílového počítače použít adresu IPv6, použijte v autorizačním pravidle původní adresu IPv6 (která obsahuje dvojtečky).
Jako název cílového počítače, na přihlašovací stránce Windows PowerShell Web Access, ale není v autorizační pravidla jsou podporované doménové i číselné (s dvojtečkami) adresy IPv6.

Další informace o adresách IPv6 najdete v tématu [jak funguje IPv6](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx).

## <a name="see-also"></a>Viz také

- [Autorizační pravidla a funkce zabezpečení Windows PowerShell Web Accessu](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)
- [Použití konzole založené na webu Windows PowerShell](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)
- [about_Remote_Requirements](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_remote_requirements)