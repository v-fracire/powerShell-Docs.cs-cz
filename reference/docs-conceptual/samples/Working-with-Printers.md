---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce s tiskárnami
ms.assetid: 4f29ead3-f83b-4706-ac3e-f2154ff38dc5
ms.openlocfilehash: 5638629fdf79371c8eff9ee9194b642034250fff
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404062"
---
# <a name="working-with-printers"></a><span data-ttu-id="4248e-103">Práce s tiskárnami</span><span class="sxs-lookup"><span data-stu-id="4248e-103">Working with Printers</span></span>

<span data-ttu-id="4248e-104">Prostředí Windows PowerShell můžete použít ke správě pomocí rozhraní WMI a objekt modelu COM WScript.Network z prostředí WSH tiskárny.</span><span class="sxs-lookup"><span data-stu-id="4248e-104">You can use Windows PowerShell to manage printers by using WMI and the WScript.Network COM object from WSH.</span></span> <span data-ttu-id="4248e-105">Budeme používat kombinaci obou nástroje k předvedení konkrétní úlohy.</span><span class="sxs-lookup"><span data-stu-id="4248e-105">We will use a mix of both tools to demonstrate specific tasks.</span></span>

### <a name="listing-printer-connections"></a><span data-ttu-id="4248e-106">Seznam připojení tiskáren</span><span class="sxs-lookup"><span data-stu-id="4248e-106">Listing Printer Connections</span></span>

<span data-ttu-id="4248e-107">Nejjednodušší způsob, jak seznamu tiskárny nainstalované v počítači je použít rozhraní WMI **Win32_Printer** třídy:</span><span class="sxs-lookup"><span data-stu-id="4248e-107">The simplest way to list the printers installed on a computer is to use the WMI **Win32_Printer** class:</span></span>

```powershell
Get-WmiObject -Class Win32_Printer -ComputerName
```

<span data-ttu-id="4248e-108">Můžete také zobrazit seznam tiskáren s použitím **WScript.Network** objektu COM, který se obvykle používá ve skriptech prostředí WSH:</span><span class="sxs-lookup"><span data-stu-id="4248e-108">You can also list the printers by using the **WScript.Network** COM object that is typically used in WSH scripts:</span></span>

```powershell
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

<span data-ttu-id="4248e-109">Vzhledem k tomu tento příkaz vrátí kolekci jednoduchým řetězcem port názvy a tiskárny zařízení bez jakékoli rozlišovací popisky, není snadné interpretovat.</span><span class="sxs-lookup"><span data-stu-id="4248e-109">Because this command returns a simple string collection of port names and printer device names without any distinguishing labels, it is not easy to interpret.</span></span>

### <a name="adding-a-network-printer"></a><span data-ttu-id="4248e-110">Přidání síťové tiskárny</span><span class="sxs-lookup"><span data-stu-id="4248e-110">Adding a Network Printer</span></span>

<span data-ttu-id="4248e-111">Chcete-li přidat nové tiskárny sítě, použijte **WScript.Network**:</span><span class="sxs-lookup"><span data-stu-id="4248e-111">To add a new network printer, use **WScript.Network**:</span></span>

```powershell
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

### <a name="setting-a-default-printer"></a><span data-ttu-id="4248e-112">Nastavení výchozí tiskárna</span><span class="sxs-lookup"><span data-stu-id="4248e-112">Setting a Default Printer</span></span>

<span data-ttu-id="4248e-113">Pomocí služby WMI nastaví výchozí tiskárnu, Najít tiskárny v **Win32_Printer** kolekce a pak vyvolejte **SetDefaultPrinter** metody:</span><span class="sxs-lookup"><span data-stu-id="4248e-113">To use WMI to set the default printer, find the printer in the **Win32_Printer** collection and then invoke the **SetDefaultPrinter** method:</span></span>

```powershell
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

<span data-ttu-id="4248e-114">**WScript.Network** je o něco jednodušší, pokud chcete použít, protože má **SetDefaultPrinter** metodu, která přebírá pouze název tiskárny jako argument:</span><span class="sxs-lookup"><span data-stu-id="4248e-114">**WScript.Network** is a little simpler to use, because it has a **SetDefaultPrinter** method that takes only the printer name as an argument:</span></span>

```powershell
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

### <a name="removing-a-printer-connection"></a><span data-ttu-id="4248e-115">Odebrání připojení k tiskárně</span><span class="sxs-lookup"><span data-stu-id="4248e-115">Removing a Printer Connection</span></span>

<span data-ttu-id="4248e-116">Chcete-li odebrat připojení k tiskárně, použijte **WScript.Network RemovePrinterConnection** metody:</span><span class="sxs-lookup"><span data-stu-id="4248e-116">To remove a printer connection, use the **WScript.Network RemovePrinterConnection** method:</span></span>

```powershell
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```