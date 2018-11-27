---
title: Pomocí Visual Studio Code pro vývoj v prostředí PowerShell
description: Pomocí Visual Studio Code pro vývoj v prostředí PowerShell
ms.date: 08/06/2018
ms.openlocfilehash: 6433a875c233283f94d70c7acd7d394c73029b6d
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320444"
---
# <a name="using-visual-studio-code-for-powershell-development"></a>Pomocí Visual Studio Code pro vývoj v prostředí PowerShell

Kromě [prostředí PowerShell ISE][ise], prostředí PowerShell je také dobře podporované ve Visual Studio Code.
Kromě toho ISE nepodporuje pomocí prostředí PowerShell Core, i když Visual Studio Code podporuje prostředí PowerShell Core na všech platformách (Windows, macOS a Linux)

Můžete použít Visual Studio Code ve Windows pomocí prostředí PowerShell verze 5 s použitím Windows 10 nebo po instalaci [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) pro nižší úrovně OSs Windows (např. Windows 8.1, atd.).

Před jeho zahájením, ujistěte se prosím, že prostředí PowerShell v systému existuje.
Pro moderní úlohy ve Windows, macOS a Linuxu naleznete v tématu:

- [Instalace Powershellu Core v Linuxu][install-pscore-linux]
- [Instalace Powershellu Core v macOS][install-pscore-macos]
- [Instalace Powershellu Core ve Windows][install-pscore-windows]

Pro tradiční úlohy v prostředí Windows PowerShell najdete v článku [instalace prostředí Windows PowerShell][install-winps].

## <a name="editing-with-visual-studio-code"></a>Úpravy ve Visual Studiu Code

### <a name="1-installing-visual-studio-codehttpscodevisualstudiocomdocssetupsetup-overview"></a>[1. Instalace Visual Studio Code](https://code.visualstudio.com/Docs/setup/setup-overview)

