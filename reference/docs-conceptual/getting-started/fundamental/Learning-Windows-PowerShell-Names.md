---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Učení názvů Windows PowerShellu
ms.assetid: b4d0fd22-8298-4ee6-82ae-9b6f2907c986
ms.openlocfilehash: 381aa619a41ccacb2ff3a4cdbc2b75b7f04282d1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="learning-windows-powershell-names"></a>Učení názvů Windows PowerShellu
Learning názvy příkazů a parametry příkazu je déle investice s Většina rozhraní příkazového řádku. Problém je, že v případě vzorů velmi málo tak, aby jediný způsob, jak další používáním každý příkaz a každý parametr, který je nutné použít v pravidelných intervalech.

Při práci s parametry a nový příkaz, nemůžete použít obecně co již víte; budete muset najít a další nový název. Pokud se podíváte na tom, jak rozhraní dosáhnout z malého nástrojů s přírůstkové přídavky funkce, je snadno zjistit, proč je nestandardní strukturu. S názvy příkazů konkrétně to může zvukových logické vzhledem k tomu, že každý příkaz je samostatný nástroj, ale je lepší způsob, jak zpracovat názvy příkazů.

Většina příkazů využívají ke správě prvky operačního systému nebo aplikace, jako je například služeb nebo procesů. Příkazy mít různé názvy, které může nebo nemusí začlenit do rodinu. V systémech Windows, například můžete použít **net start** a **net stop** příkazů pro spuštění a zastavení služby. Neexistuje jiný více zobecněný nástroj service ovládací prvek pro Windows, který má úplně jiný název, **sc**, který se nevejde do vzoru pro pojmenovávání pro **net** služby příkazy. Pro proces správy systému Windows má **tasklist** příkaz seznamu procesy a **taskkill** příkaz ukončit procesy.

Příkazy, které provést parametry mají specifikace nestandardní parametru. Nelze použít **net start** příkaz ke spuštění služby ve vzdáleném počítači. **Sc** příkazu spustí službu ve vzdáleném počítači, ale pokud chcete zadat vzdálený počítač, musíte přidat předponu názvu s dvojité zpětné lomítko. Například spusťte službu zařazování tisku ve vzdáleném počítači s názvem DC01, zadali byste **sc \\ \\DC01 spustit zařazování**. Do seznamu úloh spuštěných na DC01, budete muset použít **/S** parametr (pro "systém") a zadejte název DC01 bez zpětná lomítka takto: **tasklist /S DC01**.

I když jsou důležité technické rozdíly mezi službou a proces, jsou obě příklady spravovat elementů v počítači, které mají dobře definovaný životní cyklus. Můžete se ke spuštění nebo zastavení služby nebo proces nebo získat seznam všech aktuálně spuštěných služeb nebo procesů. Jinými slovy i když služba a proces jsou různých věcí, akce, které se provádí na službu nebo proces jsou často koncepčně stejné. Kromě toho výběry, které můžeme provést akce přizpůsobit tak, že zadáte parametry může být koncepčně podobá také.

Prostředí Windows PowerShell zneužije tyto podobnosti a snížit počet různých názvů, je nutné znát pochopit a používat rutiny.

### <a name="cmdlets-use-verb-noun-names-to-reduce-command-memorization"></a>Použití rutiny sloveso-podstatné jméno názvy ke snížení Memorization příkaz
Prostředí Windows PowerShell používá pojmenování systému "sloveso-podstatné jméno", kde každý název rutiny se skládá z standardní operaci s pomlčkami s konkrétní podstatné jméno. Příkazy prostředí Windows PowerShell nejsou vždy anglické příkazy, ale jejich express určitých akcí v prostředí Windows PowerShell. Podstatná jména jsou hodně podobá podstatná jména v jakémkoli jiném jazyce, popisují konkrétní typy objektů, které jsou důležité v systému správy. Je snadné ukazují, jak tyto dvě části názvy snížit learning úsilí prohlížením několik příkladů příkazy a podstatná jména.

Podstatná jména jsou méně s omezeným přístupem, ale vždy měli popisují, co příkaz funguje na. Prostředí Windows PowerShell obsahuje příkazy, jako **Get-Process**, **Stop-Process**, **Get-Service**, a **Stop-Service**.

