# BIP44
[![Go Report Card](https://goreportcard.com/badge/github.com/algoGuy/EasyMIDI)](https://goreportcard.com/report/github.com/algoGuy/EasyMIDI)
[![GoDoc](https://godoc.org/github.com/algoGuy/EasyMIDI?status.svg)](https://godoc.org/github.com/algoGuy/EasyMIDI)

A Golang implementation of the BIP44 for Hierarchical Deterministic (HD) addresses.

Released under the terms of the [MIT LICENSE](LICENSE).

## Should I use this in production?
This library is in very early stages. Please be aware that some bugs may exist. 

## Can I trust this code?
> Do not trust. Verify.

We recommend every user of this library audit and verify any underlying code for its validity and suitability.

## Installation
```bash 
go get -u ####TODO 
```

## Usage

### New 24-word Mnemonic and Seed
```golang
mnemonic, _ := bitcoin_address.NewMnemonic(256)
seedBytes := m.NewSeed("my password")
```

### Master key From Seed Hex
```golang
xKey, _ := bitcoin_address.NewKeyFromSeedHex("your secret seed in hex format", bitcoin_address.MAINNET)
```

### Master key From Seed bytes
```golang
xKey, _ := bitcoin_address.NewKeyFromSeedBytes(seedBytes, bitcoin_address.MAINNET)
```

### From base58-encoded Extended Key
```golang
ak, _ := bitcoin_address.NewAccountKeyFromXKey(xPubKey)

externalAddress, _ := accountKey.DeriveP2PKAddress(bitcoin_address.ExternalChangeType, 0, bitcoin_address.MAINNET)
internalAddress, _ := accountKey.DeriveP2PKAddress(bitcoin_address.InternalChangeType, 0, bitcoin_address.MAINNET)
```

### BIP44

| coin    | account | chain    | address | path                      |
| ------- | ------- | -------- | ------- | ------------------------- |
| Bitcoin | first   | external | first   | m / 44' / 0' / 0' / 0 / 0 |

```golang 
xKey, _ := bitcoin_address.NewKeyFromSeedHex("your secret seed in hex format", bitcoin_address.MAINNET)
accountKey, _ := xKey.BIP44AccountKey(bitcoin_address.BitcoinCoinType, 0, true)

externalAddress, _ := accountKey.DeriveP2PKAddress(bitcoin_address.ExternalChangeType, 0, bitcoin_address.MAINNET)
```

---

| coin    | account | chain    | address | path                      |
| ------- | ------- | -------- | ------- | ------------------------- |
| Bitcoin | first   | external | second   | m / 44' / 0' / 0' / 0 / 1 |

```golang 
xKey, _ := bitcoin_address.NewKeyFromSeedHex("your secret seed in hex format", bitcoin_address.MAINNET)
accountKey, _ := xKey.BIP44AccountKey(bitcoin_address.BitcoinCoinType, 0, true)

externalAddress, _ := accountKey.DeriveP2PKAddress(bitcoin_address.ExternalChangeType, 1, bitcoin_address.MAINNET)
```

---

m / purpose' / coin_type' / account' / change / address_index

| coin            | account  | chain    | address | path                      |
| --------------- | -------- | -------- | ------- | ------------------------- |
| Bitcoin Testnet | second   | internal | first   | m / 44' / 1' / 1' / 1 / 0 |

```golang 
xKey, _ := bitcoin_address.NewKeyFromSeedHex("your secret seed in hex format", bitcoin_address.TESTNET3)
accountKey, _ := xKey.BIP44AccountKey(bitcoin_address.TestnetCoinType, 1, true)

externalAddress, _ := accountKey.DeriveP2PKAddress(bitcoin_address.InternalChangeType, 0, bitcoin_address.TESTNET3)
```



## TODO
- [ ] Unit Tests
- [ ] Create GoDoc
- [ ] Stellar
- [ ] Ethereum
