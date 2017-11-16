---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 4185d9395f2f3e5ba1c8daa0c365cb2bf322936b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="get-childitem-has--depth-parameter"></a><span data-ttu-id="527ad-102">Get-ChildItem má – hloubka parametr</span><span class="sxs-lookup"><span data-stu-id="527ad-102">Get-ChildItem has -Depth parameter</span></span>
<span data-ttu-id="527ad-103">**Get-ChildItem** má teď **– hloubka** parametr použijete s **– Recurse** omezit rekurze:</span><span class="sxs-lookup"><span data-stu-id="527ad-103">**Get-ChildItem** now has a **–Depth** parameter you use with **–Recurse** to limit the recursion:</span></span>

<span data-ttu-id="527ad-104">PS C:\\uživatelé\\slee\\stáhne\\příklad&gt; Get-ChildItem-Recurse - hloubka 0</span><span class="sxs-lookup"><span data-stu-id="527ad-104">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 0</span></span>

<span data-ttu-id="527ad-105">Adresář: C:\\uživatelé\\slee\\stáhne\\příklad</span><span class="sxs-lookup"><span data-stu-id="527ad-105">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="527ad-106">Název režimu LastWriteTime délka</span><span class="sxs-lookup"><span data-stu-id="527ad-106">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="527ad-107">d---Depth0 17:36:00 4 14. prosince 2015</span><span class="sxs-lookup"><span data-stu-id="527ad-107">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="527ad-108">-a---4/14. prosince 2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="527ad-108">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="527ad-109">-a---4/14. prosince 2015 1:19 PM 0 Soubor2.txt</span><span class="sxs-lookup"><span data-stu-id="527ad-109">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="527ad-110">-a---4/14. prosince 2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="527ad-110">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="527ad-111">PS C:\\uživatelé\\slee\\stáhne\\příklad&gt; Get-ChildItem-Recurse - hloubku 1</span><span class="sxs-lookup"><span data-stu-id="527ad-111">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 1</span></span>

<span data-ttu-id="527ad-112">Adresář: C:\\uživatelé\\slee\\stáhne\\příklad</span><span class="sxs-lookup"><span data-stu-id="527ad-112">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="527ad-113">Název režimu LastWriteTime délka</span><span class="sxs-lookup"><span data-stu-id="527ad-113">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="527ad-114">d---Depth0 17:36:00 4 14. prosince 2015</span><span class="sxs-lookup"><span data-stu-id="527ad-114">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="527ad-115">-a---4/14. prosince 2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="527ad-115">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="527ad-116">-a---4/14. prosince 2015 1:19 PM 0 Soubor2.txt</span><span class="sxs-lookup"><span data-stu-id="527ad-116">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="527ad-117">-a---4/14. prosince 2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="527ad-117">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="527ad-118">Adresář: C:\\uživatelé\\slee\\stáhne\\příklad\\Depth0</span><span class="sxs-lookup"><span data-stu-id="527ad-118">Directory: C:\\Users\\slee\\Downloads\\Example\\Depth0</span></span>

<span data-ttu-id="527ad-119">Název režimu LastWriteTime délka</span><span class="sxs-lookup"><span data-stu-id="527ad-119">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="527ad-120">d---Depth1 5:33 odp 4 14. prosince 2015</span><span class="sxs-lookup"><span data-stu-id="527ad-120">d----- 4/14/2015 5:33 PM Depth1</span></span>

