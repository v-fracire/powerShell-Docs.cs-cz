---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Opravy chyb v WMF 5.1
ms.openlocfilehash: 1e46d6d0419b3497450e6eaddbaa47456b004691
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="bug-fixes-in-wmf-51"></a><span data-ttu-id="dd055-103">Opravy chyb v WMF 5.1#</span><span class="sxs-lookup"><span data-stu-id="dd055-103">Bug Fixes in WMF 5.1#</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="dd055-104">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="dd055-104">Bug fixes</span></span> ##

<span data-ttu-id="dd055-105">Následující významné chyby budou opraveny v WMF 5.1:</span><span class="sxs-lookup"><span data-stu-id="dd055-105">The following notable bugs are fixed in WMF 5.1:</span></span>

### <a name="module-auto-discovery-fully-honors-envpsmodulepath"></a><span data-ttu-id="dd055-106">Automatické zjišťování modul plně ctí `$env:PSModulePath`</span><span class="sxs-lookup"><span data-stu-id="dd055-106">Module auto-discovery fully honors `$env:PSModulePath`</span></span> ###

<span data-ttu-id="dd055-107">Modul automatického zjišťování (načítání moduly automaticky bez explicitní Import-Module při volání příkazu) byla zavedená v WMF 3.</span><span class="sxs-lookup"><span data-stu-id="dd055-107">Module auto-discovery (loading modules automatically without an explicit Import-Module when calling a command) was introduced in WMF 3.</span></span>
<span data-ttu-id="dd055-108">Když se zavádí, prostředí PowerShell kontroluje pro příkazy v `$PSHome\Modules` před použitím `$env:PSModulePath`.</span><span class="sxs-lookup"><span data-stu-id="dd055-108">When introduced, PowerShell checked for commands in `$PSHome\Modules` before using `$env:PSModulePath`.</span></span>

<span data-ttu-id="dd055-109">WMF 5.1 změny tohoto chování respektovat `$env:PSModulePath` úplně.</span><span class="sxs-lookup"><span data-stu-id="dd055-109">WMF 5.1 changes this behavior to honor `$env:PSModulePath` completely.</span></span>
<span data-ttu-id="dd055-110">To umožňuje, aby uživatelem definovanou modul, který definuje příkazy dostupné prostředí PowerShell (například `Get-ChildItem`) automaticky-načíst a správně přepsání předdefinovaných příkaz.</span><span class="sxs-lookup"><span data-stu-id="dd055-110">This allows for a user-authored module that defines commands provided by PowerShell (e.g. `Get-ChildItem`) to be auto-loaded and correctly overriding the built-in command.</span></span>

### <a name="file-redirection-no-longer-hard-codes--encoding-unicode"></a><span data-ttu-id="dd055-111">Přesměrování souborů žádné delší pevně `-Encoding Unicode`</span><span class="sxs-lookup"><span data-stu-id="dd055-111">File redirection no longer hard-codes `-Encoding Unicode`</span></span> ###

<span data-ttu-id="dd055-112">V všechny předchozí verze prostředí PowerShell, nebylo možné vytvořit k řízení kódování souborů, které se používá operátor přesměrování souboru, například `Get-ChildItem > out.txt` vzhledem k tomu prostředí PowerShell přidá `-Encoding Unicode`.</span><span class="sxs-lookup"><span data-stu-id="dd055-112">In all previous versions of PowerShell, it was impossible to control the file encoding used by the file redirection operator, e.g. `Get-ChildItem > out.txt` because PowerShell added `-Encoding Unicode`.</span></span>

<span data-ttu-id="dd055-113">Od verze WMF 5.1, nyní můžete měnit kódování souborů přesměrování nastavením `$PSDefaultParameterValues`:</span><span class="sxs-lookup"><span data-stu-id="dd055-113">Starting with WMF 5.1, you can now change the file encoding of redirection by setting `$PSDefaultParameterValues`:</span></span>

```
$PSDefaultParameterValues["Out-File:Encoding"] = "Ascii"
```

### <a name="fixed-a-regression-in-accessing-members-of-systemreflectiontypeinfo"></a><span data-ttu-id="dd055-114">Pevné Regrese v přístup ke členům `System.Reflection.TypeInfo`</span><span class="sxs-lookup"><span data-stu-id="dd055-114">Fixed a regression in accessing members of `System.Reflection.TypeInfo`</span></span> ###

<span data-ttu-id="dd055-115">Regrese ve WMF 5.0 překročila přístupem členy `System.Reflection.RuntimeType`, například `[int].ImplementedInterfaces`.</span><span class="sxs-lookup"><span data-stu-id="dd055-115">A regression introduced in WMF 5.0 broke accessing members of `System.Reflection.RuntimeType`, e.g. `[int].ImplementedInterfaces`.</span></span>
<span data-ttu-id="dd055-116">V WMF 5.1 byl opraven této chyby.</span><span class="sxs-lookup"><span data-stu-id="dd055-116">This bug has been fixed in WMF 5.1.</span></span>


