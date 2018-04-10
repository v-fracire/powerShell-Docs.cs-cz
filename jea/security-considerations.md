---
ms.date: 06/12/2017
author: rpsqrd
ms.topic: conceptual
keywords: jea, prostředí powershell, zabezpečení
title: Aspekty zabezpečení JEA
ms.openlocfilehash: 1b83a73c047b056a4cc094d7e4b0bbf31f75f53a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="jea-security-considerations"></a>Aspekty zabezpečení JEA

> Platí pro: prostředí Windows PowerShell 5.0

JEA vám pomůže zlepšit lepšímu zabezpečení tím, že snižuje počet trvalých správců na vašich počítačích.
Dělá to tak tak, že vytvoříte nový vstupní bod pro uživatele pro správu systému (konfigurace relace prostředí PowerShell), který je ve výchozím nastavení, aby se zabránilo zneužití úzce uzamčena.
Uživatele, kteří potřebují některé, ale ne neomezený přístup ke koncovému bodu JEA můžete udělit přístup k počítači k provádění úloh správy.
Protože JEA umožňuje, aby se spouštěly správce příkazy přímo bez přístupu správce, můžete odebrat uživatele, pak z vysoce privilegované skupiny zabezpečení (ujistěte se, je standardní uživatelé).

Toto téma popisuje model zabezpečení JEA a osvědčené postupy podrobněji.

## <a name="run-as-account"></a>Účet Spustit jako

Každý koncový bod JEA má účet určený "Spustit jako", což je účet, pod kterým se provádějí akce připojování uživatelů.
Tento účet je konfigurovatelná v [relace konfigurační soubor](session-configurations.md), a zvolíte účet nemá významný vliv na zabezpečení váš koncový bod.

**Virtuální účty** jsou doporučeným způsobem konfigurace spustit jako účet.
Virtuální účty jsou jednorázové, dočasný místní účty, které jsou vytvořené pro je připojující se uživatel k použití během trvání relace jejich JEA.
Při jejich relace je ukončena, virtuální účet bude zrušen a již nelze použít.
Je připojující se uživatel nebude vědět, přihlašovací údaje pro virtuální účet a nemůže používat virtuální účet pro přístup k systému prostřednictvím jiným způsobem, jako je vzdálené plochy nebo koncový bod neomezeným prostředí PowerShell.

Ve výchozím nastavení virtuální účty patřit do místní skupiny administrators v počítači.
Díky tomu je úplná práva ke správě nic v systému, ale žádná práva ke správě prostředků v síti.
Při ověřování s jinými počítači, bude uživatelský kontext, účet místního počítače, není virtuální účet.

Řadiče domény představují zvláštní případ, protože neexistuje žádná koncepce místní skupiny administrators.
Místo toho virtuální účty patří do skupiny Domain Admins místo toho a můžete spravovat directory services na řadiči domény.
Identita domény je stále omezen na použít na řadiči domény, kde byla vytvořena instance relace JEA, a místo toho pochází z objektu počítače řadiče domény se zobrazí všechny přístup k síti.

V obou případech můžete také explicitně definovat, které virtuální účet musí patřit do skupiny zabezpečení.
To je vhodné, pokud úlohy, kterou provádíte jde provést bez oprávnění správce pro místní nebo domény.
Pokud už máte skupinu zabezpečení pro vaši správci definována, můžete jednoduše udělit členství virtuální účet do této skupiny jí přidělit oprávnění, která potřebuje.
Členství ve skupině virtuální účet je omezený na místní skupiny zabezpečení na pracovní stanici a členské servery, ale na řadiči domény lze pouze členy skupiny zabezpečení domény.
Jakmile zadáte jednu nebo více skupin zabezpečení pro virtuální účet patří, se už patří do výchozí skupiny (místní správce nebo správce domény).

Následující tabulka shrnuje možnosti možné konfigurace a výsledný oprávnění pro virtuální účty

Typ počítače                | Konfigurace skupiny virtuální účet | Kontext místní uživatele                                      | Kontext uživatele sítě
-----------------------------|-------------------------------------|---------------------------------------------------------|--------------------------------------------------
Řadič domény            | Výchozí                             | Uživatel domény, členem '*domény*\Domain Admins         | Účet počítače
Řadič domény            | Skupiny v doméně A a B               | Uživatel domény, členem '*domény*\A ','*domény*\B.       | Účet počítače
Členský server nebo pracovní stanice | Výchozí                             | Místního uživatele, členem '*BUILTIN*\Administrators.        | Účet počítače
Členský server nebo pracovní stanice | Místní skupiny C a D                | Místního uživatele, členem '*počítače*\C' a '*počítače*\D. | Účet počítače

