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
# <a name="uninstall-windows-powershell-web-access"></a><span data-ttu-id="66a2e-103">Odinstalace Windows PowerShell Web Accessu</span><span class="sxs-lookup"><span data-stu-id="66a2e-103">Uninstall Windows PowerShell Web Access</span></span>

<span data-ttu-id="66a2e-104">Aktualizováno: 24. června 2013</span><span class="sxs-lookup"><span data-stu-id="66a2e-104">Updated: June 24, 2013</span></span>

<span data-ttu-id="66a2e-105">Platí pro: Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="66a2e-105">Applies To: Windows Server 2012 R2, Windows Server 2012</span></span>

<span data-ttu-id="66a2e-106">Kroky v tomto tématu odebrat ze serveru brány, kde je nainstalovaný Windows PowerShell Web Accessu webu a příslušné aplikace.</span><span class="sxs-lookup"><span data-stu-id="66a2e-106">The steps in this topic remove the Windows PowerShell Web Access website and corresponding application from the gateway server where it is installed.</span></span>

## <a name="notify-users"></a><span data-ttu-id="66a2e-107">Upozornit uživatele</span><span class="sxs-lookup"><span data-stu-id="66a2e-107">Notify users</span></span>

<span data-ttu-id="66a2e-108">Než začnete, upozorněte uživatele webové konzoly, že tento web odeberete.</span><span class="sxs-lookup"><span data-stu-id="66a2e-108">Before you begin, notify users of the web-based console that you are removing the website.</span></span>

<span data-ttu-id="66a2e-109">Odinstalace Windows PowerShell Web Accessu neodinstaluje službu IIS ani žádné další funkce, které byly nainstalovány automaticky, protože Windows PowerShell Web Accessu vyžaduje, aby běžela.</span><span class="sxs-lookup"><span data-stu-id="66a2e-109">Uninstalling Windows PowerShell Web Access does not uninstall IIS or any other features that were installed automatically because Windows PowerShell Web Access requires them to run.</span></span>
<span data-ttu-id="66a2e-110">Proces odinstalace ponechá funkce nainstalované, na kterých byl závislé; Windows PowerShell Web Accessu v případě potřeby, můžete tyto funkce odinstalovat samostatně.</span><span class="sxs-lookup"><span data-stu-id="66a2e-110">The uninstallation process leaves features installed upon which Windows PowerShell Web Access was dependent; you can uninstall those features separately if needed.</span></span>

## <a name="recommended-quick-uninstallation"></a><span data-ttu-id="66a2e-111">Doporučená (rychlá) odinstalace</span><span class="sxs-lookup"><span data-stu-id="66a2e-111">Recommended (quick) uninstallation</span></span>

<span data-ttu-id="66a2e-112">Postupy v této části vám umožní odinstalovat obojí:</span><span class="sxs-lookup"><span data-stu-id="66a2e-112">Procedures in this section help you uninstall both:</span></span>

- <span data-ttu-id="66a2e-113">Webová aplikace Windows PowerShell Web Accessu a</span><span class="sxs-lookup"><span data-stu-id="66a2e-113">the Windows PowerShell Web Access web application, and</span></span>
- <span data-ttu-id="66a2e-114">funkci Windows PowerShell Web Accessu</span><span class="sxs-lookup"><span data-stu-id="66a2e-114">the Windows PowerShell Web Access feature</span></span>

<span data-ttu-id="66a2e-115">pomocí rutin Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="66a2e-115">by using Windows PowerShell cmdlets.</span></span>

### <a name="step-1-delete-the-web-application-using-cmdlets"></a><span data-ttu-id="66a2e-116">Krok 1: Odstranění webové aplikace pomocí rutin</span><span class="sxs-lookup"><span data-stu-id="66a2e-116">Step 1: Delete the web application using cmdlets</span></span>

