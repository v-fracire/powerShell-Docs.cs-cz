---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 559ff1793a18e28dad2f176bdb20eb53bc08630d
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403790"
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="bfab6-103">Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="bfab6-103">ApplyConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="bfab6-104">Pomocí agenta konfigurace použije konfiguraci, která čeká na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="bfab6-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span>

<span data-ttu-id="bfab6-105">Pokud není žádná konfigurace čekající, tato metoda znovu použije aktuální konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="bfab6-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="bfab6-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="bfab6-106">Syntax</span></span>

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="bfab6-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="bfab6-107">Parameters</span></span>

<span data-ttu-id="bfab6-108">*Vynutit* \[v\] Pokud je to **true**, aktuální konfigurace je znovu použita, i v případě konfigurace čekající.</span><span class="sxs-lookup"><span data-stu-id="bfab6-108">*force* \[in\] If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="bfab6-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="bfab6-109">Return value</span></span>

<span data-ttu-id="bfab6-110">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="bfab6-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="bfab6-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="bfab6-111">Remarks</span></span>

<span data-ttu-id="bfab6-112">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="bfab6-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="bfab6-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="bfab6-113">Requirements</span></span>

<span data-ttu-id="bfab6-114">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="bfab6-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="bfab6-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="bfab6-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="bfab6-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="bfab6-116">See also</span></span>

[<span data-ttu-id="bfab6-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="bfab6-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)