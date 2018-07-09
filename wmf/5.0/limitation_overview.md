---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 4eb2f0bac4f2169a9a06d80cb4fa214a09cdfa86
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892980"
---
# <a name="known-issues-and-limitations"></a><span data-ttu-id="9bee4-102">Známé problémy a omezení</span><span class="sxs-lookup"><span data-stu-id="9bee4-102">Known Issues and Limitations</span></span>

## <a name="powershell-shortcuts-are-broken-when-used-for-the-first-time"></a><span data-ttu-id="9bee4-103">Při prvním použití jsou přerušená klávesové zkratky prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bee4-103">PowerShell Shortcuts are broken when used for the first time</span></span>

<span data-ttu-id="9bee4-104">**Řešení:** proveďte jeden z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="9bee4-104">**Resolution:** Perform one of the following actions:</span></span>

1. <span data-ttu-id="9bee4-105">Klikněte pravým tlačítkem na zástupce Powershellu.</span><span class="sxs-lookup"><span data-stu-id="9bee4-105">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="9bee4-106">Vyberte "Windows PowerShell" ke spuštění v režimu bez zvýšených oprávnění.</span><span class="sxs-lookup"><span data-stu-id="9bee4-106">Select “Windows PowerShell” to launch in a non-elevated mode.</span></span>
2. <span data-ttu-id="9bee4-107">Klikněte pravým tlačítkem na zástupce Powershellu.</span><span class="sxs-lookup"><span data-stu-id="9bee4-107">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="9bee4-108">Klikněte pravým tlačítkem myši klikněte na "Windows PowerShell" a vyberte spustit jako správce."ke spuštění v režimu se zvýšenými oprávněními.</span><span class="sxs-lookup"><span data-stu-id="9bee4-108">Right click on “Windows PowerShell” and select “Run As Administrator” to launch in an elevated mode.</span></span>

<span data-ttu-id="9bee4-109">Jakmile jste provedli jednu z výše uvedených akcí, bude fungovat klávesové zkratky prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bee4-109">Once you have performed either of the above actions, the PowerShell shortcuts will work.</span></span> <span data-ttu-id="9bee4-110">Tato akce je nutné provést pouze jednou.</span><span class="sxs-lookup"><span data-stu-id="9bee4-110">These actions need to be performed only once.</span></span>

## <a name="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7"></a><span data-ttu-id="9bee4-111">Moduly Powershellu a prostředky DSC sestavy chyb o ExecutionPolicy ve Windows 7</span><span class="sxs-lookup"><span data-stu-id="9bee4-111">PowerShell Modules and DSC Resources report errors about ExecutionPolicy on Windows 7</span></span>

<span data-ttu-id="9bee4-112">Ve Windows 7 používání modulů Powershellu a prostředky DSC může vést k chybám o ExecutionPolicy.</span><span class="sxs-lookup"><span data-stu-id="9bee4-112">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

<span data-ttu-id="9bee4-113">**Řešení:** nastaveno ExecutionPolicy RemoteSigned spuštěním následujícího příkazu v relaci Powershellu se zvýšenými oprávněními (Spustit jako správce):</span><span class="sxs-lookup"><span data-stu-id="9bee4-113">**Resolution:** Set the ExecutionPolicy to RemoteSigned by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

## <a name="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash"></a><span data-ttu-id="9bee4-114">Připojení k staré vzdálený koncový bod serveru Exchange způsobí selhání</span><span class="sxs-lookup"><span data-stu-id="9bee4-114">Connecting to an old remote Exchange endpoint causes a crash</span></span>

<span data-ttu-id="9bee4-115">Staré koncový bod výměny přesměruje do nového koncového bodu.</span><span class="sxs-lookup"><span data-stu-id="9bee4-115">The old Exchange endpoint redirects to a new endpoint.</span></span> <span data-ttu-id="9bee4-116">Je chyby logiky přesměrování této výsledky v chybovému ukončení.</span><span class="sxs-lookup"><span data-stu-id="9bee4-116">There is a bug in the redirection logic that results in a crash.</span></span>

<span data-ttu-id="9bee4-117">**Řešení:** připojit přímo do nového koncového bodu.</span><span class="sxs-lookup"><span data-stu-id="9bee4-117">**Resolution:** Connect directly to the new endpoint.</span></span>

## <a name="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2"></a><span data-ttu-id="9bee4-118">Funkce protokolování inventáře softwaru je chybně zastavena po instalaci WMF 5.0 v systému Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="9bee4-118">Software Inventory Logging feature is erroneously stopped after WMF 5.0 installation on Windows Server 2012 R2</span></span>

