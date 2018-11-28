# Mirror of [asn1-packer.js](https://git.coolaj86.com/coolaj86/asn1-packer.js)

Official Repository: <https://git.coolaj86.com/coolaj86/asn1-packer.js>

# Bluecrypt ASN.1 Packer

An ASN.1 builder in less than 100 lines of Vanilla JavaScript,
part of the Bluecrypt suite.
<br>
<small>(< 150 with newlines and comments)</small>

# Features

| <100 lines of code | <1k gzipped | 1.8k minified | 3.3k with comments |

* [x] Complete ASN.1 packer
  * [x] Parses x.509 certificates
  * [x] PEM (base64-encoded DER)
* [x] VanillaJS, Zero Dependencies
  * [x] Browsers (even old ones)
  * [x] Online [Demo](https://coolaj86.com/demos/asn1-packer/)
  * [ ] Node.js (built, publishing soon)

# Demo

<https://coolaj86.com/demos/asn1-packer/>

<img border="1" src="https://i.imgur.com/phGeuMw.png" />

# Usage

```html
<script src="https://git.coolaj86.com/coolaj86/asn1-packer.js/raw/branch/master/asn1-packer.js"></script>
```

```js
'use strict';

var ASN1 = window.ASN1  // 62 lines
var Enc = window.Enc    // 27 lines
var PEM = window.PEM    //  6 lines

var arr = [
  0x30,
  [
    [ 0x30, [ [ 0x06, "2a8648ce3d0201" ], [ 0x06, "2a8648ce3d030107" ] ] ],
    [ 0x03, "04213d5258bc6c69c3e2139675ea3928a409fcffef39acc8e0c82a24ae78c37ede98fd89c0e00e74c997bb0a716ca9e0dca673dbb9b3fa72962255c9debcd218ca" ]
  ]
];

var hex = ASN1.pack(arr);
var buf = Enc.hexToBuf(hex);
var pem = PEM.packBlock({ type: "PUBLIC KEY", bytes: buf });

console.log(pem);
```

```
-----BEGIN PUBLIC KEY-----
MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEIT1SWLxsacPiE5Z16jkopAn8/+85
rMjgyCokrnjDft6Y/YnA4A50yZe7CnFsqeDcpnPbubP6cpYiVcnevNIYyg==
-----END PUBLIC KEY-----
```

### Simple Packing

All types are handled by the same rules except for Integer (0x02)
and Bit String (0x03), which require special padding.

This is sufficient for RSA and EC keypairs, and CSRs.

I don't know of any format for which it is not sufficient,
but if you find one I'd like to know about it.

### Zero Dependencies

> A little copying is better than a little dependency - Golang Proverbs by Rob Pike

Rather than requiring hundreds (or thousands) of lines of dependencies,
this library takes the approach of including from other libraries in its suite
to produce a small, focused file that does exactly what it needs to do.

# Legal

[Bluecrypt VanillaJS ASN.1 Packer](https://git.coolaj86.com/coolaj86/asn1-packer.js) |
MPL-2.0
