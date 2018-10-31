---
title: Pomocí Visual Studio Code pro vývoj v prostředí PowerShell
description: Pomocí Visual Studio Code pro vývoj v prostředí PowerShell
ms.date: 08/06/2018
ms.openlocfilehash: 9c06ce72c39d08e75fcb7e5cf9d5f92ae5dd8ed9
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2018
ms.locfileid: "50225790"
---
# <a name="using-visual-studio-code-for-powershell-development"></a><span data-ttu-id="c3078-103">Pomocí Visual Studio Code pro vývoj v prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3078-103">Using Visual Studio Code for PowerShell Development</span></span>

<span data-ttu-id="c3078-104">Kromě [prostředí PowerShell ISE][ise], prostředí PowerShell je také dobře podporované ve Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c3078-104">In addition to the [PowerShell ISE][ise], PowerShell is also well-supported in Visual Studio Code.</span></span>
<span data-ttu-id="c3078-105">Kromě toho ISE nepodporuje pomocí prostředí PowerShell Core, i když Visual Studio Code podporuje prostředí PowerShell Core na všech platformách (Windows, macOS a Linux)</span><span class="sxs-lookup"><span data-stu-id="c3078-105">Furthermore, the ISE is not supported with PowerShell Core, while Visual Studio Code is supported for PowerShell Core on all platforms (Windows, macOS, and Linux)</span></span>

<span data-ttu-id="c3078-106">Můžete použít Visual Studio Code ve Windows pomocí prostředí PowerShell verze 5 s použitím Windows 10 nebo po instalaci [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) pro nižší úrovně OSs Windows (např. Windows 8.1, atd.).</span><span class="sxs-lookup"><span data-stu-id="c3078-106">You can use Visual Studio Code on Windows with PowerShell version 5 by using Windows 10 or by installing [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) for down-level Windows OSs (e.g. Windows 8.1, etc.).</span></span>

<span data-ttu-id="c3078-107">Před jeho zahájením, ujistěte se prosím, že prostředí PowerShell v systému existuje.</span><span class="sxs-lookup"><span data-stu-id="c3078-107">Before starting it, please make sure PowerShell exists on your system.</span></span>
<span data-ttu-id="c3078-108">Pro moderní úlohy ve Windows, macOS a Linuxu naleznete v tématu:</span><span class="sxs-lookup"><span data-stu-id="c3078-108">For modern workloads on Windows, macOS, and Linux, see:</span></span>

- <span data-ttu-id="c3078-109">[Instalace Powershellu Core v Linuxu][install-pscore-linux]</span><span class="sxs-lookup"><span data-stu-id="c3078-109">[Installing PowerShell Core on Linux][install-pscore-linux]</span></span>
- <span data-ttu-id="c3078-110">[Instalace Powershellu Core v macOS][install-pscore-macos]</span><span class="sxs-lookup"><span data-stu-id="c3078-110">[Installing PowerShell Core on macOS][install-pscore-macos]</span></span>
- <span data-ttu-id="c3078-111">[Instalace Powershellu Core ve Windows][install-pscore-windows]</span><span class="sxs-lookup"><span data-stu-id="c3078-111">[Installing PowerShell Core on Windows][install-pscore-windows]</span></span>

<span data-ttu-id="c3078-112">Pro tradiční úlohy v prostředí Windows PowerShell najdete v článku [instalace prostředí Windows PowerShell][install-winps].</span><span class="sxs-lookup"><span data-stu-id="c3078-112">For traditional Windows PowerShell workloads, see [Installing Windows PowerShell][install-winps].</span></span>

## <a name="editing-with-visual-studio-code"></a><span data-ttu-id="c3078-113">Úpravy ve Visual Studiu Code</span><span class="sxs-lookup"><span data-stu-id="c3078-113">Editing with Visual Studio Code</span></span>

