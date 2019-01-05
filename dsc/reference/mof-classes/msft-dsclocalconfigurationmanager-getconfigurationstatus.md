---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: c66ccc4eefaef2d0c3a68fa8a96c5abb9bda6e4c
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048165"
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="f9f1e-103">Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="f9f1e-103">GetConfigurationStatus method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="f9f1e-104">Zobrazit historii stavu konfigurace.</span><span class="sxs-lookup"><span data-stu-id="f9f1e-104">Get the configuration status history.</span></span>

## <a name="syntax"></a><span data-ttu-id="f9f1e-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f9f1e-105">Syntax</span></span>

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

## <a name="parameters"></a><span data-ttu-id="f9f1e-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="f9f1e-106">Parameters</span></span>

<span data-ttu-id="f9f1e-107">*Všechny* \[v\] **true** Pokud tato metoda by měla vrátit informace o všech konfiguraci běží na počítači, včetně konfigurace aplikace a kontrolu konzistence.</span><span class="sxs-lookup"><span data-stu-id="f9f1e-107">*All* \[in\] **true** if this method should return information about all the configuration runs on the machine, including the configuration application and the consistency check.</span></span>

<span data-ttu-id="f9f1e-108">*configurationStatus* \[si\] na vrátit, obsahuje vložený instance **MSFT_DSCConfigurationStatus** třídu, která definuje nastavení.</span><span class="sxs-lookup"><span data-stu-id="f9f1e-108">*configurationStatus* \[out\] On return, contains an embedded instance of the **MSFT_DSCConfigurationStatus** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="f9f1e-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="f9f1e-109">Return value</span></span>

<span data-ttu-id="f9f1e-110">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="f9f1e-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="f9f1e-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="f9f1e-111">Remarks</span></span>

<span data-ttu-id="f9f1e-112">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="f9f1e-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="f9f1e-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f9f1e-113">Requirements</span></span>

<span data-ttu-id="f9f1e-114">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="f9f1e-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="f9f1e-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="f9f1e-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="f9f1e-116">Viz také</span><span class="sxs-lookup"><span data-stu-id="f9f1e-116">See also</span></span>

[<span data-ttu-id="f9f1e-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="f9f1e-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)