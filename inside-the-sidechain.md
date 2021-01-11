## Transfer inside the sidechain

## Create a new direction to transfer

```
$ curl -X POST "http://127.0.0.1:9085/wallet/createPrivateKey25519" -H "accept: application/json"
```

```

{
  "result" : {
    "proposition" : {
      "publicKey" : "c6869f3aa8928fe57c24d41ceaca6a1fc57a6bdfdf309dc2de7552790c514bcc"
    }
  }
}
```

## Transaction
```
$ curl -X POST "http://127.0.0.1:9085/transaction/sendCoinsToAddress" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"outputs\":[{\"publicKey\":\"c6869f3aa8928fe57c24d41ceaca6a1fc57a6bdfdf309dc2de7552790c514bcc\",\"value\":1000000000}],\"fee\":0}"
```

```
{
  "result" : {
    "transactionId" : "7d91b2dce6488e007e73291820ad9eba19cceea0c6432a425c701fb8481a1c53"
  }
}
```

## Generate the next block
Block 2, epoch 2

```
$ curl -X POST "http://127.0.0.1:9085/block/generate" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"epochNumber\":2,\"slotNumber\":2}"
```

```
{
  "result" : {
    "blockId" : "8212da2852b492f6207575ff6f40a89455686e500cb9c85f94483861dc4735ab"
  }
}
```

## Check all boxes
```
$ curl -X POST "http://127.0.0.1:9085/wallet/allBoxes" -H "accept: application/json" -H "Content-Type: application/json"
```

```
{
  "result" : {
    "boxes" : [ {
      "nonce" : 5812663359062504556,
      "id" : "2554ee10f4d7d89a3db905e5aabd4ce02c4398d98144ef94bf39124a7ff0c85c",
      "typeId" : 3,
      "blockSignProposition" : {
        "publicKey" : "9c31622802b4f079026bc16b13f52e51c8b5230b5d8a6346814bd8d4229fbaca"
      },
      "vrfPubKey" : {
        "valid" : true,
        "publicKey" : "b2a5c0330c25acb00dfc83efe866e3346817ad4fc7c4b308a835a745460881fe76381330556eab3ef2eda66df0ab7b069d6261aae76d1843e53ec7dfd39f221c5e06d623dccb30b9938c686298788030167db12bd4260ea80366e5ededae0000cae29a4fb8b2ead93e3caa39bd4170fa35aae9145f2fbca207eb49c749b9c78e279fd1cc8673a3ac184fc34a6b75117f7cdd425a7c8b4309e4f95085a9f53637a108224a9405a1e4c19974833f831014f446e31ef50f3fdece3e4b1b69d8000000"
      },
      "proposition" : {
        "publicKey" : "9c31622802b4f079026bc16b13f52e51c8b5230b5d8a6346814bd8d4229fbaca"
      },
      "value" : 100000000000
    }, {
      "nonce" : 7869225102044838903,
      "id" : "c6f7a0f8b42c2b9518655ab30fae3b416afdcabb2548c5ddf5f029ecdbcbcb69",
      "typeId" : 1,
      "proposition" : {
        *"publicKey" : "c6869f3aa8928fe57c24d41ceaca6a1fc57a6bdfdf309dc2de7552790c514bcc"
      },
      *"value" : 1000000000
    }, {
      "nonce" : -5471419949906646475,
      "id" : "719ad73b45778a7487ab898874106909ba106e14e9d49a830c42f5aba8045159",
      "typeId" : 1,
      "proposition" : {
        "publicKey" : "9c31622802b4f079026bc16b13f52e51c8b5230b5d8a6346814bd8d4229fbaca"
      },
      "value" : 4000000000
    } ]
  }
}
```
