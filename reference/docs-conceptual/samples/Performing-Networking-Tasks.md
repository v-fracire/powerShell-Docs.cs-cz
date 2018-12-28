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
# <a name="performing-networking-tasks"></a><span data-ttu-id="f48d7-103">Provádění síťových úloh</span><span class="sxs-lookup"><span data-stu-id="f48d7-103">Performing Networking Tasks</span></span>

<span data-ttu-id="f48d7-104">Protože TCP/IP je nejčastěji používanou síťový protokol, zahrnují většinu úkolů správy nižší úrovně sítě protokolu TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="f48d7-104">Because TCP/IP is the most commonly used network protocol, most low-level network protocol administration tasks involve TCP/IP.</span></span> <span data-ttu-id="f48d7-105">V této části jsme pomocí prostředí Windows PowerShell a rozhraní WMI k provedení těchto úloh.</span><span class="sxs-lookup"><span data-stu-id="f48d7-105">In this section, we use Windows PowerShell and WMI to do these tasks.</span></span>

### <a name="listing-ip-addresses-for-a-computer"></a><span data-ttu-id="f48d7-106">Seznam IP adres pro počítače</span><span class="sxs-lookup"><span data-stu-id="f48d7-106">Listing IP Addresses for a Computer</span></span>

<span data-ttu-id="f48d7-107">Pokud chcete získat všechny IP adresy používané v místním počítači, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="f48d7-107">To get all IP addresses in use on the local computer, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Format-Table -Property IPAddress
```

<span data-ttu-id="f48d7-108">Výstup tohoto příkazu se liší od většiny seznamech vlastností, protože hodnoty jsou uzavřeny ve složených závorkách:</span><span class="sxs-lookup"><span data-stu-id="f48d7-108">The output of this command differs from most property lists, because values are enclosed in braces:</span></span>

```output
IPAddress
---------
{192.168.1.80}
{192.168.148.1}
{192.168.171.1}
{0.0.0.0}
```

<span data-ttu-id="f48d7-109">Abyste pochopili, proč se zobrazí složené závorky, použijte rutinu Get-Member k prozkoumání **IPAddress** vlastnost:</span><span class="sxs-lookup"><span data-stu-id="f48d7-109">To understand why the braces appear, use the Get-Member cmdlet to examine the **IPAddress** property:</span></span>

```
PS> Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Get-Member -Name IPAddress


TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapterConfiguration

Name      MemberType Definition
----      ---------- ----------
IPAddress Property   System.String[] IPAddress {get;}
```

<span data-ttu-id="f48d7-110">Vlastnost IP adresa pro každý síťový adaptér je ve skutečnosti pole.</span><span class="sxs-lookup"><span data-stu-id="f48d7-110">The IPAddress property for each network adapter is actually an array.</span></span> <span data-ttu-id="f48d7-111">Složené závorky v definici označuje, že **IPAddress** není **System.String** hodnotu, ale pole **System.String** hodnoty.</span><span class="sxs-lookup"><span data-stu-id="f48d7-111">The braces in the definition indicate that **IPAddress** is not a **System.String** value, but an array of **System.String** values.</span></span>

### <a name="listing-ip-configuration-data"></a><span data-ttu-id="f48d7-112">Výpis dat konfigurace IP adresy</span><span class="sxs-lookup"><span data-stu-id="f48d7-112">Listing IP Configuration Data</span></span>

<span data-ttu-id="f48d7-113">Chcete-li zobrazit podrobné data konfigurace protokolu IP pro každý síťový adaptér, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="f48d7-113">To display detailed IP configuration data for each network adapter, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName .
```

