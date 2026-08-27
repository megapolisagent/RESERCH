# Находки — Эталонная декомпозиция роли «стратегический маркетинговый консультант» (профессия, не AI-агент) и прямая сверка с ядром AI Marketing Strategist

Задача от ENGINEER, по поручению владельца. Критерий зафиксирован до поиска: конкретная, проверяемая декомпозиция роли стратегического маркетингового консультанта из авторитетного источника (профессиональная методология/признанный фреймворк индустрии), с пометкой ЗНАЮ/ПРЕДПОЛАГАЮ, и отдельно — прямой ответ, совпадает ли уже написанное ядро AI Marketing Strategist (4 способности: Audience Research, Positioning & Category Definition, Messaging & Persuasion Design, Brand Strategy & Equity Management + режим Advisory) с этим эталоном, и если расходится — в чём именно.

**Responsibility Boundary Gate** (`skills/reverse-engineering/references/METHODOLOGY.md`): это **research + synthesis**, не design. Отчёт называет рыночный эталон и сверяет с ним уже написанный текст. Он не решает, что менять в `AI Marketing Strategist/HOME.md` — это отдельный, gated шаг владельца и/или Engineer.

**Internal-context-first** (Stage 1): прочитано целиком перед внешним поиском — `AI Marketing Strategist/HOME.md` (текущее ядро), `AI_OS/specializations/marketing_agent.md` v1.4 (легаси-источник ядра, откуда взяты 4 способности и режим Advisory), запись `AI Marketing Strategist` в `ENGINEER/knowledge/built-agents-registry.md` (честно зафиксировано: методология там **не** сверена с Researcher — это и есть повод этого отчёта).

---

## Профессиональная модель целиком (прежде чем сверять по пунктам)

Профессия «маркетинговый стратег» — не список из 4 умений, а один участок внутри полной карты Marketing Management, у которой есть признанная индустрией структура (ниже, §1–2) и **два независимых измерения**, которые нельзя сверять по отдельности:

1. **По содержанию** — полная карта маркетинга как дисциплины это: Insight/Data (исследование и аналитика) → Strategy & Planning (куда идти) → Offering (Product + Price + Brand) → Delivery (Place/Channel/Distribution) → Communication (Promotion: контент, digital, PR, продажи) — плюс сквозные, не привязанные к одному этапу компетенции: Commercial (финансовая грамотность/бюджет/риск), Leadership & Management, Digital Agility, Customer Experience/CRM.
2. **По уровню вовлечённости (не по содержанию)** — один и тот же контент можно поставлять на трёх разных, реально существующих на рынке уровнях: **in-house CMO** (владеет бюджетом, P&L, командой, всей картой целиком), **fractional CMO** (владеет стратегией и *надзирает* за исполнением, не полный P&L), **marketing strategy consultant** (владеет только стратегией/рекомендацией, ничего не исполняет, бюджетом не распоряжается).

Ядро AI Marketing Strategist — это выбор **узкого среза по содержанию** (Audience Research + Positioning + Messaging-стратегия + Brand) **и узкого среза по вовлечённости** (Advisory = третий уровень, consultant-tier). Это два разных решения, и ниже они сверяются раздельно.

---

## 1. Содержание профессии — AMA Professional Certified Marketer, Marketing Management Body of Knowledge — Confirmed, primary/official

**Источник**: `ama.org/wp-content/uploads/2019/01/ama-pcm-marketing-management-body-of-knowledge.pdf` — официальный документ American Marketing Association (профессиональный орган, выдающий признанную индустрией сертификацию), получен и прочитан напрямую как PDF (primary, уровень 1), не по пересказу.

**Механизм**: экзамен/квалификация построены на **8 доменах**, с фиксированным весом:

1. Marketing Strategy (10%) — планирование, ценностное предложение, SWOT, конкурентная стратегия.
2. Global, Ethical, and Sustainable Marketing (11%).
3. Managing Information for Marketing Insights (15%) — market research, CRM, data/marketing analytics.
4. Buyers and Markets (17%) — consumer/organizational behavior, **Segmentation, Targeting, and Positioning**.
5. The Offering – Product and Service (21%, крупнейший домен) — Product Strategy, New Product Development, **Branding Strategy**, Service Strategy.
6. Manage Pricing Decisions (7%).
7. Deliver the Value Offering (8%) — channels, distribution, logistics, supply chain.
8. Communicate the Value Offering (11%) — promotion basics (AIDA), digital marketing, social media, «legacy» (реклама, PR, personal selling).

