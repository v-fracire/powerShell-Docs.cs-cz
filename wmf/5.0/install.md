---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 3679c13c2d28f28f3102b24f6369f1dc264d6884
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="installation-instructions"></a>Pokyny k instalaci

Stáhněte si správný balíček pro operační systém a architektura:

| Operační systém       | Architektura | Název balíčku              |
|------------------------|--------------|---------------------------|
| Windows Server 2012 R2 | x64      | [Win8.1AndW2K12R2-KB3134758-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) |
| Windows Server 2012    | x64      | [W2K12-KB3134759-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717506) |
| Windows Server 2008 R2 | x64      | [Win7AndW2K8R2-KB3134760-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504) |
| Windows 8.1            | x64          | [Win8.1AndW2K12R2-KB3134758-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) |
| Windows 8.1            | x86          | [Win8.1-KB3134758-x86.msu](http://go.microsoft.com/fwlink/?LinkID=717963) |
| Windows 7 SP1          | x64          | [Win7AndW2K8R2-KB3134760-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504) |
| Windows 7 SP1          | x86          | [Win7-KB3134760-x86.msu](http://go.microsoft.com/fwlink/?LinkID=717962) |


**K instalaci WMF 5.0 z Průzkumníka Windows (nebo v Průzkumníku souborů v systému Windows Server 2012 R2 a Windows 8.1):**

1. Přejděte do složky, do které jste stáhli soubor MSU.

2. Dvakrát klikněte na MSU ji spustit.

**K instalaci WMF 5.0 z příkazového řádku:**

1. Po stažení správný balíček pro architekturu vašeho počítače, otevřete okno příkazového řádku se zvýšenými uživatelskými právy (příkazem Spustit jako správce). V možnosti instalace jádra serveru systému Windows Server 2012 R2 nebo Windows Server 2012 nebo Windows Server 2008 R2 SP1 příkazový řádek se zvýšenými uživatelskými právy ve výchozím nastavení otevře.

2. Změňte adresář na složku, do které jste stáhli nebo zkopírovali instalační balíček WMF 5.0.

3. Spusťte jeden z následujících příkazů:
    - Na počítačích se systémem Windows Server 2012 R2 nebo Windows 8.1 x64 spusťte **Win8.1AndW2K12R2-KB3134758-x64.msu quiet**.
    - Na počítačích se systémem Windows Server 2012 spusťte **W2K12-KB3134759-x64.msu quiet**.
    - Na počítačích se systémem Windows Server 2008 R2 SP1 nebo Windows 7 SP1 x 64, spusťte **Win7AndW2K8R2-KB3134760-x64.msu quiet**.
    - Na počítačích se systémem Windows 8.1 x86 spusťte **Win8.1-KB3134758-x86.msu quiet**.
    - Na počítačích se systémem Windows 7 SP1 x 86 spusťte **Win7-KB3134760-x86.msu quiet**.

**Další poznámky k instalaci pro Windows Server 2008 SP1 a Windows 7 SP1:**

Zajistěte, aby byly splněny následující požadavky:
- Je nainstalována nejnovější aktualizaci service pack.
- [Formát WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) je nainstalován

*WinRM závislost:* požadovaného stavu aplikace Windows PowerShell (DSC) závisí na vzdálené správy systému Windows. WinRM není povoleno ve výchozím nastavení na Windows Server 2008 R2 a Windows 7. Chcete-li povolit WinRM, v prostředí Windows PowerShell se zvýšenými oprávněními spusťte relaci **Set-WSManQuickConfig**.