<span data-ttu-id="9bee4-119">Při instalaci WMF 5.0 na Windows Server 2012 R2, která je již spuštěna SIL, funkce protokolování inventáře softwaru je chybně zastavena po instalaci.</span><span class="sxs-lookup"><span data-stu-id="9bee4-119">When installing WMF 5.0 on a Windows Server 2012 R2 that is already running SIL, the Software Inventory Logging feature is erroneously stopped after installation.</span></span>

<span data-ttu-id="9bee4-120">**Řešení:** spusťte rutinu Start-SilLogging jednou po instalaci WMF, protože proces instalace se zastaví chybně funkce protokolování inventáře softwaru.</span><span class="sxs-lookup"><span data-stu-id="9bee4-120">**Resolution:** Run the Start-SilLogging cmdlet once after the WMF installation, as the installation process will errantly stop the Software Inventory Logging feature.</span></span>

## <a name="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together"></a><span data-ttu-id="9bee4-121">`Get-ChildItem` Pokud se společně používají - LiteralPath a - Recurse nefunguje</span><span class="sxs-lookup"><span data-stu-id="9bee4-121">`Get-ChildItem` does not work if -LiteralPath and -Recurse are used together</span></span>

<span data-ttu-id="9bee4-122">Pokud název adresáře obsahuje neplatný zástupný znak, pak `Get-ChildItem` nevytvoří očekávané výsledky, když - LiteralPath i - Recurse se používají společně.</span><span class="sxs-lookup"><span data-stu-id="9bee4-122">If a directory name contains an invalid wildcard character, then `Get-ChildItem` will not produce expected results when both -LiteralPath and -Recurse are used together.</span></span>

<span data-ttu-id="9bee4-123">**Řešení:** není ideální, ale aktuální alternativním řešením je implementace rekurze ve skriptu, spíše než využívají rutiny.</span><span class="sxs-lookup"><span data-stu-id="9bee4-123">**Resolution:** Not ideal, but current workaround is to implement recursion in the script rather than rely on the cmdlet.</span></span>

## <a name="sysprep-fails-after-wmf-50-installation"></a><span data-ttu-id="9bee4-124">Nástroj Sysprep selže po instalaci WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="9bee4-124">Sysprep fails after WMF 5.0 installation</span></span>

<span data-ttu-id="9bee4-125">Existují dvě alternativní řešení tohoto problému v závislosti na verzi Windows serveru.</span><span class="sxs-lookup"><span data-stu-id="9bee4-125">There are two workarounds for this issue depending on the version of Windows Server you are running.</span></span>

<span data-ttu-id="9bee4-126">**Řešení:**</span><span class="sxs-lookup"><span data-stu-id="9bee4-126">**Resolution:**</span></span>

- <span data-ttu-id="9bee4-127">Pro systémy s operačním systémem **systému Windows Server 2008 R2**</span><span class="sxs-lookup"><span data-stu-id="9bee4-127">For systems running **Windows Server 2008 R2**</span></span>
  1. <span data-ttu-id="9bee4-128">Otevřete Powershell jako správce</span><span class="sxs-lookup"><span data-stu-id="9bee4-128">Open Powershell as an administrator</span></span>
  2. <span data-ttu-id="9bee4-129">Spuštěním následujícího příkazu</span><span class="sxs-lookup"><span data-stu-id="9bee4-129">Run the following command</span></span>

     ```powershell
     Set-SilLogging –TargetUri https://BlankTarget –CertificateThumbprint 0123456789
     ```

  3. <span data-ttu-id="9bee4-130">Spusťte příkaz a ignorovat chybu, protože se očekává.</span><span class="sxs-lookup"><span data-stu-id="9bee4-130">Run the command and ignore the error, as they are expected.</span></span>

     ```powershell
     Publish-SilData
     ```

  4. <span data-ttu-id="9bee4-131">Odstranit soubory v adresáři \Windows\System32\Logfiles\SIL\\</span><span class="sxs-lookup"><span data-stu-id="9bee4-131">Delete the files in  \Windows\System32\Logfiles\SIL\ directory</span></span>

     ```powershell
     Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
     ```

  5. <span data-ttu-id="9bee4-132">Nainstalujte všechny dostupné důležité aktualizace Windows a zahájí operaci Sysyprep normálně.</span><span class="sxs-lookup"><span data-stu-id="9bee4-132">Install all available important Windows Updates, and begin Sysyprep operation normally.</span></span>

