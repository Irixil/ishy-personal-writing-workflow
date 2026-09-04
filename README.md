# ISHY Personal Writing Workflow

一套为 ISHY 持续维护的个人写作工作流，用于把真实经历、产品材料、事实证据和作者判断推进成可以公开署名的文章。

[中文](#中文) · [English](#english)

当前版本为 <code>2.4.0</code>。

## 中文

### 名字说明

- GitHub 仓库名是 <code>ishy-personal-writing-workflow</code>。
- Codex 中的 Skill 调用名是 <code>$ai-pm-personal-writing</code>。
- 仓库名称代表整套个人写作流程，Skill 名称保留原来的调用兼容性。

### 这套工作流解决什么

它覆盖一篇文章从想法还没有收束，到最终完成审阅的全过程，也可以为这些文章制作风格一致的封面和系列插图。

题目与材料 → 观点讨论 → 大纲确认 → 逐章写作 → 全文整合 → 自动检查 → Article Reviewer 批注 → 保存新版本

它不会只根据一个主题直接生成一篇看起来完整的长文。开始写作前会先检查题目是否成立、材料是否足够、哪些内容属于事实、哪些只是作者判断。文章形成以后，还可以进入 Article Reviewer，由作者直接编辑、添加批注，再让 Codex 按最新版继续修改。

### 核心能力

| 能力 | 实际作用 |
| --- | --- |
| 观点讨论 | 找出文章真正要回答的问题，检验隐藏前提、中心观点、最强反方和成立边界 |
| 材料检查 | 区分用户亲历、官方事实、公开证据、作者推断和当前未知，材料不足时研究、追问或缩小篇幅 |
| 大纲设计 | 为每一章确定任务、主要材料、限制条件和对下一章的推进作用 |
| 逐章写作 | 按已确认的大纲分段生成，保留用户已经修改和确认的版本 |
| 全文整合 | 合并重复内容，统一术语、来源、时间口径和个人文风 |
| 两种文章模式 | 支持 AI 产品经理专业文章与个人观察型产品随笔 |
| 个人声音 | 保留具体经历的时间、频率和限制，写出有立场但克制、有一线实操感的作者位置 |
| 文章检查器 | 检查占位符、空泛开场、模型化路标、营销表达、绝对化断言、反问、短句排队和来源风险 |
| Article Reviewer | 打开可编辑审阅页面，接收直接修改和批注，按版本安全保存并重新打开 |
| 文章插图 | 按指定视觉 Profile 先做样稿、根据反馈局部修改，经两次确认后完成批量图片与长期角色固定 |

### 两种文章模式

#### AI 产品经理专业文章

适合以下内容：

- AI 产品方法、产品设计和迭代经验
- Agent、RAG、模型能力、评测和数据反馈
- AI 行业与产品趋势判断
- 产品案例拆解和项目复盘
- 面向 AI 产品经理或转行人群的专业科普

文章会同时检查用户价值、产品机制、商业条件、风险边界和验证标准。技术概念必须落到真实产品动作，抽象判断要能被事实或可观察条件支撑。

#### 个人观察型产品随笔

适合从个人经历、阅读材料、亲近关系或现实分歧进入产品判断的文章。

这类文章可以先把作者自己放进问题，再逐步走向思想材料和产品案例。结尾回到一个具体行动、仍未解决的问题或下一次会怎样判断，不用临时升高成时代宣言。

### 默认协作流程

#### 1. 讨论观点

先确认题目、读者、问题、材料和篇幅。Skill 会检查题目中的隐藏前提，并给出中心观点、主要依据、最强反方、限制和未知。

观点没有确认时，不提前生成大纲和正文。

#### 2. 确认大纲

观点确认后，再确定标题、目标读者、章节任务、关键材料、预计篇幅和仍需补充的证据。

大纲没有确认时，不开始正文。

#### 3. 逐章生成

默认每轮写一章。用户直接修改过的章节是唯一当前版本，后续内容不能退回更早草稿。

如果新证据足以推翻中心观点，Skill 会停止续写并回到观点讨论。

#### 4. 全文整合

所有章节确认后，Skill 会合并重复内容、修正衔接、统一术语和来源，并运行对应的文章检查模式。

如果希望一次性交付，可以明确说“跳过确认”“直接写完”或“连续生成”。Skill 仍会在内部完成观点和结构检查。

### 红围巾猫头鹰插图流程

文章需要封面、配图或系列插图时，可以调用“红围巾猫头鹰 × 撕纸拼贴”视觉 Profile。纯写作任务不会自动进入配图流程。

~~~text
使用红围巾猫头鹰拼贴视觉配置。
~~~

固定流程为：单张样稿 → 用户反馈局部修改 → 确认本批次角色与风格 → 批量生成 → 整组确认 → 固定长期角色。局部修改只动指定维度；重要中文优先确定性排版，图像模型直出的中文必须逐字检查。

### Article Reviewer 审阅闭环

文章完成后，可以直接说：

~~~text
使用 $ai-pm-personal-writing 写完这篇文章，然后打开 Article Reviewer 让我批注。
~~~

审阅页面打开后，你可以：

- 直接修改正文
- 选中文字添加批注
- 等待页面显示已经保存
- 回到对话发送“开始修改”或“按批注修改”

收到“开始修改”后，Codex 必须先读取 Article Reviewer 中最新保存的正文和全部批注。页面里的直接修改优先于聊天旧稿和磁盘旧稿。

随后它会：

1. 按顺序处理全部有效批注。
2. 只修改批注授权的内容，不顺手重写其他段落。
3. 保存为新的不可变版本，并清空已处理批注。
4. 重新打开同一篇文章，让你检查结果。

批注位置不明确、正文为空、版本冲突或源文件哈希变化时，流程会停止，不会猜测或静默覆盖。

如果审阅记录关联了源文件，写入前还会重新核对文件哈希、创建可恢复备份，并保留原始 Markdown 或其他文件格式。

Article Reviewer 是可选功能。普通写作任务不会自动打开审阅页面。

### 事实与证据边界

- 用户亲历保留原来的时间、频率、场景和程度，不能扩大成普遍结论。
- 产品功能优先以官方文档、实际流程和可核验资料为准。
- 模型能力、产品能力和具体版本分开描述。
- 数据说明来源、时间、样本和口径。
- 公开用户反馈不能伪造成具体身份、精确原话或普遍事实。
- 因果证据不足时，使用“相关”“可能影响”或明确说明仍待验证。
- 一千二百字以上的现实文章，内部至少要有五件能够组成实际过程的具体材料。

### 使用示例

讨论观点：

~~~text
使用 $ai-pm-personal-writing，和我讨论一篇关于 Agent 产品授权边界的文章。
~~~

直接完成专业文章：

~~~text
使用 $ai-pm-personal-writing，跳过确认，根据这些材料完成一篇 AI 产品分析文章。
~~~

写个人观察型产品随笔：

~~~text
使用 $ai-pm-personal-writing，把这段真实经历和阅读材料写成一篇个人观察型产品随笔。
~~~

深度修改已有文章：

~~~text
使用 $ai-pm-personal-writing，检查这篇文章的事实、反方、产品边界和结论，再完成全文改稿。
~~~

进入审阅页面：

~~~text
使用 $ai-pm-personal-writing 写完文章，并打开 Article Reviewer 让我修改和批注。
~~~

制作文章插图：

~~~text
使用红围巾猫头鹰拼贴视觉配置，为这篇文章制作封面和系列插图。
~~~

### 安装

把仓库克隆到 Codex Skills 目录：

~~~bash
git clone https://github.com/Irixil/ishy-personal-writing-workflow.git ~/.codex/skills/ai-pm-personal-writing
~~~

也可以下载仓库后，把完整目录复制到：

~~~text
~/.codex/skills/ai-pm-personal-writing
~~~

重新打开一个 Codex 任务后即可使用 <code>$ai-pm-personal-writing</code>。

Article Reviewer 审阅功能需要同时安装并启用 Article Reviewer 插件。没有该插件时，写作、改稿和文章检查器仍然可以正常使用。

### 文章检查器

检查专业文章：

~~~bash
python3 scripts/check_ai_pm_article.py 稿件.md
~~~

检查个人观察型产品随笔：

~~~bash
python3 scripts/check_ai_pm_article.py --mode essay 稿件.md
~~~

检查器负责发现稳定的文字形状和风险信号，不代替作者对事实、观点和体裁的判断。

### 目录结构

~~~text
ai-pm-personal-writing/
├── SKILL.md
├── VERSION
├── README.md
├── LICENSE
├── agents/
│   └── openai.yaml
├── assets/
│   └── icon.svg
├── references/
│   ├── article-reviewer.md
│   ├── article-structure.md
│   ├── evidence.md
│   ├── revision.md
│   ├── visual-profile-red-scarf-owl.md
│   └── voice-profile.md
└── scripts/
    └── check_ai_pm_article.py
~~~

- <code>SKILL.md</code> 定义任务边界、四阶段协作、Article Reviewer 与视觉 Profile 路由。
- <code>voice-profile.md</code> 保存已经确认的个人声音和写作习惯。
- <code>article-structure.md</code> 提供不同文章类型的结构与论证方法。
- <code>evidence.md</code> 规定事实、数据、产品能力和个人经历的边界。
- <code>revision.md</code> 负责全文形成后的系统改稿。
- <code>article-reviewer.md</code> 定义打开、批注、修改、保存和复核流程。
- <code>visual-profile-red-scarf-owl.md</code> 定义红围巾猫头鹰撕纸拼贴插图的角色、视觉、生成和 QA 规则。
- <code>check_ai_pm_article.py</code> 提供两种可重复执行的成稿检查模式。

### 不适用的任务

这套 Skill 不用于 PRD、管理层汇报、小说、营销软文、普通聊天和纯代码教程。遇到这些任务时，应当使用更合适的 Skill 或工作流。

### License

MIT License

## English

### Naming

- The GitHub repository is named <code>ishy-personal-writing-workflow</code>.
- The Codex skill is invoked as <code>$ai-pm-personal-writing</code>.
- The repository name describes ISHY's complete writing workflow, while the skill name remains stable for invocation compatibility.

### What this workflow does

ISHY Personal Writing Workflow covers the full path from an unsettled idea to a reviewed, versioned article. It can also create a consistent cover and illustration series for those articles.

Topic and materials → claim discussion → outline approval → section drafting → full revision → automated checks → Article Reviewer annotations → new saved version

It does not treat a topic as permission to generate a polished-looking long article immediately. It first checks whether the question holds, whether the materials are sufficient, which statements are facts, and which are the author's judgment. After drafting, the article can move into Article Reviewer for direct editing, annotations, version-safe revision, and verification.

### Core capabilities

| Capability | What it does |
| --- | --- |
| Claim discussion | Identifies the real question, hidden assumptions, central claim, strongest counterargument, and limits |
| Material checks | Separates personal experience, official facts, public evidence, inference, and unknowns |
| Outline design | Gives every section a purpose, supporting material, limitations, and a clear role in the argument |
| Section drafting | Drafts from the approved outline and preserves the user's latest edits as the only current version |
| Full revision | Removes repetition and aligns terminology, sources, chronology, structure, and personal voice |
| Two writing modes | Supports professional AI product articles and reflective product essays |
| Personal voice | Preserves the time, frequency, context, and limits of real experience while keeping a clear but restrained position |
| Article checker | Flags placeholders, generic openings, model-like signposting, hype, absolute claims, rhetorical questions, repetitive short sentences, and source risks |
| Article Reviewer | Opens an editable review page, reads direct edits and annotations, saves a new version, and reopens it for verification |
| Article illustrations | Uses a selected visual profile to create one sample, apply scoped feedback, pass two approval gates, and only then lock a reusable character |

### Two writing modes

#### Professional AI product articles

Designed for AI product methods, product design and iteration, Agents, RAG, model evaluation, industry analysis, product case studies, project retrospectives, and professional explainers.

The workflow checks user value, product mechanics, commercial conditions, risk boundaries, counterarguments, and testable standards. Technical concepts must eventually connect to observable product behavior.

#### Reflective product essays

Designed for articles that begin with personal experience, reading, close relationships, or a real disagreement and gradually move toward a product judgment.

The writer can first place themselves inside the problem, then use verified intellectual material and a real product case to develop the argument. The ending returns to a concrete action, an unresolved question, or a clearer boundary instead of making a sudden claim about the entire era.

### Default collaboration flow

1. Discuss the question, central claim, evidence, counterarguments, limits, and unknowns.
2. Confirm the title, audience, purpose of each section, supporting materials, and expected length.
3. Draft one section at a time while preserving the user's latest edits.
4. Integrate the full article, align sources and terminology, and run the appropriate article-checking mode.

To receive a complete draft in one pass, explicitly ask to “skip confirmation,” “write the full article directly,” or “continue without stopping.” The skill will still test the claim and structure internally.

### Red scarf owl illustration flow

For a cover, article image, or illustration series, invoke the “red scarf owl × torn-paper collage” visual profile. Pure writing tasks do not start this workflow automatically.

~~~text
使用红围巾猫头鹰拼贴视觉配置。
~~~

The fixed sequence is: one sample → scoped edits from user feedback → approval of the batch character and style → batch generation → full-set approval → long-term character lock. Important Chinese text uses deterministic typesetting when possible; any model-rendered Chinese is checked character by character.

### Article Reviewer loop

Ask the skill to finish an article and open it for review:

~~~text
Use $ai-pm-personal-writing to finish this article, then open it in Article Reviewer for my edits and annotations.
~~~

In the review page, edit the body directly or attach notes to selected text. Wait until the page reports that the version has been saved, then return to the conversation and say “start editing” or “apply the annotations.”

Codex must retrieve the latest saved article and every active annotation before making changes. It then applies only the authorized edits, saves a new immutable version, clears resolved annotations, and reopens the same article for verification.

The process stops rather than guessing when an annotation is ambiguous, the article is empty, a version conflict occurs, or a linked source file has changed. Linked source files are hash-checked and backed up before any write.

Article Reviewer is optional and opens only when requested. The writing workflow and article checker still work without it.

### Evidence boundaries

- Preserve the original time, frequency, context, and degree of personal experience.
- Prefer official documentation, observed product behavior, and verifiable sources for product capabilities.
- Keep model capability, product capability, and specific versions separate.
- State the source, date, sample, and measurement definition for data.
- Never invent user identities, precise quotations, platform reactions, or universal conclusions.
- Use cautious language when the evidence supports correlation or a possible mechanism rather than causation.
- A nonfiction article planned at 1,200 Chinese characters or more needs at least five concrete materials that can form a real process.

### Usage examples

~~~text
Use $ai-pm-personal-writing to discuss the central claim for an article about authorization boundaries in Agent products.
~~~

~~~text
Use $ai-pm-personal-writing to skip confirmation and turn these materials into a complete AI product analysis.
~~~

~~~text
Use $ai-pm-personal-writing to turn this real experience and reading material into a reflective product essay.
~~~

~~~text
Use $ai-pm-personal-writing to review this article's facts, counterarguments, product boundaries, and conclusion, then complete the revision.
~~~

~~~text
使用红围巾猫头鹰拼贴视觉配置，为这篇文章制作封面和系列插图。
~~~

### Installation

~~~bash
git clone https://github.com/Irixil/ishy-personal-writing-workflow.git ~/.codex/skills/ai-pm-personal-writing
~~~

Open a new Codex task and invoke <code>$ai-pm-personal-writing</code>.

The Article Reviewer workflow requires the Article Reviewer plugin. All other writing and checking features work without it.

### Article checker

Professional article:

~~~bash
python3 scripts/check_ai_pm_article.py draft.md
~~~

Reflective product essay:

~~~bash
python3 scripts/check_ai_pm_article.py --mode essay draft.md
~~~

The checker surfaces repeatable textual patterns and risk signals. It does not replace editorial judgment about evidence, claims, or genre.

### Repository structure

~~~text
ai-pm-personal-writing/
├── SKILL.md
├── VERSION
├── README.md
├── LICENSE
├── agents/openai.yaml
├── assets/icon.svg
├── references/
│   ├── article-reviewer.md
│   ├── article-structure.md
│   ├── evidence.md
│   ├── revision.md
│   ├── visual-profile-red-scarf-owl.md
│   └── voice-profile.md
└── scripts/check_ai_pm_article.py
~~~

### Out of scope

This skill is not intended for PRDs, executive reports, fiction, promotional copy, casual conversation, or code-only tutorials.

### License

MIT License
