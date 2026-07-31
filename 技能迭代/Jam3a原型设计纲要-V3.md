# Jam3a 原型设计纲要（V3 基准）

## 文档定位

本文件是Jam3a原型的设计蓝图，记录V3版本确立的完整设计体系。核心用途：

- **小调整**：直接修改原型文件，更新本纲要中对应部分
- **大重构**：以本纲要为唯一设计规范源，重新生成原型时确保观感一致
- **新人上手**：快速理解当前原型的设计语言，无需逐页分析代码

---

## 一、设计理念

### 核心关键词
**竞技荣耀 · 深空神秘 · 奢华克制**

### 设计哲学
- **暗色为底，金色为魂**：深空黑作为主背景，金色作为品牌识别色，形成强烈的视觉记忆点
- **紫色点缀**：辅助品牌色，用于区分层级、增加神秘感
- **光效克制**：发光效果仅用于关键交互（选中态、CTA按钮、稀有奖励），避免光污染
- **Orbitron字体定调**：科技感标题字体，强化"竞技平台"属性
- **Emoji图标体系**：原型阶段使用Emoji作为功能图标，降低设计资源依赖

### 对标参考
- **竞技感**：参考Riot Games（Valorant）、暴雪（Overwatch）的深色金属质感
- **奢华感**：参考中东高端品牌（金色+紫色组合）
- **社区感**：参考Discord的功能布局思路

---

## 二、色彩体系

### 2.1 CSS变量（直接复用）

```css
:root {
  /* 背景色 */
  --bg-black: #0a0a0f;       /* 最深背景，页面底色 */
  --bg-dark: #12121a;         /* 次级背景，输入框、资产栏 */
  --bg-card: #1a1a24;         /* 卡片背景 */
  --bg-card-2: #20202c;       /* 卡片Hover背景 */
  --bg-elevated: #252533;     /* 更高层级背景，Ghost按钮 */

  /* 品牌色 */
  --gold: #FFD700;            /* 金色主色 */
  --gold-dim: #c9a700;        /* 金色暗色 */
  --gold-glow: rgba(255, 215, 0, 0.35); /* 金色发光 */
  --purple: #9D4EDD;          /* 紫色主色 */
  --purple-glow: rgba(157, 78, 221, 0.35); /* 紫色发光 */
  --purple-dim: #7b2cbf;      /* 紫色暗色 */

  /* 文字色 */
  --text-primary: #ffffff;    /* 主文字 */
  --text-secondary: #a0a0b0;  /* 副文字 */
  --text-muted: #6b6b80;      /* 弱化文字 */

  /* 功能色 */
  --green: #2ecc71;  /* 成功/在线 */
  --red: #e74c3c;    /* 错误/危险 */
  --orange: #e67e22; /* 警告/限时 */
  --blue: #3498db;   /* 信息/链接 */

  /* 边框色 */
  --border-gold: rgba(255, 215, 0, 0.25);
  --border-purple: rgba(157, 78, 221, 0.25);
  --border-subtle: rgba(255, 255, 255, 0.08);

  /* 阴影 */
  --shadow-card: 0 2px 12px rgba(0, 0, 0, 0.5);
  --shadow-gold: 0 0 20px rgba(255, 215, 0, 0.3);
  --shadow-purple: 0 0 20px rgba(157, 78, 221, 0.3);

  /* 圆角 */
  --radius-sm: 8px;   /* 小元素：按钮、输入框、标签 */
  --radius-md: 12px;  /* 卡片、列表项 */
  --radius-lg: 16px;  /* 大卡片、弹窗 */
  --radius-xl: 20px;  /* Banner、特殊容器 */

  /* 尺寸常量 */
  --navbar-h: 52px;      /* 顶部导航栏 */
  --tabbar-h: 62px;      /* 底部Tab栏 */
  --statusbar-h: 28px;   /* 状态栏 */
}
```

### 2.2 色彩使用规则

| 用途 | 颜色 | 说明 |
|------|------|------|
| 页面背景 | `--bg-black` | 永远是最底层 |
| 卡片/容器 | `--bg-card` | 比背景亮一级 |
| 输入框 | `--bg-dark` | 输入区域用暗色 |
| 主CTA按钮 | `--gold` 渐变 | 最重要的操作 |
| 次要CTA按钮 | `--purple` 渐变 | 辅助重要操作 |
| 选中态 | `--gold` | 当前激活项 |
| 分隔线 | `--border-subtle` | 极弱的分隔 |
| 强调边框 | `--border-gold` / `--border-purple` | 用于重要卡片 |
| 禁用态 | `--bg-elevated` + `--text-muted` | 灰色不可操作 |

