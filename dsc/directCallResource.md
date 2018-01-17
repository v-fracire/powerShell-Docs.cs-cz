---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Přímé volání metody prostředků DSC"
ms.openlocfilehash: 3e83984fbf31dfcfec76fa15cdd9b83d92501aa0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="calling-dsc-resource-methods-directly"></a>Přímé volání metody prostředků DSC

>Platí pro: Prostředí Windows PowerShell 5.0

Můžete použít [Invoke-DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx) rutiny volat přímo funkce nebo metody prostředek DSC ( **Get-TargetResource**, **Set-TargetResource**a  **Test-TargetResource** funkce na základě MOF prostředku, nebo **získat**, **nastavit**, a **Test** metody založené na třídě prostředku). Tímto lze třetích stran, které chcete použít prostředků DSC, nebo jako užitečné nástroje při vývoji prostředky. 

Tato rutina se obvykle používá v kombinaci s vlastností metakonfiguraci `refreshMode = 'Disabled'`, ale dá se používat bez ohledu na to, co **refreshMode** je nastaven na.

Při volání metody **Invoke-DscResource** rutiny, zadejte metody nebo funkce, která se pro volání **metoda** parametr. Zadejte vlastnosti prostředku předáním zatřiďovací tabulku jako hodnotu **vlastnost** parametr.

Následují příklady přímo volání metody prostředků:

## <a name="ensure-a-file-is-present"></a>Ujistěte se, že soubor existuje

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a>Otestovat, zda soubor existuje

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a>Získat obsah souboru

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

>**Poznámka:** přímo volání metody složené prostředků není podporováno. Místo toho volejte metody základní prostředky, které tvoří složené prostředků.

## <a name="see-also"></a>Viz také
- [Psaní vlastních prostředků DSC s MOF](authoringResourceMOF.md) 
- [Psaní vlastních prostředků DSC s třídami, prostředí PowerShell](authoringResourceClass.md)
- [Ladění prostředků DSC](debugResource.md)

