---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Psaní nápovědy ke konfiguracím DSC
ms.openlocfilehash: 498ec0f594ed3229e097903c4ea2ae34d3da03a2
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403809"
---
# <a name="writing-help-for-dsc-configurations"></a><span data-ttu-id="591de-103">Psaní nápovědy ke konfiguracím DSC</span><span class="sxs-lookup"><span data-stu-id="591de-103">Writing help for DSC configurations</span></span>

><span data-ttu-id="591de-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="591de-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="591de-105">Nápověda založená na komentáře můžete v konfiguracích DSC.</span><span class="sxs-lookup"><span data-stu-id="591de-105">You can use comment-based help in DSC configurations.</span></span> <span data-ttu-id="591de-106">Uživatelé můžou používat v nápovědě tak volání **konfigurace** s `-?`, nebo pomocí [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) rutiny.</span><span class="sxs-lookup"><span data-stu-id="591de-106">Users can access the help by calling the **Configuration** with `-?`, or by using the [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) cmdlet.</span></span> <span data-ttu-id="591de-107">Umístit vaši přímo nad založená na komentářích pomoc `Configuration` – klíčové slovo.</span><span class="sxs-lookup"><span data-stu-id="591de-107">Place your Comment-based help directly above the `Configuration` keyword.</span></span>
<span data-ttu-id="591de-108">Parametr nápovědy v řádku můžete umístit vaše blok komentáře a přímo nad deklaraci parametru nebo obojí stejně jako v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="591de-108">You can place parameter help in-line with your comment block, directly above the parameter declaration, or both as in the example below.</span></span>

<span data-ttu-id="591de-109">Další informace o Nápověda založená na komentářích prostředí PowerShell najdete v tématu [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).</span><span class="sxs-lookup"><span data-stu-id="591de-109">For more information about PowerShell comment-based help, see [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).</span></span>

> [!NOTE]
> <span data-ttu-id="591de-110">Vývojová prostředí PowerShell, jako jsou VSCode a ISE, je navíc fragmenty kódu, aby bylo možné automaticky vložit komentář bloku šablony.</span><span class="sxs-lookup"><span data-stu-id="591de-110">PowerShell development environments, like VSCode and the ISE, also have snippets to allow you to automatically insert comment block templates.</span></span>