<span data-ttu-id="f48d7-114">Výchozí zobrazení pro objekt konfigurace síťového adaptéru je velmi omezenou sadu dostupné informace.</span><span class="sxs-lookup"><span data-stu-id="f48d7-114">The default display for the network adapter configuration object is a very reduced set of the available information.</span></span> <span data-ttu-id="f48d7-115">Pro důkladnou kontrolu a řešení potíží použijte k určení vlastností, který se má zobrazit Select-Object nebo formátování rutin, jako je například Format-List.</span><span class="sxs-lookup"><span data-stu-id="f48d7-115">For in-depth inspection and troubleshooting, use Select-Object or a formatting cmdlet, such as Format-List, to specify the properties to be displayed.</span></span>

<span data-ttu-id="f48d7-116">Pokud vás nezajímají ve vlastnostech protokolu IPX nebo WINS – pravděpodobně případ v síti TCP/IP moderní – parametr ExcludeProperty Select-Object můžete skrýt vlastnosti s názvy začínajícími řetězcem "WINS" nebo "IPX:"</span><span class="sxs-lookup"><span data-stu-id="f48d7-116">If you are not interested in IPX or WINS properties—probably the case in a modern TCP/IP network—you can use the ExcludeProperty parameter of Select-Object to hide properties with names that begin with "WINS" or "IPX:"</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

<span data-ttu-id="f48d7-117">Tento příkaz vrátí podrobné informace o směrování DHCP, DNS a další vedlejší vlastnosti konfigurace IP.</span><span class="sxs-lookup"><span data-stu-id="f48d7-117">This command returns detailed information about DHCP, DNS, routing, and other minor IP configuration properties.</span></span>

### <a name="pinging-computers"></a><span data-ttu-id="f48d7-118">Příkaz ping počítače</span><span class="sxs-lookup"><span data-stu-id="f48d7-118">Pinging Computers</span></span>

<span data-ttu-id="f48d7-119">Můžete provést jednoduché ping proti počítači pomocí podle **Win32_PingStatus**.</span><span class="sxs-lookup"><span data-stu-id="f48d7-119">You can perform a simple ping against a computer using by **Win32_PingStatus**.</span></span> <span data-ttu-id="f48d7-120">Následující příkaz provede příkaz ping, ale vrátí dlouhý výstup:</span><span class="sxs-lookup"><span data-stu-id="f48d7-120">The following command performs the ping, but returns lengthy output:</span></span>

```powershell
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

<span data-ttu-id="f48d7-121">Další užitečné formulář pro zobrazení souhrnných informací o vlastnosti adresy, čas odezvy a StatusCode vygenerovaný pomocí následujícího příkazu.</span><span class="sxs-lookup"><span data-stu-id="f48d7-121">A more useful form for summary information a display of the Address, ResponseTime, and StatusCode properties, as generated by the following command.</span></span> <span data-ttu-id="f48d7-122">Automaticky přizpůsobit velikost parametru Format-Table změní velikost sloupců tabulky tak, aby se zobrazí správně v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f48d7-122">The Autosize parameter of Format-Table resizes the table columns so that they display properly in Windows PowerShell.</span></span>

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
```

<span data-ttu-id="f48d7-123">StatusCode má hodnotu 0 indikuje úspěšné provedení příkazu ping.</span><span class="sxs-lookup"><span data-stu-id="f48d7-123">A StatusCode of 0 indicates a successful ping.</span></span>

<span data-ttu-id="f48d7-124">Pole můžete použít příkaz ping více počítačů pomocí jediného příkazu.</span><span class="sxs-lookup"><span data-stu-id="f48d7-124">You can use an array to ping multiple computers with a single command.</span></span> <span data-ttu-id="f48d7-125">Vzhledem k tomu, že existuje více než jednu adresu, použít **ForEach-Object** pro odeslání příkazu ping adresu každého samostatně:</span><span class="sxs-lookup"><span data-stu-id="f48d7-125">Because there is more than one address, use the **ForEach-Object** to ping each address separately:</span></span>

