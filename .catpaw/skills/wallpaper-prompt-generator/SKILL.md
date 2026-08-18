---
name: wallpaper-prompt-generator
description: 米哈游游戏角色壁纸 AI 生图 prompts 每日生成工具。根据游戏热点（原神/绝区零/崩铁版本更新、前瞻直播、新角色上线）、社区热度（B站/小红书/米游社）、时事节日、角色人气，自动决策当天要制作哪个角色的壁纸，并生成 10 条左右高质量 prompts（含 positive/negative prompt、背景场景、人物动作描述）。触发词：生成壁纸prompts、今日壁纸、每日壁纸、wallpaper prompts、角色壁纸、游戏壁纸、原神壁纸、绝区零壁纸、崩铁壁纸、米哈游壁纸。
---

# 米哈游游戏角色壁纸 Prompts 每日生成

## 工作流概览

三阶段流水线：**热点搜索 → 类型与角色决策 → Prompts 生成**

每天的产出对应一条**视频**的素材合集。视频有四种类型，每种类型的 prompts 结构和数量不同。

---

## Phase 1: 热点搜索

从以下信息源收集当日热点，**按优先级排序**：

### 1. 米哈游官方（最高优先级）

| 信息源 | URL | 用途 |
|--------|-----|------|
| 原神官网 | https://ys.mihoyo.com/ | 版本公告、角色展示 |
| 崩铁官网 | https://sr.mihoyo.com/ | 版本公告、角色展示 |
| 绝区零官网 | https://zzz.mihoyo.com/ | 版本公告、角色展示 |
| 米游社（原神） | https://www.miyoushe.com/ys/ | 官方公告、前瞻直播、角色资讯 |
| 米游社（崩铁） | https://www.miyoushe.com/sr/ | 官方公告、前瞻直播 |
| 米游社（绝区零） | https://www.miyoushe.com/zzz/ | 官方公告、前瞻直播 |
| HoYoLab | https://www.hoyolab.com/ | 国际版官方社区 |

### 2. 社区热度

| 信息源 | URL | 用途 |
|--------|-----|------|
| B站搜索 | https://search.bilibili.com/ | 视频热度、二创趋势、角色讨论 |
| 小红书搜索 | https://www.xiaohongshu.com/ | 同人图、角色热度、cosplay |
| B站WIKI（原神） | https://wiki.biligame.com/ys/ | 角色资料、立绘下载 |
| B站WIKI（崩铁） | https://wiki.biligame.com/sr/ | 角色资料、立绘下载 |
| B站WIKI（绝区零） | https://wiki.biligame.com/zzz/ | 角色资料、立绘下载 |

### 3. 角色人气榜

通过 web_search 搜索：`原神 角色人气榜`、`绝区零 角色人气投票`、`崩坏星穹铁道 角色人气`、社区抽卡意愿调查等。

### 4. 时事热点

通过 web_search 搜索当天节日、赛事、文化事件。常见结合方向：春节/中秋/七夕、世界杯/ChinaJoy、季节变化（夏日/秋冬）、开学季等。

### 5. 梗图热源（类型 E 专用）

搜索当天各平台的米哈游游戏热梗，判断哪些角色有正在传播的梗形象：

| 平台 | URL | 梗形态 | 特点 |
|------|-----|--------|------|
| B站搜索 | https://search.bilibili.com/ | OPUS图文合集、梗百科视频、二创整活 | 梗的起源地和系统化整理，适合发现新梗 |
| 抖音搜索 | https://search.douyin.com/ | 梗形象二创视频 | 传播最快、播放量最大，适合判断热度 |
| 小红书 | https://www.xiaohongshu.com/ | 梗形象图文、整活合集 | 偏视觉呈现，适合看梗形象的视觉效果 |
| 米游社 | https://www.miyoushe.com/ | 梗图收集合集帖 | 官方社区，玩家原创梗集中地 |
| 百度贴吧 | https://tieba.baidu.com/ | 原神梗吧、星穹铁道吧 | 长期讨论沉淀，适合挖掘老梗 |
| NGA | https://ngabbs.com/ | 梗图楼、讨论帖 | 硬核玩家社区，梗的质量较高 |
| 微博 | https://weibo.com/ | 梗图大赏账号 | 实时传播，适合追踪最新梗 |
| TapTap | https://www.taptap.cn/ | #原神梗图 等话题 | 玩家社区讨论 |

### 搜索关键词参考

`原神 最新版本 新角色`、`绝区零 版本更新`、`崩坏星穹铁道 新角色`、`Genshin Impact update`、`Zenless Zone Zero new character`、`Honkai Star Rail new character`

**梗图搜索关键词**（类型 E 时使用）：`原神 梗 最新`、`绝区零 整活 热门`、`崩铁 梗图 今天`、`米哈游 角色 梗形象`、`原神 二创 整活 热门`

### 6. 角色社区梗与爱称（Phase 2 选定角色后执行）

在 Phase 2 确定角色之后、Phase 4 生成标题之前，**必须**针对选定角色执行社区梗搜索。搜集到的信息将直接用于 Phase 4 标题创作，是趣味性标题的核心素材来源。

**搜索内容**：

| 搜索维度 | 说明 | 搜索关键词模板 |
|----------|------|---------------|
| 爱称/昵称/外号 | 玩家对角色的非正式称呼 | `{角色名} 爱称 昵称 外号 玩家社区 梗` |
| 弹幕/评论热词 | B站PV弹幕、米游社评论中的高频词 | `{角色名} B站 弹幕 评论 热梗` |
| 强度定位标签 | 攻略区对角色的定位标签 | `{角色名} "神子下位" OR "替代" OR "最强" 攻略` |
| 玩家情绪热词 | 围绕角色的社区情绪关键词 | `{角色名} "白嫖" OR "免费" OR "必抽" 评论 玩家讨论` |
| 角色梗/趣味细节 | 官方装扮描述、角色故事中的趣味点 | `{角色名} 萌娘百科 角色梗 外号 百度贴吧 NGA` |
| 配队/体系讨论 | 角色在配队讨论中的热门搭配 | `{角色名} 配队 "最强队友" OR "最佳搭档"` |
| PV金句/标志性台词 | 角色PV或角色语音中被广泛传播的台词 | `{角色名} PV 台词 金句 弹幕` |