<span data-ttu-id="591de-111">Následující příklad ukazuje skript, který obsahuje konfiguraci a založená na komentářích nápovědy pro něj.</span><span class="sxs-lookup"><span data-stu-id="591de-111">The following example shows a script that contains a configuration and comment-based help for it.</span></span> <span data-ttu-id="591de-112">Tento příklad znázorňuje konfiguraci s parametry.</span><span class="sxs-lookup"><span data-stu-id="591de-112">This example shows a Configuration with parameters.</span></span> <span data-ttu-id="591de-113">Další informace o používání parametrů ve vašich konfiguracích najdete v tématu [přidání parametrů ke konfiguraci](add-parameters-to-a-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="591de-113">To learn more about using parameters in your Configurations, see [Add Parameters to your Configurations](add-parameters-to-a-configuration.md).</span></span>

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

.EXAMPLE
HelpSample -ComputerName localhost

A sample command that uses the function or script, optionally followed by sample output and a description. Repeat this keyword for each example.
PowerShell automatically prefaces the first line with a PowerShell prompt. Additional lines are treated as output and description. The example can contain spaces, newlines and PowerShell code.

If you have multiple examples, there is no need to number them. PowerShell will number the examples in help text.
.EXAMPLE
HelpSample -FilePath "C:\output.txt"

This example will be labeled "EXAMPLE 2" when help is displayed to the user.
#>
configuration HelpSample1
{
    param
    (
        [string]$ComputerName = 'localhost',
        # Provide a PARAMETER section for each parameter that your script or function accepts.
        [string]$FilePath = 'C:\Destination.txt'
    )

    Node $ComputerName
    {
        File HelloWorld
        {
            Contents="Hello World"
            DestinationPath = $FilePath
        }
    }
}
```

## <a name="viewing-configuration-help"></a><span data-ttu-id="591de-114">Zobrazení konfigurace nápovědy</span><span class="sxs-lookup"><span data-stu-id="591de-114">Viewing configuration help</span></span>

<span data-ttu-id="591de-115">Chcete-li zobrazit nápovědu pro konfiguraci, použijte `Get-Help` rutinu s názvem funkce nebo zadejte název funkce následovaný `-?`.</span><span class="sxs-lookup"><span data-stu-id="591de-115">To view the help for a configuration, use the `Get-Help` cmdlet with the name of the function, or type the name of the function followed by `-?`.</span></span> <span data-ttu-id="591de-116">Následuje výstupu předchozí konfiguraci předán `Get-Help`.</span><span class="sxs-lookup"><span data-stu-id="591de-116">The following is the output of the previous Configuration passed to `Get-Help`.</span></span>

```powershell
Get-Help HelpSample1 -Detailed
```

```output
NAME
    HelpSample1

SYNOPSIS
    A brief description of the function or script. This keyword can be used only once for each configuration.


SYNTAX
    HelpSample1 [[-InstanceName] <String>] [[-DependsOn] <String[]>] [[-PsDscRunAsCredential] <PSCredential>] [[-OutputPath] <String>] [[-ConfigurationData] <Hashtable>] [[-ComputerName] <String>] [[-FilePath] <String>] [<CommonParameters>]


DESCRIPTION
    A detailed description of the function or script. This keyword can be used only once for each configuration.


PARAMETERS
    -InstanceName <String>

    -DependsOn <String[]>

    -PsDscRunAsCredential <PSCredential>

    -OutputPath <String>

    -ConfigurationData <Hashtable>

    -ComputerName <String>
        The description of a parameter. Add a .PARAMETER keyword for each parameter in the function or script syntax.

        Type the parameter name on the same line as the .PARAMETER keyword. Type the parameter description on the lines following the .PARAMETER keyword.
        Windows PowerShell interprets all text between the .PARAMETER line and the next keyword or the end of the comment block as part of the parameter description.
        The description can include paragraph breaks.

        The Parameter keywords can appear in any order in the comment block, but the function or script syntax determines the order in which the parameters
        (and their descriptions) appear in help topic. To change the order, change the syntax.

    -FilePath <String>
        Provide a PARAMETER section for each parameter that your script or function accepts.

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (https:/go.microsoft.com/fwlink/?LinkID=113216).

    -------------------------- EXAMPLE 1 --------------------------

    PS C:\>HelpSample -ComputerName localhost

    A sample command that uses the function or script, optionally followed by sample output and a description. Repeat this keyword for each example.
    PowerShell automatically prefaces the first line with a PowerShell prompt. Additional lines are treated as output and description. The example can contain spaces, newlines and PowerShell code.

    If you have multiple examples, there is no need to number them. PowerShell will number the examples in help text.




    -------------------------- EXAMPLE 2 --------------------------

    PS C:\>HelpSample -FilePath "C:\output.txt"

    This example will be labeled "EXAMPLE 2" when help is displayed to the user.




REMARKS
    To see the examples, type: "get-help HelpSample1 -examples".
    For more information, type: "get-help HelpSample1 -detailed".
    For technical information, type: "get-help HelpSample1 -full".
```

> [!NOTE]
> <span data-ttu-id="591de-117">Syntaxe pole a atributy parametru jsou automaticky generované pro vás prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="591de-117">Syntax fields and parameter attributes are automatically generated for you by PowerShell.</span></span>

## <a name="see-also"></a><span data-ttu-id="591de-118">Viz také</span><span class="sxs-lookup"><span data-stu-id="591de-118">See Also</span></span>

- [<span data-ttu-id="591de-119">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="591de-119">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="591de-120">Psaní, kompilace a použití konfigurace</span><span class="sxs-lookup"><span data-stu-id="591de-120">Write, Compile, and Apply a Configuration</span></span>](write-compile-apply-configuration.md)
- [<span data-ttu-id="591de-121">Přidání parametrů ke konfiguraci</span><span class="sxs-lookup"><span data-stu-id="591de-121">Add Parameters to a Configuration</span></span>](add-parameters-to-a-configuration.md)
