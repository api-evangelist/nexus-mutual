# Nexus Mutual

Nexus Mutual is a decentralized insurance protocol built on Ethereum that allows members to share risk through a discretionary mutual structure. Operating since 2019, the protocol has provided over 10,000 covers protecting more than $6 billion in crypto assets against smart contract hacks, custody failure, slashing events, depeg occurrences, and bespoke protocol risks, backed by $100M+ in on-chain reserves managed by Collective Risk Services CIC.

## APIs

The Nexus Mutual **Cover Router REST API** (`https://api.nexusmutual.io/v2`) is a public, unauthenticated API that enables third-party developers and integrators to build cover purchase flows directly on top of the Nexus Mutual protocol. Key endpoints include:

- `GET /v2/quote` - Fetch optimal premium price and pool allocation for a cover purchase
- `GET /v2/capacity` - Query available capacity across all cover products
- `GET /v2/capacity/{productId}` - Per-product capacity with optional per-pool breakdown
- `GET /v2/capacity/pools/{poolId}` - All product capacities within a specific staking pool
- `GET /v2/capacity/pools/{poolId}/products/{productId}` - Single product capacity in a pool
- `GET /v2/products` - Full catalogue of 245+ cover products with pricing and metadata

## Links

- **Website:** https://nexusmutual.io
- **Application:** https://app.nexusmutual.io
- **Documentation:** https://docs.nexusmutual.io
- **API Docs (Swagger):** https://api.nexusmutual.io/v2/api/docs/
- **SDK:** https://sdk.nexusmutual.io
- **GitHub:** https://github.com/NexusMutual
- **Cover Router Repo:** https://github.com/NexusMutual/cover-router
- **Bug Bounty:** https://immunefi.com/bounty/nexusmutual/
- **Analytics:** https://dune.com/nexus_mutual
- **Terms of Use:** https://v2.nexusmutual.io/assets/Terms-of-Use.pdf
- **Privacy Policy:** https://v2.nexusmutual.io/assets/Privacy-Policy.pdf
