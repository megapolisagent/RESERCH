# Как реально устроена автономная (unattended/headless) работа AI-агентов — 2026-08-18

Вопрос передан Engineer напрямую, зарегистрирован в `ENGINEER/OPEN_QUESTIONS.md` (запись 2026-08-18). Контекст: в тот же день владелец явно отклонила `--dangerously-skip-permissions` как решение (`ENGINEER/DECISIONS.md`, 2026-08-18) — это закрытая тема, не переоткрывается здесь. Вопрос не «как отключить проверки», а как реально устроенные системы дают безопасную автономность тремя гранями сразу: sandboxing, non-interactive конфигурация (и что технически заменяет собой approval), post-hoc audit trail.

Критерий зафиксирован до поиска (дословно из брифа): по каждому из трёх под-вопросов — минимум 2 реально существующие системы, разобранные на уровне механизма, с источником; честное «не найдено» там, где нечего сказать; по каждой находке — применимо к реальной среде владельца (Claude Code, Windows/git-bash, три независимых репозитория без общей инфраструктуры и без уже настроенной контейнеризации) или нет.

Метод: Tool router (`METHODOLOGY.md`) применён буквально — где нашёлся официальный URL через поиск, прямой fetch выполнен немедленно, не остановилась на WebSearch-агрегации. Все ключевые находки ниже — Confirmed или Established, source-hierarchy уровень 1–2 (первичная документация вендора), не блоги-агрегаторы, кроме явно помеченных исключений.

---

## Под-вопрос 1 — Sandboxing/containerization

### Система 1 — Claude Code: слоистая модель изоляции (Confirmed, первичный источник)

**Источник**: `code.claude.com/docs/en/sandbox-environments`, полный fetch напрямую (не через агрегатор), 2026-08-18.

**Механизм**, не просто название — шесть реально различных уровней, каждый со своим порогом настройки:
1. **Sandboxed Bash tool** — встроенный, только для команд Bash (`/sandbox` панель), OS-примитивы (Seatbelt на macOS, bubblewrap на Linux/WSL2). Не покрывает MCP-серверы и hooks.
2. **Sandbox runtime** (`@anthropic-ai/sandbox-runtime`, beta) — оборачивает весь процесс Claude Code (включая file tools, MCP, hooks) в тот же Seatbelt/bubblewrap. Default-deny сеть, запись ограничена явно перечисленными путями; `denyWrite` жёстко перекрывает `.git/hooks`, `.mcp.json`, `.claude/commands` — то, что могло бы дать сессии персистентность за пределами одного запуска.
3. **Dev container** — Docker-контейнер с default-deny iptables firewall (`init-firewall.sh`, allowlist по доменам: npm registry, GitHub, Claude API). Официальный пример в репозитории `anthropics/claude-code`. Именно эта конфигурация официально называется предпосылкой для безопасного `--dangerously-skip-permissions` («Because the firewall blocks unapproved egress, a configuration like this supports running Claude Code with `--dangerously-skip-permissions` for unattended work»).
4. **Custom container** — произвольный Docker/OCI-образ, свои seccomp-профили; типичный путь для CI-раннеров.
5. **Virtual machine** — Firecracker microVM и подобные, самый сильный барьер (свой kernel).
6. **Claude Code on the web** — Anthropic-управляемая VM + сетевой прокси с allowlist, отдельный прокси держит GitHub-токен вне песочницы.

Дословная официальная позиция о том, что заменяет проверку: «With no prompts to catch mistakes, the isolation boundary you choose is what protects your system.» — то есть явно называется прямая зависимость: чем меньше approval-пауз, тем сильнее должна быть изоляция, а не наоборот.

**Применимость к нашей среде**: частично, с honest gap. Sandboxed Bash tool и Sandbox runtime **официально не поддерживают нативный Windows** («This option does not support native Windows. On Windows hosts, use WSL2 or one of the container or VM approaches below» — дословно) — у владельца именно нативный Windows-хост (`OS Version: Windows 11`), WSL2 не подтверждена как настроенная. Dev container / custom container / VM — технически доступны на Windows через Docker Desktop (сам Docker Desktop использует WSL2-бэкенд внутри себя, но это не то же самое, что «агент работает через WSL2 напрямую»), но ни один из трёх независимых репозиториев-агентов сейчас не имеет своего `.devcontainer/` или Dockerfile — инфраструктура физически возможна, но не настроена, ровно как и предполагал сам бриф.

### Система 2 — OpenAI Codex CLI: OS-примитивы без контейнера по умолчанию (Confirmed, первичный источник)

**Источник**: `learn.chatgpt.com/docs/agent-approvals-security` (редирект с `developers.openai.com/codex/agent-approvals-security`), полный fetch напрямую, 2026-08-18.

