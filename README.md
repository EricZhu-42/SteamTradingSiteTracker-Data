# SteamTradingSiteTracker-Data
Datadumps/Datasets for SteamTradingSiteTracker (www.iflow.work)

## 数据仓库
为了方便在主仓库上的 clone, watch 等操作，与数据集相关的文件自 2022/07/01 起被迁移至独立的[数据仓库](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data)。

## 数据集

为了获得最优的饰品筛选规则，以获得包含尽可能多低比例饰品且尽量小的饰品追踪列表，本项目构造了 [SteamBuffSnapshot](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/tree/main/SteamBuffSnapshot) 数据集。

该数据集包含了 2022 年 2 月 14 日 BUFF 平台 dota2 与 csgo 所有饰品的价格数据与对应的 Steam Market 数据，共计 **38075** 条。

## Data Dumps

从 2022/4/25 起，可以在 [DataDumps](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/tree/main/DataDumps) 目录下获取 7 天前的 DATA 数据库的完整内容。

Data dumps 将作为 _SteamBuffSnapshot_ 数据集的补充，便于开发者在更长的时间周期内进行数据分析。
