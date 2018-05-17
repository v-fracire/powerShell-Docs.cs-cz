---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 14208e3b5d5c2fef80fa42a87cc00aeee81bd042
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="cryptographic-message-syntax-cms-cmdlets"></a>Kryptografické rutiny zpráva syntaxe (CMS)

Rutiny Cryptographic Message Syntax podporují šifrování a dešifrování obsahu pomocí formátu standard sdružení IETF pro kryptograficky ochranu zprávy, jak je uvedeno ve [RFC5652](https://tools.ietf.org/html/rfc5652).

```powershell
Get-CmsMessage [-Content] <string>
Get-CmsMessage [-Path] <string>
Get-CmsMessage [-LiteralPath] <string>
Protect-CmsMessage [-To] <CmsMessageRecipient[]> [-Content] <string> [[-OutFile] <string>]
Protect-CmsMessage [-To] <CmsMessageRecipient[]> [-Path] <string> [[-OutFile] <string>]
Protect-CmsMessage [-To] <CmsMessageRecipient[]> [-LiteralPath] <string> [[-OutFile] <string>]
Unprotect-CmsMessage [-EventLogRecord] <EventLogRecord> [[-To] <CmsMessageRecipient[]>] [-IncludeContext]
Unprotect-CmsMessage [-Content] <string> [[-To] <CmsMessageRecipient[]>] [-IncludeContext]
Unprotect-CmsMessage [-Path] <string> [[-To] <CmsMessageRecipient[]>] [-IncludeContext]
Unprotect-CmsMessage [-LiteralPath] <string> [[-To] <CmsMessageRecipient[]>] [-IncludeContext]
```

Standardní CMS šifrování implementuje kryptografie využívající veřejného klíče, kde klíče použitý k šifrování obsahu ( *veřejný klíč*) a klíče, které slouží k dešifrování obsahu ( *privátní klíč*) jsou oddělené.

Veřejný klíč je možné sdílet široce a není citlivá data. Pokud je tento veřejný klíč je šifrován žádný obsah, můžete ho dešifrovat jenom váš privátní klíč. Další informace najdete v tématu [Public key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography).

Rozpoznat v prostředí PowerShell, šifrovací certifikáty vyžadovat identifikátor jedinečný použití klíče (EKU) identifikovat jako certifikáty šifrování dat (např. identifikátory "podepisování kódu', 'šifrované pošty).

Tady je příklad vytvoření certifikát, který je vhodný pro šifrování dokumentu:

```powershell
(Change the text in **Subject** to your name, email, or other identifier), and put in a file (i.e.: DocumentEncryption.inf):
[Version]
Signature = "$Windows NT$"
[Strings]
szOID\_ENHANCED\_KEY\_USAGE = "2.5.29.37"
szOID\_DOCUMENT\_ENCRYPTION = "1.3.6.1.4.1.311.80.1"
[NewRequest]
Subject = "<cn=me@somewhere.com>"
MachineKeySet = false
KeyLength = 2048
KeySpec = AT\_KEYEXCHANGE
HashAlgorithm = Sha1
Exportable = true
RequestType = Cert
KeyUsage = "CERT\_KEY\_ENCIPHERMENT\_KEY\_USAGE | CERT\_DATA\_ENCIPHERMENT\_KEY\_USAGE"
ValidityPeriod = "Years"
ValidityPeriodUnits = "1000"
[Extensions]
%szOID\_ENHANCED\_KEY\_USAGE% = "{text}%szOID\_DOCUMENT\_ENCRYPTION%"
```

Pak spusťte tyto příkazy:
```powershell
certreq -new DocumentEncryption.inf DocumentEncryption.cer
```

A teď můžete šifrování a dešifrování obsahu:

```powershell
$protected = "Hello World" | Protect-CmsMessage -To "\*me@somewhere.com\*[](mailto:*leeholm@microsoft.com*)"
$protected
-----BEGIN CMS-----
MIIBqAYJKoZIhvcNAQcDoIIBmTCCAZUCAQAxggFQMIIBTAIBADA0MCAxHjAcBgNVBAMMFWxlZWhv
bG1AbWljcm9zb2Z0LmNvbQIQQYHsbcXnjIJCtH+OhGmc1DANBgkqhkiG9w0BAQcwAASCAQAnkFHM
proJnFy4geFGfyNmxH3yeoPvwEYzdnsoVqqDPAd8D3wao77z7OhJEXwz9GeFLnxD6djKV/tF4PxR
E27aduKSLbnxfpf/sepZ4fUkuGibnwWFrxGE3B1G26MCenHWjYQiqv+Nq32Gc97qEAERrhLv6S4R
G+2dJEnesW8A+z9QPo+DwYU5FzD0Td0ExrkswVckpLNR6j17Yaags3ltNVmbdEXekhi6Psf2MLMP
TSO79lv2L0KeXFGuPOrdzPAwCkV0vNEqTEBeDnZGrjv/5766bM3GW34FXApod9u+VSFpBnqVOCBA
DVDraA6k+xwBt66cV84OHLkh0kT02SIHMDwGCSqGSIb3DQEHATAdBglghkgBZQMEASoEEJbJaiRl
KMnBoD1dkb/FzSWAEBaL8xkFwCu0e1ZtDj7nSJc=
-----END CMS-----

$protected | Unprotect-CmsMessage
Hello World
```

Libovolný parametr typu **CMSMessageRecipient** podporuje identifikátory v následujících formátech:
- Certifikát skutečné (jako je načtena z poskytovatel certifikátu)
- Cesta k souboru, který obsahuje certifikát
- Cesta k adresáři, který obsahuje certifikát
- Kryptografický otisk certifikátu (použije pro vyhledávání v úložišti certifikátů)
- Název subjektu certifikátu (použije pro vyhledávání v úložišti certifikátů)

Chcete-li zobrazit dokumentu šifrovací certifikáty ve zprostředkovateli certifikátu, můžete použít **- DocumentEncryptionCert** dynamický parametr:

```powershell
dir -DocumentEncryptionCert
```
