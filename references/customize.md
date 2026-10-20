# 改 Prompt

默认版：第二段是健康打卡、讲今天、中文、Asia/Shanghai。下面每一种改法都只动列出来的位置，其余一字不改。
改完把两段全文重新发给用户，并同步改工作区的 `speaking.json`。

## 第二段换主题

一共四个位置要一起改：

| | 文件 | 位置 |
|---|---|---|
| ① | 开始 Prompt | `FOUR PARTS` 列表里的第 2 条 |
| ② | 开始 Prompt | `CHECK-IN RULES (PART 2)` 整块 |
| ③ | 开始 Prompt | `THE FOUR OPENING QUESTIONS` 里 Part 2 的问题，以及 `ENDING THE SESSION` 第 4 条 |
| ④ | 结束 Prompt | `CHECK-IN RULES` 整块、frontmatter 的打卡字段、`## Check-in` 下面的小节 |

另外，开始 Prompt 的 `Do not invent events, … foods, amounts, or exercise` 和结束 Prompt `ACCURACY RULES` 里的 `foods, amounts, exercise, or sleep times`，换成新主题会被记下的东西。

### 学习 / 工作

① `2. My daily check-in: what I studied or worked on, and for how long`

② 

```
CHECK-IN RULES (PART 2)

- Part 2 is still speaking practice. Let me speak freely, then polish and retry as usual.
- In the polished version, keep every task, subject, time, and number exactly as I reported it.
- If I leave out something essential (what I worked on or for how long), you may ask ONE short question that covers everything missing. If I say I don't know, accept it and move on.
- After my retry and your language corrections, give me a short check-in note in simple English, no more than about 80 words:
  1. One thing I did well.
  2. One or two specific suggestions for tomorrow, such as how to plan, focus, or rest, based only on what I actually reported.
- Be practical and encouraging, not preachy. Do not invent achievements.
- Words for my subjects and my work are useful new language too. Teach them naturally when I ask how to say something.
```

③ Part 2 问题：`“Now let's do your daily check-in. What did you study or work on, for how long, and how did it go? Say ‘I've finished this part’ when you are done.”`；Ending 第 4 条不变。

④ frontmatter 打卡字段换成 `focus_minutes: X`；`## Check-in` 下面换成：

```
### My Check-in Report

Use the final polished version from Part 2.

### Log

| Task | Time spent | Result | Notes |
|---|---|---|---|
| ... | ... | ... | ... |

### Coach Advice

1. **做得好：** ...
2. **明天调整：** ...

**Tomorrow's check-in focus:** One small, specific action.
```

结束 Prompt 的 `CHECK-IN RULES` 换成：只用用户报过的任务和时长；没报的数字写 `null` / `Not reported`；Coach Advice 用中文、最多三条、针对用户今天实际做的；没聊到就所有打卡字段写 `null`、`## Check-in` 下写 `Not discussed`。

### 爱好练习（练琴、练字、某项运动……）

把下面的 `<hobby>` 换成具体的事，比如 `piano`。

① `2. My daily check-in: my <hobby> practice`

② 同「学习 / 工作」那一版，第 2 条改成 `keep every piece, exercise, tempo, time, and number exactly as I reported it`，
建议那条改成 `One or two specific suggestions for my next practice session`。

③ Part 2 问题：`“Now let's do your daily check-in. What did you practise today, for how long, and what felt difficult? Say ‘I've finished this part’ when you are done.”`

④ frontmatter 换成 `practice_minutes: X`；`### Log` 的表头换成 `| What I practised | Time | How it went |`。

### 不要第二段

- 开始 Prompt：`EXACTLY FOUR PARTS` → `EXACTLY THREE PARTS`，删掉第 2 条并把后面两条改成 2、3；删掉 `Part 2 has one extra step …` 那段、整块 `CHECK-IN RULES (PART 2)`、
  Part 2 的开场问题、`TRANSITIONS` 里的 `(plus the check-in note in Part 2)` 和 `In Part 2, this can be …` 那句、`ENDING` 第 4 条；剩下的 Part 3、Part 4 改称 Part 2、Part 3。
  第一段 `do a short daily check-in, ` 删掉。
- 结束 Prompt：删掉整块 `CHECK-IN RULES`、frontmatter 的三个打卡字段和 `check-in` 标签、整个 `## Check-in` 节；
  `If one of the four topics` → `If one of the three topics`；`Connect the four parts` → `Connect the three parts`；两节引用的 `Part 3`、`Part 4` 改成 `Part 2`、`Part 3`。

