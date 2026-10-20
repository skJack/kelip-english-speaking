# kelip-english-speaking

**简体中文** | [English](README.en.md)

用 AI 练英语口语，顺手把每一天写成英文日记——一箭双雕。

这是一个 skill：把仓库交给你的 AI Agent，它会帮你把整套流程搭起来。核心是两段 Prompt，不想搭系统也可以直接复制来用。

```
开始 Prompt ─▶ ChatGPT 语音（GPT Live）按四段讲 ─▶ 结束 Prompt ─▶ 一篇 Markdown 英文日记
                                                                    │ 发给 Agent：「入库」
                                                                    ▼
                    日记按日期存档 · 新表达去重进词库 · 白天定时推复习卡 · 傍晚没交就提醒一次
```

## 两段 Prompt（核心）

| | 在哪贴 | 它管什么 |
|---|---|---|
| [开始 Prompt](prompts/start-prompt.md) | 每天在 ChatGPT 新建对话，贴进去再开语音 | 让它当口语教练：每天固定讲四段（做了什么 / 打卡 / 最大进展 / 反思）；你讲完一整段它才整段润色，你用自己的话再说一遍，它只挑一两处 |
| [结束 Prompt](prompts/end-prompt.md) | 讲完退出语音，**在同一个对话里**贴 | 把刚才的对话整理成一篇 Markdown 日记：润色后的四段、纠错表、真正新学的词和句型、口语评分 |

几条设计，都是每天练、改了几个月留下来的：

- **讲的时候不打断。** 讲完一整段再改，人才敢开口。
- **整段润色，再自己说一遍。** 学到的是一段连起来的说法，不是零碎的单句纠错；马上再说一遍，练的是输出。
- **只挑一两处。** 一次纠十处，一处也记不住。
- **不追问，不变成采访。** 你只管连着说。
- **卡住了随时用中文问「这个怎么说」。** 它答完让你接着讲。
- **不编造。** 日记里每一句都来自你说过的话；没聊到的就写 Not discussed。
- **新词只收真正新学的。** 它教的、你问的、纠错时学到的，带上介词和句型（`be proud of`，而不是 `proud`）。

第二段默认是健康打卡（吃喝、运动、睡眠），可以换成任何你想天天记的事——学习、练琴……改法见 [references/customize.md](references/customize.md)。

## 两种用法

**只要 Prompt**：打开上面两个文件，复制代码块里的内容。每天：新建对话 → 贴开始 Prompt → 开语音讲四段 → 退出语音 →
同一个对话里贴结束 Prompt → 把生成的 Markdown 存起来。

**让 Agent 把整套搭起来**：不知道 skill 怎么装也没关系——把这个 GitHub 链接直接甩给你的 Agent，让它自己装好，再跟它说「帮我搭一个英语口语练习系统」。两句可以一起发：

```
帮我装好这个 skill：https://github.com/skJack/kelip-english-speaking
装好后帮我搭一个英语口语练习系统。
```

它会一次问你几个问题（工作区放哪、早上还是晚上练、第二段记什么、复习卡几点发……），然后：

- 按你的回答生成你自己的两段 Prompt；
- 建好工作区：日记目录、词库，和一份写清全部规则的 `AGENTS.md`——以后换任何 agent 都能接着用；
- 设好定时任务：白天每 2 小时一张复习卡、每张 3 条；每天 18:00 检查昨天的日记交了没有，没交提醒一次。

之后每天讲完，把结束 Prompt 的输出发给它说「入库」：日记按日期存好，新表达去重进词库，再告诉你今天的评分和新学了什么。

复习卡长这样，先出题，答案在下面：

```
☀️ 复习卡（先想一想，答案在下面）

1. 用完了、耗尽了，用英语怎么说？
2. 把时间往后推、推迟，怎么说？
3. 摸到了某件事的窍门，怎么说？

---

答案

1. `run out of something`
   你的例句：We ran out of time.
   提示：run out of 后面接名词。

2. `push something back`
   你的例句：My part was pushed back to Friday.
   提示：说「被推迟到某天」用 be pushed back to + 时间。

3. `get the hang of something`
   你的例句：I finally got the hang of the new data tool.
   提示：后面接名词或 doing。

挑一两个造句发我，我帮你改，再更新复习记录。
```

回它句子，它帮你改，再按 1 → 3 → 7 → 14 → 30 天排下一次复习；想不起来就明天再考。

## 安装

最省事的办法：把这个仓库的链接发给你的 Agent，说「帮我装好这个 skill」，它会照下面的步骤自己装。

**Claude Code**：

```bash
git clone https://github.com/skJack/kelip-english-speaking.git ~/.claude/skills/kelip-english-speaking
```

然后说「帮我搭一个英语口语练习系统」。

**Codex / Cursor / 其他 Agent**：clone 下来，让它读 `SKILL.md` 照着做。仓库根目录有一份 `AGENTS.md`，会自动读它的 agent 不用额外配置。

**云端个人 Agent**（我自己用的是 Grok Bot 里的一个 bot）：把仓库地址发给它，让它读 `SKILL.md`，搭在它的云端工作目录里。
好处是电脑合上了也照样收复习卡和提醒。

没有依赖，不用装任何东西。

## 隐私

仓库里只有流程和 Prompt，**没有任何人的日记**。你的日记、词库、打卡数据只在你自己的工作区里：工作区自带的 `.gitignore` 把它们全部排除，
agent 也被要求不把它们传到任何公开的地方。打卡要是记健康，你给教练的个人背景（目标、身体情况）也只写在你自己那份 Prompt 里。

## 文件

| 路径 | 是什么 |
|---|---|
| `SKILL.md` | 给 agent 的流程：第一次怎么搭、日常请求怎么分流 |
| `AGENTS.md` | 一页指路，给会自动读它的 agent |
| `prompts/start-prompt.md` | 开始 Prompt + 每一块在干什么 |
| `prompts/end-prompt.md` | 结束 Prompt + 输出格式 |
| `references/customize.md` | 换第二段主题、加个人背景、早上讲昨天、改时区和母语 |
| `references/dashboard.md` | （可选）本地看板的页面清单 |
| `templates/AGENTS.md` | 复制进你工作区的日常规则：入库、词库、复习卡、提醒、周总结 |
| `templates/language-bank.md` | 空词库 |
| `templates/speaking.json` | 设置的默认值 |
| `templates/gitignore` | 工作区的 `.gitignore` |
| `examples/journal-example.md` | 结束 Prompt 生成的一篇日记长什么样（虚构的例子） |

## 相关

- [kelip-slide](https://github.com/skJack/kelip-slide)：单文件 HTML 讲解幻灯片
- [kelip-paper-reading](https://github.com/skJack/kelip-paper-reading)：让 AI Agent 带你精读一篇论文

## License

MIT
