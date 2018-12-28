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
# <a name="working-with-printers"></a>Práce s tiskárnami

Prostředí Windows PowerShell můžete použít ke správě pomocí rozhraní WMI a objekt modelu COM WScript.Network z prostředí WSH tiskárny. Budeme používat kombinaci obou nástroje k předvedení konkrétní úlohy.

### <a name="listing-printer-connections"></a>Seznam připojení tiskáren

Nejjednodušší způsob, jak seznamu tiskárny nainstalované v počítači je použít rozhraní WMI **Win32_Printer** třídy:

```powershell
Get-WmiObject -Class Win32_Printer -ComputerName
```

Můžete také zobrazit seznam tiskáren s použitím **WScript.Network** objektu COM, který se obvykle používá ve skriptech prostředí WSH:

```powershell
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

Vzhledem k tomu tento příkaz vrátí kolekci jednoduchým řetězcem port názvy a tiskárny zařízení bez jakékoli rozlišovací popisky, není snadné interpretovat.

### <a name="adding-a-network-printer"></a>Přidání síťové tiskárny

Chcete-li přidat nové tiskárny sítě, použijte **WScript.Network**:

```powershell
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

### <a name="setting-a-default-printer"></a>Nastavení výchozí tiskárna

Pomocí služby WMI nastaví výchozí tiskárnu, Najít tiskárny v **Win32_Printer** kolekce a pak vyvolejte **SetDefaultPrinter** metody:

```powershell
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

**WScript.Network** je o něco jednodušší, pokud chcete použít, protože má **SetDefaultPrinter** metodu, která přebírá pouze název tiskárny jako argument:

```powershell
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

### <a name="removing-a-printer-connection"></a>Odebrání připojení k tiskárně

Chcete-li odebrat připojení k tiskárně, použijte **WScript.Network RemovePrinterConnection** metody:

```powershell
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```