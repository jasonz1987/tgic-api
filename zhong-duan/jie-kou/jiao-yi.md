# 交易

交易是有符号的、序列化的有效载荷，成批地放在一起形成一个区块。

## 创建交易

为事务创建正确的有效负载并非易事，因为它需要加密功能和特定的序列化协议。 我们的加密SDK提供大多数主要编程语言所需的功能。 您可以在“发送交易”部分中了解更多信息。

### 接口

```text
POST /api/transactions
```

### 参数内容

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| transactions | array | 要创建的交易列表 | 是 |

### 反应

```text
{
  "data": {
    "accept": [
      "15d4b3e933b79e5172bbf14c2bd3f92d927394cd8ebd102f18dcc2203af363ca",
      "c48862c4df75a8b0859b559658c757c1c289088488630494fe51613db0747e57",
      "bd10b25444363252e0787e46f5cac90797d08a0c34d507a10d064c94cccf6226"
    ],
    "broadcast": [
      "15d4b3e933b79e5172bbf14c2bd3f92d927394cd8ebd102f18dcc2203af363ca",
      "c48862c4df75a8b0859b559658c757c1c289088488630494fe51613db0747e57",
      "bd10b25444363252e0787e46f5cac90797d08a0c34d507a10d064c94cccf6226"
    ],
    "excess": [],
    "invalid": []
  },
  "errors": null
}
```

## 检索交易

通过ID获取交易不需要高级逻辑;因为API不返回序列化的交易，而是一个DTO。

### 接口

```text
GET /api/transactions/{id}
```

### 路径参数

```text
{
  "data": {
    "id": "5c6ce775447a5acd22050d72e2615392494953bb1fb6287e9ffb3c33eaeb79aa",
    "blockId": "4271682877946294396",
    "type": 0,
    "amount": 32106400000,
    "fee": 10000000,
    "sender": "DDiTHZ4RETZhGxcyAi1VruCXZKxBFqXMeh",
    "recipient": "DQnQNoJuNCvpjYhxL7fsnGepHBqrumgsyP",
    "signature": "3044022047c39f6f45a46a87f91ca867f9551dbebf0035adcfcbdc1370222c7a1517fc0002206fb5ecc10460e0352a8b626a508e2fcc76e39e490b0a2581dd772ebc8079696e",
    "confirmations": 1928,
    "timestamp": {
      "epoch": 32794053,
      "unix": 1522895253,
      "human": "2018-04-05T02:27:33Z"
    }
  }
}
```

## 交易列表

分页API用于查询多个交易。您可以通过查询参数来搜索特定的交易。

### 接口

```text
GET /api/transactions
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| page | int | 将返回的页面编号 | 否 |
| limit | int | 每页的资源数量 | 否 |
| type | int | 要检索的交易类型 | 否 |
| blockld | int | 要检索的区块ID | 否 |
| id | int | 要检索的交易ID | 否 |

### 反应

```text
{
  "meta": {
    "count": 2,
    "pageCount": 127430,
    "totalCount": 254860,
    "next": "/v2/transactions?page=2",
    "previous": null,
    "self": "/v2/transactions?page=1",
    "first": "/v2/transactions?page=1",
    "last": "/v2/transactions?page=127430"
  },
  "data": [
    {
      "id": "5c6ce775447a5acd22050d72e2615392494953bb1fb6287e9ffb3c33eaeb79aa",
      "blockId": "4271682877946294396",
      "version": 1,
      "type": 0,
      "amount": 32106400000,
      "fee": 10000000,
      "sender": "DDiTHZ4RETZhGxcyAi1VruCXZKxBFqXMeh",
      "recipient": "DQnQNoJuNCvpjYhxL7fsnGepHBqrumgsyP",
      "signature": "3044022047c39f6f45a46a87f91ca867f9551dbebf0035adcfcbdc1370222c7a1517fc0002206fb5ecc10460e0352a8b626a508e2fcc76e39e490b0a2581dd772ebc8079696e",
      "asset": {},
      "confirmations": 1924,
      "timestamp": {
        "epoch": 32794053,
        "unix": 1522895253,
        "human": "2018-04-05T02:27:33Z"
      }
    }
  ]
}
```

## 列出所有未确认的交易

未经确认的交易尚未纳入区块链，而是驻留在内存池中。 尽管通常会在数分钟内清除内存池，但在网络负载较高的情况下，费用低廉的交易将在此处停留相当长的时间。 如果您将交易费用设置为接近零，则代表可能不会接收该交易，并且超时。

### 接口

```text
GET /api/transactions/unconfirmed/
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| page | int | 将返回页面编号 | 否 |
| limit | int | 每页的资源数量 | 否 |

### 反应

