---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Psaní nápovědy pro konfigurace DSC"
ms.openlocfilehash: c5d499ec887829c864c0f63f64af2d0a7738220b
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="writing-help-for-dsc-configurations"></a><span data-ttu-id="ee6b0-103">Psaní nápovědy pro konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="ee6b0-103">Writing help for DSC configurations</span></span>

><span data-ttu-id="ee6b0-104">Platí pro: Windows prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ee6b0-104">Applies To: Windows Windows PowerShell 5.0</span></span>

<span data-ttu-id="ee6b0-105">Nápověda založená na komentáře můžete použít v konfiguracích DSC.</span><span class="sxs-lookup"><span data-stu-id="ee6b0-105">You can use comment-based help in DSC configurations.</span></span> <span data-ttu-id="ee6b0-106">Mohou uživatelé v nápovědě voláním funkce konfigurace se `-?`, nebo pomocí [Get-Help](https://technet.microsoft.com/library/hh849696.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="ee6b0-106">Users can access the help by calling the configuration function with `-?`, or by using the [Get-Help](https://technet.microsoft.com/library/hh849696.aspx) cmdlet.</span></span> <span data-ttu-id="ee6b0-107">Další informace o Nápověda založená na komentářích prostředí PowerShell najdete v tématu [about_Comment_Based_Help](https://technet.microsoft.com/library/hh847834.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee6b0-107">For more information about PowerShell comment-based help, see [about_Comment_Based_Help](https://technet.microsoft.com/library/hh847834.aspx).</span></span>

<span data-ttu-id="ee6b0-108">Následující příklad ukazuje skript, který obsahuje konfiguraci a založená na komentářích nápovědy pro ni:</span><span class="sxs-lookup"><span data-stu-id="ee6b0-108">The following example shows a script that contains a configuration and comment-based help for it:</span></span>

```powershell
<#
.SYNOPSIS
A brief description of the function or script. This keyword can be used only once for each configuration.


.DESCRIPTION
A detailed description of the function or script. This keyword can be used only once for each configuration.


.PARAMETER ComputerName
The description of a parameter. Add a .PARAMETER keyword for each parameter in the function or script syntax.

Type the parameter name on the same line as the .PARAMETER keyword. Type the parameter description on the lines following the .PARAMETER keyword. 
Windows PowerShell interprets all text between the .PARAMETER line and the next keyword or the end of the comment block as part of the parameter description. 
The description can include paragraph breaks.

The Parameter keywords can appear in any order in the comment block, but the function or script syntax determines the order in which the parameters 
(and their descriptions) appear in help topic. To change the order, change the syntax.

.PARAMETER FilePath
Provide a PARAMETER section for each parameter that your script or function accepts.

.EXAMPLE
A sample command that uses the function or script, optionally followed by sample output and a description. Repeat this keyword for each example. If you have multiple examples,
there is no need to number them. PowerShell will number the examples in help text.

.EXAMPLE
This example will be labeled "EXAMPLE 2" when help is displayed to the user.
#>

configuration HelpSample1
{
    param([string]$ComputerName,[string]$FilePath)
    File f
    {
        Contents="Hello World"
        DestinationPath = "c:\Destination.txt"
    }
}
```

## <a name="viewing-configuration-help"></a><span data-ttu-id="ee6b0-109">Nápověda k nástroji Konfigurace zobrazení</span><span class="sxs-lookup"><span data-stu-id="ee6b0-109">Viewing configuration help</span></span>

<span data-ttu-id="ee6b0-110">Chcete-li zobrazit nápovědu pro konfiguraci, použijte **Get-Help** rutiny s název funkce nebo typ následuje název funkce `-?`.</span><span class="sxs-lookup"><span data-stu-id="ee6b0-110">To view the help for a configuration, use the **Get-Help** cmdlet with the name of the function, or type the name of the function followed by `-?`.</span></span> <span data-ttu-id="ee6b0-111">Následuje výstup předchozí funkce když předána **Get-Help**:</span><span class="sxs-lookup"><span data-stu-id="ee6b0-111">The following is the output of the previous function when passed to **Get-Help**:</span></span>

```powershell
PS C:\> Get-Help HelpSample1

NAME
    HelpSample1
    
SYNOPSIS
    A brief description of the function or script. This keyword can be used only once for each configuration.
    
    
SYNTAX
    HelpSample1 [[-InstanceName] <String>] [[-DependsOn] <String[]>] [[-OutputPath] <String>] [[-ConfigurationData] <Hashtable>] [[-ComputerName] 
    <String>] [[-FilePath] <String>] [<CommonParameters>]
    
    
DESCRIPTION
    A detailed description of the function or script. This keyword can be used only once for each configuration.
    

RELATED LINKS

REMARKS
    To see the examples, type: "get-help HelpSample1 -examples".
    For more information, type: "get-help HelpSample1 -detailed".
    For technical information, type: "get-help HelpSample1 -full".
```

## <a name="see-also"></a><span data-ttu-id="ee6b0-112">Viz také</span><span class="sxs-lookup"><span data-stu-id="ee6b0-112">See Also</span></span>
* [<span data-ttu-id="ee6b0-113">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="ee6b0-113">DSC Configurations</span></span>](configurations.md)

