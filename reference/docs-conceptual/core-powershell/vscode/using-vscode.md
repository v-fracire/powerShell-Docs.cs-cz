# <a name="using-visual-studio-code-for-powershell-development"></a>Pomocí kódu v sadě Visual Studio pro vývoj prostředí PowerShell

Kromě [prostředí PowerShell ISE][ise], prostředí PowerShell je také dobře podporované v kódu Visual Studio.
Kromě toho se ISE nepodporuje základní prostředí PowerShell, když Visual Studio Code je podporována pro základní prostředí PowerShell na všech platformách (Windows, systému macOS a Linux)

Visual Studio Code můžete použít v systému Windows v prostředí PowerShell verze 5 s použitím Windows 10 nebo instalací [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) pro nižší úrovně operačních systémů Windows (např. Windows 8.1, atd.).

Před zahájením ho, Zkontrolujte prosím, že prostředí PowerShell v systému existuje.
Pro moderní úlohy u systému Windows, systému macOS a Linux, přečtěte si část:

- [Instalace jádra prostředí PowerShell v systému macOS a Linux][install-pscore-linux]
- [Instalace jádra prostředí PowerShell v systému Windows][install-pscore-windows]

Pro tradiční úlohy prostředí Windows PowerShell, najdete v části [instalace prostředí Windows PowerShell][install-winps].

## <a name="editing-with-visual-studio-code"></a>Úpravy s Visual Studio Code

### <a name="1-installing-visual-studio-codehttpscodevisualstudiocomdocssetupsetup-overview"></a>[1. Instalace Visual Studio Code](https://code.visualstudio.com/Docs/setup/setup-overview)

