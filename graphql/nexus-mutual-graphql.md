# Nexus Mutual GraphQL (The Graph Subgraph)

## Description

Nexus Mutual exposes on-chain protocol data through a community-maintained subgraph
hosted on The Graph. The subgraph indexes Ethereum events emitted by Nexus Mutual
smart contracts and makes them queryable via GraphQL, covering cover purchases,
claims, staking, token events, and Minimum Capital Requirement (MCR) data.

The subgraph was originally developed by Protofire and tracks the full lifecycle of
decentralised insurance activity — from contract registration and cover issuance
through claim voting and payouts — as well as NXM token transfers, mints, burns,
and pool rebalancing events.

## Endpoint

```
https://thegraph.com/explorer/subgraph/protofire/nexus-mutual
```

The Graph hosted service endpoint (legacy):
```
https://api.thegraph.com/subgraphs/name/protofire/nexus-mutual
```

## Example Query

```graphql
{
  covers(first: 10, orderBy: created, orderDirection: desc) {
    id
    amount
    period
    expires
    premium
    premiumNXM
    status
    user {
      address
    }
    contract {
      address
    }
  }
}
```

## Schema Source

- Repository: https://github.com/protofire/nexus-mutual-subgraph
- Schema file: schema.graphql
- Subgraph explorer: https://thegraph.com/explorer/subgraph/protofire/nexus-mutual

## Key Types

| Type | Kind | Description |
|------|------|-------------|
| Contract | Entity | Insured smart contract with cover and stake counts |
| Cover | Entity | Individual insurance cover policy linked to a contract and user |
| Claim | Entity | Claim submitted against a cover, with voting state |
| Vote | Entity | Member vote (accept/deny) on a claim |
| Stake | Entity | NXM stake placed on a contract by a member |
| Commission | Entity | Commission earned on a staked contract |
| User | Entity | Protocol member with aggregated cover, stake, claim, and vote counts |
| Payout | Entity | Claim payout from the capital pool |
| Rebalancing | Entity | Pool rebalancing event |
| Token | Entity | NXM token aggregate stats (supply, burned, minted, transferred) |
| MCRData | Entity | Minimum Capital Requirement snapshot per block |
| ApprovalEvent | Entity | NXM token approval event |
| BurnEvent | Entity | NXM token burn event |
| MintEvent | Entity | NXM token mint event |
| TransferEvent | Entity | NXM token transfer event |
| BlackListedEvent | Entity | Address blacklisted from NXM transfers |
| WhiteListedEvent | Entity | Address whitelisted for NXM transfers |
| Accumulator | Entity | Running total metric |
| Counter | Entity | Count metric |

## Enumerations

- **CoverStatus**: `ACTIVE`, `CLAIM_ACCEPTED`, `CLAIM_DENIED`, `COVER_EXPIRED`, `CLAIM_SUBMITTED`, `REQUESTED`
- **ClaimStatus**: `CA_VOTE`, `MEMBER_VOTE`, `ACCEPTED`, `DENIED`
- **Verdict**: `ACCEPTED`, `DENIED`

## Interfaces

- **InsuranceAction**: base interface for Cover, Stake, Commission (id, contract, user)
- **PoolEvent**: base interface for Payout, Rebalancing
- **TokenEvent**: base interface for all NXM token events (id, token, account, block, timestamp, transaction)
- **Metric**: base interface for Accumulator, Counter

## Notes

- The subgraph tracks NXM token events via a fork of the ERC-20 token subgraph pattern
  maintained by Protofire.
- `MCRData` snapshots the capital pool health ratio (`mcrPercx100`) and ETH value
  (`mcrEtherx100`) at each MCR update block.
- Nexus Mutual's official documentation does not currently link to a first-party
  subgraph; the Protofire subgraph is the primary community indexer for this protocol.
- Cover and Stake entities implement the `InsuranceAction` interface and share `contract`
  and `user` foreign keys.
