# humanizer-asd-ste100

[![skills.sh](https://skills.sh/b/octavvartan/humanizer-asd-ste100)](https://skills.sh/octavvartan/humanizer-asd-ste100)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

An agent skill that makes AI write clear, human text. It uses the rules of **ASD-STE100 Simplified Technical English** and removes AI-writing patterns. It works for docs, answers, code comments, and commit messages in any language. English and Russian have extra rules.

[Русская версия ниже](#на-русском)

## What it does

- **Applies STE rules.** One word has one meaning. Active voice. Imperative steps. Max 20 words in a procedure sentence and 25 in a description. Max 3 nouns in a row. Correct WARNING and CAUTION format.
- **Removes AI patterns.** Chat wrappers, flattery, filler, buzzwords, "not just X, but Y", rule of three, generic conclusions, emoji and bold noise.
- **Adapts to the text.** It selects one of three levels:

  | Level | For | Rules |
  | --- | --- | --- |
  | Strict | Procedures, runbooks, installation steps, safety text, text for translation | Full STE, hard word limits |
  | Standard (default) | Answers, explanations, docs, emails, PRs, code comments, commits | Approximately 80% STE, natural tone |
  | Light | Personal or creative text, "keep my voice" | Removes AI patterns only |

- **Supports Russian.** Канцелярит, причастные и деепричастные обороты, цепочки существительных, форма «вы», «ёлочки».
- **Keeps what must not change.** Code, commands, identifiers, quotes, UI labels, and the language of the source. It does not invent facts.

## Install

**Any agent** (Claude Code, Codex, Cursor, Gemini CLI, GitHub Copilot, OpenCode, Windsurf, and [70+ more](https://github.com/vercel-labs/skills/blob/main/docs/agents.md)):

```bash
npx skills add octavvartan/humanizer-asd-ste100
```

Options:

```bash
# Install for all your projects (user level)
npx skills add octavvartan/humanizer-asd-ste100 -g

# Install for one agent only
npx skills add octavvartan/humanizer-asd-ste100 -a claude-code
npx skills add octavvartan/humanizer-asd-ste100 -a codex
```

**Claude.ai.** Make a ZIP file of the `skills/humanizer-asd-ste100` folder. Upload it in the Skills section of the Claude settings.

**ChatGPT.** Create a project or a custom GPT. Upload `skills/humanizer-asd-ste100/SKILL.md` as a file. Add this instruction: `Follow the rules in SKILL.md for every text you write.`

**Manual installation.** Copy the `skills/humanizer-asd-ste100` folder into the skills folder of your agent, for example `.claude/skills/` or `.agents/skills/`.

### Use it for all text

An agent loads a skill when the task matches the skill description. To apply the rules to all text, add this line to `CLAUDE.md`, `AGENTS.md`, or your custom instructions:

```text
Use the humanizer-asd-ste100 skill for every text you write: answers, docs, code comments, and commit messages.
```

## Usage

```text
Rewrite this procedure in strict STE: ...
Remove AI patterns from this release note: ...
Write a commit message for this diff.
Перепиши по STE: ...
Убери признаки ИИ из текста: ...
```

## Examples

**English, Strict level.**

Before:

> Sure! In order to ensure that the backup has been completed successfully, the log file should be checked, and after that the service can be restarted. Let me know if you need anything else! 😊

After:

> 1. Examine the log file to make sure that the backup is complete.
> 2. Restart the service.

**Russian, Standard level.**

Before:

> Отличный вопрос! В целях обеспечения корректной работы системы необходимо осуществить проверку конфигурационного файла, после чего производится перезапуск сервиса.

After:

> Чтобы система работала правильно, проверьте конфигурационный файл. Затем перезапустите сервис.

## Evals

[`evals/evals.json`](skills/humanizer-asd-ste100/evals/evals.json) has 20 test cases: English, Russian, German, code comments, commit messages, and scope limits. Each case has a prompt, the trap that a model falls into without the skill, the expected output, and assertions.

To test the skill, run each prompt two times: with the skill and without it. Then grade both outputs against the assertions.

## Repository structure

```text
skills/humanizer-asd-ste100/
├── SKILL.md            # Rules for the agent
└── evals/evals.json    # Test cases
```

## Source and disclaimer

The rules come from [ASD-STE100 Issue 9](https://www.asd-ste100.org/) (2025), Simplified Technical English. ASD-STE100 is a registered trademark of ASD. This project is an independent writing aid. ASD does not endorse it. It does not contain the STE dictionary. The full standard is [free to download](https://www.asd-ste100.org/assets/files/ASD-STE100_ISSUE9.pdf).

The skill format follows [samber/cc-skills: humanizer-en-asd-ste100](https://github.com/samber/cc-skills/tree/main/skills/humanizer-en-asd-ste100).

## License

[MIT](LICENSE)

---

## На русском

Скилл для ИИ-агентов. Агент пишет понятный текст по правилам ASD-STE100 (Simplified Technical English) и не оставляет признаков ИИ. Скилл работает для документации, ответов, комментариев в коде и сообщений коммитов. Работает на любом языке. Для английского и русского языков есть отдельные правила.

### Что делает скилл

- Применяет правила STE: одно слово — одно значение, действительный залог, повелительное наклонение в инструкциях, до 20 слов в шаге и до 25 слов в описании.
- Убирает признаки ИИ: «Отличный вопрос!», «Важно отметить», «не просто X, а Y», «играет ключевую роль», «В заключение», эмодзи и лишний жирный шрифт.
- Выбирает уровень строгости: строго для инструкций, примерно на 80% для ответов и комментариев, мягко для личных текстов.
- Для русского языка убирает канцелярит, длинные причастные обороты и цепочки существительных. Использует форму «вы» и «ёлочки».
- Не меняет код, команды, названия и язык исходного текста. Не придумывает факты.

### Установка

```bash
npx skills add octavvartan/humanizer-asd-ste100
```

Для всех проектов добавьте флаг `-g`. Для одного агента добавьте `-a claude-code` или `-a codex`.

Чтобы агент применял правила ко всем текстам, добавьте строку в `CLAUDE.md` или `AGENTS.md`:

```text
Use the humanizer-asd-ste100 skill for every text you write: answers, docs, code comments, and commit messages.
```

### Примеры запросов

```text
Перепиши по STE: ...
Убери признаки ИИ из текста: ...
Напиши сообщение коммита для этих изменений.
```
