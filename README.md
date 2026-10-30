<p align="center">
  <img src="https://chaohuiguan.pages.dev/assets/icon.png" width="88" alt="超会管图标" />
</p>

<h1 align="center">超会管</h1>

<p align="center">让每一笔资产都清晰可见</p>

<p align="center">
  <img alt="Flutter" src="https://img.shields.io/badge/Flutter-3.x-02569B?logo=flutter&logoColor=white" />
  <img alt="Android" src="https://img.shields.io/badge/Android-arm64-3DDC84?logo=android&logoColor=white" />
  <img alt="Version" src="https://img.shields.io/badge/version-1.3.7-F5C242" />
  <img alt="Local-first" src="https://img.shields.io/badge/local--first-%E6%95%B0%E6%8D%AE%E4%B8%8D%E4%B8%8A%E4%BA%91-F5C242" />
</p>

超会管是一款**本机优先**的私人资产管家：股票、贵金属、房产车位、现金账户、借贷往来，一屏看清净资产。没有账号体系，不接第三方统计与推送，记账内容默认只留在本机；可以加应用锁加密数据库，也可以备份到你自己的 WebDAV。

> A local-first personal net-worth manager for Android, built with Flutter.

<p align="center">
  <a href="https://oss.f2e.me/app/chaohui.guan-v1.3.7-arm64.apk"><b>下载 Android 版（arm64，约 25 MB）</b></a>
</p>

## 截图

| 概览 | 持仓 | 分析 | 设置 |
| :---: | :---: | :---: | :---: |
| <img src="https://chaohuiguan.pages.dev/assets/overview.png" width="220" alt="概览" /> | <img src="https://chaohuiguan.pages.dev/assets/stock.png" width="220" alt="持仓" /> | <img src="https://chaohuiguan.pages.dev/assets/analysis.png" width="220" alt="分析" /> | <img src="https://chaohuiguan.pages.dev/assets/settings.png" width="220" alt="设置" /> |
| 总资产、净资产、资产构成、本月收支 | 七类资产分页管理，表头排序 | 账面收益、盈亏结构与分类收益 | 主题、货币、安全、备份与更新 |

## 功能

### 一屏看清净值

- 总资产领衔，净资产与总负债分列，附负债率。
- 资产构成按分类拆开，颜色与持仓页一致。
- 本月收支按借贷还款计划汇总：借出计划还款算收入，借入计划还款算支出。

### 七类资产，一本账

- **股票**：美股 / 港股 / A 股，输代码查询行情后填数量与成本；列表展示市值、现价、持仓盈亏。
- **贵金属**：黄金按克、白银按千克记录重量与成本价，行情按当日一次拉全。
- **固定资产**：房产、车辆、其它，类别可自填，支持多币种，记购入价与当前估值。
- **流动资金**：现金、储蓄、网络账户按类别记余额。
- **应收款 / 应付款**：私人、机构 × 借出、借入，同一主体下挂多笔借贷，各自独立计息。
- **其他**：收藏品等不好归类的资产。
- 分类左右滑动切换，表头点按排序，分类顺序可拖动自定义（「其他」固定最后）。

### 借贷，不只记一笔

- 四种还款方式：等额本金、等额本息、先息后本、按月还息到期还本。
- 本金、利率（日 / 月 / 年）、违约金（%/天）、起止日期、每月还款日。
- 完整还款计划，每期标注已还 / 部分 / 逾期 / 本月无还款项。
- 记还款默认按「违约金 → 利息 → 本金」扣款，也可只还其中一项；保存前实时预览拆分，支持免除本期违约金。
- 利息按「剩余本金 × 年化 ÷ 365 × 天数」计提，逾期金额按天计违约金；删除还款后自动重算。

### 分析

- 账面收益 = 持仓浮动盈亏 + 借贷已计利息，人民币口径。
- 盈亏结构、各类资产收益率、盈亏贡献排行。
- 借贷质量与逾期统计，缺汇率的持仓会明确标注而不是静默漏算。

### 多币种与行情

- 人民币为基准，内置 26 种货币，可添加带国旗的外币。
- 汇率每日拉取一次并缓存，离线也能折算；总资产与账面收益保留完整数字，列表金额默认万 / 亿缩写。
- 行情只在需要时联网，查过即缓存；断网照样能看、能算。

### 隐私与安全

- **无账号、无广告、无第三方统计与推送**，记账内容不上传。
- 数据库是应用私有目录里的单个 SQLite 文件，不写相册、不建外部目录。
- **应用锁即数据库加密**：4–16 位密码经 PBKDF2-HMAC-SHA256 派生 30,000 次得到 32 字节密钥，交给 SQLCipher 直接加密数据库；忘记密码谁也打不开，包括开发者。
- 支持指纹解锁；指纹免密有 3 天宽限期，避免把密码彻底忘掉。
- 退到后台后重新上锁的延迟可选：立即 / 1 / 5 / 10 / 30 分钟，默认 5 分钟。
- **WebDAV 备份**：上传数据库到你自己配置的空间；恢复时逐表合并、不整体覆盖，合并前自动留一份 `.bak` 快照。

### 体验细节

- 深色 / 浅色 / 跟随系统，深色为纯黑底 + 蜂蜜黄主色。
- 涨跌配色可在「红涨绿跌」与「绿涨红跌」之间切换，只影响涨跌数字。
- 底部菜单是自绘的液态玻璃材质（Fragment Shader + 实时折射）。
- 按 390pt 设计稿等比缩放，并锁定竖屏，窄屏和大屏都不跑版。
- 启动时静默检查更新清单，有新版本时提示下载安装。


## 免责声明

本应用仅用于个人资产记录与测算，不构成任何投资、借贷或税务建议。行情与汇率可能存在延迟或误差，请以券商、银行等官方数据为准。卸载应用或清除数据前请先做好备份。

## 联系

- 邮箱：service@chaohui.app
- 包名：`com.chaohui.guan`
