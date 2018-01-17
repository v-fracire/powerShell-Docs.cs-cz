---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Začínáme s potřeby konfigurace stavu (DSC) pro Linux"
ms.openlocfilehash: 4fd8460bc5d2564cab291904b60a1a0c26c3e5a7
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="get-started-with-desired-state-configuration-dsc-for-linux"></a><span data-ttu-id="15b1d-103">Začínáme s potřeby konfigurace stavu (DSC) pro Linux</span><span class="sxs-lookup"><span data-stu-id="15b1d-103">Get started with Desired State Configuration (DSC) for Linux</span></span>

<span data-ttu-id="15b1d-104">Toto téma vysvětluje, jak začít používat prostředí PowerShell požadovaného stavu konfigurace (DSC) pro Linux.</span><span class="sxs-lookup"><span data-stu-id="15b1d-104">This topic explains how to get started using PowerShell Desired State Configuration (DSC) for Linux.</span></span> <span data-ttu-id="15b1d-105">Obecné informace o DSC najdete v tématu [začít pracovat s konfigurace požadovaného stavu aplikace Windows PowerShell](overview.md).</span><span class="sxs-lookup"><span data-stu-id="15b1d-105">For general information about DSC, see [Get Started with Windows PowerShell Desired State Configuration](overview.md).</span></span>

## <a name="supported-linux-operation-system-versions"></a><span data-ttu-id="15b1d-106">Podporované verze systému Linux operace</span><span class="sxs-lookup"><span data-stu-id="15b1d-106">Supported Linux operation system versions</span></span>

<span data-ttu-id="15b1d-107">Následující verze operačního systému Linux jsou podporovány pro DSC pro Linux.</span><span class="sxs-lookup"><span data-stu-id="15b1d-107">The following Linux operating system versions are supported for DSC for Linux.</span></span>
- <span data-ttu-id="15b1d-108">CentOS 5, 6 a 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="15b1d-108">CentOS 5, 6, and 7 (x86/x64)</span></span>
- <span data-ttu-id="15b1d-109">Debian GNU/Linux 6, 7 a 8 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="15b1d-109">Debian GNU/Linux 6, 7 and 8 (x86/x64)</span></span>
- <span data-ttu-id="15b1d-110">Oracle Linux 5, 6 a 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="15b1d-110">Oracle Linux 5, 6 and 7 (x86/x64)</span></span>
- <span data-ttu-id="15b1d-111">Red Hat Enterprise Linux Server 5, 6 a 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="15b1d-111">Red Hat Enterprise Linux Server 5, 6 and 7 (x86/x64)</span></span>
- <span data-ttu-id="15b1d-112">SUSE Linux Enterprise Server 10, 11 a 12 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="15b1d-112">SUSE Linux Enterprise Server 10, 11 and 12 (x86/x64)</span></span>
- <span data-ttu-id="15b1d-113">Ubuntu Server 12.04 LTS, 14.04 LTS a 16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="15b1d-113">Ubuntu Server 12.04 LTS, 14.04 LTS and 16.04 LTS (x86/x64)</span></span>

<span data-ttu-id="15b1d-114">Následující tabulka popisuje závislosti požadovaný balíček pro DSC pro Linux.</span><span class="sxs-lookup"><span data-stu-id="15b1d-114">The following table describes the required package dependencies for DSC for Linux.</span></span>

