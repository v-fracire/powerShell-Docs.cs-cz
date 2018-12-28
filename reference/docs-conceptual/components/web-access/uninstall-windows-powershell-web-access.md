---
ms.date: 08/23/2017
keywords: rutiny prostředí PowerShell
title: odinstalace windows powershell web Accessu
ms.openlocfilehash: 22c874d766445dccedd8494097daf16c30fa66ff
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404051"
---
# <a name="uninstall-windows-powershell-web-access"></a>Odinstalace Windows PowerShell Web Accessu

Aktualizováno: 24. června 2013

Platí pro: Windows Server 2012 R2, Windows Server 2012

Kroky v tomto tématu odebrat ze serveru brány, kde je nainstalovaný Windows PowerShell Web Accessu webu a příslušné aplikace.

## <a name="notify-users"></a>Upozornit uživatele

Než začnete, upozorněte uživatele webové konzoly, že tento web odeberete.

Odinstalace Windows PowerShell Web Accessu neodinstaluje službu IIS ani žádné další funkce, které byly nainstalovány automaticky, protože Windows PowerShell Web Accessu vyžaduje, aby běžela.
Proces odinstalace ponechá funkce nainstalované, na kterých byl závislé; Windows PowerShell Web Accessu v případě potřeby, můžete tyto funkce odinstalovat samostatně.

## <a name="recommended-quick-uninstallation"></a>Doporučená (rychlá) odinstalace

Postupy v této části vám umožní odinstalovat obojí:

- Webová aplikace Windows PowerShell Web Accessu a
- funkci Windows PowerShell Web Accessu

pomocí rutin Windows Powershellu.

### <a name="step-1-delete-the-web-application-using-cmdlets"></a>Krok 1: Odstranění webové aplikace pomocí rutin

1. Proveďte jednu z následujících akcí otevřete relaci Windows Powershellu.

    -   Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu.

    -   V Windows **Start** obrazovce, klikněte na tlačítko **prostředí Windows PowerShell**.

