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

## 关于三种“挂刀比例”的数据说明

1. 对于 `quick_price` 字段**大于 8 元**的饰品

    1. 最优寄售比例：以平台最低售价卖家购入，以 Steam Market 最低寄售价卖出
    2. 最优求购比例：以平台最低售价卖家购入，以 Steam Market 最高求购价卖出
    3. 稳定求购比例：以平台最低售价**三位**卖家的均价购入，以 Steam Market 最高求购价第三位的价格卖出

2. 对于 `quick_price` 字段**小于等于 8 元**的饰品
    1. 最优寄售比例：以平台最低售价**十位**卖家的均价购入，以 Steam Market 最低寄售价卖出
    2. 最优求购比例：以平台最低售价**十位**卖家的均价购入，以 Steam Market 最高求购价卖出
    3. 稳定求购比例：以平台最低售价**十位**卖家的均价购入，以 Steam Market 最高求购价第三位的价格卖出

## 数据规范更新记录

1. 自 2023.04.30 起，计算 `quick_price` 字段大于 8 元的饰品的稳定求购比例时，买入价采用平台最低售价三位卖家的均价（先前为价格最低的三位卖家中发货最快的卖家的价格；但部分平台不提供有意义的“发货速度”信息）