```powershell
'127.0.0.1','localhost','research.microsoft.com' | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

<span data-ttu-id="f48d7-126">K otestování příkazem ping všechny počítače v podsíti, jako je například privátní síti, která používá číslo 192.168.1.0 sítě a masky podsítě standardní třídy C (255.255.255.0) můžete použít stejný formát příkazu., jsou pouze adresy v rozsahu 192.168.1.1 až 192.168.1.254 oprávněné místních adres (0 je vždy vyhrazena pro číslo sítě a 255 je adresa všesměrového vysílání podsítě).</span><span class="sxs-lookup"><span data-stu-id="f48d7-126">You can use the same command format to ping all of the computers on a subnet, such as a private network that uses network number 192.168.1.0 and a standard Class C subnet mask (255.255.255.0)., Only addresses in the range of 192.168.1.1 through 192.168.1.254 are legitimate local addresses (0 is always reserved for the network number and 255 is a subnet broadcast address).</span></span>

<span data-ttu-id="f48d7-127">K reprezentaci pole čísel od 1 do 254 v prostředí Windows PowerShell, použijte příkaz **1..254.**</span><span class="sxs-lookup"><span data-stu-id="f48d7-127">To represent an array of the numbers from 1 through 254 in Windows PowerShell, use the statement **1..254.**</span></span> <span data-ttu-id="f48d7-128">Generování pole a následným přidáním hodnoty do částečné adresu v příkazu ping lze provést odeslání příkazu ping kompletní podsítě:</span><span class="sxs-lookup"><span data-stu-id="f48d7-128">A complete subnet ping can be performed by generating the array and then adding the values onto a partial address in the ping statement:</span></span>

```powershell
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

<span data-ttu-id="f48d7-129">Všimněte si, že tento postup pro generování rozsah adres můžete použít i jinde.</span><span class="sxs-lookup"><span data-stu-id="f48d7-129">Note that this technique for generating a range of addresses can be used elsewhere as well.</span></span> <span data-ttu-id="f48d7-130">Tímto způsobem můžete vygenerovat kompletní sadu adresy:</span><span class="sxs-lookup"><span data-stu-id="f48d7-130">You can generate a complete set of addresses in this way:</span></span>

```powershell
$ips = 1..254 | ForEach-Object -Process {'192.168.1.' + $_}
```

### <a name="retrieving-network-adapter-properties"></a><span data-ttu-id="f48d7-131">Načítají se vlastnosti síťového adaptéru</span><span class="sxs-lookup"><span data-stu-id="f48d7-131">Retrieving Network Adapter Properties</span></span>

<span data-ttu-id="f48d7-132">Dříve v této uživatelské příručce už jsme zmínili, že by mohla načíst vlastnosti Obecné konfigurace pomocí **Win32_NetworkAdapterConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="f48d7-132">Earlier in this user's guide, we mentioned that you could retrieve general configuration properties by using **Win32_NetworkAdapterConfiguration**.</span></span> <span data-ttu-id="f48d7-133">I když se nejedná vyloženě TCP/IP informace, informace o síťového adaptéru jako jsou MAC adres a typy adaptéru může být užitečné pro pochopení, co se děje s počítačem.</span><span class="sxs-lookup"><span data-stu-id="f48d7-133">Although not strictly TCP/IP information, network adapter information such as MAC addresses and adapter types can be useful for understanding what is going on with a computer.</span></span> <span data-ttu-id="f48d7-134">Přehled tyto informace získáte pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="f48d7-134">To get a summary of this information, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

### <a name="assigning-the-dns-domain-for-a-network-adapter"></a><span data-ttu-id="f48d7-135">Přiřazení domény DNS pro síťový adaptér</span><span class="sxs-lookup"><span data-stu-id="f48d7-135">Assigning the DNS Domain for a Network Adapter</span></span>

