---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC pro Linux nxSshAuthorizedKeys prostředků"
ms.openlocfilehash: f48ecec39ffe24cee99ca08ad9d050b36c5e04bf
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-for-linux-nxsshauthorizedkeys-resource"></a><span data-ttu-id="da0af-103">DSC pro Linux nxSshAuthorizedKeys prostředků</span><span class="sxs-lookup"><span data-stu-id="da0af-103">DSC for Linux nxSshAuthorizedKeys Resource</span></span>

<span data-ttu-id="da0af-104">**NxAuthorizedKeys** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě oprávnění ssh klíče pro zadaného uživatele.</span><span class="sxs-lookup"><span data-stu-id="da0af-104">The **nxAuthorizedKeys** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage authorized ssh keys for a specified user.</span></span>

## <a name="syntax"></a><span data-ttu-id="da0af-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="da0af-105">Syntax</span></span>

```
nxAuthorizedKeys <string> #ResourceName
{
    KeyComment = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Username = <string> ]
    [ Key = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="da0af-106">Properties</span><span class="sxs-lookup"><span data-stu-id="da0af-106">Properties</span></span>

|  <span data-ttu-id="da0af-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="da0af-107">Property</span></span> |  <span data-ttu-id="da0af-108">Popis</span><span class="sxs-lookup"><span data-stu-id="da0af-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="da0af-109">KeyComment</span><span class="sxs-lookup"><span data-stu-id="da0af-109">KeyComment</span></span>| <span data-ttu-id="da0af-110">Komentář jedinečné klíče.</span><span class="sxs-lookup"><span data-stu-id="da0af-110">A unique comment for the key.</span></span> <span data-ttu-id="da0af-111">Slouží k jednoznačné identifikaci klíče.</span><span class="sxs-lookup"><span data-stu-id="da0af-111">This is used to uniquely identify keys.</span></span>| 
| <span data-ttu-id="da0af-112">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="da0af-112">Ensure</span></span>| <span data-ttu-id="da0af-113">Určuje, zda je klíč definován.</span><span class="sxs-lookup"><span data-stu-id="da0af-113">Specifies whether the key is defined.</span></span> <span data-ttu-id="da0af-114">Nastavením této vlastnosti "Chybí" zajistěte, aby byl že klíč neexistuje v souboru oprávnění klíče uživatele.</span><span class="sxs-lookup"><span data-stu-id="da0af-114">Set this property to "Absent" to ensure the key does not exist in the user’s authorized keys file.</span></span> <span data-ttu-id="da0af-115">Nastavte ji na "Přítomen" zajistěte, aby byl že klíč je definována v souboru klíče autorizované uživatele.</span><span class="sxs-lookup"><span data-stu-id="da0af-115">Set it to "Present" to ensure the key is defined in the user’s authorized key file.</span></span>| 
| <span data-ttu-id="da0af-116">Uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="da0af-116">Username</span></span>| <span data-ttu-id="da0af-117">Uživatelské jméno ssh spravovat oprávnění klíče pro.</span><span class="sxs-lookup"><span data-stu-id="da0af-117">The username to manage ssh authorized keys for.</span></span> <span data-ttu-id="da0af-118">Pokud není definován, je výchozí uživatel "kořenový".</span><span class="sxs-lookup"><span data-stu-id="da0af-118">If not defined, the default user is "root".</span></span>| 
| <span data-ttu-id="da0af-119">Klávesa</span><span class="sxs-lookup"><span data-stu-id="da0af-119">Key</span></span>| <span data-ttu-id="da0af-120">Obsah klíče.</span><span class="sxs-lookup"><span data-stu-id="da0af-120">The contents of the key.</span></span> <span data-ttu-id="da0af-121">To je potřeba, pokud **zajistěte, aby** je nastaven na "Dispozici".</span><span class="sxs-lookup"><span data-stu-id="da0af-121">This is required if **Ensure** is set to "Present".</span></span>| 
| <span data-ttu-id="da0af-122">dependsOn</span><span class="sxs-lookup"><span data-stu-id="da0af-122">DependsOn</span></span> | <span data-ttu-id="da0af-123">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="da0af-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="da0af-124">Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="da0af-124">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="example"></a><span data-ttu-id="da0af-125">Příklad</span><span class="sxs-lookup"><span data-stu-id="da0af-125">Example</span></span>

<span data-ttu-id="da0af-126">V následujícím příkladu definuje oprávnění ssh veřejné klíče pro uživatele "monuser".</span><span class="sxs-lookup"><span data-stu-id="da0af-126">The following example defines a public ssh authorized key for the user "monuser".</span></span>

```
Import-DSCResource -Module nx 

Node $node {

nxSshAuthorizedKeys myKey{
   KeyComment = "myKey"
   Ensure = "Present"
   Key = 'ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEA0b+0xSd07QXRifm3FXj7Pn/DblA6QI5VAkDm6OivFzj3U6qGD1VJ6AAxWPCyMl/qhtpRtxZJDu/TxD8AyZNgc8aN2CljN1hOMbBRvH2q5QPf/nCnnJRaGsrxIqZjyZdYo9ZEEzjZUuMDM5HI1LA9B99k/K6PK2Bc1NLivpu7nbtVG2tLOQs+GefsnHuetsRMwo/+c3LtwYm9M0XfkGjYVCLO4CoFuSQpvX6AB3TedUy6NZ0iuxC0kRGg1rIQTwSRcw+McLhslF0drs33fw6tYdzlLBnnzimShMuiDWiT37WqCRovRGYrGCaEFGTG2e0CN8Co8nryXkyWc6NSDNpMzw== rsa-key-20150401'
   UserName = "monuser"
} 
}
```

