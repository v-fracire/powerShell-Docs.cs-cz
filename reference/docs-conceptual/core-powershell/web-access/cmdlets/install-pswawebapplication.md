---
ms.topic: reference
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Install-PswaWebApplication
ms.openlocfilehash: 68455d9490f7d5c33c1a928ac262a76a78ad7128
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="install-pswawebapplication"></a>Install-PswaWebApplication

## <a name="synopsis"></a>STRUČNÝ OBSAH

Nakonfiguruje Windows PowerShell® Web Access webové aplikace ve službě IIS.

## <a name="syntax"></a>SYNTAXE

### <a name="default"></a>Výchozí
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a>POPIS

**Rutiny Install-PswaWebApplication** rutiny se konfiguruje Windows PowerShell Web Access webové aplikace. Tato rutina nainstaluje webovou aplikaci, přidruží ji k webovému serveru a volitelně vytváří pomocí certifikátu testovací SSL **useTestCertificate** parametr. Pro zabezpečení Správci webové důvodů neměli používat testovací certifikát pro produkční prostředí.

## <a name="parameters"></a>PARAMETRY

### <a name="-usetestcertificate"></a>-UseTestCertificate

Určuje, jestli je vytvořená testovací certifikát. Pokud tento parametr je nastaven na hodnotu true, pak tato rutina vytvoří testovací certifikát a nakonfiguruje webové aplikace Windows PowerShell Web Access k použití certifikátu pro požadavky HTTPS. Pokud tento parametr je nastaven na hodnotu false, pak je vytvořen žádný certifikát nebo vazby. Tuto hodnotu nastavte na hodnotu false, pokud se používá jiný certifikát pro Windows PowerShell Web Access.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | Hodnota TRUE                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-webapplicationnameltstringgt"></a>-WebApplicationName&lt;řetězec&gt;

Určuje název webové aplikace. Zobrazuje se jako poslední část Windows PowerShell Web Access URL.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | 1                                    |
| Výchozí hodnota                        | pswa                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-websitenameltstringgt"></a>-Zadaným hodnotám WebSiteName&lt;řetězec&gt;

Určuje název webového serveru (IIS) webu, na který chcete nainstalovat tuto webovou aplikaci Windows PowerShell Web Access.

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

Tato rutina neprodukuje žádný výstup.

## <a name="examples"></a>PŘÍKLADY

### <a name="example-1"></a>PŘÍKLAD 1

Tento příklad nainstaluje pomocí výchozí hodnoty pro webové aplikace PSWA **WebApplicationName** (*pswa*) a **zadaným hodnotám WebSiteName** (*výchozí web* ) parametry.

```
Install-PswaWebApplication
```

### <a name="example-2"></a>PŘÍKLAD 2

Tento příklad nainstaluje s testovací certifikát a pomocí výchozí hodnoty pro webové aplikace PSWA **WebApplicationName** a **zadaným hodnotám WebSiteName** parametry.

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a>Příbuzná témata

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
- [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)