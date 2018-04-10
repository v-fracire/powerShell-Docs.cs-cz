---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Provádění síťových úloh
ms.assetid: a43cc55f-70c1-45c8-9467-eaad0d57e3b5
ms.openlocfilehash: 64c57c95a70bc4cad4b695a59d96673ed18afdf4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="performing-networking-tasks"></a>Provádění síťových úloh

Protože TCP/IP je nejčastěji používanou síťový protokol, zahrnují většinu úloh správy sítě nízké úrovně protokol TCP/IP. V této části jsme pomocí prostředí Windows PowerShell a WMI provádět tyto úlohy.

### <a name="listing-ip-addresses-for-a-computer"></a>Seznam IP adres pro počítač

Pokud chcete získat všechny IP adresy používané v místním počítači, použijte následující příkaz:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Format-Table -Property IPAddress
```

Výstup tohoto příkazu se liší od většina seznamech vlastností, protože hodnoty jsou uzavřené do složených závorek:

```output
IPAddress
---------
{192.168.1.80}
{192.168.148.1}
{192.168.171.1}
{0.0.0.0}
```

Zjistit, proč se zobrazuje složené závorky, použijte rutinu Get-člen prozkoumat **IPAddress** vlastnost:

```
PS> Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Get-Member -Name IPAddress


TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapterConfiguration

Name      MemberType Definition
----      ---------- ----------
IPAddress Property   System.String[] IPAddress {get;}
```

Vlastnost IP adresa pro každý síťový adaptér je ve skutečnosti pole. V definici složené závorky označuje, že **IPAddress** není **System.String** hodnoty, ale pole **System.String** hodnoty.

### <a name="listing-ip-configuration-data"></a>Výpis dat konfigurace IP adresy

Pokud chcete zobrazit podrobné data konfigurace protokolu IP pro každý síťový adaptér, použijte následující příkaz:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName .
```

Výchozí zobrazení pro objekt konfigurace síťového adaptéru je velmi omezená sada dostupné informace. Pro hloubkové kontrole a řešení potíží použijte Select-Object nebo formátování rutinu, jako je například Format-List, k určení vlastností, který se má zobrazit.

Pokud vás zajímá není ve vlastnostech protokolu IPX nebo WINS – pravděpodobně velká písmena v síti TCP/IP moderní – parametr ExcludeProperty Select-Object můžete skrýt vlastnosti s názvy začínajícími řetězcem "WINS" nebo "IPX:"

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

Tento příkaz vrátí podrobné informace o směrování DHCP, DNS a další dílčí vlastnosti konfigurace IP.

### <a name="pinging-computers"></a>Příkaz ping počítače

Můžete provádět jednoduché ping proti počítači pomocí podle **Win32_PingStatus**. Následující příkaz provede příkazem ping, ale vrátí zdlouhavé výstup:

```powershell
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

Užitečnější formulář pro souhrnné informace zobrazení z vlastností adresu, ResponseTime a StatusCode generovaná pomocí následujícího příkazu. Parametr Autosize Format-Table změní velikost sloupců tabulky, aby se zobrazí správně v prostředí Windows PowerShell.

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
```

StatusCode 0 označuje úspěšný příkaz ping.

Pole můžete použít k otestování příkazem ping více počítačů pomocí jediného příkazu. Protože je víc než jednou adresou, použijte **ForEach-Object** na příkaz ping adresu každého samostatně:

```powershell
'127.0.0.1','localhost','research.microsoft.com' | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

Můžete použít stejný formát příkaz ping všechny počítače v podsíti, jako jsou privátní sítě, které používá číslo sítě 192.168.1.0 a standardní maska podsítě třídy C (255.255.255.0)., jsou pouze adresy v rozsahu 192.168.1.1 až 192.168.1.254 oprávněné místní adresy (0 je vždy vyhrazené pro číslo sítě a 255 je adresu všesměrového vysílání podsítě).

Chcete-li představují pole čísel od 1 do 254 v prostředí Windows PowerShell, použijte příkaz **1..254.** Generování pole a pak přidáním hodnoty do adresu částečné v příkazu ping je možné provádět ping dokončení podsítě:

```powershell
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

