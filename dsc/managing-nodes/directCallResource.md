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
# <a name="calling-dsc-resource-methods-directly"></a><span data-ttu-id="a1305-103">Přímé volání metod prostředku DSC</span><span class="sxs-lookup"><span data-stu-id="a1305-103">Calling DSC resource methods directly</span></span>

><span data-ttu-id="a1305-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="a1305-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="a1305-105">Můžete použít [Invoke-DscResource](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource) rutiny volat přímo funkcí nebo metod prostředku DSC ( **Get-TargetResource**, **Set-TargetResource**a  **Test-TargetResource** funkce prostředek založený na souboru MOF nebo **získat**, **nastavit**, a **Test** metody založené na třídě prostředku).</span><span class="sxs-lookup"><span data-stu-id="a1305-105">You can use the [Invoke-DscResource](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource) cmdlet to directly call the functions or methods of a DSC resource (The **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions of a MOF-based resource, or the **Get**, **Set**, and **Test** methods of a class-based resource).</span></span>
<span data-ttu-id="a1305-106">To je možné třetími stranami, které chcete použít prostředky DSC, nebo jako užitečné nástroje při vývoji prostředky.</span><span class="sxs-lookup"><span data-stu-id="a1305-106">This can be used by third-parties that want to use DSC resources, or as a helpful tool while developing resources.</span></span>

<span data-ttu-id="a1305-107">Tato rutina se obvykle používá v kombinaci s vlastností metaconfiguration `refreshMode = 'Disabled'`, ale dá se použít bez ohledu na to, co **refreshMode** nastavena.</span><span class="sxs-lookup"><span data-stu-id="a1305-107">This cmdlet is typically used in combination with a metaconfiguration property `refreshMode = 'Disabled'`, but it can be used no matter what **refreshMode** is set to.</span></span>

<span data-ttu-id="a1305-108">Při volání **Invoke-DscResource** rutiny, zadejte metody nebo funkce volání pomocí **metoda** parametru.</span><span class="sxs-lookup"><span data-stu-id="a1305-108">When calling the **Invoke-DscResource** cmdlet, you specify which method or function to call by using the **Method** parameter.</span></span> <span data-ttu-id="a1305-109">Zadejte vlastnosti prostředku předáním zatřiďovací tabulku jako hodnotu **vlastnost** parametru.</span><span class="sxs-lookup"><span data-stu-id="a1305-109">You specify the properties of the resource by passing a hashtable as the value of the **Property** parameter.</span></span>

<span data-ttu-id="a1305-110">Následují příklady přímé volání metod prostředku:</span><span class="sxs-lookup"><span data-stu-id="a1305-110">The following are examples of directly calling resource methods:</span></span>

## <a name="ensure-a-file-is-present"></a><span data-ttu-id="a1305-111">Ujistěte se, že soubor je k dispozici</span><span class="sxs-lookup"><span data-stu-id="a1305-111">Ensure a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a><span data-ttu-id="a1305-112">Otestovat, zda soubor existuje</span><span class="sxs-lookup"><span data-stu-id="a1305-112">Test that a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a><span data-ttu-id="a1305-113">Získat obsah souboru</span><span class="sxs-lookup"><span data-stu-id="a1305-113">Get the contents of file</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

><span data-ttu-id="a1305-114">**Poznámka:** Přímé volání metody složeného prostředků se nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="a1305-114">**Note:** Directly calling composite resource methods is not supported.</span></span> <span data-ttu-id="a1305-115">Místo toho volejte metody příslušných prostředků, které tvoří složených prostředků.</span><span class="sxs-lookup"><span data-stu-id="a1305-115">Instead, call the methods of the underlying resources that make up the composite resource.</span></span>

## <a name="see-also"></a><span data-ttu-id="a1305-116">Viz také</span><span class="sxs-lookup"><span data-stu-id="a1305-116">See Also</span></span>
- [<span data-ttu-id="a1305-117">Psaní vlastních prostředků DSC s MOF</span><span class="sxs-lookup"><span data-stu-id="a1305-117">Writing a custom DSC resource with MOF</span></span>](../resources/authoringResourceMOF.md)
- [<span data-ttu-id="a1305-118">Psaní vlastních prostředků DSC pomocí tříd Powershellu</span><span class="sxs-lookup"><span data-stu-id="a1305-118">Writing a custom DSC resource with PowerShell classes</span></span>](../resources/authoringResourceClass.md)
- [<span data-ttu-id="a1305-119">Ladění prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="a1305-119">Debugging DSC resources</span></span>](../troubleshooting/debugResource.md)