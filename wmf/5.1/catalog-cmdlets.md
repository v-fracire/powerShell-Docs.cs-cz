---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Katalogové rutiny
ms.openlocfilehash: ec5fc866fe27a894b23b93d3ea46ad9c0cba288e
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522884"
---
# <a name="catalog-cmdlets"></a><span data-ttu-id="f2d1c-103">Katalogové rutiny</span><span class="sxs-lookup"><span data-stu-id="f2d1c-103">Catalog Cmdlets</span></span>

<span data-ttu-id="f2d1c-104">Přidali jsme dvě nové rutiny v [Microsoft.Powershell.Secuity](https://technet.microsoft.com/library/hh847877.aspx) modul pro generování a ověřování souborů katalogu systému windows.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-104">We have added two new cmdlets in [Microsoft.Powershell.Secuity](https://technet.microsoft.com/library/hh847877.aspx) module to generate and validate windows catalog files.</span></span>

## <a name="new-filecatalog"></a><span data-ttu-id="f2d1c-105">New-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="f2d1c-105">New-FileCatalog</span></span>
--------------------------------

<span data-ttu-id="f2d1c-106">`New-FileCatalog` Vytvoří soubor katalogu systému windows pro sadu složek a souborů.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-106">`New-FileCatalog` creates a windows catalog file for set of folders and files.</span></span> <span data-ttu-id="f2d1c-107">Soubor katalogu obsahuje hodnoty hash pro všechny soubory v zadané cesty.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-107">A catalog file contains hashes for all files in specified paths.</span></span> <span data-ttu-id="f2d1c-108">Sadu složek společně s odpovídající soubor katalogu, který představuje tyto složky můžete distribuovat uživatelům.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-108">Users can distribute the set of folders along with corresponding the catalog file that represents those folders.</span></span> <span data-ttu-id="f2d1c-109">Soubor katalogu lze příjemci obsahu k ověření, zda byly provedeny žádné změny do složek po vytvoření katalogu.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-109">A catalog file can be used by the recipient of content to validate whether any changes were made to the folders after the catalog was created.</span></span>

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
<span data-ttu-id="f2d1c-110">Podporuje vytváření katalogu verze 1 a 2.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-110">We support creating catalog version 1 and 2.</span></span> <span data-ttu-id="f2d1c-111">K vytvoření hodnoty hash souboru a verze 2 používá SHA256 verze 1 používá algoritmus hash SHA1.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-111">Version 1 uses SHA1 hashing algorithm to create file hashes and version 2 uses SHA256.</span></span> <span data-ttu-id="f2d1c-112">Katalog verze 2 nepodporuje *systému Windows Server 2008 R2* a *Windows 7*.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-112">Catalog version 2 is not supported on *Windows Server 2008 R2* and *Windows 7*.</span></span> <span data-ttu-id="f2d1c-113">Doporučuje se použití katalogu verze 2, pokud používáte platformy *Windows 8*, *systému Windows Server 2012* a vyšší.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-113">It is recommended to use catalog version 2 if using platforms *Windows 8*, *Windows Server 2012* and above.</span></span>

<span data-ttu-id="f2d1c-114">Pokud chcete použít tento příkaz na existující modul, určete CatalogFilePath a cestu proměnné tak, aby odpovídaly umístění manifestu modulu.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-114">To use this command on an existing module, specify the CatalogFilePath and Path variables to match the location of the module manifest.</span></span> <span data-ttu-id="f2d1c-115">V následujícím příkladu je manifestu modulu v C:\Program Files\Windows PowerShell\Modules\Pester.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-115">In the example below, the module manifest is in C:\Program Files\Windows PowerShell\Modules\Pester.</span></span>

![](../images/NewFileCatalog.jpg)

<span data-ttu-id="f2d1c-116">Tím se vytvoří soubor katalogu.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-116">This creates the catalog file.</span></span>

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

<span data-ttu-id="f2d1c-117">Chcete-li ověřit integritu souboru katalogu (Pester.cat v nad příkladu) by měl být podepsáno, pomocí [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-117">To verify the integrity of a catalog file (Pester.cat in above exmaple) it should be signed using the [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) cmdlet.</span></span>


## <a name="test-filecatalog"></a><span data-ttu-id="f2d1c-118">Test-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="f2d1c-118">Test-FileCatalog</span></span>
--------------------------------

<span data-ttu-id="f2d1c-119">`Test-FileCatalog` ověří katalogu představující sadu složek.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-119">`Test-FileCatalog` validates the catalog representing a set of folders.</span></span>

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

<span data-ttu-id="f2d1c-120">Tato rutina porovnává hodnoty hash všechny soubory a jejich relativní cesty nacházejí v souboru katalogu s těmi, které je uloženo na disk.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-120">This cmdlet compares the hashes of all files and their relative paths found in the catalog file with ones saved to disk.</span></span> <span data-ttu-id="f2d1c-121">Když najde jakákoli Neshoda mezi hodnoty hash souboru a cesty vrátí stav `ValidationFailed`.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-121">If it detects any mismatch between file hashes and paths it returns a status of `ValidationFailed`.</span></span>
<span data-ttu-id="f2d1c-122">Uživatelé mohou načítat všechny informace pomocí `Detailed` přepnout.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-122">Users can retrieve all this information using the `Detailed` switch.</span></span> <span data-ttu-id="f2d1c-123">Podepisování stav katalogu se zobrazí jako `Signature` pole, která je stejná jako volání funkce [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx) rutinu na soubor katalogu.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-123">The signing status of the catalog is displayed as the `Signature` field, which is same as calling the [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx) cmdlet on the catalog file.</span></span>
<span data-ttu-id="f2d1c-124">Uživatelé také přeskočit všechny soubory během ověřování s použitím `FilesToSkip` parametru.</span><span class="sxs-lookup"><span data-stu-id="f2d1c-124">Users can also skip any file during validation by using the `FilesToSkip` parameter.</span></span>