### 2.3 渐变使用规范

```css
/* 金色渐变 - 用于主按钮、Banner金色版 */
background: linear-gradient(135deg, var(--gold) 0%, #ffaa00 100%);

/* 紫色渐变 - 用于紫色按钮 */
background: linear-gradient(135deg, var(--purple) 0%, var(--purple-dim) 100%);

/* 页面底色（body） */
background: linear-gradient(135deg, #0a0a12, #12121f);

/* 引导页底色 */
background: radial-gradient(circle at 50% 40%, #1a0a2e 0%, #0a0a0f 70%);

/* Banner紫色版 */
background: linear-gradient(135deg, #1a0a2e 0%, #16213e 50%, #0f3460 100%);

/* Banner金色版 */
background: linear-gradient(135deg, #2e1a0a 0%, #3e2723 50%, #1a1a00 100%);

/* 段位徽章 */
rank-bronze:  linear-gradient(135deg, #cd7f32, #8b4513);
rank-silver:  linear-gradient(135deg, #c0c0c0, #808080);
rank-gold:    linear-gradient(135deg, #FFD700, #b8860b);
rank-platinum:linear-gradient(135deg, #00dede, #008080);
rank-diamond: linear-gradient(135deg, #b9f2ff, #4682b4);
rank-master:  linear-gradient(135deg, var(--purple), var(--purple-dim));
```

---

## 三、字体系统

### 3.1 字体家族

| 用途 | 字体 | 备选 |
|------|------|------|
| 标题（英文） | Orbitron | sans-serif |
| 正文（英文） | Inter | sans-serif |
| 正文（中文） | Noto Sans SC | sans-serif |
| 数字（特殊） | Orbitron | 用于倒计时、段位数字 |

### 3.2 加载方式

```html
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@500;700;900&family=Inter:wght@400;500;600;700&family=Noto+Sans+SC:wght@400;500;700&display=swap" rel="stylesheet">
```

### 3.3 字号层级

| 层级 | 大小 | 字重 | 字体 | 使用场景 |
|------|------|------|------|----------|
| H1 | 42px | 900 | Orbitron | 引导页Logo |
| H2 | 20px | 700 | Orbitron | 引导页标题 |
| H3 | 18px | 700/900 | Orbitron | Banner标题 |
| H4 | 16px | 700 | Orbitron | 导航栏标题 |
| Section | 14px | 700 | Orbitron | 模块标题（金色） |
| Body | 14px | 500 | Inter | 正文、列表标题 |
| Body-S | 13px | 400 | Inter | 次要描述 |
| Caption | 12px | 400 | Inter | 辅助说明 |
| Small | 10-11px | 500 | Inter | 标签、Tab文字 |

### 3.4 文字颜色规则

- **主标题**：`--text-primary`（#ffffff）
- **正文**：`--text-primary`（#ffffff）
- **描述**：`--text-secondary`（#a0a0b0）
- **辅助/禁用**：`--text-muted`（#6b6b80）
- **模块标题**：`--gold`（#FFD700）+ Orbitron
- **金色按钮文字**：#1a1a00（深色，确保对比度）
- **紫色按钮文字**：#ffffff

---

## 四、组件库

### 4.1 按钮（Button）

```css
/* 基础按钮 */
.btn {
  display: inline-flex; align-items: center; justify-content: center;
  gap: 8px; border: none; border-radius: var(--radius-sm);
  font-family: 'Inter', sans-serif; font-size: 14px; font-weight: 600;
  cursor: pointer; transition: all 0.2s ease;
  text-decoration: none; white-space: nowrap;
}

/* 变体 */
.btn-primary   /* 金色渐变填充，深色文字，金色发光 */
.btn-purple    /* 紫色渐变填充，白色文字，紫色发光 */
.btn-secondary /* 透明背景，金色边框，金色文字 */
.btn-ghost     /* 深灰背景(elevated)，白色文字 */
.btn-danger    /* 红色背景，白色文字 */

/* 尺寸 */
.btn-sm  /* 6px 14px, 12px字号 */
.btn-md  /* 10px 20px, 13px字号 */
.btn-lg  /* 14px 24px, 15px字号, 100%宽度, md圆角 */
.btn-icon/* 36x36, 圆形 */

/* 禁用态 */
.btn:disabled, .btn-disabled { bg:elevated, color:muted, shadow:none, cursor:not-allowed }
```

