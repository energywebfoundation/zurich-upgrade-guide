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
  
  - For Nethermind client, if you use flag based configuration, `nethermind -c energyweb` command will load new chainspec automatically. Once done you can proceed to point **3**
  - If you use OpenEtherum client or have custom chainspec placement proceed with manual chainspec modification (points ***2.1-2.3***).

## 2.1 Manual download of new Chainspec 📥

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

In case chainspec file of your node is placed in different folder, please update it accordingly. 


## 3. Restart EVM Client 🚀

**Restart the EVM client service (Nethermind or OpenEthereum) to apply the upgrade changes.**