<span data-ttu-id="f48d7-136">Chcete-li přiřadit domény DNS pro překlad názvů automatické, použijte **Win32_NetworkAdapterConfiguration SetDNSDomain** metody.</span><span class="sxs-lookup"><span data-stu-id="f48d7-136">To assign the DNS domain for automatic name resolution, use the **Win32_NetworkAdapterConfiguration SetDNSDomain** method.</span></span> <span data-ttu-id="f48d7-137">Vzhledem k tomu, že je doména DNS pro každou konfiguraci síťového adaptéru přiřadit nezávisle na sobě, budete muset použít **ForEach-Object** příkaz každého adaptéru přiřadit domény:</span><span class="sxs-lookup"><span data-stu-id="f48d7-137">Because you assign the DNS domain for each network adapter configuration independently, you need to use a **ForEach-Object** statement to assign the domain to each adapter:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain('fabrikam.com') }
```

<span data-ttu-id="f48d7-138">Filtrování příkaz "IPEnabled = $true" je nezbytné, protože i v síti, která používá jenom protokol TCP/IP, řadu konfigurací síťových adaptérů v počítači není true TCP/IP adaptéry; jsou obecné softwarovými prvky podpůrných RAS, PPTP, technologie QoS a jinými službami pro všechny adaptéry a proto nemají své vlastní adresu.</span><span class="sxs-lookup"><span data-stu-id="f48d7-138">The filtering statement "IPEnabled=$true" is necessary, because even on a network that uses only TCP/IP, several of the network adapter configurations on a computer are not true TCP/IP adapters; they are general software elements supporting RAS, PPTP, QoS, and other services for all adapters and thus do not have an address of their own.</span></span>

<span data-ttu-id="f48d7-139">Tento příkaz lze filtrovat pomocí **Where-Object** rutiny, namísto použití **Get-WmiObject** filtru.</span><span class="sxs-lookup"><span data-stu-id="f48d7-139">You can filter the command by using the **Where-Object** cmdlet, instead of using the **Get-WmiObject** filter.</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain('fabrikam.com')}
```

### <a name="performing-dhcp-configuration-tasks"></a><span data-ttu-id="f48d7-140">Provádění úlohy konfigurace DHCP</span><span class="sxs-lookup"><span data-stu-id="f48d7-140">Performing DHCP Configuration Tasks</span></span>

<span data-ttu-id="f48d7-141">Úprava podrobností DHCP součástí je práce se sadou síťových adaptérů, stejně jako konfiguraci serveru DNS.</span><span class="sxs-lookup"><span data-stu-id="f48d7-141">Modifying DHCP details involves working with a set of network adapters, just as the DNS configuration does.</span></span> <span data-ttu-id="f48d7-142">Existuje několik různých akcí, které můžete provést pomocí rozhraní WMI a jsme přesune se krokování přes několik běžných struktur.</span><span class="sxs-lookup"><span data-stu-id="f48d7-142">There are several distinct actions you can perform by using WMI, and we will step through a few of the common ones.</span></span>

#### <a name="determining-dhcp-enabled-adapters"></a><span data-ttu-id="f48d7-143">Určení adaptéry s povoleným protokolem DHCP</span><span class="sxs-lookup"><span data-stu-id="f48d7-143">Determining DHCP-Enabled Adapters</span></span>

<span data-ttu-id="f48d7-144">K vyhledání adaptéry povoleným protokolem DHCP na počítači, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="f48d7-144">To find the DHCP-enabled adapters on a computer, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName .
```

<span data-ttu-id="f48d7-145">Vyloučit adaptéry s problémy s konfigurací protokolu IP, můžete načíst pouze adaptéry povolenou adresou IP:</span><span class="sxs-lookup"><span data-stu-id="f48d7-145">To exclude adapters with IP configuration problems, you can retrieve only IP-enabled adapters:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName .
```

#### <a name="retrieving-dhcp-properties"></a><span data-ttu-id="f48d7-146">Načítání vlastností DHCP</span><span class="sxs-lookup"><span data-stu-id="f48d7-146">Retrieving DHCP Properties</span></span>

