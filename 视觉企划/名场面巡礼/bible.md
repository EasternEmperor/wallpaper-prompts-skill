# 名场面巡礼 · 定位圣经

## 母定位宣言

把米游角色放进知名动漫的经典名场面构图——每一期都是一次「角色 × 名场面」的化学反应，粉丝猜的是"下一个角色会走进哪个场面"。prompt 中**不写原作名**，用构图描述还原名场面（规避生成器版权词拦截）；每条选题必须溯源到来源动漫与集数。

## 风格 DNA 固定块（positive，逐字复用，禁止改动）

```
masterpiece anime-style illustration, iconic anime scene recreation, clean simple background, minimalist uncluttered composition, soft cinematic lighting, vivid film-like color grading, highly detailed, 3:4 vertical portrait wallpaper
```

## 定位专属负面块（逐字复用）

```
cluttered background, busy background, overly detailed background, stacked overlapping elements, excessive glowing particles, excessive bokeh, light clutter, messy composition, 3d render, photorealistic, western cartoon
```

## 名场面溯源规则（本系列专属）

1. **来源登记（锚定真实名场面）**：每条选题必须锚定一部真实作品的知名名场面（场景可考据、观众能识别），登记作品名与集数。TV 版尽量定位到「第 N 话」；反复出现的固定舞台场景可记「TV·××场景」；剧场版/电影记「剧场版」。**禁止「通用构图」档位**——不得登记无具体出处的泛化构图（2026-10-07 起废止，存量选题已全部回改替换为真实名场面）。
2. **双源验证**：新增选题时需两类来源交叉验证：①知名度来源（投票/榜单/名场面盘点，如 NHK 全日本アニメ件名投票、goo ランキング、Bangumi、萌娘百科）；②结构化来源（确认集数归属，如 Wikipedia 作品条目、官方站点、豆瓣剧集分集页）。两源齐全方可入矩阵。
3. **仅文本溯源，不下载名场面图**：溯源仅保留文本登记（来源动漫 + 集数），**不搜索、不下载名场面剧照/截图**。出图构图/光线/色调完全由 prompt 构图描述还原，**不得虚构可考据的画面细节**（如实地元素可查证时尽量准确）。
4. **角色参考图作用域**：角色外观由角色官方参考图锁定：`Referring to the attached artwork for character appearance only — do not copy the outfit, pose, or composition of the reference`。

## Prompts 撰写规则（人体结构约束，逐字复用）

1. **Positive 人体锚点块**：手部可见时必须插入，位置在风格 DNA 块之后、角色锚点之前：

```text
perfect hands, five fingers on each hand, anatomically correct hands, well-defined fingers, natural hand pose, clean finger separation
```

   高危手部姿势（扶栏、抬手接物、伸手等）额外追加 `fingers elegantly relaxed`。
2. **Negative 人体穷举块**：逐字追加在「定位专属负面块」之后（手部 24 项 + 腿部 17 项 + 全局项）：

```text
bad hands, extra fingers, fewer fingers, missing fingers, fused fingers, webbed fingers, merged fingers, overlapping fingers, deformed fingers, mutated fingers, six fingers, four fingers, three fingers, more than five fingers, less than five fingers, disfigured hands, poorly drawn hands, bad hand anatomy, asymmetrical hands, broken fingers, claw hands, blurry hands, indistinct fingers, smeared hands, missing legs, missing feet, missing calves, cropped legs, legs out of frame, twisted legs, rotated hips, dislocated hip, extra legs, third leg, fused legs, malformed knees, knees bending in opposite directions, unnatural sitting pose, disproportionate limbs, elongated calves, deformed feet, extra limbs, disfigured, mutation, wrong hair color, wrong eye color, incorrect character
```

3. **自检计数**（每份 prompts 文件产出后执行，N=该文件 prompt 条数）：`fused fingers` = N、`malformed knees` = N、`perfect hands` = N、`extra limbs` = N、`3:4 vertical portrait wallpaper` = N；负面块中不得出现 nude/nsfw/loli/underage/topless/nipples/areola/suggestive 等审查敏感词；占位符 = 0。

## 选题矩阵

| 编号 | 角色 | 子场景（名场面构图） | 来源动漫 | 集数 | 状态 |
|------|------|---------------------|----------|------|------|

