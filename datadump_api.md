# Public Datadump API

我们公开提供 iflow.work 站点 `priority` 数据库的 Dadadump，具体介绍请见：[README](https://github.com/EricZhu-42/SteamTradingSiteTracker-Data/blob/main/README.md)

Datadump 的获取通过以下的两个 API 完成：

## 列出 Datadump 文件

GET https://api.iflow.work/export/list?dir_name=priority_archive

样例输出：

```json
{
    "files":[
        "2024-02-13-00-15.zip",
        "2024-02-13-12-15.zip",
        "...",
        "2024-02-17-12-15.zip"
    ],
    "success":true
}
```

此处 JSON 中的 `2024-02-13-00-15.zip` 等即为 Datadump 文件名，表示该文件导出的具体时间

## 下载 Datadump 文件

GET https://api.iflow.work/export/download?dir_name=priority_archive&file_name=FILENAME

- 将 FILENAME 替换为具体的 Datadump 文件名即可
- 例如：https://api.iflow.work/export/download?dir_name=priority_archive&file_name=2024-02-13-00-15.zip

通过程序发起下载请求时，请允许请求进行 301 重定向跳转。
