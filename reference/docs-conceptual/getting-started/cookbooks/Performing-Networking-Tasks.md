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
ms.locfileid: "30954122"
---
# <a name="performing-networking-tasks"></a><span data-ttu-id="fc261-103">Provádění síťových úloh</span><span class="sxs-lookup"><span data-stu-id="fc261-103">Performing Networking Tasks</span></span>

<span data-ttu-id="fc261-104">Protože TCP/IP je nejčastěji používanou síťový protokol, zahrnují většinu úloh správy sítě nízké úrovně protokol TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="fc261-104">Because TCP/IP is the most commonly used network protocol, most low-level network protocol administration tasks involve TCP/IP.</span></span> <span data-ttu-id="fc261-105">V této části jsme pomocí prostředí Windows PowerShell a WMI provádět tyto úlohy.</span><span class="sxs-lookup"><span data-stu-id="fc261-105">In this section, we use Windows PowerShell and WMI to do these tasks.</span></span>

### <a name="listing-ip-addresses-for-a-computer"></a><span data-ttu-id="fc261-106">Seznam IP adres pro počítač</span><span class="sxs-lookup"><span data-stu-id="fc261-106">Listing IP Addresses for a Computer</span></span>

<span data-ttu-id="fc261-107">Pokud chcete získat všechny IP adresy používané v místním počítači, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="fc261-107">To get all IP addresses in use on the local computer, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Format-Table -Property IPAddress
```

<span data-ttu-id="fc261-108">Výstup tohoto příkazu se liší od většina seznamech vlastností, protože hodnoty jsou uzavřené do složených závorek:</span><span class="sxs-lookup"><span data-stu-id="fc261-108">The output of this command differs from most property lists, because values are enclosed in braces:</span></span>

```output
IPAddress
---------
{192.168.1.80}
{192.168.148.1}
{192.168.171.1}
{0.0.0.0}
```

<span data-ttu-id="fc261-109">Zjistit, proč se zobrazuje složené závorky, použijte rutinu Get-člen prozkoumat **IPAddress** vlastnost:</span><span class="sxs-lookup"><span data-stu-id="fc261-109">To understand why the braces appear, use the Get-Member cmdlet to examine the **IPAddress** property:</span></span>

```
PS> Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Get-Member -Name IPAddress


TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapterConfiguration

Name      MemberType Definition
----      ---------- ----------
IPAddress Property   System.String[] IPAddress {get;}
```

<span data-ttu-id="fc261-110">Vlastnost IP adresa pro každý síťový adaptér je ve skutečnosti pole.</span><span class="sxs-lookup"><span data-stu-id="fc261-110">The IPAddress property for each network adapter is actually an array.</span></span> <span data-ttu-id="fc261-111">V definici složené závorky označuje, že **IPAddress** není **System.String** hodnoty, ale pole **System.String** hodnoty.</span><span class="sxs-lookup"><span data-stu-id="fc261-111">The braces in the definition indicate that **IPAddress** is not a **System.String** value, but an array of **System.String** values.</span></span>

### <a name="listing-ip-configuration-data"></a><span data-ttu-id="fc261-112">Výpis dat konfigurace IP adresy</span><span class="sxs-lookup"><span data-stu-id="fc261-112">Listing IP Configuration Data</span></span>

<span data-ttu-id="fc261-113">Pokud chcete zobrazit podrobné data konfigurace protokolu IP pro každý síťový adaptér, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="fc261-113">To display detailed IP configuration data for each network adapter, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName .
```

<span data-ttu-id="fc261-114">Výchozí zobrazení pro objekt konfigurace síťového adaptéru je velmi omezená sada dostupné informace.</span><span class="sxs-lookup"><span data-stu-id="fc261-114">The default display for the network adapter configuration object is a very reduced set of the available information.</span></span> <span data-ttu-id="fc261-115">Pro hloubkové kontrole a řešení potíží použijte Select-Object nebo formátování rutinu, jako je například Format-List, k určení vlastností, který se má zobrazit.</span><span class="sxs-lookup"><span data-stu-id="fc261-115">For in-depth inspection and troubleshooting, use Select-Object or a formatting cmdlet, such as Format-List, to specify the properties to be displayed.</span></span>