|  <span data-ttu-id="15b1d-115">Požadovaný balíček</span><span class="sxs-lookup"><span data-stu-id="15b1d-115">Required package</span></span> |  <span data-ttu-id="15b1d-116">Popis</span><span class="sxs-lookup"><span data-stu-id="15b1d-116">Description</span></span> |  <span data-ttu-id="15b1d-117">Minimální verze</span><span class="sxs-lookup"><span data-stu-id="15b1d-117">Minimum version</span></span> | 
|---|---|---|
| <span data-ttu-id="15b1d-118">glibc</span><span class="sxs-lookup"><span data-stu-id="15b1d-118">glibc</span></span>| <span data-ttu-id="15b1d-119">Knihovna GNU</span><span class="sxs-lookup"><span data-stu-id="15b1d-119">GNU Library</span></span>| <span data-ttu-id="15b1d-120">2…4 – 31.30</span><span class="sxs-lookup"><span data-stu-id="15b1d-120">2…4 – 31.30</span></span>| 
| <span data-ttu-id="15b1d-121">Python</span><span class="sxs-lookup"><span data-stu-id="15b1d-121">python</span></span>| <span data-ttu-id="15b1d-122">Python</span><span class="sxs-lookup"><span data-stu-id="15b1d-122">Python</span></span>| <span data-ttu-id="15b1d-123">2.4 – 3.4</span><span class="sxs-lookup"><span data-stu-id="15b1d-123">2.4 – 3.4</span></span>| 
| <span data-ttu-id="15b1d-124">omiserver</span><span class="sxs-lookup"><span data-stu-id="15b1d-124">omiserver</span></span>| <span data-ttu-id="15b1d-125">Infrastruktura OMI (Open Management Infrastructure)</span><span class="sxs-lookup"><span data-stu-id="15b1d-125">Open Management Infrastructure</span></span>| <span data-ttu-id="15b1d-126">1.0.8.1</span><span class="sxs-lookup"><span data-stu-id="15b1d-126">1.0.8.1</span></span>| 
| <span data-ttu-id="15b1d-127">OpenSSL</span><span class="sxs-lookup"><span data-stu-id="15b1d-127">openssl</span></span>| <span data-ttu-id="15b1d-128">Knihovny OpenSSL</span><span class="sxs-lookup"><span data-stu-id="15b1d-128">OpenSSL Libraries</span></span>| <span data-ttu-id="15b1d-129">0.9.8 nebo 1.0</span><span class="sxs-lookup"><span data-stu-id="15b1d-129">0.9.8 or 1.0</span></span>| 
| <span data-ttu-id="15b1d-130">ctypes</span><span class="sxs-lookup"><span data-stu-id="15b1d-130">ctypes</span></span>| <span data-ttu-id="15b1d-131">Knihovna Python CTypes</span><span class="sxs-lookup"><span data-stu-id="15b1d-131">Python CTypes library</span></span>| <span data-ttu-id="15b1d-132">Musí odpovídat verzi jazyka Python</span><span class="sxs-lookup"><span data-stu-id="15b1d-132">Must match Python version</span></span>| 
| <span data-ttu-id="15b1d-133">libcurl</span><span class="sxs-lookup"><span data-stu-id="15b1d-133">libcurl</span></span>| <span data-ttu-id="15b1d-134">Klientská knihovna pro cURL http</span><span class="sxs-lookup"><span data-stu-id="15b1d-134">cURL http client library</span></span>| <span data-ttu-id="15b1d-135">7.15.1</span><span class="sxs-lookup"><span data-stu-id="15b1d-135">7.15.1</span></span>| 

## <a name="installing-dsc-for-linux"></a><span data-ttu-id="15b1d-136">Instalace DSC pro Linux</span><span class="sxs-lookup"><span data-stu-id="15b1d-136">Installing DSC for Linux</span></span>

<span data-ttu-id="15b1d-137">Je nutné nainstalovat [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) před instalací DSC pro Linux.</span><span class="sxs-lookup"><span data-stu-id="15b1d-137">You must install the [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) before installing DSC for Linux.</span></span>

### <a name="installing-omi"></a><span data-ttu-id="15b1d-138">Instalace OMI</span><span class="sxs-lookup"><span data-stu-id="15b1d-138">Installing OMI</span></span>

<span data-ttu-id="15b1d-139">Konfigurace stavu požadovaného pro Linux vyžaduje server CIM infrastruktury OMI (Open Management Infrastructure), verze 1.0.8.1 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="15b1d-139">Desired State Configuration for Linux requires the Open Management Infrastructure (OMI) CIM server, version 1.0.8.1 or later.</span></span> <span data-ttu-id="15b1d-140">OMI si můžete stáhnout z otevřené skupiny: [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi).</span><span class="sxs-lookup"><span data-stu-id="15b1d-140">OMI can be downloaded from The Open Group: [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi).</span></span>