1. <span data-ttu-id="66a2e-117">Proveďte jednu z následujících akcí otevřete relaci Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="66a2e-117">Do one of the following to open a Windows PowerShell session.</span></span>

    -   <span data-ttu-id="66a2e-118">Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu.</span><span class="sxs-lookup"><span data-stu-id="66a2e-118">On the Windows desktop, right-click **Windows PowerShell** on the taskbar.</span></span>

    -   <span data-ttu-id="66a2e-119">V Windows **Start** obrazovce, klikněte na tlačítko **prostředí Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-119">On the Windows **Start** screen, click **Windows PowerShell**.</span></span>

2. <span data-ttu-id="66a2e-120">Typ `Uninstall-PswaWebApplication`a potom stiskněte klávesu **Enter**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-120">Type `Uninstall-PswaWebApplication`, and then press **Enter**.</span></span>
   1. <span data-ttu-id="66a2e-121">Pokud jste zadali vlastní název webu, přidejte do příkazu parametr `-WebsiteName` a zadejte název tohoto webu.</span><span class="sxs-lookup"><span data-stu-id="66a2e-121">If you have specified your own, custom website name, add the `-WebsiteName` parameter to your command, and specify the website name.</span></span>

        `Uninstall-PswaWebApplication -WebsiteName <web-site-name>`
   1. <span data-ttu-id="66a2e-122">Pokud jste použili vlastní webovou aplikaci (ne výchozí aplikaci, **pswa**, přidejte `-WebApplicationName` parametr k příkazu a zadejte název webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="66a2e-122">If you have used a custom web application (not the default application, **pswa**, add the `-WebApplicationName` parameter to your command, and specify the name of the web application.</span></span>

        `Uninstall-PswaWebApplication -WebApplicationName <web-application-name>`
   1. <span data-ttu-id="66a2e-123">Pokud používáte testovací certifikát, přidejte do rutiny parametr `DeleteTestCertificate` jako v tomto příkladu.</span><span class="sxs-lookup"><span data-stu-id="66a2e-123">If you are using a test certificate, add the `DeleteTestCertificate` parameter to the cmdlet, as shown in the following example.</span></span>

        `Uninstall-PswaWebApplication -DeleteTestCertificate`

### <a name="step-2-uninstall-windows-powershell-web-access-using-cmdlets"></a><span data-ttu-id="66a2e-124">Krok 2: Odinstalace Windows PowerShell Web Accessu pomocí rutin</span><span class="sxs-lookup"><span data-stu-id="66a2e-124">Step 2: Uninstall Windows PowerShell Web Access using cmdlets</span></span>

1. <span data-ttu-id="66a2e-125">Proveďte jednu z následujících akcí otevřete relaci Windows Powershellu se zvýšenými uživatelskými právy.</span><span class="sxs-lookup"><span data-stu-id="66a2e-125">Do one of the following to open a Windows PowerShell session with elevated user rights.</span></span> <span data-ttu-id="66a2e-126">Jestli je relace už otevřená, přejděte na další krok.</span><span class="sxs-lookup"><span data-stu-id="66a2e-126">If a session is already open, go on to the next step.</span></span>

    -   <span data-ttu-id="66a2e-127">Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu a pak klikněte na tlačítko **spustit jako správce**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-127">On the Windows desktop, right-click **Windows PowerShell** on the taskbar, and then click **Run as Administrator**.</span></span>

    -   <span data-ttu-id="66a2e-128">V Windows **Start** obrazovce, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na tlačítko **spustit jako správce**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-128">On the Windows **Start** screen, right-click **Windows PowerShell**, and then click **Run as Administrator**.</span></span>

1. <span data-ttu-id="66a2e-129">Zadejte následující příkaz a stiskněte klávesu **Enter**, kde *název_počítače* je vzdálený server, ze kterého chcete odebrat Windows PowerShell Web Accessu.</span><span class="sxs-lookup"><span data-stu-id="66a2e-129">Type the following, and then press **Enter**, where *computer_name* represents a remote server from which you want to remove Windows PowerShell Web Access.</span></span> <span data-ttu-id="66a2e-130">Parametr `-Restart` automaticky restartuje cílové servery, pokud to odebrání vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="66a2e-130">The `-Restart` parameter automatically restarts destination servers if required by the removal.</span></span>

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -ComputerName <computer_name> -Restart

    <span data-ttu-id="66a2e-131">Pokud chcete odebrat role a funkce z offline virtuálního pevného disku, je nutné přidat parametr `-ComputerName` i parametr `-VHD`.</span><span class="sxs-lookup"><span data-stu-id="66a2e-131">To remove roles and features from an offline VHD, you must add both the `-ComputerName` parameter and the `-VHD` parameter.</span></span> <span data-ttu-id="66a2e-132">Parametr `-ComputerName` obsahuje název serveru, ke kterému chcete připojit virtuální pevný disk. Parametr `-VHD` pak obsahuje cestu k souboru VHD na určeném serveru.</span><span class="sxs-lookup"><span data-stu-id="66a2e-132">The `-ComputerName` parameter contains the name of the server on which to mount the VHD, and the `-VHD` parameter contains the path to the VHD file on the specified server.</span></span>

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -VHD <path> -ComputerName <computer_name> -Restart

1. <span data-ttu-id="66a2e-133">Po dokončení odebrání ověřte, že odeberete tak, že otevřete Windows PowerShell Web Accessu **všechny servery** stránku ve Správci serveru, vyberete server, ze kterého jste tuto funkci odebrali a zobrazení **role a Funkce** dlaždice na stránce vybraného serveru.</span><span class="sxs-lookup"><span data-stu-id="66a2e-133">When removal is finished, verify that you removed Windows PowerShell Web Access by opening the **All Servers** page in Server Manager, selecting a server from which you removed the feature, and viewing the **Roles and Features** tile on the page for the selected server.</span></span>

    <span data-ttu-id="66a2e-134">Můžete taky spustit `Get-WindowsFeature` rutinu určenou pro vybraný server (Get-WindowsFeature - ComputerName &lt; *název_počítače*&gt;) Chcete-li zobrazit seznam rolí a funkcí nainstalovaných na serveru.</span><span class="sxs-lookup"><span data-stu-id="66a2e-134">You can also run the `Get-WindowsFeature` cmdlet targeted at the selected server (Get-WindowsFeature -ComputerName &lt;*computer_name*&gt;) to view a list of roles and features that are installed on the server.</span></span>

## <a name="custom-uninstallation"></a><span data-ttu-id="66a2e-135">Vlastní odinstalace</span><span class="sxs-lookup"><span data-stu-id="66a2e-135">Custom uninstallation</span></span>

<span data-ttu-id="66a2e-136">Postupy v této části vám umožní odinstalovat webovou aplikaci Windows PowerShell Web Accessu a funkci Windows PowerShell Web Accessu pomocí odebrat role a funkce Průvodce ve Správci serveru a konzoly Správce služby IIS.</span><span class="sxs-lookup"><span data-stu-id="66a2e-136">Procedures in this section help you uninstall both the Windows PowerShell Web Access web application and the Windows PowerShell Web Access feature by using the Remove Roles and Features Wizard in Server Manager, and the IIS Manager console.</span></span>

### <a name="step-1-delete-the-web-application-using-iis-manager"></a><span data-ttu-id="66a2e-137">Krok 1: Odstranění webové aplikace pomocí Správce služby IIS</span><span class="sxs-lookup"><span data-stu-id="66a2e-137">Step 1: Delete the web application using IIS Manager</span></span>


1. <span data-ttu-id="66a2e-138">Otevřete konzolu Správce služby IIS některým z následujících postupů.</span><span class="sxs-lookup"><span data-stu-id="66a2e-138">Open the IIS Manager console by doing one of the following.</span></span> <span data-ttu-id="66a2e-139">Jestli je už otevřená, přejděte na další krok.</span><span class="sxs-lookup"><span data-stu-id="66a2e-139">If it is already open, go on to the next step.</span></span>

    -   <span data-ttu-id="66a2e-140">Na ploše Windows spusťte Správce serveru klikněte na **správce serveru** na hlavním panelu Windows.</span><span class="sxs-lookup"><span data-stu-id="66a2e-140">On the Windows desktop, start Server Manager by clicking **Server Manager** in the Windows taskbar.</span></span> <span data-ttu-id="66a2e-141">Na **nástroje** nabídky ve Správci serveru klikněte na tlačítko **Správce Internetové informační služby (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-141">On the **Tools** menu in Server Manager, click **Internet Information Services (IIS) Manager**.</span></span>

    -   <span data-ttu-id="66a2e-142">V Windows **Start** zadejte libovolné části názvu **Správce Internetové informační služby (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-142">On the Windows **Start** screen, type any part of the name **Internet Information Services (IIS) Manager**.</span></span> <span data-ttu-id="66a2e-143">Až se zobrazí, klikněte na zástupce **aplikace** výsledky.</span><span class="sxs-lookup"><span data-stu-id="66a2e-143">Click the shortcut when it is displayed in the **Apps** results.</span></span>

1. <span data-ttu-id="66a2e-144">V podokně stromu Správce služby IIS vyberte web, na kterém běží webová aplikace Windows PowerShell Web Accessu.</span><span class="sxs-lookup"><span data-stu-id="66a2e-144">In the IIS Manager tree pane, select the website that is running the Windows PowerShell Web Access web application.</span></span>

1. <span data-ttu-id="66a2e-145">V **akce** podokně v části **spravovat web**, klikněte na tlačítko **Zastavit**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-145">In the **Actions** pane, under **Manage Website**, click **Stop**.</span></span>

1. <span data-ttu-id="66a2e-146">V podokně stromu klikněte pravým tlačítkem na webovou aplikaci na webu, na kterém běží webová aplikace Windows PowerShell Web Accessu a potom klikněte na tlačítko **odebrat**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-146">In the tree pane, right-click the web application in the website that is running the Windows PowerShell Web Access web application, and then click **Remove**.</span></span>

1. <span data-ttu-id="66a2e-147">V podokně stromu vyberte **fondy aplikací**, vyberte složku fondu aplikací Windows PowerShell Web Accessu, klikněte na tlačítko **Zastavit** v **akce** podokně a pak klikněte na tlačítko  **Odebrat** v podokně obsahu.</span><span class="sxs-lookup"><span data-stu-id="66a2e-147">In the tree pane, select **Application Pools**, select the Windows PowerShell Web Access application pool folder, click **Stop** in the **Actions** pane, and then click **Remove** in the content pane.</span></span>

1. <span data-ttu-id="66a2e-148">Zavřete Správce služby IIS.</span><span class="sxs-lookup"><span data-stu-id="66a2e-148">Close IIS Manager.</span></span>

> <span data-ttu-id="66a2e-149">![Poznámka: upozornění](images/SecurityNote.jpeg)**Poznámka**:</span><span class="sxs-lookup"><span data-stu-id="66a2e-149">![Warning note](images/SecurityNote.jpeg)**Note**:</span></span>
>
> <span data-ttu-id="66a2e-150">Certifikát se během odinstalace neodstraní.</span><span class="sxs-lookup"><span data-stu-id="66a2e-150">The certificate is not deleted during uninstallation.</span></span>
>
> <span data-ttu-id="66a2e-151">Pokud jste vytvořili certifikát podepsaný svým držitelem nebo použili testovací certifikát a chcete ho odebrat, odstraňte certifikát ve Správci služby IIS.</span><span class="sxs-lookup"><span data-stu-id="66a2e-151">If you created a self-signed certificate or used a test certificate and want to remove it, delete the certificate in IIS Manager.</span></span>

### <a name="step-2-uninstall-windows-powershell-web-access-using-the-remove-roles-and-features-wizard"></a><span data-ttu-id="66a2e-152">Krok 2: Odinstalace Windows PowerShell Web Accessu pomocí funkce Průvodce odebráním rolí a</span><span class="sxs-lookup"><span data-stu-id="66a2e-152">Step 2: Uninstall Windows PowerShell Web Access using the Remove Roles and Features Wizard</span></span>

1. <span data-ttu-id="66a2e-153">Pokud správce serveru je už otevřená, přejděte k dalšímu kroku.</span><span class="sxs-lookup"><span data-stu-id="66a2e-153">If Server Manager is already open, go on to the next step.</span></span> <span data-ttu-id="66a2e-154">Správce serveru ještě není otevřený, otevřete ho jedním z následujících akcí.</span><span class="sxs-lookup"><span data-stu-id="66a2e-154">If Server Manager is not already open, open it by doing one of the following.</span></span>

    -   <span data-ttu-id="66a2e-155">Na ploše Windows spusťte Správce serveru klikněte na **správce serveru** na hlavním panelu Windows.</span><span class="sxs-lookup"><span data-stu-id="66a2e-155">On the Windows desktop, start Server Manager by clicking **Server Manager** in the Windows taskbar.</span></span>

    -   <span data-ttu-id="66a2e-156">V Windows **Start** obrazovce, klikněte na tlačítko **správce serveru**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-156">On the Windows **Start** screen, click **Server Manager**.</span></span>

1. <span data-ttu-id="66a2e-157">Na **spravovat** nabídky, klikněte na tlačítko **odebrat role a funkce**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-157">On the **Manage** menu, click **Remove Roles and Features**.</span></span>

1. <span data-ttu-id="66a2e-158">Na **vybrat cílový server** stránky, vyberte server nebo offline virtuální pevný disk, ze kterého chcete odebrat tuto funkci.</span><span class="sxs-lookup"><span data-stu-id="66a2e-158">On the **Select destination server** page, select the server or offline VHD from which you want to remove the feature.</span></span> <span data-ttu-id="66a2e-159">Pokud chcete zvolit offline virtuální pevný disk,  vyberte nejdřív server, ke kterému chcete virtuální pevný disk připojit, a pak vyberte příslušný soubor VHD.</span><span class="sxs-lookup"><span data-stu-id="66a2e-159">To select an offline VHD, first select the server on which to mount the VHD, and then select the VHD file.</span></span> <span data-ttu-id="66a2e-160">Po výběru cílového serveru, klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-160">After you have selected the destination server, click **Next**.</span></span>

1. <span data-ttu-id="66a2e-161">Klikněte na tlačítko **Další** znovu přejděte do **odebrat funkce** stránky.</span><span class="sxs-lookup"><span data-stu-id="66a2e-161">Click **Next** again to skip to the **Remove features** page.</span></span>

1. <span data-ttu-id="66a2e-162">Zrušte zaškrtnutí políčka pro **Windows PowerShell Web Accessu**a potom klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-162">Clear the check box for **Windows PowerShell Web Access**, and then click **Next**.</span></span>

1. <span data-ttu-id="66a2e-163">Na **potvrdit vybrané možnosti odebrání** klikněte na **odebrat**.</span><span class="sxs-lookup"><span data-stu-id="66a2e-163">On the **Confirm removal selections** page, click **Remove**.</span></span>

## <a name="see-also"></a><span data-ttu-id="66a2e-164">Viz také</span><span class="sxs-lookup"><span data-stu-id="66a2e-164">See Also</span></span>

- [<span data-ttu-id="66a2e-165">Nainstalovat a používat Windows PowerShell Web Accessu</span><span class="sxs-lookup"><span data-stu-id="66a2e-165">Install and Use Windows PowerShell Web Access</span></span>](install-and-use-windows-powershell-web-access.md)
- [<span data-ttu-id="66a2e-166">Nápověda k aplikaci IIS 7.0 Manager</span><span class="sxs-lookup"><span data-stu-id="66a2e-166">IIS Manager 7.0 Help</span></span>](https://technet.microsoft.com/library/cc732664.aspx)