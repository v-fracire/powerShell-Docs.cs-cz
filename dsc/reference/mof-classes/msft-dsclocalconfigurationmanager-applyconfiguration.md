---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 559ff1793a18e28dad2f176bdb20eb53bc08630d
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048110"
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="d5664-103">Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="d5664-103">ApplyConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="d5664-104">Pomocí agenta konfigurace použije konfiguraci, která čeká na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="d5664-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span>

<span data-ttu-id="d5664-105">Pokud není žádná konfigurace čekající, tato metoda znovu použije aktuální konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="d5664-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="d5664-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d5664-106">Syntax</span></span>

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="d5664-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="d5664-107">Parameters</span></span>

<span data-ttu-id="d5664-108">*Vynutit* \[v\] Pokud je to **true**, aktuální konfigurace je znovu použita, i v případě konfigurace čekající.</span><span class="sxs-lookup"><span data-stu-id="d5664-108">*force* \[in\] If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="d5664-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="d5664-109">Return value</span></span>

<span data-ttu-id="d5664-110">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="d5664-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="d5664-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d5664-111">Remarks</span></span>

<span data-ttu-id="d5664-112">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="d5664-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="d5664-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d5664-113">Requirements</span></span>

<span data-ttu-id="d5664-114">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="d5664-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="d5664-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="d5664-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="d5664-116">Viz také</span><span class="sxs-lookup"><span data-stu-id="d5664-116">See also</span></span>

[<span data-ttu-id="d5664-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="d5664-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)