V případě dvě podstatná jména a dva příkazy konzistence není zjednodušit, že velmi učení. Pokud se podíváte na standardní sadu 10 příkazy a 10 podstatná jména, ale budete mít jenom 20 slova pochopit, ale tato slova lze použít k vytvoření 100 příkaz odlišné názvy.

Často poznáte příkaz jaké načtením jeho název a je obvykle zřejmá, zadejte název by měl být použito pro nový příkaz. Příkaz pro vypnutí počítače může být například **Stop-Computer**. Příkaz, který obsahuje seznam všech počítačů v síti může být **Get-Computer**. Příkaz, který získá systémové datum je **Get-Date**.

Můžete vytvořit seznam všechny příkazy, které obsahují konkrétní operaci s **-příkaz** parametr pro **Get-Command** (se budeme zabývat **Get-Command** podrobně v další části). Například pokud chcete zobrazit všechny rutiny, které používají příkaz **získat**, zadejte:

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

**-Podstatné jméno** parametr jsou i další užitečné, protože umožňuje najdete řadu příkazů, které ovlivňují stejný typ objektu. Například pokud chcete zobrazit příkazy, které jsou k dispozici pro správu služeb, zadejte následující příkaz:

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

Příkaz není nutně rutiny, stačí, protože obsahuje schéma pojmenování sloveso-podstatné jméno. Příkladem nativní příkaz prostředí Windows PowerShell, který není rutina, ale má název sloveso-podstatné jméno, je příkaz vymazání okna konzoly, Clear-Host. Příkaz Clear-hostitel je ve skutečnosti funkci interního, jak je vidět, pokud je u ní spustit Get-Command:

```
PS> Get-Command -Name Clear-Host

CommandType     Name                            Definition
-----------     ----                            ----------
Function        Clear-Host                      $spaceType = [System.Managem...
```

### <a name="cmdlets-use-standard-parameters"></a>Použití rutiny standardní parametry
Jak již bylo uvedeno dříve, funkce použité v tradiční rozhraní příkazového řádku nemají obecně názvy parametrů konzistentní. Někdy parametry nemají názvy vůbec. Pokud tomu tak je, jsou často o délce jednoho znaku nebo se používá zkratka slova, která lze rychle zadat, ale nejsou snadno pochopitelné nové uživatele.

Na rozdíl od většině ostatních tradiční rozhraní příkazového řádku prostředí Windows PowerShell zpracovává parametry přímo a použije tento přímý přístup k parametrům spolu s pokyny pro vývojáře pro standardizaci názvy parametrů. I když to není zaručeno, že každou rutinu bude vždy odpovídají standardům, doporučte ho.

> [!NOTE]
> Názvy parametrů doposud '-' přidá jako předpona k nim při použití, aby prostředí Windows PowerShell je jasně označuje jako parametry. V **Get-Command - název Clear-Host** například název parametru je **název**, ale je zadán jako -**název**.

Zde jsou některé obecné vlastnosti standardní parametr názvy a použití.

#### <a name="the-help-parameter-"></a>Parametr nápovědy (?)
Pokud zadáte **-?** parametr pro všechny rutiny, rutina není proveden. Místo toho prostředí Windows PowerShell zobrazí nápovědu pro rutinu.

#### <a name="common-parameters"></a>Společné parametry
Prostředí Windows PowerShell obsahuje několik parametrů, které jsou známé jako *společné parametry*. Protože tyto parametry jsou řízeny modul prostředí Windows PowerShell, vždy, když jsou implementované rutiny, budou se chovat vždy stejným způsobem. Společné parametry jsou **WhatIf**, **potvrdit**, **podrobné**, **ladění**, **varování**, **ErrorAction**, **ErrorVariable**, **OutVariable**, a **OutBuffer**.

#### <a name="suggested-parameters"></a>Navrhované parametry
Základní rutiny Windows Powershellu používat standardní názvy pro podobné parametry. I když není vynucené použití názvy parametrů, je explicitní pokyny pro použití na podporu standardizace.

Například pokyny doporučuje pojmenování parametr, který odkazuje na počítači podle názvu jako **ComputerName**, nikoli serveru, hostitele, systému, uzel nebo jiná běžné alternativní slova. Mezi důležité navrhované parametr názvů **Force**, **vyloučit**, **zahrnout**, **PassThru**, **cesta**, a **CaseSensitive**.