**搜索平台**：

| 平台 | 用途 | 适合挖掘的内容 |
|------|------|---------------|
| B站（视频+弹幕） | 高播放量攻略/PV的标题用语、弹幕高频词 | 强度标签（如"4星雷奶"）、爱称、PV金句传播 |
| 米游社 | 官方角色介绍帖、玩家讨论帖 | 角色免费获取方式、官方定位描述 |
| 百度百科/萌娘百科 | 角色设定汇总、同伴/宠物名字等细节 | 角色技能名、同伴名（如"图加林"）、装扮描述趣味点 |
| 抖音 | PV播放量、金句传播量 | 传播最广的角色标语（如"似隼疾掠，弋猎于冬"） |
| NGA/百度贴吧 | 深度讨论、强度争议、配队理论 | 强度对比标签（如"叫板八重神子"）、配队梗（如"木偶最强队友"） |
| TapTap | 版本前瞻讨论、玩家第一反应 | "免费四星""白嫖战神"等情绪热词 |
| Gachabase等数据站 | 角色装扮描述、设定文本原文 | 官方趣味描述（如"帽子是狗头因为很可爱"） |

**输出要求**：

搜索结果需记录在 `titles.md` 文件头部，格式为带URL的有序列表，按参考权重排序。示例：

```markdown
> 社区梗/爱称数据来源（按参考权重排序）：
> 1. [B站攻略视频「XX前瞻攻略！」· 播放6.6万](https://...) — "4星雷奶"标签来源
> 2. [米游社官方角色介绍](https://...) — "免费获取"设定
> 3. [抖音官方PV · 3.3亿喜欢](https://...) — 金句传播源
```

---

## Phase 2: 类型与角色决策

### 第一步：选定视频类型

五种视频类型：

| 类型 | 说明 | 角色数量 | 每角色 prompts | 总 prompts |
|------|------|----------|---------------|-----------|
| A. 角色单人壁纸合集 | 围绕一个角色，多场景多风格 | 1 个 | 10 条左右 | ~10 |
| B. 主题类型合集 | 同一主题，横跨多个不同角色 | 4~6 个 | 每个 1~2 条 | ~10 |
| C. 可爱动物萌化形象合集 | 不同角色的动物拟化壁纸 | 5~8 个 | 每个 1 条 | ~8 |
| D. 表情包合集 | 同一角色的玩梗表情包 | 1 个 | 8~12 条 | ~10 |
| E. 梗图合集 | 不同角色各自的梗形象图 | 3~5 个 | 每个 1~2 条 | ~8 |

**类型选择依据**：

- 有重大热点（新角色上线/前瞻直播）→ 优先 **A**（聚焦该角色深度呈现）
- 有时事主题（节日/赛事）适合多角色横向展示 → 优先 **B**（如世界杯足球宝贝）
- 近期没做过萌化/表情包，需要调节节奏 → 选 **C** 或 **D**
- 社区有某角色的梗/二创爆火 → 选 **D**（围绕该角色做表情包）或 **E**（多角色梗形象合集）
- 社区有多个角色的梗同时流行 → 优先 **E**（如冰女皇蜜雪雪王、艾莲笨蛋鲨鲨同时流行）
- 日常无特殊热点 → 在 A/C 中选人气角色

### 第二步：选定角色

综合以下维度评分：

| 维度 | 权重 | 说明 |
|------|------|------|
| 游戏官方热点 | 40% | 新角色上线、前瞻直播、版本更新当天权重最高 |
| 社区讨论热度 | 25% | B站/小红书/米游社的近期讨论量和趋势 |
| 时事/节日契合 | 20% | 角色气质与当天节日/赛事/季节的匹配度 |
| 已有素材覆盖 | 15% | 优先选未做过的角色，查看工作区已有目录避免重复 |

**决策输出**：在 prompts.md 头部注释中明确写出：选定类型、选定角色、各维度考量理由。

---

## Phase 3: Prompts 生成

### 通用规范（适用所有类型）

**Positive Prompt 必含项**：
- 画面比例与用途（如 `16:9 2K wallpaper`、`9:16 mobile wallpaper`、`1:1 表情包`）
- 角色全名与出处（如 `Odette from Genshin Impact`）
- 画风描述（`highly detailed anime-style illustration` / `3D cel-shaded` / `cute chibi` 等）
- 人物外貌特征（发色发型、瞳色、标志性配饰，必须准确）
- 服装描述（具体到款式、颜色、材质）
- 人物动作与表情（具体的肢体姿势、面部表情、眼神方向）
- 场景/背景描述（地点、环境氛围、天气、时间）
- 光影与色调（光源方向、色温、整体色彩方案）

**Negative Prompt 必含项**：
- 画质排除：`low quality, worst quality, blurry, pixelated`
- 人体结构：`bad anatomy, extra limbs`
- 风格排除：根据目标风格排除不符的（如 `chibi, photorealistic`）
- 角色准确性：`wrong hair color, wrong eye color, incorrect character`
- 通用排除：`text, watermark, logo, signature`

**手部质量优化（三条策略，必须执行）**：

AI 生图最常见的问题就是手部画错（多指、少指、融合指、模糊指）。以下三条策略必须组合使用：

1. **Negative Prompt 手部穷举**（每条 prompt 必含以下全部词条，直接粘贴到 negative prompt 中）：
   `bad hands, extra fingers, fewer fingers, missing fingers, fused fingers, webbed fingers, merged fingers, overlapping fingers, deformed fingers, mutated fingers, six fingers, four fingers, three fingers, more than five fingers, less than five fingers, disfigured hands, poorly drawn hands, bad hand anatomy, asymmetrical hands, broken fingers, claw hands, blurry hands, indistinct fingers, smeared hands`