**使用规则**：
- 每屏最多1个`.btn-lg`（主操作）
- 主操作用`.btn-primary`，取消操作用`.btn-ghost`
- 危险操作（退出、删除）用`.btn-danger`
- 次要CTA（如"邀请好友"）用`.btn-purple`

### 4.2 卡片（Card）

```css
.card {
  background: var(--bg-card);
  border: 1px solid var(--border-subtle);
  border-radius: var(--radius-md);  /* 12px */
  padding: 14px;
  box-shadow: var(--shadow-card);
}
.card-gold   { border-color: var(--border-gold); }
.card-purple { border-color: var(--border-purple); }
```

**使用规则**：
- 默认`.card`用于普通信息容器
- `.card-gold`用于重要/精选内容
- `.card-purple`用于VIP/特殊内容
- 卡片内间距统一14px

### 4.3 头像（Avatar）

```css
.avatar {
  border-radius: 50%;
  background: linear-gradient(135deg, var(--purple), var(--gold));
  display: flex; align-items: center; justify-content: center;
  font-weight: 700; color: #fff; overflow: hidden; flex-shrink: 0;
}
/* 尺寸 */
.avatar-xs  { 24px, 10px字号 }
.avatar-sm  { 32px, 12px字号 }
.avatar-md  { 40px, 14px字号 }
.avatar-lg  { 56px, 18px字号 }
.avatar-xl  { 80px, 28px字号 }
.avatar-2xl { 100px, 32px字号 }

/* 装饰 */
.avatar-ring        { 金色光环 }
.avatar-ring-purple { 紫色光环 }
.avatar-online      { 绿色在线圆点 }
```

**使用规则**：
- 个人主页：`.avatar-2xl`
- 列表项/聊天：`.avatar-md`
- 导航栏/资产栏：`.avatar-sm`
- 背景为紫色到金色的渐变

### 4.4 徽章（Badge）

```css
.badge { min-width:16px; height:16px; padding:0 5px; border-radius:8px; font-size:10px; font-weight:700; color:#fff; bg:red; }
.badge-gold   { bg:gold, color:#000 }
.badge-purple { bg:purple }
.badge-dot    { 8x8, 圆形, 无文字 }
```

### 4.5 标签（Tag）

```css
.tag { font-size:10px; padding:2px 6px; border-radius:4px; font-weight:600; }
.tag-gold   { 金色背景15%+金色边框 }
.tag-purple { 紫色背景15%+紫色边框 }
.tag-green  { 绿色背景15% }
.tag-red    { 红色背景15% }
.tag-orange { 橙色背景15% }
```

### 4.6 输入框（Input）

```css
.input-group { margin-bottom: 14px; }
.input-label { font-size:12px; color:secondary; margin-bottom:6px; font-weight:500; }
.input {
  width:100%; height:44px; bg:dark; border:1px solid border-subtle;
  border-radius:radius-sm; padding:0 14px; color:primary; font-size:14px;
  outline:none; transition:border-color 0.2s;
}
.input:focus { border-color: gold; }
.input::placeholder { color: muted; }

/* 带图标的输入框 */
.input-icon { position:relative; }
.input-icon .input { padding-left: 40px; }
.input-icon .icon-left { position:absolute; left:12px; top:50%; transform:translateY(-50%); color:muted; font-size:16px; }

/* 多行输入 */
textarea.input { height:auto; padding:10px 14px; resize:none; }
```

**使用规则**：
- 高度始终44px
- 聚焦时边框变金色
- placeholder用muted色

### 4.7 进度条（Progress Bar）

```css
.progress-bar { width:100%; height:6px; bg:elevated; border-radius:3px; overflow:hidden; }
.progress-fill { height:100%; bg:linear-gradient(90deg, gold, #ffaa00); border-radius:3px; box-shadow:0 0 6px gold-glow; }
.progress-fill-purple { bg:linear-gradient(90deg, purple, purple-dim); }
```

### 4.8 分段控件（Segmented Control）

```css
.segmented { display:flex; bg:dark; border-radius:radius-sm; padding:3px; gap:2px; }
.seg-item { flex:1; text-align:center; padding:7px 4px; font-size:12px; font-weight:500; color:secondary; border-radius:6px; cursor:pointer; }
.seg-item.active { bg:linear-gradient(135deg, gold, #ffaa00); color:#1a1a00; font-weight:700; }
```

### 4.9 列表项（List Item）