**Механизм**: единственная из проверенных систем, где песочница **включена по умолчанию без Docker** — на macOS через `sandbox-exec` (Seatbelt policies), на Linux через `bwrap` (namespace-изоляция) + `seccomp` (фильтрация системных вызовов). Три режима `sandbox_mode`: `read-only` (только чтение, всё остальное требует approval), `workspace-write` (запись/команды внутри рабочей директории, сеть по умолчанию выключена), `danger-full-access` (без песочницы вообще, «not recommended» — дословно). `.git` защищён как read-only в любом режиме записи.

**Ключевое отличие от Claude Code**: изоляция здесь — свойство процесса (OS-уровень), не контейнера; Docker используется отдельно («Docker Sandboxes», microVM) только как дополнительный, более сильный слой поверх этого, не как единственный путь к безопасности.

**Применимость к нашей среде**: не напрямую (владелец использует Claude Code, не Codex CLI) — но переносимый принцип подтверждён дважды независимо (см. Систему 1): изоляция — отдельная от approval-механизма ось, и на Windows сравнимого штатного non-Docker пути (Landlock/seccomp — Linux-специфичны, Seatbelt — macOS-специфичен) не существует ни у одной из проверенных систем.

### Дополнительно, для полноты (не заменяет два основных, третий подтверждающий пример)

**OpenHands** — client-server архитектура, каждая сессия исполняется внутри Docker-контейнера через `ActionExecutor` (docs.openhands.dev/openhands/usage/architecture/runtime, WebSearch-агрегированный substantial excerpt, не full-fetch — Medium confidence). Подтверждает тот же паттерн (контейнер как единственная граница), не добавляет новый механизм сверх Claude Code dev container.

**gVisor** — назван в исходном брифе как пример, но **не найден** ни в одном первичном источнике конкретно в контексте AI-агентных систем в ходе этого поиска (только как общая container-runtime технология Google, без привязки к agentic tooling) — честно не засчитан, не притянут.

---

## Под-вопрос 2 — Non-interactive/headless конфигурация: что технически заменяет approval

Это ядро брифа: не «какой флаг выключает проверку», а «что заменяет собой проверку». Три независимые системы, все явно называют механизм замены, не просто «отключение».

### Система 1 — Claude Code: `-p`/`--bare` + Auto mode классификатор (Confirmed, первичный источник)

**Источник**: `code.claude.com/docs/en/headless` и `code.claude.com/docs/en/permission-modes`, оба полностью прочитаны напрямую, 2026-08-18.

**Headless-механика**: `claude -p "<prompt>"` — non-interactive запуск; `--bare` пропускает автообнаружение hooks/skills/plugins/MCP/CLAUDE.md для воспроизводимости в CI; `--output-format json|stream-json` для программного разбора результата; `--allowedTools`/`--permission-mode` заранее пред-одобряют инструменты так, чтобы batch-задача не заблокировалась на approval-запросе, которого некому дать в headless-режиме.

**Что реально заменяет approval — самая содержательная находка всего поиска**: режим `auto` — не «выключенная проверка», а **вторая модель-классификатор**, которая ревьюит каждое действие вместо человека, дословно: «Auto mode lets Claude execute without routine permission prompts. A separate classifier model reviews actions before they run, blocking anything that escalates beyond your request, targets unrecognized infrastructure, or appears driven by hostile content Claude read.» Классификатор работает по умолчанию на Sonnet 5 (независимо от модели основной сессии), имеет документированный и версионированный список того, что блокирует безусловно (curl|bash, force push, `git reset --hard`, production deploy, слив секретов наружу, самоодобрение своего PR, `--dangerously-skip-permissions` внутри собственной сессии как отдельная блокируемая категория, и др. — список датирован по версиям, v2.1.195–v2.1.205, то есть это не статичный маркетинг-текст, а реально развивающийся, регрессионно расширяемый механизм). Классификатор получает только: сообщения пользователя, tool calls, CLAUDE.md — результаты инструментов **вырезаны** специально, чтобы враждебный контент из файла/веб-страницы не мог манипулировать классификатором напрямую (защита от prompt injection на уровне архитектуры проверки, не только промпта).

Отдельно — `dontAsk` режим: детерминированный allowlist (`permissions.allow` + read-only команды + PreToolUse hook), без классификатора вообще — «Use this mode for CI pipelines or restricted environments where you pre-define exactly what Claude may do; the session never waits for input.» Это ближе к тому, что уже настроено у владельца (`permissions.allow: Bash(*)`), чем `auto`-режим.

