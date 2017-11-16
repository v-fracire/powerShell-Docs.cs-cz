---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: e8620cdeb90792e86d091d3e19a169f9dfa690f9
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="known-issues-and-limitations"></a><span data-ttu-id="d4bd8-102">Známé problémy a omezení</span><span class="sxs-lookup"><span data-stu-id="d4bd8-102">Known Issues and Limitations</span></span>

<a name="powershell-shortcuts-are-broken-when-used-for-the-first-time"></a><span data-ttu-id="d4bd8-103">Při prvním použití jsou přerušená zkratky prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4bd8-103">PowerShell Shortcuts are broken when used for the first time</span></span>
------------------------------------------------------------

<span data-ttu-id="d4bd8-104">**Řešení:** proveďte jednu z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="d4bd8-104">**Resolution:** Perform one of the following actions:</span></span>

1.  <span data-ttu-id="d4bd8-105">Klikněte pravým tlačítkem na zástupce prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-105">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="d4bd8-106">Vyberte "Prostředí Windows PowerShell" ke spuštění v režimu bez zvýšených oprávnění.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-106">Select “Windows PowerShell” to launch in a non-elevated mode.</span></span>
2.  <span data-ttu-id="d4bd8-107">Klikněte pravým tlačítkem na zástupce prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-107">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="d4bd8-108">Klikněte pravým tlačítkem na "Prostředí Windows PowerShell" a vyberte možnost "Spustit jako správce" ke spuštění v režimu zvýšené.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-108">Right click on “Windows PowerShell” and select “Run As Administrator” to launch in an elevated mode.</span></span>

<span data-ttu-id="d4bd8-109">Po provedení výše uvedené operace, budou fungovat zástupce prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-109">Once you have performed either of the above actions, the PowerShell shortcuts will work.</span></span> <span data-ttu-id="d4bd8-110">Tyto akce je nutné provést pouze jednou.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-110">These actions need to be performed only once.</span></span>


<a name="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7"></a><span data-ttu-id="d4bd8-111">Moduly prostředí PowerShell a prostředků DSC hlásit chyby zásady spouštění v systému Windows 7</span><span class="sxs-lookup"><span data-stu-id="d4bd8-111">PowerShell Modules and DSC Resources report errors about ExecutionPolicy on Windows 7</span></span>
-------------------------------------------------------------------------------------
<span data-ttu-id="d4bd8-112">Ve Windows 7 může způsobit chyby oznámené o ExecutionPolicy používání modulů Powershellu a prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-112">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

<span data-ttu-id="d4bd8-113">**Řešení:** zásady spouštění nastaveny na RemoteSigned spuštěním následujícího příkazu v relaci prostředí PowerShell zvýšenými oprávněními (Spustit jako správce):</span><span class="sxs-lookup"><span data-stu-id="d4bd8-113">**Resolution:** Set the ExecutionPolicy to RemoteSigned by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

<a name="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash"></a><span data-ttu-id="d4bd8-114">Připojení k původní vzdálený koncový bod Exchange způsobí, že havárie</span><span class="sxs-lookup"><span data-stu-id="d4bd8-114">Connecting to an old remote Exchange endpoint causes a crash</span></span>
------------------------------------------------------------

<span data-ttu-id="d4bd8-115">Původní koncový bod Exchange přesměruje na nový koncový bod.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-115">The old Exchange endpoint redirects to a new endpoint.</span></span> <span data-ttu-id="d4bd8-116">Je chyby logice přesměrování této výsledky v havárie.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-116">There is a bug in the redirection logic that results in a crash.</span></span>

<span data-ttu-id="d4bd8-117">**Řešení:** připojit se přímo k nový koncový bod.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-117">**Resolution:** Connect directly to the new endpoint.</span></span>


<a name="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2"></a><span data-ttu-id="d4bd8-118">Funkce protokolování inventáře softwaru je chybně zastavena po instalaci WMF 5.0 na Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d4bd8-118">Software Inventory Logging feature is erroneously stopped after WMF 5.0 installation on Windows Server 2012 R2</span></span>
-------------------------------------------------------------------------------------------------------------

