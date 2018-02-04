---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
contributor: keithb
title: Instalace a konfigurace WMF 5.1
ms.openlocfilehash: f58676de6f7a5c51ba586a8c607097af8e60d0c9
ms.sourcegitcommit: 18e3bfae83ffe282d3fd1a45f5386f3b7250f0c0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/03/2018
---
# <a name="install-and-configure-wmf-51"></a>Instalace a konfigurace WMF 5.1 #


## <a name="download-and-install-the-wmf-51-package"></a>Stáhněte a nainstalujte balíček WMF 5.1

Stáhněte si balíček WMF 5.1 pro operační systém a architektura, které chcete nainstalovat na:

| Operační systém       | Předpoklady           | Balíček odkazy                          |
|------------------------|-------------------------|----------------------------------------|
| Windows Server 2012 R2 |                         | [Win8.1AndW2K12R2-KB3191564-x64.msu][] |
| Windows Server 2012    |                         | [W2K12-KB3191565-x64.msu][]            |
| Windows Server 2008 R2 | [.NET Framework 4.5.2][]| [Win7AndW2K8R2-KB3191566-x64.ZIP][]    |
| Windows 8.1            |                         | **x64:** [Win8.1AndW2K12R2-KB3191564-x64.msu][]</br>**x86:** [Win8.1-KB3191564-x86.msu][] |
| Windows 7 SP1          | [.NET Framework 4.5.2][]| **x64:** [Win7AndW2K8R2-KB3191566-x64.ZIP][]</br>**x86:** [Win7-KB3191566-x86.ZIP][] |

[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42642
[W2K12-KB3191565-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839513
[Win7-KB3191566-x86.ZIP]: https://go.microsoft.com/fwlink/?linkid=839522
[Win7AndW2K8R2-KB3191566-x64.ZIP]: https://go.microsoft.com/fwlink/?linkid=839523
[Win8.1-KB3191564-x86.msu]: https://go.microsoft.com/fwlink/?linkid=839521
[Win8.1AndW2K12R2-KB3191564-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839516

## <a name="install-wmf-51-for-windows-server-2008-r2-and-windows-7"></a>WMF 5.1 nainstalovat pro systém Windows Server 2008 R2 a Windows 7

> **Poznámka:** pokyny k instalaci pro Windows Server 2008 R2 a Windows 7 změnily a se liší od pokynů pro ostatní balíčky. Pokyny k instalaci pro Windows Server 2012 R2, Windows Server 2012 a Windows 8.1 jsou níže.

**Instalaci WMF 5.1 v systému Windows Server 2008 R2 a Windows 7**

1. Přejděte do složky, do které jste stáhli soubor ZIP.

2. Klikněte pravým tlačítkem na soubor ZIP a vyberte "Extrahujte všechny...". Souboru Zip obsahuje soubory, 2: MSU a souboru skriptu instalace WMF5.1.PS1.
Jakmile jste rozbalili souboru ZIP, můžete zkopírovat obsah do jakéhokoli počítače se systémem Windows 7 nebo Windows Server 2008 R2.

3. Po extrahování obsahu souboru ZIP, otevřete PowerShell jako správce a pak přejděte do složky obsahující obsah souboru ZIP.

4. Spuštění skriptu Install-Wmf5.1.ps1 v této složce a postupujte podle pokynů. Tento skript zkontroluje požadavky v místním počítači a nainstalujte WMF 5.1, pokud byly splněny požadavky. Požadavky jsou uvedené níže.

Instalace WMF5.1.ps1 mají následující parametry k usnadnění automatizace instalaci na Windows Server 2008 R2 a Windows 7:

- AcceptEula: Pokud je tento parametr zahrnuta, se smlouvou EULA automaticky přijato a nebudou zobrazeny.
- AllowRestart: Tento parametr můžete pouze použijí, pokud je zadán AcceptEula. Pokud tento parametr je součástí, a po instalaci WMF 5.1 je vyžadováno restartování, stane se restartování bez zobrazení výzvy ihned po dokončení instalace.

**WMF 5.1 požadavky pro Windows Server 2008 R2 SP1 a Windows 7 SP1**

Instalaci WMF 5.1 v systému Windows Server 2008 R2 SP1 nebo Windows 7 SP1 vyžaduje následující:
- Musí být nainstalován nejnovější aktualizaci service pack.
- Podpora produktu WMF 3.0 **musí není** nainstalovat. Instalaci WMF 5.1 přes WMF 3.0, bude mít za následek ztrátu PSModulePath, což může způsobit chybu jiných aplikací. Před instalací WMF 5.1, musíte buď odinstalaci produktu WMF 3.0, nebo uložit PSModulePath a obnovte ji ručně po dokončení instalace WMF 5.1.
- WMF 5.1 vyžaduje alespoň [rozhraní .NET Framework 4.5.2](https://www.microsoft.com/en-ca/download/details.aspx?id=42642).
Podle pokynů v umístění můžete nainstalovat rozhraní Microsoft .NET Framework 4.5.2.

**WinRM závislostí**

Požadovaného stavu aplikace Windows PowerShell (DSC) závisí na vzdálené správy systému Windows.
WinRM není povoleno ve výchozím nastavení na Windows Server 2008 R2 a Windows 7.
Spustit `Set-WSManQuickConfig`, v prostředí Windows PowerShell se zvýšenými oprávněními relace, aby Služba WinRM.


## <a name="install-wmf-51-for-windows-server-2012-r2-windows-server-2012-and-windows-81"></a>WMF 5.1 nainstalovat pro systém Windows Server 2012 R2, Windows Server 2012 a Windows 8.1
**Nainstalujte z Průzkumníka Windows (nebo v Průzkumníku souborů v systému Windows Server 2012 R2 nebo Windows 8.1)**

1. Přejděte do složky, do které jste stáhli soubor MSU.
2. Dvakrát klikněte na MSU ji spustit.

**Instalace z příkazového řádku**

1. Po stažení správný balíček pro architekturu vašeho počítače, otevřete okno příkazového řádku se zvýšenými uživatelskými právy (příkazem Spustit jako správce). V možnosti instalace jádra serveru systému Windows Server 2012 R2, Windows Server 2012 nebo Windows Server 2008 R2 SP1 příkazový řádek se zvýšenými uživatelskými právy ve výchozím nastavení otevře.
2. Změňte adresář na složku, do které jste stáhli nebo zkopírovat WMF 5.1 instalační balíček.
3. Spusťte jeden z následujících příkazů:
   - Na počítačích se systémem Windows Server 2012 R2 nebo Windows 8.1 x64 spusťte `Win8.1AndW2K12R2-KB3191564-x64.msu /quiet`.
   - Na počítačích se systémem Windows Server 2012 spusťte `W2K12-KB3191565-x64.msu /quiet`.
   - Na počítačích se systémem Windows 8.1 x86 spusťte `Win8.1-KB3191564-x86.msu /quiet`.

> [!NOTE]
> Instalaci WMF 5.1 vyžaduje restartování počítače. Pomocí `/quiet` možnost se restartovat systém bez upozornění.
> Použití `/norestart` možnost, aby se zabránilo restartování. WMF 5.1 však nebudou nainstalovány, dokud je restartovat.