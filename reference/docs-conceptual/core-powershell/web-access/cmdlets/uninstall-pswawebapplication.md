---
ms.topic: reference
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Odinstalujte PswaWebApplication
ms.openlocfilehash: b2a3e4d584fd04ee49e1e6408dba39fd8bc555dc
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34221914"
---
# <a name="uninstall-pswawebapplication"></a>Odinstalujte PswaWebApplication

## <a name="synopsis"></a>STRUČNÝ OBSAH

Odinstaluje Windows PowerShell® webové aplikace.

## <a name="syntax"></a>SYNTAXE

### <a name="default"></a>Výchozí
```
Uninstall-PswaWebApplication [[-WebApplicationName] <String> ] [-DeleteTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a>POPIS

**Uninstall-PswaWebApplication** rutiny odinstaluje prostředí Windows PowerShell webové aplikace a odebere ze služby IIS na webu. Rutina neodinstaluje službu IIS, ani žádné další funkce, nainstalovat, protože byly požadované pro prostředí Windows PowerShell ke spuštění.

## <a name="parameters"></a>PARAMETRY

### <a name="-deletetestcertificate"></a>-DeleteTestCertificate

Označuje, že testovací certifikáty vytvořená pomocí **nainstalovat\_PswaWebApplication** rutiny (s **UseTestCertificate** parametr) se odstraní.
Testovací certifikát se stejným názvem jako vytvořené **rutiny Install-PswaWebApplication** rutiny se odebere.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | Hodnota TRUE                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-webapplicationname-ltstringgt"></a>-WebApplicationName &lt;řetězec&gt;

Určuje název webové aplikace odinstalovat.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | 1                                    |
| Výchozí hodnota                        | pswa                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-websitename-ltstringgt"></a>-Zadaným hodnotám WebSiteName &lt;řetězec&gt;

Určuje název webové stránky, kde je nainstalována webová aplikace.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | Výchozí web                     |
| Přijmout kanálový vstup?               | false                                |
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

Zobrazuje, co by se stalo při spuštění rutiny.
Rutina není spuštěna.

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

Tato rutina nemá žádný vstup.

## <a name="outputs"></a>VÝSTUPY

Tato rutina vrátí žádný výstup.

## <a name="examples"></a>PŘÍKLADY

### <a name="example-1"></a>PŘÍKLAD 1

Tento příkaz odinstaluje webové aplikace Windows PowerShell.
Tuto rutinu můžete odinstalovat webovou aplikaci Windows PowerShell, pokud jste nainstalovali pomocí výchozí hodnoty.

```PowerShell
Uninstall-PswaWebApplication
```

### <a name="example-2"></a>PŘÍKLAD 2

Tento příkaz odinstaluje webové aplikace Windows PowerShell a odstraní testovací certifikát přidružený k aplikaci.
Tuto rutinu můžete odinstalovat webovou aplikaci Windows PowerShell, pokud jste nainstalovali pomocí výchozí hodnoty a vytvořit testovací certifikát.

```PowerShell
Uninstall-PswaWebApplication -DeleteTestCertificate
```

### <a name="example-3-example-3-subheading"></a>Příklad 3 {#example-3 .subHeading}

Tento příkaz odinstaluje webové aplikace Windows PowerShell, pokud vlastní web a aplikaci se zadaly během instalace.
Příkaz odebere web s názvem *server* a aplikaci s názvem *TestApplication* a určuje, že testovací certifikáty přidružené aplikace jsou také odstraněny.

```
Uninstall-PswaWebApplication -WebApplicationName TestApplication -WebsiteName MySite -DeleteTestCertificate
```

## <a name="related-topics"></a>Příbuzná témata

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Rutiny Install-PswaWebApplication](install-pswawebapplication.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
- [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)