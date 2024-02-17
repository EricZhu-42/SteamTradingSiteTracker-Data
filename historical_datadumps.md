# Historical Datadumps

[DataDumps](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/tree/main/DataDumps) 目录下包含 2022/04/18 - 2024/02/14 期间 iflow.work 站点 `DATA` 数据库的完整内容。

Data dumps 将作为 _SteamBuffSnapshot_ 数据集的补充，便于开发者在更长的时间周期内进行数据分析。

## 关于三种“挂刀比例”的说明

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