```css
.list-item {
  display:flex; align-items:center; gap:12px;
  padding:12px 14px; cursor:pointer; transition:background 0.2s;
  border-bottom:1px solid border-subtle;
}
.list-item:hover { bg:rgba(255,215,0,0.05); }
.list-item:last-child { border-bottom:none; }
.li-icon { 36x36, flex居中, 20px字号 }
.li-title { 14px, 500 }
.li-sub { 12px, secondary }
.li-arrow { muted, 14px, 右箭头 }
```

**每条列表项必须包含**：左侧图标 + 标题 + 副标题（可选） + 右侧箭头

### 4.10 游戏卡片（Game Tile）

```css
.game-tile {
  bg:card; border:1px solid border-subtle; border-radius:radius-md;
  padding:12px 8px; text-align:center; cursor:pointer;
  transition:all 0.2s; position:relative;
}
.game-tile:hover { border-color:gold; transform:translateY(-2px); box-shadow:shadow-gold; }
.gt-icon { 32px字号, margin-bottom:4px }
.gt-name { 11px, 600 }
.gt-tag { 右上角, 8px字号, 红色背景, 白色文字 }
```

### 4.11 锦标赛卡片（Tournament Card）

```css
.tournament-card {
  bg:linear-gradient(135deg, #1a1a24, #20202c);
  border:1px solid border-gold; border-radius:radius-md;
  padding:12px; cursor:pointer;
}
.tournament-card:hover { box-shadow:shadow-gold; }
```

### 4.12 Banner

```css
.banner {
  margin:12px; border-radius:radius-lg; height:140px;
  bg:linear-gradient(135deg, #1a0a2e, #16213e, #0f3460);
  position:relative; overflow:hidden;
  display:flex; align-items:center; padding:16px;
  border:1px solid border-purple;
}
.banner-gold { bg:linear-gradient(135deg, #2e1a0a, #3e2723, #1a1a00); border-color:border-gold; }
.banner-title { Orbitron, 18px, 900 }
.banner-sub { 12px, secondary }
.banner-dots { 底部居中, dot:6px圆, active:16px宽+金色 }
```

### 4.13 资产胶囊（Asset Pill）

```css
.asset-pill {
  display:flex; align-items:center; gap:4px;
  bg:card; border:1px solid border-subtle; border-radius:12px;
  padding:4px 8px; font-size:11px; font-weight:600;
}
.asset-pill.gold { border-color:border-gold; }
```

### 4.14 弹窗（Modal）

```css
.modal-overlay {
  position:absolute; top:0;left:0;right:0;bottom:0;
  bg:rgba(0,0,0,0.7); display:none; align-items:center; justify-content:center;
  z-index:500; padding:20px;
}
.modal-overlay.show { display:flex; animation:fade-in 0.2s; }
.modal-box {
  bg:card; border:1px solid border-gold; border-radius:radius-lg;
  padding:20px; width:100%; max-width:300px; text-align:center;
  animation:scale-in 0.3s; box-shadow:shadow-gold;
}
.modal-title { Orbitron, 16px, 700 }
.modal-body { 13px, secondary, line-height:1.5 }
.modal-actions { display:flex; gap:10px; }
.modal-actions .btn { flex:1; }
```

### 4.15 Toast

```css
.toast {
  position:absolute; bottom:80px; left:50%; transform:translateX(-50%);
  bg:rgba(26,26,36,0.95); border:1px solid border-gold; border-radius:20px;
  padding:10px 20px; font-size:13px; z-index:999; display:none;
  box-shadow:shadow-gold;
}
.toast.show { display:block; animation:slide-up 0.3s; }
```

### 4.16 空状态（Empty State）

```css
.empty-state {
  display:flex; flex-direction:column; align-items:center; justify-content:center;
  padding:40px 20px; text-align:center;
}
.es-icon { 48px字号, opacity:0.3, margin-bottom:12px }
.es-text { 14px, muted, margin-bottom:14px }
```

### 4.17 分隔线（Divider）

```css
.divider { height:1px; bg:border-subtle; margin:10px 0; }
.divider-label {
  display:flex; align-items:center; gap:10px; margin:14px 0;
}
.divider-label::before, .divider-label::after { content:''; flex:1; height:1px; bg:border-subtle; }
.divider-label span { 11px, muted }
```

### 4.18 加载动画（Spinner）

```css
.spinner {
  width:40px; height:40px; border:3px solid elevated;
  border-top-color:gold; border-radius:50%;
  animation:spin 0.8s linear infinite;
}
```

---

## 五、布局模式

### 5.1 页面容器结构

