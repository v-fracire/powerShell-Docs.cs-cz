---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Závislosti prostředků pomocí DependsOn
ms.openlocfilehash: 0d060f7d99bd261b0766028b245d4d32a5e1c349
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403709"
---
# <a name="resource-dependencies-using-dependson"></a><span data-ttu-id="b7a6c-103">Závislosti prostředků pomocí DependsOn</span><span class="sxs-lookup"><span data-stu-id="b7a6c-103">Resource dependencies using DependsOn</span></span>

<span data-ttu-id="b7a6c-104">Při psaní [konfigurace](configurations.md), přidáte [prostředků bloky](../resources/resources.md) pro konfiguraci aspektů cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-104">When you write [Configurations](configurations.md), you add [Resource blocks](../resources/resources.md) to configure aspects of a target Node.</span></span> <span data-ttu-id="b7a6c-105">Jak vám pokračujte přidáním prostředků bloky, vaše konfigurace můžou růst poměrně velké a těžkopádný proces pro správu.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-105">As you continue to add Resource blocks, your Configurations can grow quite large and cumbersome to manage.</span></span> <span data-ttu-id="b7a6c-106">Jeden takový problém je použité pořadí bloků prostředků.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-106">One such challenge is the applied order of your resource blocks.</span></span> <span data-ttu-id="b7a6c-107">Obvykle prostředky se použijí v pořadí, ve kterém jsou definovány v rámci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-107">Typically resources are applied in the order they are defined within the Configuration.</span></span> <span data-ttu-id="b7a6c-108">S růstem vaší konfigurace větší a složitější, můžete použít `DependsOn` klíč změníte použitých prostředků tak, že zadáte prostředku, na kterých závisí jiný prostředek.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-108">As your Configuration grows larger and more complex, you can use the `DependsOn` key to change the applied order of your resources by specifying that a resource depends on another resource.</span></span>

<span data-ttu-id="b7a6c-109">`DependsOn` Klíč lze použít v jakékoli prostředků bloku.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-109">The `DependsOn` key can be used in any Resource block.</span></span> <span data-ttu-id="b7a6c-110">Je definován pomocí mechanismu klíč/hodnota jako další klíče prostředku.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-110">It is defined with the same key/value mechanism as other Resource keys.</span></span> <span data-ttu-id="b7a6c-111">`DependsOn` Klíč očekává, že pole řetězců s následující syntaxí.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-111">The `DependsOn` key expects an array of strings with the following syntax.</span></span>

```
DependsOn = '[<Resource Type>]<Resoure Name>', '[<Resource Type>]<Resource Name'
```

<span data-ttu-id="b7a6c-112">Následující příklad nakonfiguruje pravidlo brány firewall po povolení a konfigurace veřejný profil.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-112">The following example configures a firewall rule after enabling and configuring the public profile.</span></span>

```powershell
# Install the NetworkingDSC module to configure firewall rules and profiles.
Install-Module -Name NetworkingDSC

Configuration ConfigureFirewall
{
    Import-DSCResource -Name Firewall, FirewallProfile
    Node localhost
    {
        Firewall Firewall
        {
            Name                  = 'IIS-WebServerRole-HTTP-In-TCP'
            Ensure                = 'Present'
            Enabled               = 'True'
            DependsOn             = '[FirewallProfile]FirewallProfilePublic'
        }

        FirewallProfile FirewallProfilePublic
        {
            Name = 'Public'
            Enabled = 'True'
            DefaultInboundAction = 'Block'
            DefaultOutboundAction = 'Allow'
            AllowInboundRules = 'True'
            AllowLocalFirewallRules = 'False'
            AllowLocalIPsecRules = 'False'
            NotifyOnListen = 'True'
            LogFileName = '%systemroot%\system32\LogFiles\Firewall\pfirewall.log'
            LogMaxSizeKilobytes = 16384
            LogAllowed = 'False'
            LogBlocked = 'True'
            LogIgnored = 'NotConfigured'
        }
    }
}

ConfigureFirewall -OutputPath C:\Temp\
```