2. **Positive Prompt 正面引导**（当画面中手部可见时必含）：
   `perfect hands, five fingers on each hand, anatomically correct hands, well-defined fingers, natural hand pose, detailed hands, clean finger separation`
   在人物动作描述中必须明确手部姿态（如 `hands relaxed at sides`、`arms crossed, hands tucked`），避免让 AI 自由发挥导致画崩。

3. **构图规避策略**（从源头降低风险）：
   - 优先选择手部简单或被遮挡的姿态：`hands in pockets`、`arms crossed`、`hands behind back`、`holding a large object that covers hands`
   - 避免高风险构图：手指交互复杂物体（手指夹持小卡片、手指按乐器琴弦）、手指伸展且为画面焦点
   - 如必须使用高风险手势（如"伸出手邀舞"），需在 positive prompt 中额外强调 `fingers elegantly relaxed, natural hand pose`

---

### 类型 A：角色单人壁纸合集

围绕一个角色，多场景多风格，约 10 条 prompts。

**结构**：

| 段落 | 数量 | 说明 |
|------|------|------|
| 必需·涂鸦墙街头风 | 1 | 引用 `../../needful.png`，现代街头服饰 + 涂鸦墙，冷漠/不屑表情 |
| 必需·特写肖像 | 1 | 引用 `../../needful2.png`，道具半遮面 + 矛盾表情 + 单光源暗背景，见下方「必需2 — 角色特写肖像」公式 |
| 角色设定场景 | 3~4 | 忠于游戏世界观的经典场景（剧情、战斗、标志性地点） |
| 现代风改造 | 1~2 | 御姐/可爱/赛博朋克/学院风等现代服饰改造 |
| 动态/战斗场景 | 1~2 | 元素技能释放、战斗动作、动态构图 |
| 情感/日常/反差 | 1 | 温馨日常、反差萌、私人时刻 |
| 热点主题特别版 | 0~1 | 结合当天时事（节日/赛事/纪念日），如无则省略 |
| 参考图变体 | 1~2 | 基于下载的立绘/参考图生成，含竖屏手机壁纸 |
| 跨领域参考图 | 1~2 | 基于角色职业对应的真实世界素材（照片/名画/海报） |

**参考图下载（必须在写 prompts 之前完成）**：

开始写 prompts 前，**必须先执行**以下流程下载官方立绘。下载的参考图用于校对角色外观描述（发色、服装、配饰等），确保 prompts 与官方设定一致。

按以下优先级依次尝试，某一级成功即停止：

**第 1 级：B站WIKI MediaWiki API（首选，成功率最高）**

```bash
# 1. 查询角色立绘文件的直链（替换 {game} 和 {角色名}）
# game: ys=原神, sr=崩铁, zzz=绝区零
curl -s "https://wiki.biligame.com/{game}/api.php?action=query&titles=File:{角色名}立绘.png&prop=imageinfo&iiprop=url&format=json"

# 2. 从返回 JSON 的 imageinfo.url 字段获取直链，直接下载
curl -sL -o "{角色目录}/splash-art.png" "{上一步获取的url}"

# 3. 同理下载抽卡立绘（文件名可能是 {角色名}抽卡立绘.png）
curl -s "https://wiki.biligame.com/{game}/api.php?action=query&titles=File:{角色名}抽卡立绘.png&prop=imageinfo&iiprop=url&format=json"
```

如果不确定文件名，用 `allimages` API 批量搜索：
```bash
curl -s "https://wiki.biligame.com/{game}/api.php?action=query&list=allimages&aifrom={角色名}&ailimit=50&format=json"
```

**第 2 级：B站WIKI 页面解析（API 无结果时）**

用 web_fetch 访问 `https://wiki.biligame.com/{game}/{角色名}`，从 HTML 中查找 `patchwiki.biligame.com/images/` 开头的图片 URL，提取后用 curl 下载。

**第 3 级：萌娘百科（B站WIKI 完全不可用时）**

用 web_fetch 访问 `https://zh.moegirl.org.cn/{角色名}`，提取 `storage.moegirl.org.cn` 开头的图片 URL。注意去掉 URL 中 `!/fw/` 及之后的缩放参数以获取原图。

**第 4 级：纯文本兜底（所有图片来源均失败时）**

通过 web_search 搜索角色外观描述信息（发色、瞳色、服装细节），在 prompts.md 头部注释中标注「未获取参考图，外观描述基于搜索资料」。prompts 照常生成，但需在 memory.md 中记录失败原因，便于排查。

> 完整来源文档见 [image-sources.md](image-sources.md)，包含更多来源和浏览器渲染方式。

下载成功后在 prompts.md 中用 `![alt text](filename.png)` 引用，并**对照参考图校对** prompts 中的角色外观描述。

**⚠️ 校对必须用视觉工具实际看图**：下载完成后，必须用 `mcp_tool_user-image-reader_image_read` 逐张打开参考图，肉眼确认发色、瞳色、发型、服饰、配饰等细节，再动笔写 prompts。**严禁只凭文件下载成功就认为校对完成**，也严禁仅凭 web_search 的文字描述推断外观。

#### 伴生元素必须单独找参考图（易漏项）

角色的**伴生元素**是独立于角色本体的设计对象，官方立绘常常拍不清楚或根本没入镜，**必须单独搜图确认，严禁凭名称、称呼或功能描述推断外观**。

需要单独确认的伴生元素包括：

| 类型 | 示例 |
|------|------|
| 伴生生物/宠物/机器人 | 伊涅芙的薇尔琪塔、派蒙、帕姆、邦布 |
| 标志性武器/法器 | 专武、元素爆发时召唤的巨型器物 |
| 元素显化物/召唤物 | 召唤兽、傀儡、无人机、灵体 |
| 坐骑/载具 | 飞行器、机车、兽类坐骑 |