```
page（100%容器）
├── status-bar（28px，可选）
├── navbar（52px，可选）
│   ├── nav-back（返回按钮，左）
│   ├── nav-title（居中标题，Orbitron）
│   └── nav-right（操作按钮，右）
├── asset-bar（资产栏，可选，游戏相关页面）
├── page-scroll（滚动区域）
│   ├── section（标准模块）
│   │   ├── section-header（标题+更多）
│   │   └── 内容区域
│   └── ...
└── tabbar（62px，仅一级页面）
    └── tab-item × 5
```

### 5.2 标准模块（Section）

```css
.section { padding: 14px; }
.section-header { display:flex; align-items:center; justify-content:space-between; margin-bottom:10px; }
.section-title { Orbitron, 14px, 700, color:gold; }
.section-more { 12px, secondary, cursor:pointer; }
```

### 5.3 网格系统

```css
.grid-2 { display:grid; grid-template-columns: repeat(2, 1fr); gap: 10px; }
.grid-3 { display:grid; grid-template-columns: repeat(3, 1fr); gap: 10px; }
.grid-4 { display:grid; grid-template-columns: repeat(4, 1fr); gap: 8px; }
```

### 5.4 特殊布局

- **引导页**：`onboarding-full`（radial-gradient背景，居中内容，跳过按钮右上角）
- **语聊房**：`voice-stage`（3列网格，圆形mic-slot）
- **签到日历**：`signin-cal`（7列网格，方形签到格）
- **通行证**：`bp-track`（横向滚动，flex+overflow-x:auto）
- **Ludo棋盘**：15×15网格，280×280px
- **转盘**：260×260px圆形，border+shadow+pointer+center

### 5.5 聊天布局

```css
.chat-bubble { max-width:75%; padding:10px 14px; border-radius:14px; font-size:13px; }
.chat-bubble.self { bg:purple渐变; color:#fff; align-self:flex-end; border-bottom-right-radius:4px; }
.chat-bubble.other { bg:card; color:primary; align-self:flex-start; border-bottom-left-radius:4px; }
.chat-time { 10px, muted }
```

---

## 六、导航架构

### 6.1 底部Tab导航

| 序号 | Tab | 页面ID | 图标 | 说明 |
|------|-----|--------|------|------|
| 1 | 游戏 | `game-home` | 🎮 | 首页/游戏大厅 |
| 2 | 观战 | `spectate-home` | 👁 | 观战入口 |
| 3 | 社群 | `community-home` | 👥 | 好友/战队/语聊 |
| 4 | 活动 | `events-home` | 🎁 | 活动中心 |
| 5 | 更多 | `more-home` | ☰ | 个人/设置/商城 |

**显示规则**：
- 仅5个Tab页面显示TabBar
- 二级/三级页面自动隐藏TabBar
- 选中态：金色文字+金色图标+顶部发光指示条

### 6.2 页面层级

```
Level 0: 引导页 → 注册/登录 → 设置资料
Level 1: 游戏首页 / 观战 / 社群 / 活动 / 更多（TabBar）
Level 2: 快速匹配 / 创建房间 / 房间大厅 / 人机对战 / 观战详情
         群组信息 / 语聊房 / 战队管理 / 每日杯赛 / 幸运转盘
         个人主页 / 好友 / 消息 / 商城 / 段位排行 / 设置
Level 3: 游戏棋盘 / 比赛结果 / 编辑资料 / 聊天 / 商品详情
         充值 / VIP / 游戏记录 / 装饰商店 / 礼物
```

### 6.3 页面目录（Page Index）

- 触发：`togglePageIndex()`
- 位置：固定右上角，从右侧滑出面板
- 内容：全部35个页面列表，中文名称
- 尺寸：200px宽，最大70vh高，可滚动

---

## 七、交互模式

### 7.1 页面切换

```javascript
function showPage(pageId) {
  // 1. 隐藏所有页面
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  // 2. 显示目标页面（ID: page-{pageId}）
  const page = document.getElementById('page-' + pageId);
  if (page) { page.classList.add('active'); page.querySelector('.page-scroll')?.scrollTo(0, 0); }
  // 3. 同步TabBar状态
  const tabPages = ['game-home','spectate-home','community-home','events-home','more-home'];
  // 在Tab页面显示TabBar并高亮对应Tab，否则隐藏TabBar
}
```

### 7.2 Toast反馈

```javascript
function toast(msg) {
  // 在当前激活页面内显示Toast，2秒后自动消失
  // 位置：底部居中，距底部80px
}
```

### 7.3 页面目录切换

```javascript
function togglePageIndex() {
  // 显示/隐藏页面目录面板
}
```

### 7.4 语言切换