<span data-ttu-id="15b1d-141">Pokud chcete nainstalovat OMI, nainstalujte balíček, který je vhodný pro váš systém Linux (.rpm nebo .deb) a verzí OpenSSL (ssl_098 nebo ssl_100) a architektura (x64/x86).</span><span class="sxs-lookup"><span data-stu-id="15b1d-141">To install OMI, install the package that is appropriate for your Linux system (.rpm or .deb) and OpenSSL version (ssl_098 or ssl_100), and architecture (x64/x86).</span></span> <span data-ttu-id="15b1d-142">Ot. / min balíčky jsou vhodné pro CentOS, Red Hat Enterprise Linux, Oracle Linux a SUSE Linux Enterprise Server.</span><span class="sxs-lookup"><span data-stu-id="15b1d-142">RPM packages are appropriate for CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, and Oracle Linux.</span></span> <span data-ttu-id="15b1d-143">Bázi DEB balíčky jsou vhodné pro Debian GNU/Linux a Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="15b1d-143">DEB packages are appropriate for Debian GNU/Linux and Ubuntu Server.</span></span> <span data-ttu-id="15b1d-144">Ssl_098 balíčky jsou vhodné pro počítače s OpenSSL 0.9.8 nainstalována při ssl_100 balíčky jsou vhodné pro počítače s OpenSSL 1.0 nainstalovaný.</span><span class="sxs-lookup"><span data-stu-id="15b1d-144">The ssl_098 packages are appropriate for computers with OpenSSL 0.9.8 installed while the ssl_100 packages are appropriate for computers with OpenSSL 1.0 installed.</span></span>

> <span data-ttu-id="15b1d-145">**Poznámka:**: Chcete-li zjistit, že nainstalovaná verze OpenSSL, spusťte příkaz `openssl version`.</span><span class="sxs-lookup"><span data-stu-id="15b1d-145">**Note**: To determine the installed OpenSSL version, run the command `openssl version`.</span></span>

<span data-ttu-id="15b1d-146">Spusťte následující příkaz k instalaci v systému CentOS 7 x64 OMI.</span><span class="sxs-lookup"><span data-stu-id="15b1d-146">Run the following command to install OMI on a CentOS 7 x64 system.</span></span>

`# sudo rpm -Uvh omiserver-1.0.8.ssl_100.rpm`

### <a name="installing-dsc"></a><span data-ttu-id="15b1d-147">Instalace DSC</span><span class="sxs-lookup"><span data-stu-id="15b1d-147">Installing DSC</span></span>

