# FOUNDATION_INTEGRATION_PLAN.md

Итог археологии прошлых агентов (Blueprint_Agent_System.md, Chief Design Officer, AI_OS+sandbox, MAIN_ENGINEER, MAIN_ASSISTANT, math-tutor-agent, OBSIDIAN_BUILDER) + два внешних источника (Visual Engineering Starter, heroes-camp-jtbd). Триаж по правилам `FOUNDATION_INTEGRATION_RULES.md`. Археология этим документом закрывается — дальше начинается инженерия: реальное проектирование каждого пункта из раздела 3 через тот же цикл Blueprint → Карта → Документ → Decisions, которым строился Foundation v1.

Статус всех решений ниже — **Proposal**, если не указано иное.

---

## 1. Что найдено (полная опись, с источниками)

| Находка | Источники | Сходимость |
|---|---|---|
| Decision Gateway (Proposal→Discussion→Locked) | Chief Design Officer, OBSIDIAN_BUILDER, MAIN_ASSISTANT (DECISIONS/+STATE.md), AI_OS (Decision Record) | 4 |
| Open Questions Registry | OBSIDIAN_BUILDER | 1 (частичное эхо в эпистемической лестнице AI_OS) |
| Idea Calibration / Entry Gate | MAIN_ENGINEER, AI_OS, Blueprint_Agent_System, Chief Design Officer, Visual Engineering («Ask Only Valuable Questions») | 5 |
| Execution Drift | MAIN_ENGINEER, Blueprint_Agent_System, Chief Design Officer (`Pattern — CDO Drift Modes`) | 3 |
| Decision Freeze | MAIN_ENGINEER | 1 (смежно с Decision Monotonicity ниже) |
| Decision Monotonicity + SPEC-барьер | AI_OS | 1 (та же тема, что Decision Freeze) |
| Independent Validation | AI_OS | 1 |
| Self-Modification Guard | MAIN_ENGINEER, Blueprint_Agent_System (No Self-Modification), OBSIDIAN_BUILDER (Правило изменения процесса) | 3 |
| System Health Check | MAIN_ENGINEER, AI_OS (Final Quality Gate — смежная тема), Chief Design Officer (Review-Self-Audit) | 3 |
| Capability Resolver | MAIN_ASSISTANT, Visual Engineering (Tool Routing escalation) | 2 |
| Legacy-first Alarm | AI_OS, Visual Engineering («Evolve Before Expanding»), heroes-camp-jtbd (то же название, третьей рукой) | 2 независимых + 1 совпадение по имени |
| Sources of Truth hierarchy | Chief Design Officer | 1 |
| FACT / INFERENCE / UNKNOWN | Visual Engineering, AI_OS (эпистемическая лестница) — Foundation уже имеет анти-галлюцинацию той же функции | 3 (включая сам Foundation) |
| «Не строить новую сущность, если можно усилить существующую» | Visual Engineering (Evolve Before Expanding), сам этот диалог | — методологическое, не архитектурное |

---

## 2. Что усиливает существующие файлы Foundation

Механизма у Foundation нет, но он умещается в уже существующий файл без изменения его ответственности — новая сущность не создаётся.

| Находка | Усиливает | Как именно |
|---|---|---|
| Capability Resolver | `ROUTING.md` | Классификация потребности (REMEMBER/VERIFY/EXPLORE/EXTERNAL CONTEXT) перед поиском по таблице маршрутов, плюс явный сигнал «Need → Capability отсутствует» вместо тихой деградации |
| Decision Freeze + Decision Monotonicity | Decision Gateway (см. раздел 3) | После LOCKED — запрет возвращаться к отвергнутым альтернативам без нового факта; не отдельный механизм, а поведенческое правило внутри уже нового Decision Gateway |
| Independent Validation | Decision Gateway (см. раздел 3) | Проверка изолированным рассуждением перед переходом в LOCKED для решений, меняющих сам метод работы — тоже правило внутри Decision Gateway, не отдельная сущность |
| Self-Modification Guard | `UPDATE.md` | Добавляет сценарий, которого там сейчас нет: не «апдейт из внешнего репозитория», а «агент сам хочет поправить HOME/SOUL/ROUTING по итогам разговора» — вопрос перед этим, не новый файл |
| System Health Check | `UPDATE.md` | Периодический раздел/сценарий самоаудита накопленной сложности — не новый «мир», встроен туда же, где уже живёт логика обновления |
| Legacy-first Alarm | Idea Calibration / Entry Gate (см. раздел 3) | Конкретная проверка внутри входного гейта: «прежде чем проектировать — активно поискать дубли» — часть Entry Gate, не отдельный принцип |
| Sources of Truth hierarchy | `instructions/memory-rules.md` | Явное правило «что побеждает при конфликте источников» — расширяет уже существующий файл про работу памяти, не создаёт новый |

---

## 3. Что действительно новое

Ни один существующий файл Foundation не может вместить механизм без нарушения своей ответственности.

