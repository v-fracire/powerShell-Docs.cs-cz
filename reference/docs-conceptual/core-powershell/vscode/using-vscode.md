# <a name="using-visual-studio-code-for-powershell-development"></a><span data-ttu-id="9ccd6-101">Pomocí kódu v sadě Visual Studio pro vývoj prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ccd6-101">Using Visual Studio Code for PowerShell Development</span></span>

<span data-ttu-id="9ccd6-102">Kromě [prostředí PowerShell ISE][ise], prostředí PowerShell je také dobře podporované v kódu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-102">In addition to the [PowerShell ISE][ise], PowerShell is also well-supported in Visual Studio Code.</span></span>
<span data-ttu-id="9ccd6-103">Kromě toho se ISE nepodporuje základní prostředí PowerShell, když Visual Studio Code je podporována pro základní prostředí PowerShell na všech platformách (Windows, systému macOS a Linux)</span><span class="sxs-lookup"><span data-stu-id="9ccd6-103">Furthermore, the ISE is not supported with PowerShell Core, while Visual Studio Code is supported for PowerShell Core on all platforms (Windows, macOS, and Linux)</span></span>

<span data-ttu-id="9ccd6-104">Visual Studio Code můžete použít v systému Windows v prostředí PowerShell verze 5 s použitím Windows 10 nebo instalací [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) pro nižší úrovně operačních systémů Windows (např. Windows 8.1, atd.).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-104">You can use Visual Studio Code on Windows with PowerShell version 5 by using Windows 10 or by installing [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) for down-level Windows OSs (e.g. Windows 8.1, etc.).</span></span>

<span data-ttu-id="9ccd6-105">Před zahájením ho, Zkontrolujte prosím, že prostředí PowerShell v systému existuje.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-105">Before starting it, please make sure PowerShell exists on your system.</span></span>
<span data-ttu-id="9ccd6-106">Pro moderní úlohy u systému Windows, systému macOS a Linux, přečtěte si část:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-106">For modern workloads on Windows, macOS, and Linux, see:</span></span>

- <span data-ttu-id="9ccd6-107">[Instalace jádra prostředí PowerShell v systému macOS a Linux][install-pscore-linux]</span><span class="sxs-lookup"><span data-stu-id="9ccd6-107">[Installing PowerShell Core on macOS and Linux][install-pscore-linux]</span></span>
- <span data-ttu-id="9ccd6-108">[Instalace jádra prostředí PowerShell v systému Windows][install-pscore-windows]</span><span class="sxs-lookup"><span data-stu-id="9ccd6-108">[Installing PowerShell Core on Windows][install-pscore-windows]</span></span>

<span data-ttu-id="9ccd6-109">Pro tradiční úlohy prostředí Windows PowerShell, najdete v části [instalace prostředí Windows PowerShell][install-winps].</span><span class="sxs-lookup"><span data-stu-id="9ccd6-109">For traditional Windows PowerShell workloads, see [Installing Windows PowerShell][install-winps].</span></span>

## <a name="editing-with-visual-studio-code"></a><span data-ttu-id="9ccd6-110">Úpravy s Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9ccd6-110">Editing with Visual Studio Code</span></span>

### <a name="1-installing-visual-studio-codehttpscodevisualstudiocomdocssetupsetup-overview"></a>[<span data-ttu-id="9ccd6-111">1. Instalace Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9ccd6-111">1. Installing Visual Studio Code</span></span>](https://code.visualstudio.com/Docs/setup/setup-overview)

