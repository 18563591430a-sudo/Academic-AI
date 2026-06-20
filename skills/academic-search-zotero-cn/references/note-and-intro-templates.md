# Note And Introduction Templates

## Zotero Translation Note

Use this child note title:

`中文题名与摘要翻译（Codex）`

Use this note structure:

```text
中文题名与摘要翻译（Codex）

英文题名：<English title>

中文题名：<Chinese title translation>

英文摘要：<English abstract>

中文摘要：<Chinese abstract translation>

摘要来源：<OpenAlex / CrossRef / Semantic Scholar / CNKI / publisher / DOI page / other>

处理说明：由 Codex 于 <date> 添加摘要并翻译。
```

Translation guidance:

- Translate titles in natural academic Chinese, not word-for-word.
- Preserve technical terms such as landslide, debris flow, hazard chain, cascading hazards, InSAR, DEM, Bayesian network, vulnerability, susceptibility, runout, landslide dam.
- Translate “cascading hazards” according to context as `级联灾害`, `链式灾害`, or `灾害链`.
- Translate “geohazard chain” as `地质灾害链`.
- Translate “multi-hazard chain” as `多灾种链` or `多灾种灾害链`.
- Keep quantitative values and units unchanged.
- Do not add interpretations that are not in the abstract.

## Introduction-Style Synthesis

Use this pattern for a Chinese literature synthesis:

```text
围绕<主题>，已有研究主要从<方向1>、<方向2>和<方向3>等方面展开。<作者，年份>以<地区/对象>为例，采用<方法/数据>，揭示/发现/表明<核心结果>。<作者，年份>进一步从<角度>出发，构建/提出/评估<模型或框架>，结果显示<核心结果>。此外，<作者，年份>关注<另一类过程或情景>，说明<机制或影响>。总体来看，现有研究已经在<已有进展>方面形成基础，但在<不足/空白>方面仍有待深化。因此，后续研究可从<你的研究切入点>出发，进一步<研究目标>。
```

## Per-Paper Summary Sentence

Use this compact form:

```text
<作者/第一作者>（<年份>）以<研究区/事件/对象>为例，采用<方法/数据>研究了<问题>，结果表明<主要结果/机制/贡献>。
```

Variants:

```text
<作者/第一作者>（<年份>）构建了<模型/框架>，用于评估<对象>，发现<结果>，为<应用>提供了依据。
```

```text
<作者/第一作者>（<年份>）基于<遥感/现场调查/数值模拟/统计模型>分析了<灾害链过程>，指出<触发因素>通过<过程>导致<结果>。
```

## Final Response Template

```text
已完成：
- 检索来源：<CNKI / Semantic Scholar / CrossRef / OpenAlex / publisher pages>
- 筛选标准：<年份、主题、引用量、期刊、语言>
- 导入 Zotero：<N> 篇
- 补摘要：<N>/<N>
- 生成中文翻译笔记：<N>/<N>
- 备份：<path if any>
- 导出文件：<path if any>

引言式总结：
<one or more paragraphs>
```