<span data-ttu-id="d4bd8-119">Při instalaci WMF 5.0 na Windows Server 2012 R2 a je již spuštěna SIL, funkce protokolování inventáře softwaru je chybně zastavena po instalaci.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-119">When installing WMF 5.0 on a Windows Server 2012 R2 that is already running SIL, the Software Inventory Logging feature is erroneously stopped after installation.</span></span>

<span data-ttu-id="d4bd8-120">**Řešení:** spusťte rutinu Start-SilLogging po instalaci WMF, protože proces instalace se zastaví errantly funkce protokolování inventáře softwaru.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-120">**Resolution:** Run the Start-SilLogging cmdlet once after the WMF installation, as the installation process will errantly stop the Software Inventory Logging feature.</span></span>

<a name="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together"></a><span data-ttu-id="d4bd8-121">Get-ChildItem nefunguje, pokud se společně používají - LiteralPath a - Recurse</span><span class="sxs-lookup"><span data-stu-id="d4bd8-121">Get-ChildItem does not work if -LiteralPath and -Recurse are used together</span></span>
--------------------------------------------------------------------------

<span data-ttu-id="d4bd8-122">Pokud název adresáře obsahuje neplatný zástupný znak, pak Get-ChildItem nebude vytváří očekávané výsledky v případě - LiteralPath i - Recurse používají společně.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-122">If a directory name contains an invalid wildcard character, then Get-ChildItem will not produce expected results when both -LiteralPath and -Recurse are used together.</span></span>

<span data-ttu-id="d4bd8-123">**Řešení:** není ideální, ale aktuální řešení je k implementaci rekurze ve skriptu, místo spoléhají na rutinu.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-123">**Resolution:** Not ideal, but current workaround is to implement recursion in the script rather than rely on the cmdlet.</span></span>


<a name="sysprep-fails-after-wmf-50-installation"></a><span data-ttu-id="d4bd8-124">Nástroj Sysprep selže po instalaci WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="d4bd8-124">Sysprep fails after WMF 5.0 installation</span></span>
----------------------------------------

<span data-ttu-id="d4bd8-125">Existují dvě řešení tohoto problému v závislosti na verzi Windows serveru, kterou používáte.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-125">There are two workarounds for this issue depending on the version of Windows Server you are running.</span></span>

<span data-ttu-id="d4bd8-126">**Řešení:**</span><span class="sxs-lookup"><span data-stu-id="d4bd8-126">**Resolution:**</span></span>
- <span data-ttu-id="d4bd8-127">Pro systémy s operačním systémem **Windows Server 2008 R2**</span><span class="sxs-lookup"><span data-stu-id="d4bd8-127">For systems running **Windows Server 2008 R2**</span></span>
  1. <span data-ttu-id="d4bd8-128">Otevřete Powershell jako správce</span><span class="sxs-lookup"><span data-stu-id="d4bd8-128">Open Powershell as an administrator</span></span>
  2. <span data-ttu-id="d4bd8-129">Spusťte následující příkaz</span><span class="sxs-lookup"><span data-stu-id="d4bd8-129">Run the following command</span></span> 
  
  ```powershell
    Set-SilLogging –TargetUri https://BlankTarget –CertificateThumbprint 0123456789
  ```
  3. <span data-ttu-id="d4bd8-130">Spusťte příkaz a ignorovat chybu, že jsou správně.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-130">Run the command and ignore the error, as they are expected.</span></span>
  
  ```powershell
    Publish-SilData
   ```
  4. <span data-ttu-id="d4bd8-131">Odstranit soubory v adresáři \Windows\System32\Logfiles\SIL\\</span><span class="sxs-lookup"><span data-stu-id="d4bd8-131">Delete the files in  \Windows\System32\Logfiles\SIL\ directory</span></span>
  
  ```powershell
    Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
  ```
  5. <span data-ttu-id="d4bd8-132">Nainstalujte všechny dostupné důležité aktualizace systému Windows a začít Sysyprep operace normálně.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-132">Install all available important Windows Updates, and begin Sysyprep operation normally.</span></span>
  
