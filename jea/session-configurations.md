---
ms.date: 06/12/2017
keywords: jea, prostředí powershell, zabezpečení
title: Konfigurace relace JEA
ms.openlocfilehash: 3e5a663be8e7aba09a2592c278224cd892c89a20
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190090"
---
# <a name="jea-session-configurations"></a><span data-ttu-id="1752c-103">Konfigurace relace JEA</span><span class="sxs-lookup"><span data-stu-id="1752c-103">JEA Session Configurations</span></span>

> <span data-ttu-id="1752c-104">Platí pro: prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1752c-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="1752c-105">Koncový bod JEA je zaregistrován v systému pomocí vytvoření a registrace konfigurační soubor relace prostředí PowerShell v určitým způsobem.</span><span class="sxs-lookup"><span data-stu-id="1752c-105">A JEA endpoint is registered on a system by creating and registering a PowerShell session configuration file in a specific way.</span></span>
<span data-ttu-id="1752c-106">Určení konfigurací relace *kdo* můžete použít JEA koncový bod a které rolí budou mít přístup k.</span><span class="sxs-lookup"><span data-stu-id="1752c-106">Session configurations determine *who* can use the JEA endpoint, and which role(s) they will have access to.</span></span>
<span data-ttu-id="1752c-107">Budou také definovat globální nastavení, které platí pro všechny role uživatele v relaci JEA.</span><span class="sxs-lookup"><span data-stu-id="1752c-107">They also define global settings that apply to users of any role in the JEA session.</span></span>

<span data-ttu-id="1752c-108">Toto téma popisuje postup vytvoření konfiguračního souboru relace prostředí PowerShell a zaregistrujte koncový bod JEA.</span><span class="sxs-lookup"><span data-stu-id="1752c-108">This topic describes how to create a PowerShell session configuration file and register a JEA endpoint.</span></span>

## <a name="create-a-session-configuration-file"></a><span data-ttu-id="1752c-109">Vytvoření konfiguračního souboru relace</span><span class="sxs-lookup"><span data-stu-id="1752c-109">Create a session configuration file</span></span>

<span data-ttu-id="1752c-110">Chcete-li zaregistrovat koncový bod JEA, budete muset zadat, jak by měl být nakonfigurovaný tohoto koncového bodu.</span><span class="sxs-lookup"><span data-stu-id="1752c-110">In order to register a JEA endpoint, you need to specify how that endpoint should be configured.</span></span>
<span data-ttu-id="1752c-111">Existuje řada možností vzít v úvahu zde nejdůležitější, z které toho, kdo má mít přístup ke koncovému bodu JEA, které role se jejich přiřazen, které identity JEA použije skrytě a co bude název koncového bodu JEA.</span><span class="sxs-lookup"><span data-stu-id="1752c-111">There are many options to consider here, the most important of which being who should have access to the JEA endpoint, which roles will they be assigned, which identity will JEA use under the covers, and what will be the name of the JEA endpoint.</span></span>
<span data-ttu-id="1752c-112">Tyto jsou pro všechna definovaná v konfiguračním souboru relace prostředí PowerShell, který je datový soubor prostředí PowerShell koncové s příponou .pssc.</span><span class="sxs-lookup"><span data-stu-id="1752c-112">These are all defined in a PowerShell session configuration file, which is a PowerShell data file ending with a .pssc extension.</span></span>

<span data-ttu-id="1752c-113">Pokud chcete vytvořit konfigurační soubor kostru relace pro koncové body JEA, spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="1752c-113">To create a skeleton session configuration file for JEA endpoints, run the following command.</span></span>

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> <span data-ttu-id="1752c-114">Nejběžnější možnosti konfigurace jsou součástí souboru kostru ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="1752c-114">Only the most common configuration options are included in the skeleton file by default.</span></span>
> <span data-ttu-id="1752c-115">Použití `-Full` přepínač tak, aby vygenerované PSSC zahrnout všech příslušných nastavení.</span><span class="sxs-lookup"><span data-stu-id="1752c-115">Use the `-Full` switch to include all applicable settings in the generated PSSC.</span></span>

