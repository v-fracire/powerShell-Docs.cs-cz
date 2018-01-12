# <a name="ws-management-wsman-remoting-in-powershell-core"></a>Vzdálenou komunikaci služby WS-Management (WSMan) v prostředí PowerShell jádra 

## <a name="instructions-to-create-a-remoting-endpoint"></a>Pokyny k vytvoření koncového bodu vzdálené komunikace

Balíček základní prostředí PowerShell pro systém Windows obsahuje WinRM modulu plug-in (`pwrshplugin.dll`) a také instalační skript (`Install-PowerShellRemoting.ps1`) v `$PSHome`.
Tyto soubory povolení přijímat příchozí připojení vzdáleného prostředí PowerShell v případě, že její koncový bod je zadán prostředí PowerShell.

### <a name="motivation"></a>Motivace

Instalace prostředí PowerShell můžete vytvořit relace prostředí PowerShell vzdálených počítačů pomocí `New-PSSession` a `Enter-PSSession`.
Povolit příjem příchozích připojení vzdáleného prostředí PowerShell, musí uživatel vytvoření koncového bodu vzdálenou komunikaci služby WinRM.
Jedná se o explicitní výslovný souhlas scénář kde uživatel spustí instalaci PowerShellRemoting.ps1 se vytvořit koncový bod služby WinRM.
Instalační skript je krátkodobé řešení než přidáme další funkce `Enable-PSRemoting` provádět stejné akce.
Další podrobnosti najdete v tématu problém [#1193](https://github.com/PowerShell/PowerShell/issues/1193).

### <a name="script-actions"></a>Akce skriptu

Skript

1. Vytvoří adresář modulu plug-in v rámci %windir%\System32\PowerShell
1. Zkopíruje pwrshplugin.dll do tohoto umístění
1. Generuje konfiguračního souboru
1. Zaregistruje, který modul plug-in s WinRM

### <a name="registration"></a>Registrace

Skript je třeba spustit v relaci prostředí PowerShell na úrovni správce a běží ve dvou režimech.

#### <a name="executed-by-the-instance-of-powershell-that-it-will-register"></a>Provedený instance prostředí PowerShell, které se budou registrovat

``` powershell
Install-PowerShellRemoting.ps1
```

#### <a name="executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register"></a>Provedený jiná instance prostředí PowerShell jménem instanci, která se budou registrovat

``` powershell
<path to powershell>\Install-PowerShellRemoting.ps1 -PowerShellHome "<absolute path to the instance's $PSHOME>" -PowerShellVersion "<the powershell version tag>"
```

Například:

``` powershell
C:\Program Files\PowerShell\6.0.0.9\Install-PowerShellRemoting.ps1 -PowerShellHome "C:\Program Files\PowerShell\6.0.0.9\" -PowerShellVersion "6.0.0-alpha.9"
```

**Poznámka:** skript registrace vzdálené komunikace restartuje WinRM, tak všechny existující relace PSRP přeruší okamžitě po spuštění skriptu. Je-li spustit v průběhu vzdálené relace, to se ukončí připojení.

## <a name="how-to-connect-to-the-new-endpoint"></a>Jak se připojit k nový koncový bod

Vytvořte relaci prostředí PowerShell na nový koncový bod prostředí PowerShell zadáním `-ConfigurationName "some endpoint name"`. Připojit k instanci prostředí PowerShell z v předchozím příkladu, použijte buď:

``` powershell
New-PSSession ... -ConfigurationName "powershell.6.0.0-alpha.9"
Enter-PSSession ... -ConfigurationName "powershell.6.0.0-alpha.9"
```

Všimněte si, že `New-PSSession` a `Enter-PSSession` volání, které neurčují `-ConfigurationName` se zaměří na výchozí koncový bod prostředí PowerShell, `microsoft.powershell`.
