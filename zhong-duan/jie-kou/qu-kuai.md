# 区块

每8秒，就会有一个节点将区块添加到区块链中。但由于网络/技术错误，节点可能会错过区块。两个区块之间的间隔时间是16秒，下个节点将继续进行循环。

区块链的所有状态变化都是区块的形式存在的，它们包含一系列交易处理和元数据。如果一个或多个交易处理无效，或者元数据无效，则拒绝该区块的交易;。因此，从公共API返回的区块状态是有效的。

## 区块列表

公共API可用于查询区块。该数据集包含数百万区块信息。因此，出于分析目的，我们建议您使用Elasticsearch插件或直接查询数据库。

### 接口

```text
GET /api/blocks
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| page | int | 将返回的页面编号 | 否 |
| limit | int | 每页的资源数量限制 | 否 |
| id | string | 要检索的区块标识符 | 否 |
| height | int | 要检索的区块高度 | 否 |

### 举例

```text
curl https://api.ark.io/api/blocks?limit=2
```

```text
{
  "meta": {
    "count": 2,
    "pageCount": 3927594,
    "totalCount": 7855187,
    "next": "/api/v2/blocks?limit=2&page=2",
    "previous": null,
    "self": "/api/v2/blocks?limit=2&page=1",
    "first": "/api/v2/blocks?limit=2&page=1",
    "last": "/api/v2/blocks?limit=2&page=3927594"
  },
  "data": [
    {
      "id": "10598610037719670879",
      "version": 0,
      "height": 7813396,
      "previous": "8441333128785068929",
      "forged": {
        "reward": 200000000,
        "fee": 0,
        "total": 200000000,
        "amount": 0
      },
      "payload": {
        "hash": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
        "length": 0
      },
      "generator": {
        "username": "arkworld",
        "address": "AeaqhUKfBtVqNhtMct3piBiWfdhbRwbg4W",
        "publicKey": "0257581c82d1931c4b0b2df9d658ecd303fcf2a6ea4ec291669ed06f44fb75c8fe"
      },
      "signature": "30450221009ae77d6b1c3c0e1a7efa488b2f1448f0ec1160650d836014cb739a645586f42902207e426224159252497b335e57da65c1352a6164a897bec350ad175eedf55d779a",
      "transactions": 0,
      "timestamp": {
        "epoch": 63574994,
        "unix": 1553676194,
        "human": "2019-03-27T08:43:14.000Z"
      }
    },
    {
      "id": "8441333128785068929",
      "version": 0,
      "height": 7813395,
      "previous": "7893686533852805129",
      "forged": {
        "reward": 200000000,
        "fee": 0,
        "total": 200000000,
        "amount": 0
      },
      "payload": {
        "hash": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
        "length": 0
      },
      "generator": {
        "username": "bioly",
        "address": "AbUdMhk96FbzxH7vDYAwdyqUELmLopZV5x",
        "publicKey": "02c0b645f19ab304d25aae3add139edd9f6ca9fd0d98e57a808100de0e93832181"
      },
      "signature": "3045022100ae93480145a56c3122a93d92c5504635a3cd86eead21bb6b75501b6e370e734c0220490ef1518ed4d70469868621bc41f33c0031953643ac64bde28e7dc4b55bf2ff",
      "transactions": 0,
      "timestamp": {
        "epoch": 63574986,
        "unix": 1553676186,
        "human": "2019-03-27T08:43:06.000Z"
      }
    }
  ]
}
```

```text
curl https://api.ark.io/api/blocks?height=7000042
```

```text
{
  "meta": {
    "count": 1,
    "pageCount": 1,
    "totalCount": 1,
    "next": null,
    "previous": null,
    "self": "/api/v2/blocks?height=7000042&page=1&limit=100",
    "first": "/api/v2/blocks?height=7000042&page=1&limit=100",
    "last": "/api/v2/blocks?height=7000042&page=1&limit=100"
  },
  "data": [
    {
      "id": "15447090855222023348",
      "version": 0,
      "height": 7000042,
      "previous": "2176620005503475756",
      "forged": {
        "reward": 200000000,
        "fee": 0,
        "total": 200000000,
        "amount": 0
      },
      "payload": {
        "hash": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
        "length": 0
      },
      "generator": {
        "username": "arkworld",
        "address": "AeaqhUKfBtVqNhtMct3piBiWfdhbRwbg4W",
        "publicKey": "0257581c82d1931c4b0b2df9d658ecd303fcf2a6ea4ec291669ed06f44fb75c8fe"
      },
      "signature": "3045022100f564e103c7474d2f7af5782544664f7188a5aa4e7c5829a63b15a2094a9480ae022049d18c5455dddcb5838fcac42be2d55f870ff18dd17aee3cab643f067544fcdd",
      "transactions": 0,
      "timestamp": {
        "epoch": 57039818,
        "unix": 1547141018,
        "human": "2019-01-10T17:23:38.000Z"
      }
    }
  ]
}
```

## 检索区块

可以按区块ID或按区块高度检索区块。区块高度是一个增量整数。

_在比较区块的交易处理和顺序时，我们宁可使用区块高度，也不要使用交易时间戳。因为区块高度是保证井然有序的。_

### 接口

```text
GET /api/blocks/{id|height}
```

### 参数路径

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| {id\|height} | string | 要检索的区块ID或高度 | 是 |

### 举例

```text
curl https://api.ark.io/api/blocks/15447090855222023348
```

```text
curl https://api.ark.io/api/blocks/7000042
```

```text
{
  "data": {
    "id": "15447090855222023348",
    "version": 0,
    "height": 7000042,
    "previous": "2176620005503475756",
    "forged": {
      "reward": 200000000,
      "fee": 0,
      "total": 200000000,
      "amount": 0
    },
    "payload": {
      "hash": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
      "length": 0
    },
    "generator": {
      "username": "arkworld",
      "address": "AeaqhUKfBtVqNhtMct3piBiWfdhbRwbg4W",
      "publicKey": "0257581c82d1931c4b0b2df9d658ecd303fcf2a6ea4ec291669ed06f44fb75c8fe"
    },
    "signature": "3045022100f564e103c7474d2f7af5782544664f7188a5aa4e7c5829a63b15a2094a9480ae022049d18c5455dddcb5838fcac42be2d55f870ff18dd17aee3cab643f067544fcdd",
    "transactions": 0,
    "timestamp": {
      "epoch": 57039818,
      "unix": 1547141018,
      "human": "2019-01-10T17:23:38.000Z"
    }
  }
}
```

## 区块中的所有交易列表

您可以直接获取每个区块的交易作为作为适当的交易对象，而不是反序列化区块的有效负载。

### 接口

```text
GET /api/blocks/{id|height}/transactions
```

### 路径参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| {id\|height} | string | 要检索的区块标识符 | 是 |

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| page | int | 将返回的页面编号 | 否 |
| limit | int | 每页的资源数量 | 否 |

### 举例

```text
curl https://api.ark.io/api/blocks/12079944220667996670/transactions
```

```text
{
  "meta": {
    "count": 2,
    "pageCount": 1,
    "totalCount": 2,
    "next": null,
    "previous": null,
    "self": "/api/v2/blocks/12079944220667996670/transactions?page=1&limit=100",
    "first": "/api/v2/blocks/12079944220667996670/transactions?page=1&limit=100",
    "last": "/api/v2/blocks/12079944220667996670/transactions?page=1&limit=100"
  },
  "data": [
    {
      "id": "7ce77a3520250b3e8174786835cf61b5f62db436949bf46952ed0e17fd8f903d",
      "blockId": "12079944220667996670",
      "version": 1,
      "type": 0,
      "amount": 100059429,
      "fee": 816000,
      "sender": "AKATy581uXWrbm8B4DTQh4R9RbqaWRiKRY",
      "recipient": "AKp7Bu9Nzpq3idcatrLmjsS76E6WkZ2Q2a",
      "signature": "3045022100f9af677be546ec1645fe16f057bff7e06d9410ada259960d1e89fd9cc940221a022052023db0f829d13e43f614a1dab9b07559faa15e2e571494eaf9cf93813ea7f1",
      "signSignature": "3044022067d039dcda866eb89803c9c649308db755aec1d2f7d0894436c6a06511033daf0220348a50856be0902066f8686a78c667cf5c64c504124ed1576d8aa8b029649700",
      "vendorField": "Payout from arkmoon",
      "confirmations": 356,
      "timestamp": {
        "epoch": 63573682,
        "unix": 1553674882,
        "human": "2019-03-27T08:21:22.000Z"
      }
    },
    {
      "id": "da7b05c6a2787a7744345378d614eaad503543daba422c80fc6b929f8be61a91",
      "blockId": "12079944220667996670",
      "version": 1,
      "type": 0,
      "amount": 188600000,
      "fee": 10000000,
      "sender": "AUexKjGtgsSpVzPLs6jNMM6vJ6znEVTQWK",
      "recipient": "AFvsCDPsYYUSSqmnAT7bomdAwPrdq7vDHp",
      "signature": "30440220438bb7293731cbfb62e2229590b64bc9858879d47a34caf88b29eed7761864fc022042fb49ceb25ba7982cbdde6cf544a20a893ceed2378be0564c3405e52cd33d11",
      "confirmations": 356,
      "timestamp": {
        "epoch": 63573682,
        "unix": 1553674882,
        "human": "2019-03-27T08:21:22.000Z"
      }
    }
  ]
}
```

## 搜索所有区块

可以使用搜索资源过滤特定区块。在节点端过滤区块要比大负载请求并在客户端过滤有效负载有效得多。

### 接口

```text
POST /api/blocks/search
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| page | int | 将返回页的编号 | 否 |
| limit | int | 每页的资源数量 | 否 |

