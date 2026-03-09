<div align="center">

<img src="https://nostr-wot.com/icon.svg" alt="Nostr WoT" width="80" />

# Nostr Web of Trust

**Open infrastructure for trust-based filtering on Nostr.**

Your identity, your trust network, your wallet — one ecosystem.

[![License: MIT](https://img.shields.io/badge/License-MIT-a78bfa.svg)](https://opensource.org/licenses/MIT)
[![Chrome Web Store](https://img.shields.io/badge/Chrome_Web_Store-Extension-4ade80.svg)](https://chromewebstore.google.com/detail/nostr-wot-extension/gfmefgdkmjpjinecjchlangpamhclhdo)
[![npm](https://img.shields.io/npm/v/nostr-wot-sdk?color=facc15&label=SDK)](https://www.npmjs.com/package/nostr-wot-sdk)
[![Website](https://img.shields.io/badge/Website-nostr--wot.com-8b5cf6.svg)](https://nostr-wot.com)

</div>

---

## What is Web of Trust?

Nostr has no central authority to filter spam or verify identity. Web of Trust solves this by measuring **social distance** — how many hops separate you from someone in the follow graph.

```
You → follows            → 1 hop  (trusted)
         → their follows → 2 hops (known)
              → their follows → 3+ hops (probably noise)
```

No blocklists. No moderators. Just your social graph doing the filtering.

---

## Projects

### [Browser Extension](https://github.com/nostr-wot/nostr-wot-extension)

A complete Nostr identity provider, Lightning wallet, and Web of Trust engine — all in one extension.

| Feature | Description |
|---|---|
| **NIP-07 Signer** | Sign events, encrypt messages (NIP-04 & NIP-44) on any Nostr client |
| **Encrypted Vault** | AES-256-GCM key storage with auto-lock and secure backup |
| **Multi-Account** | HD derivation, watch-only, remote signer (NIP-46) |
| **Lightning Wallet** | Built-in wallet for zaps via NWC, LNbits, or one-click setup |
| **Trust Badges** | Color-coded trust indicators injected into Nostr sites |
| **WebLN Provider** | Sites can request payments through `window.webln` |
| **6 Languages** | EN, ES, PT, DE, FR, IT |

Works on Chrome, Brave, Edge, Opera, and Firefox.

---

### [JavaScript SDK](https://github.com/nostr-wot/nostr-wot-sdk)

Integrate Web of Trust into any JavaScript or TypeScript application.

```bash
npm install nostr-wot-sdk
```

```js
import { NostrWoT } from 'nostr-wot-sdk'

const wot = new NostrWoT({ userPubkey: '...' })
const score = await wot.getTrustScore(pubkey)
```

Extension-first design — uses the browser extension when available, falls back to the Oracle. Includes React hooks (`WoTProvider`, `useWoT`).

---

### [WoT Oracle](https://github.com/nostr-wot/nostr-wot-oracle)

High-performance Rust backend that indexes the entire Nostr follow graph and serves trust queries via REST API.

- 10,000+ queries/second with sub-millisecond cached responses
- Bidirectional BFS across millions of nodes
- 100% self-hostable — run your own instance for full control
- Public instance: [wot-oracle.mappingbitcoin.com](https://wot-oracle.mappingbitcoin.com)

```bash
curl "https://wot-oracle.mappingbitcoin.com/distance?from=PUBKEY_A&to=PUBKEY_B"
```

---

## API at a Glance

```js
// Extension — client-side
await window.nostr.wot.getDistance(pubkey)
await window.nostr.wot.getTrustScore(pubkey)

// SDK — client or server
const wot = new NostrWoT({ userPubkey: '...' })
await wot.getTrustScore(pubkey)
```

```bash
# Oracle — REST
GET  /distance?from={pubkey}&to={pubkey}
POST /distance/batch
GET  /stats
```

---

## Use Cases

- Spam filtering without centralized blocklists
- Trust scores for marketplaces and reviews
- Smart notifications prioritized by social proximity
- Content discovery surfacing notes from your extended network

---

## Built With Nostr WoT

| Project | Description |
|---|---|
| [mappingbitcoin.com](https://mappingbitcoin.com) | Bitcoin merchant directory with WoT-based trust filtering |

---

## Supporters

| Organization | Website |
|---|---|
| Dandelion Labs | [dandelionlabs.io](https://dandelionlabs.io) |
| MappingBitcoin | [mappingbitcoin.com](https://mappingbitcoin.com) |

---

## Get Started

1. [Install the extension](https://chromewebstore.google.com/detail/nostr-wot-extension/gfmefgdkmjpjinecjchlangpamhclhdo) from the Chrome Web Store
2. Set up your account — create keys, import nsec, or connect via NIP-46
3. Browse Nostr — your identity and trust network follow you everywhere

Everything is open source under the [MIT License](https://opensource.org/licenses/MIT). Run your own oracle, fork the extension, build trust infrastructure for your community.

---

## Links

- [nostr-wot.com](https://nostr-wot.com)
- [Extension](https://github.com/nostr-wot/nostr-wot-extension)
- [SDK](https://github.com/nostr-wot/nostr-wot-sdk)
- [Oracle](https://github.com/nostr-wot/nostr-wot-oracle)
- [Docs](https://nostr-wot.com/docs)
