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
# <a name="working-with-printers"></a>Práce s tiskárnami

Prostředí Windows PowerShell můžete použít ke správě tiskárny pomocí rozhraní WMI a objekt WScript.Network COM z prostředí WSH. Budeme používat kombinaci obou nástrojů k předvedení konkrétní úlohy.

### <a name="listing-printer-connections"></a>Výpis připojení tiskáren

Nejjednodušší způsob, jak seznamu tiskáren nainstalovaných v počítači se má používat služba WMI **Win32_Printer** třídy:

```powershell
Get-WmiObject -Class Win32_Printer -ComputerName
```

Můžete také seznam tiskáren pomocí **WScript.Network** objektu COM, která se obvykle používá ve skriptech prostředí WSH:

```powershell
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

Protože tento příkaz vrátí kolekci jednoduchým řetězcem port názvy a tiskárny zařízení bez jakékoli rozlišovací popisky, není usnadňuje interpretovat.

### <a name="adding-a-network-printer"></a>Přidání síťové tiskárny

Chcete-li přidat nové síťové tiskárně, použijte **WScript.Network**:

```powershell
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

### <a name="setting-a-default-printer"></a>Nastavení výchozí tiskárny

Nastavení výchozí tiskárny pomocí rozhraní WMI, Najít tiskárny v **Win32_Printer** kolekci a pak vyvolejte **SetDefaultPrinter** metoda:

```powershell
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

**WScript.Network** je trochu jednodušší použít, protože obsahuje **SetDefaultPrinter** metody, která přijímá pouze název tiskárny jako argument:

```powershell
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

### <a name="removing-a-printer-connection"></a>Odebrání připojení k tiskárně

Pokud chcete odstranit připojení k tiskárně, použijte **WScript.Network RemovePrinterConnection** metoda:

```powershell
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```