**Прямое наблюдение**: домен 1 «Marketing Strategy» — отдельный, узкий (10%) домен планирования, а не то же самое, что «вся стратегическая работа». То, что ядро AI Marketing Strategist называет «стратегией», у AMA распределено по доменам 1, 4 (STP) и части 5 (Branding) — это не противоречие, а вопрос того, как резать один и тот же материал; название совпадает с одним доменом, содержание — с тремя.

## 2. Содержание профессии — CIM Global Professional Marketing Framework (GPMF), 2024 — Confirmed, primary/official

**Источник**: `cim.co.uk/media/rz2lsf2w/thegpmf.pdf` — официальный документ Chartered Institute of Marketing (британский профессиональный институт, выдаёт Chartered Marketer status), получен и прочитан напрямую (primary, уровень 1).

**Механизм**: 8 периферийных компетенций вокруг одного центрального узла:

- **Strategy & Planning**
- **Data & Insight** (research input/output, метрики/тренды, data governance)
- **Proposition Development** — **центральный, связывающий узел карты, не один из восьми равных**: Value Proposition, Market profile, Strategic fit, Creative positioning, Innovation.
- **Brand & Reputation** (Identity, Equity, Brand management, Crisis management)
- **Marketing Communications** (Integration, Multi-channel, **Content**, Communications strategy)
- **Customer Experience** (CRM/customer journey, omnichannel, сегментация/персоны, org alignment)
- **Digital Agility** (AI, emerging trends, channels, tech/e-commerce/UX/analytics)
- **Commercial** (Financial awareness — forecast/budgeting, внешние влияния, stakeholder management, конкурентная позиция, governance & risk)
- **Leadership & Management** (org development, resource management, project planning, people/performance/capability)

**Прямое наблюдение, важное для сверки ниже**: CIM ставит **Proposition Development в центр**, а не как одну из равных способностей — то есть в проф. модели позиционирование/ценностное предложение работает как связующий узел, через который проходят Brand, Comms, Data и Commercial, а не как параллельный, равный по весу пункт списка. Второе: CIM **не разделяет** messaging-стратегию и контент/канал-исполнение — «Content» стоит внутри той же компетенции «Marketing Communications», что и «Multi-channel» и «Communications strategy».

## 3. Уровень вовлечённости — «стратег/консультант» vs «fractional CMO» vs «in-house CMO» — Confirmed по 8 независимым практикам

**Источник**: 8 независимых практикующих консалтинговых/агентских сайтов (thesocialmediahat.com, authenticbrand.com, boardroomadvisors.co, saashero.net, dashsocial.com.au, treefrogmarketing.com, mahdlo.net, growthmarketingpartner.com) — не один автор, устойчиво сходящаяся терминология индустрии, не эксклюзивная методология одной фирмы.

**Механизм**: рынок реально держит три разных, названных тира одной профессии:
- **Marketing consultant / strategy consultant** — «даёт рекомендации и стратегии, но не берёт на себя прямую ответственность за исполнение, оставляя исполнение внутренней команде клиента»; работает «hands-off», за пределами команды клиента; тарификация почасовая/проектная ($50–500/час).
- **Fractional CMO** — «берёт на себя более высокий уровень ответственности — не только разрабатывает стратегию, но и надзирает за её исполнением, управляет командами/агентствами»; не полный P&L, но выше consultant по вовлечённости; тарификация — ретейнер ($5–15k/мес).
- (не в этом наборе источников, но общеизвестно из корпоративной практики) **in-house CMO** — полный P&L, бюджет, кросс-функциональное лидерство.

**Прямой вывод для вопроса брифа «Advisory = слабость или структура»**: режим Advisory (советует, не исполняет, не тратит бюджет) **не изобретение задним числом — это точное описание существующего, признанного индустрией тира «marketing consultant»**, отдельного от fractional/in-house CMO не по недостатку полномочий, а по типу контракта. Понижение статуса не в этом; вопрос в том, называет ли AI Marketing Strategist прямо, что он работает на *consultant-tier*, а не на *CMO-tier* — HOME.md называет это прямо («Не отвечает: за исполнение, публикацию, бюджет, результат на рынке») — это ЗНАЮ, совпадает с профессиональным тиром consultant, не самодельная урезка.