- **Linux**: postupujte podle pokynů k instalaci na [spuštění VS Code na Linuxu](https://code.visualstudio.com/docs/setup/linux) stránky

- **macOS**: postupujte podle pokynů k instalaci na [spuštění VS Code na macOS](https://code.visualstudio.com/docs/setup/mac) stránky

  > [!IMPORTANT]
  > V systému macOS musíte nainstalovat OpenSSL pro rozšíření prostředí PowerShell správně fungovat.
  > Nejjednodušší způsob, jak to provést, je instalace [Homebrew](https://brew.sh/) a pak spusťte `brew install openssl`.
  > VS Code teď možné úspěšně načíst rozšíření prostředí PowerShell.

- **Windows**: postupujte podle pokynů k instalaci na [spuštění VS Code na Windows](https://code.visualstudio.com/docs/setup/windows) stránky

### <a name="2-installing-powershell-extension"></a>2. Instaluje se rozšíření Powershellu

- Spuštění sady Visual Studio Code aplikaci:
  - **Windows**: psaní `code` v relaci prostředí PowerShell
  - **Linux**: psaní `code` v terminálu
  - **macOS**: psaní `code` v terminálu

- Spuštění **okno rychlého otevření** stisknutím kombinace kláves **Ctrl + P** (**Cmd + P** na počítači Mac).
- Okno rychlého otevření zadejte `ext install powershell` a přístupů **Enter**.
- **Rozšíření** na bočním panelu otevře se zobrazení. Vyberte rozšíření prostředí PowerShell od Microsoftu.
  By měl vypadat přibližně jako následující:

  ![VSCode](../../images/vscode.png)

- Klikněte na tlačítko **nainstalovat** tlačítko na rozšíření prostředí PowerShell od Microsoftu.
- Po instalaci, zobrazí **nainstalovat** tlačítko se změní **Reload**.
  Klikněte na **Reload**.
- Poté, co Visual Studio Code má nové načtení, jste připraveni pro úpravy.

Například chcete-li vytvořit nový soubor, klikněte na tlačítko **soubor -> Nový**.
Pokud chcete uložit, klikněte na tlačítko **soubor -> Uložit** a pak zadejte název souboru, Pojďme Dejme tomu, že `HelloWorld.ps1`.
Zavřete soubor, klikněte na "x" vedle jeho názvu.
Chcete-li ukončit Visual Studio Code, **soubor -> ukončení**.

#### <a name="using-a-specific-installed-version-of-powershell"></a>Pomocí konkrétní nainstalovanou verzi prostředí PowerShell

Pokud chcete použít konkrétní instalaci prostředí PowerShell pomocí Visual Studio Code, budete muset do souboru nastavení uživatele přidejte novou proměnnou.

1. Klikněte na tlačítko **soubor -> Předvolby -> Nastavení**
1. Zobrazí se dvě podokna editoru.
   V podokně úplně vpravo (`settings.json`), vložte níže uvedené nastavení vhodná pro váš operační systém někde mezi dva složené závorky (`{` a `}`) a nahraďte **\<verze\>** s nainstalovanou verzí Powershellu:

   ```json
    // On Windows:
    "powershell.powerShellExePath": "c:/Program Files/PowerShell/<version>/pwsh.exe"

    // On Linux:
    "powershell.powerShellExePath": "/opt/microsoft/powershell/<version>/pwsh"

    // On macOS:
    "powershell.powerShellExePath": "/usr/local/microsoft/powershell/<version>/pwsh"
   ```

1. Nahraďte cestou do požadovaného Powershellu spustitelný soubor nastavení
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

## <a name="debugging-with-visual-studio-code"></a>Ladění ve Visual Studiu Code

### <a name="no-workspace-debugging"></a>Ladění žádný pracovní prostor

Od verze Visual Studio Code 1.9 můžete ladit skripty Powershellu bez nutnosti otevřít složku, která obsahuje skript prostředí PowerShell.
Jednoduše otevřete soubor skriptu Powershellu pomocí **soubor -> Otevřít soubor...** , nastavte zarážku na řádku (stiskněte klávesu F9) a potom stiskněte klávesu F5 pro spuštění ladění.
Měli byste vidět podokna akcí ladění se zobrazí, které umožňuje proniknout do ladicího programu, krok, obnovit a Zastavit ladění.

### <a name="workspace-debugging"></a>Ladění pracovního prostoru

Pracovní prostor ladění odkazuje na ladění v rámci složky, kterou jste otevřeli pomocí Visual Studio Code **otevřít složku...**  z **souboru** nabídky.
Otevření složky je obvykle složky projektu Powershellu a/nebo kořenu úložiště Git.

I v tomto režimu ladění lze spustit vybrané skript Powershellu jednoduše stisknutím klávesy F5.
Ale ladění pracovního prostoru můžete zadat ladění konfigurací s víc než jenom ladění aktuálně otevřený soubor.
Můžete například přidat konfigurace, které:

- Spusťte testy Pester v ladicím programu
- Spuštění konkrétního souboru s argumenty v ladicím programu
- Spustit interaktivní relaci v ladicím programu
- Připojit ladicí program k procesu hostitele prostředí PowerShell

Postupujte podle těchto kroků můžete vytvořit konfigurační soubor ladění:

  1. Otevřít **ladění** zobrazit stisknutím klávesy **Ctrl + Shift + D** (**Cmd + Shift + D** na počítači Mac).
  2. Stisknutím klávesy **konfigurovat** ikonu ozubeného kolečka v panelu nástrojů.
  3. Visual Studio Code vás vyzve, abyste **vyberte prostředí**. Zvolte **Powershellu**.

  Když toto provedete, Visual Studio Code vytvoří adresář a soubor ".vscode\launch.json" v kořenovém adresáři vašeho pracovního prostoru.
  Toto je ukládat konfiguraci ladění. Pokud jsou vaše soubory v úložišti Git, obvykle chcete potvrdit souboru launch.json.
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
  Ale při otevření tohoto souboru v editoru, se zobrazí **Přidat konfiguraci...**  tlačítko.
  Toto tlačítko pro přidání další konfiguraci ladění Powershellu. Je jedna po ruce konfigurace k přidání **prostředí PowerShell: Spusťte skript**.
  S touto konfigurací můžete zadat konkrétní soubor s volitelné argumenty, které má být spuštěna vždy, když stisknete klávesu F5, bez ohledu na to soubor, který je právě aktivní v editoru.

  Jakmile se naváže konfiguraci ladění, můžete vybrat konfiguraci, kterou chcete použít během relace ladění výběrem jedné z rozevíracího seznamu v konfiguraci ladění **ladění** nástrojů pro zobrazení.

Existuje několik blogy, které mohou být užitečné, které vám pomůžou začít pomocí rozšíření prostředí PowerShell pro Visual Studio Code:

- [Rozšíření prostředí PowerShell][ps-extension]
- [Programujte a laďte Powershellových skriptů v aplikaci Visual Studio Code][debug]
- [Ladění v sadě Visual Studio Code pokyny][vscode-guide]
- [Ladění v prostředí PowerShell ve službě Visual Studio Code][ps-vscode]
- [Začínáme s vývojem Powershellu ve Visual Studio Code][getting-started]
- [Visual Studio Code úpravy funkce pro vývoj Powershellu – část 1][editing-part1]
- [Visual Studio Code úpravy funkce pro vývoj Powershellu – část 2][editing-part2]
- [Ladění skriptů Powershellu v aplikaci Visual Studio Code – část 1][debugging-part1]
- [Ladění skriptů Powershellu v aplikaci Visual Studio Code – část 2][debugging-part2]

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

## <a name="powershell-extension-for-visual-studio-code"></a>Rozšíření prostředí PowerShell pro Visual Studio Code

Rozšíření prostředí PowerShell zdrojový kód můžete najít na [Githubu](https://github.com/PowerShell/vscode-powershell).
