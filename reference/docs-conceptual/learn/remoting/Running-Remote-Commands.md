---
ms.date: 08/14/2018
keywords: rutiny prostředí PowerShell
title: Spuštění vzdálených příkazů
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: 2001b5509acde6ec4259bb1442944958a67aa66f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404057"
---
# <a name="running-remote-commands"></a>Spuštění vzdálených příkazů

Příkazy můžete spustit na jednom nebo stovky počítačů pomocí jediného příkazu prostředí PowerShell. Prostředí Windows PowerShell podporuje vzdálený přístup pomocí různých technologií, včetně služby WMI, RPC a WS-Management.

PowerShell Core podporuje rozhraní WMI, WS-Management a vzdálenou komunikaci SSH. RPC se už nepodporuje.

Další informace o vzdálené komunikace v prostředí PowerShell Core najdete v následujících článcích:

- [SSH vzdálené komunikace v Powershellu Core][ssh-remoting]
- [Vzdálená komunikace WSMan v Powershellu Core][wsman-remoting]

## <a name="windows-powershell-remoting-without-configuration"></a>Vzdálená komunikace Windows Powershellu bez konfigurace

Mnoho rutin prostředí Windows PowerShell mají parametr ComputerName, který vám umožní shromažďovat data a nastavení na jeden nebo více vzdálených počítačích. Tyto rutiny použít různé komunikační protokoly a fungovat ve všech operačních systémech Windows bez žádnou zvláštní konfiguraci.

Tyto rutiny zahrnují:

- [Restart-Computer](/powershell/module/microsoft.powershell.management/restart-computer)
- [Test připojení](/powershell/module/microsoft.powershell.management/test-connection)
- [Clear-EventLog](/powershell/module/microsoft.powershell.management/clear-eventlog)
- [Get-EventLog](/powershell/module/microsoft.powershell.management/get-eventlog)
- [Get-HotFix](/powershell/module/microsoft.powershell.management/get-hotfix)
- [Get-Process](/powershell/module/microsoft.powershell.management/get-process)
- [Get-Service](/powershell/module/microsoft.powershell.management/get-service)
- [Nastavení služby](/powershell/module/microsoft.powershell.management/set-service)
- [Get-WinEvent](/powershell/module/microsoft.powershell.diagnostics/get-winevent)
- [Get-WmiObject](/powershell/module/microsoft.powershell.management/get-wmiobject)

Rutiny, které podporují vzdálené komunikace bez speciální konfigurace obvykle mít parametr ComputerName a nemáte parametr relace. Chcete-li tyto rutiny najdete v relaci, zadejte:

```powershell
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a>Vzdálená komunikace Windows Powershellu

Pomocí protokolu WS-Management, umožňuje vzdálenou komunikaci Windows Powershellu můžete spouštět jakékoli příkazy prostředí Windows PowerShell na jeden nebo více vzdálených počítačích. Můžete navázat trvalé připojení, spouštění interaktivních relací a spouštět skripty na vzdálených počítačích.

Pokud chcete použít vzdálenou komunikaci prostředí Windows PowerShell, musí být vzdálený počítač nakonfigurovaný pro vzdálenou správu.
Další informace, včetně pokynů, najdete v části [vzdálené požadavky](/powershell/module/microsoft.powershell.core/about/about_remote_requirements).

Po nakonfigurování vzdálenou komunikaci prostředí Windows PowerShell, jsou k dispozici, mnoho strategií vzdálené komunikace.
Tento článek uvádí jenom některé z nich. Další informace najdete v tématu [o vzdálené](/powershell/module/microsoft.powershell.core/about/about_remote).

### <a name="start-an-interactive-session"></a>Spuštění interaktivní relace

Chcete-li spustit interaktivní relaci s jeden vzdálený počítač, použijte [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession) rutiny.
Například spuštění interaktivní relace Server01 na vzdáleném počítači, zadejte:

```powershell
Enter-PSSession Server01
```

Příkazový řádek se změny zobrazily název vzdáleného počítače. Všechny příkazy, které zadáte v příkazovém řádku spustit na vzdáleném počítači a výsledky se zobrazí v místním počítači.

Pokud chcete ukončit interaktivní relace, zadejte:

```powershell
Exit-PSSession
```

Další informace o rutinách Enter-PSSession a ukončení relace PSSession najdete v článku:

- [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession)
- [Ukončení relace PSSession](/powershell/module/microsoft.powershell.core/exit-pssession)

### <a name="run-a-remote-command"></a>Spustit vzdálený příkaz

Chcete-li spustit příkaz na jeden nebo více počítačů, použijte [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command) rutiny. Chcete-li například spustit [Get-UICulture](/powershell/module/microsoft.powershell.utility/get-uiculture) v Server01 a Server02 vzdálenými počítači, zadejte příkaz:

```powershell
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

