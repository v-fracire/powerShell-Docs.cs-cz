---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 4e0c1638bf10e57580a463c46595ac9bc142a5b4
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="just-enough-administration-jea"></a><span data-ttu-id="33f0c-102">Akorát správy (JEA)</span><span class="sxs-lookup"><span data-stu-id="33f0c-102">Just Enough Administration (JEA)</span></span>
<span data-ttu-id="33f0c-103">Právě dostatečně správy je nová funkce v WMF 5.0, která umožňuje správu na základě rolí pomocí vzdálenou komunikaci prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33f0c-103">Just Enough Administration is a new feature in WMF 5.0 that enables role-based administration through PowerShell remoting.</span></span>  <span data-ttu-id="33f0c-104">Ji rozšiřuje stávající infrastrukturu omezené koncový bod umožňuje jiným uživatelům než správcům ke spuštění konkrétních příkazů, skripty a spustitelné soubory jako správce.</span><span class="sxs-lookup"><span data-stu-id="33f0c-104">It extends the existing constrained endpoint infrastructure by allowing non-administrators to run specific commands, scripts and executables as an administrator.</span></span>  <span data-ttu-id="33f0c-105">To umožňuje snížit počet úplná oprávnění správce ve vašem prostředí a zlepšit zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="33f0c-105">This enables you to reduce the number of full administrators in your environment and improve your security.</span></span>  <span data-ttu-id="33f0c-106">JEA se dá použít pro všechny objekty, které spravujete pomocí prostředí PowerShell; Pokud budete moct spravovat něco pomocí prostředí PowerShell, můžete JEA provést tak více bezpečně.</span><span class="sxs-lookup"><span data-stu-id="33f0c-106">JEA works for everything you manage through PowerShell; if you can manage something with PowerShell, JEA can help you do so more securely.</span></span>  <span data-ttu-id="33f0c-107">Pro podrobné podívejte se na právě dostatečně správy, podívejte se [prostředí průvodce](http://aka.ms/JEA).</span><span class="sxs-lookup"><span data-stu-id="33f0c-107">For a detailed look at Just Enough Administration, check out the [experience guide](http://aka.ms/JEA).</span></span>

<span data-ttu-id="33f0c-108">Na rozdíl od původního omezené koncových bodů JEA je efektivní a snadno konfiguruje.</span><span class="sxs-lookup"><span data-stu-id="33f0c-108">Unlike old constrained endpoints, JEA is both powerful and easy to configure.</span></span>  <span data-ttu-id="33f0c-109">Možnosti uživatele v sadě nástrojů JEA lze granularly řídit, a omezení, které sady parametrů a hodnoty můžete zadat konkrétní příkaz.</span><span class="sxs-lookup"><span data-stu-id="33f0c-109">User capabilities in JEA can be granularly controlled, down to restricting which parameter sets and values can be supplied to a specific command.</span></span> <span data-ttu-id="33f0c-110">Akce uživatele se spouštějí v kontextu jednorázové virtuální účet, který má práva k provedení akce správce.</span><span class="sxs-lookup"><span data-stu-id="33f0c-110">The user’s actions are run in the context of a one-time virtual account that has the rights to perform the administrator actions.</span></span>  <span data-ttu-id="33f0c-111">Příkazy vyvolané uživatele lze protokolovat audity zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="33f0c-111">The commands invoked by the user can be logged for security audits.</span></span>

<span data-ttu-id="33f0c-112">JEA funguje tak, že umožňuje vytvářet speciálně nakonfigurovat omezené koncové body.</span><span class="sxs-lookup"><span data-stu-id="33f0c-112">JEA works by allowing you to create specially-configured constrained endpoints.</span></span>  <span data-ttu-id="33f0c-113">Tyto koncové body mají několik důležité charakteristiky:</span><span class="sxs-lookup"><span data-stu-id="33f0c-113">These endpoints have a few important characteristics:</span></span>

1. <span data-ttu-id="33f0c-114">Uživatelů, kteří se připojují k nim "Spustit jako" privilegované virtuální účet, který existuje pouze po dobu trvání této vzdálené relace.</span><span class="sxs-lookup"><span data-stu-id="33f0c-114">Users connecting to them “run as” a privileged Virtual Account that exists only for the duration of this remote session.</span></span>  <span data-ttu-id="33f0c-115">Ve výchozím nastavení, je tento virtuální účet členem předdefinované skupiny Administrators, stejně jako správce domény na řadičích domény (Poznámka: Tato oprávnění se dají konfigurovat).</span><span class="sxs-lookup"><span data-stu-id="33f0c-115">By default, this Virtual Account is a member of the built-in Administrators group, as well as a Domain Administrators on domain controllers (note: these permissions are configurable).</span></span> <span data-ttu-id="33f0c-116">Pomocí připojení jako jeden uživatel a spuštění jako jiný, privilegovaných uživatelů, můžete povolit uživatelům bez oprávnění k provádění specifických úloh správy bez nutnosti poskytnutí oprávnění správce ve vašich systémech.</span><span class="sxs-lookup"><span data-stu-id="33f0c-116">By connecting as one user and running as a different, privileged user, you can allow non-privileged users to perform specific administrative tasks without giving them administrative rights on your systems.</span></span>
2. <span data-ttu-id="33f0c-117">Koncový bod je uzamčené.</span><span class="sxs-lookup"><span data-stu-id="33f0c-117">The endpoint is locked down.</span></span>  <span data-ttu-id="33f0c-118">To znamená, prostředí PowerShell se spustí v režimu žádný jazyk.</span><span class="sxs-lookup"><span data-stu-id="33f0c-118">This means PowerShell runs in No Language mode.</span></span>  <span data-ttu-id="33f0c-119">Pouze určité příkazy, skripty a spustitelné soubory jsou viditelné pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="33f0c-119">Only specific commands, scripts, and executables are visible to the user.</span></span>
3. <span data-ttu-id="33f0c-120">Různých uživatelů, kteří se připojují k ruce jinou sadu funkcí, které jsou založené na členství ve skupině.</span><span class="sxs-lookup"><span data-stu-id="33f0c-120">Different users connecting are presented with a different set of capabilities based on group membership.</span></span>  <span data-ttu-id="33f0c-121">Můžete zadat různé role různé možnosti v stejný koncový bod.</span><span class="sxs-lookup"><span data-stu-id="33f0c-121">You can provide different roles different capabilities at the same endpoint.</span></span>