### <a name="1-installing-visual-studio-codehttpscodevisualstudiocomdocssetupsetup-overview"></a>[<span data-ttu-id="c3078-114">1. Instalace Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c3078-114">1. Installing Visual Studio Code</span></span>](https://code.visualstudio.com/Docs/setup/setup-overview)

- <span data-ttu-id="c3078-115">**Linux**: postupujte podle pokynů k instalaci na [spuštění VS Code na Linuxu](https://code.visualstudio.com/docs/setup/linux) stránky</span><span class="sxs-lookup"><span data-stu-id="c3078-115">**Linux**: follow the installation instructions on the [Running VS Code on Linux](https://code.visualstudio.com/docs/setup/linux) page</span></span>

- <span data-ttu-id="c3078-116">**macOS**: postupujte podle pokynů k instalaci na [spuštění VS Code na macOS](https://code.visualstudio.com/docs/setup/mac) stránky</span><span class="sxs-lookup"><span data-stu-id="c3078-116">**macOS**: follow the installation instructions on the [Running VS Code on macOS](https://code.visualstudio.com/docs/setup/mac) page</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c3078-117">V systému macOS musíte nainstalovat OpenSSL pro rozšíření prostředí PowerShell správně fungovat.</span><span class="sxs-lookup"><span data-stu-id="c3078-117">On macOS, you must install OpenSSL for the PowerShell extension to work correctly.</span></span>
  > <span data-ttu-id="c3078-118">Nejjednodušší způsob, jak to provést, je instalace [Homebrew](http://brew.sh/) a pak spusťte `brew install openssl`.</span><span class="sxs-lookup"><span data-stu-id="c3078-118">The easiest way to accomplish this is to install [Homebrew](http://brew.sh/) and then run `brew install openssl`.</span></span>
  > <span data-ttu-id="c3078-119">VS Code teď možné úspěšně načíst rozšíření prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c3078-119">VS Code can now load the PowerShell extension successfully.</span></span>

- <span data-ttu-id="c3078-120">**Windows**: postupujte podle pokynů k instalaci na [spuštění VS Code na Windows](https://code.visualstudio.com/docs/setup/windows) stránky</span><span class="sxs-lookup"><span data-stu-id="c3078-120">**Windows**: follow the installation instructions on the [Running VS Code on Windows](https://code.visualstudio.com/docs/setup/windows) page</span></span>

### <a name="2-installing-powershell-extension"></a><span data-ttu-id="c3078-121">2. Instaluje se rozšíření Powershellu</span><span class="sxs-lookup"><span data-stu-id="c3078-121">2. Installing PowerShell Extension</span></span>

- <span data-ttu-id="c3078-122">Spuštění sady Visual Studio Code aplikaci:</span><span class="sxs-lookup"><span data-stu-id="c3078-122">Launch the Visual Studio Code app by:</span></span>
  - <span data-ttu-id="c3078-123">**Windows**: psaní `code` v relaci prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3078-123">**Windows**: typing `code` in your PowerShell session</span></span>
  - <span data-ttu-id="c3078-124">**Linux**: psaní `code` v terminálu</span><span class="sxs-lookup"><span data-stu-id="c3078-124">**Linux**: typing `code` in your terminal</span></span>
  - <span data-ttu-id="c3078-125">**macOS**: psaní `code` v terminálu</span><span class="sxs-lookup"><span data-stu-id="c3078-125">**macOS**: typing `code` in your terminal</span></span>

- <span data-ttu-id="c3078-126">Spuštění **okno rychlého otevření** stisknutím kombinace kláves **Ctrl + P** (**Cmd + P** na počítači Mac).</span><span class="sxs-lookup"><span data-stu-id="c3078-126">Launch **Quick Open** by pressing **Ctrl+P** (**Cmd+P** on Mac).</span></span>
- <span data-ttu-id="c3078-127">Okno rychlého otevření zadejte `ext install powershell` a přístupů **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c3078-127">In Quick Open, type `ext install powershell` and hit **Enter**.</span></span>
- <span data-ttu-id="c3078-128">**Rozšíření** na bočním panelu otevře se zobrazení.</span><span class="sxs-lookup"><span data-stu-id="c3078-128">The **Extensions** view opens on the Side Bar.</span></span> <span data-ttu-id="c3078-129">Vyberte rozšíření prostředí PowerShell od Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="c3078-129">Select the PowerShell extension from Microsoft.</span></span>
  <span data-ttu-id="c3078-130">By měl vypadat přibližně jako následující:</span><span class="sxs-lookup"><span data-stu-id="c3078-130">You should see something like below:</span></span>

  ![VSCode](../../images/vscode.png)

- <span data-ttu-id="c3078-132">Klikněte na tlačítko **nainstalovat** tlačítko na rozšíření prostředí PowerShell od Microsoftu.</span><span class="sxs-lookup"><span data-stu-id="c3078-132">Click the **Install** button on the PowerShell extension from Microsoft.</span></span>
- <span data-ttu-id="c3078-133">Po instalaci, zobrazí **nainstalovat** tlačítko se změní **Reload**.</span><span class="sxs-lookup"><span data-stu-id="c3078-133">After the install, you see the **Install** button turns to **Reload**.</span></span>
  <span data-ttu-id="c3078-134">Klikněte na **Reload**.</span><span class="sxs-lookup"><span data-stu-id="c3078-134">Click on **Reload**.</span></span>
- <span data-ttu-id="c3078-135">Poté, co Visual Studio Code má nové načtení, jste připraveni pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="c3078-135">After Visual Studio Code has reload, you are ready for editing.</span></span>

<span data-ttu-id="c3078-136">Například chcete-li vytvořit nový soubor, klikněte na tlačítko **soubor -> Nový**.</span><span class="sxs-lookup"><span data-stu-id="c3078-136">For example, to create a new file, click **File->New**.</span></span>
<span data-ttu-id="c3078-137">Pokud chcete uložit, klikněte na tlačítko **soubor -> Uložit** a pak zadejte název souboru, Pojďme Dejme tomu, že `HelloWorld.ps1`.</span><span class="sxs-lookup"><span data-stu-id="c3078-137">To save it, click **File->Save** and then provide a file name, let's say `HelloWorld.ps1`.</span></span>
<span data-ttu-id="c3078-138">Zavřete soubor, klikněte na "x" vedle jeho názvu.</span><span class="sxs-lookup"><span data-stu-id="c3078-138">To close the file, click on "x" next to the file name.</span></span>
<span data-ttu-id="c3078-139">Chcete-li ukončit Visual Studio Code, **soubor -> ukončení**.</span><span class="sxs-lookup"><span data-stu-id="c3078-139">To exit Visual Studio Code, **File->Exit**.</span></span>

#### <a name="using-a-specific-installed-version-of-powershell"></a><span data-ttu-id="c3078-140">Pomocí konkrétní nainstalovanou verzi prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3078-140">Using a specific installed version of PowerShell</span></span>

<span data-ttu-id="c3078-141">Pokud chcete použít konkrétní instalaci prostředí PowerShell pomocí Visual Studio Code, budete muset do souboru nastavení uživatele přidejte novou proměnnou.</span><span class="sxs-lookup"><span data-stu-id="c3078-141">If you wish to use a specific installation of PowerShell with Visual Studio Code, you need to add a new variable to your user settings file.</span></span>

1. <span data-ttu-id="c3078-142">Klikněte na tlačítko **soubor -> Předvolby -> Nastavení**</span><span class="sxs-lookup"><span data-stu-id="c3078-142">Click **File -> Preferences -> Settings**</span></span>
1. <span data-ttu-id="c3078-143">Zobrazí se dvě podokna editoru.</span><span class="sxs-lookup"><span data-stu-id="c3078-143">Two editor panes appear.</span></span>
   <span data-ttu-id="c3078-144">V podokně úplně vpravo (`settings.json`), vložte níže uvedené nastavení vhodná pro váš operační systém někde mezi dva složené závorky (`{` a `}`) a nahraďte **\<verze\>** s nainstalovanou verzí Powershellu:</span><span class="sxs-lookup"><span data-stu-id="c3078-144">In the right-most pane (`settings.json`), insert the setting below appropriate for your OS somewhere between the two curly brackets (`{` and `}`) and replace **\<version\>** with the installed PowerShell version:</span></span>

   ```json
    // On Windows:
    "powershell.powerShellExePath": "c:/Program Files/PowerShell/<version>/pwsh.exe"

    // On Linux:
    "powershell.powerShellExePath": "/opt/microsoft/powershell/<version>/pwsh"

    // On macOS:
    "powershell.powerShellExePath": "/usr/local/microsoft/powershell/<version>/pwsh"
   ```

1. <span data-ttu-id="c3078-145">Nahraďte cestou do požadovaného Powershellu spustitelný soubor nastavení</span><span class="sxs-lookup"><span data-stu-id="c3078-145">Replace the setting with the path to the desired PowerShell executable</span></span>
1. <span data-ttu-id="c3078-146">Uložte soubor s nastaveními a restartujte Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c3078-146">Save the settings file and restart Visual Studio Code</span></span>

#### <a name="configuration-settings-for-visual-studio-code"></a><span data-ttu-id="c3078-147">Nastavení konfigurace pro Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c3078-147">Configuration settings for Visual Studio Code</span></span>

<span data-ttu-id="c3078-148">Pomocí kroků v předchozím odstavci můžete přidat nastavení konfigurace v `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="c3078-148">By using the steps in the previous paragraph you can add configuration settings in `settings.json`.</span></span>

<span data-ttu-id="c3078-149">Doporučujeme následující nastavení konfigurace pro Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="c3078-149">We recommend the following configuration settings for Visual Studio Code:</span></span>

```json
{
    "csharp.suppressDotnetRestoreNotification": true,
    "editor.renderWhitespace": "all",
    "editor.renderControlCharacters": true,
    "omnisharp.projectLoadTimeout": 120,
    "files.trimTrailingWhitespace": true
}
```

## <a name="debugging-with-visual-studio-code"></a><span data-ttu-id="c3078-150">Ladění ve Visual Studiu Code</span><span class="sxs-lookup"><span data-stu-id="c3078-150">Debugging with Visual Studio Code</span></span>

### <a name="no-workspace-debugging"></a><span data-ttu-id="c3078-151">Ladění žádný pracovní prostor</span><span class="sxs-lookup"><span data-stu-id="c3078-151">No-workspace debugging</span></span>

<span data-ttu-id="c3078-152">Od verze Visual Studio Code 1.9 můžete ladit skripty Powershellu bez nutnosti otevřít složku, která obsahuje skript prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c3078-152">As of Visual Studio Code version 1.9 you can debug PowerShell scripts without having to open the folder containing the PowerShell script.</span></span>
<span data-ttu-id="c3078-153">Jednoduše otevřete soubor skriptu Powershellu pomocí **soubor -> Otevřít soubor...** , nastavte zarážku na řádku (stiskněte klávesu F9) a potom stiskněte klávesu F5 pro spuštění ladění.</span><span class="sxs-lookup"><span data-stu-id="c3078-153">Simply open the PowerShell script file with **File->Open File...**, set a breakpoint on a line (press F9) and then press F5 to start debugging.</span></span>
<span data-ttu-id="c3078-154">Měli byste vidět podokna akcí ladění se zobrazí, které umožňuje proniknout do ladicího programu, krok, obnovit a Zastavit ladění.</span><span class="sxs-lookup"><span data-stu-id="c3078-154">You should see the Debug actions pane appear which allows you to break into the debugger, step, resume and stop debugging.</span></span>

### <a name="workspace-debugging"></a><span data-ttu-id="c3078-155">Ladění pracovního prostoru</span><span class="sxs-lookup"><span data-stu-id="c3078-155">Workspace debugging</span></span>

<span data-ttu-id="c3078-156">Pracovní prostor ladění odkazuje na ladění v rámci složky, kterou jste otevřeli pomocí Visual Studio Code **otevřít složku...**  z **souboru** nabídky.</span><span class="sxs-lookup"><span data-stu-id="c3078-156">Workspace debugging refers to debugging in the context of a folder that you have opened in Visual Studio Code using **Open Folder...** from the **File** menu.</span></span>
<span data-ttu-id="c3078-157">Otevření složky je obvykle složky projektu Powershellu a/nebo kořenu úložiště Git.</span><span class="sxs-lookup"><span data-stu-id="c3078-157">The folder you open is typically your PowerShell project folder and/or the root of your Git repository.</span></span>

<span data-ttu-id="c3078-158">I v tomto režimu ladění lze spustit vybrané skript Powershellu jednoduše stisknutím klávesy F5.</span><span class="sxs-lookup"><span data-stu-id="c3078-158">Even in this mode, you can start debugging the currently selected PowerShell script by simply pressing F5.</span></span>
<span data-ttu-id="c3078-159">Ale ladění pracovního prostoru můžete zadat ladění konfigurací s víc než jenom ladění aktuálně otevřený soubor.</span><span class="sxs-lookup"><span data-stu-id="c3078-159">However, workspace debugging allows you to define multiple debug configurations other than just debugging the currently open file.</span></span>
<span data-ttu-id="c3078-160">Můžete například přidat konfigurace, které:</span><span class="sxs-lookup"><span data-stu-id="c3078-160">For instance, you can add a configurations to:</span></span>

- <span data-ttu-id="c3078-161">Spusťte testy Pester v ladicím programu</span><span class="sxs-lookup"><span data-stu-id="c3078-161">Launch Pester tests in the debugger</span></span>
- <span data-ttu-id="c3078-162">Spuštění konkrétního souboru s argumenty v ladicím programu</span><span class="sxs-lookup"><span data-stu-id="c3078-162">Launch a specific file with arguments in the debugger</span></span>
- <span data-ttu-id="c3078-163">Spustit interaktivní relaci v ladicím programu</span><span class="sxs-lookup"><span data-stu-id="c3078-163">Launch an interactive session in the debugger</span></span>
- <span data-ttu-id="c3078-164">Připojit ladicí program k procesu hostitele prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3078-164">Attach the debugger to a PowerShell host process</span></span>

<span data-ttu-id="c3078-165">Postupujte podle těchto kroků můžete vytvořit konfigurační soubor ladění:</span><span class="sxs-lookup"><span data-stu-id="c3078-165">Follow these steps to create your debug configuration file:</span></span>

  1. <span data-ttu-id="c3078-166">Otevřít **ladění** zobrazit stisknutím klávesy **Ctrl + Shift + D** (**Cmd + Shift + D** na počítači Mac).</span><span class="sxs-lookup"><span data-stu-id="c3078-166">Open the **Debug** view by pressing **Ctrl+Shift+D** (**Cmd+Shift+D** on Mac).</span></span>
  2. <span data-ttu-id="c3078-167">Stisknutím klávesy **konfigurovat** ikonu ozubeného kolečka v panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="c3078-167">Press the **Configure** gear icon in the toolbar.</span></span>
  3. <span data-ttu-id="c3078-168">Visual Studio Code vás vyzve, abyste **vyberte prostředí**.</span><span class="sxs-lookup"><span data-stu-id="c3078-168">Visual Studio Code prompts you to **Select Environment**.</span></span> <span data-ttu-id="c3078-169">Zvolte **Powershellu**.</span><span class="sxs-lookup"><span data-stu-id="c3078-169">Choose **PowerShell**.</span></span>

  <span data-ttu-id="c3078-170">Když toto provedete, Visual Studio Code vytvoří adresář a soubor ".vscode\launch.json" v kořenovém adresáři vašeho pracovního prostoru.</span><span class="sxs-lookup"><span data-stu-id="c3078-170">When you do this, Visual Studio Code creates a directory and a file ".vscode\launch.json" in the root of your workspace folder.</span></span>
  <span data-ttu-id="c3078-171">Toto je ukládat konfiguraci ladění.</span><span class="sxs-lookup"><span data-stu-id="c3078-171">This is where your debug configuration is stored.</span></span> <span data-ttu-id="c3078-172">Pokud jsou vaše soubory v úložišti Git, obvykle chcete potvrdit souboru launch.json.</span><span class="sxs-lookup"><span data-stu-id="c3078-172">If your files are in a Git repository, you typically want to commit the launch.json file.</span></span>
  <span data-ttu-id="c3078-173">Obsah souboru launch.json jsou:</span><span class="sxs-lookup"><span data-stu-id="c3078-173">The contents of the launch.json file are:</span></span>

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

  <span data-ttu-id="c3078-174">To představuje běžné scénáře ladění.</span><span class="sxs-lookup"><span data-stu-id="c3078-174">This represents the common debug scenarios.</span></span>
  <span data-ttu-id="c3078-175">Ale při otevření tohoto souboru v editoru, se zobrazí **Přidat konfiguraci...**  tlačítko.</span><span class="sxs-lookup"><span data-stu-id="c3078-175">However, when you open this file in the editor, you see an **Add Configuration...** button.</span></span>
  <span data-ttu-id="c3078-176">Toto tlačítko pro přidání další konfiguraci ladění Powershellu.</span><span class="sxs-lookup"><span data-stu-id="c3078-176">You can press this button to add more PowerShell debug configurations.</span></span> <span data-ttu-id="c3078-177">Je jedna po ruce konfigurace k přidání **prostředí PowerShell: Spusťte skript**.</span><span class="sxs-lookup"><span data-stu-id="c3078-177">One handy configuration to add is **PowerShell: Launch Script**.</span></span>
  <span data-ttu-id="c3078-178">S touto konfigurací můžete zadat konkrétní soubor s volitelné argumenty, které má být spuštěna vždy, když stisknete klávesu F5, bez ohledu na to soubor, který je právě aktivní v editoru.</span><span class="sxs-lookup"><span data-stu-id="c3078-178">With this configuration, you can specify a specific file with optional arguments that should be launched whenever you press F5 no matter which file is currently active in the editor.</span></span>

  <span data-ttu-id="c3078-179">Jakmile se naváže konfiguraci ladění, můžete vybrat konfiguraci, kterou chcete použít během relace ladění výběrem jedné z rozevíracího seznamu v konfiguraci ladění **ladění** nástrojů pro zobrazení.</span><span class="sxs-lookup"><span data-stu-id="c3078-179">Once the debug configuration is established, you can select which configuration you want to use during a debug session by selecting one from the debug configuration drop-down in the **Debug** view's toolbar.</span></span>

<span data-ttu-id="c3078-180">Existuje několik blogy, které mohou být užitečné, které vám pomůžou začít pomocí rozšíření prostředí PowerShell pro Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="c3078-180">There are a few blogs that may be helpful to get you started using PowerShell extension for Visual Studio Code:</span></span>

- <span data-ttu-id="c3078-181">[Rozšíření prostředí PowerShell][ps-extension]</span><span class="sxs-lookup"><span data-stu-id="c3078-181">[PowerShell Extension][ps-extension]</span></span>
- <span data-ttu-id="c3078-182">[Programujte a laďte Powershellových skriptů v aplikaci Visual Studio Code][debug]</span><span class="sxs-lookup"><span data-stu-id="c3078-182">[Write and debug PowerShell scripts in Visual Studio Code][debug]</span></span>
- <span data-ttu-id="c3078-183">[Ladění v sadě Visual Studio Code pokyny][vscode-guide]</span><span class="sxs-lookup"><span data-stu-id="c3078-183">[Debugging Visual Studio Code Guidance][vscode-guide]</span></span>
- <span data-ttu-id="c3078-184">[Ladění v prostředí PowerShell ve službě Visual Studio Code][ps-vscode]</span><span class="sxs-lookup"><span data-stu-id="c3078-184">[Debugging PowerShell in Visual Studio Code][ps-vscode]</span></span>
- <span data-ttu-id="c3078-185">[Začínáme s vývojem Powershellu ve Visual Studio Code][getting-started]</span><span class="sxs-lookup"><span data-stu-id="c3078-185">[Get started with PowerShell development in Visual Studio Code][getting-started]</span></span>
- <span data-ttu-id="c3078-186">[Visual Studio Code úpravy funkce pro vývoj Powershellu – část 1][editing-part1]</span><span class="sxs-lookup"><span data-stu-id="c3078-186">[Visual Studio Code editing features for PowerShell development – Part 1][editing-part1]</span></span>
- <span data-ttu-id="c3078-187">[Visual Studio Code úpravy funkce pro vývoj Powershellu – část 2][editing-part2]</span><span class="sxs-lookup"><span data-stu-id="c3078-187">[Visual Studio Code editing features for PowerShell development – Part 2][editing-part2]</span></span>
- <span data-ttu-id="c3078-188">[Ladění skriptů Powershellu v aplikaci Visual Studio Code – část 1][debugging-part1]</span><span class="sxs-lookup"><span data-stu-id="c3078-188">[Debugging PowerShell script in Visual Studio Code – Part 1][debugging-part1]</span></span>
- <span data-ttu-id="c3078-189">[Ladění skriptů Powershellu v aplikaci Visual Studio Code – část 2][debugging-part2]</span><span class="sxs-lookup"><span data-stu-id="c3078-189">[Debugging PowerShell script in Visual Studio Code – Part 2][debugging-part2]</span></span>

[ise]: ../ise-guide.md
[install-pscore-linux]:  ../../setup/Installing-PowerShell-Core-on-Linux.md
[install-pscore-macos]:  ../../setup/Installing-PowerShell-Core-on-macOS.md
[install-pscore-windows]: ../../setup/Installing-PowerShell-Core-on-Windows.md
[install-winps]: ../../setup/Installing-Windows-PowerShell.md
[ps-extension]: https://blogs.msdn.microsoft.com/cdndevs/2015/12/11/visual-studio-code-powershell-extension/
[debug]: https://blogs.msdn.microsoft.com/powershell/2015/11/16/announcing-powershell-language-support-for-visual-studio-code-and-more/
[vscode-guide]: https://johnpapa.net/debugging-with-visual-studio-code/
[ps-vscode]: https://github.com/PowerShell/vscode-powershell/tree/master/examples
[getting-started]: https://blogs.technet.microsoft.com/heyscriptingguy/2016/12/05/get-started-with-powershell-development-in-visual-studio-code/
[editing-part1]: https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/11/visual-studio-code-editing-features-for-powershell-development-part-1/
[editing-part2]: https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/12/visual-studio-code-editing-features-for-powershell-development-part-2/
[debugging-part1]: https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/06/debugging-powershell-script-in-visual-studio-code-part-1/
[debugging-part2]: https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/13/debugging-powershell-script-in-visual-studio-code-part-2/

## <a name="powershell-extension-for-visual-studio-code"></a><span data-ttu-id="c3078-190">Rozšíření prostředí PowerShell pro Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c3078-190">PowerShell Extension for Visual Studio Code</span></span>

<span data-ttu-id="c3078-191">Rozšíření prostředí PowerShell zdrojový kód můžete najít na [Githubu](https://github.com/PowerShell/vscode-powershell).</span><span class="sxs-lookup"><span data-stu-id="c3078-191">The PowerShell extension's source code can be found on [GitHub](https://github.com/PowerShell/vscode-powershell).</span></span>
