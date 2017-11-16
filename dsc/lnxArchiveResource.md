---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC pro Linux nxArchive prostředků"
ms.openlocfilehash: da647432e14d2a4a3ceb2a36c7dee2dbfd350116
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-for-linux-nxarchive-resource"></a><span data-ttu-id="63bdf-103">DSC pro Linux nxArchive prostředků</span><span class="sxs-lookup"><span data-stu-id="63bdf-103">DSC for Linux nxArchive Resource</span></span>

<span data-ttu-id="63bdf-104">**NxArchive** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus rozbalte soubory archivu (.tar, .zip) v určité cesty na uzlu Linux.</span><span class="sxs-lookup"><span data-stu-id="63bdf-104">The **nxArchive** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to unpack archive (.tar, .zip) files at a specific path on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="63bdf-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="63bdf-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="63bdf-106">Properties</span><span class="sxs-lookup"><span data-stu-id="63bdf-106">Properties</span></span>

|  <span data-ttu-id="63bdf-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="63bdf-107">Property</span></span> |  <span data-ttu-id="63bdf-108">Popis</span><span class="sxs-lookup"><span data-stu-id="63bdf-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="63bdf-109">Zdrojová cesta</span><span class="sxs-lookup"><span data-stu-id="63bdf-109">SourcePath</span></span>| <span data-ttu-id="63bdf-110">Určuje zdroj cestu k souboru archivu.</span><span class="sxs-lookup"><span data-stu-id="63bdf-110">Specifies the source path of the archive file.</span></span> <span data-ttu-id="63bdf-111">Měl by být .tar, .zip, nebo. tar.gz souboru.</span><span class="sxs-lookup"><span data-stu-id="63bdf-111">This should be a .tar, .zip, or .tar.gz file.</span></span> | 
| <span data-ttu-id="63bdf-112">Cílová_cesta</span><span class="sxs-lookup"><span data-stu-id="63bdf-112">DestinationPath</span></span>| <span data-ttu-id="63bdf-113">Určuje umístění, kam chcete zajistit, aby že se extrahují obsah archivu.</span><span class="sxs-lookup"><span data-stu-id="63bdf-113">Specifies the location where you want to ensure the archive contents are extracted.</span></span>| 
| <span data-ttu-id="63bdf-114">Kontrolní součet</span><span class="sxs-lookup"><span data-stu-id="63bdf-114">Checksum</span></span>| <span data-ttu-id="63bdf-115">Definuje typ, který má použít při určování, zda byly aktualizovány archivu zdroje.</span><span class="sxs-lookup"><span data-stu-id="63bdf-115">Defines the type to use when determining whether the source archive has been updated.</span></span> <span data-ttu-id="63bdf-116">Hodnoty: "ctime", "mtime" nebo "md5".</span><span class="sxs-lookup"><span data-stu-id="63bdf-116">Values are: "ctime", "mtime", or "md5".</span></span> <span data-ttu-id="63bdf-117">Výchozí hodnota je "md5".</span><span class="sxs-lookup"><span data-stu-id="63bdf-117">The default value is "md5".</span></span>| 
| <span data-ttu-id="63bdf-118">Force</span><span class="sxs-lookup"><span data-stu-id="63bdf-118">Force</span></span>| <span data-ttu-id="63bdf-119">Některé operace souboru (například přepsání souboru nebo odstranění adresáře, který není prázdný) bude výsledkem chyba.</span><span class="sxs-lookup"><span data-stu-id="63bdf-119">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="63bdf-120">Pomocí **Force** vlastnost má přednost před takové chyby.</span><span class="sxs-lookup"><span data-stu-id="63bdf-120">Using the **Force** property overrides such errors.</span></span> <span data-ttu-id="63bdf-121">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="63bdf-121">The default value is **$false**.</span></span>| 
| <span data-ttu-id="63bdf-122">dependsOn</span><span class="sxs-lookup"><span data-stu-id="63bdf-122">DependsOn</span></span> | <span data-ttu-id="63bdf-123">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="63bdf-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="63bdf-124">Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="63bdf-124">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
| <span data-ttu-id="63bdf-125">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="63bdf-125">Ensure</span></span>| <span data-ttu-id="63bdf-126">Určuje, jestli se má zkontrolovat, zda existuje obsah archivu v **cílový**.</span><span class="sxs-lookup"><span data-stu-id="63bdf-126">Determines whether to check if the content of the archive exists at the **Destination**.</span></span> <span data-ttu-id="63bdf-127">Nastavením této vlastnosti "Přítomen" Ujistěte se, že existuje obsah.</span><span class="sxs-lookup"><span data-stu-id="63bdf-127">Set this property to "Present" to ensure the contents exist.</span></span> <span data-ttu-id="63bdf-128">Nastavte ji na "Chybí" Ujistěte se, že neexistují.</span><span class="sxs-lookup"><span data-stu-id="63bdf-128">Set it to "Absent" to ensure they do not exist.</span></span> <span data-ttu-id="63bdf-129">Výchozí hodnota je "Dispozici".</span><span class="sxs-lookup"><span data-stu-id="63bdf-129">The default value is "Present".</span></span>| 

## <a name="example"></a><span data-ttu-id="63bdf-130">Příklad</span><span class="sxs-lookup"><span data-stu-id="63bdf-130">Example</span></span>

<span data-ttu-id="63bdf-131">Následující příklad ukazuje, jak používat **nxArchive** prostředek se má zajistit, aby obsah souboru archivu volána `website.tar` existují a jsou extrahovány na daný cíl.</span><span class="sxs-lookup"><span data-stu-id="63bdf-131">The following example shows how to use the **nxArchive** resource to ensure that the contents of an archive file called `website.tar` exist and are extracted at a given destination.</span></span>

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
