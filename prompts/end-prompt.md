# 结束 Prompt

讲完四段后**退出语音，但留在同一个对话里**，把下面代码块里的内容整段贴进去。

它会输出一行 `FILE_PATH: journal/YYYY/YYYY-MM-DD.md` 和一个 Markdown 代码块。整段复制发给你的 agent，说「入库」；
没有 agent 的话，自己把代码块里的内容存成那个路径的 `.md` 文件就行。

````text
Please create my English journal and speaking review from the voice conversation in THIS SAME CHAT.

Do not ask me any more questions.

DATE

Use the date of the day I described, in the Asia/Shanghai time zone (UTC+8). Usually that is today. If I said I was describing yesterday or another day, use that day's date.

ACCURACY RULES

- Use only information that I actually provided.
- Do not invent activities, achievements, problems, emotions, quotations, plans, corrections, vocabulary-learning moments, foods, amounts, exercise, or sleep times.
- Preserve my original meaning and personality.
- Use the polished versions developed during our speaking practice.
- Keep the English natural, clear, and appropriate for my current level.
- Do not make it sound like a formal essay or use unnecessarily advanced vocabulary.
- Voice transcripts may contain transcription errors. Fix an error only when the intended meaning is clear.
- Only put something under “What I said” when the original wording is supported by the transcript.
- If one of the four topics was not discussed, write “Not discussed” instead of inventing content.

NEW LANGUAGE RULES

- Identify the words, phrases, collocations, fixed usage, preposition patterns, and sentence patterns that were genuinely new or unfamiliar to me during this session.
- Include expressions that you explicitly taught me, that I asked how to say, or that I learned through a correction.
- Do not fill the section with ordinary vocabulary just to reach a target number.
- Include fewer items when only a few were genuinely learned.
- Preserve required prepositions and grammar as part of the learning item. For example: `be proud of`, not only `proud`; `want to + verb`, not only `want`.
- Prefer reusable spoken English that I can apply in future conversations.
- Give every item a short Chinese meaning, its fixed usage or pattern, and a personal example based on my actual day.

CHECK-IN RULES

- Use only the meals, drinks, exercise, sleep, and body signals that I actually reported in Part 2 or anywhere else in this chat.
- Never guess numbers. In the frontmatter, write `null` for anything I did not report. In the document, write `Not reported`.
- In the frontmatter, write plain numbers without units or commas, for example `exercise_minutes: 30`, `steps: 8500`, `sleep_hours: 7.5`.
- Calorie numbers are rough estimates for typical portions. Mark every estimate with `≈`. Write `?` when the portion is too unclear to estimate.
- Write the Coach Advice in Chinese so it is easy to act on, but keep useful English words, such as food names and ordering phrases, in English.
- Coach Advice must be specific to what I actually ate and did. Give at most three points. Do not repeat generic advice.
- You are not a doctor. Do not tell me to change or stop any medicine. If I reported chest pain, dizziness, fainting, or a hot, red, swollen, or very painful joint, put a short reminder to rest and contact a doctor at the top of Coach Advice.
- If the check-in was not discussed at all, set every check-in field in the frontmatter to `null` and write `Not discussed` under `## Check-in`.

SPEAKING RATING RULES

- Give this session an evidence-based speaking rating using the same scale every day.
- Give an overall score from 1.0 to 10.0, using one decimal place, and a broad estimated CEFR level such as A1, A2, A2+, B1, B1+, B2, C1, or C2.
- Score these four dimensions from 1.0 to 10.0: Grammar Accuracy, Vocabulary and Expression, Fluency and Organization, and Communication Effectiveness.
- Base every score only on evidence from this conversation, including my original answers, retries, corrections, and how independently I communicated my ideas.
- Do not reward advanced subject matter by itself, and do not lower the score merely because the topic was difficult.
- Use this stable scale: 9–10 = consistently natural and highly independent; 7–8 = clear and independent with occasional errors; 5–6 = understandable but developing, with recurring errors or support needed; 3–4 = frequent breakdowns and substantial support needed; 1–2 = very limited evidence of usable speech.
- The overall score should reflect the four scored dimensions, not pronunciation.
- Assess Pronunciation only if you actually have reliable audio evidence from this session. If you only have a transcript or cannot reliably access the audio, write `Not assessed — no reliable audio evidence` and do not guess.
- Keep the rating constructive and calibrated. Give one short piece of evidence for each dimension and one concrete action needed to reach the next level.

OUTPUT FORMAT

First output:

FILE_PATH: journal/YYYY/YYYY-MM-DD.md

Then output exactly one Markdown code block containing the complete document. Do not write anything else outside the file path and Markdown code block. Keep every section heading exactly as shown below, even if I described yesterday.

Use this structure:

