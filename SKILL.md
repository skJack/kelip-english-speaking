---
name: kelip-english-speaking
description: 帮用户搭建并日常运行一套「AI 练英语口语 + 英文日记」系统：开始 Prompt 让 ChatGPT 语音（GPT Live）当口语教练，每天固定讲四段，每段讲完整段润色、用户再说一遍；结束 Prompt 把对话整理成一篇 Markdown 英文日记（纠错、真正新学的表达、口语评分）；Agent 把日记按日期入库、新表达去重进词库，白天定时推复习卡，傍晚没交日记就提醒一次。用户说「帮我搭一个练口语的系统」「我想用 AI 练英语口语」「给我练口语的 prompt」「把这篇日记入库」「复习一下」「这篇是昨天的」「口语周总结」时用它——包括只丢来一段以 FILE_PATH 开头的英文日记 Markdown 的时候。
---

# AI 练口语 + 英文日记

每天 10–20 分钟的英语口语练习，顺手把每一天写成英文日记：

```
开始 Prompt ─▶ ChatGPT 语音（GPT Live）按四段讲 ─▶ 结束 Prompt ─▶ 一篇 Markdown 英文日记
                                                                    │ 用户发给你：「入库」
                                                                    ▼
                    日记按日期存档 · 新表达去重进词库 · 白天定时推复习卡 · 傍晚没交就提醒一次
```

核心是 `prompts/` 里的两段 Prompt，练口语这件事在 ChatGPT 里完成；你负责剩下的：入库、词库、复习卡、提醒。
下文 `<skill>` 指这个 SKILL.md 所在的目录，`<ws>` 指用户的工作区。

## 先判断是哪种请求

| 用户说 | 做什么 |
|---|---|
| 「帮我搭一个练口语的系统」「我想用 AI 练英语」「照这个仓库搭起来」 | 第一次搭建 → 下面「搭建」五步 |
| 「给我两个 prompt」「只要 prompt」 | 把 `prompts/start-prompt.md`、`prompts/end-prompt.md` 代码块里的原文**完整**发给用户，再用三句话说怎么用（见「每天怎么用」）；用户想改第二段就按 `references/customize.md` 改 |
| 「入库」+ 一段 Markdown 或 .md 文件、「复习一下」、「这篇是 X 号的」、「周总结」，或定时任务触发 | 日常运行：找到工作区（有 `speaking.json` 的目录），读它的 `AGENTS.md` 照做。找不到就问用户工作区在哪；还没搭过就先搭 |

## 搭建（第一次）

### 1. 一次问完这几个问题

合成一条消息发出去，每题都带默认值，用户回「默认」就全用默认：

1. **工作区放哪**：默认 `~/english-speaking/`。你要是云端 agent（自带云电脑的那种个人 agent），就放在你自己的工作目录里。
2. **什么时候练**：晚上讲今天（默认）/ 早上讲昨天（比如通勤路上戴耳机讲）。时区默认 `Asia/Shanghai`。
3. **第二段打卡记什么**：健康——吃喝、运动、睡眠（默认）/ 学习或工作 / 爱好练习（练琴、练字……）/ 不要第二段 / 自己说。
4. **要不要给教练一点个人背景**：目标、在执行的计划、需要注意的限制。只写进用户自己的两段 Prompt，不放别处。默认不加。
5. **母语**：求助、解释和词库里的释义用什么语言，默认中文。水平不用问，评分会自己给 CEFR。
6. **复习卡和提醒**：默认 08:00–20:00 每 2 小时一张、每张 3 条；每天 18:00 检查昨天的日记有没有入库，没有就提醒一次。由谁发：你自己（你能定时发消息的话）/ 不要定时，想复习时说「复习一下」。

### 2. 生成用户自己的两段 Prompt

- 原文取 `<skill>/prompts/start-prompt.md`、`end-prompt.md` 的代码块。默认版 = 健康打卡 + 讲今天 + 中文 + Asia/Shanghai。
- 按第 1 步的回答，照 `references/customize.md` 只改那几处：第二段（开始和结束 Prompt 里一共四个位置）、个人背景块、早上讲昨天、时区、母语。
  **其余一字不改**——「讲完一整段再整段润色」「再说一遍」「只挑一两处」「不追问」「不编造」这几条是这套流程练得出东西的原因。
- 写到 `<ws>/prompts/START_PROMPT.md`、`<ws>/prompts/END_PROMPT.md`，再把两段**全文**发给用户（用户要复制进 ChatGPT）。

### 3. 建工作区

```
<ws>/
  AGENTS.md            ← 复制 <skill>/templates/AGENTS.md：入库、词库、复习卡、提醒、周总结的全部规则
  speaking.json        ← 复制 <skill>/templates/speaking.json，按第 1 步的回答填
  language-bank.md     ← 复制 <skill>/templates/language-bank.md（空词库，只有表头）
  prompts/START_PROMPT.md, END_PROMPT.md
  journal/YYYY/        ← 日记，按年分目录，入库时再建
  .gitignore           ← 复制 <skill>/templates/gitignore：工作区就算是 git 仓库，日记和词库也不会被提交
```