<span data-ttu-id="fc261-116">Pokud vás zajímá není ve vlastnostech protokolu IPX nebo WINS – pravděpodobně velká písmena v síti TCP/IP moderní – parametr ExcludeProperty Select-Object můžete skrýt vlastnosti s názvy začínajícími řetězcem "WINS" nebo "IPX:"</span><span class="sxs-lookup"><span data-stu-id="fc261-116">If you are not interested in IPX or WINS properties—probably the case in a modern TCP/IP network—you can use the ExcludeProperty parameter of Select-Object to hide properties with names that begin with "WINS" or "IPX:"</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

<span data-ttu-id="fc261-117">Tento příkaz vrátí podrobné informace o směrování DHCP, DNS a další dílčí vlastnosti konfigurace IP.</span><span class="sxs-lookup"><span data-stu-id="fc261-117">This command returns detailed information about DHCP, DNS, routing, and other minor IP configuration properties.</span></span>

### <a name="pinging-computers"></a><span data-ttu-id="fc261-118">Příkaz ping počítače</span><span class="sxs-lookup"><span data-stu-id="fc261-118">Pinging Computers</span></span>

<span data-ttu-id="fc261-119">Můžete provádět jednoduché ping proti počítači pomocí podle **Win32_PingStatus**.</span><span class="sxs-lookup"><span data-stu-id="fc261-119">You can perform a simple ping against a computer using by **Win32_PingStatus**.</span></span> <span data-ttu-id="fc261-120">Následující příkaz provede příkazem ping, ale vrátí zdlouhavé výstup:</span><span class="sxs-lookup"><span data-stu-id="fc261-120">The following command performs the ping, but returns lengthy output:</span></span>

```powershell
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

<span data-ttu-id="fc261-121">Užitečnější formulář pro souhrnné informace zobrazení z vlastností adresu, ResponseTime a StatusCode generovaná pomocí následujícího příkazu.</span><span class="sxs-lookup"><span data-stu-id="fc261-121">A more useful form for summary information a display of the Address, ResponseTime, and StatusCode properties, as generated by the following command.</span></span> <span data-ttu-id="fc261-122">Parametr Autosize Format-Table změní velikost sloupců tabulky, aby se zobrazí správně v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc261-122">The Autosize parameter of Format-Table resizes the table columns so that they display properly in Windows PowerShell.</span></span>

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
```

<span data-ttu-id="fc261-123">StatusCode 0 označuje úspěšný příkaz ping.</span><span class="sxs-lookup"><span data-stu-id="fc261-123">A StatusCode of 0 indicates a successful ping.</span></span>

<span data-ttu-id="fc261-124">Pole můžete použít k otestování příkazem ping více počítačů pomocí jediného příkazu.</span><span class="sxs-lookup"><span data-stu-id="fc261-124">You can use an array to ping multiple computers with a single command.</span></span> <span data-ttu-id="fc261-125">Protože je víc než jednou adresou, použijte **ForEach-Object** na příkaz ping adresu každého samostatně:</span><span class="sxs-lookup"><span data-stu-id="fc261-125">Because there is more than one address, use the **ForEach-Object** to ping each address separately:</span></span>

```powershell
'127.0.0.1','localhost','research.microsoft.com' | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

<span data-ttu-id="fc261-126">Můžete použít stejný formát příkaz ping všechny počítače v podsíti, jako jsou privátní sítě, které používá číslo sítě 192.168.1.0 a standardní maska podsítě třídy C (255.255.255.0)., jsou pouze adresy v rozsahu 192.168.1.1 až 192.168.1.254 oprávněné místní adresy (0 je vždy vyhrazené pro číslo sítě a 255 je adresu všesměrového vysílání podsítě).</span><span class="sxs-lookup"><span data-stu-id="fc261-126">You can use the same command format to ping all of the computers on a subnet, such as a private network that uses network number 192.168.1.0 and a standard Class C subnet mask (255.255.255.0)., Only addresses in the range of 192.168.1.1 through 192.168.1.254 are legitimate local addresses (0 is always reserved for the network number and 255 is a subnet broadcast address).</span></span>

<span data-ttu-id="fc261-127">Chcete-li představují pole čísel od 1 do 254 v prostředí Windows PowerShell, použijte příkaz **1..254.**</span><span class="sxs-lookup"><span data-stu-id="fc261-127">To represent an array of the numbers from 1 through 254 in Windows PowerShell, use the statement **1..254.**</span></span> <span data-ttu-id="fc261-128">Generování pole a pak přidáním hodnoty do adresu částečné v příkazu ping je možné provádět ping dokončení podsítě:</span><span class="sxs-lookup"><span data-stu-id="fc261-128">A complete subnet ping can be performed by generating the array and then adding the values onto a partial address in the ping statement:</span></span>

```powershell
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

