# 鹤悠悠 · 黄鹤楼数字漫游

黄鹤楼主题的纯前端交互网站：品牌首页 + 基于 Three.js 的 3D 数字漫游。

无需任何构建工具、无需后端，直接上传本目录即可在 GitHub Pages 上运行。

## 页面

| 文件 | 说明 |
| --- | --- |
| `index.html` | 品牌首页：夜空首屏（实景楼体抠像 + Canvas 流星雨）、名楼档案、建筑形制、海报展廊、文创市集、千古诗篇 |
| `roam.html` | 3D 数字漫游：程序化建模的五层飞檐黄鹤楼，支持环绕查看、沉浸漫游、俯瞰全景、昼夜切换、流星雨、截图导出 |

## 亮点实现

- **首屏流星雨**：Canvas 手绘的锥形光尾（头部最亮最粗、尾端渐细渐淡），分层柔光 + 白色热芯，绘制于楼体与文字之下，被楼体正常遮挡。
- **3D 黄鹤楼**：使用 Three.js 程序化建模飞檐、斗拱、金瓦、台基，支持真实照片纹理，纹理缺失时自动回退到程序化材质。
- **分解楼体**：漫游页点「分解楼体」，楼体逐层向上拉开并标注楼层，可查看各层文创与字画。
- **入楼观展**：点「入楼观展」自动分解楼体并飞入层内，正对后壁「厅名匾额 + 主挂轴 + 一对楹联」，两侧为山水画屏与文创展案，头顶六角宫灯与藻井、地面团花地毯随层不同；逐层切换（共五层），Esc 一键退出回全景。
- **3D 流星雨**：按相机视野在远处天空带横掠，出画即回收，按目标数量维持密度。
- **点击换图**：点击页面任意照片即可选择本地图片即时替换预览；要永久替换，把新图按同名覆盖 `assets/` 下对应文件即可。

## 本地预览

`index.html` 引用了本地图片与纹理，必须通过 HTTP 服务访问，直接双击打开会因浏览器安全策略导致部分资源无法加载。

```bash
python -m http.server 8000
```

然后访问 <http://localhost:8000/index.html>。

## 部署到 GitHub Pages

1. 在 GitHub 新建仓库（不要勾选自动生成 README，避免覆盖本文件）。
2. 将本目录内所有文件上传到仓库根目录（网页上传或 `git push` 均可）。
3. 打开仓库 `Settings` → `Pages` → `Source` 选择 `Deploy from a branch`，分支选 `main`、目录选 `/ (root)`，保存。
4. 等待约 1 分钟后访问 `https://<你的用户名>.github.io/<仓库名>/`。

命令行方式：

```bash
git init
git add .
git commit -m "feat: 鹤悠悠 · 黄鹤楼数字漫游"
git branch -M main
git remote add origin https://github.com/<你的用户名>/<仓库名>.git
git push -u origin main
```

## 文件清单（共 32 个，约 7.35 MB）

```
index.html                     首页
roam.html                      3D 漫游页
README.md                      本说明
lib/
  three.min.js                 Three.js 运行库
  OrbitControls.js             相机环绕控制
assets/
  opt/hhl_tower.webp           楼体实景抠像（首屏 / 名楼档案）
  opt/ip_huanghe_opt.webp      IP 形象「鹤悠悠」
  posters/p1~p6.jpg            海报展廊（6 张）
  market/m1~m8.jpg             文创市集商品图（8 张）
textures/
  huanghe_roof.jpg             黄鹤楼屋面纹理
  tex_redwall.jpg              红墙纹理
  tex_stone.jpg                石材纹理
  tex_tile_yellow.jpg          金瓦纹理
  tex_wood.jpg                 木构纹理
  tex_woodwall.jpg             木墙纹理
  ip_huanghe.png               3D 场景内的 IP 立牌
  model_shots/
    tower_aerial_clay.jpg      建筑形制 · 模型鸟瞰
    tower_front_clay.jpg       建筑形制 · 正立面
    dougong_eave_clay.jpg      建筑形制 · 斗拱飞檐
    finial_roof_clay.jpg       建筑形制 · 葫芦宝顶
```

## 未包含的内容（按需自行补充）

以下为设计素材，页面运行不需要，因此未打包：

- `stickers/` 微信表情包 GIF 与预览图
- `形象/` IP 形象原始设计图
- `textures/hhl_tower.png`、`hhl_tower_src.jpg`、`hhl_photo.jpg`、`ip_huanghe_opt.png`（原图 / 中间产物，网页已用压缩后的 webp）
- `textures/model_shots/` 其余 8 张场景渲染图

如需上架更多海报与文创图，按下述命名放置即可自动显示：

- 海报：`assets/posters/p1.jpg` …（3:4 竖版）
- 文创：`assets/market/m1.jpg` …（1:1 方图，需同时在 `index.html` 中放开对应注释）

## 已知事项

- `index.html` 页脚有指向 `../huanghehou/index.html` 的相对链接，属于另一个「四大名楼」项目。单独部署本仓库时该链接会 404，如需可删除或改为站内链接。
- `roam.html` 会尝试加载 `tex_tile_green.jpg`、`tengwang_roof.jpg`、`yueyang_roof.jpg`（其他名楼预留纹理），文件缺失时自动回退程序化材质，控制台可能出现相关 404，属于预期行为，不影响使用。
- 全站纯静态、无第三方接口调用，部署后无需任何配置。
