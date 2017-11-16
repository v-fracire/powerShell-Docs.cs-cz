---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Pomocí karty rozšíření"
ms.assetid: c8730471-bf6a-43b8-ab1d-f9ef5a74f04e
ms.openlocfilehash: 8412bd97a95719f07b16c6671d3b8801bbfab8e3
ms.sourcegitcommit: 4807ab554d55fdee499980835bcc279368b1df68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2017
---
# <a name="using-tab-expansion"></a>Pomocí karty rozšíření
Prostředí shell příkazového řádku často poskytují způsob, jak automaticky dokončit názvy dlouhé soubory nebo příkazy urychlení zadání příkazu a poskytuje. Prostředí Windows PowerShell umožňuje zadejte názvy souborů a rutiny stisknutím **kartě** klíč.

> [!NOTE]
> Vnitřní funkce TabExpansion nebo TabExpansion2 řídí karta rozšíření. Vzhledem k tomu, že tuto funkci můžete upravit nebo přepsat, je toto pojednání Průvodce chování výchozí konfigurace prostředí PowerShell.

Zadejte název souboru nebo cestu z dostupných možností automaticky, zadejte část názvu a stiskněte klávesu **kartě** klíč. Prostředí PowerShell bude automaticky rozbalte název na první shodu, která najde. Stisknutím **kartě** klíč opakovaně bude procházet všechny dostupné možnosti.

Karta rozšíření názvů rutiny se poněkud liší. K rozšíření karta na název rutiny, zadejte celý první část názvu (akce) a pomlčky, který následuje. Můžete vyplnit více název částečnou shodu. Pokud zadáte například **get-co** a potom stiskněte klávesu **kartě** klíče, prostředí PowerShell se automaticky rozšíří na **Get-Command** rutiny (Všimněte si, že změní také případě písmen jejich standardní formuláře). Pokud vyberete **kartě** klíče znovu, prostředí PowerShell nahradí to jenom jiné odpovídající název, **Get-Content**.

Karta rozšíření můžete opakovaně použít na stejném řádku. Například můžete použít kartu rozšíření na název **Get-Content** rutiny zadáním:

```
PS> Get-Con<Tab>
```

Po stisknutí klávesy **kartě** klíče, příkaz zasahuje do:

```
PS> Get-Content
```

Můžete pak částečně zadejte cestu k souboru protokolu aktivní instalace a použít karta rozšíření znovu:

```
PS> Get-Content c:\windows\acts<Tab>
```

Po stisknutí klávesy **kartě** klíče, příkaz zasahuje do:

```
PS> Get-Content C:\windows\actsetup.log
```

> [!NOTE]
> Jedním z omezení karta rozšíření procesu je, že jsou karty vždy vyhodnocena jako pokusy o dokončení slovo. Pokud je kopírujete a vkládáte příkladech do konzoly prostředí PowerShell, ujistěte se, že ukázku neobsahuje karty; Pokud ano, nepředvídatelné výsledky a nebude skoro určitě předpokladům.