<span data-ttu-id="fc261-129">Poznamenat, že tato technika pro generování rozsah adres můžete použít také jinde.</span><span class="sxs-lookup"><span data-stu-id="fc261-129">Note that this technique for generating a range of addresses can be used elsewhere as well.</span></span> <span data-ttu-id="fc261-130">Tímto způsobem můžete vygenerovat kompletní sadu adresy:</span><span class="sxs-lookup"><span data-stu-id="fc261-130">You can generate a complete set of addresses in this way:</span></span>

```powershell
$ips = 1..254 | ForEach-Object -Process {'192.168.1.' + $_}
```

### <a name="retrieving-network-adapter-properties"></a><span data-ttu-id="fc261-131">Načítání vlastností síťového adaptéru</span><span class="sxs-lookup"><span data-stu-id="fc261-131">Retrieving Network Adapter Properties</span></span>

<span data-ttu-id="fc261-132">Dříve v této uživatelské příručce jsme uvedeno, zda může načíst vlastnosti Obecné konfigurace pomocí **Win32_NetworkAdapterConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="fc261-132">Earlier in this user's guide, we mentioned that you could retrieve general configuration properties by using **Win32_NetworkAdapterConfiguration**.</span></span> <span data-ttu-id="fc261-133">I když nejedná striktně informace protokolu TCP/IP, informace o síťového adaptéru jako je například MAC adres a typy adaptéru může být užitečná pro pochopení, co se děje s počítačem.</span><span class="sxs-lookup"><span data-stu-id="fc261-133">Although not strictly TCP/IP information, network adapter information such as MAC addresses and adapter types can be useful for understanding what is going on with a computer.</span></span> <span data-ttu-id="fc261-134">Souhrn tyto informace získáte pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="fc261-134">To get a summary of this information, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

### <a name="assigning-the-dns-domain-for-a-network-adapter"></a><span data-ttu-id="fc261-135">Přiřazení domény DNS pro síťový adaptér</span><span class="sxs-lookup"><span data-stu-id="fc261-135">Assigning the DNS Domain for a Network Adapter</span></span>

<span data-ttu-id="fc261-136">Chcete-li přiřadit doménu DNS automatického překladu IP adres, použijte **Win32_NetworkAdapterConfiguration SetDNSDomain** metoda.</span><span class="sxs-lookup"><span data-stu-id="fc261-136">To assign the DNS domain for automatic name resolution, use the **Win32_NetworkAdapterConfiguration SetDNSDomain** method.</span></span> <span data-ttu-id="fc261-137">Protože nezávisle přiřadíte DNS domény pro každou konfiguraci síťového adaptéru, budete muset použít **ForEach-Object** příkaz přiřadit každý adaptér domény:</span><span class="sxs-lookup"><span data-stu-id="fc261-137">Because you assign the DNS domain for each network adapter configuration independently, you need to use a **ForEach-Object** statement to assign the domain to each adapter:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain('fabrikam.com') }
```

<span data-ttu-id="fc261-138">Příkaz filtrování "IPEnabled = $true" je nutné, protože to i v síti, která používá jenom protokol TCP/IP, řadu konfigurací síťových adaptérů v počítači není true TCP/IP adaptéry; jsou složky obecných softwarových podporující RAS, PPTP, technologie QoS a jiných služeb pro všechny adaptéry a proto nemají své vlastní adresy.</span><span class="sxs-lookup"><span data-stu-id="fc261-138">The filtering statement "IPEnabled=$true" is necessary, because even on a network that uses only TCP/IP, several of the network adapter configurations on a computer are not true TCP/IP adapters; they are general software elements supporting RAS, PPTP, QoS, and other services for all adapters and thus do not have an address of their own.</span></span>

<span data-ttu-id="fc261-139">Příkaz můžete filtrovat pomocí **Where-Object** rutiny, místo použití **Get-WmiObject** filtru.</span><span class="sxs-lookup"><span data-stu-id="fc261-139">You can filter the command by using the **Where-Object** cmdlet, instead of using the **Get-WmiObject** filter.</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain('fabrikam.com')}
```

### <a name="performing-dhcp-configuration-tasks"></a><span data-ttu-id="fc261-140">Provádění úlohy konfigurace DHCP</span><span class="sxs-lookup"><span data-stu-id="fc261-140">Performing DHCP Configuration Tasks</span></span>

