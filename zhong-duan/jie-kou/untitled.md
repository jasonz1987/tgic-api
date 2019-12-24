# 代表

代表是指那些已经注册，且有资格通过注册交易的钱包（地址）。如果一个代表在投票中名列前51位，则它可以运行一个节点，每6.8分钟生成一个区块，代表将获得交易费用。

第一个代表是初始的虚拟化代表。他们没有注册也没有投票，在主网上很久之前就已经被实际代表所代替。

## 所有代表

您可以通过这个页面分页API获得所有代表。注意，所有已注册的代表都将在此响应中返回，而不仅仅是前51个代表。

如果代表节点处于离线状态，则仍然通过此API返回；因为代表资源与实际节点无关，只与注册和钱包有关。

### 接口

```text
GET /api/delegates
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| page | int | 将返回的页面编号 | 否 |
| limit | int | 每页的资源数量 | 否 |

### 举例

```text
curl https://api.ark.io/api/delegates
```

```text
{
  "meta": {
    "count": 100,
    "pageCount": 11,
    "totalCount": 1022,
    "next": "/api/v2/delegates?page=2&limit=100",
    "previous": null,
    "self": "/api/v2/delegates?page=1&limit=100",
    "first": "/api/v2/delegates?page=1&limit=100",
    "last": "/api/v2/delegates?page=11&limit=100"
  },
  "data": [
    {
      "username": "biz_classic",
      "address": "AKdr5d9AMEnsKYxpDcoHdyyjSCKVx3r9Nj",
      "publicKey": "020431436cf94f3c6a6ba566fe9e42678db8486590c732ca6c3803a10a86f50b92",
      "votes": 290192277300775,
      "rank": 1,
      "blocks": {
        "produced": 137929,
        "missed": 294,
        "last": {
          "id": "4969352721420908242",
          "height": 8051390,
          "timestamp": {
            "epoch": 65479992,
            "unix": 1555581192,
            "human": "2019-04-18T09:53:12.000Z"
          }
        }
      },
      "production": {
        "approval": 2.27,
        "productivity": 99.79
      },
      "forged": {
        "fees": 1173040419815,
        "rewards": 27585800000000,
        "total": 28758840419815
      }
    },
    ...
  ]
}
```

```text
curl "https://api.ark.io/api/delegates?page=5&limit=2"
```

```text
{
  "meta": {
    "count": 2,
    "pageCount": 511,
    "totalCount": 1022,
    "next": "/api/v2/delegates?page=6&limit=2",
    "previous": "/api/v2/delegates?page=4&limit=2",
    "self": "/api/v2/delegates?page=5&limit=2",
    "first": "/api/v2/delegates?page=1&limit=2",
    "last": "/api/v2/delegates?page=511&limit=2"
  },
  "data": [
    {
      "username": "goose",
      "address": "ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ",
      "publicKey": "03c5d32dedf5441b3aafb2e0c6ad3e5568bb0b3e822807b133e2276e014d830e3c",
      "votes": 171643014160739,
      "rank": 9,
      "blocks": {
        "produced": 119844,
        "missed": 337,
        "last": {
          "id": "4941983238011713644",
          "height": 8051380,
          "timestamp": {
            "epoch": 65479914,
            "unix": 1555581114,
            "human": "2019-04-18T09:51:54.000Z"
          }
        }
      },
      "production": {
        "approval": 1.34,
        "productivity": 99.72
      },
      "forged": {
        "fees": 846370414394,
        "rewards": 23968800000000,
        "total": 24815170414394
      }
    },
    {
      "username": "biz_private",
      "address": "AaAy8BZkjV86YN7xUtZ35iwyXRMQKtKoAy",
      "publicKey": "02fa6902e91e127d6d3410f6abc271a79ae24029079caa0db5819757e3c1c1c5a4",
      "votes": 168585645882892,
      "rank": 10,
      "blocks": {
        "produced": 111777,
        "missed": 368,
        "last": {
          "id": "9030517911522129229",
          "height": 8051409,
          "timestamp": {
            "epoch": 65480144,
            "unix": 1555581344,
            "human": "2019-04-18T09:55:44.000Z"
          }
        }
      },
      "production": {
        "approval": 1.32,
        "productivity": 99.67
      },
      "forged": {
        "fees": 1405755397853,
        "rewards": 22355400000000,
        "total": 23761155397853
      }
    }
  ]
}
```

## 检索代表

您可以通过用户名、地址和公钥查询特定的代表，因此，下面的查询将得到相同的响应。请注意，对于代表，公钥总是已知的，因为它们之前进行了注册。但普通钱包却不是这样。

### 接口

```text
GET /api/delegates/{username|address|publicKey}
```

### 路径参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| {username\|address\|publicKey} | string | 要检索的代表标识符 | 是 |

### 举例

```text
curl https://api.ark.io/api/delegates/boldninja
```

```text
curl https://api.ark.io/api/delegates/ARMy9u1XvrZ124JzQq3oeJpjmBEnYkyU7D
```

```text
curl https://api.ark.io/api/delegates/035217d8ff31d78992e0821667fed6d9298d2b923cd63b650e894e0bf11a0a6d7a
```

```text
{
  "data": {
    "username": "boldninja",
    "address": "ARMy9u1XvrZ124JzQq3oeJpjmBEnYkyU7D",
    "publicKey": "035217d8ff31d78992e0821667fed6d9298d2b923cd63b650e894e0bf11a0a6d7a",
    "votes": 10000000,
    "rank": 180,
    "blocks": {
      "produced": 3,
      "missed": 4,
      "last": {
        "id": "17262490796048771853",
        "height": 1058,
        "timestamp": {
          "epoch": 19400,
          "unix": 1490120600,
          "human": "2017-03-21T18:23:20.000Z"
        }
      }
    },
    "production": {
      "approval": 0,
      "productivity": 42.86
    },
    "forged": {
      "fees": 0,
      "rewards": 0,
      "total": 0
    }
  }
}
```

## 代表的所有区块列表

代表允许您从特定的代表获取区块。这相当于使用区块公共公钥搜索区块。

### 接口

```text
GET /api/delegates/{username|address|publicKey}/blocks
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| {username\|address\|publicKey} | string | 要检索的代表标识符 | 是 |