Když se podíváte na události auditu zabezpečení a v protokolu událostí aplikace, zobrazí se, že každý JEA uživatelské relace má jedinečný virtuální účet.
To vám pomůže sledovat uživatele akce v koncový bod JEA zpět do původního uživatele, který spustil příkaz.
Virtuální účet názvy použijte formát "WinRM virtuální uživatelé\\WinRM\_VA\_*ACCOUNTNUMBER*\_*domény* \_ *sAMAccountName*"Pokud se uživatel"Alice"v doméně"Contoso"restartuje službu v koncový bod JEA, uživatelské jméno přidružené žádné události správce řízení služby by být například" WinRM virtuální uživatelé\\WinRM\_ VA\_1\_contoso\_alice ".


**Skupina účty spravované služby (Gmsa)** je užitečný v případě členský server musí mít přístup k síťovým prostředkům v relaci JEA.
Případ použití příkladu to je JEA koncový bod, který se používá k řízení přístupu k rozhraní REST API hostované na jiný počítač.
Je snadné k zápisu, aby požadované volání rozhraní API služby REST, ale aby bylo možné ověření pomocí rozhraní API funkce potřebujete síťové identity.
Pomocí účtu služby spravované skupiny umožňuje "druhé směrování" přitom stále má ovládací prvek, přes které počítače můžete použít účet.
Skutečná oprávnění gMSA jsou definovány pomocí skupin zabezpečení (místní nebo doménový), ke které patří k účtu gMSA.

Pokud koncový bod JEA je nakonfigurovaná pro použití účtu gMSA, se zobrazí akce všichni uživatelé JEA pocházet ze stejné skupiny účet spravované služby.
K identifikaci sadu příkazů, spusťte v relaci přepisu prostředí PowerShell je jediným způsobem, jak mohou sledovat akce zpět na konkrétního uživatele.

