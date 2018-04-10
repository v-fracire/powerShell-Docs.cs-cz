---
description: ''
ms.topic: article
ms.prod: powershell
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: odebrat pswaauthorizationrule
ms.technology: powershell
ms.openlocfilehash: 28dbfe84827d6ccb99dce1ebb520cae66dc8c50e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="remove-pswaauthorizationrule"></a>Remove-PswaAuthorizationRule

## <a name="synopsis"></a>STRUČNÝ OBSAH

Odebere zadané autorizační pravidlo z Windows PowerShell® Web Access.

## <a name="syntax"></a>SYNTAX

### <a name="id"></a>Id
```
Remove-PswaAuthorizationRule [-Id] <Int32[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

### <a name="rule"></a>Pravidlo
```
Remove-PswaAuthorizationRule [-Rule] <PswaAuthorizationRule[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a>POPIS

Odebere zadané autorizační pravidlo z Windows PowerShell Web Access.

## <a name="parameters"></a>PARAMETRY

### <a name="-force"></a>-Force

Spustí se bez zobrazení výzvy k potvrzení. Ve výchozím nastavení rutina požádá o potvrzení, než budete pokračovat.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-id-ltint32gt"></a>-Id &lt;Int32\[\]&gt;

Určuje identifikátory (ID) jeden nebo více pravidel odebrat.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | 2                                    |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | Hodnotu true (ByValue, ByPropertyName)       |
| Přijímat zástupné znaky?          | false                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a>-Pravidla &lt;PswaAuthorizationRule\[\]&gt;

Určuje pravidla k odebrání.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | 2                                    |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | Hodnotu true (ByValue)                       |
| Přijímat zástupné znaky?          | false                                |

### <a name="-confirm"></a>-Confirm

Před spuštěním rutiny zobrazí výzvu k potvrzení.

|||
|-|-|
| Povinné?                            | false                                |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | false                                |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-whatif"></a>-WhatIf

Zobrazuje, co by se stalo při spuštění rutiny. Rutina není spuštěna.

|||
|-|-|
| Povinné?                            | false                                |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | false                                |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="ltcommonparametersgt"></a>&lt;CommonParameters&gt;

Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.
Další informace najdete v tématu [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="inputs"></a>VSTUPY

### <a name="int"></a>celá čísla\[\]

Tato rutina přijímá pole celých čísel nebo pole objektů PswaAuthorizationRule.

### <a name="pswaauthorizationrule"></a>PswaAuthorizationRule\[\]

Tato rutina přijímá pole celých čísel nebo pole objektů PswaAuthorizationRule.

## <a name="outputs"></a>VÝSTUPY

Tato rutina neprodukuje žádný výstup.

## <a name="examples"></a>PŘÍKLADY

### <a name="example-1"></a>PŘÍKLAD 1

V tomto příkladu odebere autorizační pravidlo s ID *2*.

```
Remove-PswaAuthorizationRule –Id 2
```

### <a name="example-2-example-2-subheading"></a>Příklad 2 {.subHeading #example-2}

Tento příklad odebere všechna autorizační pravidla a také vyžaduje potvrzení uživatelem.

```
Get-PswaAuthorizationRule | Remove-PswaAuthorizationRule -Confirm
```

## <a name="related-topics"></a>Příbuzná témata

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Rutiny Install-PswaWebApplication](install-pswawebapplication.md)
- [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)