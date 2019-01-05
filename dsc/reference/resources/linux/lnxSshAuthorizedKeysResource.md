---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxSshAuthorizedKeys
ms.openlocfilehash: d4cdb727a94a5e89e8401769f24977d49bcf4929
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048208"
---
# <a name="dsc-for-linux-nxsshauthorizedkeys-resource"></a><span data-ttu-id="98d90-103">DSC pro Linux prostředek nxSshAuthorizedKeys</span><span class="sxs-lookup"><span data-stu-id="98d90-103">DSC for Linux nxSshAuthorizedKeys Resource</span></span>

<span data-ttu-id="98d90-104">**NxAuthorizedKeys** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě oprávnění ssh klíče pro zadaného uživatele.</span><span class="sxs-lookup"><span data-stu-id="98d90-104">The **nxAuthorizedKeys** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage authorized ssh keys for a specified user.</span></span>

## <a name="syntax"></a><span data-ttu-id="98d90-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="98d90-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="98d90-106">Properties</span><span class="sxs-lookup"><span data-stu-id="98d90-106">Properties</span></span>

|  <span data-ttu-id="98d90-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="98d90-107">Property</span></span> |  <span data-ttu-id="98d90-108">Popis</span><span class="sxs-lookup"><span data-stu-id="98d90-108">Description</span></span> |
|---|---|
| <span data-ttu-id="98d90-109">KeyComment</span><span class="sxs-lookup"><span data-stu-id="98d90-109">KeyComment</span></span>| <span data-ttu-id="98d90-110">Komentář jedinečné klíče.</span><span class="sxs-lookup"><span data-stu-id="98d90-110">A unique comment for the key.</span></span> <span data-ttu-id="98d90-111">Slouží k jednoznačné identifikaci klíče.</span><span class="sxs-lookup"><span data-stu-id="98d90-111">This is used to uniquely identify keys.</span></span>|
| <span data-ttu-id="98d90-112">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="98d90-112">Ensure</span></span>| <span data-ttu-id="98d90-113">Určuje, zda je definován klíč.</span><span class="sxs-lookup"><span data-stu-id="98d90-113">Specifies whether the key is defined.</span></span> <span data-ttu-id="98d90-114">Nastavte tuto vlastnost na "Chybí" Ujistěte se, že klíč v souboru autorizovaných klíčů uživatele neexistuje.</span><span class="sxs-lookup"><span data-stu-id="98d90-114">Set this property to "Absent" to ensure the key does not exist in the user’s authorized keys file.</span></span> <span data-ttu-id="98d90-115">Nastavte ho na "Obsahuje" Ujistěte se, že klíč je definována v souboru klíče autorizované uživatele.</span><span class="sxs-lookup"><span data-stu-id="98d90-115">Set it to "Present" to ensure the key is defined in the user’s authorized key file.</span></span>|
| <span data-ttu-id="98d90-116">Uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="98d90-116">Username</span></span>| <span data-ttu-id="98d90-117">Uživatelské jméno ssh spravovat oprávnění klíče.</span><span class="sxs-lookup"><span data-stu-id="98d90-117">The username to manage ssh authorized keys for.</span></span> <span data-ttu-id="98d90-118">Pokud není definován, je výchozí uživatel "root".</span><span class="sxs-lookup"><span data-stu-id="98d90-118">If not defined, the default user is "root".</span></span>|
| <span data-ttu-id="98d90-119">Klávesa</span><span class="sxs-lookup"><span data-stu-id="98d90-119">Key</span></span>| <span data-ttu-id="98d90-120">Obsah klíče.</span><span class="sxs-lookup"><span data-stu-id="98d90-120">The contents of the key.</span></span> <span data-ttu-id="98d90-121">To je potřeba, pokud **Ujistěte se, že** je nastavena na "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="98d90-121">This is required if **Ensure** is set to "Present".</span></span>|
| <span data-ttu-id="98d90-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="98d90-122">DependsOn</span></span> | <span data-ttu-id="98d90-123">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="98d90-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="98d90-124">Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="98d90-124">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="98d90-125">Příklad</span><span class="sxs-lookup"><span data-stu-id="98d90-125">Example</span></span>

<span data-ttu-id="98d90-126">Následující příklad definuje oprávnění ssh veřejné klíče pro uživatele "monuser".</span><span class="sxs-lookup"><span data-stu-id="98d90-126">The following example defines a public ssh authorized key for the user "monuser".</span></span>

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