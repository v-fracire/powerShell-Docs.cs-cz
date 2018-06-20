---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Spuštění Windows PowerShellu
ms.assetid: 59b649a2-c90c-4cf4-bf95-a740c59148e7
ms.openlocfilehash: b56ddc2f577225646729b99f3a2abcb8cc60d307
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953119"
---
# <a name="starting-windows-powershell"></a>Spuštění Windows PowerShellu
PowerShell je skriptovací modulu dll, která je integrována do více hostitelů.  Nejběžnější hostitele, který se spustí jsou interaktivního příkazového řádku PowerShell.exe a interaktivní PowerShell_ISE.exe prostředí skriptování.

Pokud chcete spustit Windows PowerShell® v systému Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012 a Windows 8, přečtěte si téma [běžné úlohy správy a navigace](http://technet.microsoft.com/library/hh831491.aspx).

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a>Postup spuštění prostředí Windows PowerShell na starších verzích systému Windows

Tato část vysvětluje, jak spustit prostředí Windows PowerShell a Windows PowerShell Integrované skriptovací prostředí (ISE) v systému Windows® 7, Windows Server® 2008 R2 a Windows Server® 2008. Také vysvětluje, jak povolit volitelné funkce pro Windows PowerShell ISE v prostředí Windows PowerShell 2.0 na Windows Server® 2008 R2 a Windows Server® 2008.

Ke spuštění nainstalovaná verze prostředí Windows PowerShell 3.0 nebo prostředí Windows PowerShell 4.0, kde je to možné, použijte některý z následujících metod.

#### <a name="from-the-start-menu"></a>Z nabídky Start

- Klikněte na tlačítko **spustit**, typ **prostředí PowerShell**a potom klikněte na **prostředí Windows PowerShell**.
- Z **spustit** nabídky, klikněte na tlačítko **spustit**, klikněte na tlačítko **všechny programy**, klikněte na tlačítko **Příslušenství**, klikněte na tlačítko **prostředí Windows PowerShell**  složku a pak klikněte na tlačítko **prostředí Windows PowerShell**.

#### <a name="at-the-command-prompt"></a>Na příkazovém řádku

V Cmd.exe, prostředí Windows PowerShell nebo ISE Windows PowerShell spusťte prostředí Windows PowerShell, zadejte:

```
PowerShell
```

Můžete taky parametry programu PowerShell.exe přizpůsobit relace. Další informace najdete v tématu [Nápověda příkazového řádku PowerShell.exe](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).

#### <a name="with-administrative-privileges-run-as-administrator"></a>Pomocí správy oprávnění ("Spustit jako správce")

Klikněte na tlačítko **spustit**, typ **prostředí PowerShell**, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na **spustit jako správce**.

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a>Postup spuštění Windows PowerShell ISE na starších verzích systému Windows

Ke spuštění Windows PowerShell ISE, použijte některý z následujících metod.

#### <a name="from-the-start-menu"></a>Z nabídky Start

- Klikněte na tlačítko **spustit**, typ **ISE**a potom klikněte na **Windows PowerShell ISE**.
- Z **spustit** nabídky, klikněte na tlačítko **spustit**, klikněte na tlačítko **všechny programy**, klikněte na tlačítko **Příslušenství**, klikněte na tlačítko **prostředí Windows PowerShell**  složku a pak klikněte na tlačítko **Windows PowerShell ISE**.

#### <a name="at-the-command-prompt"></a>Na příkazovém řádku

V Cmd.exe, prostředí Windows PowerShell nebo ISE Windows PowerShell spusťte prostředí Windows PowerShell, zadejte:

```
PowerShell_ISE
```

nebo

```
ISE
```

#### <a name="with-administrative-privileges-run-as-administrator"></a>Pomocí správy oprávnění ("Spustit jako správce")

Klikněte na tlačítko **spustit**, typ **ISE**, klikněte pravým tlačítkem na **Windows PowerShell ISE**a potom klikněte na **spustit jako správce**.

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a>Postup povolení ISE Windows PowerShell na starších verzích systému Windows

V prostředí Windows PowerShell 4.0 a prostředí Windows PowerShell 3.0 je povoleno Windows PowerShell ISE ve výchozím nastavení ve všech verzích systému Windows. Pokud již není povolena, Windows Management Framework 4.0 nebo Windows Management Framework 3.0 povolí ho.

V prostředí Windows PowerShell 2.0 je povoleno Windows PowerShell ISE ve výchozím nastavení v systému Windows 7. Na Windows Server 2008 R2 a Windows Server 2008, je však volitelná funkce.

Pokud chcete povolit ISE Windows PowerShell v prostředí Windows PowerShell 2.0 na Windows Server 2008 R2 nebo Windows Server 2008, použijte následující postup.

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a>Chcete-li povolit Windows PowerShell Integrované skriptovací prostředí (ISE)

1. Spusťte Správce serveru.
2. Klikněte na tlačítko **funkce** a pak klikněte na **přidat funkce**.
3. V části Vybrat funkce klikněte na tlačítko Windows PowerShell Integrované skriptovací prostředí (ISE).

## <a name="starting-the-32-bit-version-of-windows-powershell"></a>Spuštění 32bitové verze prostředí Windows PowerShell

Při instalaci prostředí Windows PowerShell na 64bitovém počítači **prostředí Windows PowerShell (x86)**, 32bitová verze prostředí Windows PowerShell je nainstalovaný kromě 64bitovou verzi. Při spuštění prostředí Windows PowerShell ve výchozím nastavení spustí 64bitovou verzi.

Však může někdy musíte spustit **prostředí Windows PowerShell (x86)**, například při použití modulu, který vyžaduje 32bitovou verzi nebo kdy se vzdáleně připojují k 32bitového počítače.

Spusťte 32bitovou verzi prostředí Windows PowerShell, použijte některý z následujících postupů.

#### <a name="in-windows-server-2012-r2"></a>In Windows Server® 2012 R2

- Na **spustit** zadejte **prostředí Windows PowerShell (x86)**. Klikněte **prostředí Windows PowerShell x86** dlaždici.
- V **správce serveru**, z **nástroje** nabídce vyberte možnost **prostředí Windows PowerShell (x86)**.
- Přesunutí kurzoru do pravého horního rohu klikněte na ploše **vyhledávání**, typ **prostředí PowerShell x86** a pak klikněte na **prostředí Windows PowerShell (x86)**.
- Prostřednictvím příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-server-2012"></a>In Windows Server® 2012

- Na **spustit** zadejte **prostředí PowerShell** a pak klikněte na **prostředí Windows PowerShell (x86)**.
- V **správce serveru**, z **nástroje** nabídce vyberte možnost **prostředí Windows PowerShell (x86)**.
- Přesunutí kurzoru do pravého horního rohu klikněte na ploše **vyhledávání**, typ **prostředí PowerShell** a pak klikněte na **prostředí Windows PowerShell (x86)**.
- Prostřednictvím příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-81"></a>V Windows® 8.1

- Na **spustit** zadejte **prostředí Windows PowerShell (x86)**. Klikněte **prostředí Windows PowerShell x86** dlaždici.
- Pokud používáte [nástrojů pro vzdálenou správu serveru](http://go.microsoft.com/fwlink/?LinkID=304145) pro Windows 8.1, můžete také otevřít prostředí Windows PowerShell x86 z **Server ManagerTools** nabídky.
  Vyberte **prostředí Windows PowerShell (x86)**.
- Přesunutí kurzoru do pravého horního rohu klikněte na ploše **vyhledávání**, typ **prostředí PowerShell x86** a pak klikněte na **prostředí Windows PowerShell (x86)**.
- Prostřednictvím příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-8"></a>V Windows® 8

- Na **spustit** obrazovky, přesuňte se ukazatelem do pravého horního rohu, klikněte na **nastavení**, klikněte na tlačítko **dlaždice**a poté přesuňte **zobrazit nástroje pro správu** jezdec na Ano. Poté zadejte **prostředí PowerShell** a klikněte na tlačítko **prostředí Windows PowerShell (x86)**.
- Pokud používáte [nástrojů pro vzdálenou správu serveru](http://www.microsoft.com/download/details.aspx?id=28972) pro systém Windows 8, můžete také otevřít prostředí Windows PowerShell x86 z **Server ManagerTools** nabídky. Vyberte **prostředí Windows PowerShell (x86)**.
- Na **spustit** obrazovky nebo plocha, zadejte **prostředí PowerShell (x86)** a pak klikněte na **prostředí Windows PowerShell (x86)**.
- Prostřednictvím příkazového řádku zadejte: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`