<span data-ttu-id="15b1d-148">DSC pro Linux je k dispozici ke stažení [zde](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="15b1d-148">DSC for Linux is available for download [here](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/latest).</span></span> 

<span data-ttu-id="15b1d-149">Pokud chcete nainstalovat DSC, nainstalujte balíček, který je vhodný pro váš systém Linux (.rpm nebo .deb) a verzí OpenSSL (ssl_098 nebo ssl_100) a architektura (x64/x86).</span><span class="sxs-lookup"><span data-stu-id="15b1d-149">To install DSC, install the package that is appropriate for your Linux system (.rpm or .deb) and OpenSSL version (ssl_098 or ssl_100), and architecture (x64/x86).</span></span> <span data-ttu-id="15b1d-150">Ot. / min balíčky jsou vhodné pro CentOS, Red Hat Enterprise Linux, Oracle Linux a SUSE Linux Enterprise Server.</span><span class="sxs-lookup"><span data-stu-id="15b1d-150">RPM packages are appropriate for CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, and Oracle Linux.</span></span> <span data-ttu-id="15b1d-151">Bázi DEB balíčky jsou vhodné pro Debian GNU/Linux a Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="15b1d-151">DEB packages are appropriate for Debian GNU/Linux and Ubuntu Server.</span></span> <span data-ttu-id="15b1d-152">Ssl_098 balíčky jsou vhodné pro počítače s OpenSSL 0.9.8 nainstalována při ssl_100 balíčky jsou vhodné pro počítače s OpenSSL 1.0 nainstalovaný.</span><span class="sxs-lookup"><span data-stu-id="15b1d-152">The ssl_098 packages are appropriate for computers with OpenSSL 0.9.8 installed while the ssl_100 packages are appropriate for computers with OpenSSL 1.0 installed.</span></span>

> <span data-ttu-id="15b1d-153">**Poznámka:**: Chcete-li zjistit, že nainstalovaná verze OpenSSL, spusťte verze openssl příkaz.</span><span class="sxs-lookup"><span data-stu-id="15b1d-153">**Note**: To determine the installed OpenSSL version, run the command openssl version.</span></span>
 
<span data-ttu-id="15b1d-154">Spusťte následující příkaz k instalaci v systému CentOS 7 x64 DSC.</span><span class="sxs-lookup"><span data-stu-id="15b1d-154">Run the following command to install DSC on a CentOS 7 x64 system.</span></span>

`# sudo rpm -Uvh dsc-1.0.0-254.ssl_100.x64.rpm`


## <a name="using-dsc-for-linux"></a><span data-ttu-id="15b1d-155">Pro Linux pomocí DSC</span><span class="sxs-lookup"><span data-stu-id="15b1d-155">Using DSC for Linux</span></span>

<span data-ttu-id="15b1d-156">Následující části popisují, jak vytvořit a spustit konfigurace DSC na počítače se systémem Linux.</span><span class="sxs-lookup"><span data-stu-id="15b1d-156">The following sections explain how to create and run DSC configurations on Linux computers.</span></span>

### <a name="creating-a-configuration-mof-document"></a><span data-ttu-id="15b1d-157">Vytvoření dokumentu MOF konfigurace</span><span class="sxs-lookup"><span data-stu-id="15b1d-157">Creating a configuration MOF document</span></span>

<span data-ttu-id="15b1d-158">Klíčové slovo konfigurace Windows Powershellu se používá k vytvoření konfiguraci pro počítače Linux, stejně jako pro počítače se systémem Windows.</span><span class="sxs-lookup"><span data-stu-id="15b1d-158">The Windows PowerShell Configuration keyword is used to create a configuration for Linux computers, just like for Windows computers.</span></span> <span data-ttu-id="15b1d-159">Následující kroky popisují vytvoření dokumentu konfigurace pro počítač se systémem Linux pomocí prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15b1d-159">The following steps describe the creation of a configuration document for a Linux computer using Windows PowerShell.</span></span>

1. <span data-ttu-id="15b1d-160">Naimportujte modul nx.</span><span class="sxs-lookup"><span data-stu-id="15b1d-160">Import the nx module.</span></span> <span data-ttu-id="15b1d-161">Modul Windows PowerShell nx obsahuje schéma pro předdefinované prostředky pro DSC pro systémy Linux a musí být nainstalované do místního počítače a importovat v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="15b1d-161">The nx Windows PowerShell module contains the schema for Built-In resources for DSC for Linux, and must be installed to your local computer and imported in the configuration.</span></span>

    <span data-ttu-id="15b1d-162">– Chcete-li nainstalovat modul nx, zkopírujte adresář modulu nx buď `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` nebo `$PSHOME\Modules`.</span><span class="sxs-lookup"><span data-stu-id="15b1d-162">-To install the nx module, copy the nx module directory to either `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` or `$PSHOME\Modules`.</span></span> <span data-ttu-id="15b1d-163">Modul nx je součástí DSC Linux instalačního balíčku (MSI).</span><span class="sxs-lookup"><span data-stu-id="15b1d-163">The nx module is included in the DSC for Linux installation package (MSI).</span></span> <span data-ttu-id="15b1d-164">Chcete-li importovat modul nx ve vaší konfiguraci, použijte __Import DSCResource__ příkaz:</span><span class="sxs-lookup"><span data-stu-id="15b1d-164">To import the nx module in your configuration, use the __Import-DSCResource__ command:</span></span>
    
```powershell
Configuration ExampleConfiguration{
   
    Import-DSCResource -Module nx

}
```
2. <span data-ttu-id="15b1d-165">Definice konfigurace a generování dokumentu konfigurace:</span><span class="sxs-lookup"><span data-stu-id="15b1d-165">Define a configuration and generate the configuration document:</span></span>

```powershell
Configuration ExampleConfiguration{
   
    Import-DscResource -Module nx
 
    Node  "linuxhost.contoso.com"{
    nxFile ExampleFile {

        DestinationPath = "/tmp/example"
        Contents = "hello world `n"
        Ensure = "Present"
        Type = "File"
    }

    }
}
ExampleConfiguration -OutputPath:"C:\temp" 
```

### <a name="push-the-configuration-to-the-linux-computer"></a><span data-ttu-id="15b1d-166">Nabízená konfiguraci počítače se systémem Linux</span><span class="sxs-lookup"><span data-stu-id="15b1d-166">Push the configuration to the Linux computer</span></span>

<span data-ttu-id="15b1d-167">Konfigurace dokumenty (soubory MOF) můžete vloží do počítač Linux pomocí [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15b1d-167">Configuration documents (MOF files) can be pushed to the Linux computer using the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet.</span></span> <span data-ttu-id="15b1d-168">Chcete-li použít tuto rutinu spolu s [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx), nebo [Test DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) rutin vzdáleně na počítač se systémem Linux, je nutné použít CIMSession.</span><span class="sxs-lookup"><span data-stu-id="15b1d-168">In order to use this cmdlet, along with the [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx), or [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) cmdlets, remotely to a Linux computer, you must use a CIMSession.</span></span> <span data-ttu-id="15b1d-169">[New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) rutina se používá k vytvoření CIMSession do počítače se systémem Linux.</span><span class="sxs-lookup"><span data-stu-id="15b1d-169">The [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) cmdlet is used to create a CIMSession to the Linux computer.</span></span>

<span data-ttu-id="15b1d-170">Následující kód ukazuje, jak vytvořit CIMSession pro DSC pro Linux.</span><span class="sxs-lookup"><span data-stu-id="15b1d-170">The following code shows how to create a CIMSession for DSC for Linux.</span></span>

```powershell
$Node = "ostc-dsc-01"
$Credential = Get-Credential -UserName:"root" -Message:"Enter Password:"

