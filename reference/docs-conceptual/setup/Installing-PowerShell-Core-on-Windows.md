# <a name="installing-powershell-core-on-windows"></a>Instalace PowerShellu Core ve Windows

## <a name="msi"></a>MSI

K instalaci prostředí PowerShell na Windows serveru nebo klienta Windows (funguje na Server 2008 R2, Windows 7 SP1 a novější), stáhněte si balíček Instalační služby MSI z našich Githubu [uvolní][] stránky.

Soubor MSI vypadá takto- `PowerShell-6.0.0.<buildversion>.<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well -->

Po stažení poklikejte na instalační program a postupujte podle pokynů.

Je umístěn v nabídce Start po instalaci zástupce.

* Ve výchozím nastavení je balíček nainstalován do `$env:ProgramFiles\PowerShell\`
* Můžete spustit prostředí PowerShell pomocí nabídky Start nebo `$env:ProgramFiles\PowerShell\pwsh.exe`

### <a name="prerequisites"></a>Předpoklady

Pokud chcete povolit vzdálenou komunikaci prostředí PowerShell přes WSMan, musí být splněny následující požadavky:

* Nainstalujte [Universal C Runtime](https://www.microsoft.com/download/details.aspx?id=50410) na verze Windows starší než Windows 10.
  Je k dispozici prostřednictvím přímé stahování nebo Windows Update.
  Opravit plně (včetně volitelné balíčky), podporované systémy budou už máte to nainstalována.
* Nainstalovat Windows Management Framework (WMF) [4.0](https://www.microsoft.com/download/details.aspx?id=40855) nebo novější ([5.1](https://www.microsoft.com/download/details.aspx?id=54616)) v systému Windows 7 a Windows Server 2008 R2.

## <a name="zip"></a>ZIP

Prostředí PowerShell binární ZIP archivy umožňujících pokročilé scénáře nasazení.
Potřeba poznamenat, že při použití archivu ZIP, nebude získat kontrolu požadovaných součástí jako balíček Instalační služby MSI.
Proto, aby pro vzdálenou komunikaci přes WSMan fungovat správně v systému Windows verze starší než Windows 10, musíte zajistit [požadavky](#prerequisites) jsou splněny.

## <a name="deploying-on-nano-server"></a>Nasazení na Nano Server

Tyto pokyny předpokládají, že na bitovou kopii Nano Server je již spuštěna verze prostředí PowerShell a že má být vygenerováno [Nano Server Image Builder](https://technet.microsoft.com/windows-server-docs/get-started/deploy-nano-server).
Nano Server je "bezobslužných" operačního systému a nasazení binárních souborů jádra prostředí PowerShell může dojít, dvěma různými způsoby:

1. Offline – připojit virtuální pevný disk Nano Server a rozbalte obsah souboru zip do zvoleného umístění v rámci připojené image.
1. Online – přenos souboru zip přes relaci prostředí PowerShell a rozbalte ho do zvoleného umístění.

V obou případech budete potřebovat verze Windows 10 x64 Zip balíček a bude nutné ke spuštění příkazů v rámci instance prostředí PowerShell "Administrator".

### <a name="offline-deployment-of-powershell-core"></a>Offline nasazení jádra prostředí PowerShell

1. Rozbalte balíček do adresáře v rámci připojené image Nano Server pomocí nástroje vaše oblíbené zip.
1. Odpojení bitové kopie a spustit ho.
1. Připojte k instanci doručené pošty prostředí Windows PowerShell.
1. Postupujte podle pokynů pro vytvoření koncového bodu vzdálené komunikace pomocí [jiná instance technika](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).

### <a name="online-deployment-of-powershell-core"></a>Online nasazení jádra prostředí PowerShell

Následující postup vás provede nasazení jádra prostředí PowerShell pro spuštěnou instanci Nano Server a konfiguraci jeho vzdálený koncový bod.

* Připojte se k instanci doručené pošty prostředí Windows PowerShell

```powershell
$session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
```

* Zkopírujte soubor do instance Nano Server

```powershell
Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
```

* Zadejte relaci

```powershell
Enter-PSSession $session
```

* Extrahujte soubor Zip

```powershell
# Insert the appropriate version.
Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
```

* Pokud chcete založená na službě WSMan vzdálenou komunikaci, postupujte podle pokynů pro vytvoření koncového bodu vzdálené komunikace pomocí [jiná instance technika](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).

## <a name="instructions-to-create-a-remoting-endpoint"></a>Pokyny k vytvoření koncového bodu vzdálené komunikace

Prostředí PowerShell jádro podporuje protokol vzdálenou komunikaci prostředí PowerShell (PSRP) prostřednictvím služby WSMan a SSH. Další informace viz:

* [SSH vzdálenou komunikaci prostředí PowerShell jádra][ssh-remoting]
* [Vzdálená komunikace WSMan v prostředí PowerShell jádra][wsman-remoting]

## <a name="artifact-installation-instructions"></a>Pokyny k instalaci artefaktů

Publikujeme archiv s CoreCLR bity na každé položky konfigurace sestavení s [AppVeyor][].

## <a name="coreclr-artifacts"></a>Artefakty CoreCLR

* Stáhněte si balíček zip z **artefakty** kartě konkrétní sestavení.
* Soubor zip odblokovat: klikněte pravým tlačítkem v Průzkumníku souborů -> Vlastnosti -> zaškrtávací políčko -> odblokovat použít
* Extrahujte soubor zip do `bin` adresáře
* `./bin/pwsh.exe`

<!-- [download-center]: TODO -->
[uvolní]: https://github.com/PowerShell/PowerShell/releases
[signing]: ../../tools/Sign-Package.ps1
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md
[AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell