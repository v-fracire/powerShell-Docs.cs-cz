---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Přímé volání metod prostředku DSC
ms.openlocfilehash: cf237f638593706e5959e2bcc0d851b0e55baf0e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403659"
---
# <a name="calling-dsc-resource-methods-directly"></a>Přímé volání metod prostředku DSC

>Platí pro: Windows PowerShell 5.0

Můžete použít [Invoke-DscResource](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource) rutiny volat přímo funkcí nebo metod prostředku DSC ( **Get-TargetResource**, **Set-TargetResource**a  **Test-TargetResource** funkce prostředek založený na souboru MOF nebo **získat**, **nastavit**, a **Test** metody založené na třídě prostředku).
To je možné třetími stranami, které chcete použít prostředky DSC, nebo jako užitečné nástroje při vývoji prostředky.

Tato rutina se obvykle používá v kombinaci s vlastností metaconfiguration `refreshMode = 'Disabled'`, ale dá se použít bez ohledu na to, co **refreshMode** nastavena.

Při volání **Invoke-DscResource** rutiny, zadejte metody nebo funkce volání pomocí **metoda** parametru. Zadejte vlastnosti prostředku předáním zatřiďovací tabulku jako hodnotu **vlastnost** parametru.

Následují příklady přímé volání metod prostředku:

## <a name="ensure-a-file-is-present"></a>Ujistěte se, že soubor je k dispozici

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

>**Poznámka:** Přímé volání metody složeného prostředků se nepodporuje. Místo toho volejte metody příslušných prostředků, které tvoří složených prostředků.

## <a name="see-also"></a>Viz také
- [Psaní vlastních prostředků DSC s MOF](../resources/authoringResourceMOF.md)
- [Psaní vlastních prostředků DSC pomocí tříd Powershellu](../resources/authoringResourceClass.md)
- [Ladění prostředků DSC](../troubleshooting/debugResource.md)