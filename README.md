# SteamTradingSiteTracker-Data

Datadumps/Datasets for SteamTradingSiteTracker (www.iflow.work)

## :star: NEWS

- [2024/07/30] We released a [dataset](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/tree/main/BotDetectionDataset) for unsupervised bot classification. (我们发布了一份无监督机器人流量识别数据集）
- [2024/02/13] 我们开始通过 Cloudflare R2 进行 Datadump 文件的分发

## Data Dumps

> 截至 2024/02/14，本仓库的 Datadump 文件已经占据了约 10GB 的存储空间。
>
> 为了减少对 GitHub 存储空间的占用，自 2024/02/14 起，我们停止将 Datadump 上传至本仓库，直接通过 iflow.work 站点进行 Datadump 文件的分发。

### 2022/04/18 - 2024/02/14

[DataDumps](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/tree/main/DataDumps) 目录下包含了 2022/04/18 - 2024/02/14 期间 iflow.work 站点 `DATA` 数据库的 Datadump 数据。

`DATA` 数据库包含约 15000 种动态筛选出的，挂刀比例较低的饰品的交易数据。饰品列表及数据 24 小时动态更新，Datadump 每 12 小时导出一次。

其他信息详见：[historical_datadumps](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/blob/main/historical_datadumps.md)

### 2024/02/13 - 至今

在 iflow.work 站点数据库重构后，我们继续公开提供与原先的 `DATA`  数据库相对应的 `priority` 数据库的 Datadump 存档下载。

我们从所有约 60000 个 Dota2 & CS2 饰品中，动态筛选出 3000 个最适合挂刀的饰品（即：交易量大，挂刀比例低）的饰品储存于 `priority` 数据库中，保持较高的更新频率，以此为 iflow.work 的用户提供及时、准确的挂刀数据信息。

相关数据时效性如下（所有时间均为 UTC+8）：

- `priority` 数据库的饰品列表自每天 03:15 时起，每 8 小时更新一次

- `priority` 数据库的 Datadump 存档自每天 00:15 起，每 12 小时更新一次

  - 即：每天 00:15, 12:15 生成并上传当前时刻的 Datadump

具体下载方式详见：[datadump_api](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/blob/main/datadump_api.md)

## Datasets

### SteamBuffSnapshot

> 发布日期：2022/02/14

为了获得最优的饰品筛选规则，以获得包含尽可能多低比例饰品且尽量小的饰品追踪列表，本项目构造了 [SteamBuffSnapshot](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/tree/main/SteamBuffSnapshot) 数据集。

该数据集包含了 2022 年 2 月 14 日 BUFF 平台 dota2 与 csgo 所有饰品的价格数据与对应的 Steam Market 数据，共计 **38075** 条。

### BotDetectionDataset

> 发布日期：2024/07/30

为了分析访问 www.iflow.work 站点的爬虫流量特征，便于相关领域的研究，我们将 www.iflow.work 在一个 14 天时间段内的访问事件清洗、脱敏后作为一个无监督分类（异常检测）的时序数据集公开发布。
