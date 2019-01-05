---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxGroup
ms.openlocfilehash: c61b6ab4a8c56d085b5297dcfc7582187d54f946
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048198"
---
# <a name="dsc-for-linux-nxgroup-resource"></a><span data-ttu-id="4f555-103">DSC pro Linux prostředek nxGroup</span><span class="sxs-lookup"><span data-stu-id="4f555-103">DSC for Linux nxGroup Resource</span></span>

<span data-ttu-id="4f555-104">**NxGroup** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě místních skupin na uzlu systému Linux.</span><span class="sxs-lookup"><span data-stu-id="4f555-104">The **nxGroup** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="4f555-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="4f555-105">Syntax</span></span>

```
nxGroup <string> #ResourceName
{
    GroupName = <string>
    [ Ensure = <string> { Absent | Present } ]
    [ Members = <string[]> ]
    [ MembersToInclude = <string[]> ]
    [ MembersToExclude = <string[]> ]
    [ DependsOn = <string[]> ]
}
```

## <a name="properties"></a><span data-ttu-id="4f555-106">Properties</span><span class="sxs-lookup"><span data-stu-id="4f555-106">Properties</span></span>

|  <span data-ttu-id="4f555-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="4f555-107">Property</span></span> |  <span data-ttu-id="4f555-108">Popis</span><span class="sxs-lookup"><span data-stu-id="4f555-108">Description</span></span> |
|---|---|
| <span data-ttu-id="4f555-109">Název skupiny</span><span class="sxs-lookup"><span data-stu-id="4f555-109">GroupName</span></span>| <span data-ttu-id="4f555-110">Určuje název skupiny, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="4f555-110">Specifies the name of the group for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="4f555-111">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="4f555-111">Ensure</span></span>| <span data-ttu-id="4f555-112">Určuje, jestli se má zkontrolovat, zda skupina existuje.</span><span class="sxs-lookup"><span data-stu-id="4f555-112">Determines whether to check if the group exists.</span></span> <span data-ttu-id="4f555-113">Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že tato skupina existuje.</span><span class="sxs-lookup"><span data-stu-id="4f555-113">Set this property to "Present" to ensure the group exists.</span></span> <span data-ttu-id="4f555-114">Nastavte ho na "Chybí" Ujistěte se, že že skupina neexistuje.</span><span class="sxs-lookup"><span data-stu-id="4f555-114">Set it to "Absent" to ensure the group does not exist.</span></span> <span data-ttu-id="4f555-115">Výchozí hodnota je "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="4f555-115">The default value is "Present".</span></span>|
| <span data-ttu-id="4f555-116">Členové</span><span class="sxs-lookup"><span data-stu-id="4f555-116">Members</span></span>| <span data-ttu-id="4f555-117">Určuje členy, které tvoří skupinu.</span><span class="sxs-lookup"><span data-stu-id="4f555-117">Specifies the members that form the group.</span></span>|
| <span data-ttu-id="4f555-118">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="4f555-118">MembersToInclude</span></span>| <span data-ttu-id="4f555-119">Určuje, že budete muset zajistit, aby uživatelé jsou členy skupiny.</span><span class="sxs-lookup"><span data-stu-id="4f555-119">Specifies the users who you want to ensure are members of the group.</span></span>|
| <span data-ttu-id="4f555-120">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="4f555-120">MembersToExclude</span></span>| <span data-ttu-id="4f555-121">Určuje, že budete muset zajistit, aby uživatelé nejsou členy skupiny.</span><span class="sxs-lookup"><span data-stu-id="4f555-121">Specifies the users who you want to ensure are not members of the group.</span></span>|
| <span data-ttu-id="4f555-122">PreferredGroupID</span><span class="sxs-lookup"><span data-stu-id="4f555-122">PreferredGroupID</span></span>| <span data-ttu-id="4f555-123">Pokud je to možné nastaví id skupiny na zadanou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="4f555-123">Sets the group id to the provided value if possible.</span></span> <span data-ttu-id="4f555-124">Pokud id skupiny je aktuálně používán, použije se další id skupiny k dispozici.</span><span class="sxs-lookup"><span data-stu-id="4f555-124">If the group id is currently in use, the next available group id is used.</span></span>|
| <span data-ttu-id="4f555-125">DependsOn</span><span class="sxs-lookup"><span data-stu-id="4f555-125">DependsOn</span></span> | <span data-ttu-id="4f555-126">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="4f555-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="4f555-127">Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = '[ResourceType]ResourceName'`.</span><span class="sxs-lookup"><span data-stu-id="4f555-127">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = '[ResourceType]ResourceName'`.</span></span>|

## <a name="example"></a><span data-ttu-id="4f555-128">Příklad</span><span class="sxs-lookup"><span data-stu-id="4f555-128">Example</span></span>

<span data-ttu-id="4f555-129">Následující příklad zajistí, že uživatel monuser existuje a je členem skupiny "DBusers".</span><span class="sxs-lookup"><span data-stu-id="4f555-129">The following example ensures that the user 'monuser' exists and is a member of the group 'DBusers'.</span></span>

```powershell
Import-DSCResource -Module nx

Node $node {
    nxUser UserExample {
       UserName = 'monuser'
       Description = 'Monitoring user'
       Password = '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
       Ensure = 'Present'
       HomeDirectory = '/home/monuser'
    }

    nxGroup GroupExample {
       GroupName = 'DBusers'
       Ensure = 'Present'
       MembersToInclude = 'monuser'
       DependsOn = '[nxUser]UserExample'
    }
}
```