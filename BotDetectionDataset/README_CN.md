# SteamTradingSiteTracker - BotDetectionDataset

> English version of this document can be found [HERE](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/tree/main/BotDetectionDataset).

> 为了分析访问 www.iflow.work 站点的爬虫流量特征，便于相关领域的研究，我们将 www.iflow.work 在一个 14 天时间段内的访问事件清洗、脱敏后作为一个无监督分类（异常检测）的时序数据集公开发布。

## 数据集描述

该数据集为 www.iflow.work 在 2024-06-30 00:00 至 2024-07-14 00:00 期间（共 14 天、336 小时）后端 API 服务器收到的查询请求。

数据集共包含 1821424（约 182 万）条查询记录，字段包含用户的 IP 标识符、访问端点及查询参数。所有数据按事件时间戳由小到大排序，其中前 100 条数据作为[预览](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/blob/main/BotDetectionDataset/BotDetectionDataset_examples.json)，完整数据可在[此处](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/blob/main/BotDetectionDataset/BotDetectionDataset.zip)下载（ZIP 格式，解压前 23.6MB，解压后为 357MB 的 JSON 文件，采用 UTF-8 编码）

> 由于日志数据库大小有限且滚动擦除，此处提供的数据不保证完整。

## 数据收集及预处理

在整理数据集的过程中，我们对数据进行了如下预处理，以在提高数据集质量的同时保护用户隐私：

1. 我们去除了所有由 Cloudflare 认证的机器人（主要为搜索引擎爬虫、网络测绘机器人等）发起的请求
2. 我们去除了所有内部站点监控发起的定期请求
3. 我们仅记录请求发生的时间戳及请求参数，除 IP 外不包含任何涉及用户隐私的敏感信息（如 UA、地理位置、语言等）；IP 则在加盐后进行哈希，仅用于标识用户，无法恢复真实用户 IP

## 数据字段

数据集内的记录样例如下：

```json
[
    {
        "ip": "9305465e7400e55271429e2523e023f8",
        "timestamp": 1719676800,
        "action": "list",
        "channel": "default",
        "args": {
            "games": [
                "csgo",
                "dota2"
            ],
            "platforms": [
                "buff",
                "igxe",
                "c5",
                "uuyp"
            ],
            "sort_by": "buy",
            "min_volume": 10,
            "min_price": 1.0,
            "max_price": 5000.0,
            "page_size": 50,
            "page": 1
        }
    },
    {
        "ip": "9bf358042b094558f58eb97eb0237906",
        "timestamp": 1719676800,
        "action": "inspect",
        "channel": "default",
        "args": {
            "id": 156140149,
            "success": true
        }
    }
]
```

其中，每个字段的大致含义如下：

| 字段名      | 类型                 | 描述                                                         |
| ----------- | -------------------- | ------------------------------------------------------------ |
| `ip`        | `string`             | 用户 IP 加盐后的哈希值，用于标识用户                         |
| `timestamp` | `int`                | 用户请求发生的时间戳                                         |
| `channel`   | `"defalut" \| "dev"`  | 用户发起请求的方式，其中 `default` 表示用户请求是过旧版 UI 发起；`dev` 表示用户请求通过新版 UI 发起 |
| `action`    | `"list" \| "inspect"` | 用户请求的端点，其中 `list` 表示用户查询所有满足 `args` 筛选条件的物品信息；`inspect` 表示用户查询满足 `args` 条件的单个物品详情 |
| `args`      | `dict` (`object`)    | 请求所需的参数，具体含义见下方                               |

其中，`action` 为 `list` 时，`args`  字段包括：

| 字段名       | 类型                                          | 描述                   |
| ------------ | --------------------------------------------- | ---------------------- |
| `games`      | `["csgo", "dota2"]` 的子集                    | 筛选游戏               |
| `platforms`  | `["buff", "igxe", "c5", "uuyp"]` 的子集       | 筛选第三方平台         |
| `sort_by`    | `"buy" \| "sell" \| "safe_buy" \| "median_sale"` | 设置排序方式           |
| `min_volume` | `int`                                         | 筛选 24 小时最小交易量 |
| `min_price`  | `float`                                       | 筛选物品价格下限       |
| `max_price`  | `float`                                       | 筛选物品价格上限       |
| `page`       | `int`                                         | 翻页页数               |

`action` 为 `inspect` 时，`args`  字段包括：

| 字段名    | 类型      | 描述                         |
| --------- | --------- | ---------------------------- |
| `id`      | `int`     | 用户查询的物品的 ID          |
| `success` | `boolean` | 该物品是否成功在数据集中找到 |

## 其他说明

1. 站点大部分用户位于 UTC+8 时区

## 引用格式

待定