<span data-ttu-id="f48d7-147">Protože vlastnosti související se serverem DHCP pro adaptér obecně začínat "DHCP", můžete zobrazit pouze vlastnosti parametrem vlastnosti Format-Table:</span><span class="sxs-lookup"><span data-stu-id="f48d7-147">Because DHCP-related properties for an adapter generally begin with "DHCP," you can use the Property parameter of Format-Table to display only those properties:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName . | Format-Table -Property DHCP*
```

#### <a name="enabling-dhcp-on-each-adapter"></a><span data-ttu-id="f48d7-148">Povolení serveru DHCP na každý adaptér</span><span class="sxs-lookup"><span data-stu-id="f48d7-148">Enabling DHCP on Each Adapter</span></span>

<span data-ttu-id="f48d7-149">Pokud chcete povolit DHCP na všechny adaptéry, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="f48d7-149">To enable DHCP on all adapters, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

<span data-ttu-id="f48d7-150">Můžete použít **filtr** příkaz "IPEnabled = $true a DHCPEnabled = $false" aby se zabránilo povolení serveru DHCP, kde už je povolená, ale vynechá tento krok nebude způsobovat chyby.</span><span class="sxs-lookup"><span data-stu-id="f48d7-150">You can use the **Filter** statement "IPEnabled=$true and DHCPEnabled=$false" to avoid enabling DHCP where it is already enabled, but omitting this step will not cause errors.</span></span>

#### <a name="releasing-and-renewing-dhcp-leases-on-specific-adapters"></a><span data-ttu-id="f48d7-151">Uvolnění a obnovovat zapůjčení DHCP konkrétní síťové adaptéry</span><span class="sxs-lookup"><span data-stu-id="f48d7-151">Releasing and Renewing DHCP Leases on Specific Adapters</span></span>

<span data-ttu-id="f48d7-152">**Win32_NetworkAdapterConfiguration** třída má **ReleaseDHCPLease** a **RenewDHCPLease** metody.</span><span class="sxs-lookup"><span data-stu-id="f48d7-152">The **Win32_NetworkAdapterConfiguration** class has **ReleaseDHCPLease** and **RenewDHCPLease** methods.</span></span> <span data-ttu-id="f48d7-153">Jak se používají stejným způsobem.</span><span class="sxs-lookup"><span data-stu-id="f48d7-153">Both are used in the same way.</span></span> <span data-ttu-id="f48d7-154">Tyto metody použijte obecně platí, pouze je potřeba uvolnit nebo obnovit adresy pro adaptér v určité podsíti.</span><span class="sxs-lookup"><span data-stu-id="f48d7-154">In general, use these methods if you only need to release or renew addresses for an adapter on a specific subnet.</span></span> <span data-ttu-id="f48d7-155">Nejjednodušší způsob, jak filtr adaptéry v podsíti je zvolit pouze konfigurací adaptérů, které používají pro tuto podsíť brány.</span><span class="sxs-lookup"><span data-stu-id="f48d7-155">The easiest way to filter adapters on a subnet is to choose only the adapter configurations that use the gateway for that subnet.</span></span> <span data-ttu-id="f48d7-156">Například následující příkaz uvolní všechny zapůjčení DHCP adaptérům na místním počítači, které jsou získávání zapůjčení DHCP ze 192.168.1.254:</span><span class="sxs-lookup"><span data-stu-id="f48d7-156">For example, the following command releases all DHCP leases on adapters on the local computer that are obtaining DHCP leases from 192.168.1.254:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

<span data-ttu-id="f48d7-157">Jediná změna pro obnovení zapůjčení DHCP, je použít **RenewDHCPLease** metoda místo **ReleaseDHCPLease** metody:</span><span class="sxs-lookup"><span data-stu-id="f48d7-157">The only change for renewing a DHCP lease is to use the **RenewDHCPLease** method instead of the **ReleaseDHCPLease** method:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> <span data-ttu-id="f48d7-158">Při použití těchto metod na vzdáleném počítači, mějte na paměti, že pokud jste připojení k němu prostřednictvím adaptéru s vydané nebo obnovit zapůjčení, můžete ztratit přístup ke vzdálenému systému.</span><span class="sxs-lookup"><span data-stu-id="f48d7-158">When using these methods on a remote computer, be aware that you can lose access to the remote system if you are connected to it through the adapter with the released or renewed lease.</span></span>

#### <a name="releasing-and-renewing-dhcp-leases-on-all-adapters"></a><span data-ttu-id="f48d7-159">Uvolnění a obnovovat zapůjčení DHCP na všechny adaptéry</span><span class="sxs-lookup"><span data-stu-id="f48d7-159">Releasing and Renewing DHCP Leases on All Adapters</span></span>

<span data-ttu-id="f48d7-160">Globální verze adres DHCP nebo obnovení můžete provádět na všechny adaptéry pomocí **Win32_NetworkAdapterConfiguration** metody, **ReleaseDHCPLeaseAll** a **RenewDHCPLeaseAll** .</span><span class="sxs-lookup"><span data-stu-id="f48d7-160">You can perform global DHCP address releases or renewals on all adapters by using the **Win32_NetworkAdapterConfiguration** methods, **ReleaseDHCPLeaseAll** and **RenewDHCPLeaseAll**.</span></span> <span data-ttu-id="f48d7-161">Ale příkazu musí použít na třídu rozhraní WMI, nikoli konkrétní adaptér, protože uvolnění a globálně obnovení zapůjčení se provádí na třídy, ne na konkrétní adaptér, je.</span><span class="sxs-lookup"><span data-stu-id="f48d7-161">However, the command must apply to the WMI class, rather than a particular adapter, because releasing and renewing leases globally is performed on the class, not on a specific adapter.</span></span>

<span data-ttu-id="f48d7-162">Odkaz na třídu služby WMI místo instance třídy, můžete získat tak, že výpis všech třídy služby WMI a pak vyberete požadovanou třídu podle názvu.</span><span class="sxs-lookup"><span data-stu-id="f48d7-162">You can get a reference to a WMI class, instead of class instances, by listing all WMI classes and then selecting only the desired class by name.</span></span> <span data-ttu-id="f48d7-163">Například následující příkaz vrátí třídy Win32_NetworkAdapterConfiguration:</span><span class="sxs-lookup"><span data-stu-id="f48d7-163">For example, the following command returns the Win32_NetworkAdapterConfiguration class:</span></span>

```powershell
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'}
```

<span data-ttu-id="f48d7-164">Lze považovat za celý příkaz třídy a pak vyvolejte **ReleaseDHCPAdapterLease** metoda na něj.</span><span class="sxs-lookup"><span data-stu-id="f48d7-164">You can treat the entire command as the class and then invoke the **ReleaseDHCPAdapterLease** method on it.</span></span> <span data-ttu-id="f48d7-165">V následujícím příkazu závorky kolem **Get-WmiObject** a **Where-Object** kanálu prvky přímé prostředí Windows PowerShell budou vyhodnoceny nejdřív:</span><span class="sxs-lookup"><span data-stu-id="f48d7-165">In the following command, the parentheses surrounding the **Get-WmiObject** and **Where-Object** pipeline elements direct Windows PowerShell to evaluate them first:</span></span>

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).ReleaseDHCPLeaseAll()
```

