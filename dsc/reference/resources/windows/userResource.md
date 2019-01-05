---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC uživatele
ms.openlocfilehash: 04543351df19160a2da05ccea96e5d392d8c55bf
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048209"
---
# <a name="dsc-user-resource"></a><span data-ttu-id="e6082-103">Prostředek DSC uživatele</span><span class="sxs-lookup"><span data-stu-id="e6082-103">DSC User Resource</span></span>

<span data-ttu-id="e6082-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e6082-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="e6082-105">**Uživatele** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě místních uživatelských účtů na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="e6082-105">The **User** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local user accounts on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="e6082-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e6082-106">Syntax</span></span>

```
User [string] #ResourceName
{
    UserName = [string]
    [ Description = [string] ]
    [ Disabled = [bool] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ FullName = [string] ]
    [ Password = [PSCredential] ]
    [ PasswordChangeNotAllowed = [bool] ]
    [ PasswordChangeRequired = [bool] ]
    [ PasswordNeverExpires = [bool] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="e6082-107">Properties</span><span class="sxs-lookup"><span data-stu-id="e6082-107">Properties</span></span>

|  <span data-ttu-id="e6082-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="e6082-108">Property</span></span>  |  <span data-ttu-id="e6082-109">Popis</span><span class="sxs-lookup"><span data-stu-id="e6082-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="e6082-110">UserName</span><span class="sxs-lookup"><span data-stu-id="e6082-110">UserName</span></span>| <span data-ttu-id="e6082-111">Určuje název účtu, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="e6082-111">Indicates the account name for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="e6082-112">Popis</span><span class="sxs-lookup"><span data-stu-id="e6082-112">Description</span></span>| <span data-ttu-id="e6082-113">Určuje popis, který chcete použít pro uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="e6082-113">Indicates the description you want to use for the user account.</span></span>|
| <span data-ttu-id="e6082-114">Zakázáno</span><span class="sxs-lookup"><span data-stu-id="e6082-114">Disabled</span></span>| <span data-ttu-id="e6082-115">Označuje, zda je účet povolen.</span><span class="sxs-lookup"><span data-stu-id="e6082-115">Indicates if the account is enabled.</span></span> <span data-ttu-id="e6082-116">Tuto vlastnost nastavte na `$true` zajistit, že tento účet je zakázaný a nastavte ho na `$false` ujistěte, že je povolena.</span><span class="sxs-lookup"><span data-stu-id="e6082-116">Set this property to `$true` to ensure that this account is disabled, and set it to `$false` to ensure that it is enabled.</span></span>|
| <span data-ttu-id="e6082-117">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="e6082-117">Ensure</span></span>| <span data-ttu-id="e6082-118">Určuje, jestli účet existuje.</span><span class="sxs-lookup"><span data-stu-id="e6082-118">Indicates if the account exists.</span></span> <span data-ttu-id="e6082-119">Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že existuje účet a nastavte ho na "Chybí" Ujistěte se, že účet neexistuje.</span><span class="sxs-lookup"><span data-stu-id="e6082-119">Set this property to "Present" to ensure that the account exists, and set it to "Absent" to ensure that the account does not exist.</span></span>|
| <span data-ttu-id="e6082-120">Jméno a příjmení</span><span class="sxs-lookup"><span data-stu-id="e6082-120">FullName</span></span>| <span data-ttu-id="e6082-121">Představuje řetězec s úplný název, který chcete použít pro uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="e6082-121">Represents a string with the full name you want to use for the user account.</span></span>|
| <span data-ttu-id="e6082-122">Heslo</span><span class="sxs-lookup"><span data-stu-id="e6082-122">Password</span></span>| <span data-ttu-id="e6082-123">Určuje heslo, které chcete použít pro tento účet.</span><span class="sxs-lookup"><span data-stu-id="e6082-123">Indicates the password you want to use for this account.</span></span> |
| <span data-ttu-id="e6082-124">PasswordChangeNotAllowed</span><span class="sxs-lookup"><span data-stu-id="e6082-124">PasswordChangeNotAllowed</span></span>| <span data-ttu-id="e6082-125">Označuje, pokud uživatel může změnit heslo.</span><span class="sxs-lookup"><span data-stu-id="e6082-125">Indicates if the user can change the password.</span></span> <span data-ttu-id="e6082-126">Tuto vlastnost nastavte na `$true` zajistit, že uživatel nemůže změnit heslo a nastavte ho na `$false` aby uživatel mohl změnit heslo.</span><span class="sxs-lookup"><span data-stu-id="e6082-126">Set this property to `$true` to ensure that the user cannot change the password, and set it to `$false` to allow the user to change the password.</span></span> <span data-ttu-id="e6082-127">Výchozí hodnota je `$false`.</span><span class="sxs-lookup"><span data-stu-id="e6082-127">The default value is `$false`.</span></span>|
| <span data-ttu-id="e6082-128">PasswordChangeRequired</span><span class="sxs-lookup"><span data-stu-id="e6082-128">PasswordChangeRequired</span></span>| <span data-ttu-id="e6082-129">Označuje, pokud uživatel musí změnit heslo při příštím přihlašování.</span><span class="sxs-lookup"><span data-stu-id="e6082-129">Indicates if the user must change the password at the next sign in.</span></span> <span data-ttu-id="e6082-130">Tuto vlastnost nastavte na `$true` Pokud musí uživatel změnit heslo.</span><span class="sxs-lookup"><span data-stu-id="e6082-130">Set this property to `$true` if the user must change the password.</span></span> <span data-ttu-id="e6082-131">Výchozí hodnota je `$true`.</span><span class="sxs-lookup"><span data-stu-id="e6082-131">The default value is `$true`.</span></span>|
| <span data-ttu-id="e6082-132">PasswordNeverExpires</span><span class="sxs-lookup"><span data-stu-id="e6082-132">PasswordNeverExpires</span></span>| <span data-ttu-id="e6082-133">Označuje, pokud vyprší platnost hesla.</span><span class="sxs-lookup"><span data-stu-id="e6082-133">Indicates if the password will expire.</span></span> <span data-ttu-id="e6082-134">K zajištění, že heslo pro tento účet nikdy nevyprší, nastavte tuto vlastnost na `$true`a nastavte ho na `$false` Pokud vyprší platnost hesla.</span><span class="sxs-lookup"><span data-stu-id="e6082-134">To ensure that the password for this account will never expire, set this property to `$true`, and set it to `$false` if the password will expire.</span></span> <span data-ttu-id="e6082-135">Výchozí hodnota je `$false`.</span><span class="sxs-lookup"><span data-stu-id="e6082-135">The default value is `$false`.</span></span>|
| <span data-ttu-id="e6082-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="e6082-136">DependsOn</span></span> | <span data-ttu-id="e6082-137">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="e6082-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="e6082-138">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="e6082-138">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="e6082-139">Příklad</span><span class="sxs-lookup"><span data-stu-id="e6082-139">Example</span></span>

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = "[Group]GroupExample" # Configures GroupExample first
}
```