**执行要求**：

1. 写 prompts 前，先列出该角色涉及的全部伴生元素清单
2. 每个元素单独搜图（B站WIKI 角色页、萌娘百科、官方宣传图、`web_search` 找官方设定图），下载为 `ref-{元素名}-official.png`
3. 用视觉工具打开逐项确认：**外形（方/圆/人形/兽形）、面部或显示方式、配色、体积比例、移动方式（悬浮/行走/飞行）**
4. 实在找不到图时，在 prompts 中**弱化处理**（只提名称与大致位置，不写具体外观细节），并在 prompts.md 注释与 memory.md 中标注「未获取到参考图，外观描述已弱化」——**宁可少写，也不要编造**

**反面案例（2026.08.11 伊涅芙）**：仅凭「多用途智能辅助单元」这一称呼，将薇尔琪塔推断为「圆形悬浮无人机 + 单个红橙色镜头眼」，实际官方设定是「方盒形 CRT 电视机头小机器人，屏幕以像素点阵显示表情，双腿站立行走」——外形、面部、移动方式全错，导致 10 处描述需要返工。**教训：伴生元素的名称几乎不携带外观信息，必须看图。**

伴生元素外观确认后，应主动挖掘其**表现力优势**并写进每个场景。如薇尔琪塔的像素屏幕可显示丰富表情，就为每个场景指定对应表情（开心弯眼/惊慌雪花屏/困困横线眼），使其从背景道具升级为有情绪反应的第二主角。

#### 必需1 — 涂鸦墙街头风 (Graffiti Wall Street Style)

每个类型 A 角色单人壁纸合集**必须包含且仅包含一条**涂鸦墙街头风 prompt。这是视频系列视觉辨识度最高的封面级 prompt，核心锚点是：**角色必须坐在涂鸦墙前、穿现代街头风服装、表情冷漠不屑**。

**参考图**：`![alt text](../../needful.png)`（刻晴坐于涂鸦墙前的街头风壁纸，全局共享，位于工作区根目录）

**核心四约束（不可偏离，按优先级排序）**：

| 优先级 | 约束项 | 硬性要求 |
|--------|--------|----------|
| 1 | 角色姿态 | **必须坐着**，如坐于矮墙/木箱/折叠椅/摩托车座/地面等，严禁站立 |
| 2 | 背景 | **必须是涂鸦墙**，色彩与角色主题色匹配，含角色名/元素符号/主题涂鸦元素 |
| 3 | 表情与眼神 | **必须冷漠、不屑、居高临下**，silently judging the viewer，严禁温暖/甜美/可爱/唱歌等表情 |
| 4 | 服装风格 | **必须是现代街头风**，严禁使用游戏原设定服装（除非原设定本身就是街头风） |

**服装公式**：

上身和下身必须同时满足以下规范，且需**突破原游戏设定**进行现代潮流改造：

- **上身**：无袖露脐短款上衣（crop top / tube top / 紧身短款背心） + 敞开的短夹克（cropped jacket / 短款机车夹克 / 短款运动外套），夹克可半脱式搭在肩上
- **下身**：短裙（skater skirt / pleated mini skirt）或短牛仔裤（denim shorts / 破洞短裤），必须露出大部分腿部线条
- **腿部**：光腿或搭配丝袜/过膝袜（根据角色气质选择，颜色需与角色主题色呼应）
- **鞋履**：运动鞋 / 马丁靴 / 厚底鞋，避免正式皮鞋或原设高跟鞋
- **配饰**：链条项链 / 耳钉 / 手环 / 腰带等潮流饰品，可加入角色标志性元素（如角色专属符号、元素主题配饰）
- **改造原则**：保留角色标志性发型、发色、瞳色、发饰，其余服装全部替换为街头潮流单品。如角色有标志性外套/披风，可将其转化为街头夹克风格

**涂鸦墙公式**：

- **色彩方案**：涂鸦墙的主色调必须与角色的主题色/元素色/阵营色**高度匹配**（如火角色→红橙暖色调涂鸦、冰角色→蓝紫冷色调涂鸦、草角色→绿黄自然色调涂鸦）
- **内容元素**：墙上必须包含以下至少两类涂鸦元素：
  - 角色名或角色外号的艺术字体涂鸦
  - 角色元素符号（如火焰/水滴/闪电/风旋等）
  - 角色主题相关图案（如角色武器剪影、标志性物品、阵营徽章）
  - 街头风格的抽象几何图形、喷漆滴落效果、涂鸦签名
- **质感要求**：多层喷漆叠加效果、墙面剥落的真实质感、霓虹光反射、喷漆罐摆放在画面一角作为道具

**表情与姿态公式**：

- **核心情绪**：cold, disdainful, dismissive, aloof, superior — 像一位居高临下的女王在审视闯入她领地的人
- **眼神方向**：直接注视镜头，眼神锐利、冷漠、带有审视感
- **肢体语言**：放松但充满掌控感，身体微微后仰或侧倚，一只手随意支撑或拿着小道具，另一只手自然垂放或搭在膝上
- **面部细节**：嘴角微不可察的弧度，不是微笑而是轻蔑；瞳孔收缩锐利；眉毛自然不皱但带有距离感
- **禁止项**：温暖的笑容（warm smile, gentle smile, cheerful）、唱歌张嘴（singing, open mouth singing）、惊讶表情、可爱表情、温柔表情

**完整 prompt 模板**：