#Ignore SSL certificate validation
#$opt = New-CimSessionOption -UseSsl:$true -SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true

#Options for a trusted SSL certificate
$opt = New-CimSessionOption -UseSsl:$true 
$Sess=New-CimSession -Credential:$credential -ComputerName:$Node -Port:5986 -Authentication:basic -SessionOption:$opt -OperationTimeoutSec:90 
```

> <span data-ttu-id="15b1d-171">**Poznámka:**:</span><span class="sxs-lookup"><span data-stu-id="15b1d-171">**Note**:</span></span>
* <span data-ttu-id="15b1d-172">"Push" režimu musí být přihlašovací údaje uživatele root uživatele na počítače se systémem Linux.</span><span class="sxs-lookup"><span data-stu-id="15b1d-172">For “Push” mode, the user credential must be the root user on the Linux computer.</span></span>
* <span data-ttu-id="15b1d-173">Pro Linux, New-CimSession musí použít s parametrem – UseSSL nastaveným na $true, podporovaná jsou jenom připojení protokolem SSL/TLS pro DSC.</span><span class="sxs-lookup"><span data-stu-id="15b1d-173">Only SSL/TLS connections are supported for DSC for Linux, the New-CimSession must be used with the –UseSSL parameter set to $true.</span></span>
* <span data-ttu-id="15b1d-174">Certifikát SSL používaný OMI (DSC) je zadána v souboru: `/opt/omi/etc/omiserver.conf` s vlastnostmi: pemfile a keyfile.</span><span class="sxs-lookup"><span data-stu-id="15b1d-174">The SSL certificate used by OMI (for DSC) is specified in the file: `/opt/omi/etc/omiserver.conf` with the properties: pemfile and keyfile.</span></span>
<span data-ttu-id="15b1d-175">Pokud tento certifikát není důvěryhodný počítači s Windows, kterou používáte [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) na rutinu, můžete ignorovat ověření certifikátu s možnostmi CIMSession:`-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`</span><span class="sxs-lookup"><span data-stu-id="15b1d-175">If this certificate is not trusted by the Windows computer that you are running the [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) cmdlet on, you can choose to ignore certificate validation with the CIMSession Options: `-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`</span></span>

<span data-ttu-id="15b1d-176">Spusťte následující příkaz pro uložení konfigurace DSC k uzlu Linux.</span><span class="sxs-lookup"><span data-stu-id="15b1d-176">Run the following command to push the DSC configuration to the Linux node.</span></span>

`Start-DscConfiguration -Path:"C:\temp" -CimSession:$Sess -Wait -Verbose`

### <a name="distribute-the-configuration-with-a-pull-server"></a><span data-ttu-id="15b1d-177">Distribuce konfigurace serveru vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="15b1d-177">Distribute the configuration with a pull server</span></span>

<span data-ttu-id="15b1d-178">Konfigurace můžete rozdělit počítač se systémem Linux pomocí serveru vyžádané replikace, stejně jako pro počítače se systémem Windows.</span><span class="sxs-lookup"><span data-stu-id="15b1d-178">Configurations can be distributed to a Linux computer with a pull server, just like for Windows computers.</span></span> <span data-ttu-id="15b1d-179">Pokyny k používání serveru vyžádané replikace, najdete v části [Windows PowerShell požadovaného stavu konfigurace vyžadování servery](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="15b1d-179">For guidance on using a pull server, see [Windows PowerShell Desired State Configuration Pull Servers](pullServer.md).</span></span> <span data-ttu-id="15b1d-180">Další informace a omezení související s použitím počítače se systémem Linux s načítacího serveru najdete v tématu poznámky k verzi pro konfigurace požadovaného stavu pro Linux.</span><span class="sxs-lookup"><span data-stu-id="15b1d-180">For additional information and limitations related to using Linux computers with a pull server, see the Release Notes for Desired State Configuration for Linux.</span></span>

### <a name="working-with-configurations-locally"></a><span data-ttu-id="15b1d-181">Práce s konfigurací místně</span><span class="sxs-lookup"><span data-stu-id="15b1d-181">Working with configurations locally</span></span>

<span data-ttu-id="15b1d-182">DSC pro Linux obsahuje skripty pro práci s konfiguraci z místního počítače se systémem Linux.</span><span class="sxs-lookup"><span data-stu-id="15b1d-182">DSC for Linux includes scripts to work with configuration from the local Linux computer.</span></span> <span data-ttu-id="15b1d-183">Tyto skripty jsou najít v `/opt/microsoft/dsc/Scripts` a zahrnují následující:</span><span class="sxs-lookup"><span data-stu-id="15b1d-183">These scripts are locate in `/opt/microsoft/dsc/Scripts` and include the following:</span></span>
* <span data-ttu-id="15b1d-184">GetDscConfiguration.py</span><span class="sxs-lookup"><span data-stu-id="15b1d-184">GetDscConfiguration.py</span></span>

 <span data-ttu-id="15b1d-185">Vrátí aktuální konfiguraci použita na počítač.</span><span class="sxs-lookup"><span data-stu-id="15b1d-185">Returns the current configuration applied to the computer.</span></span> <span data-ttu-id="15b1d-186">Podobně jako rutiny Get-DscConfiguration rutinu prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15b1d-186">Similar to the Windows PowerShell cmdlet Get-DscConfiguration cmdlet.</span></span>

`# sudo ./GetDscConfiguration.py`