```text
{
  "meta": {
    "count": 5,
    "pageCount": 8,
    "totalCount": 40,
    "next": "/api/v2/transactions/unconfirmed?limit=5&page=2",
    "previous": null,
    "self": "/api/v2/transactions/unconfirmed?limit=5&page=1",
    "first": "/api/v2/transactions/unconfirmed?limit=5&page=1",
    "last": "/api/v2/transactions/unconfirmed?limit=5&page=8"
  },
  "data": [
    {
      "id": "c94504293d23e3be535a049fdfacba95147f2a87a4ef6682c56801da96befce0",
      "version": 1,
      "type": 0,
      "amount": 70866123,
      "fee": 344000,
      "sender": "DMzBk3g7ThVQPYmpYDTHBHiqYuTtZ9WdM3",
      "recipient": "DMzBk3g7ThVQPYmpYDTHBHiqYuTtZ9WdM3",
      "signature": "30450221008adeff8eb2a780168704d9e210368d81edff79b81aa7b995e43486f3b1e0096502205caef345584319a6294b1f5283c0d17b478b8a9bcdc10570e5a58681b0eae332",
      "vendorField": "Yooooooloooooo",
      "confirmations": 0,
      "timestamp": {
        "epoch": 56388424,
        "unix": 1546489624,
        "human": "2019-01-03T04:27:04.000Z"
      }
    },
    {
      "id": "db2e54211c352217eee0313a01f6258ac1634e201f04f89b0561d34f7d598066",
      "version": 1,
      "type": 0,
      "amount": 17130719,
      "fee": 344000,
      "sender": "DMzBk3g7ThVQPYmpYDTHBHiqYuTtZ9WdM3",
      "recipient": "DKahhVFVJfqCcCmaQHuYzAVFKcWjBu5i6Z",
      "signature": "30440220069f25d555157f3216b6725e1f66f37b126dcc039f2a4eb12fe74d9e93595d7b02202980215c9375d43f24ebd26a32d6db49f260ad55199c3a137b7dce61e324c970",
      "vendorField": "Yooooooloooooo",
      "confirmations": 0,
      "timestamp": {
        "epoch": 56388424,
        "unix": 1546489624,
        "human": "2019-01-03T04:27:04.000Z"
      }
    },
    {
      "id": "825ab53b50fa99d339486ab780c6a187c7f4fbccfa1098f38be7f57226b144bd",
      "version": 1,
      "type": 0,
      "amount": 11266113,
      "fee": 344000,
      "sender": "DMzBk3g7ThVQPYmpYDTHBHiqYuTtZ9WdM3",
      "recipient": "DG92jj4vUW7SyxzM1VzkmQWMmgBGZVhrjb",
      "signature": "3045022100918864cc6e5ae22010820f1d2a3d4677472d20d7a151597f3f6c705028f28dcf02203518b755fb860b40edfcde5107909d043e7a2cc38d66f5ca52710a0be7e6d710",
      "vendorField": "Yooooooloooooo",
      "confirmations": 0,
      "timestamp": {
        "epoch": 56388425,
        "unix": 1546489625,
        "human": "2019-01-03T04:27:05.000Z"
      }
    },
    {
      "id": "26146b25cde21ab72ecd49a0ac582372314625d854154cfd705dc841a4765ac8",
      "version": 1,
      "type": 0,
      "amount": 737042,
      "fee": 344000,
      "sender": "DMzBk3g7ThVQPYmpYDTHBHiqYuTtZ9WdM3",
      "recipient": "DN8nGwcNbE3YcnZYFp8uvvc9z4WWDbytWK",
      "signature": "3044022067abb680cd6699cf5dac9194c576949dce4b29fe3e4d108724829e8aa34d8a3c02205a3bb91bb46a0182c1dc393c05538e0b673702c75ff39ad0acbf6b879082d911",
      "vendorField": "Yooooooloooooo",
      "confirmations": 0,
      "timestamp": {
        "epoch": 56388425,
        "unix": 1546489625,
        "human": "2019-01-03T04:27:05.000Z"
      }
    },
    {
      "id": "7f54d415750361b3f15bdd4c85d73cbc6ea43efbee6e7725048c223cadd9a4b2",
      "version": 1,
      "type": 0,
      "amount": 70866123,
      "fee": 344000,
      "sender": "DMzBk3g7ThVQPYmpYDTHBHiqYuTtZ9WdM3",
      "recipient": "DMzBk3g7ThVQPYmpYDTHBHiqYuTtZ9WdM3",
      "signature": "304402207a2f0ce904148dfa1aa0ffc685bdf0614b2e98de98f32b108dd205174d6b767102201566d703296801057e8f94c396fc5be208e6bddde20f5d70be3f46fbcf640bbd",
      "vendorField": "Yooooooloooooo",
      "confirmations": 0,
      "timestamp": {
        "epoch": 56388425,
        "unix": 1546489625,
        "human": "2019-01-03T04:27:05.000Z"
      }
    }
  ]
}
```