```javascript
function switchLanguage(lang) {
  // 1. 检查是否已经是目标语言
  // 2. 使用TreeWalker遍历所有文本节点
  // 3. 按长度降序匹配翻译映射表
  // 4. 同步更新placeholder属性
  // 5. 更新页面标题和语言标识
}
```

切换入口：`设置 > 通用 > 语言设置`（设置页内），不设外部浮动按钮

### 7.5 交互反馈规则

| 操作 | 反馈 |
|------|------|
| 按钮点击 | 0.2s transition，hover时上移1px+发光增强 |
| 页面跳转 | 瞬间切换（无过渡动画） |
| 操作成功 | Toast提示 |
| 操作失败 | Toast提示错误信息 |
| 加载中 | Spinner旋转动画 |
| 空数据 | Empty State组件 |
| 危险操作 | Modal二次确认 |
| 游戏卡片Hover | 边框变金+上移2px+金色发光 |

---

## 八、动画系统

### 8.1 关键帧定义

```css
@keyframes pulse-ring  { 0%{scale(0.8);opacity:0.8} 100%{scale(2.2);opacity:0} }
@keyframes pulse-glow  { 0%,100%{box-shadow:0 0 10px gold-glow} 50%{box-shadow:0 0 25px gold-glow,0 0 50px gold-glow} }
@keyframes spin        { to{rotate(360deg)} }
@keyframes float       { 0%,100%{translateY(0)} 50%{translateY(-6px)} }
@keyframes shine       { 0%{bg-position:-200% center} 100%{bg-position:200% center} }
@keyframes glow-text   { 0%,100%{text-shadow:0 0 10px gold-glow} 50%{text-shadow:0 0 20px gold-glow,0 0 30px gold-glow} }
@keyframes slide-up    { from{translateY(100%);opacity:0} to{translateY(0);opacity:1} }
@keyframes fade-in     { from{opacity:0} to{opacity:1} }
@keyframes scale-in    { from{scale(0.8);opacity:0} to{scale(1);opacity:1} }
```

### 8.2 动画使用场景

| 动画类 | 效果 | 使用场景 |
|--------|------|----------|
| `.anim-pulse-glow` | 脉冲发光 | VIP卡片、限定活动入口 |
| `.anim-float` | 上下浮动 | 引导页插图、奖励图标 |
| `.anim-glow-text` | 文字发光 | 特殊标题、稀有奖励文字 |
| `.anim-spin` | 旋转 | 加载Spinner、转盘 |
| `.anim-slide-up` | 从底部滑入 | Toast |
| `.anim-fade-in` | 淡入 | 弹窗遮罩 |
| `.anim-scale-in` | 缩放进入 | 弹窗内容 |

### 8.3 过渡动画

| 元素 | 时长 | 缓动 | 效果 |
|------|------|------|------|
| 按钮hover | 0.2s | ease | 上移1px+发光增强 |
| 输入框聚焦 | 0.2s | - | 边框变金色 |
| 游戏卡片hover | 0.2s | - | 上移2px+边框金色+发光 |
| 列表项hover | 0.2s | - | 背景金色5% |
| 转盘旋转 | 4s | cubic-bezier(0.17,0.67,0.12,0.99) | 减速停止 |

---

## 九、图标体系

### 9.1 当前图标方案

原型阶段使用Emoji作为功能图标，降低对设计资源的依赖。正式开发时替换为专用图标库。

### 9.2 Emoji映射表

| 功能 | Emoji | 使用位置 |
|------|-------|----------|
| 游戏 | 🎮 | 游戏首页Tab、游戏类入口 |
| 观战 | 👁 | 观战Tab |
| 社群 | 👥 | 社群Tab |
| 活动 | 🎁 | 活动Tab |
| 更多 | ☰ | 更多Tab |
| 锦标赛 | 🏆 | 赛事相关 |
| 金币 | 🪙 | 货币显示 |
| 钻石 | 💎 | 高级货币 |
| 闪电 | ⚡ | 快速匹配 |
| 火 | 🔥 | 热门/趋势 |
| 皇冠 | 👑 | VIP/王者 |
| 星星 | ⭐ | 评分/收藏 |
| 盾牌 | 🛡 | 防御/战队 |
| 消息 | 💬 | 聊天 |
| 设置 | ⚙ | 设置 |
| 搜索 | 🔍 | 搜索 |
| 通知 | 🔔 | 通知 |
| 朋友 | 👫 | 好友 |
| 商店 | 🛒 | 商城 |
| 排名 | 📊 | 排行 |
| 礼物 | 🎁 | 礼物 |
| 转盘 | 🎡 | 幸运转盘 |
| 日历 | 📅 | 签到 |
| 墨镜 | 😎 | VIP特权 |
| 返回 | ◀ | 返回按钮 |

