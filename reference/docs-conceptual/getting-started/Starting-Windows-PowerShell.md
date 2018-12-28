---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Spuštění Windows PowerShellu
ms.assetid: 59b649a2-c90c-4cf4-bf95-a740c59148e7
ms.openlocfilehash: 9184e8b0e508610e7f4775f1032f3a69c93bb8c1
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403859"
---
# <a name="starting-windows-powershell"></a>Spuštění Windows PowerShellu
PowerShell je skriptovací modul dll, která je součástí několika hostitelích.  Nejběžnější hostitele, bude zahájena jsou interaktivního příkazového řádku PowerShell.exe a interaktivní prostředí PowerShell_ISE.exe skriptování.

Spusťte Windows PowerShell® na Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012 a Windows 8, naleznete v tématu [běžné úlohy správy a navigace](https://technet.microsoft.com/library/hh831491.aspx).

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a>Postup spuštění prostředí Windows PowerShell na starších verzích Windows

Tato část vysvětluje, jak spustit prostředí Windows PowerShell a Windows Powershellu integrovaném skriptovacím prostředí (ISE) ve Windows® 7, Windows Server® 2008 R2 a Windows Server® 2008. Také vysvětluje, jak povolit volitelné funkce pro Windows PowerShell ISE Windows PowerShell 2.0 na Windows Server® 2008 R2 a Windows Server® 2008.

Použijte některou z následujících metod spustit nainstalovanou verzi Windows PowerShell 3.0 nebo Windows PowerShell 4.0, kde je to možné.

#### <a name="from-the-start-menu"></a>Z nabídky Start

- Klikněte na tlačítko **Start**, typ **PowerShell**a potom klikněte na tlačítko **prostředí Windows PowerShell**.
- Z **Start** nabídky, klikněte na tlačítko **Start**, klikněte na tlačítko **všechny programy**, klikněte na tlačítko **Příslušenství**, klikněte na tlačítko **prostředí Windows PowerShell**  složku a pak klikněte na tlačítko **prostředí Windows PowerShell**.

#### <a name="at-the-command-prompt"></a>Na příkazovém řádku

Do pole Cmd.exe, prostředí Windows PowerShell nebo ISE Windows PowerShell spusťte prostředí Windows PowerShell, zadejte:

```
PowerShell
```

Parametry programu PowerShell.exe můžete také použít k přizpůsobení relace. Další informace najdete v tématu [Nápověda příkazového řádku pro PowerShell.exe](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).

#### <a name="with-administrative-privileges-run-as-administrator"></a>Pomocí správy oprávnění ("Spustit jako správce")

Klikněte na tlačítko **Start**, typ **PowerShell**, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na tlačítko **spustit jako správce**.

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a>Postup spuštění Windows PowerShell ISE na starších verzích Windows

Použijte některý z následujících metod ke spuštění Windows PowerShell ISE.

#### <a name="from-the-start-menu"></a>Z nabídky Start

- Klikněte na tlačítko **Start**, typ **ISE**a potom klikněte na tlačítko **Windows PowerShell ISE**.
- Z **Start** nabídky, klikněte na tlačítko **Start**, klikněte na tlačítko **všechny programy**, klikněte na tlačítko **Příslušenství**, klikněte na tlačítko **prostředí Windows PowerShell**  složku a pak klikněte na tlačítko **Windows PowerShell ISE**.

#### <a name="at-the-command-prompt"></a>Na příkazovém řádku

Do pole Cmd.exe, prostředí Windows PowerShell nebo ISE Windows PowerShell spusťte prostředí Windows PowerShell, zadejte:

```
PowerShell_ISE
```

nebo

```
ISE
```

#### <a name="with-administrative-privileges-run-as-administrator"></a>Pomocí správy oprávnění ("Spustit jako správce")

Klikněte na tlačítko **Start**, typ **ISE**, klikněte pravým tlačítkem na **Windows PowerShell ISE**a potom klikněte na tlačítko **spustit jako správce**.

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a>Jak povolit ISE Windows PowerShell na starších verzích Windows

Ve Windows Powershellu 4.0 a Windows PowerShell 3.0 je Windows PowerShell ISE povolena ve výchozím nastavení ve všech verzích Windows. Pokud ještě není povolené, Windows Management Framework 4.0 nebo Windows Management Framework 3.0 povolí ho.

V rozhraní Windows PowerShell 2.0 je Windows PowerShell ISE povolena ve výchozím nastavení ve Windows 7. V systému Windows Server 2008 R2 a Windows Server 2008, je však volitelná funkce.

Pokud chcete povolit Windows PowerShell ISE Windows PowerShell 2.0 na Windows Server 2008 R2 nebo Windows Server 2008, pomocí následujícího postupu.

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a>Povolit Windows Powershellu integrovaném skriptovacím prostředí (ISE)

1. Spusťte Správce serveru.
2. Klikněte na tlačítko **funkce** a potom klikněte na tlačítko **přidat funkce**.
3. V části Vybrat funkce klikněte na Windows Powershellu integrovaném skriptovacím prostředí (ISE).

## <a name="starting-the-32-bit-version-of-windows-powershell"></a>Spuštění 32bitové verze Windows Powershellu

Při instalaci prostředí Windows PowerShell na 64bitovém počítači **prostředí Windows PowerShell (x86)**, kromě 64bitovou verzi je nainstalovaná 32bitová verze Windows powershellu. Při spuštění prostředí Windows PowerShell ve výchozím nastavení spustí 64bitovou verzi.

Však můžete někdy potřebovat ke spuštění **prostředí Windows PowerShell (x86)**, například při použití modulu, který vyžaduje 32bitovou verzi nebo kdy se vzdáleně připojují k 32bitového počítače.

Pokud chcete spustit 32bitovou verzi Windows powershellu, použijte některý z následujících postupů.

#### <a name="in-windows-server-2012-r2"></a>Ve Windows Server® 2012 R2

- Na **Start** zadejte **prostředí Windows PowerShell (x86)**. Klikněte na tlačítko **prostředí Windows PowerShell x86** dlaždici.
- V **správce serveru**, z **nástroje** nabídce vyberte možnost **prostředí Windows PowerShell (x86)**.
- Přesunutí kurzoru v pravém horním rohu klikněte na ploše **hledání**, typ **PowerShell x86** a potom klikněte na tlačítko **prostředí Windows PowerShell (x86)**.
- Pomocí příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-server-2012"></a>V Windows Server® 2012

- Na **Start** zadejte **PowerShell** a potom klikněte na tlačítko **prostředí Windows PowerShell (x86)**.
- V **správce serveru**, z **nástroje** nabídce vyberte možnost **prostředí Windows PowerShell (x86)**.
- Přesunutí kurzoru v pravém horním rohu klikněte na ploše **hledání**, typ **Powershellu** a potom klikněte na tlačítko **prostředí Windows PowerShell (x86)**.
- Pomocí příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-81"></a>V Windows® 8.1

- Na **Start** zadejte **prostředí Windows PowerShell (x86)**. Klikněte na tlačítko **prostředí Windows PowerShell x86** dlaždici.
- Pokud používáte [nástroje pro vzdálenou správu serveru](https://go.microsoft.com/fwlink/?LinkID=304145) pro Windows 8.1, můžete také otevřít prostředí Windows PowerShell x86 z **Server ManagerTools** nabídky.
  Vyberte **prostředí Windows PowerShell (x86)**.
- Přesunutí kurzoru v pravém horním rohu klikněte na ploše **hledání**, typ **PowerShell x86** a potom klikněte na tlačítko **prostředí Windows PowerShell (x86)**.
- Pomocí příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-8"></a>V Windows® 8

- Na **Start** obrazovky, přesuňte kurzor na pravém horním rohu, klikněte na tlačítko **nastavení**, klikněte na tlačítko **dlaždice**a poté přesuňte **zobrazit nástroje pro správu** posuvník na hodnotu Ano. Potom zadejte **PowerShell** a klikněte na tlačítko **prostředí Windows PowerShell (x86)**.
- Pokud používáte [nástroje pro vzdálenou správu serveru](https://www.microsoft.com/download/details.aspx?id=28972) pro systém Windows 8, můžete také otevřít prostředí Windows PowerShell x86 z **Server ManagerTools** nabídky. Vyberte **prostředí Windows PowerShell (x86)**.
- Na **Start** obrazovky nebo stolní počítač, zadejte **PowerShell (x86)** a potom klikněte na tlačítko **prostředí Windows PowerShell (x86)**.
- Pomocí příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`