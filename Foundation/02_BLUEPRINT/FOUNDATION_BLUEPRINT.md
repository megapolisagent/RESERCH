# FOUNDATION_BLUEPRINT.md

Blueprint происхождения, не архитектуры. Для каждого будущего файла — только откуда берутся блоки. Без объяснения архитектурных решений, без объединения, без текста сверх минимума.

Формат: Файл → Берём (Repository → блоки) → Берём (World Practices → разделы/источники) → Берём (Construction Library → номера блоков).

Три источника, три неизменных пометки происхождения:
- ✅ Repository Library → рабочая реализация
- ✅ World Practices Library → рынок независимо подтверждает
- ✅ Foundation Construction Library → официальная формулировка

Если у файла нет блоков в каком-то источнике — пишется «нет», а не подбирается замена.

---

## HOME.md

Берём → Repository Library → Д-02 → рабочая реализация

Берём → World Practices Library → раздел 1 (Структура Agent Framework) → Anthropic Building Effective Agents, эскалация сложности → рынок независимо подтверждает

Берём → Foundation Construction Library → Блок 001 → Блок 002 → Блок 008 → Блок 009 → Блок 010 → Блок 022 → Блок 023 → официальная формулировка

И всё.

---

## AGENTS.md

Берём → Repository Library → Д-03 → рабочая реализация

Берём → World Practices Library → раздел 2 (Организация дома агента) → AGENTS.md как стандарт → рынок независимо подтверждает

Берём → Foundation Construction Library → Блок 016 → Блок 017 → Блок 018 → Блок 019 → Блок 020 → Блок 021 → официальная формулировка

И всё.

---

## SOUL.md

Берём → Repository Library → Д-02 → рабочая реализация

Берём → World Practices Library → нет

Берём → Foundation Construction Library → нет

И всё.

---

## PROFILE.md

Берём → Repository Library → Д-02 → Ц-02 → рабочая реализация

Берём → World Practices Library → нет

Берём → Foundation Construction Library → нет

И всё.

---

## MEMORY.md

Берём → Repository Library → П-01 → рабочая реализация

Берём → World Practices Library → раздел 3 (Память) → LangGraph → OpenAI Sessions → LlamaIndex → Claude Agent SDK → рынок независимо подтверждает

Берём → Foundation Construction Library → Блок 026 → Блок 027 → Блок 028 → Блок 029 → Блок 052 → Блок 053 → Блок 054 → Блок 056 → Блок 057 → Блок 063 → Блок 069 → Блок 070 → Блок 071 → Блок 077 → Блок 078 → Блок 079 → официальная формулировка

И всё.

---

## memory/ (дневник + правки)

Берём → Repository Library → П-01 → П-02 → рабочая реализация

Берём → World Practices Library → раздел 3 (Память) → эпизодическая/handoff-память → рынок независимо подтверждает

Берём → Foundation Construction Library → Блок 027 → Блок 074 → официальная формулировка

И всё.

---

## knowledge/

Берём → Repository Library → П-03 → П-04 → рабочая реализация

Берём → World Practices Library → раздел 4 (Знания) → раздел 7 (Управление контекстом) → progressive disclosure, ADR-инструменты → рынок независимо подтверждает

Берём → Foundation Construction Library → Блок 043 → официальная формулировка (единственный блок)

И всё.

---

## ROUTING.md

Берём → Repository Library → П-04 → Ц-03 → рабочая реализация

Берём → World Practices Library → раздел 1 (Handoff vs tool-call, эскалация) → рынок независимо подтверждает

Берём → Foundation Construction Library → Блок 003 → Блок 004 → Блок 005 → Блок 006 → Блок 007 → Блок 018 → Блок 019 → Блок 031 → Блок 055 → официальная формулировка

И всё.

---

## skills/ (склад) + .home/skills/ (установленные)

Берём → Repository Library → Д-01 → С-01 → С-02 → С-03 → рабочая реализация

Берём → World Practices Library → раздел 7 (Модульность и расширяемость) → раздел 6 (Документация) → MCP Registry, Claude Code Plugins → рынок независимо подтверждает

Берём → Foundation Construction Library → Блок 030 → Блок 033 → Блок 041 → Блок 042 → Блок 044 → Блок 058 → Блок 059 → Блок 065 → Блок 067 → официальная формулировка

И всё.

---

## installer (скилл)

Берём → Repository Library → У-01 → У-02 → У-03 → У-04 → рабочая реализация

Берём → World Practices Library → раздел 8 (Обновление агентов) → раздел 7 (Модульность) → registry+manifest+install-time resolution → рынок независимо подтверждает

Берём → Foundation Construction Library → Блок 041 → Блок 058 → Блок 059 → официальная формулировка

И всё.

---

## UPDATE.md + update.sh

Берём → Repository Library → У-05 → У-06 → рабочая реализация

Берём → World Practices Library → раздел 10 (Обновление агентов) → immutable versioned artifact, pin-version rule → рынок независимо подтверждает

Берём → Foundation Construction Library → Блок 020 → Блок 021 → Блок 039 → Блок 040 → Блок 048 → Блок 066 → официальная формулировка

И всё.

---

## workspace/

Берём → Repository Library → Д-04 → рабочая реализация

Берём → World Practices Library → нет

Берём → Foundation Construction Library → Блок 024 → Блок 032 → официальная формулировка

И всё.

---

## COMMUNICATION.md

Берём → Repository Library → нет

Берём → World Practices Library → раздел 1 (Handoff vs tool-call) → раздел 7 (MCP vs A2A) → рынок независимо подтверждает

Берём → Foundation Construction Library → Блок 037 → Блок 038 → Блок 041 → Блок 045 → Блок 046 → Блок 047 → Блок 048 → Блок 049 → официальная формулировка

И всё.

---

## Сводка: файлы без полного покрытия трёх источников

- SOUL.md — только Repository.
- PROFILE.md — только Repository.
- knowledge/ — Repository + World Practices, Construction Library даёт один блок.
- workspace/ — Repository + Construction Library, World Practices — нет.
- COMMUNICATION.md — World Practices + Construction Library, Repository — нет.

Остальные семь файлов (HOME.md, AGENTS.md, MEMORY.md, memory/, ROUTING.md, skills/+installer, UPDATE.md) собираются из блоков всех трёх источников одновременно.
