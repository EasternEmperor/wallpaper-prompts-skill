# 参考图下载指南

本文档描述各来源的角色立绘/图片下载方式。所有来源均**无防盗链**，可直接 curl 下载。

---

## 优先级排序

1. **B站WIKI**（首选）— 有 API 可批量获取，无防盗链，图片质量高
2. **萌娘百科**（次选）— 图片质量好，需页面解析后去掉缩放参数
3. **原神官网**（官方源）— 官方最高质量，需浏览器渲染后提取
4. **百度百科**（备选）— 图片较小，作为补充来源

---

## 1. B站WIKI（首选）

### 角色页面 URL

| 游戏 | URL 格式 | 示例 |
|------|---------|------|
| 原神 | `https://wiki.biligame.com/ys/{角色名}` | `https://wiki.biligame.com/ys/刻晴` |
| 崩铁 | `https://wiki.biligame.com/sr/{角色名}` | `https://wiki.biligame.com/sr/丹恒` |
| 绝区零 | `https://wiki.biligame.com/zzz/{角色名}` | `https://wiki.biligame.com/zzz/妮可` |

### 常见立绘文件名

- `{角色名}立绘.png` — 正方形大图（通常 2250×2250）
- `{角色名}立绘2.png` — 竖版立绘
- `{角色名}抽卡立绘.png` — 横版抽卡立绘
- `{角色名}-{时装名}-立绘.png` — 时装立绘（绝区零常见）

### 方式 A：MediaWiki API（推荐，可批量获取）

```bash
# 获取特定立绘的直链（需知道文件名）
curl -s "https://wiki.biligame.com/ys/api.php?action=query&titles=File:刻晴立绘.png&prop=imageinfo&iiprop=url&format=json"

# 列出角色所有相关图片（按文件名前缀搜索）
curl -s "https://wiki.biligame.com/ys/api.php?action=query&list=allimages&aifrom=刻晴&ailimit=50&format=json"
```

返回 JSON 中 `url` 字段即为图片直链。URL 格式：`https://patchwiki.biligame.com/images/{game}/{hash1}/{hash2}/{hash}.png`

### 方式 B：页面解析

用浏览器访问角色页面，执行 JS 提取立绘图片 URL：

```javascript
Array.from(document.querySelectorAll('img[alt*="立绘"]'))
  .map(img => ({src: img.src, alt: img.alt, width: img.naturalWidth, height: img.naturalHeight}))
```

### 下载

```bash
# 直接下载，无需任何特殊 header
curl -L -o {角色名}-splash-art.png "{图片URL}"
```

### 注意事项

- 无防盗链，无 Referer 要求
- 图片 CDN：`patchwiki.biligame.com`
- API 返回的 URL 即为原图，无需额外处理

---

## 2. 萌娘百科

### 角色页面 URL

`https://zh.moegirl.org.cn/{角色名}`

示例：`https://zh.moegirl.org.cn/刻晴`

### 常见图片文件名

- `{角色名}.jpg` — 主立绘
- `{角色名}_祈愿立绘.png` — 祈愿/抽卡立绘

### 页面解析

用浏览器访问角色页面，提取图片 URL：

```javascript
// 提取信息框中的立绘
Array.from(document.querySelectorAll('.mw-file-description img'))
  .map(img => img.src)
```

### 关键操作：获取原图

页面中图片 URL 带有缩放/水印参数，**必须去掉**才能获取原图：

```
# 缩略版（带参数）
https://storage.moegirl.org.cn/moegirl/commons/3/34/刻晴.jpg!/fw/280

# 原图（去掉 !/fw/280 及之后所有参数）
https://storage.moegirl.org.cn/moegirl/commons/3/34/刻晴.jpg
```

规则：URL 中 `!/fw/` 及其后面的所有内容都是缩放/水印参数，删掉即可得到原图。

### 下载

```bash
# 下载原图（注意去掉 !/fw/ 等参数）
curl -L -o {角色名}-splash-art.jpg "{原图URL}"
```

### 注意事项

- 无防盗链
- 图片 CDN：`storage.moegirl.org.cn`（又拍云）
- API 已封禁，只能通过页面解析获取 URL
- URL 中的中文需要 URL 编码