<span data-ttu-id="b7a6c-113">Při použití konfigurace profil firewallu v programu bude vždy nakonfigurovaný nejprve bez ohledu na pořadí, které jsou definovány bloky prostředků.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-113">When you apply the Configuration, the firewall profile will always be configured first regardless of which order the Resource blocks are defined.</span></span> <span data-ttu-id="b7a6c-114">Pokud byste použít konfiguraci, je nutné si uvědomit vaší cílové uzly existující konfigurace, takže se můžete vrátit v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-114">If you apply the Configuration, be sure to note your target Nodes existing Configuration so you can revert if desired.</span></span>

```
PS> Start-DSCConfiguration -Verbose -Wait -Path C:\Temp\ -ComputerName localhost

VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendConfigurationApply,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer SERVER01 with user sid S-1-5-21-181338-0189125723-1543119021-1282804.
VERBOSE: [SERVER01]: LCM:  [ Start  Set      ]
VERBOSE: [SERVER01]:                            [DSCEngine] Importing the module C:\Program Files\WindowsPowerShell\Modules\NetworkingDsc\6.1.0.0\DscResources\MSFT_Firewall\MSFT_Firewall.psm1 in force mode.
VERBOSE: [SERVER01]:                            [DSCEngine] Importing the module C:\Program Files\WindowsPowerShell\Modules\NetworkingDsc\6.1.0.0\DscResources\MSFT_FirewallProfile\MSFT_FirewallProfile.psm1 in force mode.
VERBOSE: [SERVER01]: LCM:  [ Start  Resource ]  [[FirewallProfile]FirewallProfilePublic]
VERBOSE: [SERVER01]: LCM:  [ Start  Test     ]  [[FirewallProfile]FirewallProfilePublic]
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Importing the module MSFT_FirewallProfile in force mode.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Testing Firewall Public Profile.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Firewall Public Profile "AllowInboundRules" is "NotConfigured" but should be "True". Change required.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Firewall Public Profile "AllowLocalFirewallRules" is "NotConfigured" but should be "False". Change required.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Firewall Public Profile "AllowLocalIPsecRules" is "NotConfigured" but should be "False". Change required.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Firewall Public Profile "DefaultOutboundAction" is "NotConfigured" but should be "Allow". Change required.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Firewall Public Profile "LogBlocked" is "False" but should be "True". Change required.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Test-TargetResource: Firewall Public Profile "LogMaxSizeKilobytes" is "4096" but should be "16384". Change required.
VERBOSE: [SERVER01]: LCM:  [ End    Test     ]  [[FirewallProfile]FirewallProfilePublic]  in 1.6890 seconds.
VERBOSE: [SERVER01]: LCM:  [ Start  Set      ]  [[FirewallProfile]FirewallProfilePublic]
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Importing the module MSFT_FirewallProfile in force mode.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile.
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile parameter AllowInboundRules to "AllowInboundRules".
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile parameter AllowLocalFirewallRules to "AllowLocalFirewallRules".
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile parameter AllowLocalIPsecRules to "AllowLocalIPsecRules".
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile parameter DefaultOutboundAction to "DefaultOutboundAction".
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile parameter LogBlocked to "LogBlocked".
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile parameter LogMaxSizeKilobytes to "LogMaxSizeKilobytes".
VERBOSE: [SERVER01]:                            [[FirewallProfile]FirewallProfilePublic] Set-TargetResource: Setting Firewall Public Profile updated.
VERBOSE: [SERVER01]: LCM:  [ End    Set      ]  [[FirewallProfile]FirewallProfilePublic]  in 10.0360 seconds.
VERBOSE: [SERVER01]: LCM:  [ End    Resource ]  [[FirewallProfile]FirewallProfilePublic]
VERBOSE: [SERVER01]: LCM:  [ Start  Resource ]  [[Firewall]Firewall]
VERBOSE: [SERVER01]: LCM:  [ Start  Test     ]  [[Firewall]Firewall]
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Importing the module MSFT_Firewall in force mode.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Test-TargetResource: Checking settings for firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP'.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Test-TargetResource: Find firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP'.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Get-FirewallRule: No Firewall Rule found with Name 'IIS-WebServerRole-HTTP-In-TCP'.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Test-TargetResource: Firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP' does not exist.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Test-TargetResource: Check Firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP' returning False.
VERBOSE: [SERVER01]: LCM:  [ End    Test     ]  [[Firewall]Firewall]  in 1.1780 seconds.
VERBOSE: [SERVER01]: LCM:  [ Start  Set      ]  [[Firewall]Firewall]
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Importing the module MSFT_Firewall in force mode.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Set-TargetResource: Applying settings for firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP'.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Set-TargetResource: Find firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP'.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Get-FirewallRule: No Firewall Rule found with Name 'IIS-WebServerRole-HTTP-In-TCP'.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Set-TargetResource: We want the firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP' to exist since Ensure is set to Present.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] Set-TargetResource: We want the firewall rule with Name 'IIS-WebServerRole-HTTP-In-TCP' to exist, but it does not.
VERBOSE: [SERVER01]:                            [[Firewall]Firewall] New-NetFirewallRule DisplayName: IIS-WebServerRole-HTTP-In-TCP
VERBOSE: [SERVER01]: LCM:  [ End    Set      ]  [[Firewall]Firewall]  in 1.0850 seconds.
VERBOSE: [SERVER01]: LCM:  [ End    Resource ]  [[Firewall]Firewall]
VERBOSE: [SERVER01]: LCM:  [ End    Set      ]
VERBOSE: [SERVER01]: LCM:  [ End    Set      ]    in  15.2880 seconds.
VERBOSE: Operation 'Invoke CimMethod' complete.
VERBOSE: Time taken for configuration job to complete is 15.385 seconds
```

