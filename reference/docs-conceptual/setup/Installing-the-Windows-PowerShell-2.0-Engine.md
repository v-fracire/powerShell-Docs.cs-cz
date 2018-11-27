---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Instalace jádra Windows PowerShellu 2.0
ms.assetid: 82928f2b-f96a-4ae6-a0d0-6e7b181da308
ms.openlocfilehash: fb5ed1a5508ddca6925e9281a53caf5e6701870f
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320495"
---
# <a name="installing-the-windows-powershell-20-engine"></a>Instalace jádra Windows PowerShellu 2.0
Toto téma vysvětluje, jak nainstalovat modul Windows PowerShell 2.0.

Windows PowerShell 3.0 je navržena jako zpětně kompatibilní s Windows PowerShell 2.0. Rutiny, poskytovatelů, moduly snap in, moduly a skriptech psaných pro Windows PowerShell 2.0 bez jakýchkoli změn ve Windows Powershellu 3.0 a Windows PowerShell 4.0. Nicméně z důvodu změn v zásadách aktivace modulu runtime v rozhraní Microsoft .NET Framework 4, programy hostitele prostředí Windows PowerShell, které byly napsány pro Windows PowerShell 2.0 a zkompilován s Common Language Runtime (CLR) 2.0 nelze spustit beze změny v později verze prostředí Windows PowerShell, který je kompilován s CLR 4.0.

Zachování zpětné kompatibility s příkazy a hostitele programy, které jsou těmito změnami ovlivněny, moduly Windows Powershellu 2.0, Windows PowerShell 3.0 a Windows PowerShell 4.0 slouží ke spouštění vedle sebe. Modul Windows PowerShell 2.0 je také součástí systému Windows Server 2012 R2, Windows 8.1, Windows 8, Windows Server 2012 a Windows Management Framework 3.0. Modul Windows PowerShell 2.0 je určena pro použití pouze v případě stávajícího skriptu nebo hostitele program nelze spustit, protože není kompatibilní s Windows PowerShell 3.0, Windows PowerShell 4.0 nebo Microsoft .NET Framework 4. Očekává se, že tyto případy docházet zřídka.

Modul Windows PowerShell 2.0 je volitelná funkce systému Windows Server 2012 R2, Windows 8.1, Windows® 8 a systému Windows Server® 2012. Ve starších verzích Windows když instalujete Windows Management Framework 3.0 instalace Windows Powershellu 3.0 zcela nahrazují instalace Windows PowerShell 2.0 v adresáři instalace prostředí Windows PowerShell. Nicméně se uchovávají modul Windows PowerShell 2.0.

Informace o spuštění jádra Windows Powershellu 2.0 najdete v tématu [spuštění jádra Windows Powershellu 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="on-windows-81-and-windows-8"></a>Zařízení s Windows 8.1 a Windows 8
Na Windows 8.1 a Windows 8 je funkce jádra Windows Powershellu 2.0 ve výchozím nastavení zapnutá. Však použít, budete muset zapnout možnost pro rozhraní Microsoft .NET Framework 3.5, který vyžaduje. Tato část také vysvětluje, jak zapnout a vypnout funkci modul Windows PowerShell 2.0.

#### <a name="to-turn-on-net-framework-35"></a>Chcete-li na rozhraní .NET Framework 3.5

1. Na **Start** zadejte **funkce Windows**.

2. Na **aplikace** panelu, klikněte na tlačítko **nastavení**a potom klikněte na tlačítko **Windows zapnout nebo vypnout funkce**.

3. V **funkce Windows** klikněte **rozhraní .NET Framework 3.5 (zahrnuje .NET 2.0 a 3.0** ji vyberte.

    Když vyberete **rozhraní .NET Framework 3.5 (zahrnuje .NET 2.0 a 3.0**, pole se vyplní k označení, že je vybrána pouze část funkce. To je však dostatečná pro modul Windows PowerShell 2.0.

#### <a name="to-turn-the-windows-powershell-20-engine-on-and-off"></a>K zapnutí a vypnutí modulu Windows Powershellu 2.0

1. Na **Start** zadejte **funkce Windows**.

2. Na **aplikace** panelu, klikněte na tlačítko **nastavení**a potom klikněte na tlačítko **Windows zapnout nebo vypnout funkce**.

3. V **funkce Windows** rozbalte **Windows PowerShell 2.0** uzel a klikněte na tlačítko **jádra Windows Powershellu 2.0** a vyberte nebo zrušte zaškrtnutí.

## <a name="on-windows-server-2012-r2-and-windows-server-2012"></a>V systému Windows Server 2012 R2 a Windows Server 2012
Pomocí následujících postupů můžete přidat modul Windows PowerShell 2.0 a funkce rozhraní Microsoft .NET Framework 3.5. Modul Windows PowerShell 2.0 vyžaduje rozhraní Microsoft .NET Framework 2.0.50727 minimálně. Tento požadavek splněn rozhraním Microsoft .NET Framework 3.5.

#### <a name="to-add-the-net-framework-35-feature"></a>Chcete-li přidat funkci rozhraní .NET Framework 3.5

1. V **správce serveru**, z **spravovat** nabídce vyberte možnost **přidat role a funkce**.

    Nebo v **správce serveru**, klikněte na tlačítko **všechny servery**, klikněte pravým tlačítkem na název serveru a pak vyberte **přidat role a funkce**.

2. Na **typ instalace** stránce **instalace na základě rolí nebo na základě funkcí**.

3. Na **funkce** stránce, rozbalte **funkce rozhraní .NET Framework 3.5** uzel a vyberte možnost **rozhraní .NET Framework 3.5 (zahrnuje .NET 2.0 a 3.0)**.

    Další možnosti v tomto uzlu se nevyžadují pro modul Windows PowerShell 2.0.

#### <a name="to-add-the-windows-powershell-20-engine-feature"></a>Chcete-li přidat funkci modul Windows Powershellu 2.0

- V **správce serveru**, z **spravovat** nabídce vyberte možnost **přidat role a funkce**.

    Nebo **správce serveru**, klikněte na tlačítko **všechny servery**, klikněte pravým tlačítkem na název serveru a pak vyberte **přidat role a funkce**.

- Na **typ instalace** stránce **instalace na základě rolí nebo na základě funkcí**.

- Na **funkce** stránce, rozbalte **prostředí Windows PowerShell (nainstalováno)** uzel a vyberte možnost **jádra Windows Powershellu 2.0**.

Informace o spuštění jádra Windows Powershellu 2.0 najdete v tématu [spuštění jádra Windows Powershellu 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="on-earlier-systems"></a>V předchozích verzích systému
[Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkID=293881) balíček, který nainstaluje Windows 7, Windows Server 2008 R2 a Windows Server 2012, Windows PowerShell 4.0 obsahuje modul Windows PowerShell 2.0. Modul Windows PowerShell 2.0 je aktivní a připravený k použití, v případě potřeby bez další instalace, konfigurace nebo nastavení.

Balíček Windows Management Framework 3.0, která nainstaluje Windows 7, Windows Server 2008 R2 a Windows Server 2008, Windows PowerShell 3.0 obsahuje modul Windows PowerShell 2.0. Modul Windows PowerShell 2.0 je aktivní a připravený k použití, v případě potřeby bez další instalace, konfigurace nebo nastavení.

## <a name="see-also"></a>Viz také
- [Požadavky na prostředí PowerShell systému Windows](Windows-PowerShell-System-Requirements.md)
- [Instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md)
- [Spuštění Windows Powershellu](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)
- [Spuštění jádra Windows PowerShellu 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md)