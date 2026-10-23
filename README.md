# article-cheatsheet

将论文、综述和技术文章整理成中文速览与可打印的 PDF 速查表。默认采用 LaTeX 学术讲义风格，提供可编辑源文件，适合阅读、讨论和后续迭代。

## 内容与排版

- 按 **challenge → 核心洞察 → 对应方案 → 机制与证据** 组织内容，按论文类型调整，不机械缩写每一章。
- 首页保留完整标题、作者、主要机构、论文来源与发表状态，并用相关作品说明作者群的研究积累。
- 保持 A4 横向、宋体与英文衬线字体、细线和克制用色等视觉规范，页眉标题相对整页居中；每篇 paper 根据内容重新选择页数、栏数、图文比例和分页。
- 图表本体使用论文原文截图；图外 caption 使用中文，保留 memory、agent、LLM、模型名和必要术语。
- 区分作者结论、整理者解释与待讨论问题；关键数字保留比较条件和原文定位。

工作顺序是：**梳理内容主线 → 根据内容设计布局 → 逐页渲染与调整**。字体、页眉、标题框等局部组件可以复用；关键图表、贡献重点与解释难度决定每篇文章的具体版面。

## 示例：PerMemSafe

**示例仅供参考风格与复用局部组件，每篇 paper 都需要根据内容重新排版。** 不必沿用示例的四页结构、栏宽或模块位置。

下面是使用本 skill 生成并经多轮阅读讨论、排版调整的四页速查表（讨论稿 v3）。首页突出 challenge、核心洞察和对应方案；后续依次解释方法与消融、评测设计、结果与讨论问题。

[查看 / 下载完整 PDF](examples/permemsafe/PerMemSafe-cheatsheet.pdf) · [可编辑 LaTeX 源文件](examples/permemsafe/source/) · [论文原文与作者信息](https://aclanthology.org/2026.findings-acl.320/)

[![PerMemSafe 速查表首页：challenge、核心洞察与对应方案](examples/permemsafe/page-1.png)](examples/permemsafe/PerMemSafe-cheatsheet.pdf)

<details>
<summary>展开其余三页预览</summary>

### 方法机制与组件消融

![第 2 页：SentinelMem 的 RIE、PUP、FSMM 与组件消融](examples/permemsafe/page-2.png)

### 评测设计与基准结果

![第 3 页：PerMemSafe 数据构造、任务、指标与基准结果](examples/permemsafe/page-3.png)

### 结果解读与讨论问题

![第 4 页：总体表现、证据边界与后续讨论](examples/permemsafe/page-4.png)

</details>

示例基于 Hengyu An 等人的 *PerMemSafe: Benchmarking Implicit Personalized Safety of Long-Horizon Self-Evolving Agents*（Findings of ACL 2026）。图表本体截取自论文，中文图注及阅读整理另行编排；原图表归原作者及相应权利人所有。示例中的整理者解释与讨论问题不代表原作者结论，实验结果未独立复现。

### 修改与编译示例

[main.tex](examples/permemsafe/source/main.tex) 包含正文、中文图注和排版，配套原图在同目录的 `images/` 中。修改时保留这个目录结构。

安装含 XeLaTeX 的 TeX Live 或 MacTeX，并确保有 `xeCJK`、`fontspec`、`extarticle`、TikZ 等源文件所用宏包。在仓库根目录执行：

```bash
cd examples/permemsafe/source
xelatex -interaction=nonstopmode -halt-on-error main.tex
xelatex -interaction=nonstopmode -halt-on-error main.tex
```

生成文件为当前目录的 `main.pdf`。默认字体为 **Times New Roman、Songti SC、Heiti SC**。若环境缺少这些字体，先修改 `main.tex` 开头的三个字体设置，例如改为 TeX Live 中可用的字体：

```latex
\setmainfont{TeX Gyre Termes}
\setCJKmainfont{FandolSong-Regular}
\setCJKsansfont{FandolHei-Regular}
```

更换字体或增删内容后，请检查分页、图注和表格是否溢出；页脚中的总页数也需随实际页数更新。仓库中的示例 PDF 和预览图不会随本地编译自动更新。

## 安装到 Codex

将本仓库放入 Codex 的 skills 目录。默认目录下可使用：

```bash
git clone https://github.com/Cream-yj/article-cheatsheet.git "${CODEX_HOME:-$HOME/.codex}/skills/article-cheatsheet"
```

若目标目录已有同名 skill，请先检查已有内容；若它已是本仓库的克隆，可在其中用 `git pull` 更新。

## 使用

在 Codex 中提供论文链接或本地 PDF，例如：

```text
使用 $article-cheatsheet 阅读这篇论文，生成中文 PDF 速查表和可编辑源文件。
突出 challenge、核心洞察和对应方案，图表用原文截图，caption 用中文。
论文：<论文链接或 PDF 路径>
```

这是指导 Codex 阅读、组织与排版的 skill，不是独立运行的 PDF 生成程序。需要可读取的论文材料及可用的 PDF 生成、渲染工具；支持时优先使用 XeLaTeX，字体按运行环境替换。输出仍适合由读者结合自己的理解继续校对和迭代。

## 文件

- [SKILL.md](SKILL.md)：适用范围、阅读方法、内容组织与证据要求。
- [references/print-layout.md](references/print-layout.md)：版式、图表、中文图注和渲染检查规则，以及公开风格参考。
- [agents/openai.yaml](agents/openai.yaml)：Codex 展示信息与默认提示。

- [examples/permemsafe/](examples/permemsafe/)：四页示例 PDF、逐页预览和可编辑 LaTeX 源文件，包含有来源标注的论文图表截图。

仓库包含可复用的 skill、使用说明和公开论文的速查表示例，不包含论文原始 PDF 或私人研究记录。