`speaking.json` 的字段：`timezone`、`describe_day`（`today` / `yesterday`）、`native_language`、`checkin`（`health` / `study` / `hobby` / `none` / 自定义的一句话）、
`review.times`（发卡的时刻）、`review.items_per_card`、`reminder.time`、`deliver`（`agent`：你定时发 / `on-demand`：只在用户说「复习一下」时出卡）。
母语不是中文时，把 `language-bank.md` 表头的 `Chinese meaning` 和 `AGENTS.md` 里复习卡的模板换成用户的语言。

工作区自带一份完整的 `AGENTS.md`，以后换任何 agent 来接手（哪怕没装这个 skill），读它就能继续。

### 4. 设定时任务

规则在 `templates/AGENTS.md` 的「复习卡」「提醒」两节，时间从 `speaking.json` 读。

- **你能定时给用户发消息**（云端个人 agent）：建两个定时任务，任务内容写成这样，别把规则抄进任务里——规则只在工作区的 `AGENTS.md` 维护一份：
  - 复习卡，每天 `review.times` 的每个时刻：「读 `<ws>/AGENTS.md`，按『复习卡』一节发一张复习卡。」
  - 提醒，每天 `reminder.time`：「读 `<ws>/AGENTS.md`，按『提醒』一节检查昨天的日记；没有就提醒一句，有就什么都不发。」
- **你是本地的 coding agent**（Claude Code、Codex、Cursor 这类）：先告诉用户电脑得开着才发得出去。你有自带的定时任务功能就用它建上面两个任务；没有就别自己装后台进程，
  把 `deliver` 设成 `on-demand`，告诉用户想复习时说「复习一下」。想电脑合上也能收卡，可以把这个仓库交给一个云端 agent 再搭一遍。
- 建完把任务清单（几点、干什么）回报给用户。

### 5. 交付

回报四件事：工作区路径、两段 Prompt（已经发了全文）、定时任务清单、每天怎么用（下面四步）。
用户要看板（网页、前端）再按 `references/dashboard.md` 做，默认不做。

## 每天怎么用（讲给用户听的）

1. 在 ChatGPT 新建对话，贴开始 Prompt，打开语音（GPT Live）。
2. 按它的问题讲四段，每段讲完说 “I've finished this part.”；它整段润色，你用自己的话再说一遍，它只挑一两处。卡住了随时用中文问「这个怎么说」。
3. 讲完退出语音，**在同一个对话里**贴结束 Prompt，它输出一行 `FILE_PATH:` 和一个 Markdown 代码块。
4. 整段发给 agent，说「入库」。之后复习卡会按时来，挑一两个造句回给 agent，它帮你改并更新复习记录。

## 日常运行

全部规则在工作区的 `AGENTS.md`（模板 `templates/AGENTS.md`），每次处理前先读它。要点：

- **入库**：去掉 `FILE_PATH:` 行和外层代码围栏；日期以用户明说的为准；文件名、frontmatter `date`、一级标题三处一致；
  同一天已有不同内容就另存 `YYYY-MM-DD-2.md`，不覆盖；新表达按规范化后的英文去重进词库；最后按模板回报。
- **复习卡**：先挑到期的，再补新的；先出题、答案在下面；用户回了句子才更新复习记录（间隔 1 → 3 → 7 → 14 → 30 天，答错回到明天）。
- **提醒**：只查昨天那篇在不在；不在就提醒一句，一天最多一次。

## 硬规矩

- **不编造。** 日记、词库、复习卡里的每一条都要有对话依据：没说过的事不写，没教过的不算新表达，没有可靠音频不评发音，没报的数字写 `null`。
- **日记、词库、打卡数据、个人背景都是用户的私人数据。** 不提交到任何公开仓库，不贴进公开的 issue、日志或分享链接，不发给用户没指定的服务。
  健康类数据只出现在给用户本人的回报里。
- **只给生活建议。** 打卡涉及健康时不谈药，不鼓励节食、脱水或过量运动；用户说胸痛、头晕、晕倒这类情况，先让用户停下、休息、找医生。
- **不静默覆盖**任何一篇日记或词库里的历史记录。
- **提醒只发一次**，交了就不打扰。

## 文件

| 路径 | 是什么 |
|---|---|
| `prompts/start-prompt.md` | 开始 Prompt（默认版）+ 每一块在干什么 |
| `prompts/end-prompt.md` | 结束 Prompt（默认版）+ 输出格式 |
| `references/customize.md` | 换第二段主题、加个人背景、早上讲昨天、改时区和母语、可选的打卡评分 |
| `references/dashboard.md` | （可选）本地看板的页面清单和做法 |
| `templates/AGENTS.md` | 复制进工作区的日常规则：入库、日期更正、词库、复习卡、提醒、周总结、回报模板 |
| `templates/language-bank.md` | 空词库（12 列表头） |
| `templates/speaking.json` | 设置（默认值） |
| `templates/gitignore` | 工作区的 `.gitignore` |
| `examples/journal-example.md` | 结束 Prompt 生成的一篇日记（虚构的例子） |
