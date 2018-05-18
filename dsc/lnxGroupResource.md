---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: DSC pro Linux nxGroup prostředků
ms.openlocfilehash: 9651f3affc9b040a7ef8e7bf8d5ab4cebcca8128
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="dsc-for-linux-nxgroup-resource"></a><span data-ttu-id="fba3b-103">DSC pro Linux nxGroup prostředků</span><span class="sxs-lookup"><span data-stu-id="fba3b-103">DSC for Linux nxGroup Resource</span></span>

<span data-ttu-id="fba3b-104">**NxGroup** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě místních skupin na uzlu Linux.</span><span class="sxs-lookup"><span data-stu-id="fba3b-104">The **nxGroup** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="fba3b-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="fba3b-105">Syntax</span></span>

```powershell
nxGroup <string> #ResourceName
{
    GroupName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Members = <string[]> ]
    [ MebersToInclude = <string[]>]
    [ MembersToExclude = <string[]> ]
    [ DependsOn = <string[]> ]
}

```

## <a name="properties"></a><span data-ttu-id="fba3b-106">Properties</span><span class="sxs-lookup"><span data-stu-id="fba3b-106">Properties</span></span>

|  <span data-ttu-id="fba3b-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="fba3b-107">Property</span></span> |  <span data-ttu-id="fba3b-108">Popis</span><span class="sxs-lookup"><span data-stu-id="fba3b-108">Description</span></span> |
|---|---|
| <span data-ttu-id="fba3b-109">Název skupiny</span><span class="sxs-lookup"><span data-stu-id="fba3b-109">GroupName</span></span>| <span data-ttu-id="fba3b-110">Určuje název skupiny, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="fba3b-110">Specifies the name of the group for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="fba3b-111">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="fba3b-111">Ensure</span></span>| <span data-ttu-id="fba3b-112">Určuje, jestli se má zkontrolovat, zda skupina existuje.</span><span class="sxs-lookup"><span data-stu-id="fba3b-112">Determines whether to check if the group exists.</span></span> <span data-ttu-id="fba3b-113">Nastavením této vlastnosti "Přítomen" Ujistěte se, že existuje daná skupina.</span><span class="sxs-lookup"><span data-stu-id="fba3b-113">Set this property to "Present" to ensure the group exists.</span></span> <span data-ttu-id="fba3b-114">Nastavte ji na "Chybí" Ujistěte se, že že skupina neexistuje.</span><span class="sxs-lookup"><span data-stu-id="fba3b-114">Set it to "Absent" to ensure the group does not exist.</span></span> <span data-ttu-id="fba3b-115">Výchozí hodnota je "Dispozici".</span><span class="sxs-lookup"><span data-stu-id="fba3b-115">The default value is "Present".</span></span>|
| <span data-ttu-id="fba3b-116">Členové</span><span class="sxs-lookup"><span data-stu-id="fba3b-116">Members</span></span>| <span data-ttu-id="fba3b-117">Určuje členů, které tvoří skupinu.</span><span class="sxs-lookup"><span data-stu-id="fba3b-117">Specifies the members that form the group.</span></span>|
| <span data-ttu-id="fba3b-118">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="fba3b-118">MembersToInclude</span></span>| <span data-ttu-id="fba3b-119">Určuje, že uživatelé, kteří chcete zajistit jsou členy skupiny.</span><span class="sxs-lookup"><span data-stu-id="fba3b-119">Specifies the users who you want to ensure are members of the group.</span></span>|
| <span data-ttu-id="fba3b-120">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="fba3b-120">MembersToExclude</span></span>| <span data-ttu-id="fba3b-121">Určuje, že uživatelé, kteří chcete zajistit nejsou členy skupiny.</span><span class="sxs-lookup"><span data-stu-id="fba3b-121">Specifies the users who you want to ensure are not members of the group.</span></span>|
| <span data-ttu-id="fba3b-122">PreferredGroupID</span><span class="sxs-lookup"><span data-stu-id="fba3b-122">PreferredGroupID</span></span>| <span data-ttu-id="fba3b-123">Pokud je to možné nastaví na zadanou hodnotu id skupiny.</span><span class="sxs-lookup"><span data-stu-id="fba3b-123">Sets the group id to the provided value if possible.</span></span> <span data-ttu-id="fba3b-124">Pokud id skupiny je aktuálně používán, použije se další id skupiny k dispozici.</span><span class="sxs-lookup"><span data-stu-id="fba3b-124">If the group id is currently in use, the next available group id is used.</span></span>|
| <span data-ttu-id="fba3b-125">dependsOn</span><span class="sxs-lookup"><span data-stu-id="fba3b-125">DependsOn</span></span> | <span data-ttu-id="fba3b-126">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="fba3b-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="fba3b-127">Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="fba3b-127">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="fba3b-128">Příklad</span><span class="sxs-lookup"><span data-stu-id="fba3b-128">Example</span></span>

<span data-ttu-id="fba3b-129">Následující příklad zajistí, že uživatel "monuser" existuje a je členem skupiny "DBusers".</span><span class="sxs-lookup"><span data-stu-id="fba3b-129">The following example ensures that the user “monuser” exists and is a member of the group "DBusers".</span></span>

```
Import-DSCResource -Module nx

Node $node {

nxUser UserExample{
   UserName = "monuser"
   Description = "Monitoring user"
   Password  =    '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
   Ensure = "Present"
   HomeDirectory = "/home/monuser"
}

nxGroup GroupExample{
   GroupName = "DBusers"
   Ensure = "Present"
   MembersToInclude = "monuser"
   DependsOn = "[nxUser]UserExample"
}
}
```