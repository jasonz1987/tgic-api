# 节点

节点资源对于服务发现、运行状况检查和获得网络配置\(如费用、API和token信息\)非常有用。

> 请注意，这些参数是由特定节点返回的，其他节点可能会遵循一组不同的参数。

## 检索配置

用于访问节点的配置及其所连接的网络

### 接口

```text
GET /api/node/configuration
```

### 反应

```text
{
  "data": {
    "nethash": "578e820911f24e039733b45e4882b73e301f813a0d2c31330dafda84534ffa23",
    "token": "DARK",
    "symbol": "DѦ",
    "explorer": "https://dexplorer.ark.io",
    "version": 30,
    "ports": {
      "@arkecosystem/core-p2p": 4000,
      "@arkecosystem/core-api": 4003,
      "@arkecosystem/core-json-rpc": 8080
    },
    "constants": {
      "height": 75600,
      "reward": 200000000,
      "activeDelegates": 51,
      "blocktime": 8,
      "block": {
        "version": 0,
        "maxTransactions": 50,
        "maxPayload": 2097152
      },
      "epoch": "2017-03-21T13:00:00.000Z",
      "fees": {
        "staticFees": {
          "transfer": 10000000,
          "secondSignature": 500000000,
          "delegateRegistration": 2500000000,
          "vote": 100000000,
          "multiSignature": 500000000,
          "ipfs": 0,
          "timelockTransfer": 0,
          "multiPayment": 0,
          "delegateResignation": 0
        }
      },
      "ignoreInvalidSecondSignatureField": false
    },
    "transactionPool": {
      "maxTransactionAge": 21600,
      "dynamicFees": {
        "enabled": true,
        "minFeePool": 1000,
        "minFeeBroadcast": 1000,
        "addonBytes": {
          "transfer": 100,
          "secondSignature": 250,
          "delegateRegistration": 400000,
          "vote": 100,
          "multiSignature": 500,
          "ipfs": 250,
          "timelockTransfer": 500,
          "multiPayment": 500,
          "delegateResignation": 400000
        }
      }
    }
  }
}
```

## 检索密码配置

用于访问处理所有加密操作的程序包节点配置。

### 接口

```text
GET /api/node/configuration/crypto
```

### 反应

