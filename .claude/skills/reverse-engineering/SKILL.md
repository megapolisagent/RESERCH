---
name: reverse-engineering
description: Реверс-инженерит реальную мировую практику для заданной цели (агент/система/продукт/компания/профессиональный домен/идея будущего агента) и превращает это в Intelligence Report с evidence — не мнение, не пересказ документации. Используй, когда нужно узнать, как что-то реально делается лучшими практиками в мире, для одной цели за раз.
user-invocable: true
allowed-tools: Read, Grep, Glob, WebFetch, WebSearch
---

# reverse-engineering — точка входа для нативной авто-загрузки Claude Code

Это не отдельная копия методологии — точка входа, чтобы Claude Code (project-scope `.claude/skills/`) реально подхватил Skill. Источник истины — `skills/reverse-engineering/SKILL.md` в корне этого репозитория (тот же файл, зарегистрированный в самом Skill).

**Прочитай и выполни `skills/reverse-engineering/SKILL.md` целиком, начиная с этого момента.** Не пересказывай его, не сокращай — следуй методологии (`references/PRINCIPLES.md`, `references/METHODOLOGY.md`, `references/REVIEW_LOOP.md`) дословно, в указанном там порядке.
