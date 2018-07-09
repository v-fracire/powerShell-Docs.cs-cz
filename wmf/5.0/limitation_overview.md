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
# <a name="known-issues-and-limitations"></a>Známé problémy a omezení

## <a name="powershell-shortcuts-are-broken-when-used-for-the-first-time"></a>Při prvním použití jsou přerušená klávesové zkratky prostředí PowerShell

**Řešení:** proveďte jeden z následujících akcí:

1. Klikněte pravým tlačítkem na zástupce Powershellu. Vyberte "Windows PowerShell" ke spuštění v režimu bez zvýšených oprávnění.
2. Klikněte pravým tlačítkem na zástupce Powershellu. Klikněte pravým tlačítkem myši klikněte na "Windows PowerShell" a vyberte spustit jako správce."ke spuštění v režimu se zvýšenými oprávněními.

Jakmile jste provedli jednu z výše uvedených akcí, bude fungovat klávesové zkratky prostředí PowerShell. Tato akce je nutné provést pouze jednou.

## <a name="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7"></a>Moduly Powershellu a prostředky DSC sestavy chyb o ExecutionPolicy ve Windows 7

Ve Windows 7 používání modulů Powershellu a prostředky DSC může vést k chybám o ExecutionPolicy.

**Řešení:** nastaveno ExecutionPolicy RemoteSigned spuštěním následujícího příkazu v relaci Powershellu se zvýšenými oprávněními (Spustit jako správce):

```powershell
Set-ExecutionPolicy RemoteSigned
```

## <a name="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash"></a>Připojení k staré vzdálený koncový bod serveru Exchange způsobí selhání

Staré koncový bod výměny přesměruje do nového koncového bodu. Je chyby logiky přesměrování této výsledky v chybovému ukončení.

**Řešení:** připojit přímo do nového koncového bodu.

## <a name="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2"></a>Funkce protokolování inventáře softwaru je chybně zastavena po instalaci WMF 5.0 v systému Windows Server 2012 R2

Při instalaci WMF 5.0 na Windows Server 2012 R2, která je již spuštěna SIL, funkce protokolování inventáře softwaru je chybně zastavena po instalaci.

**Řešení:** spusťte rutinu Start-SilLogging jednou po instalaci WMF, protože proces instalace se zastaví chybně funkce protokolování inventáře softwaru.

## <a name="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together"></a>`Get-ChildItem` Pokud se společně používají - LiteralPath a - Recurse nefunguje

Pokud název adresáře obsahuje neplatný zástupný znak, pak `Get-ChildItem` nevytvoří očekávané výsledky, když - LiteralPath i - Recurse se používají společně.

**Řešení:** není ideální, ale aktuální alternativním řešením je implementace rekurze ve skriptu, spíše než využívají rutiny.

## <a name="sysprep-fails-after-wmf-50-installation"></a>Nástroj Sysprep selže po instalaci WMF 5.0

Existují dvě alternativní řešení tohoto problému v závislosti na verzi Windows serveru.

**Řešení:**

- Pro systémy s operačním systémem **systému Windows Server 2008 R2**
  1. Otevřete Powershell jako správce
  2. Spuštěním následujícího příkazu

     ```powershell
     Set-SilLogging –TargetUri https://BlankTarget –CertificateThumbprint 0123456789
     ```

  3. Spusťte příkaz a ignorovat chybu, protože se očekává.

     ```powershell
     Publish-SilData
     ```

  4. Odstranit soubory v adresáři \Windows\System32\Logfiles\SIL\

     ```powershell
     Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
     ```

  5. Nainstalujte všechny dostupné důležité aktualizace Windows a zahájí operaci Sysyprep normálně.

- Pro systémy s operačním systémem **systému Windows Server 2012**
  1. Nástroj Sysprep'd, přihlaste se jako správce položek po instalaci WMF 5.0 na serveru.
  2. Zkopírujte Generize.xml z adresáře \Windows\System32\Sysprep\ActionFiles\ do umístění mimo adresář Windows, C:\ třeba.
  3. Otevřete kopii Generalize.xml programu Poznámkový blok.
  4. Vyhledat a odstranit následující text, jedna instance každé musí odstranit, (, bude u konce dokumentu).

     ```xml
     <sysprepOrder order="0x3200"></sysprepOrder>
     <sysprepOrder order="0x3300"></sysprepOrder>
     ```

  5. Uložit upravenou kopii Generalize.xml a zavřete soubor.
  6. Otevřete příkazový řádek jako správce
  7. Spusťte následující příkaz, který převzít vlastnictví Generalize.xml souboru ve složce system32:

     ```powershell
     Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

  8. Spuštěním následujícího příkazu nastavte příslušná oprávnění v souboru:

     ```powershell
     Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F
     ```

     - Odpovězte Ano do příkazového řádku pro potvrzení.
     - Všimněte si, že `<AdministratorUserName>` by měl být nahrazen uživatelským jménem, který je správcem na počítači. Například "Administrator".

  9. Zkopírujte soubor upravit a uložit přes do adresáře nástroje Sysprep pomocí následujícího příkazu:

     ```powershell
     xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml
     ```

     - Odpovězte Ano. Pokud chcete přepsat (Všimněte si, že pokud se nezobrazí žádný dotaz přepsat, pečlivě zkontrolujte zadaná cesta).
     - Předpokládá, že vaše upravenou kopii Generalize.xml byl zkopírován do C:\.

  10. Generalize.XML je teď aktualizovaný o alternativní řešení. Spusťte nástroj Sysprep s povolenou možností generalizace.