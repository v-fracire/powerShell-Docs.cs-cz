---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Začínáme s Desired State Configuration (DSC) pro Linux
ms.openlocfilehash: d5a4a17fbcffbbbd6df3dd902dbd104769b7d17e
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893592"
---
# <a name="get-started-with-desired-state-configuration-dsc-for-linux"></a><span data-ttu-id="b8a72-103">Začínáme s Desired State Configuration (DSC) pro Linux</span><span class="sxs-lookup"><span data-stu-id="b8a72-103">Get started with Desired State Configuration (DSC) for Linux</span></span>

<span data-ttu-id="b8a72-104">Toto téma vysvětluje, jak začít používat prostředí PowerShell Desired State Configuration (DSC) pro Linux.</span><span class="sxs-lookup"><span data-stu-id="b8a72-104">This topic explains how to get started using PowerShell Desired State Configuration (DSC) for Linux.</span></span> <span data-ttu-id="b8a72-105">Obecné informace o DSC najdete v tématu [začít pracovat s Windows PowerShell Desired State Configuration](overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8a72-105">For general information about DSC, see [Get Started with Windows PowerShell Desired State Configuration](overview.md).</span></span>

## <a name="supported-linux-operation-system-versions"></a><span data-ttu-id="b8a72-106">Podporované verze systému Linux operace</span><span class="sxs-lookup"><span data-stu-id="b8a72-106">Supported Linux operation system versions</span></span>

<span data-ttu-id="b8a72-107">Tyto verze operačních systémů Linux jsou podporovány pro DSC pro Linux.</span><span class="sxs-lookup"><span data-stu-id="b8a72-107">The following Linux operating system versions are supported for DSC for Linux.</span></span>

- <span data-ttu-id="b8a72-108">CentOS 5, 6 a 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b8a72-108">CentOS 5, 6, and 7 (x86/x64)</span></span>
- <span data-ttu-id="b8a72-109">Debian GNU/Linux 6, 7 a 8 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b8a72-109">Debian GNU/Linux 6, 7 and 8 (x86/x64)</span></span>
- <span data-ttu-id="b8a72-110">Oracle Linux 5, 6 a 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b8a72-110">Oracle Linux 5, 6 and 7 (x86/x64)</span></span>
- <span data-ttu-id="b8a72-111">Red Hat Enterprise Linux Server 5, 6 a 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b8a72-111">Red Hat Enterprise Linux Server 5, 6 and 7 (x86/x64)</span></span>
- <span data-ttu-id="b8a72-112">SUSE Linux Enterprise Server 10, 11 a 12 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b8a72-112">SUSE Linux Enterprise Server 10, 11 and 12 (x86/x64)</span></span>
- <span data-ttu-id="b8a72-113">Server se systémem Ubuntu 12.04 LTS, 14.04 LTS a 16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="b8a72-113">Ubuntu Server 12.04 LTS, 14.04 LTS and 16.04 LTS (x86/x64)</span></span>

<span data-ttu-id="b8a72-114">Následující tabulka popisuje závislosti požadovaný balíček pro DSC pro Linux.</span><span class="sxs-lookup"><span data-stu-id="b8a72-114">The following table describes the required package dependencies for DSC for Linux.</span></span>

|  <span data-ttu-id="b8a72-115">Požadovaný balíček</span><span class="sxs-lookup"><span data-stu-id="b8a72-115">Required package</span></span> |  <span data-ttu-id="b8a72-116">Popis</span><span class="sxs-lookup"><span data-stu-id="b8a72-116">Description</span></span> |  <span data-ttu-id="b8a72-117">Minimální verze</span><span class="sxs-lookup"><span data-stu-id="b8a72-117">Minimum version</span></span> |
|---|---|---|
| <span data-ttu-id="b8a72-118">knihovnou glibc</span><span class="sxs-lookup"><span data-stu-id="b8a72-118">glibc</span></span>| <span data-ttu-id="b8a72-119">Knihovna GNU.</span><span class="sxs-lookup"><span data-stu-id="b8a72-119">GNU Library</span></span>| <span data-ttu-id="b8a72-120">2... 4 – 31.30</span><span class="sxs-lookup"><span data-stu-id="b8a72-120">2…4 – 31.30</span></span>|
| <span data-ttu-id="b8a72-121">Python</span><span class="sxs-lookup"><span data-stu-id="b8a72-121">python</span></span>| <span data-ttu-id="b8a72-122">Python</span><span class="sxs-lookup"><span data-stu-id="b8a72-122">Python</span></span>| <span data-ttu-id="b8a72-123">2.4 – 3.4</span><span class="sxs-lookup"><span data-stu-id="b8a72-123">2.4 – 3.4</span></span>|
| <span data-ttu-id="b8a72-124">omiserver</span><span class="sxs-lookup"><span data-stu-id="b8a72-124">omiserver</span></span>| <span data-ttu-id="b8a72-125">Infrastruktura OMI (Open Management Infrastructure)</span><span class="sxs-lookup"><span data-stu-id="b8a72-125">Open Management Infrastructure</span></span>| <span data-ttu-id="b8a72-126">1.0.8.1</span><span class="sxs-lookup"><span data-stu-id="b8a72-126">1.0.8.1</span></span>|
| <span data-ttu-id="b8a72-127">OpenSSL</span><span class="sxs-lookup"><span data-stu-id="b8a72-127">openssl</span></span>| <span data-ttu-id="b8a72-128">Knihovny OpenSSL</span><span class="sxs-lookup"><span data-stu-id="b8a72-128">OpenSSL Libraries</span></span>| <span data-ttu-id="b8a72-129">0.9.8 nebo 1.0</span><span class="sxs-lookup"><span data-stu-id="b8a72-129">0.9.8 or 1.0</span></span>|
| <span data-ttu-id="b8a72-130">ctypes</span><span class="sxs-lookup"><span data-stu-id="b8a72-130">ctypes</span></span>| <span data-ttu-id="b8a72-131">Knihovna Python CTypes</span><span class="sxs-lookup"><span data-stu-id="b8a72-131">Python CTypes library</span></span>| <span data-ttu-id="b8a72-132">Musí odpovídat verzi Pythonu</span><span class="sxs-lookup"><span data-stu-id="b8a72-132">Must match Python version</span></span>|
| <span data-ttu-id="b8a72-133">libcurl</span><span class="sxs-lookup"><span data-stu-id="b8a72-133">libcurl</span></span>| <span data-ttu-id="b8a72-134">knihovny klienta http cURL</span><span class="sxs-lookup"><span data-stu-id="b8a72-134">cURL http client library</span></span>| <span data-ttu-id="b8a72-135">7.15.1</span><span class="sxs-lookup"><span data-stu-id="b8a72-135">7.15.1</span></span>|

## <a name="installing-dsc-for-linux"></a><span data-ttu-id="b8a72-136">Instalace DSC pro Linux</span><span class="sxs-lookup"><span data-stu-id="b8a72-136">Installing DSC for Linux</span></span>

<span data-ttu-id="b8a72-137">Je nutné nainstalovat [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) před instalací DSC pro Linux.</span><span class="sxs-lookup"><span data-stu-id="b8a72-137">You must install the [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) before installing DSC for Linux.</span></span>

### <a name="installing-omi"></a><span data-ttu-id="b8a72-138">Instalace infrastruktury OMI</span><span class="sxs-lookup"><span data-stu-id="b8a72-138">Installing OMI</span></span>

<span data-ttu-id="b8a72-139">Desired State Configuration pro Linux vyžaduje server CIM Open Management Infrastructure (OMI), verze 1.0.8.1 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="b8a72-139">Desired State Configuration for Linux requires the Open Management Infrastructure (OMI) CIM server, version 1.0.8.1 or later.</span></span> <span data-ttu-id="b8a72-140">OMI je možné stáhnout z The Open Group: [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi).</span><span class="sxs-lookup"><span data-stu-id="b8a72-140">OMI can be downloaded from The Open Group: [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi).</span></span>

<span data-ttu-id="b8a72-141">Instalace infrastruktury OMI, nainstalujte balíček, který je vhodný pro systém Linux (.rpm nebo .deb) a verze OpenSSL (ssl_098 nebo ssl_100) a architektura (x64/x86).</span><span class="sxs-lookup"><span data-stu-id="b8a72-141">To install OMI, install the package that is appropriate for your Linux system (.rpm or .deb) and OpenSSL version (ssl_098 or ssl_100), and architecture (x64/x86).</span></span> <span data-ttu-id="b8a72-142">Ot. / min balíčky jsou vhodné pro CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server a Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="b8a72-142">RPM packages are appropriate for CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, and Oracle Linux.</span></span> <span data-ttu-id="b8a72-143">DEB balíčky jsou vhodné pro Debian GNU/Linux a Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="b8a72-143">DEB packages are appropriate for Debian GNU/Linux and Ubuntu Server.</span></span> <span data-ttu-id="b8a72-144">Ssl_098 balíčky jsou vhodné pro počítače s OpenSSL 0.9.8 nainstalovali při ssl_100 balíčky jsou vhodné pro počítače s OpenSSL 1.0 nainstalované.</span><span class="sxs-lookup"><span data-stu-id="b8a72-144">The ssl_098 packages are appropriate for computers with OpenSSL 0.9.8 installed while the ssl_100 packages are appropriate for computers with OpenSSL 1.0 installed.</span></span>

> [!NOTE]
> <span data-ttu-id="b8a72-145">Pokud chcete zjistit nainstalovanou verzi OpenSSL, spusťte příkaz `openssl version`.</span><span class="sxs-lookup"><span data-stu-id="b8a72-145">To determine the installed OpenSSL version, run the command `openssl version`.</span></span>

<span data-ttu-id="b8a72-146">Spusťte následující příkaz k instalaci v systému CentOS 7 x64 OMI.</span><span class="sxs-lookup"><span data-stu-id="b8a72-146">Run the following command to install OMI on a CentOS 7 x64 system.</span></span>

`# sudo rpm -Uvh omiserver-1.0.8.ssl_100.rpm`

### <a name="installing-dsc"></a><span data-ttu-id="b8a72-147">Instalaci DSC</span><span class="sxs-lookup"><span data-stu-id="b8a72-147">Installing DSC</span></span>

<span data-ttu-id="b8a72-148">DSC pro Linux je k dispozici ke stažení [tady](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/tag/v1.1.1-294).</span><span class="sxs-lookup"><span data-stu-id="b8a72-148">DSC for Linux is available for download [here](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/tag/v1.1.1-294).</span></span>

<span data-ttu-id="b8a72-149">K instalaci DSC, nainstalujte balíček, který je vhodný pro systém Linux (.rpm nebo .deb) a verze OpenSSL (ssl_098 nebo ssl_100) a architektura (x64/x86).</span><span class="sxs-lookup"><span data-stu-id="b8a72-149">To install DSC, install the package that is appropriate for your Linux system (.rpm or .deb) and OpenSSL version (ssl_098 or ssl_100), and architecture (x64/x86).</span></span> <span data-ttu-id="b8a72-150">Ot. / min balíčky jsou vhodné pro CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server a Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="b8a72-150">RPM packages are appropriate for CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, and Oracle Linux.</span></span> <span data-ttu-id="b8a72-151">DEB balíčky jsou vhodné pro Debian GNU/Linux a Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="b8a72-151">DEB packages are appropriate for Debian GNU/Linux and Ubuntu Server.</span></span> <span data-ttu-id="b8a72-152">Ssl_098 balíčky jsou vhodné pro počítače s OpenSSL 0.9.8 nainstalovali při ssl_100 balíčky jsou vhodné pro počítače s OpenSSL 1.0 nainstalované.</span><span class="sxs-lookup"><span data-stu-id="b8a72-152">The ssl_098 packages are appropriate for computers with OpenSSL 0.9.8 installed while the ssl_100 packages are appropriate for computers with OpenSSL 1.0 installed.</span></span>

> [!NOTE]
> <span data-ttu-id="b8a72-153">K určení Instalovatelné verze OpenSSL, spusťte příkaz verze openssl.</span><span class="sxs-lookup"><span data-stu-id="b8a72-153">To determine the installed OpenSSL version, run the command openssl version.</span></span>

<span data-ttu-id="b8a72-154">Spusťte následující příkaz k instalaci v systému CentOS 7 x64 DSC.</span><span class="sxs-lookup"><span data-stu-id="b8a72-154">Run the following command to install DSC on a CentOS 7 x64 system.</span></span>

`# sudo rpm -Uvh dsc-1.0.0-254.ssl_100.x64.rpm`

## <a name="using-dsc-for-linux"></a><span data-ttu-id="b8a72-155">Pomocí DSC pro Linux</span><span class="sxs-lookup"><span data-stu-id="b8a72-155">Using DSC for Linux</span></span>

<span data-ttu-id="b8a72-156">Následující části popisují, jak vytvářet a spouštět konfigurací DSC na počítače s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="b8a72-156">The following sections explain how to create and run DSC configurations on Linux computers.</span></span>

### <a name="creating-a-configuration-mof-document"></a><span data-ttu-id="b8a72-157">Vytvoření dokumentu MOF konfigurace</span><span class="sxs-lookup"><span data-stu-id="b8a72-157">Creating a configuration MOF document</span></span>

<span data-ttu-id="b8a72-158">Konfigurace Windows Powershellu – klíčové slovo se používá pro vytvoření konfigurace pro počítače s Linuxem, stejně jako u počítačů s Windows.</span><span class="sxs-lookup"><span data-stu-id="b8a72-158">The Windows PowerShell Configuration keyword is used to create a configuration for Linux computers, just like for Windows computers.</span></span> <span data-ttu-id="b8a72-159">Následující kroky popisují vytvoření dokumentu konfigurace pro počítač s Linuxem pomocí Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="b8a72-159">The following steps describe the creation of a configuration document for a Linux computer using Windows PowerShell.</span></span>

1. <span data-ttu-id="b8a72-160">Naimportujte modul nx.</span><span class="sxs-lookup"><span data-stu-id="b8a72-160">Import the nx module.</span></span> <span data-ttu-id="b8a72-161">Modul prostředí Windows PowerShell nx obsahuje schéma pro integrované prostředky pro DSC pro Linux a musí být nainstalované na místním počítači a importu v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="b8a72-161">The nx Windows PowerShell module contains the schema for Built-In resources for DSC for Linux, and must be installed to your local computer and imported in the configuration.</span></span>

   - <span data-ttu-id="b8a72-162">Pokud chcete nainstalovat modul nx, zkopírujte adresář modulu nx buď `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` nebo `$PSHOME\Modules`.</span><span class="sxs-lookup"><span data-stu-id="b8a72-162">To install the nx module, copy the nx module directory to either `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` or `$PSHOME\Modules`.</span></span> <span data-ttu-id="b8a72-163">DSC pro Linux instalační balíček (MSI) je součástí modulu nx.</span><span class="sxs-lookup"><span data-stu-id="b8a72-163">The nx module is included in the DSC for Linux installation package (MSI).</span></span> <span data-ttu-id="b8a72-164">Chcete-li importovat modul nx v konfiguraci, použijte `Import-DSCResource` příkaz:</span><span class="sxs-lookup"><span data-stu-id="b8a72-164">To import the nx module in your configuration, use the `Import-DSCResource` command:</span></span>

   ```powershell
   Configuration ExampleConfiguration{

    Import-DSCResource -Module nx

   }
   ```

2. <span data-ttu-id="b8a72-165">Definice konfigurace a generovat dokument konfigurace:</span><span class="sxs-lookup"><span data-stu-id="b8a72-165">Define a configuration and generate the configuration document:</span></span>

   ```powershell
   Configuration ExampleConfiguration
   {
        Import-DscResource -Module nx

        Node  "linuxhost.contoso.com"
        {
            nxFile ExampleFile 
            {
                DestinationPath = "/tmp/example"
                Contents = "hello world `n"
                Ensure = "Present"
                Type = "File"
            }
        }
   }

   ExampleConfiguration -OutputPath:"C:\temp"
   ```

### <a name="push-the-configuration-to-the-linux-computer"></a><span data-ttu-id="b8a72-166">Push v konfiguraci pro počítače s Linuxem</span><span class="sxs-lookup"><span data-stu-id="b8a72-166">Push the configuration to the Linux computer</span></span>

<span data-ttu-id="b8a72-167">Konfigurace dokumentů (soubory MOF) je možné nabídnout pro Linux pomocí počítače [Start-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Start-DscConfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="b8a72-167">Configuration documents (MOF files) can be pushed to the Linux computer using the [Start-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Start-DscConfiguration) cmdlet.</span></span> <span data-ttu-id="b8a72-168">Chcete-li použít tuto rutinu spolu s [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration), nebo [Test-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Test-DscConfiguration) rutiny, vzdáleně k počítači s Linuxem, je nutné použít CIMSession.</span><span class="sxs-lookup"><span data-stu-id="b8a72-168">In order to use this cmdlet, along with the [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration), or [Test-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Test-DscConfiguration) cmdlets, remotely to a Linux computer, you must use a CIMSession.</span></span> <span data-ttu-id="b8a72-169">[New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) rutina se používá k vytvoření CIMSession do počítače s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="b8a72-169">The [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) cmdlet is used to create a CIMSession to the Linux computer.</span></span>

<span data-ttu-id="b8a72-170">Následující kód ukazuje, jak vytvořit CIMSession DSC pro Linux.</span><span class="sxs-lookup"><span data-stu-id="b8a72-170">The following code shows how to create a CIMSession for DSC for Linux.</span></span>

```powershell
$Node = "ostc-dsc-01"
$Credential = Get-Credential -UserName:"root" -Message:"Enter Password:"

#Ignore SSL certificate validation
#$opt = New-CimSessionOption -UseSsl:$true -SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true

#Options for a trusted SSL certificate
$opt = New-CimSessionOption -UseSsl:$true
$Sess=New-CimSession -Credential:$credential -ComputerName:$Node -Port:5986 -Authentication:basic -SessionOption:$opt -OperationTimeoutSec:90
```

> [!NOTE]
> <span data-ttu-id="b8a72-171">Pro režim "Push" musí být přihlašovací údaje uživatele kořenového uživatele na počítači s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="b8a72-171">For “Push” mode, the user credential must be the root user on the Linux computer.</span></span>
> <span data-ttu-id="b8a72-172">Pro DSC pro Linux, jsou podporovány pouze připojení SSL/TLS `New-CimSession` musí použít s parametrem – UseSSL nastaveným na $true.</span><span class="sxs-lookup"><span data-stu-id="b8a72-172">Only SSL/TLS connections are supported for DSC for Linux, the `New-CimSession` must be used with the –UseSSL parameter set to $true.</span></span>
> <span data-ttu-id="b8a72-173">Certifikát SSL používaný OMI (DSC) je zadán v souboru: `/opt/omi/etc/omiserver.conf` s vlastnostmi: pemfile a keyfile.</span><span class="sxs-lookup"><span data-stu-id="b8a72-173">The SSL certificate used by OMI (for DSC) is specified in the file: `/opt/omi/etc/omiserver.conf` with the properties: pemfile and keyfile.</span></span>
> <span data-ttu-id="b8a72-174">Pokud tento certifikát není důvěryhodný počítač Windows, kterou používáte [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) na rutinu, můžete přeskočit ověření certifikátu s parametry CIMSession: `-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`</span><span class="sxs-lookup"><span data-stu-id="b8a72-174">If this certificate is not trusted by the Windows computer that you are running the [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) cmdlet on, you can choose to ignore certificate validation with the CIMSession Options: `-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`</span></span>

<span data-ttu-id="b8a72-175">Spusťte následující příkaz tak, aby nabízel konfigurace DSC k uzlu systému Linux.</span><span class="sxs-lookup"><span data-stu-id="b8a72-175">Run the following command to push the DSC configuration to the Linux node.</span></span>

`Start-DscConfiguration -Path:"C:\temp" -CimSession:$Sess -Wait -Verbose`

### <a name="distribute-the-configuration-with-a-pull-server"></a><span data-ttu-id="b8a72-176">Distribuce konfigurace serveru vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="b8a72-176">Distribute the configuration with a pull server</span></span>

<span data-ttu-id="b8a72-177">Konfigurace lze distribuovat na počítači s Linuxem pomocí serveru vyžádané replikace, stejně jako u počítačů s Windows.</span><span class="sxs-lookup"><span data-stu-id="b8a72-177">Configurations can be distributed to a Linux computer with a pull server, just like for Windows computers.</span></span> <span data-ttu-id="b8a72-178">Pokyny k používání serveru vyžádané replikace najdete v tématu [Windows PowerShell Desired State Configuration o přijetí změn servery](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="b8a72-178">For guidance on using a pull server, see [Windows PowerShell Desired State Configuration Pull Servers](pullServer.md).</span></span> <span data-ttu-id="b8a72-179">Další informace a omezení týkající se počítače s Linuxem pomocí serveru vyžádané replikace najdete v tématu poznámky k verzi pro Desired State Configuration pro Linux.</span><span class="sxs-lookup"><span data-stu-id="b8a72-179">For additional information and limitations related to using Linux computers with a pull server, see the Release Notes for Desired State Configuration for Linux.</span></span>

### <a name="working-with-configurations-locally"></a><span data-ttu-id="b8a72-180">Práce s konfigurací místně</span><span class="sxs-lookup"><span data-stu-id="b8a72-180">Working with configurations locally</span></span>

<span data-ttu-id="b8a72-181">DSC pro Linux zahrnuje skriptů pro práci s konfigurací z místního počítače s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="b8a72-181">DSC for Linux includes scripts to work with configuration from the local Linux computer.</span></span> <span data-ttu-id="b8a72-182">Tyto skripty jsou vyhledejte v `/opt/microsoft/dsc/Scripts` a zahrnují následující:</span><span class="sxs-lookup"><span data-stu-id="b8a72-182">These scripts are locate in `/opt/microsoft/dsc/Scripts` and include the following:</span></span>

- <span data-ttu-id="b8a72-183">GetDscConfiguration.py</span><span class="sxs-lookup"><span data-stu-id="b8a72-183">GetDscConfiguration.py</span></span>

<span data-ttu-id="b8a72-184">Vrátí aktuální konfiguraci použita na počítač.</span><span class="sxs-lookup"><span data-stu-id="b8a72-184">Returns the current configuration applied to the computer.</span></span> <span data-ttu-id="b8a72-185">Podobně jako rutiny Windows Powershellu `Get-DscConfiguration` rutiny.</span><span class="sxs-lookup"><span data-stu-id="b8a72-185">Similar to the Windows PowerShell cmdlet `Get-DscConfiguration` cmdlet.</span></span>

`# sudo ./GetDscConfiguration.py`

