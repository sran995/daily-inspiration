# Daily Inspiration — 专注当下

每天一幅世界名画 + 三语励志语录的单页网站。

## 项目结构
- `index.html` — 全部代码（CSS + JS 内联），705 行 → 扩到 1000+ 行（46 幅画数据）
- `SPEC.md` — 完整 SPEC 文档
- 纯静态，无依赖，GitHub Pages 部署

## 线上
- https://sran995.github.io/daily-inspiration/
- 仓库：github.com/sran995/daily-inspiration

## 如何修改

### 改画作数据
打开 `index.html`，搜索 `PAINTINGS_DATA`。数据结构：
- 9 个 key：renaissance, baroque, romanticism, impressionism, postimpressionism, ukiyoe, symbolism, surrealism, chinese
- 每幅画有 title, titleCn, artist, artistCn, year, size, location, url, desc, 以及 7 维分析字段
- 西方画用 comp/light/color/detail/bg/why
- 中国画用 school/technique/brush/placement/rhythm/poetry/why
- 维度标签在 `loadPainting` 函数中根据 `dimsType` 自动切换

### 改轮换逻辑
起始日期 `START_DATE` 在 LOGIC 区。`ALL_PAINTINGS` 是扁平数组。`getDailyPainting()` 根据日期差取模。

### 改样式
- CSS 变量在 `:root`（亮色）和 `@media(prefers-color-scheme:dark)`（暗色）
- 桌面布局在 `@media(min-width:769px)` 的 `.main` grid
- 手机布局在 `@media(max-width:768px)`，注意 `.right` 有显式高度防溢出

### 增加新画作
1. 找到对应单元 key
2. 按字段模板新增对象
3. Wikimedia Commons 图片用 `?width=1280` 缩略图 URL
4. `grep -c titleCn: index.html` 确认总数

### 部署
```bash
cd /Users/shina_527/daily-inspiration
git add index.html && git commit -m "描述改动" && git push
```
推送后 GitHub Pages 自动部署，数十秒生效。

## 已知问题 / 注意
- 手机端 `.right` 画布高度用 `height:60vw;max-height:55vh;overflow:hidden` 防止图片溢出
- Lightbox 放大镜后台加载全分辨率原图（去掉 ?width=1280）
- `?day=N` 可预览指定天数画作，`?unit=N` 跳转单元
- git 提交用 `sran995@users.noreply.github.com` 隐私邮箱
- SSH key 在 `~/.ssh/id_ed25519_github`