## 4. Реальное разногласие внутри профессии, которое ядро не называет — Confirmed, академический источник vs мейнстрим-фреймворк

**Источник**: Ehrenberg-Bass Institute for Marketing Science (Университет Южной Австралии) — Byron Sharp, *How Brands Grow* (2010) — реальный, десятилетиями цитируемый исследовательский центр, не блог одного консультанта; сверено по нескольким независимым разборам (dovetail.com, umbrex.com, researchgate.net, warc.com, thebrandgym.com).

**Механизм спора**: Kotler/Dunford-школа (STP — Segmentation, Targeting, Positioning: сузить аудиторию, найти отличие, позиционировать против него) — это ровно метод, на котором построена способность «Positioning & Category Definition» в ядре AI Marketing Strategist. Ehrenberg-Bass/Sharp эмпирически оспаривают именно эту логику: «бренды растут не за счёт узкого таргетинга — когда бренды растут, они получают клиентов из всех сегментов»; рост объясняется **mental & physical availability** (узнаваемость + доступность для покупки), а не точностью позиционирования под сегмент. Это не маргинальная критика — Ehrenberg-Bass второе по влиятельности исследовательское направление в маркетинговой науке за последние 15 лет, с реальными эмпирическими данными, не только теорией.

**Прямой вывод**: способность «Positioning & Category Definition» опирается на один из двух реально спорящих между собой лагерей профессии, и старый документ (`marketing_agent.md`) не называет существование второго лагеря нигде в списке источников — не потому что скрывает, а потому что вопрос, видимо, не всплывал на момент написания v1.4. Это не ошибка ядра (Dunford — легитимный, широко используемый метод), но честный, **не закрытый** пробел: сам факт спора нигде не зафиксирован как известный trade-off.

---

## Прямая сверка: ядро (4 способности + Advisory) против эталона

| Способность ядра | Куда ложится в AMA (§1) | Куда ложится в CIM (§2) | Совпадение |
|---|---|---|---|
| Audience Research (JTBD) | Домен 4 частично (Consumer/Org Behavior, Segmentation) | Data & Insight (частично) + Customer Experience (segmentation/personas) | **Частичное** — оба эталона держат «данные/аналитика/CRM» как отдельную, более крупную инфраструктурную компетенцию (AMA — 15% экзамена, домен 3), не только метод интервью |
| Positioning & Category Definition | Домен 4, Topic 3 (STP) | **Proposition Development — центральный узел**, не периферийный | **Совпадает по содержанию, недооценён по весу** — эталон делает это связующим центром карты, ядро — одним из четырёх равных пунктов |
| Messaging & Persuasion Design | Домен 8 (Communicate the Value Offering) — но вместе с digital/social/legacy тактикой | Marketing Communications — но вместе с Content/Multi-channel | **Расходится на границе** — оба эталона трактуют messaging-стратегию и контент/канал-исполнение как ОДНУ компетенцию; ядро проводит между ними жёсткую архитектурную границу (Messaging внутри, Content Production/Distribution — вне) |
| Brand Strategy & Equity Management | Домен 5, Topic 3 (Branding Strategy) | Brand & Reputation | **Совпадает** — прямое соответствие в обоих эталонах, как отдельная, устойчиво называемая компетенция |
| — (нигде в карте) | Домен 5 Topics 1–2 (Product Strategy, NPD) — 21% домена, крупнейший в BOK | — | **Отсутствует полностью**, не названо даже как «вне scope» |
| — (нигде в карте) | Домен 6 (Pricing) — 7% | Commercial (financial awareness) | **Отсутствует полностью**, не названо даже как «вне scope» |
| — (нигде в карте) | Домен 3 (Managing Information) — 15%, CRM/аналитика как система | Data & Insight (data governance) | **Отсутствует как инфраструктура** — есть только метод сбора (JTBD), нет пункта про аналитику/CRM-систему как актив |
| — (нигде в карте) | — | Commercial (бюджет/governance/конкурентная позиция как **компетенция суждения**, не как исполнение) | **Отсутствует** — «не отвечает за бюджет» в HOME.md про исполнение (не тратит), но про бюджет как предмет **анализа/рекомендации** — молчание |
| Режим Advisory | — | — | **Совпадает с признанным профессиональным тиром** «marketing strategy consultant» (§3), не структурная слабость |