### <a name="fixed-some-issues-with-com-objects"></a><span data-ttu-id="dd055-117">Pevné některé problémy s objekty COM</span><span class="sxs-lookup"><span data-stu-id="dd055-117">Fixed some issues with COM objects</span></span> ###

<span data-ttu-id="dd055-118">WMF 5.0 zavedl nový vazač modelu COM pro vyvolání metody na objekty modelu COM a přístupu k vlastnosti objektů COM.</span><span class="sxs-lookup"><span data-stu-id="dd055-118">WMF 5.0 introduced a new COM binder for invoking methods on COM objects and accessing properties of COM objects.</span></span>
<span data-ttu-id="dd055-119">Tento nový vazač výrazné zlepšení výkonu, ale také zavedená některé chyby, které byly opraveny v WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="dd055-119">This new binder improved performance significantly but also introduced some bugs which have been fixed in WMF 5.1.</span></span>

#### <a name="argument-conversions-were-not-always-performed-correctly"></a><span data-ttu-id="dd055-120">Převody argumentů jste neprovedli vždy správně</span><span class="sxs-lookup"><span data-stu-id="dd055-120">Argument conversions were not always performed correctly</span></span> ####

<span data-ttu-id="dd055-121">V následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="dd055-121">In the following example:</span></span>

```
$obj = New-Object -ComObject WScript.Shell
$obj.SendKeys([char]173)
```

<span data-ttu-id="dd055-122">Metoda PředatKlávesovéÚhozy očekává řetězec, ale prostředí PowerShell nepřevádět char na řetězec, odložit převod volání metody IDispatch::Invoke., který používá VariantChangeType pro převod, který v tomto příkladu výsledkem místo odesílání klíče '1', '7' a '3. Očekávaný Volume.Mute klíče.</span><span class="sxs-lookup"><span data-stu-id="dd055-122">The SendKeys method expects a string, but PowerShell did not convert the char to a string, deferring the conversion to IDispatch::Invoke, which uses VariantChangeType to do the conversion, which in this example resulted in sending the keys '1', '7', and '3' instead of the expected Volume.Mute key.</span></span>

#### <a name="enumerable-com-objects-not-always-handled-correctly"></a><span data-ttu-id="dd055-123">Vyčíslitelná objekty modelu COM, ne vždy správně zpracovat.</span><span class="sxs-lookup"><span data-stu-id="dd055-123">Enumerable COM objects not always handled correctly</span></span> ####

<span data-ttu-id="dd055-124">Prostředí PowerShell obvykle vytvoří výčet většinu vyčíslitelná objektů, ale to Regrese ve WMF 5.0 nebylo možné provést výčet objektů COM, které implementují rozhraní IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="dd055-124">PowerShell normally enumerates most enumerable objects, but a regression introduced in WMF 5.0 prevented the enumeration of COM objects that implement IEnumerable.</span></span>  <span data-ttu-id="dd055-125">Příklad:</span><span class="sxs-lookup"><span data-stu-id="dd055-125">For example:</span></span>

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

<span data-ttu-id="dd055-126">V předchozím příkladu WMF 5.0 nesprávně napsali Scripting.Dictionary do kanálu místo vytváření výčtu páry klíč/hodnota.</span><span class="sxs-lookup"><span data-stu-id="dd055-126">In the above example, WMF 5.0 incorrectly wrote the Scripting.Dictionary to the pipeline instead of enumerating the key/value pairs.</span></span>

