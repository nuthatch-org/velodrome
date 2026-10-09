# velodrome

A [nuthatch](https://github.com/nuthatch-org/nuthatch) nest: **Velodrome on Optimism**.

Aerodrome's predecessor, and the same ve(3,3) shape.

One binary, one config file, no graph-node, no gateway, no query fees.

## What it indexes

**Chain:** `optimism`. **1 contract**, **12 tables**.

| alias | address |
|---|---|
| `factory` | `0xf1046053aa5682b4f9a81b5481394da16be5ff5a` |

## Verified

Indexed blocks **155,710,387 to 155,909,798** and sealed **9 events**. Every table below is generated from the vendored ABIs, and the run above is what this nest actually decoded, not an estimate.

## Read this before trusting it

- This nest is `aerodrome` with six values changed - chain, chain_id, factory address, two start blocks and the endpoint. The ABIs are **byte-identical**, because Aerodrome is a true code fork rather than a reimplementation.
- The verification window discovered 7 brand-new pools with no trades yet. Correctness was confirmed separately: the busiest emitter of this pool `Swap` shape on Optimism returns `factory()` equal to this nest's factory.

## Run it

```sh
nuthatch init --from https://github.com/nuthatch-org/velodrome
cd velodrome
nuthatch dev --dir . --backfill 50000 --seal-direct
nuthatch sql --dir . "SELECT count(*) FROM \"factory__pool_created\""
```

The endpoint in `nuthatch.toml` is keyless and public, so this file is publishable: a `nuthatch.toml` is pinned into the nest's content address and must never carry a credential. It is enough to follow the tip. A **backfill** wants archive depth it may not have: pass your own with `--rpc`, and check it first with `nuthatch doctor --rpc <url>`.

## Tables

```
factory__pool_created
factory__set_custom_fee
factory__set_fee_manager
factory__set_pause_state
factory__set_pauser
factory__set_voter
pool__burn
pool__claim
pool__fees
pool__mint
pool__swap
pool__sync
```
