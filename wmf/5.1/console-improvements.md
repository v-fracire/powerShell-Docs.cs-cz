---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
title: Vylepšení konzoly v WMF 5.1
ms.openlocfilehash: 2abc02010c6c1d9f7fc617e9831b2d1243e0a3ee
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="console-improvements-in-wmf-51"></a>Vylepšení konzoly v WMF 5.1#

## <a name="powershell-console-improvements"></a>Vylepšení konzoly prostředí PowerShell

Powershell.exe v WMF 5.1 provedly lepší konzoly následující změny:

###<a name="vt100-support"></a>Podpora VT100

Přidání podpory pro Windows 10 [VT100 řídicí sekvence](https://msdn.microsoft.com/en-us/library/windows/desktop/mt638032(v=vs.85).aspx).
Prostředí PowerShell bude ignorovat určité VT100 formátování řídicí sekvence při výpočtu šířky tabulky.

Prostředí PowerShell také přidat nové rozhraní API, který lze použít při formátování kódu k určení, jestli VT100 podporovaná.
Příklad:

```
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
Zde je úplná [příklad](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) který slouží k zvýrazněte odpovídá řetězci vyberte.
Uložit v příkladu v souboru s názvem `MatchInfo.format.ps1xml`, pokud chcete používat, v profilu nebo jinde, spusťte `Update-FormatData -Prepend MatchInfo.format.ps1xml`.

Všimněte si, že VT100 řídicí sekvence jsou podporovány pouze v počínaje systémem Windows 10 Anniversary aktualizace; v předchozích verzích systému nejsou podporovány.

### <a name="vi-mode-support-in-psreadline"></a>Podpora režimu VI v PSReadline

[PSReadline](https://github.com/lzybkr/PSReadLine) přidá podporu vi režimu. Chcete-li použít režim vi, spusťte `Set-PSReadlineOption -EditMode Vi`.

### <a name="redirected-stdin-with-interactive-input"></a>Přesměrovaného stdin – s interaktivní vstup

V dřívějších verzích, spouštění prostředí PowerShell s `powershell -File -` nebyla nutná, pokud byl přesměrován stdin – a chcete zadat příkazy interaktivně.

S WMF 5.1, tento obtížné zjistit, že je možnost už nebude potřeba.
Prostředí PowerShell můžete spustit bez jakékoli možnosti, například `powershell`.

Všimněte si, že PSReadline v současné době nepodporuje přesměrování stdin a integrované příkazového řádku úpravy zkušenosti s přesměrovaného stdin je velmi omezené, například nejsou funkční klávesy se šipkami.
Budoucích vydání systému PSReadline by měl tento problém vyřešit.