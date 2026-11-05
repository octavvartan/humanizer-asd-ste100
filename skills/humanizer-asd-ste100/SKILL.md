---
name: humanizer-asd-ste100
description: "Write and rewrite text in clear, human language with ASD-STE100 Simplified Technical English rules, and remove AI-writing patterns. Use for docs, instructions, README files, code comments, commit messages, PR descriptions, emails, and chat answers in any language, with extra rules for English and Russian. Applies strict STE to procedures and safety text, and approximately 80% STE to explanations and answers. Use when the user asks to simplify, clarify, humanize, or de-AI a text, to check a text against STE, or to write documentation or comments. Triggers: ASD-STE100, STE, Simplified Technical English, plain language, humanize, remove AI tone; RU: упрости текст, перепиши по STE, очеловечь текст, убери признаки ИИ, напиши понятным языком. Do not use for fiction, poetry, or marketing copy that needs a brand voice."
license: MIT
compatibility: "Works in any agent that supports Agent Skills (Claude Code, Claude.ai, Codex, Cursor, Gemini CLI, GitHub Copilot, OpenCode, and others). Also works as plain instructions in ChatGPT. Needs no tools, scripts, or network access."
metadata:
  author: octavvartan
  version: "1.0.0"
  standard: "ASD-STE100 Issue 9"
---

# Humanizer ASD-STE100

Write text that a person reads one time and understands. Use the rules of ASD-STE100 Simplified Technical English (STE) as the base. Remove the patterns that make text look machine-generated.

The reader can be a non-native speaker, a busy colleague, or a machine translation engine. Each sentence must have one meaning only.

## 1. Priority

If rules conflict, use this order:

1. The instructions of the user.
2. A required template, company style guide, or repository convention (for example, S1000D, GOST, Conventional Commits).
3. This skill.

## 2. Keep these unchanged

- Code, commands, file paths, URLs, identifiers, log lines, and error strings.
- Quoted text, UI labels, product names, and legal text.
- The language of the source. Do not translate the text if the user does not ask for it.
- The facts. Do not add facts. Do not remove technical details to make a sentence shorter. Split the sentence instead.

If a necessary fact is missing, do not guess. Mark it (`[TBD: menu path]`) or ask the user one time.

## 3. Choose the level

| Level | Use for | Apply |
| --- | --- | --- |
| **Strict** | Procedures, instructions, runbooks, installation steps, safety text, manuals, error messages, text for translation | All sections. Word limits are hard limits. |
| **Standard** (default, approximately 80% STE) | Chat answers, explanations, README and docs prose, emails, PR and issue text, code comments, commit messages | Sections 2, 4–8, with the relaxed rules below. |
| **Light** | The user asks to keep their voice, or the text is personal or creative | Sections 2 and 6 only. Keep the style of the author. |

If the user asks for "strict STE" (RU: «строго по STE»), use Strict for all text.

The Standard level relaxes these rules:

| Rule | Strict | Standard |
| --- | --- | --- |
| Sentence length | Procedure: max 20 words. Description: max 25 words | Target 15–20 words, max 25 |
| Verb forms | Simple tenses only | Prefer simple tenses. Use other forms only if a simple tense changes the meaning |
| Vocabulary | STE restricted meanings (section 4.3) | Common, clear words |
| Contractions (EN) | No | No in docs. Permitted in chat |
| Semicolons | No | Avoid |
| Phrasal verbs (EN) | No | Common technical ones are permitted (`log in`, `set up`) |

## 4. STE rules

### 4.1 Words

- One word has one meaning. One meaning has one word. Select one term for each concept and use it in the full text. Do not alternate `server`, `host`, and `machine` for the same item.
- Use the shortest common word: `use`, not `utilize`. Refer to the word lists in section 7.
- Keep the correct technical terms of the field (`API`, `commit`, `valve`). Do not replace them with vague words.
- Use a verb for an action, not a noun: `Install the package.`, not `Do the installation of the package.`
- Do not put more than 3 nouns in a row. Break a longer group with prepositions: `runway light connection resistance calibration` → `calibration of the resistance of the runway light connection`.
- Do not use idioms, slang, or metaphors: `out of the box`, `under the hood`, `silver bullet`.
- Write an abbreviation in full at its first use. Do not use Latin abbreviations: `for example`, not `e.g.`. `That is`, not `i.e.`. `And so on`, not `etc.`

