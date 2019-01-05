---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda RemoveConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 03555cc73da1272bdebebc3d93b26aaf8fabc18e
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048150"
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="e4f52-103">Metoda RemoveConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="e4f52-103">RemoveConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="e4f52-104">Odstraní konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="e4f52-104">Removes the configuration files.</span></span>

## <a name="syntax"></a><span data-ttu-id="e4f52-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e4f52-105">Syntax</span></span>

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

## <a name="parameters"></a><span data-ttu-id="e4f52-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="e4f52-106">Parameters</span></span>

<span data-ttu-id="e4f52-107">*Fáze* \[v\] Určuje, který dokument konfigurace odebrat.</span><span class="sxs-lookup"><span data-stu-id="e4f52-107">*Stage* \[in\] Specifies which configuration document to remove.</span></span> <span data-ttu-id="e4f52-108">Platné jsou následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="e4f52-108">The following values are valid:</span></span>

|<span data-ttu-id="e4f52-109">Hodnota</span><span class="sxs-lookup"><span data-stu-id="e4f52-109">Value</span></span> |<span data-ttu-id="e4f52-110">Popis</span><span class="sxs-lookup"><span data-stu-id="e4f52-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="e4f52-111">**1**</span><span class="sxs-lookup"><span data-stu-id="e4f52-111">**1**</span></span> | <span data-ttu-id="e4f52-112">**Aktuální** konfiguračního dokumentu (current.mof).</span><span class="sxs-lookup"><span data-stu-id="e4f52-112">The **Current** configuration document (current.mof).</span></span> |
|<span data-ttu-id="e4f52-113">**2**</span><span class="sxs-lookup"><span data-stu-id="e4f52-113">**2**</span></span> | <span data-ttu-id="e4f52-114">**Čekající** konfiguračního dokumentu (pending.mof).</span><span class="sxs-lookup"><span data-stu-id="e4f52-114">The **Pending** configuration document (pending.mof).</span></span>  |
|<span data-ttu-id="e4f52-115">**4**</span><span class="sxs-lookup"><span data-stu-id="e4f52-115">**4**</span></span> | <span data-ttu-id="e4f52-116">**Předchozí** konfiguračního dokumentu (previous.mof).</span><span class="sxs-lookup"><span data-stu-id="e4f52-116">The **Previous** configuration document (previous.mof).</span></span> |

<span data-ttu-id="e4f52-117">*Vynutit* \[v\] **true** k vynucení odebrání konfigurace.</span><span class="sxs-lookup"><span data-stu-id="e4f52-117">*Force* \[in\] **true** to force the removal of the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="e4f52-118">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="e4f52-118">Return value</span></span>

<span data-ttu-id="e4f52-119">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="e4f52-119">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="e4f52-120">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e4f52-120">Remarks</span></span>

<span data-ttu-id="e4f52-121">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="e4f52-121">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="e4f52-122">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e4f52-122">Requirements</span></span>

<span data-ttu-id="e4f52-123">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="e4f52-123">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="e4f52-124">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e4f52-124">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="e4f52-125">Viz také</span><span class="sxs-lookup"><span data-stu-id="e4f52-125">See also</span></span>

[<span data-ttu-id="e4f52-126">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="e4f52-126">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)