---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Další užitečné skriptovací objekty
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: 0e87e9919199e011ab5abec5b07dccc8494ad64a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30949821"
---
# <a name="other-useful-scripting-objects"></a>Další užitečné skriptovací objekty

Následující objekty poskytují další skriptovací funkce v systému Windows PowerShell ISE. Nejsou součástí **$psISE** hierarchie.

## <a name="useful-scripting-objects"></a>Užitečné skriptování objekty

### <a name="psunsupportedconsoleapplications"></a>$psUnsupportedConsoleApplications

Existují určitá omezení na jak Windows PowerShell ISE komunikuje s konzolové aplikace. Příkaz nebo skriptu pro automatizaci, která vyžaduje zásah uživatele nemusí fungovat způsob, jakým funguje z konzoly pro prostředí Windows PowerShell. Můžete chtít blokovat těchto příkazů nebo skriptů v podokně Windows PowerShell ISE příkaz spouštět. **$PsUnsupportedConsoleApplications** objekt udržuje seznam těchto příkazů. Pokud se pokusíte spusťte příkazy v tomto seznamu, zobrazí zprávu, že nejsou podporovány. Následující skript přidá položku do seznamu.

```powershell
# List the unsupported commands
$psUnsupportedConsoleApplications

# Add a command to this list
$psUnsupportedConsoleApplications.Add('Mycommand')

# Show the augmented list of commands
$psUnsupportedConsoleApplications
```

### <a name="pslocalhelp"></a>$psLocalHelp

Toto je objekt slovník, který udržuje kontextová mapování mezi témata nápovědy a jejich přidružené odkazů v místním zkompilovaný soubor nápovědy HTML. Slouží k vyhledání místní Nápověda pro příslušné téma. Můžete přidat nebo odstranit témata z tohoto seznamu. Následující příklad kódu ukazuje několik příkladů páry klíč hodnota, které jsou obsaženy v **$psLocalHelp**.

```powershell
# See the local help map
$psLocalHelp | Format-List
```

### <a name="sample-output"></a>Ukázkový výstup

|||
|-|-|
|Klíč: Počítač|Value : WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm|
|Klíč: Obsah|Value : WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm|

Následující skript přidá položku do seznamu.

```powershell
$psLocalHelp.Add("get-myNoun", "c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a>$psOnlineHelp

Toto je objekt slovník, který udržuje kontextová mapování mezi názvy témat témat nápovědy a jejich přidružené externí adresy URL. Slouží k vyhledejte v nápovědě k příslušné téma na webu. Můžete přidat nebo odstranit témata z tohoto seznamu.

```powershell
$psOnlineHelp | Format-List
```

### <a name="sample-output"></a>Ukázkový výstup

|||
|-|-|
|Klíč: Počítač|Hodnota: http://go.microsoft.com/fwlink/p/?LinkID=135194|
|Klíč: Obsah|Hodnota: http://go.microsoft.com/fwlink/p/?LinkID=113278|

 Následující skript přidá položku do seznamu.

```powershell
$psOnlineHelp.Add("get-myNoun", "http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a>Viz také

- [Účelem ISE Windows PowerShell skriptování objektový Model](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)