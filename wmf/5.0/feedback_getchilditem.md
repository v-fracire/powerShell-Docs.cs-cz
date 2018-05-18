---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: d9f1ca10c948b06b234e17f688b8f899ed41c5d6
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="get-childitem-has--depth-parameter"></a><span data-ttu-id="0313a-102">Get-ChildItem má – hloubka parametr</span><span class="sxs-lookup"><span data-stu-id="0313a-102">Get-ChildItem has -Depth parameter</span></span>
<span data-ttu-id="0313a-103">**Get-ChildItem** má teď **– hloubka** parametr použijete s **– Recurse** omezit rekurze:</span><span class="sxs-lookup"><span data-stu-id="0313a-103">**Get-ChildItem** now has a **–Depth** parameter you use with **–Recurse** to limit the recursion:</span></span>

<span data-ttu-id="0313a-104">PS C:\\uživatelé\\slee\\stáhne\\příklad&gt; Get-ChildItem-Recurse - hloubka 0</span><span class="sxs-lookup"><span data-stu-id="0313a-104">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 0</span></span>

<span data-ttu-id="0313a-105">Adresář: C:\\uživatelé\\slee\\stáhne\\příklad</span><span class="sxs-lookup"><span data-stu-id="0313a-105">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="0313a-106">Název režimu LastWriteTime délka</span><span class="sxs-lookup"><span data-stu-id="0313a-106">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="0313a-107">d---Depth0 17:36:00 4 14. prosince 2015</span><span class="sxs-lookup"><span data-stu-id="0313a-107">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="0313a-108">-a---4/14. prosince 2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="0313a-108">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="0313a-109">-a---4/14. prosince 2015 1:19 PM 0 Soubor2.txt</span><span class="sxs-lookup"><span data-stu-id="0313a-109">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="0313a-110">-a---4/14. prosince 2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="0313a-110">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="0313a-111">PS C:\\uživatelé\\slee\\stáhne\\příklad&gt; Get-ChildItem-Recurse - hloubku 1</span><span class="sxs-lookup"><span data-stu-id="0313a-111">PS C:\\Users\\slee\\Downloads\\Example&gt; Get-ChildItem -Recurse -Depth 1</span></span>

<span data-ttu-id="0313a-112">Adresář: C:\\uživatelé\\slee\\stáhne\\příklad</span><span class="sxs-lookup"><span data-stu-id="0313a-112">Directory: C:\\Users\\slee\\Downloads\\Example</span></span>

<span data-ttu-id="0313a-113">Název režimu LastWriteTime délka</span><span class="sxs-lookup"><span data-stu-id="0313a-113">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="0313a-114">d---Depth0 17:36:00 4 14. prosince 2015</span><span class="sxs-lookup"><span data-stu-id="0313a-114">d----- 4/14/2015 5:36 PM Depth0</span></span>

<span data-ttu-id="0313a-115">-a---4/14. prosince 2015 1:19 PM 0 File1.txt</span><span class="sxs-lookup"><span data-stu-id="0313a-115">-a---- 4/14/2015 1:19 PM 0 File1.txt</span></span>

<span data-ttu-id="0313a-116">-a---4/14. prosince 2015 1:19 PM 0 Soubor2.txt</span><span class="sxs-lookup"><span data-stu-id="0313a-116">-a---- 4/14/2015 1:19 PM 0 File2.txt</span></span>

<span data-ttu-id="0313a-117">-a---4/14. prosince 2015 1:19 PM 0 File3.txt</span><span class="sxs-lookup"><span data-stu-id="0313a-117">-a---- 4/14/2015 1:19 PM 0 File3.txt</span></span>

<span data-ttu-id="0313a-118">Adresář: C:\\uživatelé\\slee\\stáhne\\příklad\\Depth0</span><span class="sxs-lookup"><span data-stu-id="0313a-118">Directory: C:\\Users\\slee\\Downloads\\Example\\Depth0</span></span>

<span data-ttu-id="0313a-119">Název režimu LastWriteTime délka</span><span class="sxs-lookup"><span data-stu-id="0313a-119">Mode LastWriteTime Length Name</span></span>

---- ------------- ------ ----

<span data-ttu-id="0313a-120">d---Depth1 5:33 odp 4 14. prosince 2015</span><span class="sxs-lookup"><span data-stu-id="0313a-120">d----- 4/14/2015 5:33 PM Depth1</span></span>
