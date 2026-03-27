# Capture Candidates: 2026-03-26

Черновики для Экстрактора (R2). Готовы к формализации в Pack-знания.

---

## Candidate #1: AS.FM.012 — Cascade Failures in Multi-Agent Systems

**Pack:** PACK-autonomous-agents  
**Тип:** Failure Mode  
**Статус:** Ready for capture  

**Суть:** Агент допускает ошибку в критическом действии → запускает цепную реакцию автоматических реакций других агентов/систем → ущерб обнаружен слишком поздно.

**Severity:** Критический (особенно в multi-agent environments)

**Сценарий:**
1. Агент A неправильно обрабатывает входящий запрос (email, webhook, API call)
2. Отправляет некорректный ответ/действие
3. Агент B реагирует на это действие автоматически
4. Агент C видит действия A+B и выполняет следующий шаг
5. К моменту обнаружения ошибки — нарушен SLA, потеряны деньги, испорчена репутация

**Примеры:**
- Email agent неправильно классифицировал критический запрос клиента → автоматически отправил шаблонный отказ → CRM agent закрыл тикет → billing agent приостановил подписку → клиент ушёл
- Monitoring agent ложно детектировал инцидент → escalation agent разбудил всю команду в 3am → incident response agent создал postmortem → всё оказалось false positive

**Mitigation:**
1. **Human-in-the-loop checkpoints** — для действий с финансовым/операционным/security воздействием агент ОБЯЗАН получить явное подтверждение человека
2. **Blast radius limits** — ограничивать scope автоматических действий (например: не более 5 email в минуту, не более $100 транзакций без подтверждения)
3. **Undo/rollback capabilities** — каждое автоматическое действие должно иметь механизм отката
4. **Circuit breakers** — если агент обнаружил аномальную активность (например, слишком много действий за короткое время) → автоматическая пауза + alert
5. **Audit trail** — полный лог действий для post-incident analysis

**Связь с другими FM:**
- Усиливает AS.FM.011 (Hallucination in Action) — ложная информация в действии × cascade = катастрофа
- Взаимодействует с AS.FM.009 (Loop of Death) — если cascade loop замыкается, получается бесконечный retry

**Detection:**
- Аномально высокая частота действий от связанных агентов
- Рост error rate в downstream системах
- Alerts от monitoring систем о нарушении SLA/budgets

