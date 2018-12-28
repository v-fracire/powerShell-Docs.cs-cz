---
ms.date: 06/12/2017
keywords: jea, powershell, zabezpečení
title: Konfigurace relace JEA
ms.openlocfilehash: 1b598522d43b2c1a26a739a67cee5181b21a7c32
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655459"
---
# <a name="jea-session-configurations"></a><span data-ttu-id="ffb0c-103">Konfigurace relace JEA</span><span class="sxs-lookup"><span data-stu-id="ffb0c-103">JEA Session Configurations</span></span>

> <span data-ttu-id="ffb0c-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ffb0c-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="ffb0c-105">Koncového bodu JEA je registrován v systému vytváření a registrací konfiguračního souboru relace prostředí PowerShell určitým způsobem.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-105">A JEA endpoint is registered on a system by creating and registering a PowerShell session configuration file in a specific way.</span></span>
<span data-ttu-id="ffb0c-106">Určení konfigurací relace *kdo* pomocí koncového bodu JEA a rolemi, které mají přístup k.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-106">Session configurations determine *who* can use the JEA endpoint, and which role(s) they will have access to.</span></span>
<span data-ttu-id="ffb0c-107">Také definují globální nastavení, které platí pro všechny role uživatele v relaci JEA.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-107">They also define global settings that apply to users of any role in the JEA session.</span></span>

<span data-ttu-id="ffb0c-108">Toto téma popisuje postup registrace koncového bodu JEA a vytvoření konfiguračního souboru relace Powershellu.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-108">This topic describes how to create a PowerShell session configuration file and register a JEA endpoint.</span></span>

## <a name="create-a-session-configuration-file"></a><span data-ttu-id="ffb0c-109">Vytvoření konfiguračního souboru relace</span><span class="sxs-lookup"><span data-stu-id="ffb0c-109">Create a session configuration file</span></span>

<span data-ttu-id="ffb0c-110">Aby bylo možné registrace koncového bodu JEA, je třeba zadat konfiguraci tohoto koncového bodu.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-110">In order to register a JEA endpoint, you need to specify how that endpoint should be configured.</span></span>
<span data-ttu-id="ffb0c-111">Existuje mnoho možností vzít v úvahu tady, nejdůležitější, o kterých toho, kteří mají mít přístup ke koncovému bodu JEA, které role bude, přiřadit, která identita JEA použije na pozadí a jaká bude název koncového bodu JEA.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-111">There are many options to consider here, the most important of which being who should have access to the JEA endpoint, which roles will they be assigned, which identity will JEA use under the covers, and what will be the name of the JEA endpoint.</span></span>
<span data-ttu-id="ffb0c-112">Ty jsou všechny definovány v souboru konfigurace relace prostředí PowerShell, který je datový soubor prostředí PowerShell končící příponou .pssc.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-112">These are all defined in a PowerShell session configuration file, which is a PowerShell data file ending with a .pssc extension.</span></span>

<span data-ttu-id="ffb0c-113">Vytvoření konfiguračního souboru kostru relace u koncových bodů JEA, spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-113">To create a skeleton session configuration file for JEA endpoints, run the following command.</span></span>

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> <span data-ttu-id="ffb0c-114">Nejběžnější možnosti konfigurace jsou uvedeny v kostru souboru ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-114">Only the most common configuration options are included in the skeleton file by default.</span></span>
> <span data-ttu-id="ffb0c-115">Použití `-Full` přepínače zahrnout generované PSSC všech příslušných nastavení.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-115">Use the `-Full` switch to include all applicable settings in the generated PSSC.</span></span>

