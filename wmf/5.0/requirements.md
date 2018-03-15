---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 510e1baa2933932cfd4c3bcb4e0973f3eb8095f3
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="system-requirements"></a>Systémové požadavky

- Nainstalujte nejnovější aktualizace systému Windows před instalací WMF 5.0 RTM.
- WMF 5.0 RTM, můžete nainstalovat pouze na tyto operační systémy:

    | Operační systém       | Edice         | Předpoklady        |  Balíček odkazy |
    |------------------------|--------------|------------------|----------------------| --------------|
    | Windows Server 2012 R2 |  |  | [Win8.1AndW2K12R2-KB3134758-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) |
    | Windows Server 2012    |  |  | [W2K12-KB3134759-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717506) |
    | Windows Server 2008 R2 SP1 | Všechny, s výjimkou IA64 | [Formát WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) a [rozhraní .NET Framework 4.5 nebo vyšší](https://msdn.microsoft.com/library/5a4x27ek.aspx) jsou nainstalovány| [Win7AndW2K8R2-KB3134760-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504)|
    | Windows 8.1 | Pro, Enterprise | | **x64:**  [Win8.1AndW2K12R2-KB3134758-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) </br> **x86:**  [Win8.1-KB3134758-x86.msu](http://go.microsoft.com/fwlink/?LinkID=717963)|
    | Windows 7 SP1 | Vše | [Formát WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) a [rozhraní .NET Framework 4.5 nebo vyšší](https://msdn.microsoft.com/library/5a4x27ek.aspx) jsou nainstalovány | **x64:**  [Win7AndW2K8R2-KB3134760-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504)  </br> **x86:**  [Win7-KB3134760-x86.msu](http://go.microsoft.com/fwlink/?LinkID=717962)|

# <a name="installation-instructions"></a>Pokyny k instalaci

### <a name="to-install-wmf-50-from-windows-explorer-or-file-explorer"></a>K instalaci WMF 5.0 z Průzkumníka Windows (nebo v Průzkumníku souborů):

1. Přejděte do složky, do které jste stáhli soubor MSU.

2. Dvakrát klikněte na MSU ji spustit.

### <a name="to-install-wmf-50-from-command-prompt"></a>K instalaci WMF 5.0 z příkazového řádku:

1. Po stažení správný balíček pro architekturu vašeho počítače, otevřete okno příkazového řádku se zvýšenými uživatelskými právy (příkazem Spustit jako správce). V možnosti instalace jádra serveru systému Windows Server 2012 R2 nebo Windows Server 2012 nebo Windows Server 2008 R2 SP1 příkazový řádek se zvýšenými uživatelskými právy ve výchozím nastavení otevře.

2. Změňte adresář na složku, do které jste stáhli nebo zkopírovali instalační balíček WMF 5.0.

3. Spusťte jeden z následujících příkazů:
    - Na počítačích se systémem Windows Server 2012 R2 nebo Windows 8.1 x64 spusťte **Win8.1AndW2K12R2-KB3134758-x64.msu quiet**.
    - Na počítačích se systémem Windows Server 2012 spusťte **W2K12-KB3134759-x64.msu quiet**.
    - Na počítačích se systémem Windows Server 2008 R2 SP1 nebo Windows 7 SP1 x 64, spusťte **Win7AndW2K8R2-KB3134760-x64.msu quiet**.
    - Na počítačích se systémem Windows 8.1 x86 spusťte **Win8.1-KB3134758-x86.msu quiet**.
    - Na počítačích se systémem Windows 7 SP1 x 86 spusťte **Win7-KB3134760-x86.msu quiet**.

### <a name="additional-installation-notes-for-windows-server-2008-r2-sp1-and-windows-7-sp1"></a>Další poznámky k instalaci pro Windows Server 2008 R2 SP1 a Windows 7 SP1:

Zajistěte, aby byly splněny následující požadavky:
- Je nainstalována nejnovější aktualizaci service pack.
- [Formát WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) je nainstalovaná.
- [Rozhraní .NET framework 4.5 nebo vyšší](https://msdn.microsoft.com/library/5a4x27ek.aspx) je nainstalovaná.

**Formát WMF 4.0 závislostí**

Systémy Windows Server 2008 R2 SP1 a Windows 7 SP1 mají integrované prostředí PowerShell 2.0, WinRM a WMI. Podpora produktu WMF 3.0 a WMF 4.0 balíčků, které aktualizace těchto integrované komponenty, byly vydané po vydání verze Windows Server 2008 R2 SP1 a Windows 7 SP1. Instalace nebo odinstalace produktu WMF 3.0 a WMF 4.0 balíčky zjištěných některé problémy v následující cestě upgradu:

- Předdefinované--> WMF 4.0
- Built-in --> WMF 3.0 --> WMF4.0. 

Vyřešili všechny tyto problémy v balíčcích WMF 4.0. Pro instalaci WMF 5.0 na Windows Server 2008 R2 SP1 a Windows 7 SP1 je proto předpokladem WMF 4.0. V následující tabulce jsou konkrétní problémy, které mohou nastat pokud před upgradem na verzi WMF 5.0 nenainstalujete WMF 4.0:

- Přesměrovaná protokolu událostí není k dispozici a EventCollector protokolu není zobrazené v prohlížeči událostí po odinstalaci produktu WMF 3.0 nebo WMF 5.0 (bez požadovaných WMF 4.0 nainstalované) v systému Windows 7 SP1 a Windows Server 2008 R2 SP1 ([KB2809215](https://support.microsoft.com/en-us/kb/2809215)).
- Přizpůsobení *PSModulePath* proměnnou prostředí získá resetovat na výchozí hodnotu, při upgradu přímo z integrované prostředí PowerShell 2.0 na WMF 5.0 ([KB2872035](https://support.microsoft.com/en-us/kb/2872035)) nebo z produktu WMF 3.0 na WMF 5.0. ([KB2872047](https://support.microsoft.com/en-us/kb/2872047)) v systému Windows 7 SP1 a Windows Server 2008 R2 SP1.

**WinRM závislostí**

Požadovaného stavu aplikace Windows PowerShell (DSC) závisí na vzdálené správy systému Windows. WinRM není povoleno ve výchozím nastavení v systému Windows Server 2008 R2 SP1 a Windows 7 SP1. Chcete-li povolit WinRM, v prostředí Windows PowerShell se zvýšenými oprávněními spusťte relaci **Set-WSManQuickConfig**.

# <a name="uninstallation-instructions"></a>Odinstalace pokyny

### <a name="using-command-prompt"></a>Pomocí příkazového řádku

1.  Otevřete **příkazového řádku.**

2.  Spustit [Spouštěč samostatné aktualizace Windows](https://support.microsoft.com/en-us/kb/934307) jak je uvedeno níže:

V systému Windows Server 2012 R2 a Windows 8.1:
```powershell
wusa /uninstall /kb:3134758
```
On Windows Server 2012:
```powershell
wusa /uninstall /kb:3134759
```
Na Windows Server 2008 R2 SP1 a Windows 7 SP1:
```powershell
wusa /uninstall /kb:3134760
```

### <a name="using-control-panel"></a>Pomocí ovládacích panelů

1.  Otevřete **ovládací panely.**

2.  Otevřete **programy**, pak otevřete **odinstalovat program.**

3.  Klikněte na tlačítko **zobrazit nainstalované aktualizace.**

4.  Vyberte **Windows Management Framework 5.0** ze seznamu nainstalovaných aktualizací. To odpovídá *KB3134758*, *KB3134759*, nebo *KB3134760*. Klikněte na tlačítko **odinstalovat.**

