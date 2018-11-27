---
ms.date: 08/24/2018
keywords: rutiny prostředí PowerShell
title: Učení powershellových názvů
ms.assetid: b4d0fd22-8298-4ee6-82ae-9b6f2907c986
ms.openlocfilehash: 6ed1f99513f00c174147876e1982c0d12869cacb
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320478"
---
# <a name="learning-powershell-names"></a>Učení powershellových názvů

Učení názvů příkazů a parametry vyžaduje spoustu času investici se většina rozhraní příkazového řádku. Problém je, že existuje několik vzorových postupů. Zapamatování je jediný způsob, jak další příkazy a parametry, které je třeba použít v pravidelných intervalech.

Při práci s nový příkaz nebo parametr vždy nelze použít, co už znáte. Je nutné najít a zjistěte, nový název. Rozhraní příkazového řádku tradičně, začněte s malou sadu nástrojů a růst s přírůstkové doplňky. Je snadno zjistit proto neexistuje žádný standardní struktury.
Vypadá to, že logické pro názvy příkazů vzhledem k tomu, že každý příkaz je samostatný nástroj. Prostředí PowerShell má lepší způsob, jak zpracovat názvy příkazů.

## <a name="learning-command-names-in-traditional-shells"></a>Učení názvů příkazů v tradiční prostředí

Většina příkazů se za účelem správy prvky operačních systémech a aplikacích, jako je například služeb nebo procesů. Příkazy mají názvy, které můžou nebo nemusí vejde do rodiny. Například v systémech Windows, můžete použít `net start` a `net stop` příkazy ke spuštění a zastavení služby. **Sc.exe** je jiný nástroj pro ovládací prvek služby pro Windows. Tento název se nevejde do vzor pojmenování **net.exe** služby příkazy. Pro řízení procesů, má Windows **tasklist.exe** příkaz listovat procesy a **taskkill.exe** příkazu ukončit.

Tyto příkazy mají navíc specifikace nestandardní parametru. Nelze použít `net start` příkaz pro spuštění služby ve vzdáleném počítači. **Sc.exe** příkaz službu můžete spustit na vzdáleném počítači. Ale pokud chcete zadat vzdálený počítač, musíte přidat předponu stejný název jako dvojité zpětné lomítko. Chcete-li spustit službu zařazování tisku ve vzdáleném počítači s názvem DC01, zadejte `sc.exe \\DC01 start spooler`.
Do seznamu Úkoly spuštěné v DC01 použijete **/S** parametr a název počítače bez zpětná lomítka. Například `tasklist /S DC01`.

> [!NOTE]
> Před Powershellu v6 `sc` se alias pro `Set-Content` rutiny. Ke spuštění **sc.exe** příkaz, musí obsahovat příponu souboru.

Příklady prvků spravovat počítače, které mají jasně definovaných životní cykly jsou služby a procesy. Můžete spustit nebo zastavit služby a procesy nebo získat seznam všech aktuálně spuštěné služby nebo procesy. I když existují důležité technické rozdíly mezi nimi, akce, které můžete provádět na službách a procesy jsou koncepčně stejné. Kromě toho volby, které provedeme přizpůsobit tak, že zadáte parametry akce může být koncepčně podobné také.

Powershellu zneužívá tyto podobnosti a snížit počet různých názvů, potřebujete pochopit a používat rutiny.

## <a name="cmdlets-use-verb-noun-names-to-reduce-command-memorization"></a>Rutiny využít k omezení příkaz zapamatování názvy sloveso-podstatné jméno

Prostředí PowerShell používá systém pojmenování "sloveso-podstatné jméno". Každý název rutiny se skládá z standardní operace dělení s konkrétní podstatné jméno. Příkazy prostředí PowerShell nejsou vždy anglické příkazy, ale jejich expresní určitých akcí v prostředí PowerShell. S podstatnými jmény jsou velmi podobně jako podstatná jména v jakémkoli jazyce. Popisují konkrétní typy objektů, které jsou důležité pro správu systému. Je snadné ukazují, jak tyto názvy dvou částí úsilí learning pohledem na několik příkladů.

PowerShell je doporučená sada standardních operací. Podstatná jména jsou méně s omezeným přístupem, ale vždy popisují příkaz postupuje podle. Prostředí PowerShell, jako má příkazy `Get-Process`, `Stop-Process`, `Get-Service`, a `Stop-Service`.

