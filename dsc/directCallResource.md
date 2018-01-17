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
# <a name="calling-dsc-resource-methods-directly"></a><span data-ttu-id="d7f75-103">Přímé volání metody prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="d7f75-103">Calling DSC resource methods directly</span></span>

><span data-ttu-id="d7f75-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="d7f75-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="d7f75-105">Můžete použít [Invoke-DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx) rutiny volat přímo funkce nebo metody prostředek DSC ( **Get-TargetResource**, **Set-TargetResource**a  **Test-TargetResource** funkce na základě MOF prostředku, nebo **získat**, **nastavit**, a **Test** metody založené na třídě prostředku).</span><span class="sxs-lookup"><span data-stu-id="d7f75-105">You can use the [Invoke-DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx) cmdlet to directly call the functions or methods of a DSC resource (The **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions of a MOF-based resource, or the **Get**, **Set**, and **Test** methods of a class-based resource).</span></span> <span data-ttu-id="d7f75-106">Tímto lze třetích stran, které chcete použít prostředků DSC, nebo jako užitečné nástroje při vývoji prostředky.</span><span class="sxs-lookup"><span data-stu-id="d7f75-106">This can be used by third-parties that want to use DSC resources, or as a helpful tool while developing resources.</span></span> 

<span data-ttu-id="d7f75-107">Tato rutina se obvykle používá v kombinaci s vlastností metakonfiguraci `refreshMode = 'Disabled'`, ale dá se používat bez ohledu na to, co **refreshMode** je nastaven na.</span><span class="sxs-lookup"><span data-stu-id="d7f75-107">This cmdlet is typically used in combination with a metaconfiguration property `refreshMode = 'Disabled'`, but it can be used no matter what **refreshMode** is set to.</span></span>

<span data-ttu-id="d7f75-108">Při volání metody **Invoke-DscResource** rutiny, zadejte metody nebo funkce, která se pro volání **metoda** parametr.</span><span class="sxs-lookup"><span data-stu-id="d7f75-108">When calling the **Invoke-DscResource** cmdlet, you specify which method or function to call by using the **Method** parameter.</span></span> <span data-ttu-id="d7f75-109">Zadejte vlastnosti prostředku předáním zatřiďovací tabulku jako hodnotu **vlastnost** parametr.</span><span class="sxs-lookup"><span data-stu-id="d7f75-109">You specify the properties of the resource by passing a hashtable as the value of the **Property** parameter.</span></span>

<span data-ttu-id="d7f75-110">Následují příklady přímo volání metody prostředků:</span><span class="sxs-lookup"><span data-stu-id="d7f75-110">The following are examples of directly calling resource methods:</span></span>

## <a name="ensure-a-file-is-present"></a><span data-ttu-id="d7f75-111">Ujistěte se, že soubor existuje</span><span class="sxs-lookup"><span data-stu-id="d7f75-111">Ensure a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a><span data-ttu-id="d7f75-112">Otestovat, zda soubor existuje</span><span class="sxs-lookup"><span data-stu-id="d7f75-112">Test that a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a><span data-ttu-id="d7f75-113">Získat obsah souboru</span><span class="sxs-lookup"><span data-stu-id="d7f75-113">Get the contents of file</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

><span data-ttu-id="d7f75-114">**Poznámka:** přímo volání metody složené prostředků není podporováno.</span><span class="sxs-lookup"><span data-stu-id="d7f75-114">**Note:** Directly calling composite resource methods is not supported.</span></span> <span data-ttu-id="d7f75-115">Místo toho volejte metody základní prostředky, které tvoří složené prostředků.</span><span class="sxs-lookup"><span data-stu-id="d7f75-115">Instead, call the methods of the underlying resources that make up the composite resource.</span></span>

## <a name="see-also"></a><span data-ttu-id="d7f75-116">Viz také</span><span class="sxs-lookup"><span data-stu-id="d7f75-116">See Also</span></span>
- [<span data-ttu-id="d7f75-117">Psaní vlastních prostředků DSC s MOF</span><span class="sxs-lookup"><span data-stu-id="d7f75-117">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md) 
- [<span data-ttu-id="d7f75-118">Psaní vlastních prostředků DSC s třídami, prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7f75-118">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)
- [<span data-ttu-id="d7f75-119">Ladění prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="d7f75-119">Debugging DSC resources</span></span>](debugResource.md)