<span data-ttu-id="fc261-141">Úprava DHCP podrobnosti součástí je práce se sadou síťových adaptérů, stejně jako konfiguraci serveru DNS.</span><span class="sxs-lookup"><span data-stu-id="fc261-141">Modifying DHCP details involves working with a set of network adapters, just as the DNS configuration does.</span></span> <span data-ttu-id="fc261-142">Existuje několik různých akcí, které můžete provádět pomocí rozhraní WMI a jsme bude procházet několik běžných ty.</span><span class="sxs-lookup"><span data-stu-id="fc261-142">There are several distinct actions you can perform by using WMI, and we will step through a few of the common ones.</span></span>

#### <a name="determining-dhcp-enabled-adapters"></a><span data-ttu-id="fc261-143">Určení adaptéry s podporou DHCP</span><span class="sxs-lookup"><span data-stu-id="fc261-143">Determining DHCP-Enabled Adapters</span></span>

<span data-ttu-id="fc261-144">Chcete-li najít adaptéry podporující službu DHCP na počítači, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="fc261-144">To find the DHCP-enabled adapters on a computer, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName .
```

<span data-ttu-id="fc261-145">Vyloučit adaptéry s problémy s konfigurací protokolu IP, můžete načíst pouze adaptéry zapnutá IP adresa:</span><span class="sxs-lookup"><span data-stu-id="fc261-145">To exclude adapters with IP configuration problems, you can retrieve only IP-enabled adapters:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName .
```

#### <a name="retrieving-dhcp-properties"></a><span data-ttu-id="fc261-146">Načítání vlastností DHCP</span><span class="sxs-lookup"><span data-stu-id="fc261-146">Retrieving DHCP Properties</span></span>

<span data-ttu-id="fc261-147">Protože vlastnosti týkající se služby DHCP pro adaptér obecně začínat řetězcem "DHCP", můžete pouze vlastnosti parametr vlastností formátu tabulky:</span><span class="sxs-lookup"><span data-stu-id="fc261-147">Because DHCP-related properties for an adapter generally begin with "DHCP," you can use the Property parameter of Format-Table to display only those properties:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=$true" -ComputerName . | Format-Table -Property DHCP*
```

#### <a name="enabling-dhcp-on-each-adapter"></a><span data-ttu-id="fc261-148">Povolení protokol DHCP na každý adaptér</span><span class="sxs-lookup"><span data-stu-id="fc261-148">Enabling DHCP on Each Adapter</span></span>

<span data-ttu-id="fc261-149">Pokud chcete povolit DHCP na všechny adaptéry, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="fc261-149">To enable DHCP on all adapters, use the following command:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=$true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

<span data-ttu-id="fc261-150">Můžete použít **filtru** příkaz "IPEnabled = $true a DHCPEnabled = $false" předejdete povolení DHCP, kde je již povolen, ale vynechejte tento krok nebude způsobit chyby.</span><span class="sxs-lookup"><span data-stu-id="fc261-150">You can use the **Filter** statement "IPEnabled=$true and DHCPEnabled=$false" to avoid enabling DHCP where it is already enabled, but omitting this step will not cause errors.</span></span>

#### <a name="releasing-and-renewing-dhcp-leases-on-specific-adapters"></a><span data-ttu-id="fc261-151">Uvolnění a obnovení zapůjčení DHCP konkrétní síťové adaptéry</span><span class="sxs-lookup"><span data-stu-id="fc261-151">Releasing and Renewing DHCP Leases on Specific Adapters</span></span>

<span data-ttu-id="fc261-152">**Win32_NetworkAdapterConfiguration** třída má **ReleaseDHCPLease** a **RenewDHCPLease** metody.</span><span class="sxs-lookup"><span data-stu-id="fc261-152">The **Win32_NetworkAdapterConfiguration** class has **ReleaseDHCPLease** and **RenewDHCPLease** methods.</span></span> <span data-ttu-id="fc261-153">Jak se používají stejným způsobem.</span><span class="sxs-lookup"><span data-stu-id="fc261-153">Both are used in the same way.</span></span> <span data-ttu-id="fc261-154">Obecně platí použijte tyto metody, pokud potřebujete jenom uvolnit nebo obnovit adresy pro adaptér v konkrétní podsíti.</span><span class="sxs-lookup"><span data-stu-id="fc261-154">In general, use these methods if you only need to release or renew addresses for an adapter on a specific subnet.</span></span> <span data-ttu-id="fc261-155">Nejjednodušší způsob, jak filtr adaptéry v podsíti je vybrat pouze adaptér konfigurace, které použití brány pro tuto podsíť.</span><span class="sxs-lookup"><span data-stu-id="fc261-155">The easiest way to filter adapters on a subnet is to choose only the adapter configurations that use the gateway for that subnet.</span></span> <span data-ttu-id="fc261-156">Například následující příkaz uvolní všechny zapůjčení DHCP adaptérům v místním počítači, které jsou získání zapůjčení DHCP ze 192.168.1.254:</span><span class="sxs-lookup"><span data-stu-id="fc261-156">For example, the following command releases all DHCP leases on adapters on the local computer that are obtaining DHCP leases from 192.168.1.254:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

<span data-ttu-id="fc261-157">Jedinou změnou pro obnovení zapůjčení DHCP je použití **RenewDHCPLease** metoda místo **ReleaseDHCPLease** metoda:</span><span class="sxs-lookup"><span data-stu-id="fc261-157">The only change for renewing a DHCP lease is to use the **RenewDHCPLease** method instead of the **ReleaseDHCPLease** method:</span></span>

```powershell
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true and DHCPEnabled=$true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains '192.168.1.254'} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> <span data-ttu-id="fc261-158">Při použití těchto metod ve vzdáleném počítači, mějte na paměti, že pokud jste připojení k němu pomocí adaptéru vydaná nebo obnovené zapůjčení, můžete ztratit přístup ke vzdálenému systému.</span><span class="sxs-lookup"><span data-stu-id="fc261-158">When using these methods on a remote computer, be aware that you can lose access to the remote system if you are connected to it through the adapter with the released or renewed lease.</span></span>