| 001 | 流萤 | 海上列车黄昏车窗·海风与帽檐 | 千与千寻 | 剧场版 | 已做·第1期 |
| 002 | 流萤 | 黄昏石阶坡道·回望与彗星 | 你的名字。 | 剧场版 | 已做·第1期（致敬式合成构图） |
| 003 | 流萤 | 夏日海边铁道口·电车掠过 | 灌篮高手 | TV·OP（镰仓高校前道口） | 已做·第1期 |
| 004 | 三月七 | 雪国站台·晨雾等车 | 秒速五厘米 | 剧场版·第2话《宇航员》 | 已做·第2期 |
| 005 | 三月七 | 樱花道口·列车驶过瞬间 | 秒速五厘米 | 剧场版·第1话《樱花抄》 | 未做 |
| 006 | 宵宫 | 夏日祭面具摊·纸灯一盏 | 未闻花名 | TV（夏祭场景） | 未做 |
| 007 | 宵宫 | 千本鸟居·朱红回廊尽头回眸 | 稻荷恋之歌 | TV（鸟居回廊场景） | 已做·第4期 |
| 008 | 芙宁娜 | 异色商船甲板·海坊主之海 | 怪化猫（モノノ怪） | TV·第3〜5话「海坊主」 | 已做·第3期 |
| 009 | 甘雨 | 雨后石阶·纸伞与青苔 | 言叶之庭 | 剧场版 | 已做·第5期 |
| 010 | 胡桃 | 秘密庭园·花开小径 | 借物少女艾莉缇 | 剧场版（庭园场景） | 未做 |
| 011 | 神里绫华 | 山顶神社·云海黄昏鸟居 | 你的名字。 | 剧场版（宮水神社） | 已做·第4期 |
| 012 | 雷电将军 | 神社黄昏·灯笼次第亮起 | 夏目友人帐 | TV（神社与灯影场景） | 已做·第4期 |
| 013 | 花火 | 夏夜桥上烟花·单发盛放 | 声之形 | 剧场版 | 未做 |
| 014 | 黄泉 | 星之夜站台·银河列车 | 银河铁道之夜 | 剧场版（1985） | 已做·第2期 |
| 015 | 知更鸟 | 老式唱片店橱窗·黄昏街角 | 坂道上的阿波罗 | TV·待查 | 未做 |
| 016 | 耀嘉音 | 天台黄昏·天线与晚霞 | 新世纪福音战士 | TV·多话（天台场景） | 未做 |
| 017 | 艾莲 | 图书馆窗边·阳光尘埃浮游 | 冰菓 | TV（图书室篇章） | 未做 |
| 018 | 星见雅 | 无人车站·晨雾之门 | 铃芽之旅 | 剧场版（废駅关门场景） | 已做·第2期 |
| 019 | 妮露 | 海边防波堤·水平线与裙摆 | 来自风平浪静的明天 | TV（海面与防波堤场景） | 已做·第3期 |
| 020 | 千织 | 温泉街橱窗·午后光 | 花开伊吕波 | TV（汤乃鹭温泉街场景） | 未做 |
| 021 | 镜流 | 雪之踏切·雪如樱吹雪 | 秒速五厘米 | 剧场版·第1话《樱花抄》结尾 | 未做 |
| 022 | 爱可菲 | 嵐夜海崖之家·浪与灯火 | 崖上的波妞 | 剧场版（崖上小屋场景） | 已做·第3期 |
| 023 | 玛薇卡 | 向日葵花田·蓝天积云 | CLANNAD After Story | TV（向日葵花田场景） | 已做·第5期 |
| 024 | 钟离 | 御神木古森·树影斑驳 | 犬夜叉 | TV·第1话（御神木场景） | 已做·第5期 |
| 025 | 刻晴 | 电车内黄昏·窗外流光 | 秒速五厘米 | 剧场版（东京电车段落） | 未做 |
| 026 | 神里绫人 | 川桥夕阳·金波一川 | 未闻花名 | TV（塔见川铁桥场景） | 未做 |
| 027 | 符玄 | 星空山丘·银河倾泻 | 放学后失眠的你 | TV（星空观测场景） | 未做 |
| 028 | 停云 | 上元天灯·万灯升空 | 天官赐福 | 动漫（上元祭天灯场景） | 未做 |
| 029 | 银狼 | 深夜便利店·冷柜微光 | 彻夜之歌 | TV（深夜便利店场景） | 未做 |
| 030 | 娜维娅 | 花田小径·单车与下坡 | 龙猫 | 剧场版（乡间路段落） | 未做 |

## 已产出登记表

| 期数 | 日期 | 模式 | 选题编号 | 产出路径 |
|------|------|------|----------|----------|
| 1 | 2026-10-01 | 模式一（流萤×3） | 001-003 | prompts.md |
| 2 | 2026-10-04 | 模式二（三月七/黄泉/星见雅·月台三连） | 004/014/018 | prompts-ep02.md |
| 3 | 2026-10-07 | 模式二（妮露/芙宁娜/爱可菲·海岸三连） | 008/019/022 | prompts-ep03.md |
| 4 | 2026-10-07 | 模式二（宵宫/雷电将军/神里绫华·神社三连） | 007/011/012 | prompts-ep04.md |
| 5 | 2026-10-08 | 模式二（甘雨/钟离/玛薇卡·秋日自然三连） | 009/024/023 | prompts-ep05.md |

## 禁入清单

- 高密度元素场景（大战场、人群密集、满屏特效）——违反背景简洁强制条款
- 直接写原作名/角色名于 prompt（用构图描述替代）
- **来源动漫/集数两列为空、或未按溯源规则完成登记的选题，不得进入制作**
- **「通用构图」类选题（已废止档位）不得再进入矩阵**