- **Linux**: postupujte podle pokynů k instalaci na [systémem VS Code v systému Linux](https://code.visualstudio.com/docs/setup/linux) stránky

- **systému macOS**: postupujte podle pokynů k instalaci na [systémem VS Code v systému macOS](https://code.visualstudio.com/docs/setup/mac) stránky

> [!IMPORTANT]
> V systému macOS je třeba nainstalovat OpenSSL pro rozšíření prostředí PowerShell fungovala správně.
> Nejjednodušší způsob, jak se má nainstalovat [Homebrew](http://brew.sh/) a spusťte `brew install openssl`.
> Nyní bude moct úspěšně načíst rozšíření prostředí PowerShell.

- **Windows**: postupujte podle pokynů k instalaci na [systémem VS Code v systému Windows](https://code.visualstudio.com/docs/setup/windows) stránky

### <a name="2-installing-powershell-extension"></a>2. Instaluje se rozšíření prostředí PowerShell

- Spuštění sady Visual Studio Code aplikace pomocí:
    - **Windows**: zadáním `code` v relaci prostředí PowerShell
    - **Linux**: zadáním `code` v terminálu
    - **systému macOS**: zadáním `code` v terminálu

- Spusťte **rychlé otevřete** stisknutím **Ctrl + P** (**Cmd + P** na Mac).
- V rychlé otevřený, zadejte `ext install powershell` a počtu **Enter**.
- **Rozšíření** na straně panelu se otevře zobrazení. Vyberte požadované rozšíření prostředí PowerShell od společnosti Microsoft.
  Zobrazí se něco jako níže:

  ![VSCode](../../images/vscode.png)

- Klikněte **nainstalovat** tlačítko pro rozšíření prostředí PowerShell od společnosti Microsoft.
- Po instalaci, zobrazí se **nainstalovat** tlačítko se změní **opětovného načtení**.
  Klikněte na **opětovného načtení**.
- Po Visual Studio Code má načíst znovu, jste připraveni pro úpravy.

Například pokud chcete vytvořit nový soubor, klikněte na možnost **souboru -> Nový**.
Chcete-li uložit, klikněte na tlačítko **souboru -> Uložit** a pak zadejte název souboru, můžeme vyslovte `HelloWorld.ps1`.
Zavřete soubor, klikněte na "x" vedle názvu souboru.
Chcete-li ukončit Visual Studio Code **souboru -> ukončení**.

#### <a name="using-a-specific-installed-version-of-powershell"></a>Pomocí konkrétní nainstalovaná verze prostředí PowerShell

Pokud chcete použít konkrétní instalaci prostředí PowerShell s kódem jazyka Visual Studio, musíte přidat nové proměnné do souboru nastavení uživatele.

1. Klikněte na tlačítko **souboru -> Předvolby -> Nastavení**
1. Zobrazí se dvě podokna editor.
   V podokně nejvíce vpravo (`settings.json`), vložte následující nastavení vhodné pro váš operační systém někde mezi dvěma složené závorky (`{` a `}`) a nahraďte  *<version>*  s nainstalovaným klientem Verze prostředí PowerShell:

  ```json
    // On Windows:
    "powershell.powerShellExePath": "c:/Program Files/PowerShell/<version>/pwsh.exe"

    // On Linux:
    "powershell.powerShellExePath": "/opt/microsoft/powershell/<version>/pwsh"

    // On macOS:
    "powershell.powerShellExePath": "/usr/local/microsoft/powershell/<version>/pwsh"
  ```
1. Nastavení nahraďte cesta k požadované spustitelný soubor prostředí PowerShell
1. Uložte soubor s nastaveními a restartujte Visual Studio Code

#### <a name="configuration-settings-for-visual-studio-code"></a>Nastavení konfigurace pro Visual Studio Code

Pomocí kroků v předchozím odstavci můžete přidat nastavení konfigurace v `settings.json`.

Doporučujeme následující nastavení konfigurace pro Visual Studio Code:

```json
{
    "csharp.suppressDotnetRestoreNotification": true,
    "editor.renderWhitespace": "all",
    "editor.renderControlCharacters": true,
    "omnisharp.projectLoadTimeout": 120,
    "files.trimTrailingWhitespace": true
}
```

## <a name="debugging-with-visual-studio-code"></a>Ladění pomocí kódu v sadě Visual Studio

### <a name="no-workspace-debugging"></a>Prostoru bez ladění

Od verze Visual Studio Code 1.9 můžete ladit skripty prostředí PowerShell, bez nutnosti otevřít složku, která obsahuje skript prostředí PowerShell.
Stačí otevřít soubor skriptu prostředí PowerShell s **souboru -> Otevřít soubor...** , zarážku na řádek (stiskněte F9) a poté stisknutím klávesy F5 spusťte ladění.
Zobrazí se v podokně Akce ladění zobrazují, které umožňuje rozdělit ladicí program, krok, opětovné spuštění a zastavení ladění.

### <a name="workspace-debugging"></a>Pracovní prostor ladění

Pracovní prostor ladění odkazuje na ladění v kontextu složce, kterou jste otevřeli pomocí Visual Studio Code **otevřít složku...**  z **souboru** nabídky.
Otevření složky je obvykle složky projektu prostředí PowerShell nebo kořenového úložiště Git.

I v tomto režimu můžete spustit ladění aktuálně vybrané skriptu prostředí PowerShell jednoduše stisknutím klávesy F5.
Ale ladění prostoru umožňuje definovat ladění konfigurací s více než jen ladění aktuálně otevřených souborů.
Například můžete přidat konfigurace, které:

- Spusťte testy Pester v ladicím programu
- Spuštění určitého souboru s argumenty v ladicím programu
- Spusťte interaktivní relace v ladicím programu
- Připojí ladicí program k hostitelskému procesu prostředí PowerShell

Postupujte podle těchto kroků můžete vytvořit ladění konfiguračním souboru:

1. Otevřete **ladění** zobrazení stisknutím **Ctrl + Shift + D** (**Cmd + Shift + D** v systému Mac).
1. Stiskněte **konfigurace** ozubené kolečko ikonu na panelu nástrojů.
1. Visual Studio Code vás vyzve k **vyberte prostředí**.
   Zvolte **prostředí PowerShell**.

   Když to uděláte, Visual Studio Code vytvoří adresář a soubor ".vscode\launch.json" v kořenové složce pracovního prostoru.
   Toto je, kde je uložen konfiguraci ladění. Pokud jsou vaše soubory v úložišti Git, obvykle můžete potvrdit soubor launch.json.
   Obsah souboru launch.json jsou:

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

To představuje běžné scénáře ladění.
Ale při otevření tohoto souboru v editoru, zobrazí se **Přidat konfiguraci...**  tlačítko.
Toto tlačítko k přidání více konfigurací ladění prostředí PowerShell. Je užitečný konfigurací přidat **prostředí PowerShell: Spustí skript**.
Pomocí této konfigurace můžete zadat konkrétní soubor s volitelné argumenty, které musí být spuštěna vždy, když stisknete klávesu F5, bez ohledu na soubor, který je aktuálně aktivní v editoru.

Po vytvoření konfiguraci ladění, můžete vybrat konfiguraci, kterou chcete použít během relace ladění výběrem jedné z rozevíracího seznamu v konfiguraci ladění **ladění** zobrazení panelu nástrojů.

Existuje několik blogy, které mohou být užitečné, které vám pomůžou začít pomocí prostředí PowerShell rozšíření pro Visual Studio Code

- Visual Studio Code: [rozšíření prostředí PowerShell][ps-extension]
- [Zápis a ladění skriptů prostředí PowerShell v kódu Visual Studio][debug]
- [Ladění v sadě Visual Studio Code pokyny][vscode-guide]
- [Ladění prostředí PowerShell v sadě Visual Studio kódu][ps-vscode]
- [Začínáme s vývojem pro prostředí PowerShell v kódu Visual Studio][getting-started]
- [Visual Studio Code úpravy funkce pro vývoj prostředí PowerShell – část 1][editing-part1]
- [Visual Studio Code úpravy funkce pro vývoj prostředí PowerShell – část 2][editing-part2]
- [Ladění skriptu prostředí PowerShell v kódu Visual Studio – část 1][debugging-part1]
- [Ladění skriptu prostředí PowerShell v kódu Visual Studio – část 2][debugging-part2]

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

## <a name="powershell-extension-for-visual-studio-code"></a>Rozšíření prostředí PowerShell pro Visual Studio Code

Rozšíření prostředí PowerShell zdrojový kód najdete na [Githubu](https://github.com/PowerShell/vscode-powershell).
