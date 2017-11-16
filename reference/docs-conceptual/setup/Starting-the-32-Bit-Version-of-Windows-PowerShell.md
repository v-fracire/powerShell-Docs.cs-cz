---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Spuštění 32bitové verze prostředí Windows PowerShell"
ms.assetid: 12b31890-2609-4a76-8c24-0ebe78084f50
ms.openlocfilehash: d682ce45ebc92cda3a9008ab608bacf9ef8eba57
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="starting-the-32-bit-version-of-windows-powershell"></a>Spuštění 32bitové verze prostředí Windows PowerShell
Při instalaci prostředí Windows PowerShell na 64bitovém počítači **prostředí Windows PowerShell (x86)**, 32bitová verze prostředí Windows PowerShell je nainstalovaný kromě 64bitovou verzi. Při spuštění prostředí Windows PowerShell ve výchozím nastavení spustí 64bitovou verzi.

Však může někdy musíte spustit **prostředí Windows PowerShell (x86)**, například při použití modulu, který vyžaduje 32bitovou verzi nebo kdy se vzdáleně připojují k 32bitového počítače.

Spusťte 32bitovou verzi prostředí Windows PowerShell, použijte některý z následujících postupů.

#### <a name="in-windows-server-2012-r2"></a>V systému Windows Server® 2012 R2

- Na **spustit** zadejte **prostředí Windows PowerShell (x86)**. Klikněte **prostředí Windows PowerShell x86** dlaždici.

- V **správce serveru**, z **nástroje** nabídce vyberte možnost **prostředí Windows PowerShell (x86)**.

- Přesunutí kurzoru do pravého horního rohu klikněte na ploše **vyhledávání**, typ **prostředí PowerShell x86** a pak klikněte na **prostředí Windows PowerShell (x86)**.

- Prostřednictvím příkazového řádku zadejte:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-server-2012"></a>V systému Windows Server® 2012

- Na **spustit** zadejte **prostředí PowerShell** a pak klikněte na **prostředí Windows PowerShell (x86)**.

- V **správce serveru**, z **nástroje** nabídce vyberte možnost **prostředí Windows PowerShell (x86)**.

- Přesunutí kurzoru do pravého horního rohu klikněte na ploše **vyhledávání**, typ **prostředí PowerShell** a pak klikněte na **prostředí Windows PowerShell (x86)**.

- Prostřednictvím příkazového řádku zadejte:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-81"></a>V Windows® 8.1

- Na **spustit** zadejte **prostředí Windows PowerShell (x86)**. Klikněte **prostředí Windows PowerShell x86** dlaždici.

- Pokud používáte [nástrojů pro vzdálenou správu serveru](http://go.microsoft.com/fwlink/?LinkID=304145) pro Windows 8.1, můžete také otevřít prostředí Windows PowerShell x86 z **Server ManagerTools** nabídky. Vyberte **prostředí Windows PowerShell (x86)**.

- Přesunutí kurzoru do pravého horního rohu klikněte na ploše **vyhledávání**, typ **prostředí PowerShell x86** a pak klikněte na **prostředí Windows PowerShell (x86)**.
   
- Prostřednictvím příkazového řádku zadejte:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-8"></a>V Windows® 8

- Na **spustit** obrazovky, přesuňte se ukazatelem do pravého horního rohu, klikněte na **nastavení**, klikněte na tlačítko **dlaždice**a poté přesuňte **zobrazit nástroje pro správu** jezdec na Ano. Poté zadejte **prostředí PowerShell** a klikněte na tlačítko **prostředí Windows PowerShell (x86)**.

- Pokud používáte [nástrojů pro vzdálenou správu serveru](http://www.microsoft.com/download/details.aspx?id=28972) pro systém Windows 8, můžete také otevřít prostředí Windows PowerShell x86 z **Server ManagerTools** nabídky. Vyberte **prostředí Windows PowerShell (x86)**.

- Na **spustit** obrazovky nebo plocha, zadejte **prostředí PowerShell (x86)** a pak klikněte na **prostředí Windows PowerShell (x86)**.

- Prostřednictvím příkazového řádku zadejte:`%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