## 获取未确认的交易

与查询确认交易一样，您可以直接查询未确认交易。

### 接口

```text
GET /api/transactions/unconfirmed/{id}
```

### 路径参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| id | string | 要检索的交易的标识符 | 是 |

### 反应

```text
{
  "data": {
    "id": "c94504293d23e3be535a049fdfacba95147f2a87a4ef6682c56801da96befce0",
    "version": 1,
    "type": 0,
    "amount": 70866123,
    "fee": 344000,
    "sender": "DMzBk3g7ThVQPYmpYDTHBHiqYuTtZ9WdM3",
    "recipient": "DMzBk3g7ThVQPYmpYDTHBHiqYuTtZ9WdM3",
    "signature": "30450221008adeff8eb2a780168704d9e210368d81edff79b81aa7b995e43486f3b1e0096502205caef345584319a6294b1f5283c0d17b478b8a9bcdc10570e5a58681b0eae332",
    "vendorField": "Yooooooloooooo",
    "confirmations": 0,
    "timestamp": {
      "epoch": 56388424,
      "unix": 1546489624,
      "human": "2019-01-03T04:27:04.000Z"
    }
  }
}
```

## 交易查询

对于细粒度搜索，使用交易查询接口。注意，除非使用特定的主体参数，否则响应可能包含大量交易\(数十万\)。最好是过滤尽可能多的交易节点，而不是分析解剖响应客户端。

### 接口

```text
POST /api/transactions/search
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| page | int | 将返回页面编号 | 否 |
| limit | int | 每一页的资源数量 | 否 |

### 参数内容

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| orderBy | string | ... | 否 |
| id | string | ... | 否 |
| blockId | string | ... | 否 |
| type | int | ... | 否 |
| version | int | ... | 否 |
| senderPublicKey | string | ... | 否 |
| senderId | string | ... | 否 |
| recipientId | string | ... | 否 |
| ownerId | string | ... | 否 |
| vendorFieldHex | string | ... | 否 |
| timestamp | object | ... | 否 |
| timestamp.from | int | ... | 否 |
| timestamp.to | int | ... | 否 |
| amount | object | ... | 否 |
| amount.from | int | ... | 否 |
| amount.to | int | ... | 否 |
| fee | object | ... | 否 |
| fee.from | int | ... | 否 |
| fee.to | int | ... | 否 |

### 反应

```text
{
  "meta": {
    "Count": 1,
    "PageCount": 79382,
    "totalCount": 79382,
    "next": "/api/v2/transactions/search?limit=1&page=2",
    "previous": null,
    "self": "/api/v2/transactions/search?limit=1&page=1",
    "first": "/api/v2/transactions/search?limit=1&page=1",
    "last": "/api/v2/transactions/search?limit=1&page=79382"
  },
  "data": [
    {
      "id": "026fbc15cf630e8fc2a3e963d2c436c744d880611a468b34b85145e181b80dc0",
      "blockId": "14085724014999449555",
      "version": 1,
      "type": 0,
      "amount": 737042,
      "fee": 344000,
      "sender": "DMzBk3g7ThVQPYmpYDTHBHiqYuTtZ9WdM3",
      "recipient": "DN8nGwcNbE3YcnZYFp8uvvc9z4WWDbytWK",
      "signature": "3045022100cb2c2d9086188f4b09c97b99374da91579d15c99206bbb04512053922cb0209f022026a4676483d1162eaafd64d2acfa43413e02f587922cf55f3205bbf509bd118b",
      "vendorField": "Yooooooloooooo",
      "confirmations": 103,
      "timestamp": {
        "epoch": 56388434,
        "unix": 1546489634,
        "human": "2019-01-03T04:27:14.000Z"
      }
    }
  ]
}
```

## 获取交易类型

交易类型是特定于网络的。ARK目前支持八种不同的类型，但如果出于业务目的需要，BridgeChains可以定义更多或更少的内容。

### 接口

```text
GET /api/transactions/types
```

### 反应

```text
{
  "data": {
    "Transfer": 0,
    "SecondSignature": 1,
    "DelegateRegistration": 2,
    "Vote": 3,
    "MultiSignature": 4,
    "Ipfs": 5,
    "TimelockTransfer": 6,
    "MultiPayment": 7,
    "DelegateResignation": 8
  }
}
```

## 获取交易费用（非动态）

静态交易费用明显高于动态交易费用。使用节点资源查找动态费用更常用。

### 接口

```text
GET /api/transactions/fees
```

### 反应

```text
{
  "data": {
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
}
```



