---
ms.date: 06/12/2017
keywords: jea, prostředí powershell, zabezpečení
title: JEA požadavky
ms.openlocfilehash: a5cf5519b30b24d44c12bdeedcf4cd763e2edbde
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="prerequisites"></a>Předpoklady

> Platí pro: prostředí Windows PowerShell 5.0

Právě dostatečně správy je funkce modulu pomocí prostředí Windows PowerShell 5.0 a vyšší.
Toto téma popisuje požadavky, které je nutné splnit, aby bylo možné začít používat JEA.

## <a name="install-jea"></a>Nainstalujte JEA

JEA je k dispozici v prostředí Windows PowerShell 5.0 a vyšší, ale pro plnou funkčnost se doporučuje nainstalovat nejnovější verzi prostředí PowerShell, které jsou k dispozici pro váš systém.
Následující tabulka popisuje dostupnost JEA je v systému Windows Server:

Serverový operační systém   | JEA dostupnosti
--------------------------|--------------------------------
Windows Server 2016       | Předinstalována
Windows Server 2012 R2    | Plnou funkčnost služby WMF 5.1
Windows Server 2012       | Plnou funkčnost služby WMF 5.1
Windows Server 2008 R2    | Snížená funkce<sup>1</sup> s WMF 5.1

Můžete taky JEA v počítači domácí nebo pracovní:

Klientský operační systém   | JEA dostupnosti
--------------------------|-----------------------------------------------------
Windows 10 1607+          | Předinstalována
Windows 10 1603, 1511     | Předinstalována, se snižuje funkce<sup>2</sup>
Windows 10 1507           | Nedostupné
Windows 8, 8.1            | Plnou funkčnost služby WMF 5.1
Windows 7                 | Snížená funkce<sup>1</sup> s WMF 5.1

<sup>1</sup> JEA nedá nakonfigurovat na použití skupinové účty spravované služby v systému Windows Server 2008 R2 nebo Windows 7.
Virtuální účty a další funkce JEA *jsou* podporována.

<sup>2</sup> Windows 10 verze 1511 a 1603 nepodporují následující funkce JEA: spuštěna jako skupinu spravovaný účet služby, pravidla podmíněného přístupu v konfigurace relace, jednotky uživatele a přidělit přístup k místní uživatelské účty.
Získat podporu pro tyto funkce, aktualizujte Windows verze 1607 (výročí aktualizace) nebo vyšší.

### <a name="check-which-version-of-powershell-is-installed"></a>Zkontrolujte nainstalované verze prostředí PowerShell

Chcete-li zkontrolovat, která verze prostředí PowerShell je nainstalovaná ve vašem systému, zkontrolujte `$PSVersionTable` proměnné v řádku prostředí Windows PowerShell.

```powershell
PS C:\> $PSVersionTable.PSVersion

Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

Budete chtít použít JEA, pokud *hlavní* verze je rovna nebo větší než **5**.
Pro dosažení co nejlepších výsledků a získat přístup k nejnovějším funkcím, doporučuje se upgradovat na verzi prostředí PowerShell **5.1** Pokud je to možné.

### <a name="install-windows-management-framework"></a>Nainstalovat Windows Management Framework

Pokud používáte starší verzi prostředí PowerShell, budete muset aktualizovat systém s nejnovější aktualizace služby Windows Management Framework (WMF).
Balíčky aktualizací a odkaz na nejnovější poznámky k verzi WMF jsou k dispozici v [Download Center](https://aka.ms/WMF5).

Důrazně doporučujeme, abyste otestovali vaše úlohy kompatibilitu s WMF před upgradem všech vašich serverů.

Uživatelé Windows 10 měli nainstalovat nejnovější aktualizace funkcí na aktuální verzi prostředí Windows PowerShell.

## <a name="enable-powershell-remoting"></a>Povolit vzdálenou komunikaci prostředí PowerShell

Vzdálená komunikace prostředí PowerShell poskytuje základ, na kterém je vytvořené JEA.
Je proto nutné zajistit povolena vzdálená komunikace PowerShell a [správně zabezpečené](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity) ve vašem systému, než budete moci použít JEA.

Ve výchozím nastavení v systému Windows Server 2012, 2012 R2 a 2016 je povolena vzdálená komunikace prostředí PowerShell.
Můžete povolit vzdálenou komunikaci prostředí PowerShell spuštěním následujícího příkazu v okně Powershellu se zvýšenými oprávněními.

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a>Povolit modul prostředí PowerShell a protokolování bloku skriptu (volitelné)

Následující postup povolení protokolování pro všechny akce prostředí PowerShell v systému.
Protokolování modulu PowerShell není vyžadován pro JEA, ale důrazně doporučujeme zapnout je zajistit, že uživatelé příkazy spouštět se protokolují v centrálním umístění.

Můžete nakonfigurovat pomocí zásad skupiny Zásady protokolování modulu prostředí PowerShell.

1. Otevřete Editor místních zásad skupiny na pracovní stanici nebo objektu zásad skupiny v konzole pro správu zásad skupiny na řadič domény služby Active Directory
2. Přejděte na **konfigurace počítače\\šablony pro správu\\součásti systému Windows\\prostředí Windows PowerShell**
3. Dvakrát klikněte na **zapnout protokolování modulu**
4. Klikněte na tlačítko **povoleno**
5. V části možnosti klikněte na **zobrazit** vedle názvy modulů
6. Typ "**\***" v zobrazeném okně. Tím se nastaví prostředí PowerShell k protokolování příkazy ze všech modulů.
7. Klikněte na tlačítko **OK** nastavit zásady
8. Dvakrát klikněte na **zapnout protokolování bloku skriptu prostředí PowerShell**
9. Klikněte na tlačítko **povoleno**
10. Klikněte na tlačítko **OK** nastavit zásady
11. (Na připojený k doméně počítače pouze) Spustit **gpupdate** nebo počkejte na zpracování aktualizované zásady a použít nastavení zásad skupiny

Můžete také povolit systémového prostředí PowerShell přepis prostřednictvím zásad skupiny.

## <a name="next-steps"></a>Další kroky

- [Vytvořte soubor schopnosti role](role-capabilities.md)
- [Vytvoření konfiguračního souboru relace](session-configurations.md)

## <a name="see-also"></a>Viz taky

- [Další informace o zabezpečení vzdálenou komunikaci prostředí PowerShell a WinRM](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity)
- [*Prostředí PowerShell ♥ týmem Blue* příspěvku na blogu na zabezpečení](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)