```
Refer to the attached reference image (Figure 1). Generate a similar style image of {角色英文名} from {游戏英文名} sitting casually in front of a bold graffiti wall. {角色名} is seated in a relaxed but confident posture, {具体坐姿描述如"leaning back against the graffiti wall with one knee raised, her other leg stretched out casually"}, with her body language calm, controlled, and slightly provocative. Her expression should show cold, disdainful eyes, aloof, sharp, and superior, as if she is silently judging the viewer.

Keep {角色名}'s recognizable features: {保留角色标志性外貌特征列表}. Blend her canonical design with a modern edgy streetwear aesthetic: {上身服装描述 — 无袖露脐+短夹克}, {下身服装描述 — 短裙或短牛仔裤}, {腿部描述 — 光腿或丝袜}, {鞋履描述}, {潮流配饰描述}. Preserve her identity while giving her a fresh urban street-style look.

The graffiti wall behind her should be vivid and layered, full of expressive abstract shapes and energetic street-art textures in {角色主题色} tones, with graffiti elements including {角色名涂鸦字体}, {元素符号涂鸦}, {主题图案涂鸦}, creating a rebellious urban backdrop that resonates with her character theme. Add subtle {角色元素名} energy effects, {角色主题特效}, and {角色标志性小道具} around her to reinforce her identity.

Use a wide cinematic framing suitable for a 16:9 wallpaper, with {角色名} as the main focal point while still showing enough of the graffiti wall and surrounding environment for atmosphere. The mood should feel cool, stylish, intimidating, and mysterious. Highly detailed background, rich shadows, {角色主题色} glowing highlights, sharp focus on {角色名}, and a refined high-end anime illustration look.
```

**负面提示词追加项**（在常规 negative prompt 基础上**必须额外追加**以下内容）：

`standing, standing pose, upright posture, singing, open mouth singing, warm smile, gentle smile, cheerful expression, cute expression, adorable, sweet, innocent, game canonical outfit, official costume, fantasy dress, medieval clothing, armor, full gown, formal dress, beach background, ocean background, nature background, indoor background, plain background, minimal background, missing graffiti wall, low detail graffiti, generic graffiti, wrong graffiti colors, wrong streetwear, missing crop top, missing jacket, missing shorts, missing skirt, long dress, full pants, business suit, school uniform`

---

#### 必需2 — 角色特写肖像 (Close-up Portrait)

每个类型 A 角色单人壁纸合集**必须包含且仅包含一条**特写肖像 prompt。这类壁纸的核心价值在于：用一个极简画面承载角色最深的叙事内核——不是展示角色"在做什么"，而是揭示角色"是什么"。

**参考图**：`![alt text](../../needful2.png)`（阿蕾奇诺手持玫瑰半遮面特写肖像，全局共享，位于工作区根目录）

**五步公式（必须全部执行）**：

1. **道具选择 — 手持、有叙事意义、有视觉质感**

   选择一个角色可以用单手夹持/举起的小物件，该物件必须与角色的故事背景、身份或核心悲剧有深层关联。不是武器（太大会变成战斗图），不是随意装饰品（无叙事重量），而是那种"如果有人问这个角色'你最在意什么'，他们会默默从口袋里掏出来的东西"。

   | 角色类型 | 道具思路 |
   |---------|---------|
   | 贵族/统治者 | 家族徽章、旧信物、枯花、酒杯 |
   | 战士/军人 | 弹壳、断裂的剑刃、勋章、旧照片 |
   | 机械/人造生命 | 齿轮、螺丝、怀表、芯片、断线 |
   | 学者/法师 | 古书页、硬币、罗盘、星图 |
   | 旅行者/流浪者 | 车票、地图碎片、干花、口琴 |

2. **空间关系 — 道具半遮一只眼（partial obscurement）**

   道具举起至眼部高度，从侧面部分遮挡角色一只眼睛。观众通过道具的边缘/孔洞/缝隙看到被遮一侧的眼球或虹膜。这种构图制造三层视觉张力：道具本身的美感 → 被遮眼若隐若现的窥视感 → 未遮眼的正面凝视。**严禁**道具完全遮住整张脸（变成面具效果）或完全不遮挡（变成展示道具的全身图）。

3. **矛盾表情 — 同时呈现两种对立情绪**

   面部表情必须让观者同时读出两种相反的情绪状态，这是整个特写肖像的灵魂。不要写"smiling"或"sad"这种单一情绪，而是写出那种需要观者定睛看一会才能解读的复杂表情。

   | 矛盾对 | 表情描述范例 |
   |--------|-------------|
   | 温柔 vs 威胁 | "simultaneously inviting and threatening, the look of someone deciding whether to kiss you or kill you" |
   | 怀旧 vs 漠然 | "detached, melancholic amusement, as if the coin reminds him of a bet he won centuries ago and no longer cares about" |
   | 渴望 vs 恐惧 | 眼神追忆着什么，但嘴角的弧度暗示她害怕找到答案 |
   | 傲慢 vs 脆弱 | 下巴微抬的贵族姿态，但瞳孔中有未经允许的颤抖 |

   技巧：用"a faint X that never reaches Y"或"the barest Z, as if..."这类句式，让情绪的表达本身也带着克制和矛盾。

4. **叙事性总结句 — 一句话点明角色的核心悲剧/悖论/双重性**

   在 prompt 的末尾（在画面比例标注之前），写一句话总结句，将道具、表情、角色设定三者收束为一个关于"这个角色是谁"的命题。这句话不是场景描述，而是角色的命运注脚。

   范例：
   - 阿蕾奇诺：「A villain who could have been a lover, a mother who chose to be a father.」
   - 菲林斯：「A fairy who outlived his kingdom, now spending eternity cataloguing what he's lost.」

5. **单光源 + 纯黑背景 — 明暗对照法 (chiaroscuro)**

   单一光源从画面一侧（通常左上或右上）45°角照射，在面部形成强烈的明暗分界。道具在光源照射方向上呈现透光/反光质感（如玫瑰花瓣透出深红光、硬币金属表面反射冷光）。背景为纯黑（pure black background），角色只有面部、手和道具存在于画面中，极简、亲密、静谧。如角色有元素属性，可在道具上加一抹元素色彩的次级光（如雷元素角色的道具边缘有淡紫色辉光）。

