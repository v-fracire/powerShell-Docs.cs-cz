---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Řazení objektů
ms.assetid: 8530caa8-3ed4-4c56-aed7-1295dd9ba199
ms.openlocfilehash: 06aa15d89888f1ecbe60b8e1dfb4efebb1d73673
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403644"
---
# <a name="sorting-objects"></a><span data-ttu-id="0c65c-103">Řazení objektů</span><span class="sxs-lookup"><span data-stu-id="0c65c-103">Sorting Objects</span></span>

<span data-ttu-id="0c65c-104">Jsme můžete uspořádat zobrazených dat, aby bylo snazší vyhledávání s použitím `Sort-Object` rutiny.</span><span class="sxs-lookup"><span data-stu-id="0c65c-104">We can organize displayed data to make it easier to scan by using the `Sort-Object` cmdlet.</span></span> <span data-ttu-id="0c65c-105">`Sort-Object` přebírá název jednu nebo více vlastností, které se budou řadit a vrací data seřazené podle hodnoty těchto vlastností.</span><span class="sxs-lookup"><span data-stu-id="0c65c-105">`Sort-Object` takes the name of one or more properties to sort on, and returns data sorted by the values of those properties.</span></span>

## <a name="basic-sorting"></a><span data-ttu-id="0c65c-106">Základní řazení</span><span class="sxs-lookup"><span data-stu-id="0c65c-106">Basic sorting</span></span>

<span data-ttu-id="0c65c-107">Vezměte v úvahu problém uvedení podadresáře a soubory v aktuálním adresáři.</span><span class="sxs-lookup"><span data-stu-id="0c65c-107">Consider the problem of listing subdirectories and files in the current directory.</span></span>
<span data-ttu-id="0c65c-108">Pokud chceme řadit **LastWriteTime** a potom podle **název**, můžeme to udělat tak, že zadáte:</span><span class="sxs-lookup"><span data-stu-id="0c65c-108">If we want to sort by **LastWriteTime** and then by **Name**, we can do it by typing:</span></span>

```powershell
Get-ChildItem |
  Sort-Object -Property LastWriteTime, Name |
  Format-Table -Property LastWriteTime, Name
```

```output
LastWriteTime          Name
-------------          ----
11/6/2017 10:10:11 AM  .localization-config
11/6/2017 10:10:11 AM  .openpublishing.build.ps1
11/6/2017 10:10:11 AM  appveyor.yml
11/6/2017 10:10:11 AM  LICENSE
11/6/2017 10:10:11 AM  LICENSE-CODE
11/6/2017 10:10:11 AM  ThirdPartyNotices
11/6/2017 10:10:15 AM  tests
6/6/2018 7:58:59 PM    CONTRIBUTING.md
6/6/2018 7:58:59 PM    README.md
...
```

<span data-ttu-id="0c65c-109">Můžete také řadit objektů v obráceném pořadí tak, že zadáte **sestupně** přepnout parametru.</span><span class="sxs-lookup"><span data-stu-id="0c65c-109">You can also sort the objects in reverse order by specifying the **Descending** switch parameter.</span></span>

```powershell
Get-ChildItem |
  Sort-Object -Property LastWriteTime, Name -Descending |
  Format-Table -Property LastWriteTime, Name
```

```output
LastWriteTime          Name
-------------          ----
12/1/2018 10:13:50 PM  reference
12/1/2018 10:13:50 PM  dsc
...
6/6/2018 7:58:59 PM    README.md
6/6/2018 7:58:59 PM    CONTRIBUTING.md
11/6/2017 10:10:15 AM  tests
11/6/2017 10:10:11 AM  ThirdPartyNotices
11/6/2017 10:10:11 AM  LICENSE-CODE
11/6/2017 10:10:11 AM  LICENSE
11/6/2017 10:10:11 AM  appveyor.yml
11/6/2017 10:10:11 AM  .openpublishing.build.ps1
11/6/2017 10:10:11 AM  .localization-config
```

## <a name="using-hash-tables"></a><span data-ttu-id="0c65c-110">Pomocí zatřiďovacích tabulek</span><span class="sxs-lookup"><span data-stu-id="0c65c-110">Using hash tables</span></span>

<span data-ttu-id="0c65c-111">S použitím v poli zatřiďovacích tabulek můžete seřadit různé vlastnosti v různém pořadí.</span><span class="sxs-lookup"><span data-stu-id="0c65c-111">You can sort different properties in different orders by using hash tables in an array.</span></span>
<span data-ttu-id="0c65c-112">Každá tabulka hash používá **výraz** klíč k určení názvu vlastnosti jako řetězec a **vzestupně** nebo **sestupně** klíč k určení pořadí řazení podle `$true` nebo `$false`.</span><span class="sxs-lookup"><span data-stu-id="0c65c-112">Each hash table uses an **Expression** key to specify the property name as string and an **Ascending** or **Descending** key to specify the sort order by `$true` or `$false`.</span></span>
<span data-ttu-id="0c65c-113">**Výraz** klíč je povinný.</span><span class="sxs-lookup"><span data-stu-id="0c65c-113">The **Expression** key is mandatory.</span></span>
<span data-ttu-id="0c65c-114">**Vzestupně** nebo **sestupně** klíč je volitelný.</span><span class="sxs-lookup"><span data-stu-id="0c65c-114">The **Ascending** or **Descending** key is optional.</span></span>

