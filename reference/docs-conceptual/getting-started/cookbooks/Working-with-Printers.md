---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Práce s tiskárny"
ms.assetid: 4f29ead3-f83b-4706-ac3e-f2154ff38dc5
ms.openlocfilehash: c8b4d728c9fddd39e1aeb56d6f9b8ffffe4c7292
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-printers"></a>Práce s tiskárny
Prostředí Windows PowerShell můžete použít ke správě tiskárny pomocí rozhraní WMI a objekt WScript.Network COM z prostředí WSH. Budeme používat kombinaci obou nástrojů k předvedení konkrétní úlohy.

### <a name="listing-printer-connections"></a>Výpis připojení tiskáren
Nejjednodušší způsob, jak seznamu tiskáren nainstalovaných v počítači se má používat služba WMI **Win32_Printer** třídy:

```
Get-WmiObject -Class Win32_Printer -ComputerName
```

Můžete také seznam tiskáren pomocí **WScript.Network** objektu COM, která se obvykle používá ve skriptech prostředí WSH:

```
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

Protože tento příkaz vrátí kolekci jednoduchým řetězcem port názvy a tiskárny zařízení bez jakékoli rozlišovací popisky, není usnadňuje interpretovat.

### <a name="adding-a-network-printer"></a>Přidání síťové tiskárny
Chcete-li přidat nové síťové tiskárně, použijte **WScript.Network**:

```
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

### <a name="setting-a-default-printer"></a>Nastavení výchozí tiskárny
Nastavení výchozí tiskárny pomocí rozhraní WMI, Najít tiskárny v **Win32_Printer** kolekci a pak vyvolejte **SetDefaultPrinter** metoda:

```
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

**WScript.Network** je trochu jednodušší použít, protože obsahuje **SetDefaultPrinter** metody, která přijímá pouze název tiskárny jako argument:

```
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

### <a name="removing-a-printer-connection"></a>Odebrání připojení k tiskárně
Pokud chcete odstranit připojení k tiskárně, použijte **WScript.Network RemovePrinterConnection** metoda:

```
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```