<span data-ttu-id="ffb0c-116">Soubor konfigurace relace můžete otevřít v libovolném textovém editoru.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-116">You can open the session configuration file in any text editor.</span></span>
<span data-ttu-id="ffb0c-117">`-SessionType RestrictedRemoteServer` Pole označuje, že konfigurace relace použije JEA pro zabezpečenou správu.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-117">The `-SessionType RestrictedRemoteServer` field indicates that the session configuration will be used by JEA for secure management.</span></span>
<span data-ttu-id="ffb0c-118">Relace tak budou fungovat v [NoLanguage režimu](https://technet.microsoft.com/library/dn433292.aspx) a obsahovat jenom následující příkazy 8 výchozí (a aliasy) k dispozici:</span><span class="sxs-lookup"><span data-stu-id="ffb0c-118">Sessions configured this way will operate in [NoLanguage mode](https://technet.microsoft.com/library/dn433292.aspx) and only have the following 8 default commands (and aliases) available:</span></span>

- <span data-ttu-id="ffb0c-119">Clear-Host (kompatibilní se specifikací, zrušte zaškrtnutí)</span><span class="sxs-lookup"><span data-stu-id="ffb0c-119">Clear-Host (cls, clear)</span></span>
- <span data-ttu-id="ffb0c-120">Konec-PSSession (exsn, konec)</span><span class="sxs-lookup"><span data-stu-id="ffb0c-120">Exit-PSSession (exsn, exit)</span></span>
- <span data-ttu-id="ffb0c-121">Get – příkaz (gcm)</span><span class="sxs-lookup"><span data-stu-id="ffb0c-121">Get-Command (gcm)</span></span>
- <span data-ttu-id="ffb0c-122">Get-FormatData</span><span class="sxs-lookup"><span data-stu-id="ffb0c-122">Get-FormatData</span></span>
- <span data-ttu-id="ffb0c-123">Get-Help</span><span class="sxs-lookup"><span data-stu-id="ffb0c-123">Get-Help</span></span>
- <span data-ttu-id="ffb0c-124">Objekt míry (měření)</span><span class="sxs-lookup"><span data-stu-id="ffb0c-124">Measure-Object (measure)</span></span>
- <span data-ttu-id="ffb0c-125">Výchozí out-Buffer:</span><span class="sxs-lookup"><span data-stu-id="ffb0c-125">Out-Default</span></span>
- <span data-ttu-id="ffb0c-126">Select-Object (výběr)</span><span class="sxs-lookup"><span data-stu-id="ffb0c-126">Select-Object (select)</span></span>

<span data-ttu-id="ffb0c-127">Žádní zprostředkovatelé prostředí PowerShell, jsou k dispozici, ani při že jakékoli vnější programy (spustitelné soubory, skripty atd.).</span><span class="sxs-lookup"><span data-stu-id="ffb0c-127">No PowerShell providers are available, nor are any external programs (executables, scripts, etc.).</span></span>

<span data-ttu-id="ffb0c-128">Existuje několik dalších polí, které můžete nakonfigurovat pro relaci JEA.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-128">There are several other fields you will want to configure for the JEA session.</span></span>
<span data-ttu-id="ffb0c-129">Tyto jsou popsané v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-129">They are covered in the following sections.</span></span>

### <a name="choose-the-jea-identity"></a><span data-ttu-id="ffb0c-130">Vyberte identitu funkce JEA</span><span class="sxs-lookup"><span data-stu-id="ffb0c-130">Choose the JEA identity</span></span>

<span data-ttu-id="ffb0c-131">Na pozadí musí JEA identitu (účet) pro použití při spuštění příkazů připojeného uživatele.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-131">Behind the scenes, JEA needs an identity (account) to use when running a connected user's commands.</span></span>
<span data-ttu-id="ffb0c-132">Můžete rozhodnout, která identita JEA použije v konfiguračním souboru relace.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-132">You decide which identity JEA will use in the session configuration file.</span></span>

#### <a name="local-virtual-account"></a><span data-ttu-id="ffb0c-133">Místní virtuální účet</span><span class="sxs-lookup"><span data-stu-id="ffb0c-133">Local Virtual Account</span></span>

<span data-ttu-id="ffb0c-134">Pokud role podporována tímto koncovým bodem JEA se používají ke správě místního počítače a účet místního správce stačí spustit příkazy úspěšně, měli byste nakonfigurovat JEA použít místní virtuální účet.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-134">If the roles supported by this JEA endpoint are all used to manage the local machine, and a local administrator account is sufficient to run the commands succesfully, you should configure JEA to use a local virtual account.</span></span>
<span data-ttu-id="ffb0c-135">Virtuální účty jsou dočasné, které jsou jedinečné pro konkrétní uživatele a pouze poslední po dobu trvání jejich relace Powershellu.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-135">Virtual accounts are temporary accounts that are unique to a specific user and only last for the duration of their PowerShell session.</span></span>
<span data-ttu-id="ffb0c-136">Na členském serveru nebo pracovní stanici, virtuální účty patří do místního počítače **správci** skupiny a mají přístup k většině systémových prostředků.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-136">On a member server or workstation, virtual accounts belong to the local computer's **Administrators** group, and have access to most system resources.</span></span>
<span data-ttu-id="ffb0c-137">Na řadič domény Active Directory virtuální účty patří do domény **Domain Admins** skupiny.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-137">On an Active Directory Domain Controller, virtual accounts belong to the domain's **Domain Admins** group.</span></span>

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

<span data-ttu-id="ffb0c-138">Pokud role podporuje konfiguraci relace nevyžadují, aby takové široká oprávnění, můžete volitelně zadat skupiny zabezpečení, ke kterým bude patřit virtuální účet.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-138">If the roles supported by the session configuration do not require such broad privileges, you can optionally specify the security groups to which the virtual account will belong.</span></span>
<span data-ttu-id="ffb0c-139">Na členském serveru nebo pracovní stanici musí být určených skupinách zabezpečení místních skupin, nejsou skupiny z domény.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-139">On a member server or workstation, the specified security groups must be local groups, not groups from a domain.</span></span>

<span data-ttu-id="ffb0c-140">Pokud je zadána jedna nebo více skupin zabezpečení, virtuální účet se už nebude patřit do skupiny administrators místní nebo doménový.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-140">When one or more security groups is specified, the virtual account will no longer belong to the local or domain administrators group.</span></span>

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```
> [!NOTE]
> <span data-ttu-id="ffb0c-141">Virtuální účty jsou dočasně udělena přihlášení jako služba vpravo v zásadách zabezpečení místního serveru.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-141">Virtual accounts are temporarily granted the Logon as a service right in the local server security policy.</span></span>  <span data-ttu-id="ffb0c-142">Pokud jeden z VirtualAccountGroups zadaný již byla udělena tato práva v zásadách, budou jednotlivé virtuální účet už přidávat a odebírat z této zásady.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-142">If one of the VirtualAccountGroups specified has already been granted this right in the policy, the individual virtual account will no longer be added and removed from the policy.</span></span>  <span data-ttu-id="ffb0c-143">To může být užitečné v situacích, jako jsou řadiče domény, ve kterém jsou úzce auditovat revize pro zásady zabezpečení řadiče domény.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-143">This can be useful in scenarios such as domain controllers where revisions to the domain controller security policy are closely audited.</span></span>  <span data-ttu-id="ffb0c-144">To je k dispozici pouze ve Windows serveru 2016 a listopadu 2018 nebo novější kumulativní a 2019 systému Windows Server s 2019. ledna nebo pozdější kumulativní.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-144">This is only available in Windows Server 2016 with the November 2018 or later rollup and Windows Server 2019 with the January 2019 or later rollup.</span></span>

#### <a name="group-managed-service-account"></a><span data-ttu-id="ffb0c-145">Účet spravované služby skupiny</span><span class="sxs-lookup"><span data-stu-id="ffb0c-145">Group Managed Service Account</span></span>


<span data-ttu-id="ffb0c-146">Účet skupiny spravované služby (gMSA) pro scénářům, které vyžadují JEA uživateli přístup k síťovým prostředkům, jako jsou ostatní počítače nebo webové služby, je vhodnější identity používat.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-146">For scenarios requiring the JEA user to access network resources such as other machines or web services, a group managed service account (gMSA) is a more appropriate identity to use.</span></span>
<span data-ttu-id="ffb0c-147">účty gMSA poskytnout identitu domény, který slouží k ověřování na základě prostředků na jakýkoli počítač v rámci domény.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-147">gMSA accounts give you a domain identity which can be used to authenticate against resources on any machine within the domain.</span></span>
<span data-ttu-id="ffb0c-148">Práva získáte účtu gMSA se určuje podle zdroje se připojujete.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-148">The rights the gMSA account gives you is determined by the resources you are accessing.</span></span>
<span data-ttu-id="ffb0c-149">Práva správce na všechny počítače nebo služby nebudou mít automaticky, pokud správce počítače nebo služby se explicitně udělí oprávnění účtu gMSA oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-149">You will not automatically have admin rights on any machines or services unless the machine/service administrator has explicitly granted the gMSA account admin privileges.</span></span>

```powershell
# Configure JEA sessions to use the gMSA account in the local computer's domain with the sAMAccountName of 'MyJEAgMSA'
GroupManagedServiceAccount = 'Domain\MyJEAgMSA'
```

<span data-ttu-id="ffb0c-150">účty gMSA by měla sloužit pouze při přístupu k síťovým prostředkům jsou požadovány pro z několika důvodů:</span><span class="sxs-lookup"><span data-stu-id="ffb0c-150">gMSA accounts should only be used when access to network resources are required for a few reasons:</span></span>

- <span data-ttu-id="ffb0c-151">Je obtížnější vysledovat zpět akce, které uživatele při použití účtu gMSA, protože každý uživatel sdílí stejnou identitu spustit jako.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-151">It is harder to trace back actions to a user when using a gMSA account since every user shares the same run-as identity.</span></span> <span data-ttu-id="ffb0c-152">Je potřeba záznamy o studiu relace prostředí PowerShell a protokoly je možné korelovat s jejich akce uživatele.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-152">You will need to consult PowerShell session transcripts and logs to correlate users with their actions.</span></span>

- <span data-ttu-id="ffb0c-153">Účet gMSA může mít přístup k mnoha síťovým prostředkům, kterých je připojující se uživatel nemusí přístup k.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-153">The gMSA account may have access to many network resources which the connecting user does not need access to.</span></span> <span data-ttu-id="ffb0c-154">Vždy pokusí omezení účinný oprávnění v relaci JEA postupovat podle principu nejnižší úrovně oprávnění.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-154">Always try to limit effective permissions in a JEA session to follow the principle of least privilege.</span></span>

> [!NOTE]
> <span data-ttu-id="ffb0c-155">Účty spravované služby skupiny jsou pouze k dispozici ve Windows PowerShell 5.1 nebo novější a na počítačích připojených k doméně.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-155">Group managed service accounts are only available in Windows PowerShell 5.1 or newer and on domain-joined machines.</span></span>


#### <a name="more-information-about-run-as-users"></a><span data-ttu-id="ffb0c-156">Další informace o spouštění jako uživatele</span><span class="sxs-lookup"><span data-stu-id="ffb0c-156">More information about run as users</span></span>

<span data-ttu-id="ffb0c-157">Další informace o spuštění jako identit a jak se zohlednit do zabezpečení JEA relace najdete v [aspekty zabezpečení](security-considerations.md) článku.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-157">Additional information about run as identities and how they factor into the security of a JEA session can be found in the [security considerations](security-considerations.md) article.</span></span>

### <a name="session-transcripts"></a><span data-ttu-id="ffb0c-158">Záznamy o studiu relace</span><span class="sxs-lookup"><span data-stu-id="ffb0c-158">Session transcripts</span></span>

<span data-ttu-id="ffb0c-159">Doporučuje konfiguraci relace JEA konfigurační soubor automaticky záznamu přepisy uživatelské relace.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-159">It is recommended that you configure a JEA session configuration file to automatically record transcripts of users' sessions.</span></span>
<span data-ttu-id="ffb0c-160">Záznamy o studiu relace prostředí PowerShell obsahují informace o připojení uživatele spustit jako identity přiřazené, a příkazy se spouští podle uživatele.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-160">PowerShell session transcripts contain information about the connecting user, the run as identity assigned to them, and the commands run by the user.</span></span>
<span data-ttu-id="ffb0c-161">Mohou být užitečné pro auditování týmu, který je potřeba pochopit, kdo provedl určité změny do systému.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-161">They can be useful to an auditing team who needs to understand who performed a specific change to a system.</span></span>

<span data-ttu-id="ffb0c-162">Ke konfiguraci automatický přepis v konfiguračním souboru relací zadejte cestu ke složce, ve kterém by měly být uložené záznamy o studiu.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-162">To configure automatic transcription in the session configuration file, provide a path to a folder where the transcripts should be stored.</span></span>

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

<span data-ttu-id="ffb0c-163">Zadaná složka musí být nakonfigurovaný zabránit uživatelům ve změnách nebo odstranění všech dat v něm.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-163">The specified folder should be configured to prevent users from modifying or deleting any data in it.</span></span>
<span data-ttu-id="ffb0c-164">Záznamy o studiu jsou zapsány do složky podle místní systémový účet, který vyžaduje oprávnění čtení a zápisu do adresáře.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-164">Transcripts are written to the folder by the Local System account, which requires read and write access to the directory.</span></span>
<span data-ttu-id="ffb0c-165">Standardní uživatelé by měli mít přístup ke složce a omezenou sadu správci zabezpečení mají mít přístup k auditu záznamy o studiu.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-165">Standard users should have no access to the folder, and a limited set of security administrators should have access to audit the transcripts.</span></span>

### <a name="user-drive"></a><span data-ttu-id="ffb0c-166">Jednotka uživatele</span><span class="sxs-lookup"><span data-stu-id="ffb0c-166">User drive</span></span>

<span data-ttu-id="ffb0c-167">Pokud vaše připojujících se uživatelů bude nutné zkopírovat soubory z koncového bodu JEA Chcete-li spustit příkaz, můžete povolit disk uživatele v konfiguračním souboru relace.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-167">If your connecting users will need to copy files to/from the JEA endpoint in order to run a command, you can enable the user drive in the session configuration file.</span></span>
<span data-ttu-id="ffb0c-168">Jednotka uživatele je [PSDrive](https://msdn.microsoft.com/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives) , který se mapuje na jedinečné složku pro každý připojující se uživatel.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-168">The user drive is a [PSDrive](https://msdn.microsoft.com/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives) that is mapped to a unique folder for each connecting user.</span></span>
<span data-ttu-id="ffb0c-169">Tato složka slouží jako místo jejich kopírování souborů ze systému, aniž by jim poskytne přístup k systému souborů úplné nebo vystavení poskytovatele FileSystem provider.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-169">This folder serves as a space for them to copy files to/from the system, without giving them access to the full file system or exposing the FileSystem provider.</span></span>
<span data-ttu-id="ffb0c-170">Obsah jednotky uživatele je trvalé napříč relacemi tak, aby vyhovovaly situací, ve kterém se můžou přerušit připojení k síti.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-170">The user drive contents are persistent across sessions to accommodate situations where network connectivity may be interrupted.</span></span>

```powershell
MountUserDrive = $true
```

<span data-ttu-id="ffb0c-171">Ve výchozím nastavení jednotky uživatele můžete uložit maximálně 50MB dat za uživatele.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-171">By default, the user drive allows you to store a maximum of 50MB of data per user.</span></span>
<span data-ttu-id="ffb0c-172">Můžete omezit množství dat uživatele můžou využívat s *UserDriveMaximumSize* pole.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-172">You can limit the amount of data a user can consume with the *UserDriveMaximumSize* field.</span></span>

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

<span data-ttu-id="ffb0c-173">Pokud nechcete, aby data na jednotce uživatele být trvalé, můžete nakonfigurovat naplánovanou úlohu na systém a automaticky vyčistit složku každou noc.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-173">If you do not want data in the user drive to be persistent, you can configure a scheduled task on the system to automatically clean up the folder every night.</span></span>

> [!NOTE]
> <span data-ttu-id="ffb0c-174">Jednotka uživatele je pouze k dispozici ve Windows PowerShell 5.1 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-174">The user drive is only available in Windows PowerShell 5.1 or newer.</span></span>

### <a name="role-definitions"></a><span data-ttu-id="ffb0c-175">Definice rolí</span><span class="sxs-lookup"><span data-stu-id="ffb0c-175">Role definitions</span></span>

<span data-ttu-id="ffb0c-176">Definice rolí v konfiguračním souboru relace definovat mapování *uživatelé* k *role*.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-176">Role definitions in a session configuration file define the mapping of *users* to *roles*.</span></span>
<span data-ttu-id="ffb0c-177">Každý uživatel nebo skupina součástí toto pole se automaticky udělí oprávnění do koncového bodu JEA po jeho registraci.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-177">Every user or group included in this field will automatically be granted permission to the JEA endpoint when it is registered.</span></span>
<span data-ttu-id="ffb0c-178">Každý uživatel nebo skupina může být zahrnut jako klíče zatřiďovací tabulky jenom jednou, ale je možné přiřadit víc rolí.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-178">Each user or group can be included as a key in the hashtable only once, but can be assigned multiple roles.</span></span>
<span data-ttu-id="ffb0c-179">Název role funkce by měl být název souboru role funkce bez přípony .psrc.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-179">The name of the role capability should be the name of the role capability file, without the .psrc extension.</span></span>

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

<span data-ttu-id="ffb0c-180">Pokud uživatel patří do více než jedné skupiny v definici role, dostanou přístup k rolím jednotlivých.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-180">If a user belongs to more than one group in the role definition, they will get access to the roles of each.</span></span>
<span data-ttu-id="ffb0c-181">Pokud dvě role udělit přístup ke stejné rutiny, udělí se nejvíce omezující sada parametrů pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-181">If two roles grant access to the same cmdlets, the most permissive parameter set will be granted to the user.</span></span>

<span data-ttu-id="ffb0c-182">Při zadávání v poli definice role místního uživatele nebo skupiny, nezapomeňte použít název počítače (nikoli *localhost* nebo *.*) před zpětným lomítkem.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-182">When specifying local users or groups in the role definitions field, be sure to use the computer name (not *localhost* or *.*) before the backslash.</span></span>
<span data-ttu-id="ffb0c-183">Název počítače můžete zkontrolovat, že zkontrolujete `$env:computername` proměnné.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-183">You can check the computer name by inspecting the `$env:computername` variable.</span></span>

```powershell
RoleDefinitions = @{
    'MyComputerName\MyLocalGroup' = @{ RoleCapabilities = 'DnsAuditor' }
}
```

### <a name="role-capability-search-order"></a><span data-ttu-id="ffb0c-184">Pořadí hledání funkce rolí</span><span class="sxs-lookup"><span data-stu-id="ffb0c-184">Role capability search order</span></span>
<span data-ttu-id="ffb0c-185">Jak je znázorněno v příkladu výše, funkce rolí odkazuje jednoduchý název (název souboru bez přípony) soubor funkce role.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-185">As shown in the example above, role capabilities are referenced by the flat name (filename without the extension) of the role capability file.</span></span>
<span data-ttu-id="ffb0c-186">Pokud více funkcí role jsou k dispozici v systému se stejným názvem, bez stromové struktury, prostředí PowerShell pomocí jeho pořadí implicitní hledání vyberte soubor funkce účinného role.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-186">If multiple role capabilities are available on the system with the same flat name, PowerShell will use its implicit search order to select the effective role capability file.</span></span>
<span data-ttu-id="ffb0c-187">Bude **není** poskytnout přístup ke všem souborům funkce role se stejným názvem.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-187">It will **not** give access to all role capability files with the same name.</span></span>

<span data-ttu-id="ffb0c-188">JEA používá `$env:PSModulePath` proměnnou prostředí k určení, které cesty kontrolovala soubory funkce role.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-188">JEA uses the `$env:PSModulePath` environment variable to determine which paths to scan for role capability files.</span></span>
<span data-ttu-id="ffb0c-189">V rámci každé z těchto cest JEA bude hledat platný moduly Powershellu, které obsahují podsložku "RoleCapabilities".</span><span class="sxs-lookup"><span data-stu-id="ffb0c-189">Within each of those paths, JEA will look for valid PowerShell modules that contain a "RoleCapabilities" subfolder.</span></span>
<span data-ttu-id="ffb0c-190">Stejně jako u importu modulů JEA upřednostňuje funkce rolí, které jsou součástí Windows k funkcím vlastní role se stejným názvem.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-190">As with importing modules, JEA prefers role capabilities that are shipped with Windows to custom role capabilities with the same name.</span></span>
<span data-ttu-id="ffb0c-191">Pro všechny ostatní konflikty názvů priorita je určen podle pořadí, ve kterém Windows zobrazí soubory v adresáři (není zaručena podle abecedy).</span><span class="sxs-lookup"><span data-stu-id="ffb0c-191">For all other naming conflicts, precedence is determined by the order in which Windows enumerates the files in the directory (not guaranteed to be alphabetically).</span></span>
<span data-ttu-id="ffb0c-192">První soubor funkce role najít odpovídající požadovaný název se použije pro připojení uživatele.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-192">The first role capability file found that matches the desired name will be used for the connecting user.</span></span>

<span data-ttu-id="ffb0c-193">Protože pořadí hledání funkce role není deterministický. Pokud dvě nebo více rolí možnosti sdílejí stejný název, je **důrazně doporučujeme** zajištění funkcí role na počítači máte jedinečné názvy.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-193">Since the role capability search order is not deterministic when two or more role capabilities share the same name, it is **strongly recommended** that you ensure role capabilities have unique names on your machine.</span></span>

### <a name="conditional-access-rules"></a><span data-ttu-id="ffb0c-194">Pravidla podmíněného přístupu</span><span class="sxs-lookup"><span data-stu-id="ffb0c-194">Conditional access rules</span></span>

<span data-ttu-id="ffb0c-195">Všichni uživatelé a skupiny součástí RoleDefinitions pole jsou automaticky udělen přístup do koncových bodů JEA.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-195">All users and groups included in the RoleDefinitions field are automatically granted access to JEA endpoints.</span></span>
<span data-ttu-id="ffb0c-196">Pravidla podmíněného přístupu umožňují Upřesnit tohoto přístupu a vyžadovat, aby uživatelé patří do skupiny další zabezpečení, které nemají vliv role, které jsou přiřazeny.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-196">Conditional access rules allow you to refine this access and require users to belong to additional security groups which do not impact the roles which they are assigned.</span></span>
<span data-ttu-id="ffb0c-197">To může být užitečné, pokud chcete integrovat "počítačům v čase" privilegovaný přístup k řešení pro správu, ověřování pomocí čipové karty nebo jiného řešení vícefaktorového ověřování s JEA.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-197">This can be useful if you want to integrate a "just in time" privileged access management solution, smartcard authentication, or other multifactor authentication solution with JEA.</span></span>

<span data-ttu-id="ffb0c-198">Pravidla podmíněného přístupu jsou definovány v poli RequiredGroups v konfiguračním souboru relace.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-198">Conditional access rules are defined in the RequiredGroups field in a session configuration file.</span></span>
<span data-ttu-id="ffb0c-199">Tady můžete zadat zatřiďovací tabulku (volitelně vnořené), která používá "A" a "Nebo" klíče k vytvoření pravidla.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-199">There, you can provide a hashtable (optionally nested) that uses 'And' and 'Or' keys to construct your rules.</span></span>
<span data-ttu-id="ffb0c-200">Tady je několik příkladů toho, jak využít toto pole:</span><span class="sxs-lookup"><span data-stu-id="ffb0c-200">Here are some examples of how to leverage this field:</span></span>

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

> [!NOTE]
> <span data-ttu-id="ffb0c-201">Pravidla podmíněného přístupu jsou pouze k dispozici ve Windows PowerShell 5.1 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-201">Conditional access rules are only available in Windows PowerShell 5.1 or newer.</span></span>

### <a name="other-properties"></a><span data-ttu-id="ffb0c-202">Další vlastnosti</span><span class="sxs-lookup"><span data-stu-id="ffb0c-202">Other properties</span></span>
<span data-ttu-id="ffb0c-203">Soubory konfigurace relace můžete také provést všechno, co soubor funkce role můžete provést pouze bez schopnost spojovací uživatelům poskytnout přístup na různé příkazy.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-203">Session configuration files can also do everything a role capability file can do, just without the ability to give connecting users access to different commands.</span></span>
<span data-ttu-id="ffb0c-204">Pokud chcete povolit všem uživatelům přístup ke konkrétní rutiny, funkce nebo poskytovatelů, můžete tak učinit přímo v konfiguračním souboru relace.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-204">If you want to allow all users access to specific cmdlets, functions, or providers, you can do so right in the session configuration file.</span></span>
<span data-ttu-id="ffb0c-205">Úplný seznam podporovaných vlastností v souboru konfigurace relace, spusťte `Get-Help New-PSSessionConfigurationFile -Full`.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-205">For a full list of supported properties in the session configuration file, run `Get-Help New-PSSessionConfigurationFile -Full`.</span></span>

## <a name="testing-a-session-configuration-file"></a><span data-ttu-id="ffb0c-206">Testování souboru konfigurace relace</span><span class="sxs-lookup"><span data-stu-id="ffb0c-206">Testing a session configuration file</span></span>

<span data-ttu-id="ffb0c-207">Můžete otestovat pomocí konfigurace relace [testovací PSSessionConfigurationFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) rutiny.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-207">You can test a session configuration using the [Test-PSSessionConfigurationFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) cmdlet.</span></span>
<span data-ttu-id="ffb0c-208">Důrazně doporučujeme, abyste otestovali konfiguračního souboru relace Pokud jste upravili soubor pssc ručně pomocí textového editoru k zajištění, že je syntaxe správná.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-208">It is strongly recommended that you test your session configuration file if you have edited the pssc file manually using a text editor to ensure the syntax is correct.</span></span>
<span data-ttu-id="ffb0c-209">Pokud soubor konfigurace relace neprojde tímto testem, nebudete moci úspěšně zaregistrovat v systému.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-209">If a session configuration file does not pass this test, it will not be able to be successfully registered on the system.</span></span>

## <a name="sample-session-configuration-file"></a><span data-ttu-id="ffb0c-210">Ukázkový soubor konfigurace relace</span><span class="sxs-lookup"><span data-stu-id="ffb0c-210">Sample session configuration file</span></span>

<span data-ttu-id="ffb0c-211">Níže je úplný příklad ukazuje, jak vytvořit a ověřit konfiguraci relace pro JEA.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-211">Below is a complete example showing how to create and validate a session configuration for JEA.</span></span>
<span data-ttu-id="ffb0c-212">Všimněte si, že jsou vytvořeny a uloženy v definicích rolí `$roles` proměnné pro lepší čitelnost a pohodlí.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-212">Note that the role definitions are created and stored in the `$roles` variable for convenience and readability.</span></span>
<span data-ttu-id="ffb0c-213">Není potřeba udělat.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-213">It is not a requirement to do so.</span></span>

```powershell
$roles = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}

