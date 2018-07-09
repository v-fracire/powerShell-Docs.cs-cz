---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
title: Vylepšení konzoly ve WMF 5.1
ms.openlocfilehash: a8e82e2f973916c2ed5007eba90ee6f2b7a9a769
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892922"
---
# <a name="console-improvements-in-wmf-51"></a>Vylepšení konzoly ve WMF 5.1

## <a name="powershell-console-improvements"></a>Vylepšení konzoly Powershellu

Byly provedeny následující změny k powershell.exe ve WMF 5.1 na zlepšení uživatelského rozhraní konzoly:

### <a name="vt100-support"></a>Podpora VT100

Přidání podpory pro Windows 10 [VT100 řídicí sekvence](/windows/console/console-virtual-terminal-sequences).
Prostředí PowerShell bude ignorovat určité VT100 formátování řídicí sekvence při výpočtu šířky tabulky.

Prostředí PowerShell také přidali nová rozhraní API, které lze použít při formátování kódu k určení, jestli je podporovaná VT100.
Příklad:

```powershell
if ($host.UI.SupportsVirtualTerminal)
{
    $esc = [char]0x1b
    "A yellow ${esc}[93mhello${esc}[0m"
}
else
{
    "A default hello"
}
```

Tady je úplný [příklad](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) , který lze použít ke zvýraznění shody z `Select-String`.
Uložit v příkladu v souboru s názvem `MatchInfo.format.ps1xml`, pokud chcete použít, v profilu nebo jinde, spusťte `Update-FormatData -Prepend MatchInfo.format.ps1xml`.

Všimněte si, že sekvence escape VT100 podporují jenom od verze Windows 10 Anniversary update; nejsou podporovány v předchozích verzích systému.

### <a name="vi-mode-support-in-psreadline"></a>Podpora režimu VI v PSReadline

[PSReadline](https://github.com/lzybkr/PSReadLine) přidává podporu pro režim editoru vi. Pokud chcete použít režim vi, spusťte `Set-PSReadlineOption -EditMode Vi`.

### <a name="redirected-stdin-with-interactive-input"></a>Přesměrované stdin s interaktivní vstup

V dřívějších verzích spuštění Powershellu s `powershell -File -` byla požadována, když byl přesměrován stdin a chcete zadat příkazy interaktivně.

S WMF 5.1, tomto je obtížné zjistit, že možnost již není nezbytné.
Prostředí PowerShell můžete spustit bez jakýchkoli možností, například `powershell`.

Všimněte si, že PSReadline v současné době nepodporuje přesměrováno stdin a integrované prostředí příkazového řádku úprav s přesměrovaného stdin je velmi omezené, třeba klávesy se šipkami nefungují.
Příští verzi PSReadline by měla tento problém vyřešit.