---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Ladění skriptů v prostředí Windows PowerShell ISE
ms.openlocfilehash: b7af2de83a3f796a2057514e36ad8b74367e8ce2
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404082"
---
# <a name="how-to-debug-scripts-in-windows-powershell-ise"></a>Ladění skriptů v prostředí Windows PowerShell ISE

Tento článek popisuje, jak pomocí Windows Powershellu integrovaném skriptovacím prostředí (ISE) vizuální ladění funkcí ladění skriptů v místním počítači.

## <a name="how-to-manage-breakpoints"></a>Jak spravovat zarážky

Zarážka je určené místo ve skriptu, ve kterém chcete operace pozastavit, takže můžete zkontrolovat aktuální stav proměnné a prostředí, ve kterém je spuštěn skript. Jakmile váš skript je pozastaveno zarážku, můžete spouštět příkazy v podokně konzoly pro zjištění stavu vašeho skriptu.  Můžete výstup proměnné nebo spustit další příkazy. Dokonce můžete upravit hodnotu proměnné, které jsou viditelné pro kontext aktuálně spuštěného skriptu. Po kontrole, co chcete zobrazit, můžete obnovit operace skriptu.

Tři typy zarážky můžete nastavit v ladicím prostředí Windows PowerShell:

1. **Řádek zarážky**. Skript pozastaví při dosažení řádku určené během operace skriptu

2. **Zarážka v proměnné.** Skript pozastaví pokaždé, když se změní hodnota proměnné určené.

3. **Příkaz zarážku.** Skript pozastaví pokaždé, když určený příkaz bude spuštěn při operaci skriptu. Může obsahovat parametry dál filtrovat zarážky pouze operace, které chcete. Příkaz může být také funkce, které jste vytvořili.

Z těchto v prostředí Windows PowerShell ISE ladění lze nastavit pouze řádek zarážky pomocí nabídky nebo pomocí klávesové zkratky. Další dva druhy zarážky můžete nastavit, ale jsou nastavené v podokně konzoly pomocí [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) rutiny. Tato část popisuje, jak můžete provádět ladění úlohy v prostředí Windows PowerShell ISE pomocí nabídky, pokud je k dispozici a provádět širší škálu příkazy z podokna konzoly pomocí skriptování.

### <a name="to-set-a-breakpoint"></a>Chcete-li nastavit zarážku

Zarážku lze nastavit ve skriptu, až po se uložil. Klikněte pravým tlačítkem na řádek, ve které chcete nastavit zarážku řádek a potom klikněte na **Přepnout zarážku**. Nebo klikněte na řádek, ve které chcete nastavit zarážku řádku a stisknutím klávesy **F9** nebo na **ladění** nabídky, klikněte na tlačítko **Přepnout zarážku**.

Následující skript je příklad, jak můžete nastavit zarážku proměnné z podokna konzoly pomocí [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) rutiny.

```powershell
# This command sets a breakpoint on the Server variable in the Sample.ps1 script.
Set-PSBreakpoint -Script sample.ps1 -Variable Server
```

### <a name="list-all-breakpoints"></a>Vypsat všechny zarážky

Zobrazí všechny zarážky v aktuální relaci Windows Powershellu.

Na **ladění** nabídky, klikněte na tlačítko **seznamu zarážek**. Následující skript představuje příklad, o tom, jak můžete vytvořit seznam všechny zarážky v podokně konzoly pomocí [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) rutiny.

```powershell
# This command lists all breakpoints in the current session.
Get-PSBreakpoint
```

### <a name="remove-a-breakpoint"></a>Odebrat zarážky

Odebrání zarážku ji odstraní.