Официально задокументированный порог отказа: 3 подряд или 20 суммарно заблокированных действий — auto mode приостанавливается и возвращается к прямому approval (в интерактиве) или просто не выполняет действие (в headless — «Claude Code doesn't count a denial toward either threshold when a safety check separate from auto mode refuses the classifier's own request... Claude Code doesn't stop the run in either case» — то есть в headless нет паузы «на подумать», есть либо выполнение, либо тихий отказ конкретного действия).

**Применимость к нашей среде — прямая, без новой инфраструктуры**: `auto`-режим — не гипотетика, а штатная функция того же Claude Code, что уже используется. Более того, документация утверждает, что на Pro/Max/Team-планах `auto` уже является встроенным стартовым режимом по умолчанию (для терминальных сессий и VS Code) — какой план у владельца, не проверено в этом поиске, отмечено как [UNKNOWN], не додумано. `dontAsk` — уже структурно близко к текущей настройке (`permissions.allow: Bash(*)`), отличие — детерминированный allowlist без классификатора, а не наоборот.

### Система 2 — OpenAI Codex CLI: две независимые оси (`sandbox_mode` × `approval_policy`) (Confirmed, первичный источник)

**Источник**: тот же fetch, что и в под-вопросе 1.

**Механизм**: официально названы «two layers that work together: Sandbox mode (what Codex can do technically) and Approval policy (when Codex must ask you before executing)» — прямое, явное разделение «что технически возможно» от «когда спросить», а не одна ручка. `approval_policy=never` — headless-эквивалент; безопасность в этом режиме держится не на доверии к модели, а на том, что `sandbox_mode` (Seatbelt/Landlock, см. под-вопрос 1) физически не даёт выйти за пределы объявленной директории/сети независимо от того, попросила ли модель разрешения. `approval_policy=untrusted` — второй слой: «Codex runs only known-safe read operations automatically», остальное — approval.

**Применимость**: как и в под-вопросе 1, не напрямую (другой продукт) — но подтверждает тот же паттерн, что и Claude Code: замена approval **всегда** двухслойная (техническая граница + программная политика), никогда не «просто выключить проверку».

### Система 3 — AutoGen (Microsoft): `human_input_mode="NEVER"` + `DockerCommandLineCodeExecutor` (Established, официальная документация Microsoft)

**Источник**: `microsoft.github.io/autogen/0.2/docs/topics/code-execution/cli-code-executor/`, полный fetch напрямую, 2026-08-18.

**Механизм**: `human_input_mode="NEVER"` на `ConversableAgent` — убирает паузу на human input между шагами диалога агентов. Это само по себе **не** механизм безопасности — документация прямо предупреждает про локальный executor: «The local version will run code on your local system. Use it with caution.» Что реально заменяет проверку — выбор `DockerCommandLineCodeExecutor` вместо `LocalCommandLineCodeExecutor`: тот же код, но исполняется в Docker-контейнере, а не в процессе хоста. То есть у AutoGen нет классификатора (в отличие от Claude Code) и нет двухслойной политики (в отличие от Codex) — единственная граница безопасности при `human_input_mode="NEVER"` — это контейнер, и ничего больше; если разработчик оставил `LocalCommandLineCodeExecutor`, `human_input_mode="NEVER"` в этой конфигурации не защищено вообще ничем.

**Применимость**: не напрямую (другой фреймворк) — честный контраст: показывает нижнюю границу того, что может пойти не так, если non-interactive настроить без замены на что-либо (ни классификатор, ни allowlist, ни sandbox_mode-подобный технический барьер — просто контейнер как единственная защита).

---

## Под-вопрос 3 — Provenance/audit trail post-factum

### Система 1 — GitHub Copilot coding agent: session log + сигнатура коммита + структурный запрет самоодобрения (Confirmed, первичный источник)

**Источник**: `docs.github.com/en/copilot/concepts/agents/cloud-agent/risks-and-mitigations`, полный fetch напрямую, 2026-08-18.

**Механизм, три части одновременно**:
1. **Атрибуция и подпись**: коммиты подписаны как «Verified» на GitHub, автор — Copilot, соавтор — пользователь, который поставил задачу. Ничто не может быть анонимным постфактум.
2. **Session logs**: «Each commit message includes a link to the agent session logs» — прямая, постоянная ссылка от каждого коммита к полному логу того, что агент делал в этой сессии, специально «for auditing purposes» — дословно.
3. **Структурный gate, не просто лог**: инициатор задачи технически **не может** одобрить получившийся PR («the developer who assigned the issue... can't approve it, which preserves the expected 'Required approvals' controls») — это превращает post-hoc проверку из опции в обязательное условие мержа, а не просто доступную для чтения запись.

**Применимость к нашей среде — прямое структурное совпадение с уже действующей практикой**: у владельца уже сегодня (2026-08-18, `ENGINEER/DECISIONS.md`, несколько записей подряд) действует ровно тот же паттерн вручную — Engineer готовит и коммитит, push делает владелец лично, то есть тот, кто выполнил работу, не является тем, кто её пропускает в канон. GitHub Copilot coding agent — независимое внешнее подтверждение, что этот паттерн (не совпадение исполнителя и одобряющего) реально используется production-системой как основной audit-gate, а не изобретён ad hoc в этой экосистеме.

### Система 2 — AWS Bedrock AgentCore: CloudTrail как отдельный, не встроенный в агента слой (Confirmed, первичный источник)

**Источник**: `docs.aws.amazon.com/bedrock-agentcore/latest/devguide/registry-cloudtrail.html` и смежные страницы того же официального домена, WebSearch-агрегированный substantial excerpt по нескольким официальным страницам (не единый full-fetch одной страницы) — Medium confidence, не High, честно так и помечено.

**Механизм**: каждый вызов агента (`InvokeAgent`, `InvokeInlineAgent`) и каждый вызов Gateway API логируется в CloudTrail как management- или data-plane событие — **платформа**, не сам агент, формирует запись; агент не может её не создать, не отредактировать задним числом. Data events для Gateway требуют явного создания trail в S3 (не включены по умолчанию — честно задокументированное ограничение самого AWS, не наша догадка). Проверяется не синхронно, а постфактум — CloudTrail-запись читается инструментами compliance/security команды в любое время после события.

**Применимость к нашей среде**: не применимо напрямую — требует AWS-инфраструктуры (аккаунт, CloudTrail, S3 trail), которой у трёх независимых markdown/git-репозиториев владельца нет и не предполагается. Ценность — как контрастный пример: показывает, что «serious» post-hoc audit в индустрии обычно означает **отдельный, платформенный** сервис записи, а не то, что сам агент ведёт свой лог (тот же паттерн, что уже был закрыт 2026-08-12 в вопросе про execution record для независимо живущих агентов — см. `OPEN_QUESTIONS.md`, запись 2026-08-12, Batch EXECREC — не переоткрывается здесь, только подтверждается тем же выводом с новой стороны).

### Дополнительно — Claude Code сам, новая деталь этого поиска (не переоткрывает Batch EXECREC, дополняет)

`code.claude.com/docs/en/headless` (тот же fetch, что и выше) описывает post-hoc проверку subagent-работы, которой не было в прошлом исследовании EXECREC: классификатор (тот же, что в auto-режиме) делает третью, отдельную проверку **после** завершения саб-агента — «When the subagent finishes, the classifier reviews its full action history; if that return check flags a concern, a security warning is prepended to the subagent's results.» Это не замена синхронного approval на паузу, а именно постфактум-ревью целой истории действий уже готового результата, с явной пометкой «unreviewed and should be treated as untrusted», если сама проверка не удалась технически. Прямо применимо: это тот же Claude Code, что уже используется, механизм уже включён при использовании `auto`-режима — не требует новой инфраструктуры.

---

## Честно не найдено / не проверено

- Дословное подтверждение gVisor в контексте AI-агентов — не найдено, не притянуто.
- Cursor и CrewAI — не проверены прямым fetch в этом поиске (WebSearch по ним не выполнялся отдельно, время/скоуп ушли на подтверждённо более сильные и более прямо применимые находки — Claude Code официальная документация оказалась настолько содержательной, что закрыла оба под-вопроса 1 и 2 с запасом раньше, чем потребовалось открывать третий-четвёртый источник — P6, насыщение). Честно помечено как «не проверено», не как «не существует».
- Devin (Cognition) — не проверен в этом заходе; упоминался в исходном брифе, но не был нужен для выполнения критерия (минимум 2 системы на под-вопрос уже выполнен без него).
- План владельца (Pro/Max/Team/Enterprise) для Claude Code — от которого зависит, стартует ли `auto`-режим по умолчанию — не проверялся, это факт среды, не предмет этого исследования; помечено [UNKNOWN] в тексте выше, не предположено.

## Границы (соблюдены по `MISSION.md`)

Архитектура/решение для среды владельца не спроектированы. Не сказано, что именно внедрять, в каком объёме и в каком порядке — это остаётся Engineer/владельцу. Единственное, что сделано сверх голого перечисления фактов — по каждой находке явно названо, требует ли она новой инфраструктуры (контейнеризация, WSL2, AWS-аккаунт) или доступна уже сегодня в той же среде (Claude Code auto/dontAsk-режимы, GitHub-подобный паттерн неодобрения-своей-же-работы, который уже практикуется вручную).
