---
ms.date: 06/12/2017
keywords: jea, powershell, zabezpečení
title: Požadavky na funkce JEA
ms.openlocfilehash: acc16c0c7eec357b621c0706a66b8752ae5578cd
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893031"
---
# <a name="prerequisites"></a>Předpoklady

> Platí pro: Windows PowerShell 5.0

Just Enough Administration je funkce zahrnuté pomocí Windows Powershellu 5.0 a vyšším.
Toto téma popisuje požadavky, které musí být splněny, aby bylo možné začít používat funkce JEA.

## <a name="install-jea"></a>Instalace funkce JEA

JEA je k dispozici pomocí Windows Powershellu 5.0 a vyšším, ale pro všechny funkce se doporučuje nainstalovat nejnovější verzi prostředí PowerShell, které jsou k dispozici pro váš systém.
Následující tabulka popisuje JEA na dostupnost ve Windows serveru:

Serverový operační systém   | Dostupnost funkce JEA
--------------------------|--------------------------------
Windows Server 2016       | Předinstalované
Windows Server 2012 R2    | Všechny funkce s WMF 5.1
Windows Server 2012       | Všechny funkce s WMF 5.1
Windows Server 2008 R2    | Funkčnost omezená<sup>1</sup> s WMF 5.1

Můžete také JEA domácí nebo pracovní počítače:

Klientský operační systém   | Dostupnost funkce JEA
--------------------------|-----------------------------------------------------
Windows 10 1607+          | Předinstalované
Windows 10 1603, 1511     | Předinstalované, s funkčnost omezená<sup>2</sup>
Windows 10 1507           | Nedostupné
Windows 8, 8.1            | Všechny funkce s WMF 5.1
Windows 7                 | Funkčnost omezená<sup>1</sup> s WMF 5.1

<sup>1</sup> JEA nedá nakonfigurovat na použití skupinové účty spravované služby v systému Windows Server 2008 R2 nebo Windows 7.
Virtuální účty a další funkce JEA *jsou* podporována.

<sup>2</sup> Windows 10 verze 1511 a 1603 nepodporuje následující funkce JEA: spuštění jako skupinu spravovaný účet služby, pravidla podmíněného přístupu v konfiguraci relace, uživatel jednotky a poskytnutí přístupu pro místní uživatelské účty.
Chcete-li získat podporu pro tyto funkce, aktualizaci Windows verze 1607 (Anniversary Update) nebo vyšší.

### <a name="check-which-version-of-powershell-is-installed"></a>Zkontrolujte, kterou verzi prostředí PowerShell je nainstalovaný.

Ke kontrole, kterou verzi prostředí PowerShell je nainstalovaný ve vašem systému, zkontrolujte, `$PSVersionTable` proměnné v příkazový řádek Windows Powershellu.

```powershell
$PSVersionTable.PSVersion
```

```output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

Jste připraveni používat funkce JEA, pokud *hlavní* verze je větší než nebo rovno **5**.
Pro dosažení co nejlepších výsledků a mít přístup k nejnovějším funkcím, doporučuje se, že upgradujete na verzi prostředí PowerShell **5.1** Pokud je to možné.

### <a name="install-windows-management-framework"></a>Nainstalujte Windows Management Framework

Pokud používáte starší verzi prostředí PowerShell, je potřeba aktualizovat váš systém pomocí nejnovější aktualizace Windows Management Frameworku (WMF).
Balíčky aktualizací a odkaz na nejnovější poznámky k verzi WMF jsou k dispozici v [Download Center](https://blogs.msdn.microsoft.com/powershell/2016/02/24/windows-management-framework-wmf-5-0-rtm-packages-has-been-republished/).

Důrazně doporučujeme, abyste otestovali kompatibilitu vašich úloh s WMF před provedením upgradu všech serverů.

Uživatelé Windows 10 nainstalujte nejnovější aktualizace funkcí k získání aktuální verze Windows Powershellu.

## <a name="enable-powershell-remoting"></a>Povolení vzdálené komunikace Powershellu

Vzdálenou komunikaci prostředí PowerShell poskytuje základ, na kterém je sestavena JEA.
Proto je nutné zajistit, je povolená Vzdálená komunikace prostředí PowerShell a [správně zabezpečená](/powershell/scripting/setup/winrmsecurity) ve vašem systému, abyste mohli používat JEA.

Ve výchozím nastavení systému Windows Server 2012, 2012 R2 a 2016 je povolená Vzdálená komunikace prostředí PowerShell.
Můžete povolit vzdálenou komunikaci prostředí PowerShell spuštěním následujícího příkazu v okně PowerShell se zvýšenými oprávněními.

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a>Povolit modul prostředí PowerShell a protokolování bloku skriptu (volitelné)

Následujícím postupem povolíte protokolování pro všechny akce prostředí PowerShell v systému.
Není vyžadováno pro JEA protokolování modulu prostředí PowerShell, ale důrazně doporučujeme zapnout je zajistit, že uživatelé příkazy spouštět se protokolují v centrálním umístění.

Můžete nakonfigurovat pomocí zásad skupiny Zásady protokolování modulu prostředí PowerShell.

1. Otevřete Editor místních zásad skupiny na pracovní stanici nebo objektu zásad skupiny v konzole pro správu zásad skupiny na řadič domény služby Active Directory
2. Přejděte do **konfigurace počítače\\šablony pro správu\\součásti Windows\\prostředí Windows PowerShell**
3. Dvakrát klikněte na **zapnout protokolování modulu**
4. Klikněte na tlačítko **povoleno**
5. V části Možnosti, klikněte na **zobrazit** vedle názvů modulů
6. Typ `\*` v zobrazeném okně. Toto dá pokyn k protokolování příkazy ze všech modulů Powershellu.
7. Klikněte na tlačítko **OK** nastavení zásad
8. Dvakrát klikněte na **zapnout protokolování bloku skriptu prostředí PowerShell**
9. Klikněte na tlačítko **povoleno**
10. Klikněte na tlačítko **OK** nastavení zásad
11. (Počítačích připojených k doméně jenom) Spustit `gpupdate` nebo počkejte na zpracování aktualizované zásady a použít nastavení zásad skupiny

Můžete také povolit přepis systémová Powershellu prostřednictvím zásad skupiny.

## <a name="next-steps"></a>Další kroky

[Vytvořte soubor funkce rolí](role-capabilities.md)

[Vytvoření konfiguračního souboru relace](session-configurations.md)

## <a name="see-also"></a>Viz taky

[Další informace o zabezpečení vzdálené komunikace Powershellu a WinRM](/powershell/scripting/setup/winrmsecurity)

[*Prostředí PowerShell ♥ modrý tým* blogový příspěvek o zabezpečení](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)