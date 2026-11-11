# tvbox

TVBox 多仓索引仓库，只放两个文件。

## 文件

| 文件 | 说明 |
| --- | --- |
| `feng.json` | 多仓索引：`urls` 数组，每条 `{ "url": 配置地址, "name": 显示名 }` |
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

## 当前线路（11 条，2026-11-11 实测可用）

| 名称 | 类型 | 备注 |
| --- | --- | --- |
| 锅大侠 | JSON | 严格 JSON，sites=71 |
| wwb521 | JSON | 严格 JSON，sites=12 |
| PG one | JSON | 严格 JSON，sites=298 |
| 肥猫 | JSON | 带 `//` 注释，sites=234 |
| XYQTVBox | JSON | 带注释，sites=48 |
| 分享者18+ | JSON | 带注释，sites=3 |
| 二哈18+ | JSON | 带注释，sites=125 |
| 星云线路 | JSON | 带注释，sites=1045 |
| 扛把子线路 | JSON | BOM+`#` 注释，sites=153 |
| Huhujun线路 | JSON | 严格 JSON，sites=87 |
| bizhangjie | JSON | 严格 JSON，sites=113 |

已剔除：`agit.ai` 全域（6 条统一回 114 字节 lander 页）、notabug 404、`tv.lan2wan.top` 反盗链页，以及 2 条重复项。

## 增删

```bash
# 校验仍是合法 JSON
python3 -m json.tool feng.json > /dev/null && echo ok

# 追加一条
python3 - <<'PY'
import json
d = json.load(open("feng.json"))
d["urls"].append({"url": "https://example.com/config.json", "name": "新线路"})
json.dump(d, open("feng.json", "w"), ensure_ascii=False, indent=2)
PY
```

注意：多仓索引本身的字段是 `urls`；被引用的每个地址内部才是 `sites` / `spider` / `lives` / `parses` 那种单仓配置。混了就会加载失败。
