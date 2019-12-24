# 对等体

对等资源与节点资源非常相似，但是仅公开所连接对等设备的IP和端口。 递归遍历此API及其响应使您可以检查整个网络。

## 对等体列表

返回节点已知的所有对等点。这些不一定都是对等体;这里只出现公共节点。

### 接口

```text
GET /api/peers
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| page | int | 将返回页面编号 | 否 |
| limit | int | 每页的资源数量 | 否 |
| port | int | 筛选资源的端口 | 否 |
| status | string | 筛选资源的状态 | 否 |
| os | string | 用于过滤资源的操作系统 | 否 |
| version | string | 筛选资源的节点版本 | 否 |
| orderBy | string | 资源排序所依据的列 | 否 |

### 反应

```text
{
  "meta": {
    "count": 2,
    "pageCount": 1,
    "totalCount": 2,
    "next": null,
    "previous": null,
    "self": "/v2/peers?page=1",
    "first": "/v2/peers?page=1",
    "last": "/v2/peers?page=1"
  },
  "data": [
    {
      "ip": "167.114.29.53",
      "port": 4001,
      "version": "2.0.16",
      "height": 6881793,
      "status": 200,
      "os": "linux",
      "latency": 1390
    }
  ]
}
```

## 检索对等

特定的对等方可以通过IP地址找到。 请注意，同位体可能禁用了其公共API，因此只能通过p2p 内部API才能访问它们。

### 接口

```text
GET /api/peers/{ip}
```

### 查询参数

| 名称 | 类型 | 描述 | 是否必填 |
| :--- | :--- | :--- | :--- |
| ip | string | 要检索的对等点的IP地址 | 是 |

### 反应

```text
{
  "data": {
    "ip": "167.114.29.55",
    "port": 4001,
    "version": "2.0.16",
    "height": 6881793,
    "status": 200,
    "os": "linux",
    "latency": 355
  }
}
```