New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\JEAConfig.pssc -RunAsVirtualAccount -TranscriptDirectory 'C:\ProgramData\JEAConfiguration\Transcripts' -RoleDefinitions $roles -RequiredGroups @{ Or = '2FA-logon', 'smartcard-logon' }
Test-PSSessionConfigurationFile -Path .\JEAConfig.pssc # should yield True
```

## <a name="updating-session-configuration-files"></a><span data-ttu-id="ffb0c-214">Aktualizace relace konfiguračních souborů</span><span class="sxs-lookup"><span data-stu-id="ffb0c-214">Updating session configuration files</span></span>

<span data-ttu-id="ffb0c-215">Pokud potřebujete změnit vlastnosti konfigurace relace JEA, včetně mapování uživatelů k rolím, je nutné [zrušit registraci](register-jea.md#unregistering-jea-configurations) a [přeregistrovat](register-jea.md) JEA konfiguraci relace.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-215">If you need to change properties of a JEA session configuration, including the mapping of users to roles, you must [unregister](register-jea.md#unregistering-jea-configurations) and [re-register](register-jea.md) the JEA session configuration.</span></span>
<span data-ttu-id="ffb0c-216">Při konfiguraci relace JEA přeregistrovat, použijte aktualizované prostředí PowerShell relace konfiguračního souboru, který obsahuje vaše požadované změny.</span><span class="sxs-lookup"><span data-stu-id="ffb0c-216">When you re-register the JEA session configuration, use an updated PowerShell session configuration file that includes your desired changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffb0c-217">Další kroky</span><span class="sxs-lookup"><span data-stu-id="ffb0c-217">Next steps</span></span>

- [<span data-ttu-id="ffb0c-218">Zaregistruje konfiguraci funkce JEA</span><span class="sxs-lookup"><span data-stu-id="ffb0c-218">Register a JEA configuration</span></span>](register-jea.md)
- [<span data-ttu-id="ffb0c-219">Autor JEA role</span><span class="sxs-lookup"><span data-stu-id="ffb0c-219">Author JEA roles</span></span>](role-capabilities.md)
