# 类型 A：角色单人壁纸合集

围绕一个角色，多场景多风格，约 12 条 prompts。主 SKILL.md 的通用规范（Positive/Negative 必含项、手部/腿部穷举、尺度红线）同样适用，此处不再重复。

## 结构

| 段落 | 数量 | 说明 |
|------|------|------|
| 必需·涂鸦墙街头风 | 1 | **先判定角色性别**：女引用 `needful1-woman.png`，男引用 `needful1-man.png`；现代街头服饰 + 涂鸦墙，冷漠/不屑表情 |
| 必需·特写肖像 | 2 | 16:9 横版 + 9:20 手机竖屏版（竖版为胸部及以上或半身构图，不出全身）；引用 `needful2.png`，道具半遮面 + 矛盾表情 + 单光源暗背景，见下方「必需2 — 角色特写肖像」公式 |
| 角色设定场景 | 2 | 忠于游戏世界观的经典场景（剧情、日常、标志性地点） |
| 现代风改造 | 1~2 | 御姐/可爱/赛博朋克/学院风等现代服饰改造 |
| 情感/日常/反差 | 1 | 温馨日常、反差萌、私人时刻 |
| 热点主题特别版 | 0~1 | 结合当天时事（节日/赛事/纪念日），如无则省略 |
| 动漫性感风 | 4 | 2D 日漫风 + 性感妩媚服装三型分配 + 简约朴素场景背景，四比例系列（手机 9:20 / 电脑 16:9 / iPad 4:3 / 阔折叠 √2:1），见下方「动漫性感风 — 2D 日漫简约背景系列」 |
| 跨领域参考图 | 1~2 | 基于角色职业对应的真实世界素材（照片/名画/海报），见文末 |

## 模板参考图位置

三张全局模板图随本 skill 存放于 `references/` 目录（`needful1-woman.png` / `needful1-man.png` / `needful2.png`）。在角色目录 `原神|绝区零|崩坏星穹铁道/{角色名}/prompts.md` 中引用时使用相对路径：

```
![alt text](../../../.catpaw/skills/wallpaper-prompt-generator/references/needful1-woman.png)
```

## 伴生元素必须单独找参考图（易漏项）

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

## 必需1 — 涂鸦墙街头风 (Graffiti Wall Street Style)

每个类型 A 角色单人壁纸合集**必须包含且仅包含一条**涂鸦墙街头风 prompt。这是视频系列视觉辨识度最高的封面级 prompt，核心锚点是：**角色必须坐在涂鸦墙前、穿现代街头风服装、表情冷漠不屑**。

**参考图（按角色性别二选一，全局共享，位于本 skill `references/` 目录）**：

- **女性角色**：`needful1-woman.png`（刻晴坐于涂鸦墙前的街头风壁纸）
- **男性角色**：`needful1-man.png`（砂金·戏浪坐于涂鸦墙前的街头风壁纸）

**⚠️ 性别判定与参考图选择（写 prompt 前的第一步，不可跳过）**：

1. 先依据官方立绘/头像/游戏内模型判定角色性别；拿不准时必须看图确认，宁可信官方资料也不要猜（体型描述如「少年」「小男孩」「成男」均可作为辅助判据）。
2. 女性角色引用 `needful1-woman.png` 并使用下方**女版服装公式与模板**；男性角色引用 `needful1-man.png` 并使用**男版服装公式与模板**。严禁男角色套用女版公式。
3. **参考图的作用域必须锁定**：它只提供构图、坐姿气质、涂鸦墙风格与整体氛围参考。prompt 中必须显式声明人物性别并加入体型锚定词，并在模板开头写明参考图仅用于构图/背景/氛围（"for composition, graffiti-wall style, and overall atmosphere only"），防止参考图角色的性别气质（长发、曲线、妆容、露肤方式）污染产图。