### 路径参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| page | int | 要返回的页面编号 | 否 |
| limit | int | 每页的资源数量 | 否 |

### 举例

```text
curl "https://api.ark.io/api/delegates/ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ/blocks?page=5&limit=2"
```

```text
{
  "meta": {
    "count": 2,
    "pageCount": 62029,
    "totalCount": 124057,
    "next": "/api/v2/delegates/ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ/blocks?page=6&limit=2",
    "previous": "/api/v2/delegates/ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ/blocks?page=4&limit=2",
    "self": "/api/v2/delegates/ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ/blocks?page=5&limit=2",
    "first": "/api/v2/delegates/ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ/blocks?page=1&limit=2",
    "last": "/api/v2/delegates/ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ/blocks?page=62029&limit=2"
  },
  "data": [
    {
      "id": "15452336890126796922",
      "version": 0,
      "height": 8051452,
      "previous": "9864401348516061780",
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
        "username": "goose",
        "address": "ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ",
        "publicKey": "03c5d32dedf5441b3aafb2e0c6ad3e5568bb0b3e822807b133e2276e014d830e3c"
      },
      "signature": "3045022100b768b2a96868c4f442699f5b3978c8fb3ac94b31d44568ba9431be04611c5b8d02201d79cb91e5dd0fb88985a72f73643b96d34baaf196ec6ce6785308ce7a56e4b9",
      "transactions": 0,
      "timestamp": {
        "epoch": 65480490,
        "unix": 1555581690,
        "human": "2019-04-18T10:01:30.000Z"
      }
    },
    {
      "id": "4941983238011713644",
      "version": 0,
      "height": 8051380,
      "previous": "10030681307966151993",
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
        "username": "goose",
        "address": "ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ",
        "publicKey": "03c5d32dedf5441b3aafb2e0c6ad3e5568bb0b3e822807b133e2276e014d830e3c"
      },
      "signature": "304502210080ab4a74453a2fa456dea52188397a3f9a5edd64e592dd2e2fb0c0a9714eff9a0220216fb5aeeebc8189e5ee8dab643457a393f2874df8aff531f7b8377dd8d6deb1",
      "transactions": 0,
      "timestamp": {
        "epoch": 65479914,
        "unix": 1555581114,
        "human": "2019-04-18T09:51:54.000Z"
      }
    }
  ]
}
```

## 代表的所有投票人列表

获得代表的选票也很简单。节点返回活跃的投票者。为了获取历史投票人，最好直接查询数据库。

### 接口