Výstup se vrací do vašeho počítače.

```output
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```

### <a name="run-a-script"></a>Spuštění skriptu

Pro spuštění skriptu na jeden nebo více vzdálených počítačích, použít parametr FilePath `Invoke-Command` rutiny. Skript musí být přístupné pro místního počítače. Výsledky jsou vráceny do místního počítače.

Například následující příkaz spustí skript DiskCollect.ps1 na vzdálených počítačích, Server01 a Server02.

```powershell
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

### <a name="establish-a-persistent-connection"></a>Navázat trvalé připojení

Použití `New-PSSession` rutina pro vytvoření trvalého relace na vzdáleném počítači. Následující příklad vytvoří na Server01 a Server02 vzdálené relace. Objekty relace jsou uloženy v `$s` proměnné.

```powershell
$s = New-PSSession -ComputerName Server01, Server02
```

Teď, když jsou vytvořeny na relace, můžete spouštět jakékoli příkazy v nich. A protože relací jsou trvalé, můžete shromažďovat data z jednoho příkazu a použít v jiné příkazu.

Například následující příkaz spustí příkaz Get-HotFix v relacích $s proměnné a uloží výsledky do $h proměnné. $H proměnná je vytvořená ve všech relacích v $s, ale neexistuje v místní relaci.

```powershell
Invoke-Command -Session $s {$h = Get-HotFix}
```

Teď můžete použít data v `$h` proměnné s jinými příkazy ve stejné relaci. Výsledky se zobrazí v místním počítači. Příklad:

```powershell
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a>Pokročilé vzdálené komunikace

Vzdálená správa prostředí Windows PowerShell začíná právě tady. Pomocí rutiny nainstalované pomocí prostředí Windows PowerShell můžete vytvořit a nakonfigurovat vzdálené relace z konců místních a vzdálených vytvářet přizpůsobené a s omezeným přístupem relace, umožňuje uživatelům importovat příkazy ze vzdálené relace, které skutečně běží. implicitně na vzdálenou relaci, nakonfigurujte zabezpečení vzdálené relace a spoustu dalších věcí.

Prostředí Windows PowerShell obsahuje poskytovatele služby WSMan. Vytvoří poskytovatele `WSMAN:` jednotky, ve kterém můžete procházet hierarchii konfigurovat nastavení pro místní i vzdálené počítače.

Další informace o poskytovateli WSMan najdete v tématu [WSMan poskytovatele](https://technet.microsoft.com/library/dd819476.aspx) a [o WS-Management – rutiny](/powershell/module/microsoft.powershell.core/about/about_ws-management_cmdlets), nebo v konzole Windows Powershellu zadejte `Get-Help wsman`.

Další informace viz:

- [Informace o vzdálené – nejčastější dotazy](https://technet.microsoft.com/library/dd315359.aspx)
- [Register-PSSessionConfiguration](https://go.microsoft.com/fwlink/?LinkId=821508)
- [Import-PSSession](https://go.microsoft.com/fwlink/?LinkId=821821)

Vzdálená komunikace vyřešení problémů, najdete v části [about_Remote_Troubleshooting](https://technet.microsoft.com/library/dd347642.aspx).

## <a name="see-also"></a>Viz také

- [about_Remote](https://technet.microsoft.com/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [about_Remote_FAQ](https://technet.microsoft.com/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [about_Remote_Requirements](https://technet.microsoft.com/library/da213949-134c-4741-b307-81f4492ba1bd)
- [about_Remote_Troubleshooting](https://technet.microsoft.com/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [about_PSSessions](https://technet.microsoft.com/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [about_WS-Management_Cmdlets](https://technet.microsoft.com/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command)
- [Import-PSSession](https://go.microsoft.com/fwlink/?LinkId=821821)
- [Nová relace PSSession](https://go.microsoft.com/fwlink/?LinkId=821498)
- [Register-PSSessionConfiguration](https://go.microsoft.com/fwlink/?LinkId=821508)
- [Poskytovatel služby WSMan](https://technet.microsoft.com/library/66fe1241-e08f-49ca-832f-a84c33ca8735)

[wsman-remoting]: WSMan-Remoting-in-PowerShell-Core.md
[ssh-remoting]: SSH-Remoting-in-PowerShell-Core.md