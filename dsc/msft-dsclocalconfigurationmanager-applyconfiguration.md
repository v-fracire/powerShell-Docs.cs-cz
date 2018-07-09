---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 559ff1793a18e28dad2f176bdb20eb53bc08630d
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892603"
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="27fc9-103">Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="27fc9-103">ApplyConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="27fc9-104">Pomocí agenta konfigurace použije konfiguraci, která čeká na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="27fc9-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span>

<span data-ttu-id="27fc9-105">Pokud není žádná konfigurace čekající, tato metoda znovu použije aktuální konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="27fc9-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="27fc9-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="27fc9-106">Syntax</span></span>

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="27fc9-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="27fc9-107">Parameters</span></span>

<span data-ttu-id="27fc9-108">*Vynutit* \[v\] Pokud je to **true**, aktuální konfigurace je znovu použita, i v případě konfigurace čekající.</span><span class="sxs-lookup"><span data-stu-id="27fc9-108">*force* \[in\] If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="27fc9-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="27fc9-109">Return value</span></span>

<span data-ttu-id="27fc9-110">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="27fc9-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="27fc9-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="27fc9-111">Remarks</span></span>

<span data-ttu-id="27fc9-112">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="27fc9-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="27fc9-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="27fc9-113">Requirements</span></span>

<span data-ttu-id="27fc9-114">**Soubor MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="27fc9-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="27fc9-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="27fc9-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="27fc9-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="27fc9-116">See also</span></span>

[<span data-ttu-id="27fc9-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="27fc9-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)