**完整 prompt 模板（以阿蕾奇诺为范例）**：

```
Refer to the attached reference image (Figure 2). Generate a cinematic close-up portrait of {角色英文名} from {游戏英文名}. She holds a {道具描述} close to the {左/右} side of her face, {道具与面部的空间关系}, partially obscuring her {左/右} eye. Her visible {另一侧} eye gazes directly at the viewer — {矛盾表情的完整描述}. Expression: {表情细节，包含两种对立情绪}. Dramatic single-source lighting from the upper {左/右} casts deep chiaroscuro across her features, the {道具材质} glowing {颜色} where the light passes through. Her {肤色描述} contrasts sharply against a pure black background. Her signature {发型发色描述} {头发与画面的关系}; her {服装描述} is only barely visible at the collar. {叙事性总结句}. 16:9 2K wallpaper.
```

**负面提示词要点**：在常规 negative prompt 基础上额外排除 `full body shot, wide shot, landscape, multiple subjects, busy background, bright cheerful lighting, outdoor scene, action pose, weapon drawn`——特写肖像的极简画面反过来要求 negative prompt 更积极地排除一切非特写元素。

---

### 类型 B：主题类型合集

选定一个主题，横跨 4~6 个不同角色，每角色 1~2 条 prompt。

**适用场景**：节日/赛事热点、季节主题、风格主题（赛博朋克、古风、校园等）

**结构**：
- 文件头注明主题名称、热点背景
- 需要一张主题风格的参考图（第一张生成的图可作为后续角色的风格参考）
- 每个角色一个 `##` 段落，包含：角色名 + 该主题下的完整 prompt
- 所有角色的服装/场景/构图需保持主题一致性，仅改变角色外貌特征和配色

**Prompt 要点**：
- 第一个角色的 prompt 最详细（定义整体风格基调）
- 后续角色 prompt 引用第一张图作为风格参考（`Referring to the attached image, generate a similar style image for {角色名}`）
- 每个角色的主色需要替换（如足球宝贝主题中，安比是绿黑、妮可是黑白）
- 保留每个角色的标志性特征（发型、发饰、尾巴等）

**目录**：`主题类型/{主题名}/prompts.md`

---

### 类型 C：可爱动物萌化形象合集

选 5~8 个不同角色，每个角色 1 条萌化 prompt，统一为同一种动物形象（如猫猫、兔兔）。

**适用场景**：日常无特殊热点、调节视频节奏、社区萌系需求

**结构**：
- 文件头注明动物类型（猫猫/兔兔/etc）
- 需要一张设定图作为基础参考（第一个角色生成后即为后续参考）
- 每个角色一个 `##` 段落

**Prompt 要点**：
- 动物品种可根据角色气质选择（如高冷角色→布偶猫、活泼角色→橘猫）
- **必须保留**的角色特征：主色调（毛色）、标志性头饰/配饰、瞳色、呆毛/特殊发型
- **移除**：人类衣服（除非角色衣服是极度标志性的），人类头发
- **可保留**：项圈/颈饰（替代项链）、小帽子、耳饰
- 背景要求：简洁、不过于复杂，匹配角色性格和主色调
- 可添加角色相关的小道具/玩具（如角色的召唤物、武器缩小版）
- 画面比例：16:9 2K wallpaper
- 后续角色 prompt 引用前面生成的图作为风格参考，确保系列一致性

**目录**：`动物化/{动物形象}/prompts.md`（如 `动物化/猫猫形象/cat-prompts.md`）

---

### 类型 D：表情包合集

选定一个角色的一种形象（可以是动物化、Q版、正常形象），围绕该形象生成 8~12 个不同表情/动作。

**适用场景**：某角色的梗/二创在社区爆火、已有该角色的萌化设定图可复用

**结构**：
- 文件头注明角色和形象类型（如"芙宁娜·猫咪形象"）
- 需要一张该角色形象的设定图作为基础参考
- 每个表情一个 `##` 段落，标题为表情名称

**Prompt 要点**：
- 画面比例：**1:1**（表情包专用）
- 所有表情必须基于**同一角色形象**，保持风格、线条、色彩一致
- 每条 prompt 需描述：表情（面部表情细节）、动作（肢体姿态）、文字（如有玩梗文字需注明内容和位置）、背景（简洁或纯色）
- 表情建议覆盖常用情绪：得意、疑惑、惊慌、无语、喜欢、顿悟、思考、生气、哭泣、偷笑、加油、摆烂
- Prompt 语言可以是中文（表情包更贴近中文社区用语习惯）
- 玩梗文字直接写在 prompt 中（如"不愧是我"、"顿悟"）

**目录**：`表情包/{角色名}-{形象类型}/prompts.md`

---

### 类型 E：梗图合集

选 3~5 个不同角色，每个角色基于社区热梗生成一张"梗形象图"（如冰女皇变蜜雪雪王、艾莲变笨蛋鲨鲨、大黑塔变严厉导师）。

**适用场景**：社区有多个角色的梗同时流行、节日/版本更新引发大量二创整活

**与类型 D 的区别**：D 是一个角色的多种表情（同一形象变表情），E 是多个不同角色各变成一个完全不同的梗人设。

**结构**：
- 文件头注明梗图主题和热点背景
- 每个角色一个 `##` 段落，标题为 `{角色名}·{梗形象名}`
- 第一个角色的 prompt 最详细，后续可引用第一张图保持风格统一

**Prompt 要点**：
- 画面比例：**3:4**（竖版梗图，适合手机浏览和社交分享）
- **核心原则**：保留角色的标志性特征（发色、瞳色、标志性配饰），但整体形象和服装完全改成梗的风格
- 每条 prompt 需描述：梗形象的概念来源（如"蜜雪冰城雪王"）、角色保留的特征、梗风格的服装/造型、动作与表情（要夸张、有梗感）、背景（简洁或与梗相关的场景）
- 风格可以夸张、搞笑、反差，不必忠于原设定
- 可添加与梗相关的文字或标志（如蜜雪冰城的"你爱我我爱你"）
- Negative Prompt 需排除与梗冲突的元素（如做搞笑梗时排除 `serious, dark, edgy`）