- <span data-ttu-id="b8a72-186">GetDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="b8a72-186">GetDscLocalConfigurationManager.py</span></span>

<span data-ttu-id="b8a72-187">Vrátí aktuální meta konfigurace použita na počítač.</span><span class="sxs-lookup"><span data-stu-id="b8a72-187">Returns the current meta-configuration applied to the computer.</span></span> <span data-ttu-id="b8a72-188">Podobně jako rutiny [Get-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) rutiny.</span><span class="sxs-lookup"><span data-stu-id="b8a72-188">Similar to the cmdlet [Get-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) cmdlet.</span></span>

`# sudo ./GetDscLocalConfigurationManager.py`

- <span data-ttu-id="b8a72-189">InstallModule.py</span><span class="sxs-lookup"><span data-stu-id="b8a72-189">InstallModule.py</span></span>

<span data-ttu-id="b8a72-190">Nainstaluje vlastní modul zdroje DSC.</span><span class="sxs-lookup"><span data-stu-id="b8a72-190">Installs a custom DSC resource module.</span></span> <span data-ttu-id="b8a72-191">Vyžaduje se cesta k souboru ZIP obsahující modul sdíleného objektu knihovny a soubory MOF schématu.</span><span class="sxs-lookup"><span data-stu-id="b8a72-191">Requires the path to a .zip file containing the module shared object library and schema MOF files.</span></span>

