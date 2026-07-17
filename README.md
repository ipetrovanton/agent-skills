# agent-skills

Набор скилов для ИИ-агентов (Claude Code, Codex, Windsurf, Cursor, OpenCode и любых
агентов, поддерживающих формат **Anthropic Agent Skills**).

Каждый скил — это папка внутри `skills/` с файлом `SKILL.md`. В начале файла — YAML-
фронтматтер с полями `name` и `description`, далее — инструкции для модели. Описания и
все созданные в этом репозитории скилы написаны на русском языке. Заимствованные
open-source скилы приведены в оригинальном виде с сохранением атрибуции и лицензий
(см. раздел «Атрибуция и лицензии» и файл [`NOTICE`](./NOTICE)).

## Список скилов

### Заимствованные (open-source)

| Скил | Назначение | Источник |
|------|-----------|----------|
| [`karpathy-guidelines`](./skills/karpathy-guidelines/SKILL.md) | 4 принципа LLM-кодинга: думать до кода, простота, точечные правки, проверяемые критерии успеха | [swarmclawai/andrej-karpathy-skills](https://github.com/swarmclawai/andrej-karpathy-skills) |
| [`deep-research`](./skills/deep-research/SKILL.md) | Глубокое многофазное исследование темы с отчётом и цитированием источников | [l8ntlabs/agent-skills](https://github.com/l8ntlabs/agent-skills) |
| [`humanizer`](./skills/humanizer/SKILL.md) | Убирает признаки ИИ-генерации из текста, делает его естественным | [blader/humanizer](https://github.com/blader/humanizer) |
| [`caveman`](./skills/caveman/SKILL.md) | Компрессия output-токенов: сверхкраткие ответы без потери сути | [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) |

### Созданные в этом репозитории

| Скил | Назначение |
|------|-----------|
| [`code-reviewer`](./skills/code-reviewer/SKILL.md) | Базовое ревью кода: стиль, корректность, безопасность, тесты |
| [`context-keeper`](./skills/context-keeper/SKILL.md) | Сохранение и восстановление контекста сессии (`.remember/`) |
| [`interrogator`](./skills/interrogator/SKILL.md) | Уточнение требований по принципу следователя, выявление скрытых требований |
| [`deep-code-review`](./skills/deep-code-review/SKILL.md) | Детальное ревью: поиск багов, снижение когнитивной нагрузки, нейминг, форматирование |
| [`plain-docs-writer`](./skills/plain-docs-writer/SKILL.md) | Документация простым языком для неспециалиста, гуманизация текста |
| [`research-writer`](./skills/research-writer/SKILL.md) | Фактура для статей и исследований: «Проблема → Диагноз → Решение → Итог», только реальные данные |
| [`database-expert`](./skills/database-expert/SKILL.md) | Проектирование схем, оптимизация запросов, миграции, индексы |
| [`prompt-engineer`](./skills/prompt-engineer/SKILL.md) | Создание и оптимизация эффективных промтов с нуля |

## Как подключить

Скилы — это обычные папки с `SKILL.md`. Скопируйте нужные в каталог скилов вашего агента
в целевом проекте:

```bash
# Claude Code
cp -r skills/<имя-скила> /путь/к/проекту/.claude/skills/

# Windsurf
cp -r skills/<имя-скила> /путь/к/проекту/.windsurf/skills/
```

Скопировать все сразу:

```bash
# Claude Code
cp -r skills/* /путь/к/проекту/.claude/skills/

# Windsurf
cp -r skills/* /путь/к/проекту/.windsurf/skills/
```

Некоторые агенты используют другие каталоги (`.codeium/windsurf/skills/`,
`.agents/skills/`, `.cursor/skills/` и т.п.) — сверьтесь с документацией вашего агента.
После копирования агент сам подхватит скил и активирует его, когда задача совпадёт с
полем `description`.

## Формат скила

```markdown
---
name: имя-скила
description: >
  Когда и для чего использовать этот скил. Именно по описанию агент решает,
  активировать ли скил.
---

# Заголовок

Инструкции для модели...
```

- `name` совпадает с именем папки.
- `description` — по нему агент понимает, когда применять скил; пишите конкретно.

## Атрибуция и лицензии

Заимствованные скилы включены в неизменном виде с сохранением авторства. Все четыре
распространяются под лицензией **MIT**. Полные тексты лицензий и копирайты — в файле
[`NOTICE`](./NOTICE).

- `karpathy-guidelines` © 2026 forrestchang и SwarmClaw AI contributors —
  [swarmclawai/andrej-karpathy-skills](https://github.com/swarmclawai/andrej-karpathy-skills)
  (MIT). Основано на [наблюдениях Андрея Карпаты](https://x.com/karpathy/status/2015883857489522876).
- `deep-research` © 2026 L8NTLABS LLC —
  [l8ntlabs/agent-skills](https://github.com/l8ntlabs/agent-skills) (MIT).
- `humanizer` © 2025 Siqi Chen —
  [blader/humanizer](https://github.com/blader/humanizer) (MIT). Основано на странице
  Wikipedia «Signs of AI writing».
- `caveman` © 2026 Julius Brussee —
  [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) (MIT).

Скилы, созданные в этом репозитории, распространяются под лицензией MIT (см.
[`LICENSE`](./LICENSE)).