---

## 3. 原神官网（官方源）

### 角色页面 URL

`https://ys.mihoyo.com/main/character/{region}?char={index}`

region 列表：`mondstadt`（蒙德）、`liyue`（璃月）、`inazuma`（稻妻）、`sumeru`（须弥）、`fontaine`（枫丹）、`natlan`（纳塔）、`snezhnaya`（至冬）

示例：`https://ys.mihoyo.com/main/character/liyue?char=6`（刻晴）

### 获取方式

官网使用 Swiper 组件动态加载，需用浏览器渲染后提取：

```javascript
// 提取当前展示角色的立绘大图
document.querySelector('.swiper-slide-active img')?.src

// 或提取所有角色图片
Array.from(document.querySelectorAll('img'))
  .filter(img => img.src.includes('webstatic.mihoyo.com') && img.naturalWidth > 500)
  .map(img => ({src: img.src, width: img.naturalWidth}))
```

### 图片 URL 格式

```
https://webstatic.mihoyo.com/upload/contentweb/{date}/{hash}_{id}.png
```

### 下载

```bash
curl -L -o {角色名}-official-art.png "{图片URL}"
```

### 注意事项

- 无防盗链
- 图片 CDN：`webstatic.mihoyo.com`（阿里云 OSS）
- 图片为官方最高质量
- 需要浏览器渲染，不能直接 curl 获取页面 HTML
- 绝区零和崩铁官网结构类似，URL 分别为 `zzz.mihoyo.com` 和 `sr.mihoyo.com`

---

## 4. 百度百科（备选）

### 搜索 URL

`https://baike.baidu.com/search?word={角色名}+{游戏名}`

示例：`https://baike.baidu.com/search?word=刻晴+原神`

### 获取方式

用浏览器访问搜索结果中的词条页面，提取图片 URL：

```javascript
Array.from(document.querySelectorAll('img'))
  .filter(img => img.src.includes('bkimg.cdn.bcebos.com') && img.naturalWidth > 200)
  .map(img => ({src: img.src, width: img.naturalWidth}))
```

### 关键操作：获取原图

图片 URL 带有处理参数，**去掉参数获取原图**：

```
# 缩放版（带参数）
https://bkimg.cdn.bcebos.com/pic/{hash}?x-bce-process=image/format,f_auto/resize,m_lfit,limit_1,h_400

# 原图（去掉 ?x-bce-process 及之后所有参数）
https://bkimg.cdn.bcebos.com/pic/{hash}

# 信息框缩略图（带 -bkimg-process 后缀和 ? 参数）
https://bkimg.cdn.bcebos.com/smart/{hash}-bkimg-process,v_1,rw_1,rh_1,maxl_216?x-bce-process=...

# 信息框原图（去掉 -bkimg-process... 和 ?x-bce-process... 后缀）
https://bkimg.cdn.bcebos.com/smart/{hash}
```

### 下载

```bash
curl -L -o {角色名}-baike-art.jpg "{原图URL}"
```

### 注意事项

- 无防盗链
- 图片 CDN：`bkimg.cdn.bcebos.com`（百度云 BOS）
- 图片通常较小，质量不如 B站WIKI 和萌娘百科
- 词条 ID 需通过搜索获取

---

## 下载流程建议

1. **首选 B站WIKI API**：用 `api.php?action=query&list=allimages&aifrom={角色名}` 批量搜索，从结果中挑选立绘
2. **如果 B站WIKI 没有**：访问萌娘百科角色页，解析页面提取图片 URL，去掉缩放参数
3. **需要官方最高质量**：用浏览器访问官网角色展示页，渲染后提取 `img` 标签
4. **以上都没有**：百度百科搜索，作为最后补充

### 浏览器下载方式

对于需要浏览器渲染的网站，通用流程：

1. `catdesk browser-action '{"action":"navigate","url":"{页面URL}","waitUntil":"networkidle"}'`
2. `catdesk browser-action '{"action":"evaluate","script":"{提取img的JS代码}"}'`
3. 从返回结果中选取目标图片 URL
4. `curl -L -o {文件名} "{图片URL}"`