**反面案例（2026.09.15 米提亚）**：男角色直接套用女版公式与女参考图，保留了 crop top + 牛仔短裤等女性符号，且未锁定参考图作用域，产图出现明显女性化特征（身形曲线化、妆容化）。**教训：性别判定必须先行，男版女版公式不可混用，参考图作用域必须显式限定。**

**核心四约束（不可偏离，按优先级排序）**：

| 优先级 | 约束项 | 硬性要求 |
|--------|--------|----------|
| 1 | 角色姿态 | **必须坐着**，如坐于矮墙/木箱/折叠椅/摩托车座/地面等，严禁站立 |
| 2 | 背景 | **必须是涂鸦墙**，色彩与角色主题色匹配，含角色名/元素符号/主题涂鸦元素 |
| 3 | 表情与眼神 | **必须冷漠、不屑、居高临下**，silently judging the viewer，严禁温暖/甜美/可爱/唱歌等表情 |
| 4 | 服装风格 | **必须是现代街头风**，严禁使用游戏原设定服装（除非原设定本身就是街头风） |

**服装公式（按性别二选一）**：

上身和下身必须同时满足以下规范，且需**突破原游戏设定**进行现代潮流改造：

**女版（女性角色专用）**：

- **上身**：无袖露脐短款上衣（crop top / tube top / 紧身短款背心） + 敞开的短夹克（cropped jacket / 短款机车夹克 / 短款运动外套），夹克可半脱式搭在肩上
- **下身**：短裙（skater skirt / pleated mini skirt）或短牛仔裤（denim shorts / 破洞短裤），必须露出大部分腿部线条
- **腿部**：光腿或搭配丝袜/过膝袜（根据角色气质选择，颜色需与角色主题色呼应）
- **体型锚定**：必须写入女性身形描述（如 slender feminine figure），与参考图气质呼应
- **鞋履**：运动鞋 / 马丁靴 / 厚底鞋，避免正式皮鞋或原设高跟鞋
- **配饰**：链条项链 / 耳钉 / 手环 / 腰带等潮流饰品，可加入角色标志性元素（如角色专属符号、元素主题配饰）
- **改造原则**：保留角色标志性发型、发色、瞳色、发饰，其余服装全部替换为街头潮流单品。如角色有标志性外套/披风，可将其转化为街头夹克风格

**男版（男性角色专用）**：

- **上身**：宽松短袖 T 恤（oversized tee）或合身无袖背心（fitted tank top，不露脐） + 敞开的短夹克（cropped jacket / 机车夹克 / 印花衬衫），衬衫/夹克可敞开露出胸口，严禁 crop top / tube top 等露脐单品
- **下身**：束脚工装裤（cargo pants）/ 破洞牛仔裤（ripped jeans）/ 及膝宽松休闲短裤（relaxed-fit shorts），版型必须宽松利落，严禁短裙/紧身短裤
- **体型锚定**：必须写入男性身形描述（如 masculine athletic build, broad shoulders, toned arms），少年体型角色可用 boyish handsome features 替代肌肉描述，但 broad shoulders 等性别锚定词不可省略
- **鞋履**：运动鞋 / 高帮板鞋 / 马丁靴，避免正式皮鞋
- **配饰**：链条项链（可叠戴）/ 戒指 / 手环 / 腰链等潮流饰品，可加入角色标志性元素
- **改造原则**：保留角色标志性发型、发色、瞳色、发饰，其余服装全部替换为街头潮流单品。如角色有标志性外套/披风，可将其转化为街头夹克或衬衫风格

**涂鸦墙公式**：

- **色彩方案**：涂鸦墙的主色调必须与角色的主题色/元素色/阵营色**高度匹配**（如火角色→红橙暖色调涂鸦、冰角色→蓝紫冷色调涂鸦、草角色→绿黄自然色调涂鸦）
- **内容元素**：墙上必须包含以下至少两类涂鸦元素：
  - 角色名或角色外号的艺术字体涂鸦
  - 角色元素符号（如火焰/水滴/闪电/风旋等）
  - 角色主题相关图案（如角色武器剪影、标志性物品、阵营徽章）
  - 街头风格的抽象几何图形、喷漆滴落效果、涂鸦签名