```text
{
   "data":{
      "exceptions":{},
      "genesisBlock":{
         "version":0,
         "totalAmount":"12500000000000000",
         "totalFee":"0",
         "reward":"0",
         "payloadHash":"d9acd04bde4234a81addb8482333b4ac906bed7be5a9970ce8ada428bd083192",
         "timestamp":0,
         "numberOfTransactions":153,
         "payloadLength":35960,
         "previousBlock":null,
         "generatorPublicKey":"03b47f6b6719c76bad46a302d9cff7be9b1c2b2a20602a0d880f139b5b8901f068",
         "transactions":[
            {
               "type":0,
               "amount":"245098000000000",
               "fee":"0",
               "recipientId":"AHXtmB84sTZ9Zd35h9Y1vfFvPE2Xzqj8ri",
               "timestamp":0,
               "asset":{

               },
               "senderPublicKey":"035b63b4668ee261c16ca91443f3371e2fe349e131cb7bf5f8a3e93a3ddfdfc788",
               "signature":"304402205fcb0677e06bde7aac3dc776665615f4b93ef8c3ed0fddecef9900e74fcb00f302206958a0c9868ea1b1f3d151bdfa92da1ce24de0b1fcd91933e64fb7971e92f48d",
               "id":"db1aa687737858cc9199bfa336f9b1c035915c30aaee60b1e0f8afadfdb946bd"
            },
            ...
         ],
         "height":1,
         "id":"17184958558311101492",
         "blockSignature":"304402202fe5de5697fa25d3d3c0cb24617ac02ddfb1c915ee9194a89f8392f948c6076402200d07c5244642fe36afa53fb2d048735f1adfa623e8fa4760487e5f72e17d253b"
      },
      "milestones":[
         {
            "height":1,
            "reward":0,
            "activeDelegates":51,
            "blocktime":8,
            "block":{
               "version":0,
               "maxTransactions":150,
               "maxPayload":2097152
            },
            "epoch":"2017-03-21T13:00:00.000Z",
            "fees":{
               "staticFees":{
                  "transfer":10000000,
                  "secondSignature":500000000,
                  "delegateRegistration":2500000000,
                  "vote":100000000,
                  "multiSignature":500000000,
                  "ipfs":500000000,
                  "timelockTransfer":0,
                  "multiPayment":0,
                  "delegateResignation":2500000000
               }
            },
            "vendorFieldLength":64,
            "aip11":true
         },
         {
            "height":75600,
            "reward":200000000,
            "activeDelegates":51,
            "blocktime":8,
            "block":{
               "version":0,
               "maxTransactions":150,
               "maxPayload":2097152
            },
            "epoch":"2017-03-21T13:00:00.000Z",
            "fees":{
               "staticFees":{
                  "transfer":10000000,
                  "secondSignature":500000000,
                  "delegateRegistration":2500000000,
                  "vote":100000000,
                  "multiSignature":500000000,
                  "ipfs":500000000,
                  "timelockTransfer":0,
                  "multiPayment":0,
                  "delegateResignation":2500000000
               }
            },
            "vendorFieldLength":64,
            "aip11":true
         },
         {
            "height":100000,
            "reward":200000000,
            "activeDelegates":51,
            "blocktime":8,
            "block":{
               "version":0,
               "maxTransactions":150,
               "maxPayload":2097152
            },
            "epoch":"2017-03-21T13:00:00.000Z",
            "fees":{
               "staticFees":{
                  "transfer":10000000,
                  "secondSignature":500000000,
                  "delegateRegistration":2500000000,
                  "vote":100000000,
                  "multiSignature":500000000,
                  "ipfs":500000000,
                  "timelockTransfer":0,
                  "multiPayment":0,
                  "delegateResignation":2500000000
               }
            },
            "vendorFieldLength":255,
            "aip11":true
         },
         {
            "height":1000000000,
            "reward":200000000,
            "activeDelegates":51,
            "blocktime":8,
            "block":{
               "version":0,
               "maxTransactions":150,
               "maxPayload":2097152,
               "idFullSha256":true
            },
            "epoch":"2017-03-21T13:00:00.000Z",
            "fees":{
               "staticFees":{
                  "transfer":10000000,
                  "secondSignature":500000000,
                  "delegateRegistration":2500000000,
                  "vote":100000000,
                  "multiSignature":500000000,
                  "ipfs":500000000,
                  "timelockTransfer":0,
                  "multiPayment":0,
                  "delegateResignation":2500000000
               }
            },
            "vendorFieldLength":255,
            "aip11":true
         }
      ],
      "network":{
         "name":"testnet",
         "messagePrefix":"TEST message:\n",
         "bip32":{
            "public":70617039,
            "private":70615956
         },
         "pubKeyHash":23,
         "nethash":"d9acd04bde4234a81addb8482333b4ac906bed7be5a9970ce8ada428bd083192",
         "wif":186,
         "slip44":1,
         "aip20":0,
         "client":{
            "token":"TARK",
            "symbol":"TѦ",
            "explorer":"http://texplorer.ark.io"
         }
      }
   }
}
```

## 检索费用统计

用于访问节点的费用统计信息

### 接口

```text
GET /api/node/fees
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| days | int | 将被考虑的天数 | 否 |

### 反应

```text
{
  "meta": {
    "days": 7
  },
  "data": [
    {
      "type": "0",
      "min": "192309",
      "max": "100000000",
      "avg": "653891",
      "sum": "2820887339",
      "median": "460000"
    },
    {
      "type": "3",
      "min": "1822918",
      "max": "73422894",
      "avg": "59645587",
      "sum": "715747046",
      "median": "68488514"
    }
  ]
}
```

## 检索状态

该状态允许运行状况检查，显示节点是否与网络同步。

### 接口

```text
GET /api/node/status
```

### 反应

```text
{
  "data": {
    "synced": false,
    "now": 3034451,
    "blocksCount": -36
  }
}
```

## 检索同步状态

同步资源类似于节点状态，提供了有关同步进度的信息。如果某个节点没有同步，在区块中明显落后，则那么可能需要执行检查。

### 接口

```text
GET /api/node/syncing
```

### 反应

```text
{
  "data": {
    "syncing": true,
    "blocks": -36,
    "height": 3034451,
    "id": "5444078994968869529"
  }
}
```

