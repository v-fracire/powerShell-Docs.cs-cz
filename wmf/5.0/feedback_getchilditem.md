---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 62cccabd7c63c6ba928fc2bf8addd3d11483e90f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="get-childitem-has--depth-parameter"></a><span data-ttu-id="d28a8-102">Get-ChildItem má – hloubka parametr</span><span class="sxs-lookup"><span data-stu-id="d28a8-102">Get-ChildItem has -Depth parameter</span></span>
<span data-ttu-id="d28a8-103">**Get-ChildItem** má teď **– hloubka** parametr použijete s **– Recurse** omezit rekurze:</span><span class="sxs-lookup"><span data-stu-id="d28a8-103">**Get-ChildItem** now has a **–Depth** parameter you use with **–Recurse** to limit the recursion:</span></span>

<span data-ttu-id="d28a8-104">PS C:\\uživatelé\\slee\\stáhne\\příklad&gt; Get-ChildItem-Recurse - hloubka 0</span><span class="sxs-lookup"><span data-stu-id="d28a8-104">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 0</span></span>

<span data-ttu-id="d28a8-105">Adresář: C:\\uživatelé\\slee\\stáhne\\příklad</span><span class="sxs-lookup"><span data-stu-id="d28a8-105">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="d28a8-106">Název režimu LastWriteTime délka</span><span class="sxs-lookup"><span data-stu-id="d28a8-106">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="d28a8-107">d---Depth0 17:36:00 4 14. prosince 2015</span><span class="sxs-lookup"><span data-stu-id="d28a8-107">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="d28a8-108">-a---4/14. prosince 2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="d28a8-108">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="d28a8-109">-a---4/14. prosince 2015 1:19 PM 0 Soubor2.txt</span><span class="sxs-lookup"><span data-stu-id="d28a8-109">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="d28a8-110">-a---4/14. prosince 2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="d28a8-110">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="d28a8-111">PS C:\\uživatelé\\slee\\stáhne\\příklad&gt; Get-ChildItem-Recurse - hloubku 1</span><span class="sxs-lookup"><span data-stu-id="d28a8-111">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 1</span></span>

<span data-ttu-id="d28a8-112">Adresář: C:\\uživatelé\\slee\\stáhne\\příklad</span><span class="sxs-lookup"><span data-stu-id="d28a8-112">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="d28a8-113">Název režimu LastWriteTime délka</span><span class="sxs-lookup"><span data-stu-id="d28a8-113">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="d28a8-114">d---Depth0 17:36:00 4 14. prosince 2015</span><span class="sxs-lookup"><span data-stu-id="d28a8-114">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="d28a8-115">-a---4/14. prosince 2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="d28a8-115">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="d28a8-116">-a---4/14. prosince 2015 1:19 PM 0 Soubor2.txt</span><span class="sxs-lookup"><span data-stu-id="d28a8-116">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="d28a8-117">-a---4/14. prosince 2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="d28a8-117">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="d28a8-118">Adresář: C:\\uživatelé\\slee\\stáhne\\příklad\\Depth0</span><span class="sxs-lookup"><span data-stu-id="d28a8-118">Directory: C:\\Users\\slee\\Downloads\\Example\\Depth0</span></span>

<span data-ttu-id="d28a8-119">Název režimu LastWriteTime délka</span><span class="sxs-lookup"><span data-stu-id="d28a8-119">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="d28a8-120">d---Depth1 5:33 odp 4 14. prosince 2015</span><span class="sxs-lookup"><span data-stu-id="d28a8-120">d----- 4/14/2015 5:33 PM Depth1</span></span>