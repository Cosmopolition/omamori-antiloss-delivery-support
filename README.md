# 没落下 / On Person / いっしょ · 隐私政策 & 支持中心

三语静态站点（纯 HTML + CSS，无框架、无构建步骤），通过 **GitHub Pages** 公开。
App Store 的「隐私政策网址」与「支持网址」都指向这里。

> 站点源码在本目录，但**它自己是一个独立的 Git 仓库**（有独立的 `.git` 与 remote）——
> 与 `eyecare/support` 同一个做法：内容要单独推到一个 public 仓库才能被 Pages 托管。

---

## 页面结构

```
support/
├── index.html          # 根重定向页（按浏览器语言 → ja/ zh/ en/）
├── privacy.html        # 隐私政策重定向页
├── support.html        # 帮助中心重定向页
├── css/
│   └── style.css       # 共享暗色仪表主题（配色取自 App 主题 A）
├── en/
│   ├── privacy.html    # 隐私政策（英文）
│   └── support.html    # 帮助中心（英文）
├── ja/
│   ├── privacy.html    # 隐私政策（日文）
│   └── support.html    # 帮助中心（日文）
└── zh/
    ├── privacy.html    # 隐私政策（中文）
    └── support.html    # 帮助中心（中文）
```

## 线上地址

| 本地化 | 隐私政策 | 支持 |
|---|---|---|
| zh-Hans | `https://cosmopolition.github.io/onperson-support/zh/privacy.html` | `https://cosmopolition.github.io/onperson-support/zh/support.html` |
| en-US | `https://cosmopolition.github.io/onperson-support/en/privacy.html` | `https://cosmopolition.github.io/onperson-support/en/support.html` |
| ja | `https://cosmopolition.github.io/onperson-support/ja/privacy.html` | `https://cosmopolition.github.io/onperson-support/ja/support.html` |

根路径的 `privacy.html` / `support.html` / `index.html` 按 `navigator.language` 自动分流
（`ja*` → ja/、`zh*` → zh/、其余 → en/），给「用户自己敲域名」和 App 内 WebView 用。

> ★ **商店页用各语言目录，不走根重定向** —— 描述是按语言写的，读者点进去就该看到同一种语言，
> 不该先闪一下再跳。

---

## 页面内容（基于 App 的真实技术边界，不是套模板）

### 隐私政策（9 节）

写的是这个 App **实际上**做了什么，每一条都能在源码里对上：

* **零收集、零上传** —— 全部 App 源码里没有一处 `URLSession` / `URLRequest` / 网络框架链接；
  不是「承诺不传」，是那段代码不存在。唯一例外是 App Store 的购买与恢复购买（走 StoreKit）。
* **只问两个权限** —— 蓝牙（始终，Info.plist 的 `NSBluetoothAlwaysUsageDescription` 原文照抄）
  与通知（**仅手表端**，`WatchNotificationService.requestAuthorization`）。
  位置 / 摄像头 / 麦克风 / 追踪（ATT）/ 健康 / 键盘 —— 全部不申请。
* **记了什么，有一张表** —— 事件记录（≤50 条）、设置、守护状态（当前值，不是历史），
  全在 App Group 容器 `group.com.nearby.antiloss`（`Shared/Store/SharedStore.swift`）。
* **事件记录的字段逐个列了** —— `id / timestamp / kind / note`（`Shared/Model/GuardEvent.swift`），
  九种 kind 全部列出，并明说**里面没有**：位置坐标、位置历史、信号强度时序、设备清单、广告标识符。
* **RSSI 不是位置** —— 单开一节讲清楚「信号强度是无线电数值，不是坐标」。
* **不加密是明说的** —— 明文换取「你随时能自己打开核对」，代价写清楚，不假装有。
* **儿童隐私 / App Store 隐私标签 / 政策变更 / 你的权利** —— 四节各一条可执行的路径。

### 帮助中心

* 是什么（一句话 + 三个核心功能卡片：守护 / 分离报警 / 静默策略 / 连接自检）
* **10 条 FAQ**，刻意以「为什么不响 / 怎么让它一定响 / 会不会误报 / 怎么恢复」为主 ——
  这是这个 App 用户最先想确认的事。
  每条 FAQ 的答案都取自 App 自己的实现（宽限 30 s、阈值 −72 dBm、六条静默规则、
  四项自检、后台约 10～15 分钟唤醒一次）。

---

## 视觉语言

* **App 是暗的，站点也暗** —— 用户从 App 打开链接，看到同一个视觉体系。
  配色 token 直接搬 `docs/03-visual-spec.md` 主题 A：
  底 `#070A0F` / 面板 `#0E141C` / 抬起 `#151D27` / 结构线 `#2A3B4E` /
  正文 `#E8EFF6` / 次要 `#9DB2C6` / 丝印 `#6A7F94` / 信号色 `#38E0C6` / 警告 `#F2B33D`。
* **三条纪律跟着 App 走**：零渐变、零阴影、3px 直角；丝印标签用等宽字体 + 大写字距。
* 列表标记是**小方块**（App 隐私屏上的 ▪ 同款），不是圆点。
* 主按钮 = App 里的「让手机响」：实心信号色 + 深色字。
* 字体栈含 `PingFang SC` / `Noto Sans CJK SC` / `Hiragino Sans` / `Yu Gothic`，中日文都能正常渲染。
* `<details>` / `<summary>` 实现 FAQ 手风琴交互。

---

## 语言切换

页面右上角顺序统一为 **EN | 中文 | 日本語**，当前页高亮。
**语言名恒用各自母语写法** —— 英文页上也写「中文」「日本語」，不写 Chinese / Japanese。

新增语言时：加 `xx/privacy.html` 与 `xx/support.html` 两份，顶部 logo 与 header 结构照抄现有一页即可。

---

## 内容纪律

三语成稿都过一遍项目自己的语言漂移规则（`store/aso/description/check_desc.py` 里的
字符级 + 词级规则，直接复用，不另立一套）：

* 简体独有字 / 日文新字体 / 假名 —— 串进另一种语言就抓
* 词级（共享汉字拼出来的中文残句）—— 字符级抓不到的那种
* **非目标语言残留**（韩文 / 西里尔 / 不该出现的拉丁词）也扫

> 这一轮就靠它抓到并修掉了日文稿里的真实串味：
> 简体字「设」、韩文「저장 / 접근 / 아닙니다」、西语「aquí」、英文残片「fetcher / content / generals / Account / \emph{}」。

---

## 部署

### GitHub Pages

1. 把仓库设为 **public**
2. **Settings → Pages** → Source 选 `main` branch、`/ (root)` 目录 → Save
3. 站点会在 `https://cosmopolition.github.io/onperson-support/` 上线

### 推送到 GitHub

```bash
cd support
git add -A
git commit -m "初始：隐私政策与支持中心（中英日）"
git push -u origin main
```

### 自定义域名（可选）

仓库根目录加 `CNAME` 文件写上域名，再在域名服务商处配置 CNAME 指向 `<org>.github.io`。

### 本地预览

```bash
cd support
python3 -m http.server 8000
# http://localhost:8000  → 按浏览器语言自动跳到对应语言
```

---

## 联系

Email: peer2peer.wang@gmail.com
