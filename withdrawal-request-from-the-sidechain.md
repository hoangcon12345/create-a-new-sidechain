# Withdrawal request from the sidechain

## Create a mainchain address

```
$ ./src/zen-cli -regtest getnewaddress
```

```
ztqPb1tc1J2b6sE6oibK3MsNW4HaEdLqUEK
```

## Create withdrawal order
```
$ curl -X POST "http://127.0.0.1:9085/transaction/withdrawCoins" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"outputs\":[{\"publicKey\":\"ztqPb1tc1J2b6sE6oibK3MsNW4HaEdLqUEK\",\"value\":1000000000}],\"fee\":0}"
```

```
{
  "result" : {
    "transactionId" : "0fa53c2f97730cb9e5c25308bbf1b8a1f32bc7ddf256817ba30d1c88ad35f2dd"
  }
}
```

## Mine block
```
$ curl -X POST "http://127.0.0.1:9085/block/generate" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"epochNumber\":2,\"slotNumber\":3}"
```

```
{
  "result" : {
    "blockId" : "573e2a822102f94114222d3a67b7ac84c8abbb6c93e6ab1357530e6bfa7b8e24"
  }
}
```

```
$ ./src/zen-cli -regtest generate 1
```

```
[
  "0d3743b7a53b6ab9289181c71d647dd3a0291ec513812512430d04b8c371144f"
]
```

but we need to generate more blocks until we fill the 10 epochs.

```
[2-Hop-akka.actor.default-dispatcher-3] INFO com.horizen.certificatesubmitter.CertificateSubmitter - Can't submit certificate, withdrawal epoch info = WithdrawalEpochInfo(0,2)
```

## Generate more blocks
```
$ ./src/zen-cli -regtest generate 1000
```

## Check balance
```
./src/zen-cli -regtest listaddressgroupings
```

```
[
  [
    [
      "ztUDFmnGYxb1zKkCgBWSSM5VyKCBaZaLk4C",
      12.00014204
    ],
    [
      "ztVNJ7wADi8BeiLhvbAWuFMtv5ki1vKZUua",
      1121.99984905
    ]
  ],
  [
    [
      "ztqPb1tc1J2b6sE6oibK3MsNW4HaEdLqUEK",
      7.50000891,
      ""
    ]
  ],
  [
    [
      "ztrF7ETwvuXXckPP3knkstnDfVTJ4j8swiJ",
      6780.00000000
    ]
  ]
]
```

