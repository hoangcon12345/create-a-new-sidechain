# Transfer from the mainchain to the sidechain

## Check mainchain and sidechain balances
```
$ ./src/zen-cli -regtest getbalance
```

```
336.49984905
```

```
$ curl -X POST "http://127.0.0.1:9085/wallet/balance" -H "accept: application/json" -H "Content-Type: application/json"
```

```
{
  "result" : {
    "balance" : 100000000000
  }
}
```

```
$ ./src/zen-cli -regtest sc_send "9c31622802b4f079026bc16b13f52e51c8b5230b5d8a6346814bd8d4229fbaca" 50 "2ac103f1afba4c678ff58e1cfc4e015ebd40697518a61ae10750cd8f8d62505d"
```


```
1832fd94371fa8f146465f0311cd71c607ab0fe984b0989fb2f4d1cdf8fd8c75
```

## Generate block in the mainchain
```
$ ./src/zen-cli -regtest generate 1
```

```
[
  "0f0023537c70d72a62c6b8c78321cef0026957e61f8dd68a09970ba98c2c0d01"
]
```

Check block
```
$ ./src/zen-cli -regtest getblock "0f0023537c70d72a62c6b8c78321cef0026957e61f8dd68a09970ba98c2c0d01"
```

```
{
  "hash": "0f0023537c70d72a62c6b8c78321cef0026957e61f8dd68a09970ba98c2c0d01",
  "confirmations": 1,
  "size": 1254,
  "height": 222,
  "version": 3,
  "merkleroot": "97e8700cf902f193f30375a1031d5117546bc6cf89ae9d30b124f44b90f1881e",
  "scTxsCommitment": "d403d9bbe76d02b2b66edd2950c21aefd1243a68346ef16a375ce3af3f4b269a",
  "tx": [
    "fc272888dbbb63ca2102caf551460a125442e4170ef92805059578cd47889210",
    "1832fd94371fa8f146465f0311cd71c607ab0fe984b0989fb2f4d1cdf8fd8c75"
  ],
  "cert": [
  ],
  "time": 1610349843,
  "nonce": "00000a477f00349047b9fe81005b93fc373027f436d2c9c3b282803e0d810024",
  "solution": "09294cf75099d07b2025e992fd93b4a111ad312de6d9936a41dbac37cedc9095ed3a0557",
  "bits": "200f0f02",
  "difficulty": 1.000013172800801,
  "chainwork": "0000000000000000000000000000000000000000000000000000000000000ecf",
  "anchor": "59d2cde5e65c1414c32ba54f0fe4bdb3d67618125286e6a191317917c812c6d7",
  "valuePools": [
    {
      "id": "sprout",
      "monitored": true,
      "chainValue": 0.00000000,
      "chainValueZat": 0,
      "valueDelta": 0.00000000,
      "valueDeltaZat": 0
    }
  ],
  "previousblockhash": "040816a37ce4a1b2a89c3a9421b554aade5abe1d83aaed4b28a660c7f06b88fa"
}
```

## Sidechain block generation

Epoch
```
$ curl -X POST "http://127.0.0.1:9085/block/forgingInfo" -H "accept: application/json" -H "Content-Type: application/json"
```

```
{
  "result" : {
    "consensusSecondsInSlot" : 120,
    "consensusSlotsInEpoch" : 720,
    "bestEpochNumber" : 1,
    "bestSlotNumber" : 720
  }
}
```

Generate another one to start next epoch
```
$ curl -X POST "http://127.0.0.1:9085/block/generate" -H "accept: application/json"  -H "Content-Type: application/json" -d "{\"epochNumber\":2,\"slotNumber\":1}"
```

```
{
  "result" : {
    "blockId" : "9aa9a1248bc465ab59040866a3a07d68be78eccea3a94e7426da033cfaeef6e0"
  }
}
```

## Verify sidechain balance

```
$ curl -X POST "http://127.0.0.1:9085/wallet/balance" -H "accept: application/json"
```

```
{
  "result" : {
    "balance" : 105000000000
  }
}
```
