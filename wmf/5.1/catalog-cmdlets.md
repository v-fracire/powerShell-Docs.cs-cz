---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Katalogové rutiny
ms.openlocfilehash: 7eaca09667af0eb5d719f23e987bb112e8514978
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="catalog-cmdlets"></a><span data-ttu-id="bd433-103">Rutiny katalogu</span><span class="sxs-lookup"><span data-stu-id="bd433-103">Catalog Cmdlets</span></span>

<span data-ttu-id="bd433-104">Jsme přidali dvě nové rutiny v [Microsoft.Powershell.Secuity](https://technet.microsoft.com/en-us/library/hh847877.aspx) modulu pro vygenerování a ověření souborů katalogu systému windows.</span><span class="sxs-lookup"><span data-stu-id="bd433-104">We have added two new cmdlets in [Microsoft.Powershell.Secuity](https://technet.microsoft.com/en-us/library/hh847877.aspx) module to generate and validate windows catalog files.</span></span>

## <a name="new-filecatalog"></a><span data-ttu-id="bd433-105">New-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="bd433-105">New-FileCatalog</span></span>
--------------------------------

<span data-ttu-id="bd433-106">`New-FileCatalog` Vytvoří soubor katalogu systému windows pro sadu složek a souborů.</span><span class="sxs-lookup"><span data-stu-id="bd433-106">`New-FileCatalog` creates a windows catalog file for set of folders and files.</span></span> <span data-ttu-id="bd433-107">Soubor katalogu obsahuje hodnoty hash pro všechny soubory v zadané cesty.</span><span class="sxs-lookup"><span data-stu-id="bd433-107">A catalog file contains hashes for all files in specified paths.</span></span> <span data-ttu-id="bd433-108">Uživatele můžete distribuovat sadu složek spolu s odpovídající soubor katalogu, který představuje těchto složek.</span><span class="sxs-lookup"><span data-stu-id="bd433-108">Users can distribute the set of folders along with corresponding the catalog file that represents those folders.</span></span> <span data-ttu-id="bd433-109">Soubor katalogu lze příjemce obsahu k ověření, zda všechny změny byly provedeny do složek, po vytvoření katalogu.</span><span class="sxs-lookup"><span data-stu-id="bd433-109">A catalog file can be used by the recipient of content to validate whether any changes were made to the folders after the catalog was created.</span></span>

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
<span data-ttu-id="bd433-110">Podporujeme vytváření katalogu verze 1 a 2.</span><span class="sxs-lookup"><span data-stu-id="bd433-110">We support creating catalog version 1 and 2.</span></span> <span data-ttu-id="bd433-111">Verze 1 používá algoritmus hash SHA1 k vytvoření hodnoty hash souboru a verze 2 používá algoritmus SHA256.</span><span class="sxs-lookup"><span data-stu-id="bd433-111">Version 1 uses SHA1 hashing algorithm to create file hashes and version 2 uses SHA256.</span></span> <span data-ttu-id="bd433-112">Katalog verze 2 není podporována na *Windows Server 2008 R2* a *Windows 7*.</span><span class="sxs-lookup"><span data-stu-id="bd433-112">Catalog version 2 is not supported on *Windows Server 2008 R2* and *Windows 7*.</span></span> <span data-ttu-id="bd433-113">Doporučuje se používat katalog verze 2, pokud pomocí platformy *Windows 8*, *systému Windows Server 2012* a vyšší.</span><span class="sxs-lookup"><span data-stu-id="bd433-113">It is recommended to use catalog version 2 if using platforms *Windows 8*, *Windows Server 2012* and above.</span></span>

<span data-ttu-id="bd433-114">Chcete-li použít tento příkaz na existující modul, zadejte CatalogFilePath a cestu proměnné tak, aby odpovídala umístění manifestu modulu.</span><span class="sxs-lookup"><span data-stu-id="bd433-114">To use this command on an existing module, specify the CatalogFilePath and Path variables to match the location of the module manifest.</span></span> <span data-ttu-id="bd433-115">V následujícím příkladu je manifestu modulu v C:\Program Files\Windows PowerShell\Modules\Pester.</span><span class="sxs-lookup"><span data-stu-id="bd433-115">In the example below, the module manifest is in C:\Program Files\Windows PowerShell\Modules\Pester.</span></span>

![](../images/NewFileCatalog.jpg)

<span data-ttu-id="bd433-116">Tím se vytvoří soubor katalogu.</span><span class="sxs-lookup"><span data-stu-id="bd433-116">This creates the catalog file.</span></span>

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

<span data-ttu-id="bd433-117">Chcete-li ověřit integritu soubor katalogu (Pester.cat v výše exmaple) by měla být podepsána, pomocí [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="bd433-117">To verify the integrity of a catalog file (Pester.cat in above exmaple) it should be signed using the [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) cmdlet.</span></span>


## <a name="test-filecatalog"></a><span data-ttu-id="bd433-118">Test FileCatalog</span><span class="sxs-lookup"><span data-stu-id="bd433-118">Test-FileCatalog</span></span>
--------------------------------

<span data-ttu-id="bd433-119">`Test-FileCatalog` ověří katalogu představující sadu složek.</span><span class="sxs-lookup"><span data-stu-id="bd433-119">`Test-FileCatalog` validates the catalog representing a set of folders.</span></span>

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

<span data-ttu-id="bd433-120">Tato rutina porovnává hodnoty hash všech souborů a jejich relativní cesty nacházejí v souboru katalogu s těch, které jsou uloženy na disk.</span><span class="sxs-lookup"><span data-stu-id="bd433-120">This cmdlet compares the hashes of all files and their relative paths found in the catalog file with ones saved to disk.</span></span> <span data-ttu-id="bd433-121">Pokud zjistí jakékoli neshody mezi hodnoty hash souboru a cesty vrátí stav `ValidationFailed`.</span><span class="sxs-lookup"><span data-stu-id="bd433-121">If it detects any mismatch between file hashes and paths it returns a status of `ValidationFailed`.</span></span>
<span data-ttu-id="bd433-122">Uživatele můžete načíst všechny tato informace pomocí `Detailed` přepínače.</span><span class="sxs-lookup"><span data-stu-id="bd433-122">Users can retrieve all this information using the `Detailed` switch.</span></span> <span data-ttu-id="bd433-123">Podpisový stav katalogu se zobrazí jako `Signature` pole, která je stejná jako volání [Get-AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) na soubor katalogu rutinu.</span><span class="sxs-lookup"><span data-stu-id="bd433-123">The signing status of the catalog is displayed as the `Signature` field, which is same as calling the [Get-AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) cmdlet on the catalog file.</span></span>
<span data-ttu-id="bd433-124">Uživatelé také přeskočit všechny soubory během ověřování pomocí `FilesToSkip` parametr.</span><span class="sxs-lookup"><span data-stu-id="bd433-124">Users can also skip any file during validation by using the `FilesToSkip` parameter.</span></span>