```text
GET /api/delegates/{username|address|publicKey}/voters
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| {username\|address\|publicKey} | string | 要检索的代表标识符 | 是 |

### 路径参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| page | int | 将返回的页面编号 | 否 |
| limit | int | 每页的资源数量 | 否 |

### 举例

```text
curl "https://api.ark.io/api/delegates/ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ/voters?page=1&limit=1"
```

```text
{
  "meta": {
    "count": 1,
    "pageCount": 626,
    "totalCount": 626,
    "next": "/api/v2/delegates/ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ/voters?page=2&limit=1",
    "previous": null,
    "self": "/api/v2/delegates/ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ/voters?page=1&limit=1",
    "first": "/api/v2/delegates/ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ/voters?page=1&limit=1",
    "last": "/api/v2/delegates/ALLZ3TQKTaHm2Bte4SrXL9C5cS8ZovqFfZ/voters?page=626&limit=1"
  },
  "data": [
    {
      "address": "Af1e7oavXTJs1RYs7DeRuphC6eSAUFpsWC",
      "publicKey": "02a589e02e853bb5b9c989b2935a63eab88d847addb35bcbd838597a7623ba5748",
      "username": null,
      "secondPublicKey": null,
      "balance": 16338033891543,
      "isDelegate": false,
      "vote": "03c5d32dedf5441b3aafb2e0c6ad3e5568bb0b3e822807b133e2276e014d830e3c"
    }
  ]
}
```

## 代表搜索

对于细粒度搜索，使用搜索接口。

### 接口

```text
POST /api/delegates/search
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| page | int | 将返回页面编号 | 否 |
| limit | int | 每页的资源数量 | 否 |

### 参数内容

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| address | string | 要检索的代表地址 | 否 |
| publicKey | string | 要检索的代表公钥 | 否 |
| username | string | 要检索的代表用户名 | 否 |
| usernames | array | 要检索的代表用户名 | 否 |
| approval | object | 要检索的代表批准率 | 否 |
| approval.from | float | 批准率下限 | 否 |
| approval.to | float | 批准率上限 | 否 |
| forgedFees | object | 将被收回的制造代表费用 | 否 |
| forgedFees.from | int | 制造费用下限 | 否 |
| forgedFees.to | int | 制造费用上限 | 否 |
| forgedRewards | object | 要收回的制造代表奖励 | 否 |
| forgedRewards.from | int | 制造奖励下限 | 否 |
| forgedRewards.to | int | 制造奖励上限 | 否 |
| forgedTotal | object | 制造总计 | 否 |
| forgedTotal.from | int | 制造总计下限 | 否 |
| forgedTotal.to | int | 制造总计上限 | 否 |
| producedBlocks | object | 要检索的代表的生成区块数 | 否 |
| producedBlocks.from | int | 生成区块数的下限 | 否 |
| producedBlocks.to | int | 生成区块数的上限 | 否 |
| voteBalance | object | 要检索的代表投票数 | 否 |
| voteBalance.from | int | 投票数下限 | 否 |
| voteBalance.to | int | 投票数上限 | 否 |

### 举例

```text
curl --data 'producedBlocks={ "from": 41100 }' https://api.ark.io/api/delegates/search
```

```text
{
  "meta": {
    "count": 8,
    "pageCount": 1,
    "totalCount": 8,
    "next": null,
    "previous": null,
    "self": "/api/v2/delegates/search?page=1&limit=100",
    "first": "/api/v2/delegates/search?page=1&limit=100",
    "last": "/api/v2/delegates/search?page=1&limit=100"
  },
  "data": [
    {
      "username": "geops",
      "address": "DJpFwW39QnQvQRQJF2MCfAoKvsX4DJ28jq",
      "publicKey": "027716e659220085e41389efc7cf6a05f7f7c659cf3db9126caabce6cda9156582",
      "votes": 9241946380207,
      "rank": 9,
      "blocks": {
        "produced": 41226,
        "last": {
          "id": "c71bdf9695cadd91ac45483bf343e15c69b65590d866972023370707ce3b950b",
          "height": 1961065,
          "timestamp": {
            "epoch": 63998664,
            "unix": 1554096264,
            "human": "2019-04-01T05:24:24.000Z"
          }
        }
      },
      "production": {
        "approval": 0.07
      },
      "forged": {
        "fees": 124498624079,
        "rewards": 8205200000000,
        "total": 8329698624079
      }
    },
    ...
  ]
}
```