2. Typ `Uninstall-PswaWebApplication`a potom stiskněte klávesu **Enter**.
   1. Pokud jste zadali vlastní název webu, přidejte do příkazu parametr `-WebsiteName` a zadejte název tohoto webu.

        `Uninstall-PswaWebApplication -WebsiteName <web-site-name>`
   1. Pokud jste použili vlastní webovou aplikaci (ne výchozí aplikaci, **pswa**, přidejte `-WebApplicationName` parametr k příkazu a zadejte název webové aplikace.

        `Uninstall-PswaWebApplication -WebApplicationName <web-application-name>`
   1. Pokud používáte testovací certifikát, přidejte do rutiny parametr `DeleteTestCertificate` jako v tomto příkladu.

        `Uninstall-PswaWebApplication -DeleteTestCertificate`

### <a name="step-2-uninstall-windows-powershell-web-access-using-cmdlets"></a>Krok 2: Odinstalace Windows PowerShell Web Accessu pomocí rutin

1. Proveďte jednu z následujících akcí otevřete relaci Windows Powershellu se zvýšenými uživatelskými právy. Jestli je relace už otevřená, přejděte na další krok.

    -   Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu a pak klikněte na tlačítko **spustit jako správce**.

    -   V Windows **Start** obrazovce, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na tlačítko **spustit jako správce**.

1. Zadejte následující příkaz a stiskněte klávesu **Enter**, kde *název_počítače* je vzdálený server, ze kterého chcete odebrat Windows PowerShell Web Accessu. Parametr `-Restart` automaticky restartuje cílové servery, pokud to odebrání vyžaduje.

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -ComputerName <computer_name> -Restart

    Pokud chcete odebrat role a funkce z offline virtuálního pevného disku, je nutné přidat parametr `-ComputerName` i parametr `-VHD`. Parametr `-ComputerName` obsahuje název serveru, ke kterému chcete připojit virtuální pevný disk. Parametr `-VHD` pak obsahuje cestu k souboru VHD na určeném serveru.

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -VHD <path> -ComputerName <computer_name> -Restart

1. Po dokončení odebrání ověřte, že odeberete tak, že otevřete Windows PowerShell Web Accessu **všechny servery** stránku ve Správci serveru, vyberete server, ze kterého jste tuto funkci odebrali a zobrazení **role a Funkce** dlaždice na stránce vybraného serveru.

    Můžete taky spustit `Get-WindowsFeature` rutinu určenou pro vybraný server (Get-WindowsFeature - ComputerName &lt; *název_počítače*&gt;) Chcete-li zobrazit seznam rolí a funkcí nainstalovaných na serveru.

## <a name="custom-uninstallation"></a>Vlastní odinstalace

Postupy v této části vám umožní odinstalovat webovou aplikaci Windows PowerShell Web Accessu a funkci Windows PowerShell Web Accessu pomocí odebrat role a funkce Průvodce ve Správci serveru a konzoly Správce služby IIS.

### <a name="step-1-delete-the-web-application-using-iis-manager"></a>Krok 1: Odstranění webové aplikace pomocí Správce služby IIS


1. Otevřete konzolu Správce služby IIS některým z následujících postupů. Jestli je už otevřená, přejděte na další krok.

    -   Na ploše Windows spusťte Správce serveru klikněte na **správce serveru** na hlavním panelu Windows. Na **nástroje** nabídky ve Správci serveru klikněte na tlačítko **Správce Internetové informační služby (IIS)**.

    -   V Windows **Start** zadejte libovolné části názvu **Správce Internetové informační služby (IIS)**. Až se zobrazí, klikněte na zástupce **aplikace** výsledky.

1. V podokně stromu Správce služby IIS vyberte web, na kterém běží webová aplikace Windows PowerShell Web Accessu.

1. V **akce** podokně v části **spravovat web**, klikněte na tlačítko **Zastavit**.

1. V podokně stromu klikněte pravým tlačítkem na webovou aplikaci na webu, na kterém běží webová aplikace Windows PowerShell Web Accessu a potom klikněte na tlačítko **odebrat**.

1. V podokně stromu vyberte **fondy aplikací**, vyberte složku fondu aplikací Windows PowerShell Web Accessu, klikněte na tlačítko **Zastavit** v **akce** podokně a pak klikněte na tlačítko  **Odebrat** v podokně obsahu.

1. Zavřete Správce služby IIS.

> ![Poznámka: upozornění](images/SecurityNote.jpeg)**Poznámka**:
>
> Certifikát se během odinstalace neodstraní.
>
> Pokud jste vytvořili certifikát podepsaný svým držitelem nebo použili testovací certifikát a chcete ho odebrat, odstraňte certifikát ve Správci služby IIS.

### <a name="step-2-uninstall-windows-powershell-web-access-using-the-remove-roles-and-features-wizard"></a>Krok 2: Odinstalace Windows PowerShell Web Accessu pomocí funkce Průvodce odebráním rolí a

1. Pokud správce serveru je už otevřená, přejděte k dalšímu kroku. Správce serveru ještě není otevřený, otevřete ho jedním z následujících akcí.

    -   Na ploše Windows spusťte Správce serveru klikněte na **správce serveru** na hlavním panelu Windows.

    -   V Windows **Start** obrazovce, klikněte na tlačítko **správce serveru**.

1. Na **spravovat** nabídky, klikněte na tlačítko **odebrat role a funkce**.

1. Na **vybrat cílový server** stránky, vyberte server nebo offline virtuální pevný disk, ze kterého chcete odebrat tuto funkci. Pokud chcete zvolit offline virtuální pevný disk,  vyberte nejdřív server, ke kterému chcete virtuální pevný disk připojit, a pak vyberte příslušný soubor VHD. Po výběru cílového serveru, klikněte na tlačítko **Další**.

1. Klikněte na tlačítko **Další** znovu přejděte do **odebrat funkce** stránky.

1. Zrušte zaškrtnutí políčka pro **Windows PowerShell Web Accessu**a potom klikněte na tlačítko **Další**.

1. Na **potvrdit vybrané možnosti odebrání** klikněte na **odebrat**.

## <a name="see-also"></a>Viz také

- [Nainstalovat a používat Windows PowerShell Web Accessu](install-and-use-windows-powershell-web-access.md)
- [Nápověda k aplikaci IIS 7.0 Manager](https://technet.microsoft.com/library/cc732664.aspx)