**梗形象设计思路**：
- 品牌联动型：角色变成某品牌吉祥物风格（如冰女皇→蜜雪雪王）
- 职业反差型：角色变成反差职业形象（如大黑塔→严厉学术导师）
- 动物/物品拟化型：角色变成某种搞笑动物或物品（如艾莲→西瓜帽笨蛋鲨鲨）
- 名画/名场面型：角色融入世界名画或经典影视场面
- 网络流行语型：角色演绎当前网络流行梗

**目录**：`梗图/{主题名}/prompts.md`（如 `梗图/蜜雪冰城系列/prompts.md`）

---

## 参考图处理（通用）

### 官方参考图

官方立绘（splash art、gacha art）的下载流程已内嵌在上方「类型 A → 参考图下载」中，包含四级回退链路和具体命令。**所有视频类型**在需要角色参考图时，均按该流程执行。完整来源文档见 [image-sources.md](image-sources.md)。

### 跨领域参考图（类型 A 专用）

根据角色的**多个维度标签**，从真实世界中寻找对应领域的高质量参考素材（照片、名画、海报等），下载到角色目录，并编写融合 prompt。核心价值：将真实世界的专业美学注入游戏角色，产出更有艺术感和独特性的壁纸。

**多维度标签体系**：

每个角色可同时匹配多个维度，建议从 2~3 个维度交叉搜索参考图：

| 维度 | 说明 | 搜索方向示例 | 参考素材类型 |
|------|------|-------------|-------------|
| 职业/技能 | 角色的职业或战斗方式 | 芭蕾舞者→天鹅湖演出照、德加名画；剑士→剑道摄影、浮世绘；弓箭手→射箭运动、阿尔忒弥斯雕塑 | 职业摄影、古典绘画 |
| 物种/种族 | 非人类角色的物种设定 | 仙灵→精灵插画、神话生物；妖怪→日本妖怪绘卷；机甲→科幻概念图；人偶→木偶戏剧照 | 神话插画、概念艺术 |
| 身份/阵营 | 角色的组织归属和社会身份 | 愚人众→军事摄影、noir电影；骑士团→中世纪骑士画；王室→皇室加冕油画；侦探→黑色电影海报 | 军事摄影、历史绘画、电影海报 |
| 元素/属性 | 角色的元素能力视觉特征 | 冰→冰川风光摄影；火→火山熔岩摄影；雷→闪电风暴摄影；水→深海/瀑布摄影 | 自然风光摄影 |
| 性格/气质 | 角色的情感特质和气场 | 高冷→时尚杂志冷调肖像；活泼→街头快拍；腹黑→暗黑哥特艺术；温柔→印象派柔光 | 时尚摄影、情绪摄影 |
| 地域/文化 | 角色所属地区的现实文化原型 | 至冬→东欧/俄罗斯风光、冬宫油画；璃月→中国山水画、水墨；稻妻→日本浮世绘、和风摄影 | 风光摄影、民族艺术 |

**交叉搜索示例**：

| 角色 | 维度 1 | 维度 2 | 维度 3 | 参考素材组合 |
|------|--------|--------|--------|-------------|
| 奥黛塔 | 芭蕾舞者 | 愚人众成员 | 冰元素 | 德加芭蕾画 × 间谍noir摄影 × 冰川风光 |
| 夜兰 | 间谍/特工 | 水元素 | 璃月文化 | noir电影海报 × 深海摄影 × 中国水墨画 |
| 11号 | 军人 | 火元素 | 赛博朋克 | 军事阅兵摄影 × 火山摄影 × 赛博朋克概念图 |
| 妮露 | 舞者 | 水元素 | 须弥文化 | 波斯细密画 × 瀑布摄影 × 中东舞蹈海报 |

**搜索来源**：Pixabay（免费可商用照片）、WikiArt/维基百科（世界名画）、Unsplash（高质量摄影）

**融合 prompt 写法要点**：
1. 明确指出参考图的来源和具体要参考什么（构图/姿态/光影/氛围）
2. 角色本身保持游戏角色设计的清晰度（面部、发色、标志性配饰不变）
3. 环境/氛围/画风可大胆融合参考素材的风格（如印象派笔触、电影光影）
4. 用角色的元素能力为参考场景增加独特变化（如冰元素让舞台结霜）
5. 在 Negative Prompt 中排除不想要的风格冲突

跨领域参考图在 prompts.md 中放在 `# 跨领域参考图` 段落下，命名格式 `ref-{描述}.jpg/png`。

---

## 输出目录结构

```
{workspace}/
├── needful.png                          # 涂鸦墙模板参考图（全局共享）
├── 原神/{角色名}/
│   ├── prompts.md                       # 类型 A
│   ├── titles.md                        # 视频发布文案
│   ├── splash-art.png
│   ├── gacha-art.png
│   └── ref-{描述}.jpg                   # 跨领域参考图
├── 绝区零/{角色名}/
│   ├── prompts.md                       # 类型 A
│   └── titles.md
├── 崩坏星穹铁道/{角色名}/
│   ├── prompts.md                       # 类型 A
│   └── titles.md
├── 主题类型/{主题名}/
│   ├── prompts.md                       # 类型 B
│   └── titles.md
├── 动物化/{动物形象}/
│   ├── {animal}-prompts.md              # 类型 C
│   └── titles.md
├── 表情包/{角色名}-{形象类型}/
│   ├── prompts.md                       # 类型 D
│   └── titles.md
└── 梗图/{主题名}/
    ├── prompts.md                       # 类型 E
    └── titles.md
```

---

## Phase 4: 视频发布文案生成