---

## Что проверено и не найдено

- Прямого фетча CIM PDF через `WebFetch` не получилось (403) — прочитано через `mcp__firecrawl__firecrawl_scrape` тем же URL, тот же файл, тот же результат (primary, не пересказ).
- Table of contents Kotler & Keller *Marketing Management* (канонический академический учебник дисциплины) получен только через вторичные описания поиска (books/library-каталоги), не через прямое чтение оригинала — уровень **Established, single-source, вторично** — использован только как подтверждающая деталь (структура Part 4 «Building Strong Brands» = Positioning + Brand Equity, согласуется с AMA/CIM), не как несущий источник ни для одного вывода выше.
- Не искался (за пределами брифа, не требовалось критерием) реестр российских/рунет-стандартов маркетинговой профессии — вопрос был про «признанную индустрией методологию» в целом, не про региональную специфику; при необходимости — отдельный, узкий запрос.
- Насыщение (P6): два независимых официальных фреймворка (AMA, CIM) сошлись на одной и той же структуре (insight → strategy/proposition → offering/brand → communication + сквозные commercial/leadership/digital) — третий источник того же типа не добавил бы новой категории, поиск остановлен на этом основании, не по нехватке времени.

---

## Переиспользуемые находки (Definition of Done 5a)

**Карточка 1 — Двухосевая модель профессии (содержание × вовлечённость) как критерий сверки**

- **Назначение**: рамка из §«Профессиональная модель целиком» — любую роль маркетингового консультанта можно и нужно сверять по двум независимым осям: что именно входит в контент работы (какие домены/компетенции), и на каком уровне вовлечённости это поставляется (consultant / fractional / in-house).
- **Почему интересен**: без этого разделения вопрос владельца «Advisory — это слабость?» неразрешим — он смешивает вопрос о *содержании* (чего не хватает в списке способностей) с вопросом об *уровне* (советует vs делает), а это два эталона из разных источников (AMA/CIM — про содержание; практика fractional CMO/consultant — про уровень), не один.
- **Наш вывод**: использовать полностью — как структуру именно этого сравнительного раздела отчёта.
- **Если адаптируем — с чем**: с самой таблицей сверки выше — каждая строка таблицы — это про ось «содержание», отдельная строка про Advisory — про ось «вовлечённость».
- **Почему именно так**: смешение осей — конкретная ошибка, которую этот отчёт должен был не повторить: если бы Advisory сверялось против AMA/CIM (это фреймворки про содержание, не про тир контракта), вывод был бы неверным по конструкции вопроса, а не по факту.
- **Что конкретно переносим**: ✔ сама двухосевая структура сравнения; ✘ конкретные названия тиров (consultant/fractional/in-house) — они относятся к рынку США/Запада, не проверялись на русскоязычном рынке отдельно.

**Карточка 2 — Три конкретных пробела в карте способностей, ранее не названные даже как «вне scope»**

- **Назначение**: Product Strategy/NPD (AMA домен 5, 21% BOK), Pricing (AMA домен 6, 7%), и Data/Analytics-инфраструктура как отдельный актив (AMA домен 3, 15%; CIM Data & Insight) — три компетенции, которые оба независимых профессиональных эталона держат как именованные, весомые домены дисциплины, но которых нет ни внутри, ни в списке «вне scope» карты AI Marketing Strategist (`marketing_agent.md` называет вне-scope explicitly только Content Production, Distribution, Measurement — не Pricing/Product/Data-инфраструктуру).
- **Почему интересен**: разница между «осознанно исключено, названо» и «просто отсутствует, не названо» — старый документ проходит первое (Content/Distribution/Measurement названы прямо, с обоснованием), но не проходит второе для этих трёх — это не то же самое, что «неверно», это именно пробел в полноте карты, который эталон делает видимым.
- **Наш вывод**: отложить — это факт сравнения (карта неполна против эталона), не решение о том, нужно ли это добавлять; решение — Engineer/владелец.
- **Если адаптируем/объединяем — с чем**: с существующим списком «вне ядра» в `AI Marketing Strategist/HOME.md`, если владелец решит явно назвать эти три пункта (как уже названы Content Production/Distribution/Measurement), а не оставлять их немыми пробелами.
- **Почему именно так**: молчание о домене неотличимо снаружи от «забыли, что он существует» — а явное «вне scope, потому что X» (как уже сделано для Content Production) само по себе укрепляет ядро, не расширяя его.
- **Что конкретно переносим**: ✔ сам факт трёх пробелов и их источник (AMA домены 3/5/6, CIM Commercial/Data&Insight); ✘ вывод о том, что их нужно добавить в ядро — это решение не этого отчёта.