- <span data-ttu-id="9ccd6-112">**Linux**: postupujte podle pokynů k instalaci na [systémem VS Code v systému Linux](https://code.visualstudio.com/docs/setup/linux) stránky</span><span class="sxs-lookup"><span data-stu-id="9ccd6-112">**Linux**: follow the installation instructions on the [Running VS Code on Linux](https://code.visualstudio.com/docs/setup/linux) page</span></span>

- <span data-ttu-id="9ccd6-113">**systému macOS**: postupujte podle pokynů k instalaci na [systémem VS Code v systému macOS](https://code.visualstudio.com/docs/setup/mac) stránky</span><span class="sxs-lookup"><span data-stu-id="9ccd6-113">**macOS**: follow the installation instructions on the [Running VS Code on macOS](https://code.visualstudio.com/docs/setup/mac) page</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ccd6-114">V systému macOS je třeba nainstalovat OpenSSL pro rozšíření prostředí PowerShell fungovala správně.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-114">On macOS, you must install OpenSSL for the PowerShell extension to work correctly.</span></span>
> <span data-ttu-id="9ccd6-115">Nejjednodušší způsob, jak se má nainstalovat [Homebrew](http://brew.sh/) a spusťte `brew install openssl`.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-115">The easiest way to accomplish this is to install [Homebrew](http://brew.sh/) and then run `brew install openssl`.</span></span>
> <span data-ttu-id="9ccd6-116">Nyní bude moct úspěšně načíst rozšíření prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-116">The PowerShell extension will now be able to load successfully.</span></span>

- <span data-ttu-id="9ccd6-117">**Windows**: postupujte podle pokynů k instalaci na [systémem VS Code v systému Windows](https://code.visualstudio.com/docs/setup/windows) stránky</span><span class="sxs-lookup"><span data-stu-id="9ccd6-117">**Windows**: follow the installation instructions on the [Running VS Code on Windows](https://code.visualstudio.com/docs/setup/windows) page</span></span>

### <a name="2-installing-powershell-extension"></a><span data-ttu-id="9ccd6-118">2. Instaluje se rozšíření prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ccd6-118">2. Installing PowerShell Extension</span></span>

- <span data-ttu-id="9ccd6-119">Spuštění sady Visual Studio Code aplikace pomocí:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-119">Launch the Visual Studio Code app by:</span></span>
    - <span data-ttu-id="9ccd6-120">**Windows**: zadáním `code` v relaci prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ccd6-120">**Windows**: typing `code` in your PowerShell session</span></span>
    - <span data-ttu-id="9ccd6-121">**Linux**: zadáním `code` v terminálu</span><span class="sxs-lookup"><span data-stu-id="9ccd6-121">**Linux**: typing `code` in your terminal</span></span>
    - <span data-ttu-id="9ccd6-122">**systému macOS**: zadáním `code` v terminálu</span><span class="sxs-lookup"><span data-stu-id="9ccd6-122">**macOS**: typing `code` in your terminal</span></span>

- <span data-ttu-id="9ccd6-123">Spusťte **rychlé otevřete** stisknutím **Ctrl + P** (**Cmd + P** na Mac).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-123">Launch **Quick Open** by pressing **Ctrl+P** (**Cmd+P** on Mac).</span></span>
- <span data-ttu-id="9ccd6-124">V rychlé otevřený, zadejte `ext install powershell` a počtu **Enter**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-124">In Quick Open, type `ext install powershell` and hit **Enter**.</span></span>
- <span data-ttu-id="9ccd6-125">**Rozšíření** na straně panelu se otevře zobrazení.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-125">The **Extensions** view will open on the Side Bar.</span></span> <span data-ttu-id="9ccd6-126">Vyberte požadované rozšíření prostředí PowerShell od společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-126">Select the PowerShell extension from Microsoft.</span></span>
  <span data-ttu-id="9ccd6-127">Zobrazí se něco jako níže:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-127">You will see something like below:</span></span>

  ![VSCode](../../images/vscode.png)

- <span data-ttu-id="9ccd6-129">Klikněte **nainstalovat** tlačítko pro rozšíření prostředí PowerShell od společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-129">Click the **Install** button on the PowerShell extension from Microsoft.</span></span>
- <span data-ttu-id="9ccd6-130">Po instalaci, zobrazí se **nainstalovat** tlačítko se změní **opětovného načtení**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-130">After the install, you will see the **Install** button turns to **Reload**.</span></span>
  <span data-ttu-id="9ccd6-131">Klikněte na **opětovného načtení**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-131">Click on **Reload**.</span></span>
- <span data-ttu-id="9ccd6-132">Po Visual Studio Code má načíst znovu, jste připraveni pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-132">After Visual Studio Code has reload, you are ready for editing.</span></span>

<span data-ttu-id="9ccd6-133">Například pokud chcete vytvořit nový soubor, klikněte na možnost **souboru -> Nový**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-133">For example, to create a new file, click **File->New**.</span></span>
<span data-ttu-id="9ccd6-134">Chcete-li uložit, klikněte na tlačítko **souboru -> Uložit** a pak zadejte název souboru, můžeme vyslovte `HelloWorld.ps1`.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-134">To save it, click **File->Save** and then provide a file name, let's say `HelloWorld.ps1`.</span></span>
<span data-ttu-id="9ccd6-135">Zavřete soubor, klikněte na "x" vedle názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-135">To close the file, click on "x" next to the file name.</span></span>
<span data-ttu-id="9ccd6-136">Chcete-li ukončit Visual Studio Code **souboru -> ukončení**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-136">To exit Visual Studio Code, **File->Exit**.</span></span>

#### <a name="using-a-specific-installed-version-of-powershell"></a><span data-ttu-id="9ccd6-137">Pomocí konkrétní nainstalovaná verze prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ccd6-137">Using a specific installed version of PowerShell</span></span>

<span data-ttu-id="9ccd6-138">Pokud chcete použít konkrétní instalaci prostředí PowerShell s kódem jazyka Visual Studio, musíte přidat nové proměnné do souboru nastavení uživatele.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-138">If you wish to use a specific installation of PowerShell with Visual Studio Code, you will need to add a new variable to your user settings file.</span></span>

1. <span data-ttu-id="9ccd6-139">Klikněte na tlačítko **souboru -> Předvolby -> Nastavení**</span><span class="sxs-lookup"><span data-stu-id="9ccd6-139">Click **File -> Preferences -> Settings**</span></span>
1. <span data-ttu-id="9ccd6-140">Zobrazí se dvě podokna editor.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-140">Two editor panes will appear.</span></span>
   <span data-ttu-id="9ccd6-141">V podokně nejvíce vpravo (`settings.json`), vložte následující nastavení vhodné pro váš operační systém někde mezi dvěma složené závorky (`{` a `}`) a nahraďte *<version>* s nainstalovaným klientem Verze prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-141">In the right-most pane (`settings.json`), insert the setting below appropriate for your OS somewhere between the two curly brackets (`{` and `}`) and replace *<version>* with the installed PowerShell version:</span></span>

  ```json
    // On Windows:
    "powershell.powerShellExePath": "c:/Program Files/PowerShell/<version>/pwsh.exe"

    // On Linux:
    "powershell.powerShellExePath": "/opt/microsoft/powershell/<version>/pwsh"

    // On macOS:
    "powershell.powerShellExePath": "/usr/local/microsoft/powershell/<version>/pwsh"
  ```
1. <span data-ttu-id="9ccd6-142">Nastavení nahraďte cesta k požadované spustitelný soubor prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ccd6-142">Replace the setting with the path to the desired PowerShell executable</span></span>
1. <span data-ttu-id="9ccd6-143">Uložte soubor s nastaveními a restartujte Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9ccd6-143">Save the settings file and restart Visual Studio Code</span></span>

#### <a name="configuration-settings-for-visual-studio-code"></a><span data-ttu-id="9ccd6-144">Nastavení konfigurace pro Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9ccd6-144">Configuration settings for Visual Studio Code</span></span>

<span data-ttu-id="9ccd6-145">Pomocí kroků v předchozím odstavci můžete přidat nastavení konfigurace v `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-145">By using the steps in the previous paragraph you can add configuration settings in `settings.json`.</span></span>

<span data-ttu-id="9ccd6-146">Doporučujeme následující nastavení konfigurace pro Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-146">We recommend the following configuration settings for Visual Studio Code:</span></span>

```json
{
    "csharp.suppressDotnetRestoreNotification": true,
    "editor.renderWhitespace": "all",
    "editor.renderControlCharacters": true,
    "omnisharp.projectLoadTimeout": 120,
    "files.trimTrailingWhitespace": true
}
```

## <a name="debugging-with-visual-studio-code"></a><span data-ttu-id="9ccd6-147">Ladění pomocí kódu v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9ccd6-147">Debugging with Visual Studio Code</span></span>

### <a name="no-workspace-debugging"></a><span data-ttu-id="9ccd6-148">Prostoru bez ladění</span><span class="sxs-lookup"><span data-stu-id="9ccd6-148">No-workspace debugging</span></span>

<span data-ttu-id="9ccd6-149">Od verze Visual Studio Code 1.9 můžete ladit skripty prostředí PowerShell, bez nutnosti otevřít složku, která obsahuje skript prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-149">As of Visual Studio Code version 1.9 you can debug PowerShell scripts without having to open the folder containing the PowerShell script.</span></span>
<span data-ttu-id="9ccd6-150">Stačí otevřít soubor skriptu prostředí PowerShell s **souboru -> Otevřít soubor...** , zarážku na řádek (stiskněte F9) a poté stisknutím klávesy F5 spusťte ladění.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-150">Simply open the PowerShell script file with **File->Open File...**, set a breakpoint on a line (press F9) and then press F5 to start debugging.</span></span>
<span data-ttu-id="9ccd6-151">Zobrazí se v podokně Akce ladění zobrazují, které umožňuje rozdělit ladicí program, krok, opětovné spuštění a zastavení ladění.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-151">You will see the Debug actions pane appear which allows you to break into the debugger, step, resume and stop debugging.</span></span>

### <a name="workspace-debugging"></a><span data-ttu-id="9ccd6-152">Pracovní prostor ladění</span><span class="sxs-lookup"><span data-stu-id="9ccd6-152">Workspace debugging</span></span>

<span data-ttu-id="9ccd6-153">Pracovní prostor ladění odkazuje na ladění v kontextu složce, kterou jste otevřeli pomocí Visual Studio Code **otevřít složku...**  z **souboru** nabídky.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-153">Workspace debugging refers to debugging in the context of a folder that you have opened in Visual Studio Code using **Open Folder...** from the **File** menu.</span></span>
<span data-ttu-id="9ccd6-154">Otevření složky je obvykle složky projektu prostředí PowerShell nebo kořenového úložiště Git.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-154">The folder you open is typically your PowerShell project folder and/or the root of your Git repository.</span></span>

<span data-ttu-id="9ccd6-155">I v tomto režimu můžete spustit ladění aktuálně vybrané skriptu prostředí PowerShell jednoduše stisknutím klávesy F5.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-155">Even in this mode, you can start debugging the currently selected PowerShell script by simply pressing F5.</span></span>
<span data-ttu-id="9ccd6-156">Ale ladění prostoru umožňuje definovat ladění konfigurací s více než jen ladění aktuálně otevřených souborů.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-156">However, workspace debugging allows you to define multiple debug configurations other than just debugging the currently open file.</span></span>
<span data-ttu-id="9ccd6-157">Například můžete přidat konfigurace, které:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-157">For instance, you can add a configurations to:</span></span>

- <span data-ttu-id="9ccd6-158">Spusťte testy Pester v ladicím programu</span><span class="sxs-lookup"><span data-stu-id="9ccd6-158">Launch Pester tests in the debugger</span></span>
- <span data-ttu-id="9ccd6-159">Spuštění určitého souboru s argumenty v ladicím programu</span><span class="sxs-lookup"><span data-stu-id="9ccd6-159">Launch a specific file with arguments in the debugger</span></span>
- <span data-ttu-id="9ccd6-160">Spusťte interaktivní relace v ladicím programu</span><span class="sxs-lookup"><span data-stu-id="9ccd6-160">Launch an interactive session in the debugger</span></span>
- <span data-ttu-id="9ccd6-161">Připojí ladicí program k hostitelskému procesu prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ccd6-161">Attach the debugger to a PowerShell host process</span></span>

<span data-ttu-id="9ccd6-162">Postupujte podle těchto kroků můžete vytvořit ladění konfiguračním souboru:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-162">Follow these steps to create your debug configuration file:</span></span>

1. <span data-ttu-id="9ccd6-163">Otevřete **ladění** zobrazení stisknutím **Ctrl + Shift + D** (**Cmd + Shift + D** v systému Mac).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-163">Open the **Debug** view by pressing **Ctrl+Shift+D** (**Cmd+Shift+D** on Mac).</span></span>
1. <span data-ttu-id="9ccd6-164">Stiskněte **konfigurace** ozubené kolečko ikonu na panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-164">Press the **Configure** gear icon in the toolbar.</span></span>
1. <span data-ttu-id="9ccd6-165">Visual Studio Code vás vyzve k **vyberte prostředí**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-165">Visual Studio Code will prompt you to **Select Environment**.</span></span>
   <span data-ttu-id="9ccd6-166">Zvolte **prostředí PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-166">Choose **PowerShell**.</span></span>

   <span data-ttu-id="9ccd6-167">Když to uděláte, Visual Studio Code vytvoří adresář a soubor ".vscode\launch.json" v kořenové složce pracovního prostoru.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-167">When you do this, Visual Studio Code creates a directory and a file ".vscode\launch.json" in the root of your workspace folder.</span></span>
   <span data-ttu-id="9ccd6-168">Toto je, kde je uložen konfiguraci ladění.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-168">This is where your debug configuration is stored.</span></span> <span data-ttu-id="9ccd6-169">Pokud jsou vaše soubory v úložišti Git, obvykle můžete potvrdit soubor launch.json.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-169">If your files are in a Git repository, you will typically want to commit the launch.json file.</span></span>
   <span data-ttu-id="9ccd6-170">Obsah souboru launch.json jsou:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-170">The contents of the launch.json file are:</span></span>

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "PowerShell",
            "request": "launch",
            "name": "PowerShell Launch (current file)",
            "script": "${file}",
            "args": [],
            "cwd": "${file}"
        },
        {
            "type": "PowerShell",
            "request": "attach",
            "name": "PowerShell Attach to Host Process",
            "processId": "${command.PickPSHostProcess}",
            "runspaceId": 1
        },
        {
            "type": "PowerShell",
            "request": "launch",
            "name": "PowerShell Interactive Session",
            "cwd": "${workspaceRoot}"
        }
    ]
}
```

<span data-ttu-id="9ccd6-171">To představuje běžné scénáře ladění.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-171">This represents the common debug scenarios.</span></span>
<span data-ttu-id="9ccd6-172">Ale při otevření tohoto souboru v editoru, zobrazí se **Přidat konfiguraci...**  tlačítko.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-172">However, when you open this file in the editor, you will see an **Add Configuration...** button.</span></span>
<span data-ttu-id="9ccd6-173">Toto tlačítko k přidání více konfigurací ladění prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-173">You can press this button to add more PowerShell debug configurations.</span></span> <span data-ttu-id="9ccd6-174">Je užitečný konfigurací přidat **prostředí PowerShell: Spustí skript**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-174">One handy configuration to add is **PowerShell: Launch Script**.</span></span>
<span data-ttu-id="9ccd6-175">Pomocí této konfigurace můžete zadat konkrétní soubor s volitelné argumenty, které musí být spuštěna vždy, když stisknete klávesu F5, bez ohledu na soubor, který je aktuálně aktivní v editoru.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-175">With this configuration, you can specify a specific file with optional arguments that should be launched whenever you press F5 no matter which file is currently active in the editor.</span></span>

<span data-ttu-id="9ccd6-176">Po vytvoření konfiguraci ladění, můžete vybrat konfiguraci, kterou chcete použít během relace ladění výběrem jedné z rozevíracího seznamu v konfiguraci ladění **ladění** zobrazení panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-176">Once the debug configuration is established, you can select which configuration you want to use during a debug session by selecting one from the debug configuration drop-down in the **Debug** view's toolbar.</span></span>

<span data-ttu-id="9ccd6-177">Existuje několik blogy, které mohou být užitečné, které vám pomůžou začít pomocí prostředí PowerShell rozšíření pro Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9ccd6-177">There are a few blogs that may be helpful to get you started using PowerShell extension for Visual Studio Code</span></span>

- <span data-ttu-id="9ccd6-178">Visual Studio Code: [rozšíření prostředí PowerShell][ps-extension]</span><span class="sxs-lookup"><span data-stu-id="9ccd6-178">Visual Studio Code: [PowerShell Extension][ps-extension]</span></span>
- <span data-ttu-id="9ccd6-179">[Zápis a ladění skriptů prostředí PowerShell v kódu Visual Studio][debug]</span><span class="sxs-lookup"><span data-stu-id="9ccd6-179">[Write and debug PowerShell scripts in Visual Studio Code][debug]</span></span>
- <span data-ttu-id="9ccd6-180">[Ladění v sadě Visual Studio Code pokyny][vscode-guide]</span><span class="sxs-lookup"><span data-stu-id="9ccd6-180">[Debugging Visual Studio Code Guidance][vscode-guide]</span></span>
- <span data-ttu-id="9ccd6-181">[Ladění prostředí PowerShell v sadě Visual Studio kódu][ps-vscode]</span><span class="sxs-lookup"><span data-stu-id="9ccd6-181">[Debugging PowerShell in Visual Studio Code][ps-vscode]</span></span>
- <span data-ttu-id="9ccd6-182">[Začínáme s vývojem pro prostředí PowerShell v kódu Visual Studio][getting-started]</span><span class="sxs-lookup"><span data-stu-id="9ccd6-182">[Get started with PowerShell development in Visual Studio Code][getting-started]</span></span>
- <span data-ttu-id="9ccd6-183">[Visual Studio Code úpravy funkce pro vývoj prostředí PowerShell – část 1][editing-part1]</span><span class="sxs-lookup"><span data-stu-id="9ccd6-183">[Visual Studio Code editing features for PowerShell development – Part 1][editing-part1]</span></span>
- <span data-ttu-id="9ccd6-184">[Visual Studio Code úpravy funkce pro vývoj prostředí PowerShell – část 2][editing-part2]</span><span class="sxs-lookup"><span data-stu-id="9ccd6-184">[Visual Studio Code editing features for PowerShell development – Part 2][editing-part2]</span></span>
- <span data-ttu-id="9ccd6-185">[Ladění skriptu prostředí PowerShell v kódu Visual Studio – část 1][debugging-part1]</span><span class="sxs-lookup"><span data-stu-id="9ccd6-185">[Debugging PowerShell script in Visual Studio Code – Part 1][debugging-part1]</span></span>
- <span data-ttu-id="9ccd6-186">[Ladění skriptu prostředí PowerShell v kódu Visual Studio – část 2][debugging-part2]</span><span class="sxs-lookup"><span data-stu-id="9ccd6-186">[Debugging PowerShell script in Visual Studio Code – Part 2][debugging-part2]</span></span>

[ise]: ../ise-guide.md
[install-pscore-linux]:  ../../setup/Installing-PowerShell-Core-on-macOS-and-Linux.md
[install-pscore-windows]: ../../setup/Installing-PowerShell-Core-on-Windows.md
[install-winps]: ../../setup/Installing-Windows-PowerShell.md
[ps-extension]:https://blogs.msdn.microsoft.com/cdndevs/2015/12/11/visual-studio-code-powershell-extension/
[debug]:https://blogs.msdn.microsoft.com/powershell/2015/11/16/announcing-powershell-language-support-for-visual-studio-code-and-more/
[vscode-guide]:https://johnpapa.net/debugging-with-visual-studio-code/
[ps-vscode]:https://github.com/PowerShell/vscode-powershell/tree/master/examples
[getting-started]:https://blogs.technet.microsoft.com/heyscriptingguy/2016/12/05/get-started-with-powershell-development-in-visual-studio-code/
[editing-part1]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/11/visual-studio-code-editing-features-for-powershell-development-part-1/
[editing-part2]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/12/visual-studio-code-editing-features-for-powershell-development-part-2/
[debugging-part1]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/06/debugging-powershell-script-in-visual-studio-code-part-1/
[debugging-part2]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/13/debugging-powershell-script-in-visual-studio-code-part-2/

## <a name="powershell-extension-for-visual-studio-code"></a><span data-ttu-id="9ccd6-187">Rozšíření prostředí PowerShell pro Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9ccd6-187">PowerShell Extension for Visual Studio Code</span></span>

<span data-ttu-id="9ccd6-188">Rozšíření prostředí PowerShell zdrojový kód najdete na [Githubu](https://github.com/PowerShell/vscode-powershell).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-188">The PowerShell extension's source code can be found on [GitHub](https://github.com/PowerShell/vscode-powershell).</span></span>