```markdown
---
date: YYYY-MM-DD
tags:
  - daily-journal
  - speaking-practice
  - check-in
source: ChatGPT Live
speaking_rating: "X.X/10"
estimated_cefr: "A2+"
rating_basis: transcript-and-coaching
exercise_minutes: X
steps: X
sleep_hours: X.X
---

# YYYY-MM-DD — A Short Title

## What I Did Today

Write a clear first-person account using the final polished version from Part 1.

## Check-in

### My Check-in Report

Use the final polished version from Part 2.

### Food and Drinks

| Meal | What I ate and drank | Est. kcal | Notes |
|---|---|---:|---|
| Breakfast | ... | ≈ ... | ... |
| Lunch | ... | ≈ ... | ... |
| Dinner | ... | ≈ ... | ... |
| Snacks & drinks | ... | ≈ ... | ... |
| **Total** | | **≈ ...** | |

Write `Not reported` for any meal I did not mention.

### Exercise and Sleep

| Item | Amount | Notes |
|---|---|---|
| Exercise | ... | ... |
| Steps | ... | ... |
| Sleep | ... | ... |

### Coach Advice

1. **做得好：** ...
2. **明天调整：** ...
3. **明天调整：** ...

**Tomorrow's check-in focus:** One small, specific action.

## Biggest Progress or Contribution

Use the final polished version from Part 3.

## Reflection and Problems

Use the final polished version from Part 4.

## Today in Summary

Connect the four parts into a concise, coherent first-person reflection without adding new information.

## Better English

| What I said | A natural version | What I can learn |
|---|---|---|
| ... | ... | ... |

Include up to eight corrections that are genuinely supported by the conversation. Use short Chinese explanations when helpful.

## Polished Sentences to Practise

List five to eight natural sentences from today that would be useful to practise aloud.

## New Vocabulary and Fixed Phrases

| Item | Type | Chinese meaning | Fixed usage or pattern | Personal example |
|---|---|---|---|---|
| ... | word / phrase / collocation / pattern | ... | ... | ... |

Include only language that was genuinely new or unfamiliar to me in this session. Keep required prepositions and grammatical structures inside the item.

## Tomorrow

Include only plans or intentions I actually mentioned. Otherwise write `Not discussed`.

## Speaking Review

### What Improved Today

List the three most important improvements.

### Recurring Problems

Identify recurring grammar, vocabulary, or sentence-structure problems supported by the conversation.

### Next Speaking Focus

Give one small and specific focus for my next session.

## Speaking Rating

**Overall:** X.X/10

**Estimated CEFR:** A2+

**Evidence basis:** State briefly what evidence was actually available, such as the voice conversation, transcript, original answers, retries, and corrections.

| Dimension | Score | Evidence |
|---|---:|---|
| Grammar Accuracy | X.X/10 | One brief observation supported by this session. |
| Vocabulary and Expression | X.X/10 | One brief observation supported by this session. |
| Fluency and Organization | X.X/10 | One brief observation supported by this session. Do not claim to know speaking speed from text alone. |
| Communication Effectiveness | X.X/10 | One brief observation supported by this session. |

**Pronunciation:** X.X/10 with brief audio-based evidence, or `Not assessed — no reliable audio evidence`.

**To reach the next level:** Give one specific, realistic action for the next speaking session.

## Conversation Notes

Summarize the main content. Clearly treat this as a summary, not a verbatim transcript.
```
````

## 输出长什么样

一篇完整的例子（虚构的）在 [../examples/journal-example.md](../examples/journal-example.md)。固定的二级标题依次是：

What I Did Today · Check-in · Biggest Progress or Contribution · Reflection and Problems · Today in Summary ·
Better English · Polished Sentences to Practise · New Vocabulary and Fixed Phrases · Tomorrow · Speaking Review ·
Speaking Rating · Conversation Notes

frontmatter 里的 `date`、`speaking_rating`、`estimated_cefr` 和三个打卡数字（没说就是 `null`）是给入库和看板读的。

## 每一块在干什么

| 块 | 作用 |
|---|---|
| THIS SAME CHAT | 必须在刚才练习的那个对话里贴，它要读整段语音对话 |
| Do not ask | 不再追问，直接出文件 |
| DATE | 用你讲的那一天的日期：讲的是昨天就记昨天 |
| ACCURACY RULES | 只写你说过的；用练习里润色过的版本；没聊到的写 Not discussed；转写错了只在意思明确时才改 |
| NEW LANGUAGE RULES | 只收真正新学的：它教的、你问的、纠错时学到的；介词和句型算条目的一部分；每条带中文意思、用法和你今天的例句——这张表直接进词库，复习卡也从这里出题 |
| CHECK-IN RULES | 数字不猜，没说就 `null` / Not reported；热量只是估计、标 ≈；Coach Advice 用中文、最多三条、针对你今天实际做的 |
| SPEAKING RATING RULES | 1–10 分的固定尺度 + CEFR + 四个维度各一句证据；不因话题难而加分或减分；没有可靠音频就不评发音 |
| OUTPUT FORMAT | 一行 FILE_PATH + 一个代码块、二级标题固定——agent 能直接入库，看板能直接解析 |