- **质感要求**：多层喷漆叠加效果、墙面剥落的真实质感、霓虹光反射、喷漆罐摆放在画面一角作为道具

**表情与姿态公式**：

- **核心情绪**：cold, disdainful, dismissive, aloof, superior — 女版像一位居高临下的女王在审视闯入她领地的人，男版像一位执掌棋局的年轻帝王在审视送上门的对手
- **眼神方向**：直接注视镜头，眼神锐利、冷漠、带有审视感
- **肢体语言**：放松但充满掌控感，身体微微后仰或侧倚，一只手随意支撑或拿着小道具，另一只手自然垂放或搭在膝上。男版坐姿推荐单膝立起、小臂搭膝，或手臂展开撑靠，避免以展示腿部曲线为目的的姿态语言
- **面部细节**：嘴角微不可察的弧度，不是微笑而是轻蔑；瞳孔收缩锐利；眉毛自然不皱但带有距离感
- **禁止项**：温暖的笑容（warm smile, gentle smile, cheerful）、唱歌张嘴（singing, open mouth singing）、惊讶表情、可爱表情、温柔表情

**完整 prompt 模板（女版，女性角色专用，配 `needful1-woman.png`）**：

```
Refer to the attached reference image (Figure 1). Generate a similar style image of {角色英文名} from {游戏英文名} sitting casually in front of a bold graffiti wall. {角色名} is seated in a relaxed but confident posture, {具体坐姿描述如"leaning back against the graffiti wall with one knee raised, her other leg bent with her foot flat on the ground"}, with her body language calm, controlled, and slightly provocative. Her expression should show cold, disdainful eyes, aloof, sharp, and superior, as if she is silently judging the viewer.

Keep {角色名}'s recognizable features: {保留角色标志性外貌特征列表}. Blend her canonical design with a modern edgy streetwear aesthetic: {上身服装描述 — 无袖露脐+短夹克}, {下身服装描述 — 短裙或短牛仔裤}, {腿部描述 — 光腿或丝袜}, {鞋履描述}, {潮流配饰描述}. Preserve her identity while giving her a fresh urban street-style look.

The graffiti wall behind her should be vivid and layered, full of expressive abstract shapes and energetic street-art textures in {角色主题色} tones, with graffiti elements including {角色名涂鸦字体}, {元素符号涂鸦}, {主题图案涂鸦}, creating a rebellious urban backdrop that resonates with her character theme. Add subtle {角色元素名} energy effects, {角色主题特效}, and {角色标志性小道具} around her to reinforce her identity.

Use a wide cinematic framing suitable for a 16:9 wallpaper, with {角色名} as the main focal point while still showing enough of the graffiti wall and surrounding environment for atmosphere. The mood should feel cool, stylish, intimidating, and mysterious. Highly detailed background, rich shadows, {角色主题色} glowing highlights, sharp focus on {角色名}, and a refined high-end anime illustration look.
```

**完整 prompt 模板（男版，男性角色专用，配 `needful1-man.png`）**：