Tento příklad dvou podstatná jména a příkazy konzistence není zjednodušit učení této snazší. Rozšíření seznamu standardizované sadu 10 příkazy a 10 podstatná jména. Nyní máte jenom 20 slova, která chcete pochopit.
Ale tato slova mohou být kombinovány pro názvy formuláře 100 různých příkazů.

Je snadno pochopit, co dělá příkaz prostředí PowerShell najdete jeho název. Vypnout počítač pomocí příkazu `Stop-Computer`. Seznam všech počítačů v síti pomocí příkazu `Get-Computer`. Pomocí příkazu získat systémové datum `Get-Date`.

Můžete zobrazit seznam všech příkazů, které obsahují konkrétní operaci s **příkaz** parametr pro `Get-Command`. Například, pokud chcete zobrazit všechny rutiny, které používají příkaz `Get`, typ:

```
PS> Get-Command -Verb Get

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Get-Acl                         Get-Acl [[-Path] <String[]>]...
Cmdlet          Get-Alias                       Get-Alias [[-Name] <String[]...
Cmdlet          Get-AuthenticodeSignature       Get-AuthenticodeSignature [-...
Cmdlet          Get-ChildItem                   Get-ChildItem [[-Path] <Stri...
...
```

Použití **podstatné jméno** parametr zobrazíte řadu příkazů, které mají vliv stejný typ objektu. Například spusťte následující příkaz zobrazí příkazy, které jsou k dispozici pro správu služeb:

```
PS> Get-Command -Noun Service

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Get-Service                     Get-Service [[-Name] <String...
Cmdlet          New-Service                     New-Service [-Name] <String>...
Cmdlet          Restart-Service                 Restart-Service [-Name] <Str...
Cmdlet          Resume-Service                  Resume-Service [-Name] <Stri...
Cmdlet          Set-Service                     Set-Service [-Name] <String>...
Cmdlet          Start-Service                   Start-Service [-Name] <Strin...
Cmdlet          Stop-Service                    Stop-Service [-Name] <String...
Cmdlet          Suspend-Service                 Suspend-Service [-Name] <Str...
...
```

## <a name="cmdlets-use-standard-parameters"></a>Rutiny používají standardní parametry

Jak bylo uvedeno dříve, příkazech použitých v tradiční rozhraní příkazového řádku vždy mají názvy parametrů konzistentní vzhledem k aplikacím. Parametry jsou často jedním znakem nebo se používá zkratka slova, která se dají snadno na typ, ale nejsou snadno srozumitelné pro nové uživatele.

Na rozdíl od většina jiných tradiční rozhraní příkazového řádku Powershellu přímo zpracovává parametrů a používá tento přímý přístup k parametrům společně s pokyny pro vývojáře ke standardizaci názvy parametrů. Tyto doprovodné materiály může vést ke vzniku, ale nezaručuje, že každou rutinu odpovídá standardu.

Prostředí PowerShell také standardizuje parametr oddělovače. Názvy parametrů mít vždy "-" před pomocí příkazu prostředí PowerShell. Vezměte v úvahu v následujícím příkladu:

```powershell
Get-Command -Name Clear-Host
```

Název parametru je **název**, ale je typovaný jako `-Name` při použití v příkazovém řádku jako parametr.

Tady jsou některé obecné charakteristiky standardní parametr názvy a použití.

### <a name="the-help-parameter-"></a>Parametr nápovědy (?)

Pokud zadáte `-?` parametru u libovolné rutiny prostředí PowerShell zobrazí nápovědu pro rutinu.
Rutina není spuštěn.

### <a name="common-parameters"></a>Společné parametry

Prostředí PowerShell víme o několika *společné parametry*. Tyto parametry se řídí modul prostředí PowerShell. Společné parametry vždy chovají stejným způsobem. Společné parametry jsou **WhatIf**, **potvrdit**, **Verbose**, **ladění**, **upozornit**, **ErrorAction**, **ErrorVariable**, **OutVariable**, a **OutBuffer**.

### <a name="recommended-parameter-names"></a>Názvy parametrů doporučené

Rutiny prostředí PowerShell core použít standardní názvy pro podobně jako parametry. Použijte tyto standardní názvy nevynucuje, ale neexistuje explicitní pokyny, které podpořit standardizaci.

Doporučený název parametru, který odkazuje na počítači je třeba, **ComputerName**, nikoli serveru, hostitele, System, uzel nebo Další běžnou alternativou. Další důležité doporučené parametr názvy jsou **platnost**, **vyloučit**, **zahrnout**, **PassThru**, **cesta**, a **CaseSensitive**.