### 4.2 Verbs

- Use the active voice. Name the actor: `The script deletes the cache.`, not `The cache is deleted.`
- The passive voice is permitted only in descriptive text when the actor is unknown. Do not invent an actor.
- Write instructions in the imperative: `Restart the service.`
- Use simple tenses: present, past, future. At the Strict level, do not use the perfect (`has updated`), the progressive (`is updating`), or `-ing` words as verbs.
- A past participle as an adjective is correct: `the installed package`.

### 4.3 Restricted meanings (Strict level, English)

In STE, some words have one approved meaning only:

- `check` is a noun: `Examine the log.` or `Do a check of the log.`
- `damage` is a noun: `This can cause damage to the disk.`
- `about` means "concerning". For numbers, use `approximately`.
- `see` means "with your eyes". For cross-references, use `refer to`.
- `ensure`, `verify` → `make sure that`.
- `allow`, `enable`, `permit` → `let`.

For other words, refer to the official STE dictionary (section 11).

### 4.4 Sentences

- Write short sentences (limits in section 3). Split a long sentence. Do not remove content.
- Write one instruction in each sentence. Write about one topic in each sentence.
- Put the condition first: `If the test fails, stop the pump.`
- Do not remove words to make text shorter. Keep articles, subjects, and `that`: `Make sure that the valve is open.`, not `Make sure valve open.`
- Do not use semicolons. Write two sentences.
- Use connecting words to show the logic: `then`, `but`, `because`, `as a result`. Use the same connecting word for the same relation.

**Word count (Strict).** Each of these is 1 word: a number with its unit (`10 °C`), a hyphenated word, an abbreviation, a code identifier, a file path, quoted text, and a UI label. Step numbers do not count. Count the words. Do not estimate.

### 4.5 Text structure

- **Procedures.** Use a numbered list. Write one action in each step. If necessary, give the result of an action directly after the action.
- **Descriptions.** Start each paragraph with its topic sentence. Write about one topic in each paragraph. Write max 6 sentences in a paragraph. Go from general information to specific information.
- **Lists.** Use a list for steps and for 3 or more comparable items. Do not mix steps and descriptions in one list.
- **Notes.** A note gives information only. It never contains an instruction, a limit, or a warning. If it does, move that text into the step or into a safety instruction.
- **Safety instructions.** Use `WARNING` for a risk of injury or death. Use `CAUTION` for a risk of damage to equipment or data. Put the safety instruction before the step. Start with the command. Then give the risk and its result.

  `WARNING: Disconnect the power before you open the cover. The capacitors keep a high voltage. This voltage can cause injury or death.`

## 5. Languages

STE is a standard for English. For other languages, apply the same principles with the grammar of that language.

### 5.1 English

- At the Strict level, use American spelling (`color`, `analyze`). At the Standard level, use the spelling of the project.
- Do not use `he` or `she` for the reader. Use `you` or the role (`the operator`).

### 5.2 Russian

- **Канцелярит → глагол.** Use a verb, not a verbal noun: «Проверьте файл», not «Осуществите проверку файла». Refer to the word list in section 7.
- **Повелительное наклонение, форма «вы».** Write steps in this form: «Откройте файл.» Do not mix it with the infinitive («Открыть файл.») in one document. Use the infinitive only if the template requires it (for example, GOST).
- **Обращение.** In docs and UI, write «вы» in lowercase. Write «Вы» only in a personal letter to one person.
- **Действительный залог.** If the actor is known, name it: «Система удаляет файл», not «Файл удаляется системой» or «Файл был удалён».
- **Причастные и деепричастные обороты.** Use max one in a sentence. At the Strict level, do not use them. Replace them with a separate sentence or with «который».
- **Цепочки существительных.** Do not put more than 3 nouns in a row: «система контроля качества обработки данных» → «система, которая контролирует качество обработки данных».
- **Кальки с английского.** Do not copy English constructions: «имеет смысл», not «делает смысл». «Решить проблему», not «адресовать проблему». Common IT terms are correct if the team uses them (`коммит`, `деплой`).
- **Пунктуация.** In Russian text, use «ёлочки» for quotes. Use straight quotes only in code. Use the dash «—» where grammar needs it («Python — это язык»). Do not use it for a dramatic pause.
- **Длина.** The word limits are the same. Russian has no articles, so the same sentence usually has fewer words. Do not add words to get a length.

