---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 725b1a2a62510a4e9b59aabdec8a7e502c737bfc
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34221761"
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="ba4dd-103">Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="ba4dd-103">GetConfigurationStatus method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="ba4dd-104">Načtení historie stav konfigurace.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-104">Get the configuration status history.</span></span>

<a name="syntax"></a><span data-ttu-id="ba4dd-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ba4dd-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

<a name="parameters"></a><span data-ttu-id="ba4dd-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="ba4dd-106">Parameters</span></span>
----------

<span data-ttu-id="ba4dd-107">*Všechny* \[v\] **true** Pokud tato metoda by měla vrátit informace o všech konfigurace běží na počítači, včetně konfigurace aplikace a kontrolu konzistence.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-107">*All* \[in\] **true** if this method should return information about all the configuration runs on the machine, including the configuration application and the consistency check.</span></span>

<span data-ttu-id="ba4dd-108">*configurationStatus* \[out\] na vrátí, obsahuje vložené instance **MSFT_DSCConfigurationStatus** třídu, která definuje nastavení.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-108">*configurationStatus* \[out\] On return, contains an embedded instance of the **MSFT_DSCConfigurationStatus** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="ba4dd-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="ba4dd-109">Return value</span></span>
------------

<span data-ttu-id="ba4dd-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="ba4dd-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="ba4dd-111">Remarks</span></span>

<span data-ttu-id="ba4dd-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="ba4dd-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ba4dd-113">Requirements</span></span>
------------
><span data-ttu-id="ba4dd-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="ba4dd-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="ba4dd-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="ba4dd-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="ba4dd-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="ba4dd-116">See also</span></span>


[<span data-ttu-id="ba4dd-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="ba4dd-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)