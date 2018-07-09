---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Další užitečné skriptovací objekty
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: 2ae9bc1864daedbcb0070c5f3862a6c98f8db2d4
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893276"
---
# <a name="other-useful-scripting-objects"></a>Další užitečné skriptovací objekty

Následující objekty poskytují další funkce skriptování v prostředí Windows PowerShell ISE. Nejsou součástí **$psISE** hierarchie.

## <a name="useful-scripting-objects"></a>Užitečné objekty skriptování

### <a name="psunsupportedconsoleapplications"></a>$psUnsupportedConsoleApplications

Existují určitá omezení pro interakci Windows PowerShell ISE pomocí konzolové aplikace. Příkaz nebo automatizační skript, který vyžaduje zásah uživatele nemusí fungovat způsob, jakým funguje v konzole Windows Powershellu. Můžete chtít blokovat útoky DoS tyto příkazy nebo skripty v aplikaci Windows PowerShell ISE příkazového podokna. **$PsUnsupportedConsoleApplications** objektu udržuje seznam těchto příkazů. Pokud se pokusíte spustit příkazy v tomto seznamu, dostanete zprávu, že se nepodporují. Následující skript přidá položku do seznamu.

```powershell
# List the unsupported commands
$psUnsupportedConsoleApplications

# Add a command to this list
$psUnsupportedConsoleApplications.Add('Mycommand')

# Show the augmented list of commands
$psUnsupportedConsoleApplications
```

### <a name="pslocalhelp"></a>$psLocalHelp

Toto je objekt slovníku, který udržuje kontextové mapování mezi témata nápovědy a souvisejících odkazů v místním zkompilovaný soubor nápovědy HTML. Používá se k vyhledání místní nápovědu pro určité téma. Můžete přidat nebo odstranit témata z tohoto seznamu. Následující příklad kódu ukazuje příklad páry klíč hodnota, které jsou obsaženy v `$psLocalHelp`.

```powershell
# See the local help map
$psLocalHelp | Format-List
```

### <a name="pslocalhelp-sample-output"></a>Ukázkový výstup $psLocalHelp

|||
|-|-|
|Klíč: Počítač|Hodnota: WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm|
|Klíč: Obsah|Hodnota: WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm|

Následující skript přidá položku do seznamu.

```powershell
$psLocalHelp.Add("get-myNoun", "c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a>$psOnlineHelp

Toto je objekt slovníku, který udržuje kontextové mapování mezi názvy témat témat nápovědy a jejich přidružené externí adresy URL. Používá se k vyhledejte v nápovědě k určitému tématu na webu. Můžete přidat nebo odstranit témata z tohoto seznamu.

```powershell
$psOnlineHelp | Format-List
```

## <a name="psonilnehelp-sample-output"></a>Ukázkový výstup $psOnilneHelp

|||
|-|-|
|Klíč: Počítač|Hodnota: http://go.microsoft.com/fwlink/p/?LinkID=135194|
|Klíč: Obsah|Hodnota: http://go.microsoft.com/fwlink/p/?LinkID=113278|

Následující skript přidá položku do seznamu.

```powershell
$psOnlineHelp.Add("get-myNoun", "http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a>Viz také

[Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)