```
Refer to the attached reference image (Figure 1) for composition, graffiti-wall style, and overall atmosphere only. Generate an image of {角色英文名}, a young man from {游戏英文名}, sitting casually in front of a bold graffiti wall. {角色名} is male — do not render him with feminine features or attire. {角色名} is seated in a relaxed but dominant posture, {具体坐姿描述如"one knee raised with his forearm resting on it, his other leg bent with his foot flat on the ground"}, with his body language calm, controlled, and quietly provocative. His expression should show cold, disdainful eyes, aloof, sharp, and superior, as if he is silently judging the viewer.

Keep {角色名}'s recognizable features: {保留角色标志性外貌特征列表}. He has a masculine youthful build with broad shoulders. Blend his canonical design with a modern edgy streetwear aesthetic: {上身服装描述 — 宽松T恤/背心+敞开夹克或印花衬衫}, {下身服装描述 — 工装裤/破洞牛仔裤/宽松短裤}, {鞋履描述}, {潮流配饰描述}. Preserve his identity while giving him a fresh urban street-style look.

The graffiti wall behind him should be vivid and layered, full of expressive abstract shapes and energetic street-art textures in {角色主题色} tones, with graffiti elements including {角色名涂鸦字体}, {元素符号涂鸦}, {主题图案涂鸦}, creating a rebellious urban backdrop that resonates with his character theme. Add subtle {角色元素名} energy effects, {角色主题特效}, and {角色标志性小道具} around him to reinforce his identity.

Use a wide cinematic framing suitable for a 16:9 wallpaper, with {角色名} as the main focal point while still showing enough of the graffiti wall and surrounding environment for atmosphere. The mood should feel cool, stylish, intimidating, and mysterious. Highly detailed background, rich shadows, {角色主题色} glowing highlights, sharp focus on {角色名}, and a refined high-end anime illustration look.
```

**负面提示词追加项**（在常规 negative prompt 基础上**必须额外追加**以下内容，按性别二选一）：

女版追加：

`standing, standing pose, upright posture, singing, open mouth singing, warm smile, gentle smile, cheerful expression, cute expression, adorable, sweet, innocent, game canonical outfit, official costume, fantasy dress, medieval clothing, armor, full gown, formal dress, beach background, ocean background, nature background, indoor background, plain background, minimal background, missing graffiti wall, low detail graffiti, generic graffiti, wrong graffiti colors, wrong streetwear, missing crop top, missing jacket, missing shorts, missing skirt, long dress, full pants, business suit, school uniform`

男版追加：

`standing, standing pose, upright posture, singing, open mouth singing, warm smile, gentle smile, cheerful expression, cute expression, adorable, sweet, innocent, game canonical outfit, official costume, fantasy dress, medieval clothing, armor, full gown, formal dress, beach background, ocean background, nature background, indoor background, plain background, minimal background, missing graffiti wall, low detail graffiti, generic graffiti, wrong graffiti colors, wrong streetwear, missing jacket, long dress, business suit, school uniform, feminine, androgynous, female body, curvy figure, skirt, crop top, tube top, fishnet, thigh strap, makeup, lipstick, slender feminine figure`

## 必需2 — 角色特写肖像 (Close-up Portrait)

每个类型 A 角色单人壁纸合集**必须包含一组两条**特写肖像 prompt（16:9 横版 + 9:20 手机竖屏版，两条共用同一套五步公式设定）。这类壁纸的核心价值在于：用一个极简画面承载角色最深的叙事内核——不是展示角色"在做什么"，而是揭示角色"是什么"。

**参考图**：`needful2.png`（阿蕾奇诺手持玫瑰半遮面特写肖像，全局共享，位于本 skill `references/` 目录）

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

**手机竖屏变体（必须同步产出，与 16:9 横版成对）**：

特写肖像除 16:9 横版外，必须额外生成一条 9:20 手机竖屏壁纸版，要求：

- 构图收紧为**胸部及以上（chest-up）或半身（waist-up）**，人物面部为画面焦点，不出现全身
- 比例标注用 `9:20 vertical mobile wallpaper`
- 五步公式（道具选择、道具半遮眼、矛盾表情、叙事性总结句、单光源 + 纯黑背景）与 16:9 横版**完全一致**，仅调整取景范围
- negative prompt 在横版基础上保留 `full body shot, wide shot` 并追加 `lower body, legs, feet` 排除下半身

## 动漫性感风 — 2D 日漫简约背景系列

