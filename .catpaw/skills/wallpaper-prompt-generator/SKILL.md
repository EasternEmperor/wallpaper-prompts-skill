---
name: wallpaper-prompt-generator
description: 米哈游游戏角色壁纸 AI 生图 prompts 每日生成工具。根据游戏热点（原神/绝区零/崩铁版本更新、前瞻直播、新角色上线）、社区热度（B站/小红书/米游社）、时事节日、角色人气，自动决策当天要制作哪个角色的壁纸，并生成 12 条左右高质量 prompts（含 positive/negative prompt、背景场景、人物动作描述）。触发词：生成壁纸prompts、今日壁纸、每日壁纸、wallpaper prompts、角色壁纸、游戏壁纸、原神壁纸、绝区零壁纸、崩铁壁纸、米哈游壁纸、签图、抽签壁纸、签文壁纸。注意：签图（类型 F）仅限用户手动触发，每日定时任务不得自动生成。
---

# 米哈游游戏角色壁纸 Prompts 每日生成

## 工作流概览

三阶段流水线：**热点搜索 → 类型与角色决策 → Prompts 生成 + 发布文案**

每天的产出对应一条**视频**的素材合集。视频有七种类型（A~G），各类型的详细生成规范拆分在 [references/](references/) 目录，主文件只保留流程、通用规范与类型路由。

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

| 类型 | 说明 | 角色数量 | 每角色 prompts | 总 prompts |
|------|------|----------|---------------|-----------|
| A. 角色单人壁纸合集 | 围绕一个角色，多场景多风格 | 1 个 | 12 条左右 | ~12 |
| B. 主题类型合集 | 同一主题，横跨多个不同角色 | 4~6 个 | 每个 1~2 条 | ~10 |
| C. 可爱动物萌化形象合集 | 不同角色的动物拟化壁纸 | 5~8 个 | 每个 1 条 | ~8 |
| D. 表情包合集 | 同一角色的玩梗表情包 | 1 个 | 8~12 条 | ~10 |
| E. 梗图合集 | 不同角色各自的梗形象图 | 3~5 个 | 每个 1~2 条 | ~8 |
| G. 视觉定位系列 | 固定视觉母定位下角色×子场景成套出图 | 1 或 3 个 | 3 或 1 | 3 |

**类型选择依据**：

- 有重大热点（新角色上线/前瞻直播）→ 优先 **A**（聚焦该角色深度呈现）
- 有时事主题（节日/赛事）适合多角色横向展示 → 优先 **B**（如世界杯足球宝贝）
- 近期没做过萌化/表情包，需要调节节奏 → 选 **C** 或 **D**
- 社区有某角色的梗/二创爆火 → 选 **D**（围绕该角色做表情包）或 **E**（多角色梗形象合集）
- 社区有多个角色的梗同时流行 → 优先 **E**（如冰女皇蜜雪雪王、艾莲笨蛋鲨鲨同时流行）
- 日常无特殊热点 → 在 A/C 中选人气角色；存在激活中的视觉定位系列时 → 续更 **G**（见 [type-g-visual-series.md](references/type-g-visual-series.md)）
- 类型 A 候选最优角色为男性且不满足性别例外条款 → 优先改选 **B/E** 多角色合集，将男性角色作为其中一员消化（男性角色单人集播放量/阅读量显著偏低）

### 第二步：选定角色

综合以下维度评分：

| 维度 | 权重 | 说明 |
|------|------|------|
| 游戏官方热点 | 40% | 新角色上线、前瞻直播、版本更新当天权重最高 |
| 社区讨论热度 | 25% | B站/小红书/米游社的近期讨论量和趋势 |
| 时事/节日契合 | 20% | 角色气质与当天节日/赛事/季节的匹配度 |
| 已有素材覆盖 | 15% | 优先选未做过的角色，查看工作区已有目录避免重复 |

**性别流量权重（仅类型 A 适用）**：

历史数据表明：类型 A 角色单人壁纸合集中，**男性角色的播放量/阅读量显著低于女性角色**。因此在类型 A 选角时，对综合评分引入性别系数：

- **女性角色**：系数 1.0，不调整
- **男性角色**：系数 **0.5**（综合得分减半，即男性候选需要约一倍的热点强度才能与女性候选同等入选）

执行细则：

