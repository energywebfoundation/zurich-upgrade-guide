# EWC Zurich Upgrade

⚠️ **WARNING**: Read All steps before proceeding.

***This guide shares the necessary information to prepare EnergyWebChain node for the Zurich Upgrade, including required EVM client versions, the updated chainspec, and instruction to restart the node.***

## 1. Update Client Version 🔄

Ensure node is running a Zurich-compatible client version:
- **Nethermind** client → upgrade to `v1.31.13`
  - https://github.com/NethermindEth/nethermind/releases/tag/1.31.13

- **OpenEthereum** client → upgrade to `v3.3.5`
  - https://github.com/openethereum/openethereum/releases/tag/v3.3.5 

## 2. Modify Chainspec file
  
If using Nethermind client with flag-based configuration, run `nethermind -c energyweb` to load the new chainspec automatically, then proceed to step **3**. Otherwise, if you are using OpenEthereum or have customly placed chainspec please follow **2.1–2.3** for manual updates.

### 2.1 Manual download of new Chainspec 📥

Download the latest EnergyWebChain chainspec:
  - [EnergyWebChain Chainspec](https://github.com/energywebfoundation/ewf-chainspec/blob/master/EnergyWebChain.json)

### 2.2 Verify SHA256 checksum ✔️

```
echo "5dedb25779a1f2d230fe8658651547e602076967b71f14d14fb984dbf38a9b3b EnergyWebChain.json" | sha256sum -c -
```

**Output should be**: `EnergyWebChain.json: OK`

### 2.3 Replace chainspec in appropriate directory:

  - For OpenEthereum client chainspec file normally can be found in config folder:
```bash
  ├── config
    ├── chainspec.json
```

  - For Nethermind client:
```bash
  ├── chainspec
    └── energyweb.json
```

In case chainspec file of your node is specified via a custom path, please update it in apropriate place accordingly. 


## 3. Restart EVM Client 🚀

**Restart the EVM client service (Nethermind or OpenEthereum) to apply the upgrade changes.**

## 4. Verify Upgrade ✅

### 4.1 Check Client Version on running node

```bash
curl -X POST -H "Content-Type: application/json" \
  --data '{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":1}' \
  http://localhost:8545
```

```bash
# Resoinse of running node of OpenEthereum
{"jsonrpc":"2.0","result":"OpenEthereum//v3.3.5-stable/x86_64-linux-musl/rustc1.59.0","id":1}

# Resoinse of running node of Nethermind
{"jsonrpc":"2.0","result":"Nethermind/v1.31.13+1b548727/linux-x64/dotnet9.0.7","id":1}

```

### 4.2 Network Sync Status ♾️

```bash
# Check sync status
curl -X POST -H "Content-Type: application/json" \
    --data '{"jsonrpc":"2.0","method":"eth_syncing","params":[],"id":1}' \
    http://localhost:8545
```

If the response is `false`, the node is fully synced.
If it returns an object with `startingBlock`, `currentBlock`, and `highestBlock`, the node is still syncing.