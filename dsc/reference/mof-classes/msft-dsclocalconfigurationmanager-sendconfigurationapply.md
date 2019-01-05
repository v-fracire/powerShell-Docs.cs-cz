---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda SendConfigurationApply třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: da3a08307122ab38ee4a6fd5d4a9b97579a988f7
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048109"
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="a8802-103">Metoda SendConfigurationApply třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="a8802-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="a8802-104">Odešle dokument konfigurace spravovaných uzlů a použít danou konfiguraci pomocí konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="a8802-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="a8802-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a8802-105">Syntax</span></span>

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="a8802-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="a8802-106">Parameters</span></span>

<span data-ttu-id="a8802-107">*ConfigurationData* \[v\] dat prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="a8802-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="a8802-108">*Vynutit* \[v\] **true** vynutit konfiguraci tak, aby zastavit.</span><span class="sxs-lookup"><span data-stu-id="a8802-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="a8802-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="a8802-109">Return value</span></span>

<span data-ttu-id="a8802-110">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="a8802-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="a8802-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="a8802-111">Remarks</span></span>

<span data-ttu-id="a8802-112">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="a8802-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="a8802-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a8802-113">Requirements</span></span>

<span data-ttu-id="a8802-114">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="a8802-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="a8802-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="a8802-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="a8802-116">Viz také</span><span class="sxs-lookup"><span data-stu-id="a8802-116">See also</span></span>

[<span data-ttu-id="a8802-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="a8802-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)