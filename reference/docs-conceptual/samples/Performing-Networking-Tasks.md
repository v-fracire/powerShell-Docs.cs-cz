---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Provádění síťových úloh
ms.assetid: a43cc55f-70c1-45c8-9467-eaad0d57e3b5
ms.openlocfilehash: 64c57c95a70bc4cad4b695a59d96673ed18afdf4
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404086"
---
# <a name="performing-networking-tasks"></a>Provádění síťových úloh

Protože TCP/IP je nejčastěji používanou síťový protokol, zahrnují většinu úkolů správy nižší úrovně sítě protokolu TCP/IP. V této části jsme pomocí prostředí Windows PowerShell a rozhraní WMI k provedení těchto úloh.

### <a name="listing-ip-addresses-for-a-computer"></a>Seznam IP adres pro počítače

Pokud chcete získat všechny IP adresy používané v místním počítači, použijte následující příkaz:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Format-Table -Property IPAddress
```

Výstup tohoto příkazu se liší od většiny seznamech vlastností, protože hodnoty jsou uzavřeny ve složených závorkách:

```output
IPAddress
---------
{192.168.1.80}
{192.168.148.1}
{192.168.171.1}
{0.0.0.0}
```

Abyste pochopili, proč se zobrazí složené závorky, použijte rutinu Get-Member k prozkoumání **IPAddress** vlastnost:

```
PS> Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Get-Member -Name IPAddress


TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapterConfiguration

Name      MemberType Definition
----      ---------- ----------
IPAddress Property   System.String[] IPAddress {get;}
```

Vlastnost IP adresa pro každý síťový adaptér je ve skutečnosti pole. Složené závorky v definici označuje, že **IPAddress** není **System.String** hodnotu, ale pole **System.String** hodnoty.

### <a name="listing-ip-configuration-data"></a>Výpis dat konfigurace IP adresy

Chcete-li zobrazit podrobné data konfigurace protokolu IP pro každý síťový adaptér, použijte následující příkaz:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName .
```

Výchozí zobrazení pro objekt konfigurace síťového adaptéru je velmi omezenou sadu dostupné informace. Pro důkladnou kontrolu a řešení potíží použijte k určení vlastností, který se má zobrazit Select-Object nebo formátování rutin, jako je například Format-List.

Pokud vás nezajímají ve vlastnostech protokolu IPX nebo WINS – pravděpodobně případ v síti TCP/IP moderní – parametr ExcludeProperty Select-Object můžete skrýt vlastnosti s názvy začínajícími řetězcem "WINS" nebo "IPX:"

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

Tento příkaz vrátí podrobné informace o směrování DHCP, DNS a další vedlejší vlastnosti konfigurace IP.

### <a name="pinging-computers"></a>Příkaz ping počítače

Můžete provést jednoduché ping proti počítači pomocí podle **Win32_PingStatus**. Následující příkaz provede příkaz ping, ale vrátí dlouhý výstup:

```powershell
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

Další užitečné formulář pro zobrazení souhrnných informací o vlastnosti adresy, čas odezvy a StatusCode vygenerovaný pomocí následujícího příkazu. Automaticky přizpůsobit velikost parametru Format-Table změní velikost sloupců tabulky tak, aby se zobrazí správně v prostředí Windows PowerShell.

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
```

StatusCode má hodnotu 0 indikuje úspěšné provedení příkazu ping.

Pole můžete použít příkaz ping více počítačů pomocí jediného příkazu. Vzhledem k tomu, že existuje více než jednu adresu, použít **ForEach-Object** pro odeslání příkazu ping adresu každého samostatně:

```powershell
'127.0.0.1','localhost','research.microsoft.com' | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

K otestování příkazem ping všechny počítače v podsíti, jako je například privátní síti, která používá číslo 192.168.1.0 sítě a masky podsítě standardní třídy C (255.255.255.0) můžete použít stejný formát příkazu., jsou pouze adresy v rozsahu 192.168.1.1 až 192.168.1.254 oprávněné místních adres (0 je vždy vyhrazena pro číslo sítě a 255 je adresa všesměrového vysílání podsítě).

K reprezentaci pole čísel od 1 do 254 v prostředí Windows PowerShell, použijte příkaz **1..254.** Generování pole a následným přidáním hodnoty do částečné adresu v příkazu ping lze provést odeslání příkazu ping kompletní podsítě:

```powershell
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

