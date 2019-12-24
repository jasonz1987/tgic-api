# 投票

投票是一种特定的交易类型。 一个钱包给另一个钱包投票，该钱包已经注册自己有资格成为代表。 钱包可以自己投票。

> 用户经常被投票机制和与投票相关的费用所迷惑。一个代表不会从他们的选民那里得到ARK，他们产生的块的数量也与他们的投票权成正比。

## 投票列表

可以通过此API获得所有投票交易，这相当于参数内容中类型3的交易搜索。

### 接口

```text
GET /api/votes
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
    "count": 2,
    "pageCount": 658,
    "totalCount": 1315,
    "next": "/v2/votes?page=2",
    "previous": null,
    "self": "/v2/votes?page=1",
    "first": "/v2/votes?page=1",
    "last": "/v2/votes?page=658"
  },
  "data": [
    {
      "id": "560959e435cbf8eec60691890f3dd55d141e76077e1fe803f65d137c91099240",
      "blockId": "12872155462883631430",
      "version": 1,
      "type": 3,
      "amount": 0,
      "fee": 100000000,
      "sender": "DAp7JjULVgqzd4jLofkUyLRovHRPUTQwiZ",
      "recipient": "DAp7JjULVgqzd4jLofkUyLRovHRPUTQwiZ",
      "signature": "30440220522eadff84b5b4b2fc6a3ef611bf093dbd0a06963c32c767ee28729898d0a1d302203f851594e5b2271a987e98daa4fc8b5f384fac65c41eb1c43739af2d4b5dc902",
      "asset": {
        "votes": [
          "-032fe001dff675a6edfe3d0e51201b2900d3b5050a46d770306aefaa574c022672"
        ]
      },
      "confirmations": 39989,
      "timestamp": {
        "epoch": 32414926,
        "unix": 1522516126,
        "human": "2018-03-31T17:08:46Z"
      }
    }
  ]
}
```

## 投票检索

可以使用投票的事务ID检索投票。请注意包含投票对象的资产字段。数组中每个项的第一个字符表示它是投票+，还是取消投票 -，后跟代表的公钥。

### 接口

```text
GET /api/votes/{id}
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| id | string | 将被检索的投票标识符 | 是 |

### 反应

```text
{
  "data": {
    "id": "beb8dd43c640f562704090159154b2742afba7eacada9e8edee447e34e7675c6",
    "blockId": "13661015019049808045",
    "version": 1,
    "type": 3,
    "amount": 0,
    "fee": 100000000,
    "sender": "DAp7JjULVgqzd4jLofkUyLRovHRPUTQwiZ",
    "recipient": "DAp7JjULVgqzd4jLofkUyLRovHRPUTQwiZ",
    "signature": "3045022100e9a743c5aa0df427f49af61d35fe617182479f7e8d368ce23b7ec43ab6d269c80220193aafd4ccb3eedbd76ded7ea99f31629013dc3af60540029fe98b274d42d284",
    "asset": {
      "votes": [
        "+032fe001dff675a6edfe3d0e51201b2900d3b5050a46d770306aefaa574c022672"
      ]
    },
    "confirmations": 48189,
    "timestamp": {
      "epoch": 32338609,
      "unix": 1522439809,
      "human": "2018-03-30T19:56:49Z"
    }
  }
}
```