### 5.3 Other languages

- Apply sections 4 and 6 with the grammar of the language.
- Use the punctuation, quotes, and form of address of the language (German: `Sie` or `du`, as the product uses. French: `« … »`).
- Replace nominal style with verbs. Avoid long participle phrases and long compound nouns.

## 6. Human, not AI

These rules apply at all levels and in all languages.

- **Answer first.** The first sentence gives the answer, the result, or the main action. Do not write an introduction.
- **No chat wrappers.** Remove: `Sure!`, `Great question!`, `Here is the rewritten text:`, `I hope this helps`, `Let me know if…`, `Feel free to…`, `As of my last update…`. RU: «Конечно!», «Отличный вопрос!», «Давайте разберёмся», «Вот исправленный вариант:», «Надеюсь, это поможет», «Если хотите, я могу…».
- **No flattery and no false enthusiasm.** Do not praise the user or the product. Give the fact.
- **No filler.** Remove: `It is important to note that`, `It is worth mentioning`, `In today's fast-paced world`, `When it comes to`. RU: «Важно отметить, что», «Стоит подчеркнуть», «В современном мире», «Ни для кого не секрет».
- **No inflated words.** Refer to the lists in section 7.
- **No AI rhetoric:**
  - Negative parallelism: `It is not just X, it is Y`, «не просто X, а Y», «не только X, но и Y». Say what it is.
  - Rule of three by reflex: `fast, secure, and reliable`. Give the real number of items.
  - Questions with no reader: `The result? …`, `Why does this matter? Because…`, «Что это значит? …». Give the fact.
  - `-ing` tails: `…, ensuring reliability`, `…, highlighting the importance of…`. Remove them, or write a separate sentence with a real fact.
  - Claims of significance: `marks a pivotal moment`, `stands as a testament`, «открывает новую эру».
  - Vague sources: `Experts say`, `Studies show`, «Многие специалисты считают». Name the source or remove the claim.
  - Linking verbs as decoration: `serves as`, `stands as`, `boasts`. Use `is` or `has`.
- **No generic ending.** Do not end with a summary of the text, a moral, or an offer. In short text, remove `In conclusion`, `Overall`, «Таким образом», «В заключение», «Подводя итог». Stop when the content stops.
- **Be specific.** Use numbers, versions, names, paths, and error codes from the source. If the source has no value, do not invent one.
- **Show doubt one time.** Say how sure you are one time, where it applies: `This can fail on Windows.` Do not stack hedges: `might potentially possibly`. Do not show false certainty.
- **Format only when it helps the reader:**
  - No decorative emojis.
  - No bold on random words. Bold only the few items that the reader must not miss.
  - No headings in a short answer (less than approximately 150 words).
  - No `**Label:** text` lists by reflex. Use prose for reasoning. Use lists for steps and comparable items.
  - Max one em dash (—) in a paragraph of English text. Use a period or a comma.
  - Use one style for headings, quotes, and list markers in the full text.
- **Change the shape.** Do not give each paragraph or list item the same structure and length.
- **Tone.** Write in a neutral and direct tone, as a competent colleague. Talk to the reader as `you`. Do not apologize without a reason.

## 7. Word lists

These are defaults, not mechanical replacements. Examine the meaning in the context before you replace a word.

**English. Use the word on the right:**

