---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Spuštění Windows PowerShellu v předchozích verzích Windows"
ms.assetid: 57125436-3d1e-4e7f-b5c4-8f0ecb49d642
ms.openlocfilehash: 52e3acc1fd3009ecad3b7134008e38d4edfb5ca7
ms.sourcegitcommit: 18e3bfae83ffe282d3fd1a45f5386f3b7250f0c0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/08/2018
---
# <a name="starting-windows-powershell-on-earlier-versions-of-windows"></a>Spuštění Windows PowerShellu v předchozích verzích Windows
Tato část vysvětluje, jak spustit prostředí Windows PowerShell a Windows PowerShell Integrované skriptovací prostředí (ISE) v systému Windows® 7, Windows Server® 2008 R2 a Windows Server® 2008. Také vysvětluje, jak povolit volitelné funkce pro Windows PowerShell ISE v prostředí Windows PowerShell 2.0 na Windows Server® 2008 R2 a Windows Server® 2008.

Chcete-li nainstalovat prostředí Windows PowerShell 4.0 na podporovaných systémů, stáhněte a nainstalujte [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881). Další informace najdete v tématu [instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md).

Chcete-li nainstalovat prostředí Windows PowerShell 3.0 na podporovaných systémů, stáhněte a nainstalujte [Windows Management Framework 3.0](http://go.microsoft.com/fwlink/?LinkID=240290). Další informace najdete v tématu [instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md).

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a>Postup spuštění prostředí Windows PowerShell na starších verzích systému Windows
Ke spuštění nainstalovaná verze prostředí Windows PowerShell 3.0 nebo prostředí Windows PowerShell 4.0, kde je to možné, použijte některý z následujících metod.

#### <a name="from-the-start-menu"></a>Z nabídky Start

- Klikněte na tlačítko **spustit**, typ **prostředí PowerShell**a potom klikněte na **prostředí Windows PowerShell**.

- Z **spustit** nabídky, klikněte na tlačítko **spustit**, klikněte na tlačítko **všechny programy**, klikněte na tlačítko **Příslušenství**, klikněte na tlačítko **prostředí Windows PowerShell**  složku a pak klikněte na tlačítko **prostředí Windows PowerShell**.

#### <a name="at-the-command-prompt"></a>Na příkazovém řádku

- V Cmd.exe, prostředí Windows PowerShell nebo ISE Windows PowerShell spusťte prostředí Windows PowerShell, zadejte:

    ```
    PowerShell
    ```

    Můžete taky parametry programu PowerShell.exe přizpůsobit relace. Další informace najdete v tématu [Nápověda příkazového řádku PowerShell.exe](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).

#### <a name="with-administrative-privileges-run-as-administrator"></a>Pomocí správy oprávnění ("Spustit jako správce")

1. Klikněte na tlačítko **spustit**, typ **prostředí PowerShell**, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na **spustit jako správce**.

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a>Postup spuštění Windows PowerShell ISE na starších verzích systému Windows
Ke spuštění Windows PowerShell ISE, použijte některý z následujících metod.

#### <a name="from-the-start-menu"></a>Z nabídky Start

- Klikněte na tlačítko **spustit**, typ **ISE**a potom klikněte na **Windows PowerShell ISE**.

- Z **spustit** nabídky, klikněte na tlačítko **spustit**, klikněte na tlačítko **všechny programy**, klikněte na tlačítko **Příslušenství**, klikněte na tlačítko **prostředí Windows PowerShell**  složku a pak klikněte na tlačítko **Windows PowerShell ISE**.

#### <a name="at-the-command-prompt"></a>Na příkazovém řádku

- V Cmd.exe, prostředí Windows PowerShell nebo ISE Windows PowerShell spusťte prostředí Windows PowerShell, zadejte:

    ```
    PowerShell_ISE
    ```

    nebo

    ```
    ISE
    ```

#### <a name="with-administrative-privileges-run-as-administrator"></a>Pomocí správy oprávnění ("Spustit jako správce")

1. Klikněte na tlačítko **spustit**, typ **ISE**, klikněte pravým tlačítkem na **Windows PowerShell ISE**a potom klikněte na **spustit jako správce**.

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a>Postup povolení ISE Windows PowerShell na starších verzích systému Windows
V prostředí Windows PowerShell 4.0 a prostředí Windows PowerShell 3.0 je povoleno Windows PowerShell ISE ve výchozím nastavení ve všech verzích systému Windows. Pokud již není povolena, Windows Management Framework 4.0 nebo Windows Management Framework 3.0 povolí ho.

V prostředí Windows PowerShell 2.0 je povoleno Windows PowerShell ISE ve výchozím nastavení v systému Windows 7. Na Windows Server 2008 R2 a Windows Server 2008, je však volitelná funkce.

Pokud chcete povolit ISE Windows PowerShell v prostředí Windows PowerShell 2.0 na Windows Server 2008 R2 nebo Windows Server 2008, použijte následující postup.

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a>Chcete-li povolit Windows PowerShell Integrované skriptovací prostředí (ISE)

1. Spusťte Správce serveru.

2. Klikněte na tlačítko **funkce** a pak klikněte na **přidat funkce**.

3. V části Vybrat funkce klikněte na tlačítko Windows PowerShell Integrované skriptovací prostředí (ISE).