## 加个人背景

用户给了目标、计划或限制时，在开始 Prompt 第三段（`The most important goal is …`）后面插一块：

```
ABOUT ME

- My goal: ...
- My plan or daily targets: ...
- Things you should be careful about: ...
```

并在结束 Prompt 的 `CHECK-IN RULES` 开头插同样内容，标题写 `My context:`，再加一条 `Compare what I did with my plan and targets in Coach Advice.`。
开始 Prompt 的 check-in note 那条改成 `based on what I actually reported and on ABOUT ME`。

要记体重：frontmatter 加 `weight_kg: X.X`，`### Exercise and Sleep` 表加一行 `| Weight | ... | ... |`，
`CHECK-IN RULES` 加 `If I reported my weight, calculate how much I have lost since my starting weight and how much is left to my goal.`（起点和目标写在背景里）。

**个人背景是私人信息**：只写进用户自己工作区里的那两份 Prompt，不进任何公开的地方。健康类的背景（体重、病史、用药）尤其不要出现在回报以外的任何位置。

## 打卡评分（可选）

用户有明确的每日目标时，可以给打卡打个分。在结束 Prompt 的 `CHECK-IN RULES` 后面加：

```
CHECK-IN SCORE RUBRIC (0–10: five checks, 0–2 points each)

1. <check 1>: 2 = <fully met>; 1 = <partly met>; 0 = <not met, or not reported>.
2. ...
5. ...

Score only with evidence from this conversation. An item that was not reported gets 0 points and the evidence `Not reported`, so that I remember to report it next time.
```

frontmatter 加 `checkin_score: "X/10"`，`### Coach Advice` 前面加一节：

```
### Check-in Score

**Score:** X/10

| Check | Points | Evidence |
|---|---:|---|
| ... | X/2 | ... |
```

健康打卡的五项可以这样定（数字从用户的背景里来）：饮食在计划内、饮料（水够不够、有没有含糖饮料和酒）、运动达标、喝水量、晚上不吃东西且按时睡。

## 早上讲昨天

- 开始 Prompt：`FOUR PARTS` 列表第 1 条换成 `What I did yesterday`，第 3 条换成 `My biggest progress or contribution yesterday`，第 2、4 条不用改；
  Part 1 问题换成 `“Please tell me about yesterday from beginning to end. Take your time, and say ‘I've finished this part’ when you are done.”`，
  Part 2 问题里的 `What did you eat and drink` 换成 `What did you eat and drink yesterday`，Part 3、Part 4 问题里的 `today` 换成 `yesterday`；
  `ENDING` 第 1 条 `my day` 不用改，第 4 条 `for tomorrow` → `for today`。
- 结束 Prompt：`DATE` 那段换成 `Use yesterday's date in the Asia/Shanghai time zone (UTC+8), unless I said I was describing a different day.`
- 二级标题不改（还是 `## What I Did Today`）——入库和看板靠固定标题识别。
- `speaking.json` 的 `describe_day` 改成 `yesterday`。

## 时区

结束 Prompt `DATE` 段里的 `Asia/Shanghai time zone (UTC+8)` 换成用户的时区，`speaking.json` 的 `timezone` 一起改。

## 母语不是中文

- 开始 Prompt：`WHEN I NEED HELP` 里三句中文示例换成用户的语言；`one very short explanation in Chinese` 和 `If I use Chinese because …` 里的 Chinese 换掉。
- 结束 Prompt：`a short Chinese meaning`、`Write the Coach Advice in Chinese`、`Use short Chinese explanations` 里的 Chinese 换掉；
  新词表表头 `Chinese meaning` 换成 `<Language> meaning`；Coach Advice 里的 `做得好`、`明天调整` 换成用户的语言。
- 工作区：`language-bank.md` 表头那一列同步改名；`AGENTS.md` 里复习卡模板翻成用户的语言。

## 别改的

- 「讲完一整段才整段润色」「用自己的话再说一遍」「只挑一两处」「不追问」「不编造」——这是这套流程练得出东西的原因。
- 别让它边说边纠错。
- 结束 Prompt 的输出格式：一行 `FILE_PATH` + 一个代码块、固定的二级标题、frontmatter 的 `date` 和评分字段。入库和看板都靠它。
