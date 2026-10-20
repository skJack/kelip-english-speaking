# 英语口语日记 · 工作区规则

这是用户「AI 练口语 + 英文日记」的工作区（由 kelip-english-speaking 搭建）。任何 agent 接手都先读完这一页；设置在 `speaking.json`。

练口语本身在 ChatGPT 里完成：开始 Prompt → 语音讲四段 → 结束 Prompt 生成一篇 Markdown 日记。你管的是之后的事。

## 你会被要求做的事

| 用户说 / 触发 | 做什么 |
|---|---|
| 「入库」+ 一段 Markdown 或一个 .md 文件；或者直接丢来一段以 `FILE_PATH:` 开头的日记 | 入库 |
| 「这篇是 X 号的」「日期错了」 | 日期更正 |
| 「复习一下」，或复习卡的定时任务 | 复习卡 |
| 提醒的定时任务 | 提醒 |
| 「周总结」 | 周总结 |
| 「给我开始 / 结束 Prompt」 | 把 `prompts/START_PROMPT.md` / `END_PROMPT.md` 代码块里的全文发给用户，不要改 |

## 目录

```
AGENTS.md                本文件
speaking.json            设置：时区、讲哪天、母语、打卡主题、复习卡时刻、提醒时刻
prompts/                 用户自己的开始 / 结束 Prompt
journal/YYYY/            日记：YYYY-MM-DD.md；同一天第二份是 YYYY-MM-DD-2.md
language-bank.md         词库：所有真正新学的表达和复习进度
review-log.md            发过的复习卡（日期、时刻、条目），用来避免同一天重复出题
weekly-reviews/          周总结：YYYY-Www.md
```

日期一律按 `speaking.json` 的 `timezone`。

## 入库

1. **读全文**，不要只看文件名猜内容。去掉第一行 `FILE_PATH: …` 和包住全文的 ``` 代码围栏，正文里的标题和表格原样保留；只保留一份 frontmatter。
2. **定日期**：用户明说的（「这是昨天的」「入库到 10 月 3 号」）优先于 frontmatter 的 `date`。两者都没有就问一句，不要猜。
3. **三处一致**：文件名 `journal/YYYY/YYYY-MM-DD.md`、frontmatter 的 `date`、一级标题 `# YYYY-MM-DD — …` 里的日期。
4. **不覆盖**：
   - 目标文件不存在 → 新建（年份目录不存在就先建）；
   - 已存在且内容完全相同 → 什么都不写，告诉用户这篇已经入过；
   - 已存在但内容不同 → 存成 `YYYY-MM-DD-2.md`（再有就 `-3`），告诉用户这一天有两份。
5. **不改内容**：不润色正文，不补评分、发音分或打卡数字。只修格式问题（缺 frontmatter 结束线、标题层级错了这类），修了什么要在回报里说。
6. **更新词库**：见下一节。
7. **回报**：模板在最后。

## 日期更正

用户说「这篇不是 5 号，是 4 号」时，一起改：文件名、frontmatter 的 `date`、一级标题里的日期；
词库里这一篇带进来的条目的 First learned（如果就是这篇首次学的）、Source 链接、Last seen 和 Next review。
改之前先确认目标日期的文件不存在；已存在就按「不覆盖」那条另存，并告诉用户。

## 词库 `language-bank.md`

表头（12 列）：

```
| First learned | Item | Type | Chinese meaning | Fixed usage or pattern | Personal example | Source | Last seen | Last reviewed | Review count | Next review | Status |
```

入库时逐行读日记的 `## New Vocabulary and Fixed Phrases` 表：

- **规范化后去重**：小写，去首尾空格，统一直引号 / 弯引号和省略号。介词和句型是条目的一部分——`be proud of` 和 `proud`、`want to + verb` 和 `want` 是不同条目。
- **新条目**：First learned 和 Last seen = 日记日期；Source = 这篇日记的相对链接，如 `[2026-03-12](journal/2026/2026-03-12.md)`；
  Last reviewed = `—`；Review count = `0`；Next review = 日记日期的第二天；Status = `New`。
