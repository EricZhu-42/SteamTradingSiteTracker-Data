## SteamTradingSiteTracker - BotDetectionDataset

> To analyze the characteristics of bot traffic accessing www.iflow.work and facilitate research in related fields, we have cleaned and anonymized the access logs of www.iflow.work over a 14-day period. This dataset is now publicly released as an **unsupervised bot classification (anomaly detection) time series dataset**.

### Dataset Description

This dataset contains access logs from the backend API servers of www.iflow.work during the period from 2024-06-30 00:00 to 2024-07-14 00:00 (14 days, 336 hours in total).

The dataset includes **1,821,424** (approximately **1.82 million**) access records. Each record contains a user IP identifier, accessed endpoint, and query parameters. All data is sorted by timestamp in ascending order. 

The first 100 records are provided as a [preview](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/blob/main/BotDetectionDataset/BotDetectionDataset_examples.json), and the complete dataset can be downloaded [here](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/blob/main/BotDetectionDataset/BotDetectionDataset.zip) (ZIP format, 23.6MB compressed, 357MB JSON file when extracted, UTF-8 encoded).

> Due to the limited size of the log database and rolling deletion, the data provided here may not be complete.

### Data Collection and Preprocessing

In compiling this dataset, we performed the following preprocessing steps to improve data quality while protecting user privacy:

1. We removed all requests from Cloudflare-certified bots (mainly search engine crawlers, network mapping bots, etc.).
2. We removed all periodic requests from internal site monitoring systems.
3. We only recorded the timestamp and request parameters. Except for IP, no sensitive information involving user privacy (such as User-Agent, geolocation, language, etc.) is included. The IP addresses are salted and hashed, used only to identify users, making it impossible to recover the original IP.

### Data Fields

An example record in the dataset is as follows:

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
    },
    ...
]
```

The meaning of each field is as follows:

| Field Name  | Type                 | Description                                                  |
| ----------- | -------------------- | ------------------------------------------------------------ |
| `ip`        | `string`             | Salted hash of the user's IP, used to identify unique users  |
| `timestamp` | `int`                | Unix timestamp of when the request occurred                  |
| `channel`   | `"default" | "dev"`  | The interface used for the request. `default` indicates the old UI; `dev` indicates the new UI |
| `action`    | `"list" | "inspect"` | The endpoint requested. `list` queries information for multiple items meeting the `args` filter conditions; `inspect` queries details of a single item |
| `args`      | `dict` (`object`)    | Parameters for the request, detailed below                   |

When `action` is `list`, the `args` field includes:

| Field Name   | Type                                          | Description                           |
| ------------ | --------------------------------------------- | ------------------------------------- |
| `games`      | Subset of `["csgo", "dota2"]`                 | Games to search                       |
| `platforms`  | Subset of `["buff", "igxe", "c5", "uuyp"]`    | Third-party platforms to search       |
| `sort_by`    | `"buy" | "sell" | "safe_buy" | "median_sale"` | Sorting method                        |
| `min_volume` | `int`                                         | Minimum 24-hour trading volume filter |
| `min_price`  | `float`                                       | Lower price limit filter              |
| `max_price`  | `float`                                       | Upper price limit filter              |
| `page`       | `int`                                         | Page number for pagination            |

When `action` is `inspect`, the `args` field includes:

| Field Name | Type      | Description                                             |
| ---------- | --------- | ------------------------------------------------------- |
| `id`       | `int`     | ID of the item being queried                            |
| `success`  | `boolean` | Whether the item was successfully found in the database |

### Additional Notes

1. Most site users are in the UTC+8 time zone.

### Citation

To be determined
