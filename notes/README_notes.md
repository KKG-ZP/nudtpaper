# Notes Subsystem

本目录是独立于学位论文主线的科研论文阅读笔记子系统，用于把单篇精读、文献梳理和后续开题素材沉淀在同一套 LaTeX 结构中。

## 目录说明

```text
notes/
├── README_notes.md              # 本说明文档
├── Makefile                     # 简单编译入口
├── indexes/
│   └── reading_index.tex        # 手工维护的已读论文总索引
├── templates/
│   ├── preamble.tex             # 共享导言区与常用版式配置
│   └── paper_note_template.tex  # 新建单篇论文笔记时复制的模板
├── papers/
│   ├── sample_note.tex          # 完整示例：DeepSeek-R1 论文笔记
│   └── sample_deepseekmath_note.tex # 第二个示例：DeepSeekMath 论文笔记
├── bib/
│   └── references.bib           # 论文笔记共享 Bib 数据库
├── figures/
│   └── README.md                # 插图命名与放置约定
└── output/                      # 编译产物目录
```

## 如何复制模板新建笔记

推荐流程：

1. 进入 `notes/` 目录。
2. 复制 [`templates/paper_note_template.tex`](./nudtpaper/notes/templates/paper_note_template.tex) 到 `papers/`，文件名建议使用 `年份-作者缩写-主题.tex` 或 `paperkey_note.tex`。
3. 打开新文件后，优先修改文首的元信息字段：
   - `\papertitle`
   - `\paperauthors`
   - `\papervenue`
   - `\paperyear`
   - `\paperdoi`
   - `\paperurl`
   - `\readingdate`
   - `\paperonesentence`
   - `\paperkeywords`
4. 将正文中示例性的 `\cite{...}` 替换为你自己的 Bib key。

如果希望保留统一目录结构，单篇笔记建议只放在 `papers/`，图片统一放在 `figures/`。

## 如何维护阅读总索引

总索引文件是 [`indexes/reading_index.tex`](./nudtpaper/notes/indexes/reading_index.tex)。

维护原则：

- 索引只保留“快速回看最需要的信息”，不重复正文细节。
- 每新增一篇笔记，都在 `reading_index.tex` 中手工追加一条 `\paperentry{...}{...}{...}{...}{...}{...}`。
- 第 1 个参数建议填写标题；如果想在标题后附引文，直接写成 `标题~\cite{bibkey}`。
- 第 6 个参数填写对应笔记文件路径，推荐使用相对于 `indexes/` 的路径，例如 `../papers/sample_note.tex`。
- `run:` 链接在部分 PDF 查看器中可能被禁用，因此路径文本本身也应保持清晰可读。

推荐流程：

1. 在 `papers/` 中新建笔记文件。
2. 补全笔记头部元信息，尤其是 `\paperonesentence`。
3. 在 `indexes/reading_index.tex` 里复制一条 `\paperentry` 并改成对应信息。
4. 运行 `make index` 编译索引。

## 如何维护 `references.bib`

`notes/bib/references.bib` 是笔记系统的共享文献库，建议遵守以下约定：

- 一个条目对应一个稳定的 Bib key，例如 `deepseekai2025r1`。
- 优先补全 `author`、`title`、`year`、`journal`/`booktitle`、`volume`、`number`、`pages`、`doi`、`url`。
- 中文文献请直接使用中文作者、题名、刊名，并补 `langid = {chinese}`。
- 英文文献保持标准 BibTeX 英文字段写法。
- 若你未来想把多篇笔记汇总成综述或开题文档，尽量不要为同一篇论文重复造不同 key。

## 如何编译

编译前请确认本机 TeX Live 环境至少提供以下命令或对应组件：

- `xelatex`
- `biber`
- `latexmk`
- `ctex`
- `biblatex`
- `biblatex-gb7714-2015`

### 方式 1：推荐，使用 `latexmk`

在 `notes/` 目录下执行：

```bash
make sample
```

或编译任意单篇笔记：

```bash
make note FILE=papers/sample_note.tex
```

编译总索引：

```bash
make index
```

产物会输出到 `notes/output/`。

### 方式 2：手工编译链

若不使用 `latexmk`，可在 `notes/papers/` 目录执行：

```bash
xelatex -output-directory=../output sample_note.tex
biber ../output/sample_note
xelatex -output-directory=../output sample_note.tex
xelatex -output-directory=../output sample_note.tex
```

之所以采用这条链路，是因为当前模板使用 `biblatex` + `biber` 实现 GB/T 7714—2015。

对于阅读总索引，手工流程改为：

```bash
cd notes
xelatex -output-directory=output indexes/reading_index.tex
biber output/reading_index
xelatex -output-directory=output indexes/reading_index.tex
xelatex -output-directory=output indexes/reading_index.tex
```

## 如何把单篇笔记沉淀成开题报告材料

建议把每篇笔记中的以下内容当作“可迁移资产”来维护：

- `快速浏览` 中的研究问题与核心贡献，可直接转化为“相关工作定位”。
- `Method` 中的差异点与公式，可提炼为“现有方法分析”和“技术路线对比”。
- `Reflection` 中的局限与启发，可直接沉淀为“待解决问题”和“研究切入点”。
- `Reuse for Proposal` 章节建议写成接近正式文风的草稿，后续可以直接改写并迁移到 `proposal/`。

一个实用做法是：每篇笔记至少留下 3 段可复用文字。

- 一段背景动机
- 一段方法描述
- 一段与你课题关联的论证

这样后续写开题时，不需要重新从零组织语言。

## 后续如何扩展成综述文档

当积累到多篇笔记后，可以在 `notes/` 下继续扩展，例如增加：

- `review/outline.tex`：综述或阶段性汇总主文档
- `review/sections/`：按主题拆分章节
- `review/figures/`：综述专用图表

扩展原则：

- 继续复用 [`templates/preamble.tex`](./nudtpaper/notes/templates/preamble.tex)
- 继续复用 `bib/references.bib`
- 单篇笔记保持独立，不和综述正文混写

这样可以把“单篇精读”平滑升级成“主题综述”或“开题文献综述”。
