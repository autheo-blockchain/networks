# Autheo Chain Config

This repository contains official configuration files for connecting to Autheo networks.

## Structure

```
mainnet/    # Mainnet configuration
```

## Common Parameters

| Parameter | Value |
|---|---|
| Native Denom | `aauth` (1 THEO = 10^18 aauth) |
| Binary | `autheod` |
| Bech32 Prefix | `autheo` |

## Files

Each network directory contains:

| File | Description |
|---|---|
| `chain-id` | Chain identifier |
| `genesis.json` | Genesis file — required to join the network |
| `persistent_peers.txt` | Persistent peer addresses for `config.toml` |
| `seeds.txt` | Seed node addresses for peer discovery |

## Joining a Network

Replace `<network>` with `mainnet` in the commands below.

**Step 1 — Initialize your node:**
```bash
autheod init <moniker> --chain-id $(cat <network>/chain-id) --home ~/.autheo
```

**Step 2 — Copy genesis:**
```bash
cp <network>/genesis.json ~/.autheo/config/genesis.json
```

**Step 3 — Set persistent peers in `~/.autheo/config/config.toml`:**
```bash
persistent_peers = "$(cat <network>/persistent_peers.txt)"
```

**Step 4 — Set minimum gas price in `~/.autheo/config/app.toml`:**
```toml
minimum-gas-prices = "10000000000000aauth"
```

**Step 5 — Start the node:**
```bash
autheod start --home ~/.autheo
```
