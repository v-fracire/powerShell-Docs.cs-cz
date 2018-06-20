---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce s tiskárnami
ms.assetid: 4f29ead3-f83b-4706-ac3e-f2154ff38dc5
ms.openlocfilehash: 5638629fdf79371c8eff9ee9194b642034250fff
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954496"
---
# <a name="working-with-printers"></a><span data-ttu-id="525d1-103">Práce s tiskárnami</span><span class="sxs-lookup"><span data-stu-id="525d1-103">Working with Printers</span></span>

<span data-ttu-id="525d1-104">Prostředí Windows PowerShell můžete použít ke správě tiskárny pomocí rozhraní WMI a objekt WScript.Network COM z prostředí WSH.</span><span class="sxs-lookup"><span data-stu-id="525d1-104">You can use Windows PowerShell to manage printers by using WMI and the WScript.Network COM object from WSH.</span></span> <span data-ttu-id="525d1-105">Budeme používat kombinaci obou nástrojů k předvedení konkrétní úlohy.</span><span class="sxs-lookup"><span data-stu-id="525d1-105">We will use a mix of both tools to demonstrate specific tasks.</span></span>

### <a name="listing-printer-connections"></a><span data-ttu-id="525d1-106">Výpis připojení tiskáren</span><span class="sxs-lookup"><span data-stu-id="525d1-106">Listing Printer Connections</span></span>

<span data-ttu-id="525d1-107">Nejjednodušší způsob, jak seznamu tiskáren nainstalovaných v počítači se má používat služba WMI **Win32_Printer** třídy:</span><span class="sxs-lookup"><span data-stu-id="525d1-107">The simplest way to list the printers installed on a computer is to use the WMI **Win32_Printer** class:</span></span>

```powershell
Get-WmiObject -Class Win32_Printer -ComputerName
```

<span data-ttu-id="525d1-108">Můžete také seznam tiskáren pomocí **WScript.Network** objektu COM, která se obvykle používá ve skriptech prostředí WSH:</span><span class="sxs-lookup"><span data-stu-id="525d1-108">You can also list the printers by using the **WScript.Network** COM object that is typically used in WSH scripts:</span></span>

```powershell
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

<span data-ttu-id="525d1-109">Protože tento příkaz vrátí kolekci jednoduchým řetězcem port názvy a tiskárny zařízení bez jakékoli rozlišovací popisky, není usnadňuje interpretovat.</span><span class="sxs-lookup"><span data-stu-id="525d1-109">Because this command returns a simple string collection of port names and printer device names without any distinguishing labels, it is not easy to interpret.</span></span>

### <a name="adding-a-network-printer"></a><span data-ttu-id="525d1-110">Přidání síťové tiskárny</span><span class="sxs-lookup"><span data-stu-id="525d1-110">Adding a Network Printer</span></span>

<span data-ttu-id="525d1-111">Chcete-li přidat nové síťové tiskárně, použijte **WScript.Network**:</span><span class="sxs-lookup"><span data-stu-id="525d1-111">To add a new network printer, use **WScript.Network**:</span></span>

```powershell
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

### <a name="setting-a-default-printer"></a><span data-ttu-id="525d1-112">Nastavení výchozí tiskárny</span><span class="sxs-lookup"><span data-stu-id="525d1-112">Setting a Default Printer</span></span>

<span data-ttu-id="525d1-113">Nastavení výchozí tiskárny pomocí rozhraní WMI, Najít tiskárny v **Win32_Printer** kolekci a pak vyvolejte **SetDefaultPrinter** metoda:</span><span class="sxs-lookup"><span data-stu-id="525d1-113">To use WMI to set the default printer, find the printer in the **Win32_Printer** collection and then invoke the **SetDefaultPrinter** method:</span></span>

```powershell
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

<span data-ttu-id="525d1-114">**WScript.Network** je trochu jednodušší použít, protože obsahuje **SetDefaultPrinter** metody, která přijímá pouze název tiskárny jako argument:</span><span class="sxs-lookup"><span data-stu-id="525d1-114">**WScript.Network** is a little simpler to use, because it has a **SetDefaultPrinter** method that takes only the printer name as an argument:</span></span>

```powershell
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

### <a name="removing-a-printer-connection"></a><span data-ttu-id="525d1-115">Odebrání připojení k tiskárně</span><span class="sxs-lookup"><span data-stu-id="525d1-115">Removing a Printer Connection</span></span>

<span data-ttu-id="525d1-116">Pokud chcete odstranit připojení k tiskárně, použijte **WScript.Network RemovePrinterConnection** metoda:</span><span class="sxs-lookup"><span data-stu-id="525d1-116">To remove a printer connection, use the **WScript.Network RemovePrinterConnection** method:</span></span>

```powershell
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```