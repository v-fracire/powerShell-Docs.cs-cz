---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxArchive
ms.openlocfilehash: 800954478f149e29c22d1a88304c3be9950f109a
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048155"
---
# <a name="dsc-for-linux-nxarchive-resource"></a><span data-ttu-id="619f8-103">DSC pro Linux prostředek nxArchive</span><span class="sxs-lookup"><span data-stu-id="619f8-103">DSC for Linux nxArchive Resource</span></span>

<span data-ttu-id="619f8-104">**NxArchive** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus pro rozbalení souborech archivu (.tar, .zip) v určité cestě na uzlu systému Linux.</span><span class="sxs-lookup"><span data-stu-id="619f8-104">The **nxArchive** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to unpack archive (.tar, .zip) files at a specific path on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="619f8-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="619f8-105">Syntax</span></span>

```
nxArchive <string> #ResourceName
{
    SourcePath = <string>
    DestinationPath = <string>
    [ Checksum = <string> { ctime | mtime | md5 }  ]
    [ Force = <bool> ]
    [ DependsOn = <string[]> ]
    [ Ensure = <string> { Absent | Present }  ]
}
```

## <a name="properties"></a><span data-ttu-id="619f8-106">Properties</span><span class="sxs-lookup"><span data-stu-id="619f8-106">Properties</span></span>

|  <span data-ttu-id="619f8-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="619f8-107">Property</span></span> |  <span data-ttu-id="619f8-108">Popis</span><span class="sxs-lookup"><span data-stu-id="619f8-108">Description</span></span> |
|---|---|
| <span data-ttu-id="619f8-109">SourcePath</span><span class="sxs-lookup"><span data-stu-id="619f8-109">SourcePath</span></span>| <span data-ttu-id="619f8-110">Určuje zdrojovou cestu souboru archivu.</span><span class="sxs-lookup"><span data-stu-id="619f8-110">Specifies the source path of the archive file.</span></span> <span data-ttu-id="619f8-111">Mělo by se jednat .tar ZIP, nebo. tar.gz souboru.</span><span class="sxs-lookup"><span data-stu-id="619f8-111">This should be a .tar, .zip, or .tar.gz file.</span></span> |
| <span data-ttu-id="619f8-112">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="619f8-112">DestinationPath</span></span>| <span data-ttu-id="619f8-113">Určuje umístění, ve které chcete zajistit, aby že extrahování obsahu archivu.</span><span class="sxs-lookup"><span data-stu-id="619f8-113">Specifies the location where you want to ensure the archive contents are extracted.</span></span>|
| <span data-ttu-id="619f8-114">Kontrolní součet</span><span class="sxs-lookup"><span data-stu-id="619f8-114">Checksum</span></span>| <span data-ttu-id="619f8-115">Definuje typ, který má použít při určování, zda byl aktualizován archivu zdroje.</span><span class="sxs-lookup"><span data-stu-id="619f8-115">Defines the type to use when determining whether the source archive has been updated.</span></span> <span data-ttu-id="619f8-116">Hodnoty jsou: "ctime", "mtime" nebo "md5".</span><span class="sxs-lookup"><span data-stu-id="619f8-116">Values are: "ctime", "mtime", or "md5".</span></span> <span data-ttu-id="619f8-117">Výchozí hodnota je "md5".</span><span class="sxs-lookup"><span data-stu-id="619f8-117">The default value is "md5".</span></span>|
| <span data-ttu-id="619f8-118">Force</span><span class="sxs-lookup"><span data-stu-id="619f8-118">Force</span></span>| <span data-ttu-id="619f8-119">Určité operace se soubory (například soubor přepsání nebo odstranění adresáře, který není prázdný) dojde chybě.</span><span class="sxs-lookup"><span data-stu-id="619f8-119">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="619f8-120">Použití **platnost** vlastnost potlačuje tyto chyby.</span><span class="sxs-lookup"><span data-stu-id="619f8-120">Using the **Force** property overrides such errors.</span></span> <span data-ttu-id="619f8-121">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="619f8-121">The default value is **$false**.</span></span>|
| <span data-ttu-id="619f8-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="619f8-122">DependsOn</span></span> | <span data-ttu-id="619f8-123">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="619f8-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="619f8-124">Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="619f8-124">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="619f8-125">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="619f8-125">Ensure</span></span>| <span data-ttu-id="619f8-126">Určuje, jestli se má zkontrolovat, zda obsah archivu existuje na **cílové**.</span><span class="sxs-lookup"><span data-stu-id="619f8-126">Determines whether to check if the content of the archive exists at the **Destination**.</span></span> <span data-ttu-id="619f8-127">Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že existuje obsah.</span><span class="sxs-lookup"><span data-stu-id="619f8-127">Set this property to "Present" to ensure the contents exist.</span></span> <span data-ttu-id="619f8-128">Nastavte ho na "Chybí" Ujistěte se, že neexistují.</span><span class="sxs-lookup"><span data-stu-id="619f8-128">Set it to "Absent" to ensure they do not exist.</span></span> <span data-ttu-id="619f8-129">Výchozí hodnota je "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="619f8-129">The default value is "Present".</span></span>|

## <a name="example"></a><span data-ttu-id="619f8-130">Příklad</span><span class="sxs-lookup"><span data-stu-id="619f8-130">Example</span></span>

<span data-ttu-id="619f8-131">Následující příklad ukazuje způsob použití **nxArchive** prostředků k zajištění, že obsah souboru archivu volat `website.tar` existují a jsou extrahovány na určitého cíle.</span><span class="sxs-lookup"><span data-stu-id="619f8-131">The following example shows how to use the **nxArchive** resource to ensure that the contents of an archive file called `website.tar` exist and are extracted at a given destination.</span></span>

```
Import-DSCResource -Module nx

nxFile SyncArchiveFromWeb
{
   Ensure = "Present"
   SourcePath = “http://release.contoso.com/releases/website.tar”
   DestinationPath = "/usr/release/staging/website.tar"
   Type = "File"
   Checksum = “mtime”
}

nxArchive SyncWebDir
{
   SourcePath = “/usr/release/staging/website.tar”
   DestinationPath = “/usr/local/apache2/htdocs/”
   Force = $false
   DependsOn = "[nxFile]SyncArchiveFromWeb"
}
```