每个类型 A 角色单人壁纸合集**固定包含 4 条**动漫性感风 prompts。这类壁纸的核心是：**人物绘制为 2D 日漫风格、着装为性感妩媚向（服装三型），背景为简约朴素的日漫场景**——有场景感但线条简单、元素少不堆叠，同一角色同一画风形成一套四比例壁纸系列，覆盖手机、电脑、平板、阔折叠屏四种设备。

**四张固定比例（不可增减、不可替换）**：

| 张数 | 用途 | 画面比例标注 |
|------|------|-------------|
| 1 | 手机壁纸 | `9:20 vertical mobile wallpaper` |
| 2 | 电脑壁纸 | `16:9 desktop wallpaper` |
| 3 | iPad 壁纸 | `4:3 tablet wallpaper` |
| 4 | 阔折叠手机（展开态） | `√2:1 (1.414:1) foldable phone unfolded wallpaper` |

**画风与风格核心约束（必须全部满足）**：

1. **2D 日漫风人物**：positive prompt 必含 `2D Japanese anime style, flat cel shading, clean thin lineart, soft anime coloring, Japanese anime aesthetic`；人物绘制走扁平赛璐璐、细线条、柔和上色的路线，不走 3D 渲染、半写实、厚涂路线
2. **性感妩媚服装三型**（按角色气质选一，四条共用同一套服装）：泳装系（比基尼式连体/分体+透纱罩衫）、JK 系（短款衬衫+领结+百褶裙）、活力系（露脐短上衣/吊带+短裙/短裤）；男性角色做性别化处理（敞开花衬衫+沙滩裤等），不强制泳装
3. **尺度红线（写死，不可放宽）**：仅限成年角色；姿态优雅不露点；positive 统一含 `tasteful and elegant throughout, no explicit content`；negative 统一追加 `nude, topless, nipples, areola, explicit, childlike, loli, underage`
4. **简约朴素场景背景**：positive prompt 必含 `simple anime scenery background, clean minimal scene composition, Ghibli-inspired soft background, flat background with simple shapes and soft colors`——背景为单一简单场景（如一片天空与云、一片草地、远山与水面、星空），线条简单、透视平缓、元素少不堆叠；不出现复杂建筑群、多场景叠加、道具堆砌，也不出现武器交战与打斗场面；背景主色与角色主题色呼应（如冰角色→淡蓝白、火角色→米橙）
5. **构图随比例调整**：9:20 竖版用半身或全身居中构图；16:9 横版让人物站于画面一侧留白呼吸感；4:3 用居中半身；√2:1 用横向极简留白构图
6. **系列一致性**：四条 prompt 共用同一套人物外貌/服装描述、同一背景场景及配色方案，仅微调姿势、构图与背景元素的疏密/色调深浅形成系列变化，画风、配色、简约度必须统一

**Prompt 要点**：

- 人物姿势简单干净且复用安全姿势写法：站立（`standing with hands relaxed at sides`、`weight on one hip, natural stance`）或坐姿按主 SKILL.md「腿部/坐姿质量优化」的安全写法（侧坐双腿同侧/正坐双膝并拢），禁用跷二郎腿与单脚钩栏杆；姿态妩媚自然
- 表情随系列微调（平静/淡笑/回眸/闭眼），气质统一为妩媚自信或温柔慵懒
- 光影简洁柔和：`soft even lighting, gentle rim light in {角色主题色}`，场景背景光与人物光统一，避免复杂戏剧光
- 保留手部与腿部规范：手部可见时写明五指，negative 保持通用手部穷举 + 腿部穷举

**负面提示词追加项**（在通用手部/腿部穷举与画质排除基础上**必须额外追加**）：

`3D render, semi-realistic, realistic, painterly, thick oil paint, game 3D model, complex background, cluttered background, multiple overlapping scenes, busy props, heavy details, photorealistic background, weapon combat, fighting, blood, gore, nude, topless, nipples, areola, explicit, childlike, loli, underage`

## 跨领域参考图

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