Pokud si myslíte, že budete chtít později znovu použít, zvažte [zakázat zarážku](#disable-a-breakpoint) jej místo toho.
Klikněte pravým tlačítkem na řádek, kde chcete odebrat zarážku a poté klikněte na tlačítko **Přepnout zarážku**.
Nebo klikněte na řádek, ve které chcete odebrat zarážku, a dále **ladění** nabídky, klikněte na tlačítko **Přepnout zarážku**.
Následující skript představuje příklad, jak odebrat zarážku se zadaným ID z konzole pomocí [odebrat PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) rutiny.

```powershell
# This command deletes the breakpoint with breakpoint ID 2.
Remove-PSBreakpoint -Id 2
```

### <a name="remove-all-breakpoints"></a>Odebrat všechny zarážky

Chcete-li odebrat všechny zarážky, které jsou definované v aktuální relaci na **ladění** nabídky, klikněte na tlačítko **odebrat všechny zarážky**.

Následující skript představuje příklad, jak odebrat všechny zarážky v podokně konzoly pomocí [odebrat PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) rutiny.

```powershell
# This command deletes all of the breakpoints in the current session.
Get-PSBreakpoint | Remove-PSBreakpoint
```

### <a name="disable-a-breakpoint"></a>Zakázat zarážku

Zakázat zarážku neodebere. ji vypne dokud není povoleno.  Zakázat zarážku konkrétního řádku, klikněte pravým tlačítkem na řádek, ve kterém chcete zakázat zarážku a poté klikněte na tlačítko **zakázat zarážku**. Nebo klikněte na řádek, ve které chcete zakázat zarážku, a stiskněte klávesu **F9** nebo na **ladění** nabídky, klikněte na tlačítko **zakázat zarážku**. Následující skript je příklad, jak odebrat zarážku se zadaným ID z podokna konzoly pomocí [zakázat PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) rutiny.

```powershell
# This command disables the breakpoint with breakpoint ID 0.
Disable-PSBreakpoint -Id 0
```

### <a name="disable-all-breakpoints"></a>Zakázat všechny zarážky

Zakázat zarážku neodebere. ji vypne dokud není povoleno.  Chcete-li zakázat všechny zarážky v aktuální relaci, na **ladění** nabídky, klikněte na tlačítko **zakázat všechny zarážky**. Následující skript představuje příklad, o tom, jak můžete zakázat všechny zarážky v podokně konzoly pomocí [zakázat PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) rutiny.

```powershell
# This command disables all breakpoints in the current session.
# You can abbreviate this command as: "gbp | dbp".
Get-PSBreakpoint | Disable-PSBreakpoint
```

### <a name="enable-a-breakpoint"></a>Povolit zarážku

Pokud chcete povolit konkrétní zarážky, klikněte pravým tlačítkem na řádek, ve které chcete povolit zarážku a poté klikněte na tlačítko **povolit zarážku**. Nebo klikněte na řádek, ve které chcete povolit zarážku a potom stiskněte klávesu **F9** nebo na **ladění** nabídky, klikněte na tlačítko **povolit zarážku**. Následující skript představuje příklad, o tom, jak můžete povolit konkrétní zarážky v podokně konzoly pomocí [povolit PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) rutiny.

```powershell
# This command enables breakpoints with breakpoint IDs 0, 1, and 5.
Enable-PSBreakpoint -Id 0, 1, 5
```

### <a name="enable-all-breakpoints"></a>Povolit všechny zarážky

Povolit všechny zarážky, které jsou definované v aktuální relaci na **ladění** nabídky, klikněte na tlačítko **povolit všechny zarážky**. Následující skript představuje příklad, o tom, jak můžete povolit všechny zarážky v podokně konzoly pomocí [povolit PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) rutiny.

```powershell
# This command enables all breakpoints in the current session.
# You can abbreviate the command by using their aliases: "gbp | ebp".
Get-PSBreakpoint | Enable-PSBreakpoint
```

## <a name="how-to-manage-a-debugging-session"></a>Jak spravovat relace ladění

Před zahájením ladění, je nutné nastavit jednu nebo více zarážek. Nelze nastavit zarážku, není-li uložit skript, který chcete ladit. Pokyny na tom, jak nastavit zarážky, naleznete v tématu [Správa zarážky](#how-to-manage-breakpoints) nebo [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint). Po spuštění ladění, nelze upravit skript, dokud zastavíte ladění. Skript, který má jednu nebo více zarážek nastavení se automaticky uloží před spuštěním.

### <a name="to-start-debugging"></a>Pro spuštění ladění

Stisknutím klávesy **F5** nebo na panelu nástrojů klikněte na tlačítko **spustit skript** ikonu, nebo na **ladění** klikněte na nabídku **Spustit/pokračovat**. Skript se spustí, dokud nenarazí k první zarážce. Operace v ní se pozastaví a zvýrazní řádek, na kterém je pozastavená.

### <a name="to-continue-debugging"></a>Pro pokračování v ladění

Stisknutím klávesy **F5** nebo na panelu nástrojů klikněte na tlačítko **spustit skript** ikonu, nebo na **ladění** nabídky, klikněte na tlačítko **Spustit/pokračovat** nebo na panelu konzoly zadejte **C** a potom stiskněte klávesu **ENTER**. To způsobí, že skript bude moct být spuštěná na další zarážku nebo na konec skriptu, pokud nedojde k žádné další zarážky.

### <a name="to-view-the-call-stack"></a>Chcete-li zobrazit zásobník volání

Zásobník volání zobrazí aktuálního spuštění umístění ve skriptu. Pokud se ve funkci, která byla volána různých funkcí je spuštěný skript, pak, který je reprezentován v zobrazení dodatečné řádky ve výstupu. Většina dolní řádek zobrazí původní skript a řádku v něm ve kterém byla volána funkce. Na další řádek nahoru ukazuje tuto funkci a řádek v něm ve kterém může mít jinou funkci zavolání.  Nejvrchnější řádek zobrazuje aktuální kontext aktuálního řádku, na kterém je nastavena zarážka.

Během pozastavení, chcete-li zobrazit aktuální zásobník volání, stiskněte **CTRL + SHIFT + D** nebo na **ladění** nabídky, klikněte na tlačítko **zobrazit zásobník volání** nebo na panelu konzoly zadejte **tis.**  a potom stiskněte klávesu **ENTER**.

### <a name="to-stop-debugging"></a>Chcete zastavit ladění

Stisknutím klávesy **SHIFT + F5** nebo na **ladění** nabídky, klikněte na tlačítko **zastavit ladicí program**, nebo na panelu konzoly zadejte **Q** a potom stiskněte klávesu  **Zadejte**.

## <a name="how-to-step-over-step-into-and-step-out-while-debugging"></a>Krokovat přes, Krokovat s vnořením a Krokovat s Vystoupením při ladění

Krokování je proces spuštěný jeden příkaz v čase. Můžete zastavit na řádek kódu a zkoumat hodnoty proměnné a stav systému. Následující tabulka popisuje běžné úlohy ladění jako je například krokování přes, krokování a krokování navýšení kapacity.

| Ladění úloh | Popis | Jak provést v prostředí PowerShell ISE |
| --- | --- | --- |
| **Krokovat s vnořením** | Aktuální příkaz spustí a zastaví se na další příkaz. Pokud je aktuální příkaz funkci nebo volání skriptu a ladicí program vstoupí do této funkce nebo skriptu, jinak se zastaví na další příkaz. | Stisknutím klávesy **F11** nebo na **ladění** nabídky, klikněte na tlačítko **Krokovat s vnořením**, nebo na panelu konzoly zadejte **S** a stiskněte klávesu **ENTER**. |
| **Krok přes** | Aktuální příkaz spustí a zastaví se na další příkaz. Pokud je aktuální příkaz funkci nebo volání skriptu a ladicí program provede celou funkce nebo skriptu a zastaví na další příkaz následující po volání funkce. | Stisknutím klávesy **F10** nebo na **ladění** nabídky, klikněte na tlačítko **Krokovat s přeskočením**, nebo na panelu konzoly zadejte **V** a stiskněte klávesu **ENTER**. |
| **Krokovat s Vystoupením** | Kroky aktuální funkci a nahoru o jednu úroveň Pokud vnořené funkce. Pokud se v hlavní části skript provádí na konci nebo až k další zarážce. Přeskočené příkazy se provedl, ale ne prošli. | Stisknutím klávesy **SHIFT + F11**, nebo **ladění** nabídky, klikněte na tlačítko **Krokovat s Vystoupením**, nebo na panelu konzoly zadejte **O** a stiskněte klávesu **ENTER**. |
| **Pokračovat** | Pokračuje v provádění na konec nebo až k další zarážce. Přeskočené funkce a volání jsou provedeny, ale ne prošli. | Stisknutím klávesy **F5** nebo na **ladění** nabídky, klikněte na tlačítko **Spustit/pokračovat**, nebo na panelu konzoly zadejte **C** a stiskněte klávesu **ENTER**. |

## <a name="how-to-display-the-values-of-variables-while-debugging"></a>Způsob zobrazení hodnot proměnných při ladění

Jak krokovat kód, můžete zobrazit aktuální hodnoty proměnných ve skriptu.

### <a name="to-display-the-values-of-standard-variables"></a>K zobrazení hodnot proměnných standard

Použijte jednu z následujících metod:

- V podokně se skriptem najeďte myší proměnnou, a zobrazit jeho hodnotu jako popisku tlačítka.

- V podokně konzoly, zadejte název proměnné a stiskněte klávesu **ENTER**.

Všechna podokna v prostředí ISE jsou vždy ve stejném oboru. Proto v při ladění skriptu, spouštět příkazy, které zadáte v podokně konzoly v oboru skriptu. To umožňuje použití Pokokna konzoly můžete najít hodnoty proměnných a volání funkcí, které jsou definovány pouze ve skriptu.

### <a name="to-display-the-values-of-automatic-variables"></a>Chcete-li zobrazit hodnoty automatických proměnných

Předchozí postup můžete použít k zobrazení hodnoty téměř všech proměnných při ladění skriptu. Tyto metody nebude fungovat pro následující automatických proměnných.

- $_

- $Input

- $MyInvocation

- $PSBoundParameters

- $Args

Pokud se pokusíte zobrazit hodnotu kterékoli z těchto proměnných, získejte hodnotu této proměnné pro interní kanálu ladicí program používá, nikoli hodnotu proměnné ve skriptu. Můžete alternativně vyřešit to několika proměnných ($_, $Input, $MyInvocation, $PSBoundParameters a $Args) následujícím způsobem:

1. Ve skriptu přiřadíte hodnotu proměnné automatické nové proměnné.

2. Zobrazte hodnotu nové proměnné ukazatele myši na novou proměnnou z podokna skriptu, nebo tak, že zadáte nové proměnné v podokně konzoly.

Například k zobrazení hodnoty $MyInvocation proměnné ve skriptu, přiřaďte hodnotu nové proměnné, jako je například $scriptname a pak najeďte myší nebo zadejte proměnnou $scriptname k zobrazení jeho hodnoty.

```powershell
# In C:\ps-test\MyScript.ps1
$scriptname = $MyInvocation.MyCommand.Path
```

```output
# In the Console Pane:
PS> .\MyScript.ps1
PS> $scriptname
C:\ps-test\MyScript.ps1
```

## <a name="see-also"></a>Viz také

- [Seznámení s prostředím Windows PowerShell ISE](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)