---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Spuštění vzdálených příkazů"
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: 43f07abd642e7de235647fa151537c46ebe86cae
ms.sourcegitcommit: 6aed37d7f0c9652ae09bb8c11928da7e4783ed7f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/10/2018
---
# <a name="running-remote-commands"></a>Spuštění vzdálených příkazů

Příkazy můžete spustit na jednom nebo stovky počítačů pomocí jednoho příkazu prostředí Windows PowerShell. Prostředí Windows PowerShell podporuje vzdálený přístup pomocí různých technologií, včetně WS-Management, rozhraní WMI a RPC.

## <a name="remoting-in-powershell-core"></a>Vzdálená komunikace prostředí PowerShell jádra

Jádro prostředí PowerShell, na novější edici prostředí PowerShell v systému Windows, systému macOS a Linux, podporuje rozhraní WMI, WS-Management a vzdálené komunikace s SSH.
(RPC již není podporována.)

Další informace o toto nastavení najdete v tématu:

* [SSH vzdálené komunikace v prostředí PowerShell základní] [ssh-vzdálené komunikace]
* [WinRM vzdálené komunikace v prostředí PowerShell základní] [winrm vzdálené komunikace]

## <a name="remoting-without-configuration"></a>Vzdálená komunikace bez konfigurace
Mnoho rutin prostředí Windows PowerShell mít parametr ComputerName, která umožňuje shromažďování dat a změňte nastavení na jeden nebo více vzdálených počítačích. Používají různé technologie komunikace a mnoho pracovních na všechny operační systémy Windows, které podporuje prostředí Windows PowerShell bez žádnou zvláštní konfiguraci.

Zahrnout tyto rutiny:

* [Restartování počítače](https://go.microsoft.com/fwlink/?LinkId=821625)
* [Test připojení](https://go.microsoft.com/fwlink/?LinkId=821646)
* [Clear – protokolu událostí](https://go.microsoft.com/fwlink/?LinkId=821568)
* [Get-protokolu událostí](https://go.microsoft.com/fwlink/?LinkId=821585)
* [Get-oprav HotFix](https://go.microsoft.com/fwlink/?LinkId=821586)
* [Get-Process](https://go.microsoft.com/fwlink/?linkid=821590)
* [Get-Service](https://go.microsoft.com/fwlink/?LinkId=821593)
* [Nastavení služby](https://go.microsoft.com/fwlink/?LinkId=821633)
* [Get-WinEvent.](https://go.microsoft.com/fwlink/?linkid=821529)
* [Get-WmiObject](https://go.microsoft.com/fwlink/?LinkId=821595)

Rutiny, které podporují vzdálené komunikace bez zvláštní konfiguraci obvykle mají parametr ComputerName a nemají parametr relace. Chcete-li v relaci najít tyto rutiny, zadejte:

```
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a>Vzdálenou komunikaci Windows PowerShell
Vzdálená komunikace prostředí Windows PowerShell, který používá protokol WS-Management, vám umožní spustit libovolný příkaz prostředí Windows PowerShell na jeden nebo více vzdálených počítačích. Umožňuje vytvořit trvalé připojení, spusťte interaktivní relace 1:1 a spouštět skripty ve více počítačích.

Pokud chcete použít vzdálenou komunikaci prostředí Windows PowerShell, musí být vzdálený počítač konfigurován pro vzdálenou správu. Další informace, včetně pokynů, najdete v části [vzdálené požadavky](https://technet.microsoft.com/en-us/library/dd315349.aspx).

Po dokončení konfigurace vzdálené komunikace Windows Powershellu jsou dostupné mnoho strategií vzdálené komunikace. Zbývající část tohoto dokumentu jsou uvedeny jen některé z nich. Další informace najdete v tématu [o vzdálené](https://technet.microsoft.com/en-us/library/dd347744.aspx) a [o vzdálené – nejčastější dotazy](https://technet.microsoft.com/en-us/library/dd347744.aspx).

### <a name="start-an-interactive-session"></a>Spusťte interaktivní relace.
Spusťte interaktivní relace s jeden vzdálený počítač pomocí [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) rutiny.
Například spuštění interaktivní relace na vzdáleném počítači Server01, zadejte:

```
Enter-PSSession Server01
```

Změny příkazového řádku a zobrazí se název počítače, do které jste připojeni. Od toho všechny příkazy, které zadejte v příkazovém řádku spusťte na vzdáleném počítači a výsledky jsou zobrazeny v místním počítači.

Chcete-li ukončit interaktivní relace, zadejte:

```
Exit-PSSession
```

Další informace o rutinách Enter-PSSession a ukončení-PSSession najdete v tématu [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) a [ukončení-PSSession](https://go.microsoft.com/fwlink/?LinkID=821478).

### <a name="run-a-remote-command"></a>Spuštění vzdáleného příkazu
Chcete-li spustit libovolný příkaz na jeden nebo více vzdálených počítačích, použijte [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493) rutiny.
Chcete-li například spustit [Get-UICulture](https://go.microsoft.com/fwlink/?LinkId=821806) na Server01 a Server02 vzdálených počítačích, zadejte příkaz:

```
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

Výstup se vrací do vašeho počítače.

```
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```
Další informace o rutinu Invoke-Command najdete v tématu [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).

### <a name="run-a-script"></a>Spustit skript
Chcete-li spustit skript na jeden nebo více vzdálených počítačích, použijte parametr FilePath rutiny Invoke-Command. Skript musí být na nebo přístupné pro místního počítače. Výsledky jsou vráceny do místního počítače.

Například následující příkaz spustí skript DiskCollect.ps1 na vzdálených počítačích Server01 a Server02.

```
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

Další informace o rutinu Invoke-Command najdete v tématu [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).

### <a name="establish-a-persistent-connection"></a>Trvalé připojení
Pokud chcete spustit řadu související příkazy, které sdílet data, vytvoření relace na vzdáleném počítači a pak spusťte příkazy v relaci, kterou vytvoříte pomocí rutiny Invoke-Command. Pokud chcete vytvořit vzdálené relace, použijte rutinu New-PSSession.

Například následující příkaz vytvoří relaci vzdálené počítače Server01 a jiná relace vzdáleného počítače Server02. Objekty relace ukládá v proměnné $s.

```
$s = New-PSSession -ComputerName Server01, Server02
```

Teď, když jsou určeny k relacím, můžete v nich spustit libovolný příkaz. A protože relací jsou trvalé, můžete shromažďování dat do jednoho příkazu a použít ho v následující příkaz.

Například následující příkaz spustí příkaz Get-opravu HotFix v relacích v $s proměnné a uloží výsledky v $h proměnné. Proměnná $h je vytvořen v každé z relací v $s, ale neexistuje v místní relaci.

```
Invoke-Command -Session $s {$h = Get-HotFix}
```

Nyní můžete v proměnné $h v dalších příkazech, jako je třeba následující data. Výsledky jsou zobrazeny v místním počítači.

```
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a>Pokročilé vzdálené komunikace
Vzdálená správa prostředí Windows PowerShell začíná právě tady. Pomocí rutin nainstalován pomocí prostředí Windows PowerShell můžete vytvořit a nakonfigurovat vzdálené relace z místních i vzdálených zakončení, vytvoření relace přizpůsobené a s omezeným přístupem, povolte uživatelům importovat příkazy ze vzdálené relace, které ve skutečnosti spuštěna implicitně na ke vzdálené relaci, nakonfigurujte zabezpečení vzdálené relace a mnoho dalšího.

Pro usnadnění konfigurace vzdáleného, prostředí Windows PowerShell obsahuje poskytovatele WSMan. WSMAN: jednotku, která se vytvoří zprostředkovatel umožňuje procházet hierarchie konfigurační nastavení v místním počítači a vzdálených počítačů.
Další informace o poskytovateli WSMan najdete v tématu [WSMan zprostředkovatele](https://technet.microsoft.com/en-us/library/dd819476.aspx) a [o rutiny WS-Management](https://technet.microsoft.com/en-us/library/dd819481.aspx), nebo v konzole Windows PowerShell, zadejte "Get-Help wsman".

Další informace viz:
- [O vzdálené – nejčastější dotazy](https://technet.microsoft.com/en-us/library/dd315359.aspx)
- [Register-PSSessionConfiguration](https://go.microsoft.com/fwlink/?LinkId=821508)
- [Import-PSSession](https://go.microsoft.com/fwlink/?LinkId=821821)

Pomoc s chybami vzdálenou komunikaci, najdete v tématu [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx).

## <a name="see-also"></a>Viz také
- [about_Remote](https://technet.microsoft.com/en-us/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [about_Remote_FAQ](https://technet.microsoft.com/en-us/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [about_Remote_Requirements](https://technet.microsoft.com/en-us/library/da213949-134c-4741-b307-81f4492ba1bd)
- [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [about_PSSessions](https://technet.microsoft.com/en-us/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [about_WS Management_Cmdlets](https://technet.microsoft.com/en-us/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493)
- [Import-PSSession](https://go.microsoft.com/fwlink/?LinkId=821821)
- [Nový PSSession](https://go.microsoft.com/fwlink/?LinkId=821498)
- [Register-PSSessionConfiguration](https://go.microsoft.com/fwlink/?LinkId=821508)
- [Zprostředkovatel služby WSMan](https://technet.microsoft.com/en-us/library/66fe1241-e08f-49ca-832f-a84c33ca8735)

[wsman-remoting]: WSMan-Remoting-in-PowerShell-Core.md
[ssh-resmoting]: SSH-Remoting-in-PowerShell-Core.md