- <span data-ttu-id="9bee4-133">Pro systémy s operačním systémem **systému Windows Server 2012**</span><span class="sxs-lookup"><span data-stu-id="9bee4-133">For systems running **Windows Server 2012**</span></span>
  1. <span data-ttu-id="9bee4-134">Nástroj Sysprep'd, přihlaste se jako správce položek po instalaci WMF 5.0 na serveru.</span><span class="sxs-lookup"><span data-stu-id="9bee4-134">After installing WMF 5.0 on the server to be Sysprep’d, login as administrator.</span></span>
  2. <span data-ttu-id="9bee4-135">Zkopírujte Generize.xml z adresáře \Windows\System32\Sysprep\ActionFiles\ do umístění mimo adresář Windows, C:\ třeba.</span><span class="sxs-lookup"><span data-stu-id="9bee4-135">Copy Generize.xml from directory \Windows\System32\Sysprep\ActionFiles\ to a location outside of the Windows directory, C:\ for example.</span></span>
  3. <span data-ttu-id="9bee4-136">Otevřete kopii Generalize.xml programu Poznámkový blok.</span><span class="sxs-lookup"><span data-stu-id="9bee4-136">Open your Generalize.xml copy with notepad.</span></span>
  4. <span data-ttu-id="9bee4-137">Vyhledat a odstranit následující text, jedna instance každé musí odstranit, (, bude u konce dokumentu).</span><span class="sxs-lookup"><span data-stu-id="9bee4-137">Find and remove the following text, one instance of each needs to be deleted (they will be near the end of the document).</span></span>

     ```xml
     <sysprepOrder order="0x3200"></sysprepOrder>
     <sysprepOrder order="0x3300"></sysprepOrder>
     ```

  5. <span data-ttu-id="9bee4-138">Uložit upravenou kopii Generalize.xml a zavřete soubor.</span><span class="sxs-lookup"><span data-stu-id="9bee4-138">Save the edited copy of Generalize.xml and close the file.</span></span>
  6. <span data-ttu-id="9bee4-139">Otevřete příkazový řádek jako správce</span><span class="sxs-lookup"><span data-stu-id="9bee4-139">Open a command prompt as administrator</span></span>
  7. <span data-ttu-id="9bee4-140">Spusťte následující příkaz, který převzít vlastnictví Generalize.xml souboru ve složce system32:</span><span class="sxs-lookup"><span data-stu-id="9bee4-140">Run the following command to take ownership of the Generalize.xml file in system32 folder:</span></span>

     ```powershell
     Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

  8. <span data-ttu-id="9bee4-141">Spuštěním následujícího příkazu nastavte příslušná oprávnění v souboru:</span><span class="sxs-lookup"><span data-stu-id="9bee4-141">Run the following command to set appropriate permission on the file:</span></span>

     ```powershell
     Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F
     ```

     - <span data-ttu-id="9bee4-142">Odpovězte Ano do příkazového řádku pro potvrzení.</span><span class="sxs-lookup"><span data-stu-id="9bee4-142">Answer Yes at the prompt for confirmation.</span></span>
     - <span data-ttu-id="9bee4-143">Všimněte si, že `<AdministratorUserName>` by měl být nahrazen uživatelským jménem, který je správcem na počítači.</span><span class="sxs-lookup"><span data-stu-id="9bee4-143">Note that `<AdministratorUserName>` should be replaced by the username who is administrator on the machine.</span></span> <span data-ttu-id="9bee4-144">Například "Administrator".</span><span class="sxs-lookup"><span data-stu-id="9bee4-144">For example, "Administrator".</span></span>

  9. <span data-ttu-id="9bee4-145">Zkopírujte soubor upravit a uložit přes do adresáře nástroje Sysprep pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="9bee4-145">Copy the file you edited and saved over to the Sysprep directory using the following command:</span></span>

     ```powershell
     xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

     - <span data-ttu-id="9bee4-146">Odpovězte Ano. Pokud chcete přepsat (Všimněte si, že pokud se nezobrazí žádný dotaz přepsat, pečlivě zkontrolujte zadaná cesta).</span><span class="sxs-lookup"><span data-stu-id="9bee4-146">Answer Yes to overwrite (note that if there is no prompt to overwrite, double check the path entered).</span></span>
     - <span data-ttu-id="9bee4-147">Předpokládá, že vaše upravenou kopii Generalize.xml byl zkopírován do C:\.</span><span class="sxs-lookup"><span data-stu-id="9bee4-147">Assumes your edited copy of Generalize.xml was copied to C:\ .</span></span>

  10. <span data-ttu-id="9bee4-148">Generalize.XML je teď aktualizovaný o alternativní řešení.</span><span class="sxs-lookup"><span data-stu-id="9bee4-148">Generalize.xml is now updated with the workaround.</span></span> <span data-ttu-id="9bee4-149">Spusťte nástroj Sysprep s povolenou možností generalizace.</span><span class="sxs-lookup"><span data-stu-id="9bee4-149">Please run Sysprep with the generalize option enabled.</span></span>