### 参数内容

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| id | string | 区块ID | 否 |
| version | int | 区块版本 | 否 |
| previousBlock | int | 前一个区块ID | 否 |
| payloadHash | string | 有效负载容量的哈希值 | 否 |
| generatorPublicKey | string | 区块制造者的通用公钥 | 否 |
| blockSignature | string | 区块签名 | 否 |
| timestamp | object | 区块创建时间的时间戳范围。以从第一块区块创建的秒数来计算。 | 否 |
| timestamp.from | int | 区块创建时间必须大于或等于这个值 | 否 |
| timestamp.to | int | 区块创建时间必须小于或等于这个值 | 否 |
| height | object | 区块的高度范围，第一个区块的高度是1 | 否 |
| height.from | int | 区块高度必须大于或等于这个值 | 否 |
| height.to | int | 区块高度必须小于或等于这个值 | 否 |
| numberOfTransactions | object | 交易数量 | 否 |
| numberOfTransactions.from | int | 区块交易数量必须大于或等于这个值 | 否 |
| numberOfTransactions.to | int | 区块交易数量必须小于等于这个值 | 否 |
| totalAmount | object | 区块内交易总额的范围，包括区块奖励、交易费用和交易金额 | 否 |
| totalAmount.from | int | 区块交易总额必须大于或等于这个值 | 否 |
| totalAmount.to | int | 区块交易总额必须小于或等于这个值 | 否 |
| totalFee | object | 区块内所有交易费用总和的范围 | 否 |
| totalFee.from | int | 所有交易的费用总和必须大于或等于这个值 | 否 |
| totalFee.to | int | 所有交易的费用总额必须小于或等于这个值 | 否 |
| reward | object | 区块交易奖励范围 | 否 |
| reward.from | int | 区块奖励范围必须大于或等于这个值 | 否 |
| reward.to | int | 区块奖励范围必须小于或等于这个值 | 否 |
| payloadLength | object | 有效的载荷容量长度 | 否 |
| payloadLength.from | int | 区块有效载荷容量长度必须大于或等于这个值 | 否 |
| payloadLength.to | int | 区块有效载荷长度必须小于或等于这个值 | 否 |