Prompts 生成完毕后，**必须**额外生成一份 `titles.md` 文件，放在与 `prompts.md` 同一目录下，供视频发布使用。

### 文案结构

`titles.md` 需包含以下几个板块，每个板块提供 **2 个备选方案**。

**前置要求**：标题生成前必须已完成 Phase 1 第 6 步「角色社区梗与爱称搜索」。搜索结果（爱称、弹幕热词、强度标签、PV金句、趣味设定描述等）需记录在 `titles.md` 文件头部，格式为带 URL 的有序列表，按参考权重排序（参见 Phase 1 第 6 步的输出要求）。这些素材是梗向、强度向标题的核心来源。

**一、唯美向标题方案**（突出视觉美感、角色气质、诗意表达）

每个方案包含：标题（一行，含角色名+主题关键词+画质标注如"4K壁纸合集"）、简介（2~3 段，包含角色官方台词或设定引用、本期壁纸场景清单、画质/比例说明、引导三连互动）。优先使用角色PV金句或官方诗句作为标题（如「似隼疾掠，弋猎于冬」），也可用叙事性长标题讲一个迷你故事引发好奇心。避免泛用型形容词（"绝美""超好看"），追求角色专属的意境表达。

**二、角色向标题方案**（突出角色人设、故事、情感反差）

每个方案包含：标题（一行，带角色粉丝向用语如"XX厨必收"）、简介（融入角色背景故事线索，用叙事串联本期壁纸场景，突出情感共鸣）。善用角色的性格反差（如"战斗时喊XX冲锋，回家后给XX揉肚子"），标题本身就要讲一个让人想点进来看的小故事。可以使用同伴/宠物/武器等角色标志性元素的名字（如"图加林"）增加粉丝辨识度。

**三、梗向/趣味标题方案**（利用社区热词、角色梗、官方趣味描述）

每个方案包含：标题（一行，直接使用社区梗语言或角色趣味设定）、简介（轻松有趣，用梗点作为钩子引入，再展开壁纸内容）。素材来源：

- 角色获取方式相关梗（如"白嫖战神""免费四星""不花一颗原石"）
- 官方装扮描述中的趣味细节（如"帽子是狗头因为很可爱"）
- 社区情绪热词（如"原神终于能养狗了""遛狗模拟器"）
- 角色同伴/宠物相关梗（角色与同伴的互动是天然的梗素材）

**四、强度向/话题标题方案**（利用强度讨论、配队话题制造争议性点击）

每个方案包含：标题（一行，引用攻略区热门强度对比或配队讨论话题）、简介（先用强度话题吸引点击，再引导到壁纸内容本身）。素材来源：

- 攻略区强度标签（如"4星雷奶凭什么叫板八重神子？"）
- 配队讨论热点（如"木偶最强队友的12种打开方式"）
- 角色定位争议（"下位替代""重新定义四星"等话术）

注意：强度向标题的争议性是优势而非缺点——评论区讨论越激烈，互动量越高。但简介内容要回归壁纸美学，不要变成纯强度讨论帖。

**五、互动向标题方案**（突出抽卡许愿、评论互动）

每个方案包含：标题（一行，带抽卡/许愿/欧气等互动话术）、简介（轻松活泼语气，引导点赞三连+评论区许愿+关注）。

**六、短视频/Shorts 标题**（15-30 秒快节奏版本）

提供 5 条简短有力的标题（不需要简介），需覆盖不同风格维度：至少包含 1 条金句/诗意型、1 条梗向/趣味型、1 条强度/话题型、1 条节奏型（如"0.5秒一张"）、1 条粉丝向型（如"XX厨进"）。

**七、发布小贴士**

- 封面图建议：推荐哪张壁纸做封面 + 加什么文字
- 标签推荐：`#原神 #角色名 #GenshinImpact #英文角色名 #壁纸 #4K壁纸 #原神壁纸` 等（根据具体角色和游戏调整）
- 配乐建议：推荐使用角色演示 PV 或版本 PV 的 BGM
- 发布时间建议：角色生日、版本上线日等特殊节点

### 四种视频类型的文案差异

| 类型 | 唯美/角色向侧重 | 梗向/趣味侧重 | 强度/话题侧重 |
|------|---------------|-------------|-------------|
| A 角色单人合集 | PV金句 + 角色故事叙事 + 场景数 | 角色爱称/外号 + 获取方式梗 + 同伴/宠物梗 + 装扮趣味描述 | 强度定位标签 + 同类角色对比 + 配队讨论热词 |
| B 主题类型合集 | 主题诗意表达 + 角色阵容串联 | 主题与角色的反差/趣味碰撞（如"足球宝贝但是二次元"） | 角色阵容强度讨论（如"这队能打深渊吗"） |
| C 动物萌化合集 | 萌宠/猫猫 + 角色气质匹配 | 品种选择的趣味理由（如"高冷角色当然是布偶猫"） | 不适用（萌化类型无强度话题） |
| D 表情包合集 | 角色名 + 表情包 + 情感共鸣 | 玩梗文字 + 使用场景 + 社区热梗引用 | 不适用（表情包类型无强度话题） |
| E 梗图合集 | 名画/名场面的艺术感呈现 | 梗形象本身就是趣味核心，标题直接用梗名 | 不适用（梗图类型无强度话题） |

### 输出文件

`titles.md` 与 `prompts.md` 放在同一目录下。参考格式见 [titles-template.md](titles-template.md)。

---

## 自动化建议

本 skill 适合配合 CatPaw automation 设为每日定时任务（如每天早上 9:00），自动执行完整工作流并将 prompts 文件写入工作区。

每日节奏建议：以类型 A（角色单人合集）为主力，穿插类型 B（热点主题）、C（萌化）、D（表情包）、E（梗图）调节节奏。比如一周 7 天可以安排为 A-A-B-A-C-A-D，遇到社区梗爆火时替换为 E。