#### <a name="releasing-and-renewing-dhcp-leases-on-all-adapters"></a><span data-ttu-id="fc261-159">Uvolnění a obnovení zapůjčení DHCP na všechny adaptéry</span><span class="sxs-lookup"><span data-stu-id="fc261-159">Releasing and Renewing DHCP Leases on All Adapters</span></span>

<span data-ttu-id="fc261-160">Globální verze adres DHCP nebo obnovení můžete provést na všechny adaptéry pomocí **Win32_NetworkAdapterConfiguration** metody, **ReleaseDHCPLeaseAll** a **RenewDHCPLeaseAll** .</span><span class="sxs-lookup"><span data-stu-id="fc261-160">You can perform global DHCP address releases or renewals on all adapters by using the **Win32_NetworkAdapterConfiguration** methods, **ReleaseDHCPLeaseAll** and **RenewDHCPLeaseAll**.</span></span> <span data-ttu-id="fc261-161">Ale příkaz se musí vztahovat na třídu služby WMI, nikoli konkrétní adaptér, protože uvolnění a obnovení zapůjčení globálně provádí na třídu, nikoli na konkrétní adaptér.</span><span class="sxs-lookup"><span data-stu-id="fc261-161">However, the command must apply to the WMI class, rather than a particular adapter, because releasing and renewing leases globally is performed on the class, not on a specific adapter.</span></span>

<span data-ttu-id="fc261-162">Odkaz na rozhraní WMI tříd, namísto instancí třídy, můžete získat podle výpis všech tříd WMI a pak vyberte požadovanou třídu podle názvu.</span><span class="sxs-lookup"><span data-stu-id="fc261-162">You can get a reference to a WMI class, instead of class instances, by listing all WMI classes and then selecting only the desired class by name.</span></span> <span data-ttu-id="fc261-163">Například následující příkaz vrátí třídy Win32_NetworkAdapterConfiguration:</span><span class="sxs-lookup"><span data-stu-id="fc261-163">For example, the following command returns the Win32_NetworkAdapterConfiguration class:</span></span>

```powershell
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'}
```

