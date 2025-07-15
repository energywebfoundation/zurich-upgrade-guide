# EWC Zurich Upgrade

⚠️ **WARNING**: Read All steps before proceeding.

***This guide shares the necessary information to prepare EnergyWebChain node for the Zurich Upgrade, including required EVM client versions, the updated chainspec, and instruction to restart the node.***

## 1. Update Client Version 🔄

Ensure node is running a Zurich-compatible client version:
- **Nethermind** client → upgrade to `v1.31.13`
  - https://github.com/NethermindEth/nethermind/releases/tag/1.31.13

- **OpenEthereum** client → upgrade to `v3.3.5`
  - https://github.com/openethereum/openethereum/releases/tag/v3.3.5 

## 2. Download New Chainspec 📥

Download the latest EnergyWebChain chainspec:
  - [EnergyWebChain Chainspec](https://github.com/energywebfoundation/ewf-chainspec/blob/master/EnergyWebChain.json)

### 2.1 Verify SHA256 checksum ✔️

```
echo "d72895b9f2c5f6db3220c6bda22e543780b28d95a37ac570206a72a1d00896a6 EnergyWebChain.json" | sha256sum -c 
```

**Output should be**: `EnergyWebChain.json: OK`

### 2.2 Replace chainspec in appropriate directory:

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

In case chainspec file of your node is placed in different folder, please update it accordingly. 

  - For Nethermind client if you use flag based configuration:
`--config NETWORK_NAME` for energyweb it is `--config energyweb`
  
In this case it is also recommended to validate the checksum. 


## 3. Restart EVM Client 🚀

**Restart the EVM client service (Nethermind or OpenEthereum) to apply the upgrade changes.**