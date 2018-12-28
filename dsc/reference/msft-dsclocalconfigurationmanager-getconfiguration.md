---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: ae31ac30c152c96707b764ddaf00c924806afcfc
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403704"
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="f53d1-103">Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="f53d1-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="f53d1-104">Odešle dokument konfigurace spravovaných uzlů a používá **získat** metody konfigurace agenta použít danou konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f53d1-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="f53d1-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f53d1-105">Syntax</span></span>

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

## <a name="parameters"></a><span data-ttu-id="f53d1-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="f53d1-106">Parameters</span></span>

<span data-ttu-id="f53d1-107">*configurationData* \[v\] konfigurační data určená k odeslání.</span><span class="sxs-lookup"><span data-stu-id="f53d1-107">*configurationData* \[in\] Specifies the configuration data to send.</span></span>

<span data-ttu-id="f53d1-108">*konfigurace* \[si\] na vrátit, obsahuje vložený instance konfigurace.</span><span class="sxs-lookup"><span data-stu-id="f53d1-108">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="f53d1-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="f53d1-109">Return value</span></span>

<span data-ttu-id="f53d1-110">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="f53d1-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="f53d1-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="f53d1-111">Remarks</span></span>

<span data-ttu-id="f53d1-112">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="f53d1-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="f53d1-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f53d1-113">Requirements</span></span>

<span data-ttu-id="f53d1-114">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="f53d1-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="f53d1-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="f53d1-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="f53d1-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="f53d1-116">See also</span></span>

[<span data-ttu-id="f53d1-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="f53d1-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)