`# sudo ./InstallModule.py /tmp/cnx_Resource.zip`

- <span data-ttu-id="b8a72-192">RemoveModule.py</span><span class="sxs-lookup"><span data-stu-id="b8a72-192">RemoveModule.py</span></span>

<span data-ttu-id="b8a72-193">Odebere vlastního modulu prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="b8a72-193">Removes a custom DSC resource module.</span></span> <span data-ttu-id="b8a72-194">Vyžaduje název modulu, který chcete odebrat.</span><span class="sxs-lookup"><span data-stu-id="b8a72-194">Requires the name of the module to remove.</span></span>

`# sudo ./RemoveModule.py cnx_Resource`

- <span data-ttu-id="b8a72-195">StartDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="b8a72-195">StartDscLocalConfigurationManager.py</span></span>

<span data-ttu-id="b8a72-196">Konfiguračního souboru MOF se vztahuje na počítač.</span><span class="sxs-lookup"><span data-stu-id="b8a72-196">Applies a configuration MOF file to the computer.</span></span> <span data-ttu-id="b8a72-197">Podobně jako [Start-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Start-DscConfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="b8a72-197">Similar to the [Start-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Start-DscConfiguration) cmdlet.</span></span> <span data-ttu-id="b8a72-198">Vyžaduje cesta ke konfiguraci MOF, který chcete použít.</span><span class="sxs-lookup"><span data-stu-id="b8a72-198">Requires the path to the configuration MOF to apply.</span></span>

`# sudo ./StartDscLocalConfigurationManager.py –configurationmof /tmp/localhost.mof`

- <span data-ttu-id="b8a72-199">SetDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="b8a72-199">SetDscLocalConfigurationManager.py</span></span>

<span data-ttu-id="b8a72-200">Soubor MOF Meta konfigurace se vztahuje na počítač.</span><span class="sxs-lookup"><span data-stu-id="b8a72-200">Applies a Meta Configuration MOF file to the computer.</span></span> <span data-ttu-id="b8a72-201">Podobně jako [Set-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) rutiny.</span><span class="sxs-lookup"><span data-stu-id="b8a72-201">Similar to the [Set-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) cmdlet.</span></span> <span data-ttu-id="b8a72-202">Vyžaduje cesta ke konfiguraci MOF Meta použít.</span><span class="sxs-lookup"><span data-stu-id="b8a72-202">Requires the path to the Meta Configuration MOF to apply.</span></span>

`# sudo ./SetDscLocalConfigurationManager.py –configurationmof /tmp/localhost.meta.mof`

## <a name="powershell-desired-state-configuration-for-linux-log-files"></a><span data-ttu-id="b8a72-203">Prostředí PowerShell Desired State Configuration pro soubory protokolů systému Linux</span><span class="sxs-lookup"><span data-stu-id="b8a72-203">PowerShell Desired State Configuration for Linux Log Files</span></span>

<span data-ttu-id="b8a72-204">Následující soubory protokolu jsou generovány pro DSC pro Linux zprávy.</span><span class="sxs-lookup"><span data-stu-id="b8a72-204">The following log files are generated for DSC for Linux messages.</span></span>

|<span data-ttu-id="b8a72-205">Soubor protokolu</span><span class="sxs-lookup"><span data-stu-id="b8a72-205">Log file</span></span>|<span data-ttu-id="b8a72-206">Adresář</span><span class="sxs-lookup"><span data-stu-id="b8a72-206">Directory</span></span>|<span data-ttu-id="b8a72-207">Popis</span><span class="sxs-lookup"><span data-stu-id="b8a72-207">Description</span></span>|
|---|---|---|
|<span data-ttu-id="b8a72-208">**omiserver.log**</span><span class="sxs-lookup"><span data-stu-id="b8a72-208">**omiserver.log**</span></span>|`/var/opt/omi/log`|<span data-ttu-id="b8a72-209">Zprávy týkající se fungování server OMI CIM.</span><span class="sxs-lookup"><span data-stu-id="b8a72-209">Messages relating to the operation of the OMI CIM server.</span></span>|
|<span data-ttu-id="b8a72-210">**DSC.log**</span><span class="sxs-lookup"><span data-stu-id="b8a72-210">**dsc.log**</span></span>|`/var/opt/omi/log`|<span data-ttu-id="b8a72-211">Zprávy týkající se fungování operace prostředků místní Configuration Manageru (LCM) a DSC.</span><span class="sxs-lookup"><span data-stu-id="b8a72-211">Messages relating to the operation of the Local Configuration Manager (LCM) and DSC resource operations.</span></span>|