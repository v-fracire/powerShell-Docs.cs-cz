---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxUser
ms.openlocfilehash: 1b02be1559957585a2a1733630cb93440e8182f9
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048122"
---
# <a name="dsc-for-linux-nxuser-resource"></a><span data-ttu-id="47fe4-103">DSC pro Linux prostředek nxUser</span><span class="sxs-lookup"><span data-stu-id="47fe4-103">DSC for Linux nxUser Resource</span></span>

<span data-ttu-id="47fe4-104">**NxUser** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě místních uživatelů na uzlu systému Linux.</span><span class="sxs-lookup"><span data-stu-id="47fe4-104">The **nxUser** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage local users on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="47fe4-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="47fe4-105">Syntax</span></span>

```
nxUser <string> #ResourceName
{
    UserName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ FullName = <string> ]
    [ Description = <string> ]
    [ Password = <string> ]
    [ Disabled = <bool> ]
    [ PasswordChangeRequired = <bool> ]
    [ HomeDirectory = <string> ]
    [ GroupID = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="47fe4-106">Properties</span><span class="sxs-lookup"><span data-stu-id="47fe4-106">Properties</span></span>

|  <span data-ttu-id="47fe4-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="47fe4-107">Property</span></span> |  <span data-ttu-id="47fe4-108">Určuje název účtu, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="47fe4-108">Indicates the account name for which you want to ensure a specific state.</span></span> |
|---|---|
| <span data-ttu-id="47fe4-109">UserName</span><span class="sxs-lookup"><span data-stu-id="47fe4-109">UserName</span></span>| <span data-ttu-id="47fe4-110">Určuje umístění, kam chcete zajistit stavu pro soubor nebo adresář.</span><span class="sxs-lookup"><span data-stu-id="47fe4-110">Specifies the location where you want to ensure the state for a file or directory.</span></span>|
| <span data-ttu-id="47fe4-111">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="47fe4-111">Ensure</span></span>| <span data-ttu-id="47fe4-112">Určuje, jestli účet existuje.</span><span class="sxs-lookup"><span data-stu-id="47fe4-112">Specifies whether the account exists.</span></span> <span data-ttu-id="47fe4-113">Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že existuje účet a nastavte ho na "Chybí" Ujistěte se, že účet neexistuje.</span><span class="sxs-lookup"><span data-stu-id="47fe4-113">Set this property to "Present" to ensure that the account exists, and set it to "Absent" to ensure that the account does not exist.</span></span>|
| <span data-ttu-id="47fe4-114">Jméno a příjmení</span><span class="sxs-lookup"><span data-stu-id="47fe4-114">FullName</span></span>| <span data-ttu-id="47fe4-115">Řetězec obsahující úplný název pro uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="47fe4-115">A string that contains the full name to use for the user account.</span></span>|
| <span data-ttu-id="47fe4-116">Popis</span><span class="sxs-lookup"><span data-stu-id="47fe4-116">Description</span></span>| <span data-ttu-id="47fe4-117">Popis pro uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="47fe4-117">The description for the user account.</span></span>|
| <span data-ttu-id="47fe4-118">Heslo</span><span class="sxs-lookup"><span data-stu-id="47fe4-118">Password</span></span>| <span data-ttu-id="47fe4-119">Hodnota hash hesla uživatele ve formuláři vhodná pro počítače s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="47fe4-119">The hash of the users password in the appropriate form for the Linux computer.</span></span> <span data-ttu-id="47fe4-120">Obvykle je to solené SHA-256 nebo hodnoty hash SHA-512.</span><span class="sxs-lookup"><span data-stu-id="47fe4-120">Typically, this is a salted SHA-256, or SHA-512 hash.</span></span> <span data-ttu-id="47fe4-121">Debian a Ubuntu Linux tato hodnota dá vygenerovat pomocí příkazu mkpasswd.</span><span class="sxs-lookup"><span data-stu-id="47fe4-121">On Debian and Ubuntu Linux, this value can be generated with the mkpasswd command.</span></span> <span data-ttu-id="47fe4-122">Pro jiné distribuce Linuxu metoda crypt Crypt knihovny pro Python slouží ke generování hodnoty hash.</span><span class="sxs-lookup"><span data-stu-id="47fe4-122">For other Linux distros, the crypt method of Python’s Crypt library can be used to generate the hash.</span></span>|
| <span data-ttu-id="47fe4-123">Zakázáno</span><span class="sxs-lookup"><span data-stu-id="47fe4-123">Disabled</span></span>| <span data-ttu-id="47fe4-124">Určuje, zda je účet povolený.</span><span class="sxs-lookup"><span data-stu-id="47fe4-124">Indicates whether the account is enabled.</span></span> <span data-ttu-id="47fe4-125">Tuto vlastnost nastavte na **$true** zajistit, že tento účet je zakázaný a nastavte ho na **$false** ujistěte, že je povolena.</span><span class="sxs-lookup"><span data-stu-id="47fe4-125">Set this property to **$true** to ensure that this account is disabled, and set it to **$false** to ensure that it is enabled.</span></span>|
| <span data-ttu-id="47fe4-126">PasswordChangeRequired</span><span class="sxs-lookup"><span data-stu-id="47fe4-126">PasswordChangeRequired</span></span>| <span data-ttu-id="47fe4-127">Určuje, jestli uživatel může změnit heslo.</span><span class="sxs-lookup"><span data-stu-id="47fe4-127">Indicates whether the user can change the password.</span></span> <span data-ttu-id="47fe4-128">Tuto vlastnost nastavte na **$true** zajistit, že uživatel nemůže změnit heslo a nastavte ho na **$false** aby uživatel mohl změnit heslo.</span><span class="sxs-lookup"><span data-stu-id="47fe4-128">Set this property to **$true** to ensure that the user cannot change the password, and set it to **$false** to allow the user to change the password.</span></span> <span data-ttu-id="47fe4-129">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="47fe4-129">The default value is **$false**.</span></span> <span data-ttu-id="47fe4-130">Tato vlastnost je vyhodnocen pouze pokud uživatelský účet dříve neexistoval a se vytváří.</span><span class="sxs-lookup"><span data-stu-id="47fe4-130">This property is only evaluated if the user account did not exist previously and is being created.</span></span>|
| <span data-ttu-id="47fe4-131">Domovský_adresář</span><span class="sxs-lookup"><span data-stu-id="47fe4-131">HomeDirectory</span></span>| <span data-ttu-id="47fe4-132">Domovský adresář pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="47fe4-132">The home directory for the user.</span></span>|
| <span data-ttu-id="47fe4-133">ID skupiny</span><span class="sxs-lookup"><span data-stu-id="47fe4-133">GroupID</span></span>| <span data-ttu-id="47fe4-134">ID primární skupiny uživatele.</span><span class="sxs-lookup"><span data-stu-id="47fe4-134">The primary group ID for the user.</span></span>|
| <span data-ttu-id="47fe4-135">DependsOn</span><span class="sxs-lookup"><span data-stu-id="47fe4-135">DependsOn</span></span> | <span data-ttu-id="47fe4-136">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="47fe4-136">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="47fe4-137">Například pokud je ID bloku skriptu konfigurace prostředků, kterou chcete spustit nejprve "ResourceName" a její typ je "ResourceType", syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="47fe4-137">For example, if the ID of the resource configuration script block that you want to run first is "ResourceName" and its type is "ResourceType", the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="47fe4-138">Příklad</span><span class="sxs-lookup"><span data-stu-id="47fe4-138">Example</span></span>

<span data-ttu-id="47fe4-139">Následující příklad zajistí, že uživatel "monuser" existuje a je členem skupiny "DBusers".</span><span class="sxs-lookup"><span data-stu-id="47fe4-139">The following example ensures that the user "monuser" exists and is a member of the group "DBusers".</span></span>

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