### 9.3 正式图标规范（待开发）

- 风格：线性图标（非选中）+ 面性图标（选中）
- 底部Tab图标：24×24px
- 列表图标：20×20px
- 金刚区图标：40-48px
- 描边：1.5px，圆角端点

---

## 十、页面清单与状态矩阵

### 10.1 完整页面清单（35页）

| 序号 | 页面ID | 中文名称 | 层级 | TabBar | 特殊状态 |
|------|--------|----------|------|--------|----------|
| 01 | onboarding | 引导页 | 0 | 无 | 3页滑动 |
| 02 | register | 注册 | 0 | 无 | 验证码倒计时 |
| 03 | login | 登录 | 0 | 无 | 忘记密码 |
| 04 | profile-setup | 设置资料 | 0 | 无 | 头像选择 |
| 05 | game-home | 游戏首页 | 1 | 游戏 | 资产栏 |
| 06 | matchmaking | 快速匹配 | 2 | 无 | 匹配动画 |
| 07 | create-room | 创建房间 | 2 | 无 | 表单 |
| 08 | room-lobby | 房间大厅 | 2 | 无 | 等待玩家 |
| 09 | vs-ai | 人机对战 | 2 | 无 | AI难度选择 |
| 10 | spectate-home | 观战 | 1 | 观战 | 次数限制 |
| 11 | spectate-detail | 观战详情 | 2 | 无 | 实时对局 |
| 12 | community-home | 社群 | 1 | 社群 | 好友/群组/战队 |
| 13 | group-info | 群组信息 | 2 | 无 | 成员列表 |
| 14 | voice-room | 语聊房 | 2 | 无 | 麦克风状态 |
| 15 | crew-manage | 战队管理 | 2 | 无 | 权限层级 |
| 16 | events-home | 活动中心 | 1 | 活动 | 活动列表 |
| 17 | daily-cup | 每日杯赛 | 2 | 无 | 倒计时 |
| 18 | lucky-wheel | 幸运转盘 | 2 | 无 | 转盘动画 |
| 19 | game-board | 游戏棋盘 | 3 | 无 | Ludo棋盘 |
| 20 | result | 比赛结果 | 3 | 无 | 结算动画 |
| 21 | more-home | 更多 | 1 | 更多 | 功能入口 |
| 22 | profile | 个人主页 | 2 | 无 | 数据展示 |
| 23 | edit-profile | 编辑资料 | 3 | 无 | 表单 |
| 24 | friends | 好友 | 2 | 无 | 在线状态 |
| 25 | messages | 消息 | 2 | 无 | 未读角标 |
| 26 | chat | 聊天 | 3 | 无 | 气泡+输入 |
| 27 | shop | 商城 | 2 | 无 | 商品列表 |
| 28 | product-detail | 商品详情 | 3 | 无 | 购买按钮 |
| 29 | recharge | 充值 | 3 | 无 | 档位选择 |
| 30 | vip | VIP | 3 | 无 | 权益对比 |
| 31 | rank | 段位排行 | 2 | 无 | 排行榜 |
| 32 | game-history | 游戏记录 | 3 | 无 | 战绩列表 |
| 33 | settings | 设置 | 2 | 无 | 设置列表 |
| 34 | cosmetics | 装饰商店 | 3 | 无 | 皮肤/头像框 |
| 35 | gifts | 礼物 | 3 | 无 | 赠送流程 |

### 10.2 状态覆盖矩阵

重新生成原型时，以下页面必须覆盖的状态：

| 页面 | 常规 | 空状态 | 加载中 | 错误 | 成功 | 权限 |
|------|------|--------|--------|------|------|------|
| 引导页 | ✓ | - | - | - | - | - |
| 注册/登录 | ✓ | - | ✓ | ✓ | ✓ | - |
| 游戏首页 | ✓ | ✓ | ✓ | ✓ | - | - |
| 快速匹配 | - | - | ✓ | ✓ | ✓ | - |
| 创建房间 | ✓ | - | - | ✓ | ✓ | - |
| 观战 | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| 社群 | ✓ | ✓ | ✓ | ✓ | - | - |
| 活动中心 | ✓ | ✓ | ✓ | ✓ | - | - |
| 更多 | ✓ | - | - | - | - | - |
| 个人主页 | ✓ | ✓ | ✓ | ✓ | - | - |
| 好友 | ✓ | ✓ | ✓ | ✓ | - | - |
| 消息 | ✓ | ✓ | ✓ | ✓ | - | - |
| 聊天 | ✓ | ✓ | - | ✓ | - | ✓ |
| 商城 | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| 设置 | ✓ | - | - | - | ✓ | - |