- **已有条目**：不新增行。保留 First learned、Review count 和排期；Source 追加这篇；Last seen 改成这篇的日期；这次的例句更好就补上。
- 单元格里的竖线写成 `&#124;`，别把表格撑坏。
- **永远不删行**，也不改写别的条目。

## 复习卡

**挑条目**（每张 `review.items_per_card` 条，默认 3）：

1. Next review ≤ 今天的，过期越久越先；
2. 不够就补 Status 为 `New`、`Learning` 的；
3. 还不够就从 `Review`、`Mastered` 里随机补；
4. 当天已经出过的不再出——发卡后在 `review-log.md` 末尾记一行：`YYYY-MM-DD HH:MM · 条目1 · 条目2 · 条目3`。

**卡片格式**：先出题，答案放在分隔线下面，让用户先想。题目用用户的母语写意思，答案给英文条目、用户自己的例句和一句用法提示：

```
☀️ 复习卡（先想一想，答案在下面）

1. <意思>，用英语怎么说？
2. <意思>，怎么说？
3. <意思>，怎么说？

---

答案

1. `<Item>`
   你的例句：<Personal example>
   提示：<Fixed usage or pattern，一句话>

2. …

3. …

挑一两个造句发我，我帮你改，再更新复习记录。
```

**用户回了句子**：每句改成自然的说法，只指出最重要的一两处，然后更新词库里这几条：

| 这一条是第几次答对 | Next review | Status |
|---|---|---|
| 第 1 次 | 3 天后 | Learning |
| 第 2 次 | 7 天后 | Learning |
| 第 3 次 | 14 天后 | Review |
| 第 4 次 | 30 天后 | Review |
| 第 5 次 | 不再排期 | Mastered |

答对时 Review count 加 1、Last reviewed 改成今天。想不起来或用错了：Next review = 明天，Status = `Learning`，次数不变。
用户没回就什么都不改——发卡不算复习。

**用户主动说「复习一下」**：同样挑条目，但改成一次问一条，三种问法轮着用：给意思让用户说英文 / 给半句让用户补完 / 让用户用这个条目说一句自己的事。每条答完就按上表更新。

## 提醒

每天 `reminder.time`（默认 18:00）检查昨天的日记在不在（`journal/YYYY/<昨天>.md` 或 `<昨天>-2.md`）：

- 在 → 什么都不发；
- 不在 → 发一句就够，比如「昨天的口语日记还没入库，今天抽 10 分钟讲讲？讲完把结束 Prompt 的结果发我就行。」一天最多一次，不催第二遍。

用户说「这几天休息 / 出差，先别提醒」就暂停，等用户说恢复。

## 周总结

用户说「周总结」时，读这一周的日记和词库，写 `weekly-reviews/YYYY-Www.md`：

反复出现的主题、这周的进步、常见的英语问题、这周新学的表达、到期待复习的条目、口语评分的走势（有评分才写）、
打卡数字的走势（有数字才写）、下周一个口语重点和一个打卡重点。不改原日记。

## 隐私

- 日记、词库、打卡数据、Prompt 里的个人背景都是用户的私人数据：不提交到公开仓库，不贴进公开的 issue、日志或分享链接，不发给用户没指定的服务。
- 工作区要是 git 仓库，`.gitignore` 已经排除了 `journal/`、`language-bank.md`、`review-log.md`、`weekly-reviews/`、`prompts/` 和 `speaking.json`。
- 健康类打卡数据只出现在给用户本人的回报里。

## 回报模板

```
已入库 YYYY-MM-DD：
- 日记：journal/YYYY/YYYY-MM-DD.md
- 口语评分：X.X/10（CEFR X）
- 词库：新增 N 条（列出 3–5 条），更新 M 条
- 打卡：一句话（这篇没有打卡就删掉这一行）
- 明天的口语重点：取日记里的 Next Speaking Focus
```
