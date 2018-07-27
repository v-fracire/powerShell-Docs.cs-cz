---
ms.topic: reference
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Install-PswaWebApplication
ms.openlocfilehash: 29e074b75eeb387640831229c63142e6dd5e991a
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268295"
---
# <a name="install-pswawebapplication"></a>Install-PswaWebApplication

## <a name="synopsis"></a>SOUHRN

Nakonfiguruje Windows PowerShell Web Accessu webové aplikace ve službě IIS.

## <a name="syntax"></a>SYNTAXE

### <a name="default"></a>Výchozí
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a>POPIS

**Rutiny Install-PswaWebApplication** rutina nakonfiguruje webové aplikace Windows PowerShell Web Accessu.
Tato rutina nainstaluje webovou aplikaci, přidruží ji k webu a volitelně vytváří certifikát SSL test pomocí **useTestCertificate** parametru. Pro zabezpečení správcům webových důvodů nepoužívejte testovací certifikát pro produkční prostředí.

## <a name="parameters"></a>PARAMETRY

### <a name="-usetestcertificate"></a>-UseTestCertificate

Určuje, že se vytvoří testovací certifikát. Pokud tento parametr je nastaven na hodnotu true, pak tato rutina vytvoří testovací certifikát a nakonfiguruje webovou aplikaci Windows PowerShell Web Access k použití certifikátu pro požadavky HTTPS. Pokud tento parametr je nastaven na hodnotu false, pak je vytvořen žádný certifikát nebo vazby. Tuto hodnotu nastavte na hodnotu false, pokud jiný certifikát se používá pro Windows PowerShell Web Accessu.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | s názvem                                |
| Výchozí hodnota                        | Hodnota TRUE                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-webapplicationname"></a>-WebApplicationName

Určuje název pro vaši webovou aplikaci. Zobrazí se jako poslední část Windows PowerShell Web Access URL.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | 1                                    |
| Výchozí hodnota                        | pswa                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-websitename"></a>-Zadaným hodnotám WebSiteName

Určuje název webového serveru (IIS) webu, na které chcete nainstalovat tuto webovou aplikaci Windows PowerShell Web Accessu.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | s názvem                                |
| Výchozí hodnota                        | Výchozí web                     |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-confirm"></a>-Confirm

Před spuštěním rutiny zobrazí výzvu k potvrzení.

|||
|-|-|
| Povinné?                            | false                                |
| Pozice?                            | s názvem                                |
| Výchozí hodnota                        | false                                |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-whatif"></a>-WhatIf

Zobrazuje, co by se stalo při spuštění rutiny.
Rutina není spuštěna.

|||
|-|-|
| Povinné?                            | false                                |
| Pozice?                            | s názvem                                |
| Výchozí hodnota                        | false                                |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="ltcommonparametersgt"></a>&lt;CommonParameters&gt;

Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable. Další informace najdete v tématu [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="inputs"></a>VSTUPY

Tato rutina nemá žádný vstup.

## <a name="outputs"></a>VÝSTUPY

Tato rutina negeneruje žádný výstup.

## <a name="examples"></a>PŘÍKLADY

### <a name="example-1"></a>PŘÍKLAD 1

Tento příklad nainstaluje PSWA webovou aplikaci pomocí výchozích hodnot pro **WebApplicationName** (*pswa*) a **zadaným hodnotám WebSiteName** (*výchozí webový server* ) parametry.

```
Install-PswaWebApplication
```

### <a name="example-2"></a>PŘÍKLAD 2

Tento příklad nainstaluje webovou aplikaci PSWA testovací certifikát a pomocí výchozích hodnot pro **WebApplicationName** a **zadaným hodnotám WebSiteName** parametry.

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a>Příbuzná témata

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
- [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)