<span data-ttu-id="0c65c-115">Následující příklad řadí objekty v sestupném **LastWriteTime** pořadí a vzestupně **název** pořadí.</span><span class="sxs-lookup"><span data-stu-id="0c65c-115">The following example sorts objects in descending **LastWriteTime** order and ascending **Name** order.</span></span>

```powershell
Get-ChildItem |
  Sort-Object -Property @{ Expression = 'LastWriteTime'; Descending = $true }, @{ Expression = 'Name'; Ascending = $true } |
  Format-Table -Property LastWriteTime, Name
```

```output
LastWriteTime          Name
-------------          ----
12/1/2018 10:13:50 PM  dsc
12/1/2018 10:13:50 PM  reference
11/29/2018 6:56:01 PM  .openpublishing.redirection.json
11/29/2018 6:56:01 PM  gallery
11/24/2018 10:33:22 AM developer
11/20/2018 7:22:19 PM  .markdownlint.json
...
```

<span data-ttu-id="0c65c-116">Můžete také nastavit vlastnost scriptblock **výraz** klíč.</span><span class="sxs-lookup"><span data-stu-id="0c65c-116">You can also set a scriptblock to the **Expression** key.</span></span>
<span data-ttu-id="0c65c-117">Při spuštění `Sort-Object` rutiny, spouští se vlastnost scriptblock a výsledek je použít k řazení.</span><span class="sxs-lookup"><span data-stu-id="0c65c-117">When running the `Sort-Object` cmdlet, the scriptblock is executed and the result is used for sorting.</span></span>

<span data-ttu-id="0c65c-118">Následující příklad seřadí v sestupném pořadí podle časový interval mezi objekty **CreationTime** a **LastWriteTime**.</span><span class="sxs-lookup"><span data-stu-id="0c65c-118">The following example sorts objects in descending order by the time span between **CreationTime** and **LastWriteTime**.</span></span>

```powershell
Get-ChildItem |
  Sort-Object -Property @{ Expression = { $_.LastWriteTime - $_.CreationTime }; Descending = $true } |
  Format-Table -Property LastWriteTime, CreationTime
```

```output
LastWriteTime          CreationTime
-------------          ------------
12/1/2018 10:13:50 PM  11/6/2017 10:10:11 AM
12/1/2018 10:13:50 PM  11/6/2017 10:10:11 AM
11/7/2018 6:52:24 PM   11/6/2017 10:10:11 AM
11/7/2018 6:52:24 PM   11/6/2017 10:10:15 AM
11/3/2018 9:58:17 AM   11/6/2017 10:10:11 AM
10/26/2018 4:50:21 PM  11/6/2017 10:10:11 AM
11/17/2018 1:10:57 PM  11/29/2017 5:48:30 PM
11/12/2018 6:29:53 PM  12/7/2017 7:57:07 PM
...
```

## <a name="tips"></a><span data-ttu-id="0c65c-119">Tipy</span><span class="sxs-lookup"><span data-stu-id="0c65c-119">Tips</span></span>

<span data-ttu-id="0c65c-120">Můžete vynechat **vlastnost** název parametru následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="0c65c-120">You can omit the **Property** parameter name as following:</span></span>

```powershell
Sort-Object LastWriteTime, Name
```

<span data-ttu-id="0c65c-121">Kromě toho se můžete vrátit k `Sort-Object` podle jeho alias integrované `sort`:</span><span class="sxs-lookup"><span data-stu-id="0c65c-121">Besides, you can refer to `Sort-Object` by its built-in alias, `sort`:</span></span>

```powershell
sort LastWriteTime, Name
```

<span data-ttu-id="0c65c-122">Klíče v zatřiďovací tabulky pro řazení lze zkrátit následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="0c65c-122">The keys in the hash tables for sorting can be abbreviated as following:</span></span>

```powershell
Sort-Object @{ e = 'LastWriteTime'; d = $true }, @{ e = 'Name'; a = $true }
```

<span data-ttu-id="0c65c-123">V tomto příkladu **e** zastupuje **výraz**, **d** zastupuje **sestupně**a **a** zastupuje **vzestupně**.</span><span class="sxs-lookup"><span data-stu-id="0c65c-123">In this example, the **e** stands for **Expression**, the **d** stands for **Descending**, and the **a** stands for **Ascending**.</span></span>

<span data-ttu-id="0c65c-124">Aby se zlepšila čitelnost, můžete umístit zatřiďovací tabulky do samostatných proměnné:</span><span class="sxs-lookup"><span data-stu-id="0c65c-124">To improve readability, you can place the hash tables into a separate variable:</span></span>

```powershell
$order = @(
  @{ Expression = 'LastWriteTime'; Descending = $true }
  @{ Expression = 'Name'; Ascending = $true }
)

Get-ChildItem |
  Sort-Object $order |
  Format-Table LastWriteTime, Name
```