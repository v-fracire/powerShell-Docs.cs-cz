---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda SendConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: b4d4c901268344ba67d77e4dc982042bfc2abd78
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34222203"
---
# <a name="sendconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="cca0e-103">Metoda SendConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="cca0e-103">SendConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="cca0e-104">Odešle spravovaný uzel dokumentu konfigurace a uloží ji jako nevyřízenou změnu.</span><span class="sxs-lookup"><span data-stu-id="cca0e-104">Sends the configuration document to the managed node and saves it as a pending change.</span></span>

<a name="syntax"></a><span data-ttu-id="cca0e-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="cca0e-105">Syntax</span></span>
------

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="cca0e-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="cca0e-106">Parameters</span></span>
----------

<span data-ttu-id="cca0e-107">*ConfigurationData* \[v\] data prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="cca0e-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="cca0e-108">*Vynutit* \[v\] **true** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="cca0e-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="cca0e-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="cca0e-109">Return value</span></span>
------------

<span data-ttu-id="cca0e-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="cca0e-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="cca0e-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="cca0e-111">Remarks</span></span>

<span data-ttu-id="cca0e-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="cca0e-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="cca0e-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="cca0e-113">Requirements</span></span>
------------
><span data-ttu-id="cca0e-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="cca0e-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="cca0e-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="cca0e-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="cca0e-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="cca0e-116">See also</span></span>


[<span data-ttu-id="cca0e-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="cca0e-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)