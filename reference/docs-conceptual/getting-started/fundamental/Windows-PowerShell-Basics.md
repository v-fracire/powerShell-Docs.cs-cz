---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Základy Windows PowerShellu
ms.assetid: 6b3cbbc8-060c-4877-b00b-7300dbbe4e28
ms.openlocfilehash: b21c6cd84ea29d5e8085ccf8df2a5a9199e1d859
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="windows-powershell-basics"></a>Základy Windows PowerShellu
Grafické uživatelské rozhraní pomocí některé základní pojmy, které jsou dobře známé pro většinu uživatelů počítače. Uživatelé využívají znalosti těchto rozhraní k provádění úloh. Operační systémy představovat grafické reprezentace položky, které mohou procházet, obvykle pomocí rozevíracích nabídek pro přístup k určité funkce a kontext nabídky pro přístup k funkci konkrétní uživatelé.

Rozhraní příkazového řádku (CLI), jako je Windows PowerShell, musíte použít jiný přístup ke zveřejnění informací, protože nemá nabídek nebo grafické systémy pomoct uživateli. Musíte znát názvy příkazů, abyste mohli používat. I když můžete zadat komplexní příkazy, které odpovídají funkcí v prostředí s grafickým uživatelským rozhraním, musí seznámit s běžně používané příkazy a parametry příkazu.

Většina CLIs nemají vzorů, které pomáhají uživatelům další rozhraní. Protože CLIs byly první součásti pro operační systém, mnoha názvy příkazů a názvy parametrů nebyly vybrány libovolně. Názvy ve formátu Terse zasílaná příkazů obecně členové přes vymazat některé ze stávajících. I když systémů nápovědy a příkaz návrhu standardy jsou integrovány většina CLIs, budou mít byla obecně navržené pro kompatibilitu s nejdřívější příkazy, tak sadu příkazů nástroje ve rozhodnutí desetiletí před stále tvaru.

Prostředí Windows PowerShell byla navržená tak, že chcete využít výhod historické znalosti CLIs uživatele. V této kapitole se věnuje některé základní nástroje a koncepty, které vám pomůže rychle další prostředí Windows PowerShell. Patří mezi ně:

- Pomocí [Get-Command](/powershell/module/Microsoft.PowerShell.Core/get-command)

- Pomocí [Cmd.exe](/windows-server/administration/windows-commands/cmd) a [příkazů systému UNIX](/windows/wsl/reference)

- [Pomocí karty dokončení](../../core-powershell/console/using-tab-expansion.md)

- [Pomocí Get-Help](./getting-detailed-help-information.md)