**Источники:**
- [Vectara: Awesome Agent Failures](https://github.com/vectara/awesome-agent-failures)
- [EdStellar: AI Agent Reliability Challenges](https://www.edstellar.com/blog/ai-agent-reliability-challenges)
- [Maxim: Multi-Agent System Reliability](https://www.getmaxim.ai/articles/multi-agent-system-reliability-failure-patterns-root-causes-and-production-validation-strategies)

---

## Candidate #2: AS.FM.013 — Production Accuracy Drop (Context Rot + Tool Combination)

**Pack:** PACK-autonomous-agents  
**Тип:** Failure Mode  
**Статус:** Ready for capture  

**Суть:** Агенты в production показывают значительно более низкую accuracy по сравнению с pilot/dev средой из-за context rot и комбинирования выводов нескольких инструментов в фактически несогласованные ответы.

**Severity:** Высокий (61% компаний столкнулись с этим)

**Сценарий:**
1. В pilot/dev среде агент протестирован на небольшом наборе данных → accuracy 95%+
2. В production context window растёт (больше истории, больше инструментов, больше данных)
3. Context rot: по мере роста токенов в context window способность модели точно извлекать информацию падает
4. Tool combination error: агент комбинирует выводы Tool A и Tool B в ответ, который звучит убедительно, но фактически несогласован
5. Accuracy падает до 60-70%, но агент продолжает работать (т.к. нет явных errors)

**Примеры:**
- Customer support agent комбинирует данные из CRM (старый адрес) и Shipping API (новый адрес) → отправляет package на неправильный адрес
- Research agent извлекает факт из источника A и контекст из источника B → создаёт цитату, которой не существует в оригинале

**Root Causes:**
1. **Context rot:** LLMs have finite attention budget. Every token competes for attention. As context grows → precision drops, reasoning weakens.
2. **Tool output combination:** агент не проверяет consistency между outputs разных tools, просто собирает их в единый ответ

**Mitigation:**
1. **Independent verification layer** — для критических фактов требовать подтверждение из source-of-truth (не полагаться только на model memory)
2. **Source-of-truth anchoring** (уже есть в AS.FM.011, расширить) — каждый факт должен быть привязан к конкретному источнику
3. **Consistency checks** — перед финальным ответом проверять, что outputs всех tools logically consistent
4. **Context pruning** — агрессивно удалять irrelevant context (не держать весь history)
5. **Monitoring accuracy drift** — continuous tracking accuracy в production (не полагаться на pilot metrics)

**Detection:**
- User reports о factual inconsistencies
- Automated fact-checking против ground truth
- Comparison production accuracy vs pilot baseline

**IWE Context:**
- Scout комбинирует данные из multiple web searches → может создать "findings" с несогласованными фактами
- Mitigation: reasoning обязателен для каждой находки (source-of-truth anchor)

**Источники:**
- [EdStellar: AI Agent Reliability Challenges](https://www.edstellar.com/blog/ai-agent-reliability-challenges)
- [Sendbird: 10 Major Agentic AI Challenges](https://sendbird.com/blog/agentic-ai-challenges)

---

## Candidate #3: AS.FM.014 — Exponential Error Compounding in Multi-Step Workflows

**Pack:** PACK-autonomous-agents  
**Тип:** Failure Mode  
**Статус:** Ready for capture  

**Суть:** В multi-step workflows ошибки компаундятся экспоненциально: если каждый шаг 95% reliable → за 20 шагов success rate падает до 36%.

**Severity:** Критический для long-running agents (scheduler, pipeline agents)

**Сценарий:**
1. Агент выполняет workflow из N шагов (например: pull code → parse data → generate plan → commit → push)
2. Каждый шаг имеет reliability R (например, 95%)
3. Итоговая вероятность успеха = R^N
4. Для R=0.95, N=20: success = 0.95^20 = 0.36 (36%)
5. Агент завершает workflow в 36% случаев → 64% failures

**Математика:**
- 1 step @ 95% reliability: 95% success
- 5 steps: 0.95^5 = 77% success
- 10 steps: 0.95^10 = 60% success
- 20 steps: 0.95^20 = 36% success
- 50 steps: 0.95^50 = 8% success

**Примеры:**
- Scheduler agent (20+ шагов): git pull → WakaTime parse → fleeting-notes read → plan generate → Linear create tasks → commit → push
  - Если каждый шаг 95% reliable → only 36% успешных запусков
- Data pipeline agent (50+ шагов): extract → transform → validate → load → index → notify
  - При 95% per-step → только 8% успешных runs

**Root Causes:**
1. Независимые failure modes на каждом шаге (network error, API timeout, parsing error, etc.)
2. Отсутствие error budgets — агент не знает, когда остановиться
3. Retry на failed steps увеличивает N → ещё больше снижает итоговую reliability

**Mitigation:**
1. **Error budgets per stage** — каждая стадия workflow имеет allowed failure rate
2. **Early exit** — при первой критической ошибке останавливать весь workflow (не пытаться продолжить)
3. **Checkpointing** — сохранять промежуточное состояние → при failure можно resume с checkpoint, не начинать с нуля
4. **Increase per-step reliability** — focus на улучшение reliability каждого шага (95% → 98% → success 20 steps: 67% vs 36%)
5. **Reduce N** — минимизировать количество шагов (меньше шагов = выше итоговая reliability)
6. **Idempotency** — каждый шаг должен быть idempotent (можно retry без побочных эффектов)

**IWE Context:**
- scheduler.sh (WP-132): 20+ шагов без error budgets → vulnerable
- Нужно:
  - Checkpointing после критических шагов (git pull, WakaTime parse)
  - Early exit на первой critical error
  - Error budget: allow max 2 non-critical errors per run

**Improvement Example:**
- Improve per-step reliability 95% → 98%:
  - 20 steps: 36% → 67% success (почти 2x)
  - 10 steps: 60% → 82% success
- Reduce steps 20 → 10 @ 95%:
  - 36% → 60% success

**Источники:**
- [Maxim: Multi-Agent System Reliability](https://www.getmaxim.ai/articles/multi-agent-system-reliability-failure-patterns-root-causes-and-production-validation-strategies)
- [GetMaxim: Ensuring AI Agent Reliability](https://www.getmaxim.ai/articles/ensuring-ai-agent-reliability-in-production/)

---

## Candidate #4: AS.FM.015 — Intent Misalignment (Wrong Goal Optimization)

**Pack:** PACK-autonomous-agents  
**Тип:** Failure Mode  
**Статус:** Ready for capture  

**Суть:** Агент неправильно понимает цель пользователя и оптимизирует неправильный objective, тратя ресурсы (время, $, API calls) на нерелевантные задачи.

**Severity:** Средний (частый, но обычно не catastrophic)

**Сценарий:**
1. Пользователь даёт задачу агенту (например: "Помоги спланировать неделю")
2. Агент интерпретирует это как "создать детальный план каждого часа на 7 дней"
3. Пользователь имел в виду "выделить 3-5 ключевых приоритетов"
4. Агент тратит 30 минут (сотни API calls) на создание подробного расписания
5. Результат: пользователь получает overengineered план, который не нужен

**Примеры:**
- Research agent: "Найди информацию о X" → агент собрал 100 страниц текста, пользователь хотел 3 bullet points
- Code agent: "Fix the bug" → агент переписал весь модуль, пользователь хотел minimal patch
- Scout: "Найди SOTA по теме X" → агент принёс 50 findings, пользователь хотел TOP-3

**Root Causes:**
1. Недостаточная спецификация цели (vague instructions)
2. Отсутствие clarifying questions (агент сразу действует, не уточняя intent)
3. Default к maximalist approach (агент предполагает "больше = лучше")

**Mitigation:**
1. **Explicit goal validation loop** — перед началом работы агент подтверждает цель:
   - "Я понял задачу как X. Правильно?"
   - "Ожидаемый результат: Y. Согласны?"
2. **Scope constraints** — в инструкциях агента явные ограничения:
   - Scout: max 10 findings per session
   - Research agent: default output = summary (3-5 bullet points), not full report
3. **Progressive disclosure** — начать с минимального результата, спросить "нужно больше?"
4. **Cost budgets** — лимиты на API calls/time per task
5. **User preference learning** — запоминать, какой level of detail пользователь предпочитает

**Detection:**
- High API usage без соответствующей user satisfaction
- User feedback: "Too much", "Not what I asked for"
- Time spent >> expected for task type

**IWE Context:**
- Scout может принести слишком много findings (если нет ограничения max 10)
- Strategist может создать слишком детальный план (если пользователь хотел high-level)
- Mitigation: в каждом агенте явные scope constraints в инструкциях

**Источники:**
- [Sendbird: 10 Major Agentic AI Challenges](https://sendbird.com/blog/agentic-ai-challenges)
- [EdStellar: AI Agent Reliability Challenges](https://www.edstellar.com/blog/ai-agent-reliability-challenges)

---

## Candidate #5: AS.SOTA.003 Enrichment — Singapore IMDA Framework + WEF March 2026 Data

**Pack:** PACK-autonomous-agents  
**Тип:** SOTA enrichment  
**Статус:** Ready for capture  

**Добавить в AS.SOTA.003:**

### Singapore Model AI Governance Framework for Agentic AI (IMDA, March 2026)

Первый в мире национальный фреймворк для безопасного развёртывания автономных агентов. Анонсирован на WEF Annual Meeting 2026 в Давосе.

**Четыре ключевых области:**

1. **Assess and Bound Risks Upfront**
   - Выбор подходящих agentic use cases (не все задачи подходят для агентов)
   - Установка явных лимитов на:
     - Степень автономности (T0-T4)
     - Доступ к инструментам (tools access control)
     - Доступ к данным (data access policies)
   - Risk assessment ПЕРЕД развёртыванием (проактивно, не реактивно)

2. **Human Accountability**
   - Определение significant checkpoints — точек, где ОБЯЗАТЕЛЬНО требуется human approval
   - Humans remain meaningfully accountable for agent actions
   - Правило: агент может выполнять routine операции автономно, но critical decisions/actions требуют explicit human OK
   - Примеры checkpoints: финансовые транзакции >$X, изменение access control policies, удаление данных, отправка критически важных коммуникаций

3. **Technical Controls Throughout Lifecycle**
   - Контроли на всех стадиях: design → development → deployment → operation → retirement
   - Observability: полный audit trail всех действий агента
   - Guardrails: technical safeguards (rate limits, blast radius controls, circuit breakers)
   - Continuous monitoring для раннего обнаружения drift/degradation

4. **End-User Responsibility**
   - Transparency: пользователи должны понимать, что они взаимодействуют с агентом (не обманывать, что это человек)
   - Education/Training: обучение пользователей работе с агентами, пониманию их capabilities/limitations
   - Clear escalation paths: пользователь всегда должен иметь возможность перейти к человеку

**WEF Calibration Principle (March 2026):**
"The degree of autonomy granted to a system should be calibrated to the context in which it operates, the risks involved, and the institutional maturity of the organization deploying it."

**Gap Pilot→Production (WEF/Capgemini, March 2026):**
- 82% executives планируют adoption агентов в 1-3 года
- 79% enterprises внедрили агенты в какой-то форме
- Но только 11% запустили агенты в production
- **88% failure rate pilot→production** (основная причина: отсутствие зрелого governance)
- Те агенты, что дошли до production → average ROI 171% (US enterprises: 192%)

**Применение к IWE:**
- Scout/Strategist/Extractor сейчас на уровне T1 (supervised) — нет explicit human checkpoints
- Для перехода T1→T2 (autonomous with oversight) нужно:
  - Определить significant checkpoints (например: Scout не коммитит находки напрямую в Pack — только proposals)
  - Установить blast radius limits (Scout не может создавать >10 findings за сессию)
  - Реализовать audit trail (все действия логируются)
  - Добавить transparency (каждая находка содержит reasoning — почему Scout считает её релевантной)

**Источники:**
- [WEF: AI Agents in Action (March 2026)](https://www.weforum.org/publications/ai-agents-in-action-foundations-for-evaluation-and-governance/)
- [Singapore IMDA: New Model AI Governance Framework for Agentic AI](https://www.imda.gov.sg/resources/press-releases-factsheets-and-speeches/press-releases/2026/new-model-ai-governance-framework-for-agentic-ai)
- [WEF: From Chatbots to Assistants — Governance is Key](https://www.weforum.org/stories/2026/03/ai-agent-autonomy-governance/)

---

## Candidate #6: ECO.M.002 Enrichment — EdTech Churn 9.6%, Efficacy Reckoning, Funding Drop

**Pack:** PACK-ecosystem  
**Тип:** Method enrichment (benchmarks)  
**Статус:** Ready for capture  

**Добавить в ECO.M.002:**

**Churn Rate:**
- EdTech monthly churn: **9.6%** (highest among all B2B SaaS verticals)
- B2B SaaS average: 3.5%
- **Implication:** retention strategy = critical для EdTech unit economics. Без strong retention высокий CAC не окупится.

**CAC Payback:**
- EdTech payback period: **3.8 months** (best in class для некоторых сегментов)
- Benchmark: sustainable SaaS payback <12 months

**Market Shifts 2026:**

1. **The Efficacy Reckoning**
   - Institutional buyers и VCs больше не принимают engagement metrics как proof of value
   - Требуется verifiable evidence: продукт улучшает learning outcomes (student mastery OR teacher productivity) минимум на **10%**
   - Методы доказательства: Logic Models, third-party research, controlled studies
   - **Для IWE:** systems thinking outcomes measurable через FPF assessment framework → конкурентное преимущество

2. **Agentic AI Trend**
   - Переход от passive content delivery (courses, videos) к autonomous agentic systems
   - Agents manage student feedback, personalization, adaptive learning paths
   - **Для IWE:** ИИ-агенты (Scout, Strategist, Navigator, Extractor) = core value proposition, не bolt-on feature

**Funding Environment 2026:**
- EdTech funding drop: **86.75%** (2024: $270M/48 rounds → 2026: $35.8M/21 rounds)
- Valuation multiples compressed: **11.5x** (down from 20.9x in 2024)
- BUT: seed/Series A robust для компаний с:
  - High NRR (>106%)
  - Clear path to profitability
  - Measurable learning outcomes (Efficacy Reckoning)

**Retention Strategy Implications:**
- EdTech churn 9.6% означает средний customer lifetime ≈10 months (если linear)
- Для LTV:CAC 3:1 при CAC $1,143 → нужен LTV ≥$3,429
- При ARPU $100/мес → нужно удержать клиента минимум 34 месяца (≈3 года)
- **IWE sticky factors:**
  - Community (peer pressure, accountability)
  - Digital twin (накопленные данные, персональный контекст)
  - Персональные руководства (customization investment)
  - Pack-знания (source-of-truth, увеличивающийся со временем)

**Источники:**
- [We Are Founders: SaaS Churn & CAC 2026](https://www.wearefounders.uk/saas-churn-rates-and-customer-acquisition-costs-by-industry-2025-data/)
- [Qubit Capital: EdTech Series A Funding](https://qubit.capital/blog/edtech-series-a-pitch)
- [Tracxn: EdTech SaaS 2026 Market Trends](https://tracxn.com/d/sectors/edtech-saas/__SUiO1pLIK1e6SNm_-H12QoILRct8neyBcUR3nJfcXS0)
- [Qubit Capital: EdTech Storytelling](https://qubit.capital/blog/how-to-build-investor-trust-edtech)

---

## Candidate #7: DP.SOTA.009 — MCP Enterprise Adoption 2026

**Pack:** PACK-digital-platform  
**Тип:** SOTA (новый)  
**Статус:** Ready for capture  

#### DP.SOTA.009: MCP Enterprise Adoption 2026 — Industry Standard for AI-Data Integration

**Статус:** Industry standard (де-факто)

**Суть:**
Model Context Protocol (MCP) завершил переход от experimentation к enterprise-wide production adoption в 2026. Major vendors (OpenAI, Anthropic, Hugging Face, LangChain) стандартизировались вокруг MCP как core integration interface для AI systems.

**Market:**
- Market size: **$1.8B in 2025** (рост в 2026)
- Драйверы: highly regulated industries (healthcare, finance, manufacturing)
- OpenAI adopted MCP **March 2025** (ChatGPT desktop app)

**Architecture:**
- MCP = JSON-RPC-style bridge между AI host и tool servers
- НЕ замена для databases/scrapers — стандартизирует boundary где models meet APIs/files/automation
- Separate server processes → modularity, security isolation

**Integration Patterns:**

1. **Code Execution Pattern (2026 trend):**
   - Agents write code to discover/call tools on demand
   - Вместо upfront loading всех tool definitions (экономия context tokens)
   - Enables dynamic tool discovery

2. **Phased Implementation:**
   - Rollout gradually по stages
   - Review performance after each stage
   - Align stakeholders early (business teams)

3. **Governance First:**
   - Security/compliance/identity controls BEFORE rollout
   - Environment-based secrets (never model-accessible credentials)
   - Smallest tool surface principle

4. **Focused Tool Design:**
   - Small MCP servers → one thing well
   - Avoid monolithic servers with hundreds of tools
   - Easier testing, maintenance, security

**Future (Roadmap):**
- Long-running operations (survive disconnections/reconnections)
- Critical for enterprise workflows
- Enables time-consuming tasks without persistent connections

**IWE Context:**
- IWE MCP servers: Gmail, Calendar, DDT, Knowledge, Guides, Composer
- Architectural alignment: IWE следует focused tool design (отдельный сервер на домен)
- Knowledge Gateway (WP-187) должен следовать best practices:
  - Phased implementation (MVP → expand)
  - Security controls (env secrets, minimal tool surface)
  - Long-running ops support (для batch indexing)

**Различие от prompt engineering:**
- Prompt engineering = craft input text
- MCP = standardize integration boundary (tools, data sources, APIs)
- Context engineering (DP.SOTA.006) > prompt engineering > MCP integration

**Источники:**
- [CData: 2026 Year for Enterprise MCP Adoption](https://www.cdata.com/blog/2026-year-enterprise-ready-mcp-adoption)
- [Use Apify: MCP Standard & Ecosystem 2026](https://use-apify.com/blog/mcp-standard-ecosystem-2026)
- [Pento: A Year of MCP 2025 Review](https://www.pento.ai/blog/a-year-of-mcp-2025-review)
- [Wikipedia: Model Context Protocol](https://en.wikipedia.org/wiki/Model_Context_Protocol)

---

## Candidate #8: ECO.D.003 — Training for Skills ≠ Training for Agility

**Pack:** PACK-ecosystem  
**Тип:** Distinction (новый)  
**Статус:** Ready for capture  

#### ECO.D.003: Training for Skills ≠ Training for Agility

**Суть различения:**
Традиционный corporate training фокусируется на конкретные навыки для текущей роли. Agility training фокусируется на transferable capabilities для адаптации к изменениям.

**Сравнение:**

| Аспект | Training for Skills | Training for Agility |
|--------|---------------------|----------------------|
| **Фокус** | Конкретные навыки для current job | Transferable capabilities (systems thinking, learning how to learn) |
| **Срок жизни** | Краткосрочный (skills obsolete в 2-5 лет) | Долгосрочный (capabilities relevant across changes) |
| **ROI метрика** | Output improvement in specific role | Organizational agility (internal mobility, project speed, innovation) |
| **Вопрос** | "Did this improve output in this job?" | "Did this make the organization more agile?" |
| **Hiring стратегия** | "Hire for skills" (temporary fix) | "Train for agility" (permanent capability) |
| **Измерение** | Completion rates, skill assessments | Internal mobility, retention, innovation contributions, adaptation speed |
| **Риск** | Skills gap при изменении технологий/рынка | Capability gap при fundamental shifts |
| **Примеры** | "Python for Data Science", "Excel Advanced" | Systems thinking, problem framing, adaptive expertise |

**Контекст 2026:**
- Skills gap = не будущая угроза, а daily operational reality
- Gig-Hybrid workforce + autonomous systems → agility критична
- AI ROI depends on workforce capability: organizations с mature upskilling programs = **2x higher AI ROI**

**IWE Positioning:**
- Мы НЕ продаём courses (training for skills)
- Мы строим organizational agility через systems thinking methodology
- ROI measurement:
  - Internal mobility (люди переходят на более сложные роли внутри организации)
  - Innovation contributions (применяют системное мышление к новым проблемам)
  - Retention (agile workforce = engaged workforce)
  - AI ROI amplification (системное мышление усиливает AI capabilities)

**Failure Mode:**
- Продавать IWE как "курсы по системному мышлению" = позиционирование как skills training
- Правильно: "инфраструктура для развития организационной гибкости"

**Источники:**
- [DataCamp: AI ROI 2026](https://www.datacamp.com/blog/ai-roi-in-2026-why-workforce-capability-determines-the-return-on-ai)
- [EducationNest: ROI of Reskilling 2026](https://educationnest.com/the-roi-of-reskilling-navigating-the-2026-corporate-learning-revolution/)
- [Silicon UK: Skills That Matter 2026](https://www.silicon.co.uk/e-management/skills/the-skills-that-matter-in-2026-head-to-head-628346)
- [Myngle: New ROI of Employee Development 2026](https://blog.myngle.com/training-roi-2026-business-impact)