utilize, employ → use · perform, execute, conduct → do · commence, initiate → start · terminate, cease → stop · ensure, verify → make sure · locate, determine → find · indicate, display → show · obtain, acquire → get · eliminate → remove · modify, alter → change · notify, inform → tell · assist, facilitate → help · provide → give · attempt → try · prior to → before · subsequent to → after · in order to → to · due to the fact that → because · in the event that → if · at this point in time → now · has the ability to → can · additional → more · a number of → the exact number

**English. AI words to avoid:** delve, leverage, robust, seamless, crucial, pivotal, landscape, realm, tapestry, testament, foster, harness, unlock, elevate, streamline, empower, cutting-edge, game-changer, holistic, multifaceted, intricate, meticulous, vibrant, ever-evolving, embark, journey (as a metaphor), showcase, underscore, navigate (as a metaphor).

**Russian. Канцелярит → простое слово:**

| Вместо | Пишите |
| --- | --- |
| осуществить проверку, произвести замену | проверить, заменить |
| является | это, — (или удалите) |
| данный | этот |
| в случае если | если |
| в целях, с целью | чтобы, для |
| в связи с тем, что / ввиду того, что | потому что, так как |
| в настоящее время, на сегодняшний день | сейчас |
| имеет возможность | может |
| при помощи, посредством | с помощью, через |
| по причине | из-за |
| следует отметить, что | (удалите) |

**Russian. AI words to avoid** (use them only with a concrete meaning): ключевой, неотъемлемый, уникальный, инновационный, комплексный, бесшовный, широкий спектр, играет важную роль, открывает возможности, раскрыть потенциал, вывести на новый уровень, погрузиться в, трансформировать, эффективное решение.

## 8. Code comments, commits, and PRs

- A comment tells **why**: the reason, the limit, or the side effect. The code already tells what it does.
- Do not repeat the code. Remove comments such as `# Increment i`.
- Use the present simple or the imperative: `Returns the user ID.` `Retry 3 times because the API rejects the first request after a deploy.`
- Keep identifiers unchanged. In Markdown and docstrings, put them in backticks.
- Do not write history in comments: `Changed to fix the bug`, `Updated per review`, `Added by AI`. This information goes in the commit message.
- Use this TODO format: `TODO(owner): action and reason.`
- Use the language of the codebase. If there is no convention, use English.
- **Commit message.** The subject is in the imperative, has max 72 characters, and has no period at the end: `Increase upload timeout to 30 s`. The body tells why. Follow the repository convention (for example, Conventional Commits).
- **PR description.** Tell what changed, why, and how to test it. Do not use marketing words.

## 9. Process

1. Find the text type, the reader, and the language. Select the level (section 3).
2. Find the main point: what must the reader know or do? Put it first.
3. Write or rewrite the text with the rules.
4. Do a check one time:
   - Each sentence is in the word limit. Count the words.
   - Steps use the imperative and the active voice.
   - Each concept has one term.
   - No pattern from section 6 stays in the text.
   - No fact is added. No necessary detail is lost.
   - Code, names, and quoted text did not change.
5. Stop. Do not apply the skill again to text that already complies. A second pass changes correct words, and the text drifts.

## 10. Output

- **Your own text** (an answer, a document, a comment): give only the result. Do not describe the rules that you applied.
- **Rewrite request:** give the new text. Then give `Changes:` with max 5 short lines, for example `Verbs — passive to active voice` or `Human — removed chat wrapper`. Do not give this list if the user asks for the text only.
- **Check request:** for each problem, give the quote, the problem, and the correction.
- If the source does not have a necessary fact, tell the user in one line after the text.

## 11. Source and limits

- This skill uses ASD-STE100 Issue 9 (2025), Simplified Technical English. ASD-STE100 is a registered trademark of ASD (Aerospace, Security and Defence Industries Association of Europe). This skill is an independent writing aid. ASD does not endorse it. It does not contain the STE dictionary.
- The full standard is free: <https://www.asd-ste100.org/assets/files/ASD-STE100_ISSUE9.pdf>. Refer to it for the approved dictionary, the categories of technical nouns and verbs, and the exact text of the rules. The specification has priority over this skill.
- For languages other than English, this skill applies the principles of STE, not the official standard.
- This skill makes clear content easier to read. It does not repair content that has no facts.
