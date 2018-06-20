---
ms.date: 06/12/2017
keywords: jea, prostředí powershell, zabezpečení
title: Přehled akorát správy
ms.openlocfilehash: 3dae8b31d4d13ff9033803035c870c02fc7c38ca
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34222084"
---
# <a name="just-enough-administration"></a>Just Enough Administration

Právě dostatečně správy (JEA) je technologie zabezpečení, která umožňuje delegované správy pro všechno, co, kterou je možné spravovat pomocí prostředí PowerShell.
JEA můžete:

- **Snižte počet správců na vašich počítačích** pomocí využívání virtuální účty nebo skupiny spravované účty služby, které provedení privilegovaných akcí jménem běžní uživatelé.
- **Omezit, které můžou uživatelé provádět** tak, že určíte, které rutiny, funkce a externí příkazy můžete spustit.
- **Lépe pochopit, co uživatelé dělají** s protokoly a přepisy, ukazují přesně který příkazy uživatel provést během jejich relace.

**Proč je to důležité?**

Vysoce privilegované účty, které se používají ke správě vašich serverů představovat závažné ohrožení zabezpečení.
By útočník ohrozit zabezpečení jedním z těchto účtů, může spuštění [pomoci odhalit laterální útoky](http://aka.ms/pth) celé organizaci.
Všechny účty, které mohou ohrozit jim můžete poskytnout přístup i více účtů a prostředků, jejich uvádění krok blíž ke krádeži tajné údaje o společnosti, spuštění útoku odmítnutí služby a další.

Není vždy snadno buď odeberte oprávnění správce.
Zvažte běžný scénář, kde je nainstalována DNS role ve stejném počítači jako řadiči domény služby Active Directory.
Správce DNS vyžadují oprávnění místního správce o vyřešení problémů se serverem DNS, ale aby bylo možné provést, abyste získali tak, aby byly členy vysoce privilegované skupiny zabezpečení "Domain Admins".
Tento přístup efektivně poskytuje Správci DNS kontrolu nad celé domény a přístup ke všem prostředkům na tomto počítači.

JEA pomůže vyřešit tento problém tak, že vám pomáhá přijmout Princip *nejnižší oprávnění*.
S JEA můžete nakonfigurovat koncový bod správy pro Správce DNS, kteří jim udělí přístup k všechny příkazy prostředí PowerShell, které potřebují k získání své práci, ale nic Další.
To znamená, zadejte odpovídající přístup k opravě poškozená po mezipaměť DNS nebo restartujte DNS server, aniž by nechtěně jim oprávnění ke službě Active Directory nebo procházet systému souborů nebo spouštění potenciálně nebezpečná skriptů.
Ještě lepší, pokud JEA relace je nakonfigurovaná pro použití dočasné privilegované účty virtuální, Správce DNS může připojit k serveru pomocí *bez oprávnění správce* přihlašovací údaje a přitom zachovat ke spuštění příkazů, které obvykle vyžadují. oprávnění správce.
Tato funkce umožňuje odebrat uživatele z role správce široce oprávněním místní nebo domény a místo toho pečlivě řídit co je to možné udělat na každém počítači.

## <a name="get-started-with-jea"></a>Začínáme s JEA

Můžete začít používat JEA dnes z jakéhokoli počítače se systémem Windows Server 2016 nebo Windows 10.
Můžete také spustit JEA ve starších operačních systémech Windows Management Framework aktualizace.
Další informace o požadavcích na používat JEA a naučte se vytvářet, používat a auditovat koncový bod JEA, projděte si následující témata:

- [Požadavky](prerequisites.md) -vysvětluje, jak používat JEA nastavení prostředí.
- [Funkce role](role-capabilities.md) -vysvětluje, jak vytvořit role, které určují, co uživatel může provádět v relaci JEA.
- [Konfigurace relace](session-configurations.md) -vysvětluje, jak nakonfigurovat JEA koncové body, které mapování uživatelů na role a nastavte JEA identity
- [Registrace JEA](register-jea.md) – vytvoření koncového bodu JEA a zpřístupnit uživatelům připojení k.
- [Pomocí JEA](using-jea.md) -další různé způsoby, kterými můžete JEA.
- [Aspekty zabezpečení](security-considerations.md) -zkontrolujte osvědčené postupy zabezpečení a důsledků JEA možnosti konfigurace.
- [Audit a tvorba sestav o JEA](audit-and-report.md) – zjistěte, jak auditovat a tvorba sestav o JEA koncové body.

## <a name="samples-and-dsc-resource"></a>Ukázky a prostředek DSC

Ukázka JEA konfigurace a prostředek JEA DSC najdete v [úložiště JEA GitHub](https://github.com/PowerShell/JEA).