Všimněte si, že tento postup pro generování rozsah adres můžete použít i jinde. Tímto způsobem můžete vygenerovat kompletní sadu adresy:

```powershell
$ips = 1..254 | ForEach-Object -Process {'192.168.1.' + $_}
```

### <a name="retrieving-network-adapter-properties"></a>Načítají se vlastnosti síťového adaptéru

Dříve v této uživatelské příručce už jsme zmínili, že by mohla načíst vlastnosti Obecné konfigurace pomocí **Win32_NetworkAdapterConfiguration**. I když se nejedná vyloženě TCP/IP informace, informace o síťového adaptéru jako jsou MAC adres a typy adaptéru může být užitečné pro pochopení, co se děje s počítačem. Přehled tyto informace získáte pomocí následujícího příkazu:

```powershell
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

### <a name="assigning-the-dns-domain-for-a-network-adapter"></a>Přiřazení domény DNS pro síťový adaptér

Chcete-li přiřadit domény DNS pro překlad názvů automatické, použijte **Win32_NetworkAdapterConfiguration SetDNSDomain** metody. Vzhledem k tomu, že je doména DNS pro každou konfiguraci síťového adaptéru přiřadit nezávisle na sobě, budete muset použít **ForEach-Object** příkaz každého adaptéru přiřadit domény:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain('fabrikam.com') }
```

Filtrování příkaz "IPEnabled = $true" je nezbytné, protože i v síti, která používá jenom protokol TCP/IP, řadu konfigurací síťových adaptérů v počítači není true TCP/IP adaptéry; jsou obecné softwarovými prvky podpůrných RAS, PPTP, technologie QoS a jinými službami pro všechny adaptéry a proto nemají své vlastní adresu.

Tento příkaz lze filtrovat pomocí **Where-Object** rutiny, namísto použití **Get-WmiObject** filtru.

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain('fabrikam.com')}
```

### <a name="performing-dhcp-configuration-tasks"></a>Provádění úlohy konfigurace DHCP

Úprava podrobností DHCP součástí je práce se sadou síťových adaptérů, stejně jako konfiguraci serveru DNS. Existuje několik různých akcí, které můžete provést pomocí rozhraní WMI a jsme přesune se krokování přes několik běžných struktur.

#### <a name="determining-dhcp-enabled-adapters"></a>Určení adaptéry s povoleným protokolem DHCP

K vyhledání adaptéry povoleným protokolem DHCP na počítači, použijte následující příkaz:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName .
```

Vyloučit adaptéry s problémy s konfigurací protokolu IP, můžete načíst pouze adaptéry povolenou adresou IP:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName .
```

#### <a name="retrieving-dhcp-properties"></a>Načítání vlastností DHCP

Protože vlastnosti související se serverem DHCP pro adaptér obecně začínat "DHCP", můžete zobrazit pouze vlastnosti parametrem vlastnosti Format-Table:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName . | Format-Table -Property DHCP*
```

#### <a name="enabling-dhcp-on-each-adapter"></a>Povolení serveru DHCP na každý adaptér

Pokud chcete povolit DHCP na všechny adaptéry, použijte následující příkaz:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

Můžete použít **filtr** příkaz "IPEnabled = $true a DHCPEnabled = $false" aby se zabránilo povolení serveru DHCP, kde už je povolená, ale vynechá tento krok nebude způsobovat chyby.

#### <a name="releasing-and-renewing-dhcp-leases-on-specific-adapters"></a>Uvolnění a obnovovat zapůjčení DHCP konkrétní síťové adaptéry