<span data-ttu-id="1752c-116">Soubor konfigurace relace můžete otevřít v každém textovém editoru.</span><span class="sxs-lookup"><span data-stu-id="1752c-116">You can open the session configuration file in any text editor.</span></span>
<span data-ttu-id="1752c-117">`-SessionType RestrictedRemoteServer` Pole označuje, že konfigurace relace bude používat JEA pro zabezpečené správy.</span><span class="sxs-lookup"><span data-stu-id="1752c-117">The `-SessionType RestrictedRemoteServer` field indicates that the session configuration will be used by JEA for secure management.</span></span>
<span data-ttu-id="1752c-118">Relace nakonfigurovali tímto způsobem bude fungovat v [NoLanguage režimu](https://technet.microsoft.com/library/dn433292.aspx) a mít pouze následující příkazy 8 výchozí (a aliasy) k dispozici:</span><span class="sxs-lookup"><span data-stu-id="1752c-118">Sessions configured this way will operate in [NoLanguage mode](https://technet.microsoft.com/library/dn433292.aspx) and only have the following 8 default commands (and aliases) available:</span></span>

- <span data-ttu-id="1752c-119">Clear-Host (cls, zrušte zaškrtnutí)</span><span class="sxs-lookup"><span data-stu-id="1752c-119">Clear-Host (cls, clear)</span></span>
- <span data-ttu-id="1752c-120">Ukončení-PSSession (exsn, ukončení)</span><span class="sxs-lookup"><span data-stu-id="1752c-120">Exit-PSSession (exsn, exit)</span></span>
- <span data-ttu-id="1752c-121">Get-Command (gcm)</span><span class="sxs-lookup"><span data-stu-id="1752c-121">Get-Command (gcm)</span></span>
- <span data-ttu-id="1752c-122">Get-FormatData</span><span class="sxs-lookup"><span data-stu-id="1752c-122">Get-FormatData</span></span>
- <span data-ttu-id="1752c-123">Get-Help</span><span class="sxs-lookup"><span data-stu-id="1752c-123">Get-Help</span></span>
- <span data-ttu-id="1752c-124">Objekt míry (měr)</span><span class="sxs-lookup"><span data-stu-id="1752c-124">Measure-Object (measure)</span></span>
- <span data-ttu-id="1752c-125">Odchozí výchozí</span><span class="sxs-lookup"><span data-stu-id="1752c-125">Out-Default</span></span>
- <span data-ttu-id="1752c-126">Select-Object (vyberte)</span><span class="sxs-lookup"><span data-stu-id="1752c-126">Select-Object (select)</span></span>

<span data-ttu-id="1752c-127">Žádní zprostředkovatelé prostředí PowerShell jsou k dispozici, ani se, že všechny externí programy (spustitelné soubory, skripty atd.).</span><span class="sxs-lookup"><span data-stu-id="1752c-127">No PowerShell providers are available, nor are any external programs (executables, scripts, etc.).</span></span>

<span data-ttu-id="1752c-128">Existuje několik dalších polí, které můžete nakonfigurovat pro relaci JEA.</span><span class="sxs-lookup"><span data-stu-id="1752c-128">There are several other fields you will want to configure for the JEA session.</span></span>
<span data-ttu-id="1752c-129">Že jsou popsané v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="1752c-129">They are covered in the following sections.</span></span>

### <a name="choose-the-jea-identity"></a><span data-ttu-id="1752c-130">Zvolte identitu JEA</span><span class="sxs-lookup"><span data-stu-id="1752c-130">Choose the JEA identity</span></span>

<span data-ttu-id="1752c-131">Na pozadí musí JEA identity (účet) pro použití při spouštění příkazů připojeného uživatele.</span><span class="sxs-lookup"><span data-stu-id="1752c-131">Behind the scenes, JEA needs an identity (account) to use when running a connected user's commands.</span></span>
<span data-ttu-id="1752c-132">Rozhodnete, které identity JEA použije v konfiguračním souboru relace.</span><span class="sxs-lookup"><span data-stu-id="1752c-132">You decide which identity JEA will use in the session configuration file.</span></span>

#### <a name="local-virtual-account"></a><span data-ttu-id="1752c-133">Místní virtuální účet</span><span class="sxs-lookup"><span data-stu-id="1752c-133">Local Virtual Account</span></span>

<span data-ttu-id="1752c-134">Pokud role nepodporuje tento koncový bod JEA se používají ke správě místního počítače a účet místního správce stačí ke spuštění příkazů úspěšně, byste měli nakonfigurovat JEA, aby používala účet místní virtuální.</span><span class="sxs-lookup"><span data-stu-id="1752c-134">If the roles supported by this JEA endpoint are all used to manage the local machine, and a local administrator account is sufficient to run the commands succesfully, you should configure JEA to use a local virtual account.</span></span>
<span data-ttu-id="1752c-135">Virtuální účty jsou dočasné účty, které jsou jedinečné pro konkrétního uživatele a pouze poslední dobu trvání relace prostředí PowerShell systému.</span><span class="sxs-lookup"><span data-stu-id="1752c-135">Virtual accounts are temporary accounts that are unique to a specific user and only last for the duration of their PowerShell session.</span></span>
<span data-ttu-id="1752c-136">Na členském serveru nebo pracovní stanici, virtuální účty patří do místního počítače **správci** skupiny a mají přístup k většině systémové prostředky.</span><span class="sxs-lookup"><span data-stu-id="1752c-136">On a member server or workstation, virtual accounts belong to the local computer's **Administrators** group, and have access to most system resources.</span></span>
<span data-ttu-id="1752c-137">Na řadiči domény Active Directory, virtuální účty patří do domény **Domain Admins** skupiny.</span><span class="sxs-lookup"><span data-stu-id="1752c-137">On an Active Directory Domain Controller, virtual accounts belong to the domain's **Domain Admins** group.</span></span>

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

<span data-ttu-id="1752c-138">Pokud role nepodporuje konfiguraci relace nevyžadují, aby takové široká oprávnění, Volitelně můžete zadat skupiny zabezpečení, do kterých budou virtuální účet patří.</span><span class="sxs-lookup"><span data-stu-id="1752c-138">If the roles supported by the session configuration do not require such broad privileges, you can optionally specify the security groups to which the virtual account will belong.</span></span>
<span data-ttu-id="1752c-139">Na členském serveru nebo pracovní stanici musí být určených skupinách zabezpečení místních skupin, nejsou skupiny z domény.</span><span class="sxs-lookup"><span data-stu-id="1752c-139">On a member server or workstation, the specified security groups must be local groups, not groups from a domain.</span></span>

<span data-ttu-id="1752c-140">Pokud je zadána jedna nebo více skupin zabezpečení, bude virtuální účet už patřit do místní nebo doménové skupiny správců.</span><span class="sxs-lookup"><span data-stu-id="1752c-140">When one or more security groups is specified, the virtual account will no longer belong to the local or domain administrators group.</span></span>

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```

#### <a name="group-managed-service-account"></a><span data-ttu-id="1752c-141">Účet spravované služby skupiny</span><span class="sxs-lookup"><span data-stu-id="1752c-141">Group Managed Service Account</span></span>


<span data-ttu-id="1752c-142">Účet skupiny spravované služby (gMSA) pro scénářům, které vyžadují JEA uživatelům přístup k síťovým prostředkům, například další počítače nebo webové služby, je vhodnější identity použít.</span><span class="sxs-lookup"><span data-stu-id="1752c-142">For scenarios requiring the JEA user to access network resources such as other machines or web services, a group managed service account (gMSA) is a more appropriate identity to use.</span></span>
<span data-ttu-id="1752c-143">účty gMSA získáte identitu domény, který můžete použít k ověřování na základě prostředků na libovolném počítači v rámci domény.</span><span class="sxs-lookup"><span data-stu-id="1752c-143">gMSA accounts give you a domain identity which can be used to authenticate against resources on any machine within the domain.</span></span>
<span data-ttu-id="1752c-144">Práva poskytuje účet gMSA, je určen prostředky se připojujete.</span><span class="sxs-lookup"><span data-stu-id="1752c-144">The rights the gMSA account gives you is determined by the resources you are accessing.</span></span>
<span data-ttu-id="1752c-145">Práva správce na všechny počítače nebo služby, nebudete mít automaticky, pokud správce počítače nebo služby se explicitně udělí oprávnění účtu gMSA oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="1752c-145">You will not automatically have admin rights on any machines or services unless the machine/service administrator has explicitly granted the gMSA account admin privileges.</span></span>

```powershell
# Configure JEA sessions to use the gMSA account in the local computer's domain with the sAMAccountName of 'MyJEAgMSA'
GroupManagedServiceAccount = 'Domain\MyJEAgMSA'
```

<span data-ttu-id="1752c-146">účty gMSA musí být použit pouze při přístupu k síťovým prostředkům jsou požadovány pro z několika důvodů:</span><span class="sxs-lookup"><span data-stu-id="1752c-146">gMSA accounts should only be used when access to network resources are required for a few reasons:</span></span>

- <span data-ttu-id="1752c-147">Je těžší vysledovat zpět akce na uživatele při použití účtu gMSA vzhledem k tomu, že každý uživatel sdílí stejnou identitu spustit jako.</span><span class="sxs-lookup"><span data-stu-id="1752c-147">It is harder to trace back actions to a user when using a gMSA account since every user shares the same run-as identity.</span></span> <span data-ttu-id="1752c-148">Musíte se prostudovat přepisy relace prostředí PowerShell a protokoly ke koordinaci uživatelů s jejich akce.</span><span class="sxs-lookup"><span data-stu-id="1752c-148">You will need to consult PowerShell session transcripts and logs to correlate users with their actions.</span></span>

- <span data-ttu-id="1752c-149">Účet gMSA může mít přístup k mnoha síťovým prostředkům, které je připojující se uživatel nemusí přístup k.</span><span class="sxs-lookup"><span data-stu-id="1752c-149">The gMSA account may have access to many network resources which the connecting user does not need access to.</span></span> <span data-ttu-id="1752c-150">Vždy pokusí omezení skutečná oprávnění v relaci JEA podle Princip nejnižších nutných oprávnění.</span><span class="sxs-lookup"><span data-stu-id="1752c-150">Always try to limit effective permissions in a JEA session to follow the principle of least privilege.</span></span>

> [!NOTE]
> <span data-ttu-id="1752c-151">Účty spravované služby skupiny jsou pouze k dispozici v systému Windows PowerShell 5.1 nebo novější a na počítačích připojených k doméně.</span><span class="sxs-lookup"><span data-stu-id="1752c-151">Group managed service accounts are only available in Windows PowerShell 5.1 or newer and on domain-joined machines.</span></span>


#### <a name="more-information-about-run-as-users"></a><span data-ttu-id="1752c-152">Další informace o spouštění jako uživatele</span><span class="sxs-lookup"><span data-stu-id="1752c-152">More information about run as users</span></span>

<span data-ttu-id="1752c-153">Další informace o spuštění jako identit a jak se zohlednit do zabezpečení JEA relace najdete v [aspekty zabezpečení](security-considerations.md) článku.</span><span class="sxs-lookup"><span data-stu-id="1752c-153">Additional information about run as identities and how they factor into the security of a JEA session can be found in the [security considerations](security-considerations.md) article.</span></span>

### <a name="session-transcripts"></a><span data-ttu-id="1752c-154">Přepisy relace</span><span class="sxs-lookup"><span data-stu-id="1752c-154">Session transcripts</span></span>

<span data-ttu-id="1752c-155">Doporučujeme nakonfigurovat JEA relace konfigurační soubor pro automaticky záznamů přepisy uživatelské relace.</span><span class="sxs-lookup"><span data-stu-id="1752c-155">It is recommended that you configure a JEA session configuration file to automatically record transcripts of users' sessions.</span></span>
<span data-ttu-id="1752c-156">Přepisy relace prostředí PowerShell obsahují informace o připojování uživateli spustit jako identity přiřazen, a spusťte příkazy uživatelem.</span><span class="sxs-lookup"><span data-stu-id="1752c-156">PowerShell session transcripts contain information about the connecting user, the run as identity assigned to them, and the commands run by the user.</span></span>
<span data-ttu-id="1752c-157">Mohou být užitečné auditování týmu, který potřebuje zjistit, kdo provedl konkrétní změny do systému.</span><span class="sxs-lookup"><span data-stu-id="1752c-157">They can be useful to an auditing team who needs to understand who performed a specific change to a system.</span></span>

<span data-ttu-id="1752c-158">Ke konfiguraci automatického přepis v konfiguračním souboru relace, zadejte cesta ke složce, kde by měly být uložené přepisy.</span><span class="sxs-lookup"><span data-stu-id="1752c-158">To configure automatic transcription in the session configuration file, provide a path to a folder where the transcripts should be stored.</span></span>

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

<span data-ttu-id="1752c-159">V zadané složce musí být nakonfigurovaný tak, aby uživatelé z úpravy nebo odstranění všech dat v něm.</span><span class="sxs-lookup"><span data-stu-id="1752c-159">The specified folder should be configured to prevent users from modifying or deleting any data in it.</span></span>
<span data-ttu-id="1752c-160">Přepisy jsou zapsány do složky, pomocí účtu místního systému, který vyžaduje oprávnění ke čtení a zápisu do adresáře.</span><span class="sxs-lookup"><span data-stu-id="1752c-160">Transcripts are written to the folder by the Local System account, which requires read and write access to the directory.</span></span>
<span data-ttu-id="1752c-161">Standardní uživatelé musí mít žádný přístup ke složce a omezená sada správce zabezpečení mají mít přístup k auditu přepisy.</span><span class="sxs-lookup"><span data-stu-id="1752c-161">Standard users should have no access to the folder, and a limited set of security administrators should have access to audit the transcripts.</span></span>

### <a name="user-drive"></a><span data-ttu-id="1752c-162">Jednotka uživatele</span><span class="sxs-lookup"><span data-stu-id="1752c-162">User drive</span></span>

<span data-ttu-id="1752c-163">Pokud vaši uživatelé připojující bude nutné zkopírovat soubory z koncového bodu JEA aby bylo možné spustit příkaz, můžete povolit disk uživatele v konfiguračním souboru relace.</span><span class="sxs-lookup"><span data-stu-id="1752c-163">If your connecting users will need to copy files to/from the JEA endpoint in order to run a command, you can enable the user drive in the session configuration file.</span></span>
<span data-ttu-id="1752c-164">Je jednotka uživatele [PSDrive](https://msdn.microsoft.com/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives) který se mapuje na jedinečné složku pro každý připojující se uživatel.</span><span class="sxs-lookup"><span data-stu-id="1752c-164">The user drive is a [PSDrive](https://msdn.microsoft.com/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives) that is mapped to a unique folder for each connecting user.</span></span>
<span data-ttu-id="1752c-165">Tato složka slouží jako prostor pro ně kopírovat soubory do systému, nebo z nich bez bude mít přístup k systému souborů úplné nebo vystavení zprostředkovatele systému souborů.</span><span class="sxs-lookup"><span data-stu-id="1752c-165">This folder serves as a space for them to copy files to/from the system, without giving them access to the full file system or exposing the FileSystem provider.</span></span>
<span data-ttu-id="1752c-166">Obsah jednotky uživatele je trvalé napříč relacemi, aby dokázala pojmout situacích, kde může přerušit připojení k síti.</span><span class="sxs-lookup"><span data-stu-id="1752c-166">The user drive contents are persistent across sessions to accommodate situations where network connectivity may be interrupted.</span></span>

```powershell
MountUserDrive = $true
```

<span data-ttu-id="1752c-167">Ve výchozím nastavení jednotka uživatele můžete uložit maximálně 50MB dat za uživatele.</span><span class="sxs-lookup"><span data-stu-id="1752c-167">By default, the user drive allows you to store a maximum of 50MB of data per user.</span></span>
<span data-ttu-id="1752c-168">Můžete omezit množství dat, může uživatel využít s *UserDriveMaximumSize* pole.</span><span class="sxs-lookup"><span data-stu-id="1752c-168">You can limit the amount of data a user can consume with the *UserDriveMaximumSize* field.</span></span>

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

<span data-ttu-id="1752c-169">Pokud nechcete, aby se data na jednotce uživatele jako trvalé, můžete nakonfigurovat naplánovanou úlohu v systému, aby automaticky vyčistit složku každou noc.</span><span class="sxs-lookup"><span data-stu-id="1752c-169">If you do not want data in the user drive to be persistent, you can configure a scheduled task on the system to automatically clean up the folder every night.</span></span>

> [!NOTE]
> <span data-ttu-id="1752c-170">Jednotka uživatele je pouze k dispozici v systému Windows PowerShell 5.1 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="1752c-170">The user drive is only available in Windows PowerShell 5.1 or newer.</span></span>

### <a name="role-definitions"></a><span data-ttu-id="1752c-171">Definice rolí</span><span class="sxs-lookup"><span data-stu-id="1752c-171">Role definitions</span></span>

<span data-ttu-id="1752c-172">Definice rolí v konfiguračním souboru relace definovat mapování *uživatelé* k *role*.</span><span class="sxs-lookup"><span data-stu-id="1752c-172">Role definitions in a session configuration file define the mapping of *users* to *roles*.</span></span>
<span data-ttu-id="1752c-173">Každý uživatel nebo skupina součástí toto pole automaticky udělí oprávnění ke koncovému bodu JEA po jeho registraci.</span><span class="sxs-lookup"><span data-stu-id="1752c-173">Every user or group included in this field will automatically be granted permission to the JEA endpoint when it is registered.</span></span>
<span data-ttu-id="1752c-174">Každý uživatel nebo skupina může být zahrnuta jako klíč v zatřiďovací tabulce pouze jednou, ale mohou být přiřazeny více rolí.</span><span class="sxs-lookup"><span data-stu-id="1752c-174">Each user or group can be included as a key in the hashtable only once, but can be assigned multiple roles.</span></span>
<span data-ttu-id="1752c-175">Název funkce role musí být název souboru funkce role, bez přípony .psrc.</span><span class="sxs-lookup"><span data-stu-id="1752c-175">The name of the role capability should be the name of the role capability file, without the .psrc extension.</span></span>

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

<span data-ttu-id="1752c-176">Pokud uživatel patří do více než jedné skupiny v definici role, získají přístup k rolím jednotlivých.</span><span class="sxs-lookup"><span data-stu-id="1752c-176">If a user belongs to more than one group in the role definition, they will get access to the roles of each.</span></span>
<span data-ttu-id="1752c-177">Pokud dvě role uděluje přístup k stejné rutiny, bude udělen nejvíce projektovou sada parametrů pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="1752c-177">If two roles grant access to the same cmdlets, the most permissive parameter set will be granted to the user.</span></span>

<span data-ttu-id="1752c-178">Při zadávání místního uživatele nebo skupiny do pole definice role, nezapomeňte použít název počítače (ne *localhost* nebo *.*) před zpětné lomítko.</span><span class="sxs-lookup"><span data-stu-id="1752c-178">When specifying local users or groups in the role definitions field, be sure to use the computer name (not *localhost* or *.*) before the backslash.</span></span>
<span data-ttu-id="1752c-179">Název počítače můžete zkontrolovat zkontrolováním `$env:computername` proměnné.</span><span class="sxs-lookup"><span data-stu-id="1752c-179">You can check the computer name by inspecting the `$env:computername` variable.</span></span>

```powershell
RoleDefinitions = @{
    'MyComputerName\MyLocalGroup' = @{ RoleCapabilities = 'DnsAuditor' }
}
```

### <a name="role-capability-search-order"></a><span data-ttu-id="1752c-180">Pořadí hledání schopnosti role</span><span class="sxs-lookup"><span data-stu-id="1752c-180">Role capability search order</span></span>
<span data-ttu-id="1752c-181">Jak je znázorněno v příkladu nahoře, funkce role odkazuje plochý název (název souboru bez přípony) souboru funkce role.</span><span class="sxs-lookup"><span data-stu-id="1752c-181">As shown in the example above, role capabilities are referenced by the flat name (filename without the extension) of the role capability file.</span></span>
<span data-ttu-id="1752c-182">Pokud jsou k dispozici v systému se stejným názvem ploché více možnosti role, prostředí PowerShell pomocí jeho pořadí implicitní hledání vyberte soubor schopností efektivní role.</span><span class="sxs-lookup"><span data-stu-id="1752c-182">If multiple role capabilities are available on the system with the same flat name, PowerShell will use its implicit search order to select the effective role capability file.</span></span>
<span data-ttu-id="1752c-183">Zruší **není** poskytnout přístup ke všem souborům schopnosti role se stejným názvem.</span><span class="sxs-lookup"><span data-stu-id="1752c-183">It will **not** give access to all role capability files with the same name.</span></span>

<span data-ttu-id="1752c-184">Používá JEA `$env:PSModulePath` proměnné prostředí můžete zjistit které cesty pro hledání souborů schopnosti role.</span><span class="sxs-lookup"><span data-stu-id="1752c-184">JEA uses the `$env:PSModulePath` environment variable to determine which paths to scan for role capability files.</span></span>
<span data-ttu-id="1752c-185">V každém z těchto cestách JEA bude hledat platný modulů prostředí PowerShell, které obsahují podsložku "RoleCapabilities".</span><span class="sxs-lookup"><span data-stu-id="1752c-185">Within each of those paths, JEA will look for valid PowerShell modules that contain a "RoleCapabilities" subfolder.</span></span>
<span data-ttu-id="1752c-186">Stejně jako u importu modulů, upřednostní JEA funkce role, které jsou součástí systému Windows k funkcím vlastní role se stejným názvem.</span><span class="sxs-lookup"><span data-stu-id="1752c-186">As with importing modules, JEA prefers role capabilities that are shipped with Windows to custom role capabilities with the same name.</span></span>
<span data-ttu-id="1752c-187">Pro všechny ostatní ke konfliktům s názvy přednost před je dáno pořadí, ve kterém Windows zjistí počet souborů v adresáři (není zaručena bezpečnost pro abecedy).</span><span class="sxs-lookup"><span data-stu-id="1752c-187">For all other naming conflicts, precedence is determined by the order in which Windows enumerates the files in the directory (not guaranteed to be alphabetically).</span></span>
<span data-ttu-id="1752c-188">První soubor schopnosti role najít odpovídající požadovaný název se použije pro připojování uživatele.</span><span class="sxs-lookup"><span data-stu-id="1752c-188">The first role capability file found that matches the desired name will be used for the connecting user.</span></span>

<span data-ttu-id="1752c-189">Pořadí hledání schopnosti role není deterministický, pokud dvě nebo více možností role sdílejí stejný název, a proto je **důrazně doporučujeme** zkontrolujte možnosti role na počítači máte jedinečné názvy.</span><span class="sxs-lookup"><span data-stu-id="1752c-189">Since the role capability search order is not deterministic when two or more role capabilities share the same name, it is **strongly recommended** that you ensure role capabilities have unique names on your machine.</span></span>

### <a name="conditional-access-rules"></a><span data-ttu-id="1752c-190">Pravidla podmíněného přístupu</span><span class="sxs-lookup"><span data-stu-id="1752c-190">Conditional access rules</span></span>

<span data-ttu-id="1752c-191">Všichni uživatelé a skupiny součástí RoleDefinitions pole jsou automaticky udělen přístup k JEA koncové body.</span><span class="sxs-lookup"><span data-stu-id="1752c-191">All users and groups included in the RoleDefinitions field are automatically granted access to JEA endpoints.</span></span>
<span data-ttu-id="1752c-192">Pravidla podmíněného přístupu umožňují upřesnit tento přístup a vyžaduje, aby uživatel patří do skupiny další zabezpečení, které nemají vliv rolí, které jsou přiřazeny.</span><span class="sxs-lookup"><span data-stu-id="1752c-192">Conditional access rules allow you to refine this access and require users to belong to additional security groups which do not impact the roles which they are assigned.</span></span>
<span data-ttu-id="1752c-193">To může být užitečné, pokud chcete integrovat "jenom v čase" privilegovaný přístup k řešení pro správu, ověřování pomocí čipové karty nebo jiného řešení vícefaktorového ověřování s JEA.</span><span class="sxs-lookup"><span data-stu-id="1752c-193">This can be useful if you want to integrate a "just in time" privileged access management solution, smartcard authentication, or other multifactor authentication solution with JEA.</span></span>

<span data-ttu-id="1752c-194">Pravidla podmíněného přístupu jsou definovány v poli RequiredGroups v konfiguračním souboru relace.</span><span class="sxs-lookup"><span data-stu-id="1752c-194">Conditional access rules are defined in the RequiredGroups field in a session configuration file.</span></span>
<span data-ttu-id="1752c-195">Zde můžete zadat zatřiďovací tabulku (volitelně vnořená) používající 'A' a 'Nebo' klíčů můžete vytvořit vaše pravidla.</span><span class="sxs-lookup"><span data-stu-id="1752c-195">There, you can provide a hashtable (optionally nested) that uses 'And' and 'Or' keys to construct your rules.</span></span>
<span data-ttu-id="1752c-196">Tady jsou některé příklady, jak využít toto pole:</span><span class="sxs-lookup"><span data-stu-id="1752c-196">Here are some examples of how to leverage this field:</span></span>

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
> <span data-ttu-id="1752c-197">Pravidla podmíněného přístupu jsou pouze k dispozici v systému Windows PowerShell 5.1 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="1752c-197">Conditional access rules are only available in Windows PowerShell 5.1 or newer.</span></span>

### <a name="other-properties"></a><span data-ttu-id="1752c-198">Ostatní vlastnosti</span><span class="sxs-lookup"><span data-stu-id="1752c-198">Other properties</span></span>
<span data-ttu-id="1752c-199">Relace konfigurační soubory můžete také provést vše, co soubor schopnosti role mohou provádět pouze bez možnosti připojování uživatelům poskytnout přístup k jiné příkazy.</span><span class="sxs-lookup"><span data-stu-id="1752c-199">Session configuration files can also do everything a role capability file can do, just without the ability to give connecting users access to different commands.</span></span>
<span data-ttu-id="1752c-200">Pokud chcete povolit všem uživatelům přístup ke konkrétní rutiny, funkce nebo poskytovatelů, můžete tak učinit přímo do konfiguračního souboru relace.</span><span class="sxs-lookup"><span data-stu-id="1752c-200">If you want to allow all users access to specific cmdlets, functions, or providers, you can do so right in the session configuration file.</span></span>
<span data-ttu-id="1752c-201">Úplný seznam podporovaných vlastností v souboru konfigurace relace, spustit `Get-Help New-PSSessionConfigurationFile -Full`.</span><span class="sxs-lookup"><span data-stu-id="1752c-201">For a full list of supported properties in the session configuration file, run `Get-Help New-PSSessionConfigurationFile -Full`.</span></span>

## <a name="testing-a-session-configuration-file"></a><span data-ttu-id="1752c-202">Testování relace konfiguračního souboru</span><span class="sxs-lookup"><span data-stu-id="1752c-202">Testing a session configuration file</span></span>

<span data-ttu-id="1752c-203">Můžete otestovat pomocí konfigurace relace [Test PSSessionConfigurationFile](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) rutiny.</span><span class="sxs-lookup"><span data-stu-id="1752c-203">You can test a session configuration using the [Test-PSSessionConfigurationFile](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) cmdlet.</span></span>
<span data-ttu-id="1752c-204">Důrazně doporučujeme, abyste otestovali konfiguračního souboru relace, pokud jste upravili soubor pssc ručně pomocí textového editoru zajistit správnost syntaxe.</span><span class="sxs-lookup"><span data-stu-id="1752c-204">It is strongly recommended that you test your session configuration file if you have edited the pssc file manually using a text editor to ensure the syntax is correct.</span></span>
<span data-ttu-id="1752c-205">Pokud tento test neproběhne úspěšně relace konfigurační soubor, nebude moct se úspěšně zaregistroval v systému.</span><span class="sxs-lookup"><span data-stu-id="1752c-205">If a session configuration file does not pass this test, it will not be able to be successfully registered on the system.</span></span>

## <a name="sample-session-configuration-file"></a><span data-ttu-id="1752c-206">Ukázkový soubor konfigurace relace</span><span class="sxs-lookup"><span data-stu-id="1752c-206">Sample session configuration file</span></span>

<span data-ttu-id="1752c-207">Níže je úplný příklad znázorňující způsob vytvoření a ověření konfigurace relace pro JEA.</span><span class="sxs-lookup"><span data-stu-id="1752c-207">Below is a complete example showing how to create and validate a session configuration for JEA.</span></span>
<span data-ttu-id="1752c-208">Všimněte si, že jsou definice rolí vytvoří a uloží do `$roles` proměnná pro usnadnění práce a přehlednosti.</span><span class="sxs-lookup"><span data-stu-id="1752c-208">Note that the role definitions are created and stored in the `$roles` variable for convenience and readability.</span></span>
<span data-ttu-id="1752c-209">Není potřeba udělat.</span><span class="sxs-lookup"><span data-stu-id="1752c-209">It is not a requirement to do so.</span></span>

```powershell
$roles = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}

