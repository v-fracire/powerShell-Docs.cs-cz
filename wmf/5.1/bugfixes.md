---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
title: Opravy chyb v WMF 5.1
ms.openlocfilehash: 137095f50f9f926d3488ff9c1ce8270ddbda63eb
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="bug-fixes-in-wmf-51"></a>Opravy chyb v WMF 5.1#

## <a name="bug-fixes"></a>Opravy chyb ##

Následující významné chyby budou opraveny v WMF 5.1:

### <a name="module-auto-discovery-fully-honors-envpsmodulepath"></a>Automatické zjišťování modul plně ctí`$env:PSModulePath` ###

Modul automatického zjišťování (načítání moduly automaticky bez explicitní Import-Module při volání příkazu) byla zavedená v WMF 3. Když se zavádí, prostředí PowerShell kontroluje pro příkazy v `$PSHome\Modules` před použitím `$env:PSModulePath`.

WMF 5.1 změny tohoto chování respektovat `$env:PSModulePath` úplně. To umožňuje, aby uživatelem definovanou modul, který definuje příkazy dostupné prostředí PowerShell (například `Get-ChildItem`) automaticky-načíst a správně přepsání předdefinovaných příkaz.

### <a name="file-redirection-no-longer-hard-codes--encoding-unicode"></a>Přesměrování souborů žádné delší pevně`-Encoding Unicode` ###

V všechny předchozí verze prostředí PowerShell, nebylo možné vytvořit k řízení kódování souborů, které se používá operátor přesměrování souboru, například `Get-ChildItem > out.txt` vzhledem k tomu prostředí PowerShell přidá `-Encoding Unicode`.

Od verze WMF 5.1, nyní můžete měnit kódování souborů přesměrování nastavením `$PSDefaultParameterValues`:

```
$PSDefaultParameterValues["Out-File:Encoding"] = "Ascii"
```

### <a name="fixed-a-regression-in-accessing-members-of-systemreflectiontypeinfo"></a>Pevné Regrese v přístup ke členům`System.Reflection.TypeInfo` ###

Regrese ve WMF 5.0 překročila přístupem členy `System.Reflection.RuntimeType`, například `[int].ImplementedInterfaces`.
V WMF 5.1 byl opraven této chyby.


### <a name="fixed-some-issues-with-com-objects"></a>Pevné některé problémy s objekty COM ###

WMF 5.0 zavedl nový vazač modelu COM pro vyvolání metody na objekty modelu COM a přístupu k vlastnosti objektů COM. Tento nový vazač výrazné zlepšení výkonu, ale také zavedená některé chyby, které byly opraveny v WMF 5.1.

#### <a name="argument-conversions-were-not-always-performed-correctly"></a>Převody argumentů jste neprovedli vždy správně ####

V následujícím příkladu:

```
$obj = New-Object -ComObject WScript.Shell
$obj.SendKeys([char]173)
```

Metoda PředatKlávesovéÚhozy očekává řetězec, ale prostředí PowerShell nepřevádět char na řetězec, odložit převod volání metody IDispatch::Invoke., který používá VariantChangeType pro převod, který v tomto příkladu výsledkem místo odesílání klíče '1', '7' a '3. Očekávaný Volume.Mute klíče.

#### <a name="enumerable-com-objects-not-always-handled-correctly"></a>Vyčíslitelná objekty modelu COM, ne vždy správně zpracovat. ####

Prostředí PowerShell obvykle vytvoří výčet většinu vyčíslitelná objektů, ale to Regrese ve WMF 5.0 nebylo možné provést výčet objektů COM, které implementují rozhraní IEnumerable.  Příklad:

```
function Get-COMDictionary
{
    $d = New-Object -ComObject Scripting.Dictionary
    $d.Add('a', 2)
    $d.Add('b', 2)
    return $d
}

$x = Get-COMDictionary
```

V předchozím příkladu WMF 5.0 nesprávně napsali Scripting.Dictionary do kanálu místo vytváření výčtu páry klíč/hodnota.

Tato změna také adresy [vydat 1752224 na Connect](https://connect.microsoft.com/PowerShell/feedback/details/1752224)

### <a name="ordered-was-not-allowed-inside-classes"></a>`[ordered]`nebylo možné použít uvnitř třídy ###

WMF 5.0 zavedl tříd pomocí ověření literály typu používat ve třídách.  
`[ordered]`vypadá jako literál typu, ale není pravda typ formátu .NET. WMF 5.0 nesprávně oznámil chybu na `[ordered]` uvnitř třídy:

```
class CThing
{
    [object] foo($i)
    {
        [ordered]@{ Thing = $i }
    }
}
```


### <a name="help-on-about-topics-with-multiple-versions-does-not-work"></a>Nápovědu k o tématech s více verzemi nefunguje. ###

Před WMF 5.1, pokud jste měli více verzí modul nainstalovaný a všechny sdílené tématu nápovědy, například about_PSReadline, `help about_PSReadline` by vrátit několik témat jednoznačný způsob, jak zobrazit skutečné nápovědu.

WMF 5.1 opravy to vrácením v nápovědě k nejnovější verzi tohoto tématu.

`Get-Help`neposkytuje způsob, jak určit, která verze, který chcete zobrazit nápovědu pro. Chcete-li tento problém obejít, přejděte do adresáře modulů a prohlédněte si nápovědu přímo pomocí některého nástroje, například svém oblíbeném editoru. 

### <a name="powershellexe-reading-from-stdin-stopped-working"></a>čtení z stdin – PowerShell.exe nejsou funkční

Zákazníci využívat `powershell -command -` z nativní aplikace provést prostředí PowerShell předání ve skriptu prostřednictvím STDIN bohužel to je přerušený kvůli jiné změny hostitele konzoly.

https://windowsserver.uservoice.com/forums/301869-PowerShell/Suggestions/15854689-PowerShell-exe-command-is-broken-on-Windows-10

### <a name="powershellexe-creates-spike-in-cpu-usage-on-startup"></a>PowerShell.exe vytvoří špička využití procesoru při spuštění

PowerShell používá dotaz rozhraní WMI k zkontrolujte, zda byla spuštěna prostřednictvím zásad skupiny způsobovat zpoždění v přihlášení.
Dotaz WMI bude nakonec vložení tzres.mui.dll do každého procesu v systému, protože třídy WMI Win32_Process pokusí načíst informace o místním časovém pásmu.
Výsledkem velké Špička procesoru v wmiprvse (hostitel zprostředkovatele rozhraní WMI).
Oprava je použití volání rozhraní API Win32 získání informací o stejné místo pomocí služby WMI.