**Win32_NetworkAdapterConfiguration** třída má **ReleaseDHCPLease** a **RenewDHCPLease** metody. Jak se používají stejným způsobem. Tyto metody použijte obecně platí, pouze je potřeba uvolnit nebo obnovit adresy pro adaptér v určité podsíti. Nejjednodušší způsob, jak filtr adaptéry v podsíti je zvolit pouze konfigurací adaptérů, které používají pro tuto podsíť brány. Například následující příkaz uvolní všechny zapůjčení DHCP adaptérům na místním počítači, které jsou získávání zapůjčení DHCP ze 192.168.1.254:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

Jediná změna pro obnovení zapůjčení DHCP, je použít **RenewDHCPLease** metoda místo **ReleaseDHCPLease** metody:

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> Při použití těchto metod na vzdáleném počítači, mějte na paměti, že pokud jste připojení k němu prostřednictvím adaptéru s vydané nebo obnovit zapůjčení, můžete ztratit přístup ke vzdálenému systému.

#### <a name="releasing-and-renewing-dhcp-leases-on-all-adapters"></a>Uvolnění a obnovovat zapůjčení DHCP na všechny adaptéry

Globální verze adres DHCP nebo obnovení můžete provádět na všechny adaptéry pomocí **Win32_NetworkAdapterConfiguration** metody, **ReleaseDHCPLeaseAll** a **RenewDHCPLeaseAll** . Ale příkazu musí použít na třídu rozhraní WMI, nikoli konkrétní adaptér, protože uvolnění a globálně obnovení zapůjčení se provádí na třídy, ne na konkrétní adaptér, je.

Odkaz na třídu služby WMI místo instance třídy, můžete získat tak, že výpis všech třídy služby WMI a pak vyberete požadovanou třídu podle názvu. Například následující příkaz vrátí třídy Win32_NetworkAdapterConfiguration:

```powershell
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'}
```

Lze považovat za celý příkaz třídy a pak vyvolejte **ReleaseDHCPAdapterLease** metoda na něj. V následujícím příkazu závorky kolem **Get-WmiObject** a **Where-Object** kanálu prvky přímé prostředí Windows PowerShell budou vyhodnoceny nejdřív:

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).ReleaseDHCPLeaseAll()
```

Stejný formát příkaz můžete použít k vyvolání **RenewDHCPLeaseAll** metody:

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).RenewDHCPLeaseAll()
```

### <a name="creating-a-network-share"></a>Vytvoření sdílené síťové složky

Chcete-li vytvořit sdílené síťové složce, použijte **Win32_Share vytvořit** metody:

```powershell
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq 'Win32_Share'}).Create('C:\temp','TempShare',0,25,'test share of the temp folder')
```

Můžete také vytvořit sdílenou složku pomocí **příkaz net share** v prostředí Windows PowerShell:

```powershell
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

### <a name="removing-a-network-share"></a>Odebráním sdílené síťové složky

Můžete odebrat sdílené síťové složky s **Win32_Share**, je mírně liší od vytvoření sdílené složky, protože je potřeba získat konkrétní sdílenou složku k odebrání, ale místo **Win32_Share** Třída. Následující příkaz odstraní sdílenou složku "TempShare":

```powershell
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

**Příkaz net share** také funguje:

```
PS> net share tempshare /delete

tempshare was deleted successfully.
```

### <a name="connecting-a-windows-accessible-network-drive"></a>Připojení Windows dostupná síťová jednotka

**New-PSDrive** rutin vytvoří jednotku prostředí Windows PowerShell, ale disky vytvořené tímto způsobem jsou k dispozici pouze pro prostředí Windows PowerShell. Chcete-li vytvořit nové síťové jednotce, můžete použít **WScript.Network** objekt modelu COM. Následující příkaz se mapuje sdílenou složku \\ \\FPS01\\uživatele na místní disk B:

```powershell
(New-Object -ComObject WScript.Network).MapNetworkDrive('B:', '\\FPS01\users')
```

**Použití** příkaz lze také použít:

```powershell
net use B: \\FPS01\users
```

Jednotky mapované s oběma **WScript.Network** nebo příkaz net use jsou okamžitě dostupné prostředí Windows PowerShell.