New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\JEAConfig.pssc -RunAsVirtualAccount -TranscriptDirectory 'C:\ProgramData\JEAConfiguration\Transcripts' -RoleDefinitions $roles -RequiredGroups @{ Or = '2FA-logon', 'smartcard-logon' }
Test-PSSessionConfigurationFile -Path .\JEAConfig.pssc # should yield True
```

## <a name="updating-session-configuration-files"></a><span data-ttu-id="1752c-210">Aktualizace relace konfigurační soubory</span><span class="sxs-lookup"><span data-stu-id="1752c-210">Updating session configuration files</span></span>

<span data-ttu-id="1752c-211">Pokud potřebujete změnit vlastnosti konfigurace relace JEA, včetně mapování uživatelů na role, je nutné [zrušit registraci](register-jea.md#unregistering-jea-configurations) a [znovu zaregistrovat](register-jea.md) JEA konfigurace relace.</span><span class="sxs-lookup"><span data-stu-id="1752c-211">If you need to change properties of a JEA session configuration, including the mapping of users to roles, you must [unregister](register-jea.md#unregistering-jea-configurations) and [re-register](register-jea.md) the JEA session configuration.</span></span>
<span data-ttu-id="1752c-212">Při registraci znovu JEA konfigurace relace, použijte aktualizované prostředí PowerShell relace konfigurační soubor, který obsahuje požadované změny.</span><span class="sxs-lookup"><span data-stu-id="1752c-212">When you re-register the JEA session configuration, use an updated PowerShell session configuration file that includes your desired changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1752c-213">Další kroky</span><span class="sxs-lookup"><span data-stu-id="1752c-213">Next steps</span></span>

- [<span data-ttu-id="1752c-214">Zaregistruje konfiguraci JEA</span><span class="sxs-lookup"><span data-stu-id="1752c-214">Register a JEA configuration</span></span>](register-jea.md)
- [<span data-ttu-id="1752c-215">Autor JEA role</span><span class="sxs-lookup"><span data-stu-id="1752c-215">Author JEA roles</span></span>](role-capabilities.md)