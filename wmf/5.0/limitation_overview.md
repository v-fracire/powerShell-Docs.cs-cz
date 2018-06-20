---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 4b006d2ac812abf1f281b6b4e382c2760f92a95c
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34186826"
---
# <a name="known-issues-and-limitations"></a>Známé problémy a omezení

<a name="powershell-shortcuts-are-broken-when-used-for-the-first-time"></a>Při prvním použití jsou přerušená zkratky prostředí PowerShell
------------------------------------------------------------

**Řešení:** proveďte jednu z následujících akcí:

1.  Klikněte pravým tlačítkem na zástupce prostředí PowerShell. Vyberte "Prostředí Windows PowerShell" ke spuštění v režimu bez zvýšených oprávnění.
2.  Klikněte pravým tlačítkem na zástupce prostředí PowerShell. Klikněte pravým tlačítkem na "Prostředí Windows PowerShell" a vyberte možnost "Spustit jako správce" ke spuštění v režimu zvýšené.

Po provedení výše uvedené operace, budou fungovat zástupce prostředí PowerShell. Tyto akce je nutné provést pouze jednou.


<a name="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7"></a>Moduly prostředí PowerShell a prostředků DSC hlásit chyby zásady spouštění v systému Windows 7
-------------------------------------------------------------------------------------
Ve Windows 7 může způsobit chyby oznámené o ExecutionPolicy používání modulů Powershellu a prostředků DSC.

**Řešení:** zásady spouštění nastaveny na RemoteSigned spuštěním následujícího příkazu v relaci prostředí PowerShell zvýšenými oprávněními (Spustit jako správce):

```powershell
Set-ExecutionPolicy RemoteSigned
```

<a name="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash"></a>Připojení k původní vzdálený koncový bod Exchange způsobí, že havárie
------------------------------------------------------------

Původní koncový bod Exchange přesměruje na nový koncový bod. Je chyby logice přesměrování této výsledky v havárie.

**Řešení:** připojit se přímo k nový koncový bod.


<a name="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2"></a>Funkce protokolování inventáře softwaru je chybně zastavena po instalaci WMF 5.0 na Windows Server 2012 R2
-------------------------------------------------------------------------------------------------------------

Při instalaci WMF 5.0 na Windows Server 2012 R2 a je již spuštěna SIL, funkce protokolování inventáře softwaru je chybně zastavena po instalaci.

**Řešení:** spusťte rutinu Start-SilLogging po instalaci WMF, protože proces instalace se zastaví errantly funkce protokolování inventáře softwaru.

<a name="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together"></a>Get-ChildItem nefunguje, pokud se společně používají - LiteralPath a - Recurse
--------------------------------------------------------------------------

Pokud název adresáře obsahuje neplatný zástupný znak, pak Get-ChildItem nebude vytváří očekávané výsledky v případě - LiteralPath i - Recurse používají společně.

**Řešení:** není ideální, ale aktuální řešení je k implementaci rekurze ve skriptu, místo spoléhají na rutinu.


<a name="sysprep-fails-after-wmf-50-installation"></a>Nástroj Sysprep selže po instalaci WMF 5.0
----------------------------------------

Existují dvě řešení tohoto problému v závislosti na verzi Windows serveru, kterou používáte.

**Řešení:**
- Pro systémy s operačním systémem **Windows Server 2008 R2**
  1. Otevřete Powershell jako správce
  2. Spusťte následující příkaz

  ```powershell
    Set-SilLogging –TargetUri https://BlankTarget –CertificateThumbprint 0123456789
  ```
  3. Spusťte příkaz a ignorovat chybu, že jsou správně.

  ```powershell
    Publish-SilData
   ```
  4. Odstranit soubory v adresáři \Windows\System32\Logfiles\SIL\

  ```powershell
    Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
  ```
  5. Nainstalujte všechny dostupné důležité aktualizace systému Windows a začít Sysyprep operace normálně.

- Pro systémy s operačním systémem **systému Windows Server 2012**
  1.    Nástroj Sysprep'd, přihlaste se jako správce položek po instalaci WMF 5.0 na serveru, aby se.
  2.    Zkopírujte Generize.xml z adresáře \Windows\System32\Sysprep\ActionFiles\ do umístění mimo adresář systému Windows, C:\ třeba.
  3.    Otevřete vaší kopie Generalize.xml programu Poznámkový blok.
  4.    Vyhledat a odstranit následující text, jednu instanci každého musí být odstraněn (nebudou se blíží konec dokumentu).

    ```
    <sysprepOrder order="0x3200"></sysprepOrder>
    <sysprepOrder order="0x3300"></sysprepOrder>
    ```

  5.    Uložit upravenou kopii Generalize.xml a zavřete soubor.
  6.    Otevřete příkazový řádek jako správce
  7.    Spusťte následující příkaz k převzetí vlastnictví souboru Generalize.xml ve složce system32:

    ```
    Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
    ```

  8.    Spusťte následující příkaz pro nastavení příslušných oprávnění u souboru:

    ```
    Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F
    ```
      * Odpovíte kladně příkazového řádku pro potvrzení.
      * Všimněte si, že `<AdministratorUserName>` by měla být nahrazená jiným uživatelským jménem, který je správce na počítači. Například "Administrator".

  9.    Zkopírujte soubor můžete upravit a uložit přes k adresáři Sysprep pomocí následujícího příkazu:

    ```
    xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
    ```
      * Odpovíte kladně přepsat (Všimněte si, že pokud je výzva k přepsání, Překontrolujte zadaná cesta).
      * Předpokládá, že vaše upravenou kopii Generalize.xml byla zkopírována do C:\.

  10.   Generalize.XML byla aktualizována s alternativní řešení. Spusťte nástroj Sysprep s povolenou možností generalizace.
