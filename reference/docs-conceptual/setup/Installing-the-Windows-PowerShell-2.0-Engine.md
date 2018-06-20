---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Instalace jádra Windows PowerShellu 2.0
ms.assetid: 82928f2b-f96a-4ae6-a0d0-6e7b181da308
ms.openlocfilehash: 0b3282a1a67886509e749af0f499c47fe7a99411
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952337"
---
# <a name="installing-the-windows-powershell-20-engine"></a>Instalace jádra Windows PowerShellu 2.0
Toto téma vysvětluje, jak nainstalovat modul Windows PowerShell 2.0.

Prostředí Windows PowerShell 3.0 je navržený jako zpětně kompatibilní s Windows PowerShell 2.0. Rutiny, zprostředkovatelé, moduly snap in, moduly a skripty, které jsou napsané pro prostředí Windows PowerShell 2.0 spustit v prostředí Windows PowerShell 3.0 a prostředí Windows PowerShell 4.0 beze změny. Však z důvodu změn v zásadách aktivace runtime v rozhraní Microsoft .NET Framework 4, programy hostitele prostředí Windows PowerShell, které byly napsané pro prostředí Windows PowerShell 2.0 a kompilovat s Common Language Runtime (CLR) 2.0 nelze spustit bez úprav v později verze prostředí Windows PowerShell, který je kompilovat s CLR 4.0.

K zachování zpětné kompatibility s příkazy a hostitele programy, které jsou ovlivněné tyto změny, moduly prostředí Windows PowerShell 2.0, prostředí Windows PowerShell 3.0 a prostředí Windows PowerShell 4.0 slouží ke spuštění vedle sebe. Modul Windows PowerShell 2.0 je také součástí systému Windows Server 2012 R2, Windows 8.1, Windows 8, Windows Server 2012 a Windows Management Framework 3.0. Modul Windows PowerShell 2.0 je určena pro použití pouze v případě stávajícího skriptu nebo hostitele program nelze spustit, protože není kompatibilní s Windows PowerShell 3.0, prostředí Windows PowerShell 4.0 nebo Microsoft .NET Framework 4. Očekává se, že takových případech zřídka.

Modul Windows PowerShell 2.0 je volitelná funkce systému Windows Server 2012 R2, Windows 8.1, Windows® 8 a Windows Server® 2012. V dřívějších verzích systému Windows při instalaci Windows Management Framework 3.0, instalace prostředí Windows PowerShell 3.0 zcela nahradí instalace prostředí Windows PowerShell 2.0 v instalačním adresáři prostředí Windows PowerShell. Modul Windows PowerShell 2.0 se však zachová.

Informace o spouštění modulu Windows PowerShell 2.0 naleznete v tématu [spouštění modulu Windows PowerShell 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="on-windows-81-and-windows-8"></a>Na Windows 8.1 a Windows 8
Na Windows 8.1 a Windows 8 modul Windows PowerShell 2.0 funkce je zapnutá ve výchozím nastavení. Ale pokud chcete použít, musíte zapnout možnosti pro rozhraní Microsoft .NET Framework 3.5, který vyžaduje. Tato část také vysvětluje, jak zapnout funkci modul Windows PowerShell 2.0 a vypnout.

#### <a name="to-turn-on-net-framework-35"></a>Chcete-li na rozhraní .NET Framework 3.5

1. Na **spustit** zadejte **funkce systému Windows**.

2. Na **aplikace** panelu, klikněte na tlačítko **nastavení**a potom klikněte na **Windows zapnout nebo vypnout funkce**.

3. V **funkce systému Windows** pole, klikněte na tlačítko **rozhraní .NET Framework 3.5 (zahrnuje rozhraní .NET 2.0 a 3.0** ji vyberte.

    Když vyberete **rozhraní .NET Framework 3.5 (zahrnuje rozhraní .NET 2.0 a 3.0**, k označení, že je vybrána pouze část funkce vyplní celé pole. To je však dostatečná pro modul Windows PowerShell 2.0.

#### <a name="to-turn-the-windows-powershell-20-engine-on-and-off"></a>Chcete-li modul Windows PowerShell 2.0 zapnout a vypnout

1. Na **spustit** zadejte **funkce systému Windows**.

2. Na **aplikace** panelu, klikněte na tlačítko **nastavení**a potom klikněte na **Windows zapnout nebo vypnout funkce**.

3. V **funkce systému Windows** rozbalte položku **prostředí Windows PowerShell 2.0** uzel a klikněte na tlačítko **modul Windows PowerShell 2.0** políčko zaškrtněte nebo zrušte jeho zaškrtnutí.

## <a name="on-windows-server-2012-r2-and-windows-server-2012"></a>V systému Windows Server 2012 R2 a Windows Server 2012
Použijte následující postupy k přidání modul Windows PowerShell 2.0 a funkcí rozhraní Microsoft .NET Framework 3.5. Modul Windows PowerShell 2.0 vyžaduje rozhraní Microsoft .NET Framework 2.0.50727 minimálně. Tento požadavek splněn pomocí rozhraní Microsoft .NET Framework 3.5.

#### <a name="to-add-the-net-framework-35-feature"></a>Přidat funkci rozhraní .NET Framework 3.5

1. V **správce serveru**, z **spravovat** nabídce vyberte možnost **přidat role a funkce**.

    Nebo v **správce serveru**, klikněte na tlačítko **všechny servery**, klikněte pravým tlačítkem na název serveru a pak vyberte **přidat role a funkce**.

2. Na **typ instalace** vyberte **instalace na základě rolí nebo na základě funkcí**.

3. Na **funkce** rozbalte **funkce rozhraní .NET Framework 3.5** uzel a vyberte možnost **rozhraní .NET Framework 3.5 (zahrnuje rozhraní .NET 2.0 a 3.0)**.

    Další možnosti v tomto uzlu nejsou požadovány pro modul Windows PowerShell 2.0.

#### <a name="to-add-the-windows-powershell-20-engine-feature"></a>Přidat funkci modul Windows PowerShell 2.0

- V **správce serveru**, z **spravovat** nabídce vyberte možnost **přidat role a funkce**.

    Nebo **správce serveru**, klikněte na tlačítko **všechny servery**, klikněte pravým tlačítkem na název serveru a pak vyberte **přidat role a funkce**.

- Na **typ instalace** vyberte **instalace na základě rolí nebo na základě funkcí**.

- Na **funkce** rozbalte **prostředí Windows PowerShell (nainstalovaná)** uzel a vyberte možnost **modul Windows PowerShell 2.0**.

Informace o spouštění modulu Windows PowerShell 2.0 naleznete v tématu [spouštění modulu Windows PowerShell 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="on-earlier-systems"></a>V předchozích verzích systému
[Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881) balíček, který nainstaluje prostředí Windows PowerShell 4.0 na systém Windows 7, Windows Server 2008 R2 a Windows Server 2012, obsahuje modul Windows PowerShell 2.0. Modul Windows PowerShell 2.0 je aktivní a připravené k použití, v případě potřeby bez další instalace, instalace a konfigurace.

Balíček Windows Management Framework 3.0, který nainstaluje prostředí Windows PowerShell 3.0 v systému Windows 7, Windows Server 2008 R2 a Windows Server 2008, obsahuje modul Windows PowerShell 2.0. Modul Windows PowerShell 2.0 je aktivní a připravené k použití, v případě potřeby bez další instalace, instalace a konfigurace.

## <a name="see-also"></a>Viz také
- [Požadavky na prostředí PowerShell systému Windows](Windows-PowerShell-System-Requirements.md)
- [Instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md)
- [Spuštění prostředí Windows PowerShell](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)
- [Spuštění jádra Windows PowerShellu 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md)