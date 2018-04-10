---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Ladění skriptů v prostředí Windows PowerShell ISE
ms.openlocfilehash: b7af2de83a3f796a2057514e36ad8b74367e8ce2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="how-to-debug-scripts-in-windows-powershell-ise"></a>Ladění skriptů v prostředí Windows PowerShell ISE

Tento článek popisuje postup ladění skriptů v místním počítači pomocí funkce Windows PowerShell Integrované skriptovací prostředí (ISE) visual ladění.

## <a name="how-to-manage-breakpoints"></a>Jak spravovat zarážky

Zarážka je určené místo ve skriptu, kam chcete operaci pozastavit, takže můžete zkontrolovat aktuální stav proměnné a prostředí, ve kterém běží váš skript. Jakmile vašeho skriptu je pozastaveno boru přerušení, můžete spustit příkazy v podokně konzole zkontrolujte stav vašeho skriptu.  Můžete výstup proměnné nebo spouštění jiných příkazů. Dokonce můžete upravit hodnotu proměnných, které jsou viditelné pro kontext probíhající skriptu. Po zkontrolují co chcete zobrazit můžete obnovit operace skriptu.

Tři typy zarážky můžete nastavit v ladění prostředí Windows PowerShell:

1. **Řádek zarážek**. Skript se pozastaví po dosažení určené řádku během operace skriptu

2. **Proměnné zarážek.** Skript pozastaví při každé změně hodnoty proměnné určené.

3. **Příkaz zarážek.** Skript pozastaví vždy, když je určený příkaz bude během operace skript spuštěný. Může obsahovat parametry pro další filtrování zarážek pouze operace, které chcete. Příkaz může být také funkci, kterou jste vytvořili.

Z těchto v prostředí Windows PowerShell ISE ladění lze nastavit pouze řádku zarážky pomocí nabídky nebo klávesové zkratky. Další dva typy zarážky lze nastavit, ale jsou nastavené v podokně konzoly pomocí [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) rutiny. Tato část popisuje, jak můžete provádět ladění úkoly v systému Windows PowerShell ISE pomocí nabídek, pokud je k dispozici a provádět širší rozsah příkazy z podokna konzoly pomocí skriptování.

### <a name="to-set-a-breakpoint"></a>Chcete-li nastavit zarážky

Ve skriptu můžete nastavit zarážky, až poté, co byl uložen. Klikněte pravým tlačítkem na řádek, ve které chcete nastavit zarážky řádku a potom klikněte na **Přepnout zarážku**. Nebo klikněte na řádek, ve které chcete nastavit zarážky řádek, a stiskněte klávesu **F9** nebo na **ladění** nabídky, klikněte na tlačítko **Přepnout zarážku**.

Následující skript je příklad, jak můžete nastavit proměnné zarážek v podokně konzoly pomocí [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) rutiny.

```powershell
# This command sets a breakpoint on the Server variable in the Sample.ps1 script.
Set-PSBreakpoint -Script sample.ps1 -Variable Server
```

### <a name="list-all-breakpoints"></a>Zobrazí seznam všech zarážky

Zobrazí všechny zarážky v aktuální relaci prostředí Windows PowerShell.

Na **ladění** nabídky, klikněte na tlačítko **seznamu zarážky**. Následující skript je příklad, jak můžete vytvořit seznam všech zarážky z podokna konzoly pomocí [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) rutiny.

```powershell
# This command lists all breakpoints in the current session.
Get-PSBreakpoint
```

### <a name="remove-a-breakpoint"></a>Odstranění zarážky

Odebrání zarážku neodstraní.

