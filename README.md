# tvbox

TVBox 多仓索引仓库，只放两个文件。

## 文件

| 文件 | 说明 |
| --- | --- |
| `feng.json` | 多仓索引：`urls` 数组，每条 `{ "url": 配置地址, "name": 显示名 }` |
| `README.md` | 本说明 |

## 订阅

TVBox → 设置 → 配置地址：

```
https://raw.githubusercontent.com/mxcoo/tvbox/main/feng.json
https://gh-proxy.com/https://raw.githubusercontent.com/mxcoo/tvbox/main/feng.json   # 国内加速
```

## 线路清单（27 条，2026-11-11 全量实测）

### 前排：新增可用 14 条

| 名称 | sites |
| --- | --- |
| 王小二放牛娃新接口 | 100 |
| 哈基米 | 172 |
| 动漫城接口 | 27 |
| 俊佬接口 | 24 |
| HG接口 | 10 |
| dxawi | 48 |
| 小盒子单仓 | 54 |
| 真心 | 43 |
| 分享 | 162 |
| 短剧 | 35 |
| 东篱线路 | 93 |
| 嗷呜线路 | 80 |
| L佬线路 | 45 |
| 苹果CMS资源站 | 21 |

### 原有 11 条（香雅情、高天流云为同源合并后的名称）

锅大侠 71 · wwb521 12 · 肥猫 234 · 分享者18+ 3 · 二哈18+ 125 · 星云线路 1045 · 扛把子线路 153 · Huhujun线路 87 · bizhangjie 113，另有香雅情 48、高天流云 298。

### 末尾 2 条：格式需修复

| 名称 | sites | 问题 |
| --- | --- | --- |
| 小盒子4K | 53 | JSON 内混入 `//////` 注释与非标准键、字符串里有裸换行 |
| 宝盒VIP | 144 | `{"key":爱迪V2,...}` 键值未加引号 |

严格解析器直接失败；剥离注释、转义裸换行、给未加引号的值补引号后可正常解析。客户端若不认，删掉这两条即可。

## 未收录（8 条）

| 原地址 | 实际返回 |
| --- | --- |
| `www.饭太硬.net/tv` | HTML 首页，页内线索 `cdn.qiaoji8.com/tvbox.json` 本机 DNS 不可达 |
| `肥猫.net` | HTML 首页，页内线索 `9877.kstore.space/sun.json` 返回 403 |
| `我不是.摸鱼儿.top` | HTML 首页，无 json 线索 |
| `tvbox.王二小放牛娃.top` | GBK 文本页，列出多个接口地址，本身不是配置 |
| `tv.菜妮丝.top` | HTML 首页，无 json 线索 |
| `cdn.gitmirror.com/bb/xduo/...` | 域名 DNS 失效；GitHub 上 `bb/xduo` 404 |
| `yoursmile66/TVBox/main/XC.json` | 直连与 gh-proxy 版均被链路切断 |
| `pastebin` 之外的 `南风接口` 原址 | 返回 hex 密文串，非明文配置 |

## 增删

```bash
python3 -m json.tool feng.json > /dev/null && echo ok
```

多仓索引自身字段是 `urls`；每条被引用地址内部才是 `sites` / `spider` / `lives` / `parses` 那种单仓配置，混了就会加载失败。