* <span data-ttu-id="15b1d-187">GetDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="15b1d-187">GetDscLocalConfigurationManager.py</span></span>

 <span data-ttu-id="15b1d-188">Vrátí aktuální meta konfigurace použita na počítač.</span><span class="sxs-lookup"><span data-stu-id="15b1d-188">Returns the current meta-configuration applied to the computer.</span></span> <span data-ttu-id="15b1d-189">Podobně jako rutiny [Get-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15b1d-189">Similar to the cmdlet [Get-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx) cmdlet.</span></span>

`# sudo ./GetDscLocalConfigurationManager.py`

* <span data-ttu-id="15b1d-190">InstallModule.py</span><span class="sxs-lookup"><span data-stu-id="15b1d-190">InstallModule.py</span></span>

 <span data-ttu-id="15b1d-191">Nainstaluje vlastní modul prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="15b1d-191">Installs a custom DSC resource module.</span></span> <span data-ttu-id="15b1d-192">Vyžaduje cestu k souboru ZIP obsahující modulu objektu sdílené knihovny a soubory MOF schématu.</span><span class="sxs-lookup"><span data-stu-id="15b1d-192">Requires the path to a .zip file containing the module shared object library and schema MOF files.</span></span>

`# sudo ./InstallModule.py /tmp/cnx_Resource.zip`

* <span data-ttu-id="15b1d-193">RemoveModule.py</span><span class="sxs-lookup"><span data-stu-id="15b1d-193">RemoveModule.py</span></span>

 <span data-ttu-id="15b1d-194">Odebere modul vlastní prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="15b1d-194">Removes a custom DSC resource module.</span></span> <span data-ttu-id="15b1d-195">Vyžaduje název modulu odebrat.</span><span class="sxs-lookup"><span data-stu-id="15b1d-195">Requires the name of the module to remove.</span></span>

`# sudo ./RemoveModule.py cnx_Resource`

* <span data-ttu-id="15b1d-196">StartDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="15b1d-196">StartDscLocalConfigurationManager.py</span></span> 

 <span data-ttu-id="15b1d-197">Konfigurační soubor MOF se vztahuje na počítač.</span><span class="sxs-lookup"><span data-stu-id="15b1d-197">Applies a configuration MOF file to the computer.</span></span> <span data-ttu-id="15b1d-198">Podobně jako [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15b1d-198">Similar to the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet.</span></span> <span data-ttu-id="15b1d-199">Vyžaduje cesta ke konfiguraci MOF použít.</span><span class="sxs-lookup"><span data-stu-id="15b1d-199">Requires the path to the configuration MOF to apply.</span></span>

`# sudo ./StartDscLocalConfigurationManager.py –configurationmof /tmp/localhost.mof`

* <span data-ttu-id="15b1d-200">SetDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="15b1d-200">SetDscLocalConfigurationManager.py</span></span>

 <span data-ttu-id="15b1d-201">Soubor MOF Meta konfigurace se vztahuje na počítač.</span><span class="sxs-lookup"><span data-stu-id="15b1d-201">Applies a Meta Configuration MOF file to the computer.</span></span> <span data-ttu-id="15b1d-202">Podobně jako [Set-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="15b1d-202">Similar to the [Set-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx) cmdlet.</span></span> <span data-ttu-id="15b1d-203">Vyžaduje cestu k MOF konfigurace Meta použít.</span><span class="sxs-lookup"><span data-stu-id="15b1d-203">Requires the path to the Meta Configuration MOF to apply.</span></span>

`# sudo ./SetDscLocalConfigurationManager.py –configurationmof /tmp/localhost.meta.mof`

## <a name="powershell-desired-state-configuration-for-linux-log-files"></a><span data-ttu-id="15b1d-204">Prostředí PowerShell konfigurace požadovaného stavu pro soubory protokolů systému Linux</span><span class="sxs-lookup"><span data-stu-id="15b1d-204">PowerShell Desired State Configuration for Linux Log Files</span></span>

<span data-ttu-id="15b1d-205">Následující soubory protokolu jsou generovány pro DSC pro Linux zprávy.</span><span class="sxs-lookup"><span data-stu-id="15b1d-205">The following log files are generated for DSC for Linux messages.</span></span>

|<span data-ttu-id="15b1d-206">Soubor protokolu</span><span class="sxs-lookup"><span data-stu-id="15b1d-206">Log file</span></span>|<span data-ttu-id="15b1d-207">Adresář</span><span class="sxs-lookup"><span data-stu-id="15b1d-207">Directory</span></span>|<span data-ttu-id="15b1d-208">Popis</span><span class="sxs-lookup"><span data-stu-id="15b1d-208">Description</span></span>|
|---|---|---|
|<span data-ttu-id="15b1d-209">omiserver.log</span><span class="sxs-lookup"><span data-stu-id="15b1d-209">omiserver.log</span></span>|<span data-ttu-id="15b1d-210">/var/OPT/OMI/log</span><span class="sxs-lookup"><span data-stu-id="15b1d-210">/var/opt/omi/log</span></span>|<span data-ttu-id="15b1d-211">Zprávy týkající se operace server OMI CIM.</span><span class="sxs-lookup"><span data-stu-id="15b1d-211">Messages relating to the operation of the OMI CIM server.</span></span>|
|<span data-ttu-id="15b1d-212">dsc.log</span><span class="sxs-lookup"><span data-stu-id="15b1d-212">dsc.log</span></span>|<span data-ttu-id="15b1d-213">/var/OPT/OMI/log</span><span class="sxs-lookup"><span data-stu-id="15b1d-213">/var/opt/omi/log</span></span>|<span data-ttu-id="15b1d-214">Zprávy týkající se operace operace prostředků místní Configuration Manager (LCM) a DSC.</span><span class="sxs-lookup"><span data-stu-id="15b1d-214">Messages relating to the operation of the Local Configuration Manager (LCM) and DSC resource operations.</span></span>|

