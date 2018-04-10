---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: dde4ac003b346018561481e05ca7374475f9ff1d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="79a5f-103">Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="79a5f-103">GetConfigurationStatus method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="79a5f-104">Načtení historie stav konfigurace.</span><span class="sxs-lookup"><span data-stu-id="79a5f-104">Get the configuration status history.</span></span>

<a name="syntax"></a><span data-ttu-id="79a5f-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="79a5f-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

<a name="parameters"></a><span data-ttu-id="79a5f-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="79a5f-106">Parameters</span></span>
----------

<span data-ttu-id="79a5f-107">*Všechny* \[v\] **true** Pokud tato metoda by měla vrátit informace o všech konfigurace běží na počítači, včetně konfigurace aplikace a kontrolu konzistence.</span><span class="sxs-lookup"><span data-stu-id="79a5f-107">*All* \[in\] **true** if this method should return information about all the configuration runs on the machine, including the configuration application and the consistency check.</span></span>

<span data-ttu-id="79a5f-108">*configurationStatus* \[out\] na vrátí, obsahuje vložené instance **MSFT_DSCConfigurationStatus** třídu, která definuje nastavení.</span><span class="sxs-lookup"><span data-stu-id="79a5f-108">*configurationStatus* \[out\] On return, contains an embedded instance of the **MSFT_DSCConfigurationStatus** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="79a5f-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="79a5f-109">Return value</span></span>
------------

<span data-ttu-id="79a5f-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="79a5f-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="79a5f-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="79a5f-111">Remarks</span></span>

<span data-ttu-id="79a5f-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="79a5f-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="79a5f-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="79a5f-113">Requirements</span></span>
------------
><span data-ttu-id="79a5f-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="79a5f-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="79a5f-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="79a5f-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="79a5f-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="79a5f-116">See also</span></span>


[<span data-ttu-id="79a5f-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="79a5f-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)