<span data-ttu-id="fc261-164">Lze považovat za celý příkaz třídy a pak vyvolejte **ReleaseDHCPAdapterLease** metoda na něm.</span><span class="sxs-lookup"><span data-stu-id="fc261-164">You can treat the entire command as the class and then invoke the **ReleaseDHCPAdapterLease** method on it.</span></span> <span data-ttu-id="fc261-165">V následujícím příkazu závorky kolem **Get-WmiObject** a **Where-Object** kanálu elementy přímé prostředí Windows PowerShell je nejdřív vyhodnotit:</span><span class="sxs-lookup"><span data-stu-id="fc261-165">In the following command, the parentheses surrounding the **Get-WmiObject** and **Where-Object** pipeline elements direct Windows PowerShell to evaluate them first:</span></span>

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).ReleaseDHCPLeaseAll()
```

<span data-ttu-id="fc261-166">Můžete použít stejný formát příkaz má být vyvolán **RenewDHCPLeaseAll** metoda:</span><span class="sxs-lookup"><span data-stu-id="fc261-166">You can use the same command format to invoke the **RenewDHCPLeaseAll** method:</span></span>

```powershell
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq 'Win32_NetworkAdapterConfiguration'} ).RenewDHCPLeaseAll()
```

### <a name="creating-a-network-share"></a><span data-ttu-id="fc261-167">Vytvoření sdílené síťové složky</span><span class="sxs-lookup"><span data-stu-id="fc261-167">Creating a Network Share</span></span>

<span data-ttu-id="fc261-168">K vytvoření sdílené síťové složky, použijte **Win32_Share vytvořit** metoda:</span><span class="sxs-lookup"><span data-stu-id="fc261-168">To create a network share, use the **Win32_Share Create** method:</span></span>

```powershell
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq 'Win32_Share'}).Create('C:\temp','TempShare',0,25,'test share of the temp folder')
```

<span data-ttu-id="fc261-169">Můžete také vytvořit sdílenou složku pomocí **příkaz net share** v prostředí Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fc261-169">You can also create the share by using **net share** in Windows PowerShell:</span></span>

```powershell
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

### <a name="removing-a-network-share"></a><span data-ttu-id="fc261-170">Odebráním sdílené síťové složky</span><span class="sxs-lookup"><span data-stu-id="fc261-170">Removing a Network Share</span></span>

<span data-ttu-id="fc261-171">Odebráním sdílené síťové složky s **Win32_Share**, ale proces mírně lišit od vytvoření sdílené složky, protože je potřeba načíst konkrétní sdílenou složku na odebrat, místo **Win32_Share** Třída.</span><span class="sxs-lookup"><span data-stu-id="fc261-171">You can remove a network share with **Win32_Share**, but the process is slightly different from creating a share, because you need to retrieve the specific share to be removed, rather than the **Win32_Share** class.</span></span> <span data-ttu-id="fc261-172">Následující příkaz odstraní sdílenou složku "TempShare":</span><span class="sxs-lookup"><span data-stu-id="fc261-172">The following statement deletes the share "TempShare":</span></span>

```powershell
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

<span data-ttu-id="fc261-173">**Příkaz net share** funguje také:</span><span class="sxs-lookup"><span data-stu-id="fc261-173">**Net share** works as well:</span></span>

```
PS> net share tempshare /delete

tempshare was deleted successfully.
```

### <a name="connecting-a-windows-accessible-network-drive"></a><span data-ttu-id="fc261-174">Připojení Windows dostupné síťové jednotky</span><span class="sxs-lookup"><span data-stu-id="fc261-174">Connecting a Windows Accessible Network Drive</span></span>

<span data-ttu-id="fc261-175">**New-PSDrive** rutin vytvoří jednotku prostředí Windows PowerShell, ale jednotky vytvořené tímto způsobem jsou k dispozici pouze pro prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc261-175">The **New-PSDrive** cmdlets creates a Windows PowerShell drive, but drives created this way are available only to Windows PowerShell.</span></span> <span data-ttu-id="fc261-176">Pokud chcete vytvořit nový síťová jednotka, můžete použít **WScript.Network** objektu COM.</span><span class="sxs-lookup"><span data-stu-id="fc261-176">To create a new networked drive, you can use the **WScript.Network** COM object.</span></span> <span data-ttu-id="fc261-177">Následující příkaz mapuje sdílenou složku \\ \\FPS01\\uživatelům místní disk B:</span><span class="sxs-lookup"><span data-stu-id="fc261-177">The following command maps the share \\\\FPS01\\users to local drive B:</span></span>

```powershell
(New-Object -ComObject WScript.Network).MapNetworkDrive('B:', '\\FPS01\users')
```

<span data-ttu-id="fc261-178">**Net použití** příkaz lze použít také:</span><span class="sxs-lookup"><span data-stu-id="fc261-178">The **net use** command works as well:</span></span>

```powershell
net use B: \\FPS01\users
```

<span data-ttu-id="fc261-179">Jednotky namapované s buď **WScript.Network** nebo příkazu net use jsou okamžitě k dispozici pro prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc261-179">Drives mapped with either **WScript.Network** or net use are immediately available to Windows PowerShell.</span></span>