| Находка | Почему нет места в существующих файлах | Куда ляжет |
|---|---|---|
| **Decision Gateway** (включая Decision Freeze, Decision Monotonicity, Independent Validation как внутренние правила) | `MEMORY.md` сейчас — плоский список фактов без статуса и без шлюза «идея → факт»; добавить статусную модель значит дать файлу новую ответственность, а не расширить старую | `MEMORY.md` + `instructions/memory-rules.md` — новый механизм внутри существующих файлов |
| **Open Questions Registry** | У Foundation нет ни одного файла, отвечающего за незакрытый вопрос как объект с заранее заданным критерием ответа | Новый файл, ближе всего по духу к `knowledge/` |
| **Idea Calibration / Entry Gate** (включая Legacy-first Alarm как внутреннюю проверку) | `HOME.md` сейчас даёт только мягкое «задай пару уточняющих вопросов»; формальный триаж по значимости и жёсткий стоп до определения задачи — новая ответственность, не расширение старой | Новый раздел `HOME.md` |
| **Execution Drift** | У Foundation нет разницы между «нарушил явное правило» и «постепенно сполз в другое поведение, не нарушив ничего напрямую» — второго типа сбоя система не видит вообще | Открытый вопрос — новый раздел `HOME.md` либо отдельный файл, решится на этапе проектирования |

---

## 4. Что не переносится

| Находка | Источник | Причина |
|---|---|---|
| Registry (System Asset Registry) | MAIN_ENGINEER | Инфраструктура управления несколькими агентами одного владельца, не механизм внутри одного Дома |
| Function Lock | Blueprint_Agent_System | Уже отклонён ранее самим AI_OS как специфика продукта другого масштаба |
| Traceability Requirement | Blueprint_Agent_System | Оставлен AI_OS как «кандидат, не строим сейчас» — статус не меняется |
| IDEA ANCHOR | Blueprint_Agent_System | Дубликат — уже покрыто триадой SOUL/PROFILE/MEMORY «Кто я» |
| UNDERSTAND→THINK→JUDGE→ACT / Reasoning Pipeline / Execution Loop | MAIN_ASSISTANT, AI_OS, Visual Engineering | Стиль мышления, не структура — та же логика, что «характер живёт в SOUL.md, не в HOME.md»; кандидат в гипотетическое будущее кольцо «Thinking», не в Foundation |
| SSOT + derived-file recompute | math-tutor-agent, AI_OS (Derived Representation Discipline) | Условно верно, но у Foundation пока нет второго производного файла от MEMORY.md — применять нечего |
| Детерминированный расчёт PHASE | math-tutor-agent | Единичный источник, слишком специфично для агентов с несколькими явными режимами работы |
| Skill Standard (шаблон написания скилла) | Visual Engineering | Слабая, стороння провенанс; про качество документации, не про архитектуру |
| MECHANISM_LIBRARY / CAPABILITY_MAP | OBSIDIAN_BUILDER | Дубликат — уже вынесено в `skills/reverse-engineering/` отдельным решением |
| plan-apply-safety-gate | OBSIDIAN_BUILDER | Дубликат `UPDATE.md`/`update.sh` |
| UNKNOWN GATE | OBSIDIAN_BUILDER | Дубликат `[УТОЧНИТЬ]` |
| MY_AGENTS.md | OBSIDIAN_BUILDER | Специфика AI Intelligence, не Foundation |
| Builder Freeze | OBSIDIAN_BUILDER | Единичный инцидент одного проекта, без конвергенции |
| «Правило изменения процесса» | OBSIDIAN_BUILDER | Эволюция `UPDATE.md`, не новый механизм |
| Весь материал heroes-camp-jtbd | ikrasinsky-heroes-camp-jtbd-outcome-skills-handoff | Охраняемый материал третьей стороны — использование только с письменного согласия автора; не извлекалось |
| Graphify (aibasis.ru) | внешняя ссылка | Другой класс объекта — утилита оптимизации токенов, не архитектура агента |

---

## Что дальше

Разделы 2 и 3 — единственные, что перешли в реальное проектирование. Каждый пункт прошёл тот же цикл, которым строился Foundation v1: Blueprint → Карта сборки → Документ → запись в `FOUNDATION_DECISIONS.md`.

**Статус: закрыто.** Все 4 пункта раздела 3 и все 7 пунктов раздела 2 реализованы — см. `FOUNDATION_DECISIONS.md`, раздел «Foundation v2». Порядок фактически отличался от изначально предложенного (Decision Gateway → Entry Gate → усиления → новые сущности → Execution Drift/Health Check последними) — усиления были сознательно поставлены перед новыми сущностями по правилу «сначала усиливаем существующее», а не в порядке зависимостей, как планировалось здесь изначально. Каждый пункт перед сборкой заново проверялся на уже обновившейся архитектуре, а не переносился по старому выводу — два пункта (Open Questions, System Health Check) в результате получились меньше по объёму, чем изначально описано в разделах 1 и 3 этого документа.