1. 惩罚系数**仅在类型 A 生效**。类型 B/C/D/E 为多角色合集，单角色占比小、男性角色流量损失小，按正常维度评分即可。
2. 候选最优角色为男性且不满足下方例外条款时，**优先改选类型 B 或 E 多角色合集**消化该男性角色，避免出单人集。
3. 男性角色仍可入选类型 A 的例外情况（三选一）：
   - 官方热点**独家且不可替代**（如该男性角色是版本首发主角、限时活动唯一核心），且当天无同热度女性候选；
   - 该男性角色的生日/纪念等强时效节点当天无其他可比热点；
   - 用户明确指定角色。
4. 决策记录：在 prompts.md 头部「选定角色理由」中写明是否触发性别调整及理由，便于后续复盘流量数据、校准系数。

**决策输出**：在 prompts.md 头部注释中明确写出：选定类型、选定角色、各维度考量理由。

### 无热点降级策略

当天 web_search 失败或确认无可用热点（版本真空期、无节日、无梗爆火）时，按序降级：

1. 回退类型 A：从工作区覆盖池（结合 `reference-registry.md` 已校对索引与各游戏目录）中选**未做过单人集**的最高人气女性角色，正常执行完整工作流
2. 覆盖池耗尽时，选距上次单人集最久的角色，换全新角度（全新场景体系/服装主题）
3. 文件头「选定角色理由」标注「无热点日常期」，并在 automation memory.md 记录降级原因

---

## Phase 3: Prompts 生成

先按下方「类型路由」确定详细规范文件，再结合本节通用规范执行。

### 通用规范（适用所有类型）

**Positive Prompt 必含项**：
- 画面比例与用途（如 `16:9 2K wallpaper`、`9:20 mobile wallpaper`、`4:3 tablet wallpaper`、`√2:1 foldable wallpaper`、`1:1 表情包`）
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

**腿部/坐姿质量优化（必须执行，与手部同级）**：

坐姿是仅次于手部的第二画崩高发区（大腿根与髋部衔接断裂、双膝朝向矛盾、小腿拉长扭曲）：

1. **禁用高危姿势写法**：跷二郎腿（`one leg crossed over the other` / `legs crossed`）、单脚钩栏杆（`one heel hooked on the lower bar`）、双臂后撑侧转身的复合坐姿、单腿朝镜头伸直的透视缩短姿势（`leg stretched out toward the viewer`，小腿与脚易被前景遮挡吞没）——需要表现伸腿时改为屈膝落地 `foot flat on the ground`。

2. **安全坐姿写法**（三选一）：侧坐双腿同侧（`sitting side-saddle, both knees together and pointing in the same direction, calves hanging down side by side in natural parallel alignment`）；正坐双膝并拢（`sitting upright, knees together, feet flat on the ground`）；或直接改站立（`standing, weight on one leg, natural stance`）。

3. **Negative Prompt 腿部穷举**（每条必含，接在手部穷举之后）：
`missing legs, missing feet, missing calves, cropped legs, legs out of frame, twisted legs, rotated hips, dislocated hip, extra legs, third leg, fused legs, malformed knees, knees bending in opposite directions, unnatural sitting pose, disproportionate limbs, elongated calves, deformed feet`

4. **Positive 解剖锚定**（坐姿/腿部可见时必含）：`correct hip-to-thigh-to-knee anatomy, natural leg proportions, both legs in natural parallel alignment, natural seated posture`

**风格参考图作用域（B/C/E 通用，必须执行）**：

合集类型中，后续角色 prompt 引用第一张（或前面已生成）图时，必须在 prompt 开头显式锁定作用域：`Referring to the attached first artwork for style, lighting, and {当期主题} atmosphere only, generate ...`，并保证**不复制参考画面中的人物姿态、服装与构图**——继承系列成套感的同时，避免产图姿态雷同。

### 类型路由（详细生成规范见 references/）

