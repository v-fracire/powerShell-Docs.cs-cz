---
ms.topic: reference
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Get-PswaAuthorizationRule
ms.openlocfilehash: d61dce18e87311d7d815a689ba675db44aaec3cb
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188904"
---
# <a name="get-pswaauthorizationrule"></a>Get-PswaAuthorizationRule

## <a name="synopsis"></a>STRUČNÝ OBSAH

Vrací sadu autorizačních pravidel Windows PowerShell® Web Access.

## <a name="syntax"></a>Syntaxe

### <a name="id"></a>ID
```
Get-PswaAuthorizationRule [[-Id] <Int32[]> ] [ <CommonParameters>]
```

### <a name="name"></a>Název
```
Get-PswaAuthorizationRule [-RuleName] <String[]> [ <CommonParameters>]
```

## <a name="description"></a>POPIS

**Get-PswaAuthorizationRule** rutina vrací sadu autorizačních pravidel Windows PowerShell® Web Access.
Pokud **Id** parametr ani **RuleName** parametr zadaný, bude tato rutina obsahuje seznam všech pravidel. **Id** parametr můžete použít k filtrování výsledků.

## <a name="parameters"></a>PARAMETRY

### <a name="-idltint32gt"></a>-Id&lt;Int32\[\]&gt;

Určuje identifikátory (ID) pravidla, která by měl získat tuto rutinu. Pokud nejsou zadány žádné ID, tato rutina vrátí všechna autorizační pravidla.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | 2                                    |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | Hodnotu true (ByValue, ByPropertyName)       |
| Přijímat zástupné znaky?          | false                                |

### <a name="-rulenameltstringgt"></a>-RuleName&lt;řetězec\[\]&gt;

Určuje názvy autorizačních pravidel pro načtení. Tento parametr vrátí všechna pravidla, která přesně shodovat s názvy pravidel řetězců v toto pole.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | 2                                    |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | Hodnotu true (ByValue, ByPropertyName)       |
| Přijímat zástupné znaky?          | false                                |

### <a name="ltcommonparametersgt"></a>&lt;CommonParameters&gt;

Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.
Další informace najdete v tématu [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="inputs"></a>VSTUPY

### <a name="int"></a>celá čísla\[\]

Tato rutina akceptuje jako vstupní pole celá čísla nebo pole řetězcové hodnoty.

### <a name="string"></a>Řetězec\[\]

Tato rutina akceptuje jako vstupní pole celá čísla nebo pole řetězcové hodnoty.

## <a name="outputs"></a>VÝSTUPY

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]

Tato rutina vytvoří objekt PswaAuthorizationRule jako výstup.


## <a name="examples"></a>PŘÍKLADY

### <a name="example-1"></a>PŘÍKLAD 1

Tento příklad načte všechna pravidla.

```PowerShell
    PS C:\> Get-PswaAuthorizationRule
```

### <a name="example-2"></a>PŘÍKLAD 2

Tento příklad načte pravidlo s ID *2*.

```PowerShell
    PS C:\> Get-PswaAuthorizationRule –Id 2
```

### <a name="example-3-example-3-subheading"></a>Příklad 3 {#example-3 .subHeading}

Tento příklad ukazuje, jak rutina umožňuje hodnotu z kanálu.
Id pravidla a název pravidla se předávají v této rutině.

```PowerShell
    PS C:\> "rule1",0 | Get-PswaAuthorizationRule
```

## <a name="related-topics"></a>Příbuzná témata

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
- [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)
- [Rutiny Install-PswaWebApplication](install-pswawebapplication.md)