---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: a6366e18b4b6478bfab89475bc6975e6491da9f7
ms.sourcegitcommit: 735ccab3fb3834ccd8559fab6700b798e8e5ffbf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/25/2018
---
# <a name="windows-management-framework-wmf-50-rtm-release-notes-overview"></a><span data-ttu-id="50976-102">Poznámky k verzi Přehled služby Windows Management Framework (WMF) 5.0 RTM</span><span class="sxs-lookup"><span data-stu-id="50976-102">Windows Management Framework (WMF) 5.0 RTM Release Notes Overview</span></span>

<span data-ttu-id="50976-103">**WMF 5.0 je superceeded podle WMF 5.1. Uživatelé s WMF 5.0 musí upgradovat na WMF 5.1 odborná pomoc. Postupujte podle [intructions instalaci WMF 5.1](../5.1/install-configure.md)**</span><span class="sxs-lookup"><span data-stu-id="50976-103">**WMF 5.0 is superceeded by WMF 5.1. Users with WMF 5.0 must upgrade to WMF 5.1 to receive support. Please follow the [installation intructions of WMF 5.1](../5.1/install-configure.md)**</span></span>

<span data-ttu-id="50976-104">Windows Management Framework (WMF) 5.0 RTM přináší funkce, který byl aktualizován z WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="50976-104">Windows Management Framework (WMF) 5.0 RTM brings functionality that has been updated from WMF 4.0.</span></span> <span data-ttu-id="50976-105">WMF 5.0 RTM, je možné nainstalovat jenom na **Windows Server 2012 R2**, **systému Windows Server 2012**, **Windows Server 2008 R2**, **Windows 8.1**, a **Windows 7 SP1** a obsahuje aktualizované verze nebo Úvod následující funkce:</span><span class="sxs-lookup"><span data-stu-id="50976-105">WMF 5.0 RTM is available for installation only on **Windows Server 2012 R2**, **Windows Server 2012**, **Windows Server 2008 R2**, **Windows 8.1**, and **Windows 7 SP1** and contains updated versions or introduction of the following features:</span></span>

- <span data-ttu-id="50976-106">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="50976-106">Windows PowerShell</span></span>
- <span data-ttu-id="50976-107">Funkce Just Enough Administration (JEA)</span><span class="sxs-lookup"><span data-stu-id="50976-107">Just Enough Administration (JEA)</span></span>
- <span data-ttu-id="50976-108">Windows PowerShell Desired State Configuration (DSC)</span><span class="sxs-lookup"><span data-stu-id="50976-108">Windows PowerShell Desired State Configuration (DSC)</span></span>
- <span data-ttu-id="50976-109">Integrované skriptovací prostředí (ISE) v prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="50976-109">Windows PowerShell Integrated Scripting Environment (ISE)</span></span>
- <span data-ttu-id="50976-110">Windows PowerShell webové služby (OData IIS rozšíření správy)</span><span class="sxs-lookup"><span data-stu-id="50976-110">Windows PowerShell Web Services (Management OData IIS Extension)</span></span>
- <span data-ttu-id="50976-111">Vzdálená správa systému Windows (WinRM)</span><span class="sxs-lookup"><span data-stu-id="50976-111">Windows Remote Management (WinRM)</span></span>
- <span data-ttu-id="50976-112">Windows Management Instrumentation (WMI)</span><span class="sxs-lookup"><span data-stu-id="50976-112">Windows Management Instrumentation (WMI)</span></span>

<span data-ttu-id="50976-113">WMF 5.0 RTM, nahradí [WMF 5.0 produkční Preview](http://blogs.msdn.com/b/powershell/archive/2015/08/31/windows-management-framework-5-0-production-preview-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="50976-113">WMF 5.0 RTM replaces the [WMF 5.0 Production Preview](http://blogs.msdn.com/b/powershell/archive/2015/08/31/windows-management-framework-5-0-production-preview-is-now-available.aspx).</span></span> <span data-ttu-id="50976-114">WMF 5.0 RTM, můžete nainstalovat bez odinstalace WMF 5.0 produkční Preview, ale je nutné odinstalovat všechny ostatní starší verze Preview WMF 5.0 před instalací WMF 5.0 RTM.</span><span class="sxs-lookup"><span data-stu-id="50976-114">You can install WMF 5.0 RTM without uninstalling WMF 5.0 Production Preview, but you must uninstall all other older releases of WMF 5.0 previews before installing the WMF 5.0 RTM.</span></span>

<span data-ttu-id="50976-115">*Poznámka:* Pokud používáte systém Windows 10, můžete získat stejnou sadu funkcí, které jsou k dispozici v WMF 5.0 RTM aktualizací na listopad aktualizace Windows 10 (verze 1511).</span><span class="sxs-lookup"><span data-stu-id="50976-115">*Note:* If you are running Windows 10, you can get the same set of functionality available in WMF 5.0 RTM by updating to the November update of Windows 10 (Version 1511).</span></span> <span data-ttu-id="50976-116">Pokud již jste neprovedli aktualizaci systému Windows 10, vyberte tlačítko Start a potom vyberte nastavení > aktualizace a zabezpečení > Windows Update > Kontrola aktualizací.</span><span class="sxs-lookup"><span data-stu-id="50976-116">If you have not already updated your Windows 10 system, select the Start button, then select Settings > Update & security > Windows Update > Check for updates.</span></span>