**Карточка 3 — Спор STP vs Ehrenberg-Bass как названный, не скрытый trade-off метода Positioning**

- **Назначение**: реальное, эмпирически подкреплённое разногласие в дисциплине о том, работает ли узкая STP-логика (метод Dunford, лежащий в основе способности Positioning) лучше, чем широкий mental/physical availability подход Sharp/Ehrenberg-Bass.
- **Почему интересен**: способность «Positioning & Category Definition» — одна из четырёх несущих способностей ядра, а её метод опирается на одну сторону активного, неразрешённого научного спора, о существовании которого ни `marketing_agent.md`, ни `HOME.md` не упоминают нигде.
- **Наш вывод**: объединить — не как замену метода, а как явно названный, признанный trade-off рядом с методом Dunford в описании способности (по духу правила Foundation «принцип отдельно от реализации»): «метод X, применяется с оговоркой — есть конкурирующая, эмпирически подкреплённая школа, которая с этим не согласна».
- **Если объединяем — с чем**: с `skills/marketing-strategy/references/positioning.md` в AI Marketing Strategist (файл не читался в этом расследовании — это чужой репозиторий, изменение не входит в мандат Researcher; называется здесь как адрес, не как правка).
- **Почему именно так**: называть только одну сторону реального спора как метод, без упоминания второй, — это ровно то, что `MISSION.md` требует не делать («где источники реально расходятся — сама разница, не сглаженная в один консенсус»).
- **Что конкретно переносим**: ✔ факт существования спора и его источник (Ehrenberg-Bass Institute, *How Brands Grow*); ✘ вывод о том, что метод Dunford нужно менять — не решается здесь, метод легитимен и широко используется.

---

## Источники

- `ama.org/wp-content/uploads/2019/01/ama-pcm-marketing-management-body-of-knowledge.pdf` — официальный Body of Knowledge, American Marketing Association (primary, прочитан целиком).
- `cim.co.uk/media/rz2lsf2w/thegpmf.pdf` — Global Professional Marketing Framework 2024, Chartered Institute of Marketing (primary, прочитан целиком через firecrawl-scrape того же URL после отказа WebFetch 403).
- thesocialmediahat.com, authenticbrand.com, boardroomadvisors.co, saashero.net, dashsocial.com.au, treefrogmarketing.com, mahdlo.net, growthmarketingpartner.com — независимые практикующие источники по разграничению marketing consultant / fractional CMO / in-house CMO.
- dovetail.com, umbrex.com, researchgate.net (`publication/390372931`), warc.com, thebrandgym.com — независимые разборы Byron Sharp / Ehrenberg-Bass Institute, *How Brands Grow*, и критики STP.
- spencerstuart.com — CMO Tenure Study (контекст: скоуп/бюджет/трансформация роли CMO на рынке, подтверждающая деталь, не несущий источник).
- mckinsey.com, clickz.com — CMO archetypes (подтверждающая деталь про роль/уровень вовлечённости CMO, не несущий источник).
- Вторично, некорневым источником: библиотечные каталоги ToC Kotler & Keller *Marketing Management* (structure Part 4 «Building Strong Brands» — подтверждающая деталь, не прочитан напрямую).

## Внутренний контекст, использованный без повторной проверки

- `AI Marketing Strategist/HOME.md` — текущее ядро (4 способности + Advisory), объект сверки.
- `AI_OS/specializations/marketing_agent.md` (v1.4) — легаси-источник ядра, с полной цепочкой обоснования уровня абстракции.
- `ENGINEER/knowledge/built-agents-registry.md` — запись о том, что методология AI Marketing Strategist не была сверена с Researcher (повод этого отчёта).
