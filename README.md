# tvbox

TVBox 配置仓库，只放两个文件。

## 文件

| 文件 | 说明 |
| --- | --- |
| `feng.json` | TVBox 单仓配置：`sites` 站点、`lives` 直播、`parses` 解析、`flags` 播放器标识 |
| `README.md` | 本说明 |

## 订阅

TVBox → 设置 → 配置地址，填 raw 地址：

```
https://raw.githubusercontent.com/mxcoo/tvbox/main/feng.json
```

国内直连不顺时用加速前缀：

```
https://gh-proxy.com/https://raw.githubusercontent.com/mxcoo/tvbox/main/feng.json
```

## 改配置

1. `YOUR_API_HOST` / `YOUR_PARSE_HOST` 换成自己的源地址。
2. `spider` 留空表示不用 csp jar；用 csp 源时填 `jar地址;md5;32位md5`。
3. `lives[].url` 指向 m3u 直播源，可以是本地相对路径，也可以是完整 URL。
4. 改完校验：`python3 -m json.tool feng.json > /dev/null && echo ok`

## 字段要点

- `type`：`0` JSON 接口，`1` XML 接口（苹果CMS），`3` csp/网页源（需 `spider` jar）。
- `quickSearch`：聚合源多时只给主源开，否则一次搜索很慢。
- `parses[].ext.flag`：解析适用的站点标识，与 `flags` / 站点 `key` 对齐。