- <span data-ttu-id="d4bd8-133">Pro systémy s operačním systémem **systému Windows Server 2012**</span><span class="sxs-lookup"><span data-stu-id="d4bd8-133">For systems running **Windows Server 2012**</span></span>
  1.    <span data-ttu-id="d4bd8-134">Nástroj Sysprep'd, přihlaste se jako správce položek po instalaci WMF 5.0 na serveru, aby se.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-134">After installing WMF 5.0 on the server to be Sysprep’d, login as administrator.</span></span>
  2.    <span data-ttu-id="d4bd8-135">Zkopírujte Generize.xml z adresáře \Windows\System32\Sysprep\ActionFiles\ do umístění mimo adresář systému Windows, C:\ třeba.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-135">Copy Generize.xml from directory \Windows\System32\Sysprep\ActionFiles\ to a location outside of the Windows directory, C:\ for example.</span></span>
  3.    <span data-ttu-id="d4bd8-136">Otevřete vaší kopie Generalize.xml programu Poznámkový blok.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-136">Open your Generalize.xml copy with notepad.</span></span>
  4.    <span data-ttu-id="d4bd8-137">Vyhledat a odstranit následující text, jednu instanci každého musí být odstraněn (nebudou se blíží konec dokumentu).</span><span class="sxs-lookup"><span data-stu-id="d4bd8-137">Find and remove the following text, one instance of each needs to be deleted (they will be near the end of the document).</span></span>

    ```
    <sysprepOrder order="0x3200"></sysprepOrder>
    <sysprepOrder order="0x3300"></sysprepOrder>
    ```

  5.    <span data-ttu-id="d4bd8-138">Uložit upravenou kopii Generalize.xml a zavřete soubor.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-138">Save the edited copy of Generalize.xml and close the file.</span></span>
  6.    <span data-ttu-id="d4bd8-139">Otevřete příkazový řádek jako správce</span><span class="sxs-lookup"><span data-stu-id="d4bd8-139">Open a command prompt as administrator</span></span>
  7.    <span data-ttu-id="d4bd8-140">Spusťte následující příkaz k převzetí vlastnictví souboru Generalize.xml ve složce system32:</span><span class="sxs-lookup"><span data-stu-id="d4bd8-140">Run the following command to take ownership of the Generalize.xml file in system32 folder:</span></span>

    ```
    Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml 
    ```

  8.    <span data-ttu-id="d4bd8-141">Spusťte následující příkaz pro nastavení příslušných oprávnění u souboru:</span><span class="sxs-lookup"><span data-stu-id="d4bd8-141">Run the following command to set appropriate permission on the file:</span></span>

    ```
    Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F 
    ```
      * <span data-ttu-id="d4bd8-142">Odpovíte kladně příkazového řádku pro potvrzení.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-142">Answer Yes at the prompt for confirmation.</span></span> 
      * <span data-ttu-id="d4bd8-143">Všimněte si, že `<AdministratorUserName>` by měla být nahrazená jiným uživatelským jménem, který je správce na počítači.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-143">Note that `<AdministratorUserName>` should be replaced by the username who is administrator on the machine.</span></span> <span data-ttu-id="d4bd8-144">Například "Administrator".</span><span class="sxs-lookup"><span data-stu-id="d4bd8-144">For example, "Administrator".</span></span>
      
  9.    <span data-ttu-id="d4bd8-145">Zkopírujte soubor můžete upravit a uložit přes k adresáři Sysprep pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="d4bd8-145">Copy the file you edited and saved over to the Sysprep directory using the following command:</span></span>

    ```
    xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml 
    ```
      * <span data-ttu-id="d4bd8-146">Odpovíte kladně přepsat (Všimněte si, že pokud je výzva k přepsání, Překontrolujte zadaná cesta).</span><span class="sxs-lookup"><span data-stu-id="d4bd8-146">Answer Yes to overwrite (note that if there is no prompt to overwrite, double check the path entered).</span></span>
      * <span data-ttu-id="d4bd8-147">Předpokládá, že vaše upravenou kopii Generalize.xml byla zkopírována do C:\.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-147">Assumes your edited copy of Generalize.xml was copied to C:\ .</span></span>

  10.   <span data-ttu-id="d4bd8-148">Generalize.XML byla aktualizována s alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-148">Generalize.xml is now updated with the workaround.</span></span> <span data-ttu-id="d4bd8-149">Spusťte nástroj Sysprep s povolenou možností generalizace.</span><span class="sxs-lookup"><span data-stu-id="d4bd8-149">Please run Sysprep with the generalize option enabled.</span></span>