| 类型 | 一句话定义 | 比例 | 条数 | 详细规范 | 输出目录 |
|------|-----------|------|------|---------|---------|
| A 角色单人壁纸合集 | 一个角色多场景多风格，含涂鸦墙/特写肖像/性感风三条固定模板线 | 混合（16:9/9:20/4:3/√2:1） | ~12 | [type-a-single-character.md](references/type-a-single-character.md) | `原神\|绝区零\|崩坏星穹铁道/{角色名}/` |
| B 主题类型合集 | 一个主题横跨 4~6 角色，统一视觉母题 | 统一 3:4 竖版 | ~10 | [type-b-theme.md](references/type-b-theme.md) | `主题类型/{主题名}/` |
| C 动物萌化 | 5~8 角色统一动物拟化 | 16:9 | ~8 | [type-c-animal.md](references/type-c-animal.md) | `动物化/{动物形象}/` |
| D 表情包 | 单角色同一形象 8~12 表情玩梗，prompt 可中文 | 1:1 | 8~12 | [type-d-emoji.md](references/type-d-emoji.md) | `表情包/{角色名}-{形象类型}/` |
| E 梗图 | 3~5 角色各自变成热梗形象 | 3:4 | ~8 | [type-e-meme.md](references/type-e-meme.md) | `梗图/{主题名}/` |
| F 签图 | 统一模板抽签文壁纸（签名/签位/签语） | 9:20 | 按签数 | [references/fortune-slip.md](references/fortune-slip.md) | `主题类型/{签图系列名}/` |
| G 视觉定位系列 | 固定视觉母定位下「角色×子场景」成套出图，每期 3 张 | 统一 3:4 | 3 | [type-g-visual-series.md](references/type-g-visual-series.md) | `视觉企划/{系列名}/` |

⚠️ **类型 F 触发红线**：仅限用户当次明确指定时生成，**每日定时任务严禁自动产出签图**。

⚠️ **类型 G 触发边界**：新系列立项仅限用户手动确认；已有激活系列（存在 bible.md）可自动化续更下一期。

---

## Phase 3 产出自检（每期必跑）

prompts.md 写完后必须执行以下校验，全部通过才算完成：

1. 段落数 = 计划总条数；每条均含 Positive Prompt 与 Negative Prompt 两段
2. 比例标注齐全：目标比例字符串（如 `3:4 vertical portrait wallpaper`）出现次数 = 总条数
3. 禁用高危姿势 0 残留：`stretched out casually` / `leg stretched out toward the viewer` / `one heel hooked`
4. 手部穷举与腿部穷举在每条 Negative 中完整（`fused fingers`、`malformed knees` 计数均 = 总条数）
5. 所有 `![alt text](...)` 参考图路径真实存在（逐个做文件存在性测试）
6. 无 `{角色名}` 等模板占位符残留（搜索 `{` 应为 0）

可在产出目录执行的速查命令：

```bash
grep -c '^## [0-9]' prompts.md                    # 1. 条数
grep -c 'Negative Prompt' prompts.md             # 1. 应等于条数
grep -c '3:4 vertical portrait wallpaper' prompts.md  # 2. 按当期比例替换，应等于条数
grep -ci 'stretched out casually\|leg stretched out toward the viewer\|one heel hooked' prompts.md  # 3. 应为 0
grep -c 'fused fingers' prompts.md               # 4. 应等于条数
grep -c 'malformed knees' prompts.md             # 4. 应等于条数
grep -c '{' prompts.md                           # 6. 应为 0
```

---

## 参考图处理（通用）

### 官方参考图下载（四级回退，所有类型通用）

开始写 prompts 前，**必须先执行**以下流程下载官方立绘。下载的参考图用于校对角色外观描述（发色、服装、配饰等），确保 prompts 与官方设定一致。按以下优先级依次尝试，某一级成功即停止：

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

**⚠️ 校对必须用视觉工具实际看图**：下载完成后，必须用视觉工具（如 read_file 直接读图）逐张打开参考图，肉眼确认发色、瞳色、发型、服饰、配饰等细节，再动笔写 prompts。**严禁只凭文件下载成功就认为校对完成**，也严禁仅凭 web_search 的文字描述推断外观。

### 引用已有参考图前必须视觉校对（硬性要求）

不限于新下载文件：**任何类型**引用工作区已存在的参考图前，都必须用视觉工具逐张打开，确认「文件内容 = 文件名/预期角色」且分辨率可用。发现错位（A 角色目录里存的是 B 角色立绘、AI 生成图冒充官方素材、缩略图冒充原图）时：禁用该文件，改用同目录其他文件或重新下载，并登记到 `reference-registry.md` 黑名单。早期 `image.png` 命名的历史文件是错位重灾区，重点核查。

反面案例（2026.10.01）：`原神/宵宫/image.png` 实为耀嘉音官方立绘、`绝区零/耀嘉音/splash-art.png` 为 AI 生成的刻晴壁纸、`崩坏星穹铁道/流萤/original-splash-art.png` 为 100px 缩略头像。

