---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC funkce uzlu dotazů na informace z načítacího serveru."
ms.openlocfilehash: f97e1d62873fb9e23147ff137468a767455cd82c
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-function-to-query-node-information-from-pull-server"></a><span data-ttu-id="c84c4-103">DSC funkce uzlu dotazů na informace z načítacího serveru.</span><span class="sxs-lookup"><span data-stu-id="c84c4-103">DSC function to query node information from pull server.</span></span>

```powershell
function QueryNodeInformation
{
Param (      
       [string] $Uri =
"http://localhost:7070/PSDSCComplianceServer.svc/Status",                         
       [string] $ContentType = "application/json"           
     )

  Write-Host "Querying node information from pull server URI  = $Uri" -ForegroundColor Green

  Write-Host "Querying node status in content type  = $ContentType " -ForegroundColor Green

   $response = Invoke-WebRequest -Uri $Uri -Method Get -ContentType $ContentType -UseDefaultCredentials -Headers 
    @{Accept = $ContentType}

   if($response.StatusCode -ne 200)
 {
     Write-Host "node information was not retrieved." -ForegroundColor Red
 }

 $jsonResponse = ConvertFrom-Json $response.Content

  return $jsonResponse
}
```

<span data-ttu-id="c84c4-104">Nahraďte `Uri` parametr s identifikátorem URI pro vyžádání obsahu server.</span><span class="sxs-lookup"><span data-stu-id="c84c4-104">Replace the `Uri` parameter with the URI for your pull server.</span></span> <span data-ttu-id="c84c4-105">Pokud chcete informace uzlu ve formátu XML, nastavte `ContentType` k `application/xml`.</span><span class="sxs-lookup"><span data-stu-id="c84c4-105">If you want the node information in XML format, set `ContentType` to `application/xml`.</span></span>

<span data-ttu-id="c84c4-106">K načtení informací z uzlu `$json` parametr, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="c84c4-106">To retrieve the node information from the `$json` parameter, use the following:</span></span>

```powershell
$json = QueryNodeInformation –Uri http://localhost:7070/PSDSCComplianceServer.svc/Status 

$json.value | Format-Table TargetName, ConfigurationId, ServerChecksum, NodeCompliant, LastComplianceTime, StatusCode
```