<span data-ttu-id="f48d7-166">Stejný formát příkaz můžete použít k vyvolání **RenewDHCPLeaseAll** metody:</span><span class="sxs-lookup"><span data-stu-id="f48d7-166">You can use the same command format to invoke the **RenewDHCPLeaseAll** method:</span></span>

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).RenewDHCPLeaseAll()
```

### <a name="creating-a-network-share"></a><span data-ttu-id="f48d7-167">Vytvoření sdílené síťové složky</span><span class="sxs-lookup"><span data-stu-id="f48d7-167">Creating a Network Share</span></span>

<span data-ttu-id="f48d7-168">Chcete-li vytvořit sdílené síťové složce, použijte **Win32_Share vytvořit** metody:</span><span class="sxs-lookup"><span data-stu-id="f48d7-168">To create a network share, use the **Win32_Share Create** method:</span></span>

```powershell
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq 'Win32_Share'}).Create('C:\temp','TempShare',0,25,'test share of the temp folder')
```

<span data-ttu-id="f48d7-169">Můžete také vytvořit sdílenou složku pomocí **příkaz net share** v prostředí Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f48d7-169">You can also create the share by using **net share** in Windows PowerShell:</span></span>

```powershell
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

### <a name="removing-a-network-share"></a><span data-ttu-id="f48d7-170">Odebráním sdílené síťové složky</span><span class="sxs-lookup"><span data-stu-id="f48d7-170">Removing a Network Share</span></span>

