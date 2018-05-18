---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Prostředek DSC archivu
ms.openlocfilehash: 458b4f0f20dc96dab62e709183c25ff57d971aae
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="dsc-archive-resource"></a><span data-ttu-id="b1f3a-103">Prostředek DSC archivu</span><span class="sxs-lookup"><span data-stu-id="b1f3a-103">DSC Archive Resource</span></span>

> <span data-ttu-id="b1f3a-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b1f3a-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="b1f3a-105">Archiv prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus rozbalte souborech archivu (.zip) na konkrétní cesty.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-105">The Archive resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to unpack archive (.zip) files at a specific path.</span></span>

## <a name="syntax"></a><span data-ttu-id="b1f3a-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b1f3a-106">Syntax</span></span>
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

## <a name="properties"></a><span data-ttu-id="b1f3a-107">Properties</span><span class="sxs-lookup"><span data-stu-id="b1f3a-107">Properties</span></span>

|  <span data-ttu-id="b1f3a-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="b1f3a-108">Property</span></span>  |  <span data-ttu-id="b1f3a-109">Popis</span><span class="sxs-lookup"><span data-stu-id="b1f3a-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="b1f3a-110">Cíl</span><span class="sxs-lookup"><span data-stu-id="b1f3a-110">Destination</span></span>| <span data-ttu-id="b1f3a-111">Určuje umístění, kam chcete zajistit, aby že se extrahují obsah archivu.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-111">Specifies the location where you want to ensure the archive contents are extracted.</span></span>|
| <span data-ttu-id="b1f3a-112">Cesta</span><span class="sxs-lookup"><span data-stu-id="b1f3a-112">Path</span></span>| <span data-ttu-id="b1f3a-113">Určuje zdroj cestu k souboru archivu.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-113">Specifies the source path of the archive file.</span></span>|
| <span data-ttu-id="b1f3a-114">__Kontrolní součet__</span><span class="sxs-lookup"><span data-stu-id="b1f3a-114">__Checksum__</span></span>| <span data-ttu-id="b1f3a-115">Definuje typ, který má použít při určování, zda dva soubory jsou stejné.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-115">Defines the type to use when determining whether two files are the same.</span></span> <span data-ttu-id="b1f3a-116">Pokud __kontrolního součtu__ není zadán, pro porovnání se používá pouze název souboru nebo adresáře.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-116">If __Checksum__ is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="b1f3a-117">Platné hodnoty patří: SHA-1, SHA-256, SHA-512, datum vytvoření, modifiedDate, none (výchozí).</span><span class="sxs-lookup"><span data-stu-id="b1f3a-117">Valid values include: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate, none (default).</span></span> <span data-ttu-id="b1f3a-118">Pokud zadáte __kontrolního součtu__ bez __ověřením__, konfigurace se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-118">If you specify __Checksum__ without __Validate__, the configuration will fail.</span></span>|
| <span data-ttu-id="b1f3a-119">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="b1f3a-119">Ensure</span></span>| <span data-ttu-id="b1f3a-120">Určuje, jestli se má zkontrolovat, zda existuje obsah archivu v __cílový__.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-120">Determines whether to check if the content of the archive exists at the __Destination__.</span></span> <span data-ttu-id="b1f3a-121">Tuto vlastnost nastavit na __přítomen__ zajistit obsah neexistuje.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-121">Set this property to __Present__ to ensure the contents exist.</span></span> <span data-ttu-id="b1f3a-122">Nastavte ji na __chybí__ zajistit, že nejsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-122">Set it to __Absent__ to ensure they do not exist.</span></span> <span data-ttu-id="b1f3a-123">Výchozí hodnota je __přítomen__.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-123">The default value is __Present__.</span></span>|
| <span data-ttu-id="b1f3a-124">dependsOn</span><span class="sxs-lookup"><span data-stu-id="b1f3a-124">DependsOn</span></span> | <span data-ttu-id="b1f3a-125">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="b1f3a-126">Například pokud ID bloku skriptu konfigurace prostředků, který chcete spustit nejprve je ResourceName a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-126">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="b1f3a-127">Ověření</span><span class="sxs-lookup"><span data-stu-id="b1f3a-127">Validate</span></span>| <span data-ttu-id="b1f3a-128">Vlastnost kontrolního součtu se používá k určení, jestli odpovídá archivu podpis.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-128">Uses the Checksum property to determine if the archive matches the signature.</span></span> <span data-ttu-id="b1f3a-129">Pokud zadáte kontrolního součtu bez ověřením, konfigurace se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-129">If you specify Checksum without Validate, the configuration will fail.</span></span> <span data-ttu-id="b1f3a-130">Pokud zadáte ověřit bez kontrolního součtu, použije se ve výchozím nastavení kontrolního součtu SHA-256.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-130">If you specify Validate without Checksum, a SHA-256 checksum is used by default.</span></span>|
| <span data-ttu-id="b1f3a-131">Force</span><span class="sxs-lookup"><span data-stu-id="b1f3a-131">Force</span></span>| <span data-ttu-id="b1f3a-132">Některé operace souboru (například přepsání souboru nebo odstranění adresáře, který není prázdný) bude výsledkem chyba.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-132">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="b1f3a-133">Pomocí vlastnosti Vynucené přepsání takové chyby.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-133">Using the Force property overrides such errors.</span></span> <span data-ttu-id="b1f3a-134">Výchozí hodnota je False.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-134">The default value is False.</span></span>|

## <a name="example"></a><span data-ttu-id="b1f3a-135">Příklad</span><span class="sxs-lookup"><span data-stu-id="b1f3a-135">Example</span></span>

<span data-ttu-id="b1f3a-136">Následující příklad ukazuje, jak používat prostředek archivu zajistit, že obsah souboru archivu názvem Test.zip neexistuje a extrahují na daný cíl.</span><span class="sxs-lookup"><span data-stu-id="b1f3a-136">The following example shows how to use the Archive resource to ensure that the contents of an archive file called Test.zip exist and are extracted at a given destination.</span></span>

```
Archive ArchiveExample {
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Path = "C:\Users\Public\Documents\Test.zip"
    Destination = "C:\Users\Public\Documents\ExtractionPath"
}
```