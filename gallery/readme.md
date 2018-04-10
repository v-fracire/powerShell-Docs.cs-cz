---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery, psget
title: Galerie prostředí PowerShell
ms.openlocfilehash: 9519b8bcca9f43419a33db380c3b852e9bb354ac
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="the-powershell-gallery"></a>Galerie prostředí PowerShell

Galerie prostředí PowerShell je centrálním úložištěm pro obsah prostředí PowerShell. Nové příkazy prostředí PowerShell nebo prostředky konfigurace požadovaného stavu (DSC) najdete v galerii.

## <a name="powershellget-overview"></a>Přehled PowerShellGet

Tento modul PowerShellGet obsahuje rutiny pro zjišťování, instalaci, aktualizaci a publikování prostředí PowerShell artefaktů, jako jsou moduly, prostředků DSC, funkce Role a skripty od [Galerie prostředí PowerShell](https://www.PowerShellGallery.com) a jiné privátní úložiště.

## <a name="getting-started-with-the-gallery"></a>Začínáme s Galerie

Instalace položky z Galerie vyžaduje nejnovější verzi PowerShellGet modul, který je k dispozici v systému Windows 10, v systému Windows Management Framework (WMF) 5.0 nebo v instalačním programu na základě MSI (pro prostředí PowerShell 3 a 4).

- [**Get Windows 10**](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409),
- [**Získat WMF 5.0**](http://go.microsoft.com/fwlink/?LinkId=398175), nebo
- [**Získání Instalační služby MSI**](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

Na nejnovější [PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) modul, můžete:

-   Vyhledávání pomocí položky v galerii s [najít modulu](https://go.microsoft.com/fwlink/?LinkId=821658) a [najít skriptu](https://go.microsoft.com/fwlink/?LinkId=822322)
-   Uložit položky do systému z galerie s [uložit modulu](https://go.microsoft.com/fwlink/?LinkId=821669) a [uložit skriptu](https://go.microsoft.com/fwlink/?LinkId=822334)
-   Nainstalujte položky z galerie s [instalace modulu](https://go.microsoft.com/fwlink/?LinkId=821663) a [instalační skript](https://go.microsoft.com/fwlink/?LinkId=822327)
-   Nahrát položky do galerie s [publikovat modulu](https://go.microsoft.com/fwlink/?LinkId=821666) a [publikovat skriptu](https://go.microsoft.com/fwlink/?LinkId=822331)
-   Přidat vlastní úložiště s [PSRepository registrace](https://go.microsoft.com/fwlink/?LinkId=821668)

Podívejte se [Začínáme](psgallery/psgallery_gettingstarted.md) stránka Další informace o tom, jak pomocí příkazů PowerShellGet galerie. Můžete také spouštět *Update-Help-modulu PowerShellGet* k instalaci místní Nápověda pro tyto příkazy.

## <a name="supported-operating-systems"></a>Podporované operační systémy

**PowerShellGet** module vyžaduje **prostředí PowerShell 3.0 nebo novější**.

Proto **PowerShellGet** vyžaduje jednu z následujících operačních systémů:

- Windows 10
- Windows 8.1 Pro
- Windows 8.1 Enterprise
- Windows 7 SP1
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2008 R2 SP1

**PowerShellGet** taky vyžaduje rozhraní .NET Framework 4.5 nebo novější. Můžete nainstalovat rozhraní .NET Framework 4.5 nebo novější z [zde](https://msdn.microsoft.com/library/5a4x27ek.aspx).


## <a name="got-a-question-have-feedback"></a>Máte dotaz? Zpětné vazby máte?

Další informace o galerii prostředí PowerShell a PowerShellGet najdete v [Začínáme](psgallery/psgallery_gettingstarted.md) stránky. Zadejte prosím zpětnou vazbu a sestava problémy s [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).