Pokud se domníváte, že budete chtít pozdější použití, zvažte [zakázat zarážku](#disable-a-breakpoint) ho místo.
Klikněte pravým tlačítkem na řádek, ve které chcete odebrat bod přerušení a potom klikněte na **Přepnout zarážku**.
Nebo klikněte na řádek, ve které chcete odebrat bod přerušení, a na **ladění** nabídky, klikněte na tlačítko **Přepnout zarážku**.
Následující skript představuje příklad, jak odebrat zarážku se zadaným ID z podokna konzoly pomocí [odebrat PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) rutiny.

```powershell
# This command deletes the breakpoint with breakpoint ID 2.
Remove-PSBreakpoint -Id 2
```

### <a name="remove-all-breakpoints"></a>Odeberte všechny zarážky

Chcete-li odebrat všechny zarážky definované v aktuální relaci, na **ladění** nabídky, klikněte na tlačítko **odebrat všechny zarážky**.

Následující skript představuje příklad, jak odebrat všechny zarážky v podokně konzoly pomocí [odebrat PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) rutiny.

```powershell
# This command deletes all of the breakpoints in the current session.
Get-PSBreakpoint | Remove-PSBreakpoint
```

### <a name="disable-a-breakpoint"></a>Zakázat zarážky

Zakázání zarážku neodebere. ji vypne dokud není povoleno.  Zakázat zarážku konkrétní řádku, klikněte pravým tlačítkem na řádek, kde chcete zakázat zarážku, a pak klikněte na **zakázat zarážek**. Nebo klikněte na řádek, ve které chcete zakázat zarážku, a stiskněte klávesu **F9** nebo na **ladění** nabídky, klikněte na tlačítko **zakázat zarážek**. Následující skript je příklad odebrání zarážek se zadaným ID z podokna konzoly pomocí [zakázat PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) rutiny.

```powershell
# This command disables the breakpoint with breakpoint ID 0.
Disable-PSBreakpoint -Id 0
```

### <a name="disable-all-breakpoints"></a>Zakažte všechny zarážky

Zakázání zarážku neodebere. ji vypne dokud není povoleno.  Zakázání všechny zarážky v aktuální relaci, na **ladění** nabídky, klikněte na tlačítko **zakažte všechny zarážky**. Následující skript je příklad, jak můžete zakázat všechna zarážky z podokna konzoly pomocí [zakázat PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) rutiny.

```powershell
# This command disables all breakpoints in the current session.
# You can abbreviate this command as: "gbp | dbp".
Get-PSBreakpoint | Disable-PSBreakpoint
```

### <a name="enable-a-breakpoint"></a>Povolit zarážky

Pokud chcete povolit konkrétní zarážek, klikněte pravým tlačítkem na řádek, ve které chcete povolit zarážku a pak klikněte na **povolit zarážek**. Nebo klikněte na řádek, kde chcete povolit zarážky, a potom stiskněte klávesu **F9** nebo na **ladění** nabídky, klikněte na tlačítko **povolit zarážek**. Následující skript je příklad, jak můžete povolit konkrétní zarážky z podokna konzoly pomocí [povolit PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) rutiny.

```powershell
# This command enables breakpoints with breakpoint IDs 0, 1, and 5.
Enable-PSBreakpoint -Id 0, 1, 5
```

### <a name="enable-all-breakpoints"></a>Povolit všechny zarážky

Povolit všechny zarážky definované v aktuální relaci, na **ladění** nabídky, klikněte na tlačítko **povolit všechny zarážky**. Následující skript je příklad, jak můžete povolit všechny zarážky v podokně konzoly pomocí [povolit PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) rutiny.

```powershell
# This command enables all breakpoints in the current session.
# You can abbreviate the command by using their aliases: "gbp | ebp".
Get-PSBreakpoint | Enable-PSBreakpoint
```

## <a name="how-to-manage-a-debugging-session"></a>Jak spravovat ladicí relace

Než začnete, ladění, musíte nastavit jeden nebo více zarážky. Zarážku nelze nastavit, pokud je uložen skript, který chcete ladit. Pokyny o tom, jak nastavit zarážky, najdete v části [Správa zarážky](#how-to-manage-breakpoints) nebo [Set-PSBreakpoint](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/set-psbreakpoint). Po spuštění ladění, nelze upravit skript, dokud jej nezastavíte ladění. Skript, který má jeden nebo více zarážky nastavit je automaticky uloží, než je spuštěn.

### <a name="to-start-debugging"></a>Spustit ladění

Stiskněte klávesu **F5** nebo na panelu nástrojů klikněte na tlačítko **spustit skript** ikonu, nebo na **ladění** nabídce klikněte na tlačítko **spustit nebo pokračovat**. Skript se spustí, dokud zjistí první zarážky. To pozastaví operaci tam a klade důraz na řádku, na kterém je pozastavena.

### <a name="to-continue-debugging"></a>Chcete-li pokračovat, ladění

Stiskněte klávesu **F5** nebo na panelu nástrojů klikněte na tlačítko **spustit skript** ikonu, nebo na **ladění** nabídky, klikněte na tlačítko **spustit nebo pokračovat** nebo v podokně konzoly, zadejte **C** a potom stiskněte klávesu **ENTER**. To způsobí, že skript, který chcete-li pokračovat v provozu na další zarážku nebo na konec skriptu, pokud nedojde k žádné další zarážky.

### <a name="to-view-the-call-stack"></a>Chcete-li zobrazit zásobníku volání

Zásobník volání zobrazí aktuální spuštění umístění ve skriptu. Pokud skriptu běží ve funkci, která byla zavolána různých funkcí, pak která je reprezentována v zobrazení dodatečné řádky ve výstupu. Spodní krajní řádek zobrazí původní skript a na řádku v ní ve kterém byla zavolána funkce. Další rovině ukazuje, že funkce a řádku v ní ve kterém může mít jinou funkci zavolání.  Nejvyšší řádek ukazuje aktuální kontext aktuálního řádku, na kterém je nastaven breakpoint.

Při pozastavena, chcete-li zobrazit aktuální zásobníku volání, stiskněte **CTRL + SHIFT + D** nebo na **ladění** nabídky, klikněte na tlačítko **zásobníkem volání zobrazení** nebo v podokně konzoly zadejte **kB**  a potom stiskněte klávesu **ENTER**.

### <a name="to-stop-debugging"></a>Aby se ukončilo ladění

Stiskněte klávesu **SHIFT + F5** nebo na **ladění** nabídky, klikněte na tlačítko **zastavení ladicího programu**, nebo v podokně konzoly zadejte **Q** a potom stiskněte klávesu  **Zadejte**.

## <a name="how-to-step-over-step-into-and-step-out-while-debugging"></a>Postup krok přes, krok do a krok při ladění

Krokování je proces spuštěný jeden příkaz v čase. Můžete zastavit na řádek kódu a zkontrolujte hodnoty proměnné a stavu systému. Následující tabulka popisuje běžné úkoly ladění jako krokování přes, zanoříte se do a zanoříte.

| Ladění úloh | Popis | Jak provést v prostředí PowerShell ISE |
| --- | --- | --- |
| **Krok do** | Aktuální příkaz a poté se zastaví v další příkaz. Pokud aktuální příkaz funkce nebo skriptu volání a pak ladicí program do této funkce nebo skriptu, jinak se zastaví v další příkaz. | Stiskněte klávesu **F11** nebo na **ladění** nabídky, klikněte na tlačítko **Krokovat s vnořením**, nebo v podokně konzoly zadejte **S** a stiskněte klávesu **ENTER**. |
| **Krok přes** | Aktuální příkaz a poté se zastaví v další příkaz. Pokud je aktuální příkaz funkce nebo skriptu volání a pak ladicí program provede celou funkce nebo skriptu a zastaví v další příkaz po volání funkce. | Stiskněte klávesu **F10** nebo na **ladění** nabídky, klikněte na tlačítko **Krokovat s přeskočením**, nebo v podokně konzoly zadejte **V** a stiskněte klávesu **ENTER**. |
| **Krok** | Kroky mimo funkci current a jednu úroveň, pokud je vnořené funkce. Pokud v hlavní, skript se spustí na konec nebo na další zarážku. Bylo vynecháno příkazy jsou provést, ale není provedl. | Stiskněte klávesu **SHIFT + F11**, nebo na **ladění** nabídky, klikněte na tlačítko **Krokovat s Vystoupením**, nebo v podokně konzoly zadejte **O** a stiskněte klávesu **ENTER**. |
| **Pokračovat** | Pokračuje v provádění na konec nebo na další zarážku. Bylo vynecháno funkce a volání jsou provést, ale není provedl. | Stiskněte klávesu **F5** nebo na **ladění** nabídky, klikněte na tlačítko **spustit nebo pokračovat**, nebo v podokně konzoly zadejte **C** a stiskněte klávesu **ENTER**. |

## <a name="how-to-display-the-values-of-variables-while-debugging"></a>Postupy: zobrazení hodnot proměnných při ladění

V průběhu kód můžete zobrazit aktuální hodnoty proměnné ve skriptu.

### <a name="to-display-the-values-of-standard-variables"></a>K zobrazení hodnot proměnných standardní

Použijte jednu z následujících metod:

- V podokně skriptu pozastavte ukazatel myši nad proměnnou k zobrazení jeho hodnoty jako popis tlačítka.

- V podokně konzoly, zadejte název proměnné a stiskněte klávesu **ENTER**.

Všechny podokna (ISE) v jsou vždycky ve stejném oboru. Proto v při ladění skriptu, spusťte příkazy, které zadáte v podokně konzoly v oboru skriptu. To umožňuje používat k vyhledání hodnoty proměnných a volání funkce, které jsou definovány pouze ve skriptu v podokně konzoly.

### <a name="to-display-the-values-of-automatic-variables"></a>K zobrazení hodnot proměnných automatické

Předchozí postup můžete použít k zobrazení hodnot proměnných téměř všechny při ladění skriptu. Tyto metody se ale nefungují pro následující automatické proměnné.

- $_

- $Input

- $MyInvocation

- $PSBoundParameters

- $Args

Pokud se pokusíte zobrazit hodnotu tyto proměnné, můžete získat hodnotu této proměnné v interní kanálu ladicí program používá, není hodnota proměnné ve skriptu. Můžete obejít tím pár proměnných ($_, $Input, $MyInvocation, $PSBoundParameters a $Args) pomocí následující metody:

1. Ve skriptu přiřadíte hodnotu proměnné, automatické nové proměnné.

2. Zobrazte hodnotu nové proměnné, ukázáním myší nové proměnné v podokně skriptu nebo zadáním nové proměnné v podokně konzoly.

Například zobrazit hodnotu $MyInvocation proměnné ve skriptu, hodnota přiřadit nové proměnné, jako je například $scriptname a poté najeďte myší na nebo zadejte proměnnou $scriptname zobrazíte jeho hodnotu.

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