**Přihlašovací údaje průchodu přispívají** se používají, když jste nezadávejte spustit jako účet a chcete prostředí PowerShell použít přihlašovací údaje uživatele připojování ke spuštění příkazů na vzdáleném serveru.
Tato konfigurace je *není* nedoporučuje pro JEA, protože by vyžadují, abyste udělit připojování uživatelů přímý přístup ke skupinám pro správu privilegovaných.
Pokud je připojující se uživatel už má oprávnění správce, se mohou vyhnout JEA zcela a spravovat systému prostřednictvím znamená další, bez omezení.
O tom, najdete v části níže [JEA neposkytuje ochranu proti admins](#jea-does-not-protect-against-admins) Další informace.

**Standardní spustit jako účty** umožňují zadat libovolný uživatelský účet, pod kterým poběží celé relace prostředí PowerShell.
To je zásadní rozdíl, protože konfigurace relace nastavena na hodnotu použít pevné spustit jako účtu (s `-RunAsCredential` parametr) JEA neví.
To znamená, že definice rolí již nebude fungovat podle očekávání, a každý uživatel oprávnění pro přístup ke koncovému bodu se přiřadí na stejný atribut role.

Neměli byste používat RunAsCredential na koncový bod JEA z důvodu potíže v trasování akce zpět na konkrétní uživatele a nedostatečná podpora pro mapování uživatelů na role.

## <a name="winrm-endpoint-acl"></a>Koncový bod služby WinRM seznamu ACL

Jako s regulární koncových bodů vzdálenou komunikaci prostředí PowerShell, každý koncový bod JEA má seznam řízení samostatné přístupu (ACL) nastavit v konfiguraci WinRM, která určuje, kdo může ověřit s koncovým bodem JEA.
Pokud nesprávně nakonfigurována, důvěryhodní uživatelé nemusí mít přístup ke koncovému bodu JEA nebo nedůvěryhodné uživatelé mohou získat přístup.
Seznam ACL WinRM však neovlivňuje mapování uživatelům JEA role.
Která je řízena *RoleDefinitions* pole v konfiguračním souboru relace, který byl zaregistrován v systému.

Ve výchozím nastavení při registraci koncový bod JEA pomocí konfiguračního souboru relace a jeden nebo více možností role seznamu ACL WinRM nakonfigurují všichni uživatelé, mapování na jeden nebo více rolí přístup ke koncovému bodu.
Například relaci JEA nakonfigurovat pomocí následujících příkazů udělí úplný přístup k *CONTOSO\JEA\_Lev1* a *CONTOSO\JEA\_Lev2*.

```powershell
$roles = @{ 'CONTOSO\JEA_Lev1' = 'Lev1Role'; 'CONTOSO\JEA_Lev2' = 'Lev2Role' }
New-PSSessionConfigurationFile -Path '.\jea.pssc' -SessionType RestrictedRemoteServer -RoleDefinitions $roles -RunAsVirtualAccount
Register-PSSessionConfiguration -Path '.\jea.pssc' -Name 'MyJEAEndpoint'
```

Můžete auditovat oprávnění uživatele s [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) rutiny.

```powershell
PS C:\> Get-PSSessionConfiguration -Name 'MyJEAEndpoint' | Select-Object Permission

Permission
----------
CONTOSO\JEA_Lev1 AccessAllowed
CONTOSO\JEA_Lev2 AccessAllowed
```

Pokud chcete změnit, kteří uživatelé mají přístup, spusťte některý `Set-PSSessionConfiguration -Name 'MyJEAEndpoint' -ShowSecurityDescriptorUI` pro interaktivní výzvu nebo `Set-PSSessionConfiguration -Name 'MyJEAEndpoint' -SecurityDescriptorSddl <SDDL string>` aktualizovat oprávnění.
Uživatelé potřebovat aspoň *Invoke* práva pro přístup k JEA koncový bod.

Pokud dalším uživatelům udělen přístup ke koncovému bodu JEA, ale nepatří do kterékoli z těchto rolí definována v konfiguračním souboru relace, bude možné spustit relaci JEA však mít přístup pouze k rutiny výchozí.
Můžete auditovat oprávnění uživatele v koncový bod JEA spuštěním `Get-PSSessionCapability`.
Podívejte se [auditování a vytváření sestav na JEA](audit-and-report.md) článku Další informace o auditování, které příkazy uživatel má přístup k v koncový bod JEA.

## <a name="least-privilege-roles"></a>Nejnižší oprávnění role

Při navrhování JEA role, je důležité si pamatovat, že virtuální nebo skupiny spravované služby účet běžící na pozadí často má neomezený přístup ke správě místního počítače.
Funkce role JEA pomoci omezit, co tento účet slouží pro omezením příkazy a aplikace, které lze spouštět s využitím této privilegované kontextu.
Nesprávně navrženou rolí můžete povolit nebezpečná příkazy, pomocí které může umožnit uživateli rozdělit mimo hranice JEA nebo získat přístup k citlivé informace.

Zvažte například následující položku schopnosti role:

```powershell
@{
    VisibleCmdlets = 'Microsoft.PowerShell.Management\*-Process'
}
```

Tato možnost role umožňuje uživatelům umožní spouštět všechny rutiny prostředí PowerShell s podstatné jméno "Proces" z modulu Microsoft.PowerShell.Management.
Uživatelé mohou potřebovat přístup k rutiny jako `Get-Process` zjistit, co aplikace běží v systému a `Stop-Process` ukončit všechny zablokování aplikace.
Však tato položka také umožňuje `Start-Process`, který umožňuje spuštění libovolné aplikace s oprávněními správce s úplnými oprávněními.
Program nemusí být nainstalovány místně na serveru, tak nežádoucí osoba může jednoduše spustit program na sdílené složce, která poskytuje připojování uživatelská oprávnění místního správce, spustí malwaru a další. "

Bude vypadat bezpečnější verze tuto funkci stejné role:

```powershell
@{
    VisibleCmdlets = 'Microsoft.PowerShell.Management\Get-Process', 'Microsoft.PowerShell.Management\Stop-Process'
}
```

Vyhněte se použití zástupných znaků v možnosti role a nezapomeňte si [audit efektivní uživatelské oprávnění](audit-and-report.md#check-effective-rights-for-a-specific-user) pravidelně zjistit, které příkazy uživatel má přístup k.

## <a name="jea-does-not-protect-against-admins"></a>JEA neposkytuje ochranu proti admins

Jednou ze základních zásad JEA je, že umožňuje bez oprávnění správce k provedení *některé* úlohy správy.
JEA neposkytuje ochranu proti uživatelů, kteří již mají oprávnění správce.
Uživatelé patřící "domain admins," "místní správci," nebo jiných vysoce privilegovaných skupin ve vašem prostředí budou mít pořád povolený a vyhnout ochrany na JEA se po přihlášení k počítači prostřednictvím jinými prostředky.
Můžou, například, přihlaste se pomocí protokolu RDP, použít vzdálené konzoly MMC nebo připojení ke koncovým bodům neomezeným prostředí PowerShell.
Místní správci na serveru můžete také upravit JEA konfigurace, aby další uživatelé mohli spravovat systém nebo změna role schopnost rozšířit rozsah co dělat v jejich JEA relaci uživatele.
Proto je důležité vyhodnotit vaši uživatelé JEA rozšířené oprávnění k zobrazení, pokud existují další způsoby, se může získat oprávnění k přístupu do systému.

Běžnou praxí je pomocí JEA pravidelné každodenní údržby a máte "jenom v čase" privilegovaný přístup řešení pro správu povolit uživatelům dočasně stanou místní správci v případě nouze.
Díky tomu uživatelé nejsou trvalých správců systému, ale můžete získat tato práva, pokud a jenom v případě, po dokončení pracovního postupu, který dokumenty jejich používání těchto oprávnění.