Poznamenat, že tato technika pro generování rozsah adres můžete použít také jinde. Tímto způsobem můžete vygenerovat kompletní sadu adresy:

```powershell
$ips = 1..254 | ForEach-Object -Process {'192.168.1.' + $_}
```

### <a name="retrieving-network-adapter-properties"></a>Načítání vlastností síťového adaptéru

Dříve v této uživatelské příručce jsme uvedeno, zda může načíst vlastnosti Obecné konfigurace pomocí **Win32_NetworkAdapterConfiguration**. I když nejedná striktně informace protokolu TCP/IP, informace o síťového adaptéru jako je například MAC adres a typy adaptéru může být užitečná pro pochopení, co se děje s počítačem. Souhrn tyto informace získáte pomocí následujícího příkazu:

```powershell
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

### <a name="assigning-the-dns-domain-for-a-network-adapter"></a>Přiřazení domény DNS pro síťový adaptér

Chcete-li přiřadit doménu DNS automatického překladu IP adres, použijte **Win32_NetworkAdapterConfiguration SetDNSDomain** metoda. Protože nezávisle přiřadíte DNS domény pro každou konfiguraci síťového adaptéru, budete muset použít **ForEach-Object** příkaz přiřadit každý adaptér domény:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain('fabrikam.com') }
```

Příkaz filtrování "IPEnabled = $true" je nutné, protože to i v síti, která používá jenom protokol TCP/IP, řadu konfigurací síťových adaptérů v počítači není true TCP/IP adaptéry; jsou složky obecných softwarových podporující RAS, PPTP, technologie QoS a jiných služeb pro všechny adaptéry a proto nemají své vlastní adresy.

Příkaz můžete filtrovat pomocí **Where-Object** rutiny, místo použití **Get-WmiObject** filtru.

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain('fabrikam.com')}
```

### <a name="performing-dhcp-configuration-tasks"></a>Provádění úlohy konfigurace DHCP

Úprava DHCP podrobnosti součástí je práce se sadou síťových adaptérů, stejně jako konfiguraci serveru DNS. Existuje několik různých akcí, které můžete provádět pomocí rozhraní WMI a jsme bude procházet několik běžných ty.

#### <a name="determining-dhcp-enabled-adapters"></a>Určení adaptéry s podporou DHCP

Chcete-li najít adaptéry podporující službu DHCP na počítači, použijte následující příkaz:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName .
```

Vyloučit adaptéry s problémy s konfigurací protokolu IP, můžete načíst pouze adaptéry zapnutá IP adresa:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName .
```

#### <a name="retrieving-dhcp-properties"></a>Načítání vlastností DHCP

Protože vlastnosti týkající se služby DHCP pro adaptér obecně začínat řetězcem "DHCP", můžete pouze vlastnosti parametr vlastností formátu tabulky:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName . | Format-Table -Property DHCP*
```

#### <a name="enabling-dhcp-on-each-adapter"></a>Povolení protokol DHCP na každý adaptér

Pokud chcete povolit DHCP na všechny adaptéry, použijte následující příkaz:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

Můžete použít **filtru** příkaz "IPEnabled = $true a DHCPEnabled = $false" předejdete povolení DHCP, kde je již povolen, ale vynechejte tento krok nebude způsobit chyby.

#### <a name="releasing-and-renewing-dhcp-leases-on-specific-adapters"></a>Uvolnění a obnovení zapůjčení DHCP konkrétní síťové adaptéry

**Win32_NetworkAdapterConfiguration** třída má **ReleaseDHCPLease** a **RenewDHCPLease** metody. Jak se používají stejným způsobem. Obecně platí použijte tyto metody, pokud potřebujete jenom uvolnit nebo obnovit adresy pro adaptér v konkrétní podsíti. Nejjednodušší způsob, jak filtr adaptéry v podsíti je vybrat pouze adaptér konfigurace, které použití brány pro tuto podsíť. Například následující příkaz uvolní všechny zapůjčení DHCP adaptérům v místním počítači, které jsou získání zapůjčení DHCP ze 192.168.1.254:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

Jedinou změnou pro obnovení zapůjčení DHCP je použití **RenewDHCPLease** metoda místo **ReleaseDHCPLease** metoda:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> Při použití těchto metod ve vzdáleném počítači, mějte na paměti, že pokud jste připojení k němu pomocí adaptéru vydaná nebo obnovené zapůjčení, můžete ztratit přístup ke vzdálenému systému.

#### <a name="releasing-and-renewing-dhcp-leases-on-all-adapters"></a>Uvolnění a obnovení zapůjčení DHCP na všechny adaptéry

Globální verze adres DHCP nebo obnovení můžete provést na všechny adaptéry pomocí **Win32_NetworkAdapterConfiguration** metody, **ReleaseDHCPLeaseAll** a **RenewDHCPLeaseAll** . Ale příkaz se musí vztahovat na třídu služby WMI, nikoli konkrétní adaptér, protože uvolnění a obnovení zapůjčení globálně provádí na třídu, nikoli na konkrétní adaptér.

Odkaz na rozhraní WMI tříd, namísto instancí třídy, můžete získat podle výpis všech tříd WMI a pak vyberte požadovanou třídu podle názvu. Například následující příkaz vrátí třídy Win32_NetworkAdapterConfiguration:

```powershell
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'}
```

Lze považovat za celý příkaz třídy a pak vyvolejte **ReleaseDHCPAdapterLease** metoda na něm. V následujícím příkazu závorky kolem **Get-WmiObject** a **Where-Object** kanálu elementy přímé prostředí Windows PowerShell je nejdřív vyhodnotit:

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).ReleaseDHCPLeaseAll()
```

Můžete použít stejný formát příkaz má být vyvolán **RenewDHCPLeaseAll** metoda:

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).RenewDHCPLeaseAll()
```

### <a name="creating-a-network-share"></a>Vytvoření sdílené síťové složky

K vytvoření sdílené síťové složky, použijte **Win32_Share vytvořit** metoda:

```powershell
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq 'Win32_Share'}).Create('C:\temp','TempShare',0,25,'test share of the temp folder')
```

Můžete také vytvořit sdílenou složku pomocí **příkaz net share** v prostředí Windows PowerShell:

```powershell
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

### <a name="removing-a-network-share"></a>Odebráním sdílené síťové složky

Odebráním sdílené síťové složky s **Win32_Share**, ale proces mírně lišit od vytvoření sdílené složky, protože je potřeba načíst konkrétní sdílenou složku na odebrat, místo **Win32_Share** Třída. Následující příkaz odstraní sdílenou složku "TempShare":

```powershell
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

**Příkaz net share** funguje také:

```
PS> net share tempshare /delete

tempshare was deleted successfully.
```

### <a name="connecting-a-windows-accessible-network-drive"></a>Připojení Windows dostupné síťové jednotky

**New-PSDrive** rutin vytvoří jednotku prostředí Windows PowerShell, ale jednotky vytvořené tímto způsobem jsou k dispozici pouze pro prostředí Windows PowerShell. Pokud chcete vytvořit nový síťová jednotka, můžete použít **WScript.Network** objektu COM. Následující příkaz mapuje sdílenou složku \\ \\FPS01\\uživatelům místní disk B:

```powershell
(New-Object -ComObject WScript.Network).MapNetworkDrive('B:', '\\FPS01\users')
```

**Net použití** příkaz lze použít také:

```powershell
net use B: \\FPS01\users
```

Jednotky namapované s buď **WScript.Network** nebo příkazu net use jsou okamžitě k dispozici pro prostředí Windows PowerShell.