### 参考图登记表（reference-registry.md）

工作区根目录维护 `reference-registry.md`：已校对参考图索引 + 错位文件黑名单。执行前先查表——已登记文件可免重复校对，黑名单文件直接跳过。

**每期执行结束后的维护规则**：

- 本期为已有角色新增/下载了参考图 → 在该角色已有条目中**追加**新文件相对路径、内容摘要与校对日期
- 本期覆盖的角色在表中无记录 → **新增条目**（角色目录、文件相对路径、内容摘要、校对日期）
- 本期发现内容错位的文件 → 追加到黑名单
- 已有条目不重复登记、不删除

---

## 输出目录结构

```
{workspace}/
├── reference-registry.md                # 参考图登记表（已校对索引 + 错位黑名单）
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
│   ├── prompts.md                       # 类型 B / F
│   └── titles.md
├── 动物化/{动物形象}/
│   ├── {animal}-prompts.md              # 类型 C
│   └── titles.md
├── 表情包/{角色名}-{形象类型}/
│   ├── prompts.md                       # 类型 D
│   └── titles.md
├── 梗图/{主题名}/
│   ├── prompts.md                       # 类型 E
│   └── titles.md
└── 视觉企划/{系列名}/
    ├── bible.md                         # 类型 G 定位圣经（唯一权威文档）
    ├── prompts.md                       # 类型 G 当期 3 条
    └── titles.md
```

涂鸦墙/特写肖像模板参考图（`needful1-woman.png`、`needful1-man.png`、`needful2.png`）随本 skill 存放于 skill 目录的 `references/` 下，引用方式见 [type-a-single-character.md](references/type-a-single-character.md)「模板参考图位置」。

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

### 各类型文案侧重差异

| 类型 | 唯美/角色向侧重 | 梗向/趣味侧重 | 强度/话题侧重 |
|------|---------------|-------------|-------------|
| A 角色单人合集 | PV金句 + 角色故事叙事 + 场景数 | 角色爱称/外号 + 获取方式梗 + 同伴/宠物梗 + 装扮趣味描述 | 强度定位标签 + 同类角色对比 + 配队讨论热词 |
| B 主题类型合集 | 主题诗意表达 + 角色阵容串联 | 主题与角色的反差/趣味碰撞（如"足球宝贝但是二次元"） | 角色阵容强度讨论（如"这队能打深渊吗"） |
| C 动物萌化合集 | 萌宠/猫猫 + 角色气质匹配 | 品种选择的趣味理由（如"高冷角色当然是布偶猫"） | 不适用（萌化类型无强度话题） |
| D 表情包合集 | 角色名 + 表情包 + 情感共鸣 | 玩梗文字 + 使用场景 + 社区热梗引用 | 不适用（表情包类型无强度话题） |
| E 梗图合集 | 名画/名场面的艺术感呈现 | 梗形象本身就是趣味核心，标题直接用梗名 | 不适用（梗图类型无强度话题） |
| G 视觉定位系列 | 定位美学叙事 + 「下一张怎么玩这个角色」的系列悬念 | 定位与角色气质的趣味碰撞（如「刻晴但她是浮世绘美人」） | 不适用（系列无强度话题） |

### 输出文件

`titles.md` 与 `prompts.md` 放在同一目录下。参考格式见 [titles-template.md](titles-template.md)。

---

## 自动化建议

本 skill 适合配合 CatPaw automation 设为每日定时任务（如每天早上 9:00），自动执行完整工作流并将 prompts 文件写入工作区。

每日节奏建议：以类型 A（角色单人合集）为主力，穿插类型 B（热点主题）、C（萌化）、D（表情包）、E（梗图）调节节奏。比如一周 7 天可以安排为 A-A-B-A-C-A-D，遇到社区梗爆火时替换为 E；存在激活中的 G 系列时，可在无热点日常期替换续更。

⚠️ **签图（类型 F）永远不进入自动化范围**：每日定时任务仅限类型 A~E 及 G 系列续更，automation 的 prompt 中不得包含签图生成指令或新系列立项指令；签图只在用户当次手动指定时生成（详见 [references/fortune-slip.md](references/fortune-slip.md) 触发红线），G 新系列立项同样仅限用户手动确认。