---

## 十一、平铺版与手机版差异

### 11.1 CSS差异

| 属性 | 手机版 | 平铺版 |
|------|--------|--------|
| `.page` display | `none`（默认）/ `flex`（active） | `flex !important`（全部显示） |
| `.page` position | `fixed` | `relative` |
| `.page` width/height | `100%` / `100%` | `375px` / `812px`（固定） |
| `.page` margin | 0 | `20px`（间距） |
| `.page` border-radius | 0 | `20px`（模拟手机圆角） |
| `.page` box-shadow | 无 | `0 8px 32px rgba(0,0,0,0.3)` |
| 页面容器 | `phone-frame`（居中单个） | `#app`（flex-wrap多列） |
| 页面标识 | 无 | 页面序号+名称标签 |
| 页面跳转 | `showPage()`切换 | `scrollToPage()`滚动到 |
| 语言切换 | 支持 | 不支持 |

### 11.2 脚本差异

| 函数 | 手机版 | 平铺版 |
|------|--------|--------|
| `showPage()` | 隐藏所有+显示目标 | 滚动到目标位置 |
| `toast()` | 在当前页面显示 | 不显示或页面内显示 |
| `switchLanguage()` | 支持 | 不支持 |
| `togglePageIndex()` | 显示/隐藏面板 | 显示/隐藏面板 |

### 11.3 生成时注意事项

- 平铺版必须覆盖`.page`的`display:none`为`display:flex !important`
- 平铺版不需要`phone-frame`容器
- 平铺版的页面目录点击后是`scrollToPage()`而非`showPage()`
- 手机版的不活跃页面必须完全隐藏（不占空间）
- 两种版本共享同一套CSS变量和组件样式

---

## 十二、重构检查清单

重构原型时，按以下顺序逐项验证：

### 12.1 基础环境
- [ ] CSS变量完整引用（`:root`中16个变量）
- [ ] Google Fonts正确加载（Orbitron + Inter + Noto Sans SC）
- [ ] 手机框架375×812px，圆角44px，刘海屏模拟
- [ ] 页面基础结构：`.page` 容器 + `.page-scroll` 滚动区

### 12.2 组件一致性
- [ ] 按钮：5种变体（primary/purple/secondary/ghost/danger）+ 3种尺寸
- [ ] 卡片：默认/金色边框/紫色边框
- [ ] 头像：6种尺寸 + 光环 + 在线状态
- [ ] 输入框：44px高度 + 聚焦金色边框
- [ ] 列表项：图标+标题+副标题+箭头
- [ ] Toast：底部居中，2秒消失
- [ ] 弹窗：300px宽 + 金色边框 + 缩放动画
- [ ] 空状态：48px图标 + 14px文字 + 按钮

### 12.3 导航一致性
- [ ] 5个Tab：游戏/观战/社群/活动/更多
- [ ] TabBar高度62px，金色上边框
- [ ] 选中态：金色文字+图标+顶部发光条
- [ ] 二级页面自动隐藏TabBar
- [ ] 页面目录面板：200px宽，中文名称

### 12.4 交互一致性
- [ ] `showPage()` 函数：隐藏所有→显示目标→复位滚动→同步TabBar
- [ ] `toast()` 函数：当前页面内显示→2秒消失
- [ ] `togglePageIndex()` 函数：面板显隐切换
- [ ] `switchLanguage()` 函数：TreeWalker遍历→映射表替换→placeholder同步

### 12.5 视觉一致性
- [ ] 背景统一：`--bg-black`（#0a0a0f）
- [ ] 模块标题：Orbitron + 14px + 金色
- [ ] 页面内边距：14px
- [ ] 卡片内边距：14px
- [ ] 卡片圆角：12px
- [ ] 分隔线：`--border-subtle`（8%白色）
- [ ] 发光效果：仅用于选中态和CTA，不滥用

### 12.6 页面完整性
- [ ] 35个页面全部存在
- [ ] 页面ID格式：`page-{pageId}`
- [ ] 每个页面含`.page-scroll` 滚动区
- [ ] 导航栏、状态栏按需显示
- [ ] 核心页面的状态覆盖（常规/空/加载/错误）

---

**适用项目**：P008-Jam3a-2607
**基准版本**：V3.2（手机版）
**更新日期**：2026-07-29
**下次评审**：原型重构时对照更新