<span data-ttu-id="dd055-127">Tato změna také adresy [vydat 1752224 na Connect](https://connect.microsoft.com/PowerShell/feedback/details/1752224)</span><span class="sxs-lookup"><span data-stu-id="dd055-127">This change also addresses [issue 1752224 on Connect](https://connect.microsoft.com/PowerShell/feedback/details/1752224)</span></span>

### <a name="ordered-was-not-allowed-inside-classes"></a><span data-ttu-id="dd055-128">`[ordered]` nebylo možné použít uvnitř třídy</span><span class="sxs-lookup"><span data-stu-id="dd055-128">`[ordered]` was not allowed inside classes</span></span> ###

<span data-ttu-id="dd055-129">WMF 5.0 zavedl tříd pomocí ověření literály typu používat ve třídách.</span><span class="sxs-lookup"><span data-stu-id="dd055-129">WMF 5.0 introduced classes with validation of type literals used in classes.</span></span>
<span data-ttu-id="dd055-130">`[ordered]` vypadá jako literál typu, ale není pravda typ formátu .NET.</span><span class="sxs-lookup"><span data-stu-id="dd055-130">`[ordered]` looks like a type literal but is not a true .NET type.</span></span>
<span data-ttu-id="dd055-131">WMF 5.0 nesprávně oznámil chybu na `[ordered]` uvnitř třídy:</span><span class="sxs-lookup"><span data-stu-id="dd055-131">WMF 5.0 incorrectly reported an error on `[ordered]` inside a class:</span></span>

```
class CThing
{
    [object] foo($i)
    {
        [ordered]@{ Thing = $i }
    }
}
```


### <a name="help-on-about-topics-with-multiple-versions-does-not-work"></a><span data-ttu-id="dd055-132">Nápovědu k o tématech s více verzemi nefunguje.</span><span class="sxs-lookup"><span data-stu-id="dd055-132">Help on About topics with multiple versions does not work</span></span> ###

<span data-ttu-id="dd055-133">Před WMF 5.1, pokud jste měli více verzí modul nainstalovaný a všechny sdílené tématu nápovědy, například about_PSReadline, `help about_PSReadline` by vrátit několik témat jednoznačný způsob, jak zobrazit skutečné nápovědu.</span><span class="sxs-lookup"><span data-stu-id="dd055-133">Before WMF 5.1, if you had multiple versions of a module installed and they all shared a help topic, for example, about_PSReadline, `help about_PSReadline` would return multiple topics with no obvious way to view the real help.</span></span>

<span data-ttu-id="dd055-134">WMF 5.1 opravy to vrácením v nápovědě k nejnovější verzi tohoto tématu.</span><span class="sxs-lookup"><span data-stu-id="dd055-134">WMF 5.1 fixes this by returning the help for the latest version of the topic.</span></span>

<span data-ttu-id="dd055-135">`Get-Help` neposkytuje způsob, jak určit, která verze, který chcete zobrazit nápovědu pro.</span><span class="sxs-lookup"><span data-stu-id="dd055-135">`Get-Help` does not provide a way to specify which version you want help for.</span></span>
<span data-ttu-id="dd055-136">Chcete-li tento problém obejít, přejděte do adresáře modulů a prohlédněte si nápovědu přímo pomocí některého nástroje, například svém oblíbeném editoru.</span><span class="sxs-lookup"><span data-stu-id="dd055-136">To work around this, navigate to the modules directory and view the help directly with a tool like your favorite editor.</span></span>

### <a name="powershellexe-reading-from-stdin-stopped-working"></a><span data-ttu-id="dd055-137">čtení z stdin – PowerShell.exe nejsou funkční</span><span class="sxs-lookup"><span data-stu-id="dd055-137">powershell.exe reading from STDIN stopped working</span></span>

<span data-ttu-id="dd055-138">Zákazníci využívat `powershell -command -` z nativní aplikace provést prostředí PowerShell předání ve skriptu prostřednictvím STDIN bohužel to je přerušený kvůli jiné změny hostitele konzoly.</span><span class="sxs-lookup"><span data-stu-id="dd055-138">Customers use `powershell -command -` from native apps to execute PowerShell passing in the script via STDIN unfortunately this was broken due to other changes it the console host.</span></span>

https://windowsserver.uservoice.com/forums/301869-powershell/suggestions/15854689-powershell-exe-command-is-broken-on-windows-10

### <a name="powershellexe-creates-spike-in-cpu-usage-on-startup"></a><span data-ttu-id="dd055-139">PowerShell.exe vytvoří špička využití procesoru při spuštění</span><span class="sxs-lookup"><span data-stu-id="dd055-139">powershell.exe creates spike in CPU usage on startup</span></span>

<span data-ttu-id="dd055-140">PowerShell používá dotaz rozhraní WMI k zkontrolujte, zda byla spuštěna prostřednictvím zásad skupiny způsobovat zpoždění v přihlášení.</span><span class="sxs-lookup"><span data-stu-id="dd055-140">PowerShell uses a WMI query to check if it was started via Group Policy to avoid causing delay in login.</span></span>
<span data-ttu-id="dd055-141">Dotaz WMI bude nakonec vložení tzres.mui.dll do každého procesu v systému, protože třídy WMI Win32_Process pokusí načíst informace o místním časovém pásmu.</span><span class="sxs-lookup"><span data-stu-id="dd055-141">The WMI query ends up injecting tzres.mui.dll into every process on the system since the WMI Win32_Process class attempts to retrieve local timezone information.</span></span>
<span data-ttu-id="dd055-142">Výsledkem velké Špička procesoru v wmiprvse (hostitel zprostředkovatele rozhraní WMI).</span><span class="sxs-lookup"><span data-stu-id="dd055-142">This results in a large CPU spike in wmiprvse (the WMI provider host).</span></span>
<span data-ttu-id="dd055-143">Oprava je použití volání rozhraní API Win32 získání informací o stejné místo pomocí služby WMI.</span><span class="sxs-lookup"><span data-stu-id="dd055-143">Fix is to use Win32 API calls to get the same information instead of using WMI.</span></span>