<span data-ttu-id="f48d7-171">Můžete odebrat sdílené síťové složky s **Win32_Share**, je mírně liší od vytvoření sdílené složky, protože je potřeba získat konkrétní sdílenou složku k odebrání, ale místo **Win32_Share** Třída.</span><span class="sxs-lookup"><span data-stu-id="f48d7-171">You can remove a network share with **Win32_Share**, but the process is slightly different from creating a share, because you need to retrieve the specific share to be removed, rather than the **Win32_Share** class.</span></span> <span data-ttu-id="f48d7-172">Následující příkaz odstraní sdílenou složku "TempShare":</span><span class="sxs-lookup"><span data-stu-id="f48d7-172">The following statement deletes the share "TempShare":</span></span>

```powershell
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

<span data-ttu-id="f48d7-173">**Příkaz net share** také funguje:</span><span class="sxs-lookup"><span data-stu-id="f48d7-173">**Net share** works as well:</span></span>

```
PS> net share tempshare /delete

tempshare was deleted successfully.
```

### <a name="connecting-a-windows-accessible-network-drive"></a><span data-ttu-id="f48d7-174">Připojení Windows dostupná síťová jednotka</span><span class="sxs-lookup"><span data-stu-id="f48d7-174">Connecting a Windows Accessible Network Drive</span></span>

<span data-ttu-id="f48d7-175">**New-PSDrive** rutin vytvoří jednotku prostředí Windows PowerShell, ale disky vytvořené tímto způsobem jsou k dispozici pouze pro prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f48d7-175">The **New-PSDrive** cmdlets creates a Windows PowerShell drive, but drives created this way are available only to Windows PowerShell.</span></span> <span data-ttu-id="f48d7-176">Chcete-li vytvořit nové síťové jednotce, můžete použít **WScript.Network** objekt modelu COM.</span><span class="sxs-lookup"><span data-stu-id="f48d7-176">To create a new networked drive, you can use the **WScript.Network** COM object.</span></span> <span data-ttu-id="f48d7-177">Následující příkaz se mapuje sdílenou složku \\ \\FPS01\\uživatele na místní disk B:</span><span class="sxs-lookup"><span data-stu-id="f48d7-177">The following command maps the share \\\\FPS01\\users to local drive B:</span></span>

```powershell
(New-Object -ComObject WScript.Network).MapNetworkDrive('B:', '\\FPS01\users')
```

<span data-ttu-id="f48d7-178">**Použití** příkaz lze také použít:</span><span class="sxs-lookup"><span data-stu-id="f48d7-178">The **net use** command works as well:</span></span>

```powershell
net use B: \\FPS01\users
```

<span data-ttu-id="f48d7-179">Jednotky mapované s oběma **WScript.Network** nebo příkaz net use jsou okamžitě dostupné prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f48d7-179">Drives mapped with either **WScript.Network** or net use are immediately available to Windows PowerShell.</span></span>