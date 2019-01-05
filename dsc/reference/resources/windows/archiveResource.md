---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC Archive
ms.openlocfilehash: d5ccd242d000a0907c6768f30923764be6bf20a3
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048141"
---
# <a name="dsc-archive-resource"></a><span data-ttu-id="d002f-103">Prostředek DSC Archive</span><span class="sxs-lookup"><span data-stu-id="d002f-103">DSC Archive Resource</span></span>

> <span data-ttu-id="d002f-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="d002f-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="d002f-105">Prostředek Archive ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus k rozbalení archivu (ZIP) soubory do konkrétní cesty.</span><span class="sxs-lookup"><span data-stu-id="d002f-105">The Archive resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to unpack archive (.zip) files at a specific path.</span></span>

## <a name="syntax"></a><span data-ttu-id="d002f-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d002f-106">Syntax</span></span>
```MOF
Archive [string] #ResourceName
{
    Destination = [string]
    Path = [string]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Force = [bool] ]
    [ Validate = [bool] ]
}
```

## <a name="properties"></a><span data-ttu-id="d002f-107">Properties</span><span class="sxs-lookup"><span data-stu-id="d002f-107">Properties</span></span>

|  <span data-ttu-id="d002f-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="d002f-108">Property</span></span>  |  <span data-ttu-id="d002f-109">Popis</span><span class="sxs-lookup"><span data-stu-id="d002f-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="d002f-110">Cíl</span><span class="sxs-lookup"><span data-stu-id="d002f-110">Destination</span></span>| <span data-ttu-id="d002f-111">Určuje umístění, ve které chcete zajistit, aby že extrahování obsahu archivu.</span><span class="sxs-lookup"><span data-stu-id="d002f-111">Specifies the location where you want to ensure the archive contents are extracted.</span></span>|
| <span data-ttu-id="d002f-112">Cesta</span><span class="sxs-lookup"><span data-stu-id="d002f-112">Path</span></span>| <span data-ttu-id="d002f-113">Určuje zdrojovou cestu souboru archivu.</span><span class="sxs-lookup"><span data-stu-id="d002f-113">Specifies the source path of the archive file.</span></span>|
| <span data-ttu-id="d002f-114">__Kontrolní součet__</span><span class="sxs-lookup"><span data-stu-id="d002f-114">__Checksum__</span></span>| <span data-ttu-id="d002f-115">Definuje typ, který má použít při určování, zda dva soubory jsou stejné.</span><span class="sxs-lookup"><span data-stu-id="d002f-115">Defines the type to use when determining whether two files are the same.</span></span> <span data-ttu-id="d002f-116">Pokud __kontrolního součtu__ není zadán, pouze název souboru nebo složky se používá pro porovnání.</span><span class="sxs-lookup"><span data-stu-id="d002f-116">If __Checksum__ is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="d002f-117">Platné hodnoty jsou: SHA-1, SHA-256, SHA-512, datum vytvoření, modifiedDate, none (výchozí).</span><span class="sxs-lookup"><span data-stu-id="d002f-117">Valid values include: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate, none (default).</span></span> <span data-ttu-id="d002f-118">Pokud zadáte __kontrolního součtu__ bez __ověřit__, konfigurace se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="d002f-118">If you specify __Checksum__ without __Validate__, the configuration will fail.</span></span>|
| <span data-ttu-id="d002f-119">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="d002f-119">Ensure</span></span>| <span data-ttu-id="d002f-120">Určuje, jestli se má zkontrolovat, zda obsah archivu existuje na __cílové__.</span><span class="sxs-lookup"><span data-stu-id="d002f-120">Determines whether to check if the content of the archive exists at the __Destination__.</span></span> <span data-ttu-id="d002f-121">Tuto vlastnost nastavte na __k dispozici__ zajistit obsah neexistuje.</span><span class="sxs-lookup"><span data-stu-id="d002f-121">Set this property to __Present__ to ensure the contents exist.</span></span> <span data-ttu-id="d002f-122">Nastavte ho na __chybí__ zajistit ještě neexistují.</span><span class="sxs-lookup"><span data-stu-id="d002f-122">Set it to __Absent__ to ensure they do not exist.</span></span> <span data-ttu-id="d002f-123">Výchozí hodnota je __k dispozici__.</span><span class="sxs-lookup"><span data-stu-id="d002f-123">The default value is __Present__.</span></span>|
| <span data-ttu-id="d002f-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="d002f-124">DependsOn</span></span> | <span data-ttu-id="d002f-125">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="d002f-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="d002f-126">Například pokud první je ID bloku skriptu konfigurace prostředků, kterou chcete spustit ResourceName a její typ je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="d002f-126">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="d002f-127">Ověření</span><span class="sxs-lookup"><span data-stu-id="d002f-127">Validate</span></span>| <span data-ttu-id="d002f-128">Vlastnost kontrolní součet se používá k určení, pokud archiv odpovídá podpisu.</span><span class="sxs-lookup"><span data-stu-id="d002f-128">Uses the Checksum property to determine if the archive matches the signature.</span></span> <span data-ttu-id="d002f-129">Pokud chcete zadat kontrolního součtu bez ověřením, konfigurace se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="d002f-129">If you specify Checksum without Validate, the configuration will fail.</span></span> <span data-ttu-id="d002f-130">Pokud chcete zadat ověřit bez kontrolního součtu, se standardně používá kontrolního součtu SHA-256.</span><span class="sxs-lookup"><span data-stu-id="d002f-130">If you specify Validate without Checksum, a SHA-256 checksum is used by default.</span></span>|
| <span data-ttu-id="d002f-131">Force</span><span class="sxs-lookup"><span data-stu-id="d002f-131">Force</span></span>| <span data-ttu-id="d002f-132">Určité operace se soubory (například soubor přepsání nebo odstranění adresáře, který není prázdný) dojde chybě.</span><span class="sxs-lookup"><span data-stu-id="d002f-132">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="d002f-133">Pomocí vlastnosti vynucení přepsání tyto chyby.</span><span class="sxs-lookup"><span data-stu-id="d002f-133">Using the Force property overrides such errors.</span></span> <span data-ttu-id="d002f-134">Výchozí hodnota je False.</span><span class="sxs-lookup"><span data-stu-id="d002f-134">The default value is False.</span></span>|

## <a name="example"></a><span data-ttu-id="d002f-135">Příklad</span><span class="sxs-lookup"><span data-stu-id="d002f-135">Example</span></span>

<span data-ttu-id="d002f-136">Následující příklad ukazuje, jak použít prostředek Archive zajistíte, že obsah souboru archivu, s názvem Test.zip existují a jsou extrahovány na určitého cíle.</span><span class="sxs-lookup"><span data-stu-id="d002f-136">The following example shows how to use the Archive resource to ensure that the contents of an archive file called Test.zip exist and are extracted at a given destination.</span></span>

```
Archive ArchiveExample {
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Path = "C:\Users\Public\Documents\Test.zip"
    Destination = "C:\Users\Public\Documents\ExtractionPath"
}
```