### 举例

```text
curl --data 'numberOfTransactions={ "from": 100, "to": 110 }' --data 'timestamp={ "from": 60000000 }' https://api.ark.io/api/blocks/search?limit=2
```

```text
{
  "meta": {
    "count": 2,
    "pageCount": 4,
    "totalCount": 7,
    "next": "/api/v2/blocks/search?limit=2&page=2",
    "previous": null,
    "self": "/api/v2/blocks/search?limit=2&page=1",
    "first": "/api/v2/blocks/search?limit=2&page=1",
    "last": "/api/v2/blocks/search?limit=2&page=4"
  },
  "data": [
    {
      "id": "884117316712991715",
      "version": 0,
      "height": 7812000,
      "previous": "11133306790169853761",
      "forged": {
        "reward": 200000000,
        "fee": 46920000,
        "total": 246920000,
        "amount": 414375753
      },
      "payload": {
        "hash": "65b32bc2792f1c84613027503bc4534febeadce4e45612357086a46233a2199d",
        "length": 3264
      },
      "generator": {
        "username": "geops",
        "address": "AU1TGCYoWzBnGMyMK9GTS8BG6EFbgc5xxC",
        "publicKey": "02bf72c578a12c35a97ca1230b93017161ee42c3f0ab82f6fe7c95b3b43561a076"
      },
      "signature": "3044022007082f2d025c49a1daf30f8461daf0cca0fad3a67c1e0369d9438687670fbbd5022028e9cbaadc5a33c55111cf98aad23697c4618e38fa178cc8163bf8275b41632c",
      "transactions": 102,
      "timestamp": {
        "epoch": 63563826,
        "unix": 1553665026,
        "human": "2019-03-27T05:37:06.000Z"
      }
    },
    {
      "id": "14707858435494505009",
      "version": 0,
      "height": 7806541,
      "previous": "10644622929675679656",
      "forged": {
        "reward": 200000000,
        "fee": 112845000,
        "total": 312845000,
        "amount": 296221771579
      },
      "payload": {
        "hash": "9ffe089a0058c1a28f0b54643fcee66c8a8cce1c1b60253951e81170c80610ca",
        "length": 3360
      },
      "generator": {
        "username": "cams_yellow_jacket",
        "address": "AGvhBGb4cCZnP2wUo1oCSi83LUtGDG7Y6X",
        "publicKey": "02902de3fcb257e9248e2ae668d2e314027f0ca05c1eb21e1c5817c7580014669f"
      },
      "signature": "30440220715fdf928549266485e4a61bf1468d4a1fe1c6d4b9d452379ad8da742e58244b022059a9f586a2fc07521fa45bdf6dd122dc78cf594174c445648b254f4c3ef4fc29",
      "transactions": 105,
      "timestamp": {
        "epoch": 63520130,
        "unix": 1553621330,
        "human": "2019-03-26T17:28:50.000Z"
      }
    }
  ]
}
```