<span data-ttu-id="b7a6c-115">To také zajistí, že pokud **FirewallProfile** prostředků z nějakého důvodu selže **brány Firewall** bloku nebude spuštěno i v případě, že se definuje jako první.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-115">This also ensures that if the **FirewallProfile** resource fails for any reason, the **Firewall** block will not execute even though it was defined first.</span></span> <span data-ttu-id="b7a6c-116">`DependsOn` Klíč zajišťuje větší flexibilitu v seskupení prostředků bloky a ujistíte, že se závislostí vyřešit před provedením prostředku.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-116">The `DependsOn` key allows more flexibility in grouping resource blocks and ensuring that dependencies are resolved before a Resource executes.</span></span>

<span data-ttu-id="b7a6c-117">V pokročilejší konfigurace, můžete také použít [napříč závislost uzlu](crossNodeDependencies.md) umožňující ještě podrobnější řízení (například zajištění řadič domény je nakonfigurován než klienta připojíte k doméně).</span><span class="sxs-lookup"><span data-stu-id="b7a6c-117">In more advanced Configurations, you can also use [Cross Node Dependency](crossNodeDependencies.md) to allow even more granular control (For example, ensuring a domain controller is configured before joining a client to the domain).</span></span>

## <a name="cleaning-up"></a><span data-ttu-id="b7a6c-118">Čištění</span><span class="sxs-lookup"><span data-stu-id="b7a6c-118">Cleaning Up</span></span>

<span data-ttu-id="b7a6c-119">Pokud jste použili výše uvedené konfiguraci, můžete se obrátit klíče vrátit zpět všechny změny.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-119">If you applied the Configuration above, you can reverse keys to undo any changes.</span></span> <span data-ttu-id="b7a6c-120">V příkladu výše, nastavení **povoleno** klíče na hodnotu false zakáže pravidlo brány firewall a profilu.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-120">In the above example, setting the **Enabled** key to false will disable the firewall rule and profile.</span></span> <span data-ttu-id="b7a6c-121">V příkladu by měl změnit podle potřeby tak, aby odpovídaly předchozí nakonfigurovaný stav cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="b7a6c-121">You should modify the example as needed to match your target Node's previous configured state.</span></span>

```powershell
        Firewall Firewall
        {
            Name                  = 'IIS-WebServerRole-HTTP-In-TCP'
            Enabled               = 'False'
            DependsOn             = '[FirewallProfile]FirewallProfilePublic'
        }

        FirewallProfile FirewallProfilePublic
        {
            Name = 'Public'
            Enabled = 'False'
        }
```

## <a name="see-also"></a><span data-ttu-id="b7a6c-122">Viz taky</span><span class="sxs-lookup"><span data-stu-id="b7a6c-122">See also</span></span>

- [<span data-ttu-id="b7a6c-123">Použití závislostí mezi uzly</span><span class="sxs-lookup"><span data-stu-id="b7a6c-123">Use Cross Node Dependencies</span></span>](./crossNodeDependencies.md)
