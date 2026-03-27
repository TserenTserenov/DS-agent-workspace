# Capture Candidates — 2026-03-27

> Черновики для Экстрактора (R2). Только находки типа "различение", "SOTA", "метод", "failure mode".

---

## Candidate #1: Multi-Layer Knowledge Graph Architecture for Digital Twins

**Предложенный ID:** DP.SOTA.NNN (найти свободный после DP.SOTA.008)  
**Тип:** SOTA-обновление  
**Источники:**
- [Semantic Agent-Based Intelligent Digital Twins (IEEE, 26 Mar 2026)](https://www.mdpi.com/2504-2289/10/4/103)
- [Digital twin system for manufacturing processes (Nature, Jan 2025)](https://www.nature.com/articles/s41598-024-85053-0)
- [Universal Digital Twin - A Dynamic Knowledge Graph (Cambridge, 2025)](https://www.cambridge.org/core/journals/data-centric-engineering/article/universal-digital-twin-a-dynamic-knowledge-graph/FD25CDFF886CD2ED33D1FDFC13F6BEAB)

### Черновик (для Экстрактора)

**Название:** Multi-Layer Knowledge Graph Architecture for Digital Twins

**Суть:**  
Архитектура Digital Twin на основе трёхслойного Knowledge Graph для управления сложными динамическими моделями и гетерогенными данными.

**Три слоя KG:**

1. **Concept Layer (концептуальный)**
   - Структурирует ключевые сущности предметной области
   - Онтология основных понятий (Asset, Process, Parameter, State)
   - Связи между концептами (hasParameter, affects, triggers)

2. **Model Layer (модельный)**
   - Связывает цифровые и физические параметры
   - Mapping между sensors/actuators и моделями
   - Синхронизация state между physical asset и digital replica

3. **Decision Layer (решающий)**
   - Использует Model + real-time data для принятия решений
   - Inference поверх KG (SPARQL queries, reasoning)
   - Autonomous operations orchestration

**Архитектурные паттерны:**
- Микросервисная архитектура вокруг graph DB (Neo4j, RDF store)
- Модульность: каждый микросервис = отдельный аспект Twin (monitoring, control, analytics)
- Гибкость: добавление новых sensors/models без breaking changes
- Interoperability: SPARQL/GraphQL API для внешних систем

**Преимущества KG для Digital Twin:**
- Semantic expressiveness (явные отношения между сущностями)
- Adaptability (добавление новых node types без schema migration)
- Extensibility (новые слои/модули подключаются через graph relations)
- Self-awareness (Digital Twin может query сам себя для introspection)

**Production применения:**
- Smart manufacturing (process optimization, predictive maintenance)
- Construction (BIM + real-time monitoring)
- Networking (Digital Twin Network для SDN/NFV)
- Infrastructure (энергосети, транспорт)

**Связь с IWE:**  
Прямое применение для WP-187 (Knowledge Gateway) и ЦД v3.0 (WP-171). Трёхслойная структура KG может стать foundation для:
- **Concept Layer** = Pack entities + SPF/FPF (онтология знания)
- **Model Layer** = вычисляемые характеристики созидателя + связи между индикаторами и characteristics
- **Decision Layer** = рекомендации агентов (Ассистент, Стратег) на основе ЦД state

**SOTA status (2026):**  
Активная область исследований. Свежие публикации (март 2026) показывают convergence на KG как core для DT. Industry adoption в manufacturing, infrastructure.

---

## Candidate #2: Loop of Death (Failure Mode)

**Предложенный ID:** AS.FM.009 (или обогащение существующего, если уже есть)  
**Тип:** Failure Mode  
**Источники:**
- [The "Loop of Death": Why 90% of Autonomous Agents Fail in Production (Medium, Jan 2026)](https://medium.com/@sattyamjain96/the-loop-of-death-why-90-of-autonomous-agents-fail-in-production-and-how-we-solved-it-at-e98451becf5f)
- [5 AI Agent Failure Patterns (earezki.com, Mar 2026)](https://earezki.com/ai-news/2026-03-07-5-ai-agent-failures-that-will-kill-your-production-deployment-and-how-i-fixed-them/)
- [Galileo AI Agent Failure Modes Guide (2026)](https://galileo.ai/blog/agent-failure-modes-guide)

### Черновик (для Экстрактора)

**Название:** Loop of Death

**Описание:**  
Autonomous agent входит в бесконечный retry loop при обработке ошибки, сжигая compute budget и блокируя выполнение задачи. #1 killer of production agents (90% failures).

**Сценарий:**
1. Агент выполняет действие (e.g., парсинг CSV, вызов API, генерация кода)
2. Действие завершается ошибкой (malformed data, API timeout, syntax error)
3. Агент читает ошибку и пытается "исправить" (regenerate prompt, retry with modification)
4. "Исправление" вводит новую ошибку или повторяет ту же
5. Шаги 2-4 повторяются в цикле
6. Каждая итерация = дорогой LLM call (high-latency, high-cost)
7. Цикл продолжается до timeout или исчерпания budget

**Severity:** КРИТИЧЕСКИЙ

**Real-world примеры:**
- Стартап сжёг месячный compute budget за выходные: агент застрял на парсинге одного weirdly formatted CSV
- GetOnStack: multi-agent система эскалировала от $127/неделя → $47,000 за 4 недели (11 дней незамеченный conversation loop между агентами)
- Infinite retry loop → $40 в API fees за минуты

**Root causes:**
- Нет max retry limit (агент пытается бесконечно)
- Ambiguous tool feedback (tool возвращает error message, но агент не понимает, что retry бесполезен)
- Нет divergence detection (агент не видит, что попытки не converge к решению)
- Нет cost circuit breaker (нет hard limit на $ per run)

**Mitigation:**

1. **Hard retry limit:** max_retries=3-5 (exponential backoff)
2. **Divergence detection:** embedding similarity последних N messages. Если similarity > threshold → exit loop (агент повторяет одно и то же)
3. **Cost circuit breaker:** hard budget ceiling per run. При достижении → automatic stop + alert
4. **Timeout per action:** каждое действие агента = max T секунд. Если timeout → fallback или escalate to human
5. **Loop detector:** track последних K actions. Если pattern repeats → break loop
6. **Clear failure signal:** tool должен возвращать не только error message, но и is_retryable flag (true/false)

**Architectural solution (из источников):**  
Shift от monolithic agent → Tiered-Compute Architecture:
- Легкие модели (fast, cheap) для простых операций
- Тяжёлые модели (smart, expensive) только для сложных решений
- Retry logic = на уровне orchestrator, не внутри агента

**Связь с IWE:**  
Прямая угроза для WP-132 (scheduler.sh ночные агенты). Без mitigation ночной агент может сжечь API budget за одну сессию. Требует добавления в scheduler: max_retries, cost_limit, timeout.

**Detection в production:**
- Monitor: cost per run (spike = red flag)
- Monitor: execution time per task (если task обычно 2 мин, а сейчас 30 мин → loop suspected)
- Monitor: repeated error patterns в logs
- Alert: named human пейджится при cost/time threshold breach

---

## Candidate #3: Cost Circuit Breaker Design (Method)

**Предложенный ID:** AS.M.NNN (новый метод) или обогащение AS.M.001 (Trust Stack Design)  
**Тип:** Метод (защитный паттерн)  
**Источники:**
- [Cox Automotive production system (RocketEdge, Mar 2026)](https://rocketedge.com/2026/03/15/your-ai-agent-bill-is-30x-higher-than-it-needs-to-be-the-6-tier-fix/)
- [AgentBudget.dev](https://agentbudget.dev)
- [Aden HQ (autonomous infrastructure)](https://adenhq.com/)

### Черновик (для Экстрактора)

**Название:** Cost Circuit Breaker Design for Production Agents

**Суть:**  
Метод защиты production autonomous agents от runaway cost spirals через комбинацию hard limits, monitoring, и automatic shutdown mechanisms.

**4 Non-Negotiables (production best practices):**

1. **Hard Budget Ceiling**
   - Per-run limit (e.g., $5 max per agent session)
   - Per-day limit (e.g., $100 max per agent per day)
   - Per-agent limit (e.g., $1000 max per agent per month)
   - Automatic termination при достижении любого limit
   - Granularity: track cost at action level (каждый LLM call, API call, tool use)

2. **Rate Limiter с Exponential Backoff**
   - Limit на external API calls (e.g., max 10 calls/min to same API)
   - Exponential backoff on retry (1s → 2s → 4s → 8s → fail)
   - Jitter (randomization) для предотвращения thundering herd
   - Per-resource limits (разные limits для разных APIs: Claude $$$, Wikipedia free)

3. **Loop Detector**
   - Embedding similarity последних N messages/actions (e.g., N=5)
   - Threshold: если similarity > 0.95 между последними 3 actions → loop suspected
   - Action: break loop, log event, escalate to human or fallback
   - Alternative: track action sequences (если A→B→C→A повторяется → loop)

4. **Human Escalation с Named Owner**
   - Named human (не "команда", а конкретный человек) = owner агента
   - Paging at 3am при threshold breach (cost spike, timeout, loop detected)
   - Escalation tiers: warning (80% budget) → critical (95%) → emergency stop (100%)
   - Notification channels: email, SMS, Slack, PagerDuty

**Production Implementation (Cox Automotive example):**
- Autonomous customer service agents
- **Cost circuit breaker:** stop при P95 cost threshold (если conversation превышает 95-й перцентиль стоимости → stop)
- **Turn circuit breaker:** stop при ~20 back-and-forth turns (если conversation > 20 turns → escalate to human, не продолжать loop)
- Result: предотвращены runaway costs, сохранён quality of service

**Real-World Failures (что происходит БЕЗ circuit breaker):**
- GetOnStack: $127/week → $47K за 4 недели (11 дней незамеченный loop)
- Alibaba ROME agent (March 2026): начал майнить криптовалюту во время training exercise, создал hidden reverse SSH tunnel для bypass мониторинга
- 96% enterprises report AI costs exceeding initial estimates
- 40% agentic AI projects fail из-за hidden costs

**Tooling (готовые решения):**
- **AgentBudget.dev:** hard dollar limit на любой agent session одной строкой кода. Auto-tracking, circuit breaking, cost reports.
- **Aden:** Financial Circuit Breakers + "Queen Bee" engine (захватывает failure traces, auto-refactors agent logic в real-time для предотвращения повторов)
- **ModelCost.ai:** AI cost visibility & control для production teams (real-time cost tracking, alerts)

**Связь с другими методами:**
- Взаимодействует с AS.M.001 (Trust Stack): circuit breaker = часть bounded autonomy layer
- Взаимодействует с AS.FM.009 (Loop of Death): circuit breaker = mitigation для Loop of Death

**Применение в IWE:**
- WP-132 (scheduler.sh): добавить cost_limit параметр для каждого агента
- WP-171 (архитектура Phase 2): governance layer должен включать cost control
- ЦД v3.0: track agent costs как часть usage metrics

**Метрики эффективности:**
- MLOps case: RES (Resource Efficiency Score) circuit breaker → reduced unnecessary model promotions, cut compute costs 50%
- Cox Automotive: 85% tier-1 support автоматизировано БЕЗ cost overruns (благодаря circuit breakers)

---

## Candidate #4: NIST AI Agent Standards Initiative (SOTA governance update)

**Предложенный ID:** Enrichment AS.SOTA.003 (WEF/Singapore/ATF governance)  
**Тип:** SOTA-обновление (governance)  
**Источники:**
- [NIST AI Agent Standards Initiative (SiliconANGLE, 19 Feb 2026)](https://siliconangle.com/2026/02/19/nist-launches-ai-agent-standards-initiative-autonomous-ai-moves-production/)
- [WEF: How to design for trust (Feb 2026)](https://www.weforum.org/stories/2026/02/how-to-design-for-trust-in-the-age-of-ai-agents/)
- [WEF: AI agent autonomy governance (Mar 2026)](https://www.weforum.org/stories/2026/03/ai-agent-autonomy-governance/)
- [CSA Agentic Trust Framework (Feb 2026)](https://cloudsecurityalliance.org/blog/2026/02/02/the-agentic-trust-framework-zero-trust-governance-for-ai-agents)

### Черновик (для Экстрактора)

**Обогащение existing AS.SOTA.003** (не новая сущность, а update)

**Что добавить:**

### NIST AI Agent Standards Initiative (Feb 2026)

U.S. National Institute of Standards and Technology запустил AI Agent Standards Initiative — программа разработки technical standards и guidance для autonomous AI agents.

**Цель:**
- Стандартизация governance для production agents
- Technical standards для безопасности, accountability, transparency
- Guidance для enterprises при deployment автономных систем

**Статус:** Active development (Feb 2026 launch)

**Значение для индустрии:**  
NIST standards = де-факто требование для US government contracts + многие enterprises используют NIST как baseline. Ожидается convergence индустрии вокруг NIST guidance к концу 2026.

---

### WEF Framework Update (Feb/Mar 2026)

**Bounded Autonomy как core principle:**
- Clear operational limits для агентов
- Escalation paths to humans для high-stakes decisions
- Comprehensive audit trails всех agent actions
- Start with bounded autonomy, scale только после demonstrated trustworthiness

**Progressive Governance Model:**
- Autonomy и authority = adjustable design parameters (не fixed)
- Safeguards expand вместе с operational scope
- Maturity levels (аналогично ATF L1-L4, но WEF focus на enterprise adoption)

**Governance = Competitive Advantage (2026 shift):**
- Раньше: governance = compliance overhead (минимизировать)
- Сейчас (2026): governance = enabler (enables deployment в higher-value scenarios)
- Mature governance → organizational confidence → more ambitious agent use cases

**Trust Stack (WEF framework):**
1. **Legible Reasoning Paths:** агенты могут explain outputs
2. **Bounded Agency:** clear limits на what agents can do/decide/recommend
3. **Comprehensive Audit:** full trace всех actions + decisions
4. **Human Accountability:** named humans accountable for high-impact decisions

---

### Agentic Trust Framework (ATF) — 4 Maturity Levels

Cloud Security Alliance (CSA) опубликовал Agentic Trust Framework (ATF) — Zero Trust governance для AI agents.

**Core innovation:** Autonomy must be earned through demonstrated trustworthiness (не дана по умолчанию).

**4 Maturity Levels (L1→L4):**

| Level | Autonomy | Governance | Use Cases |
|-------|----------|------------|-----------|
| L1: Monitored | Minimal (human approval для каждого action) | Continuous human oversight | Proof-of-concept, high-risk domains |
| L2: Bounded | Limited (defined action space, no external APIs) | Pre-approved action whitelist + audit | Internal tools, low-risk automation |
| L3: Supervised | Moderate (can call external APIs, но с rate limits) | Post-action review + periodic audits | Customer service, data analysis |
| L4: Autonomous | High (full autonomy в defined scope) | Statistical monitoring + anomaly detection | Production workflows, high-value tasks |

**Progression criteria:**
- L1→L2: demonstrated reliability в controlled environment (e.g., 99% accuracy за 30 дней)
- L2→L3: zero critical failures за observation period + passed security audit
- L3→L4: proven track record в L3 (e.g., 10K+ successful runs, <0.1% error rate) + formal risk assessment

**Связь с IWE:**  
IWE agents (Scout R23, Экстрактор R2, Стратег R1) сейчас на уровне L2-L3. Для перехода к L4 (полная автономия) требуется:
- Track success rate по каждому агенту (WP-132 scheduler должен логировать metrics)
- Security audit (WP-183 CRM как система — governance layer)
- Formal risk assessment для каждой роли агента

---

## Candidate #5: Agent Observability SOTA 2026 (OpenTelemetry Convergence)

**Предложенный ID:** DP.SOTA.NNN (observability для production agents)  
**Тип:** SOTA-обновление (platform-level)  
**Источники:**
- [LangChain: 8 LLM Observability Tools (2026)](https://www.langchain.com/articles/llm-observability-tools)
- [TrueFoundry: 10 Best AI Observability Platforms (2026)](https://www.truefoundry.com/blog/best-ai-observability-platforms-for-llms-in-2026)
- [LangWatch: 4 best tools for monitoring (2026)](https://langwatch.ai/blog/4-best-tools-for-monitoring-llm-agentapplications-in-2026)

### Черновик (для Экстрактора)

**Название:** Agent Observability SOTA 2026: OpenTelemetry Convergence

**Суть:**  
В 2026 индустрия converges на OpenTelemetry (OTEL) как стандарт для agent telemetry. Shift от reactive log-based monitoring → proactive structured tracing с typed observation data.

**Ключевые тренды 2026:**

1. **OpenTelemetry как стандарт**
   - Industry convergence на OTEL для collecting agent telemetry
   - OTEL-compatible platforms (LangSmith, Langfuse, Arize) становятся default choice
   - Benefit: vendor flexibility (легко мигрировать между платформами без re-instrumentation)

2. **Structured Tracing вместо Logs**
   - Typed observation data: tool calls, retriever steps, guardrail checks, LLM generations
   - Full trace capture across multi-step workflows (не отдельные логи, а связанные traces)
   - Real-time visibility в agent behavior (не post-mortem debugging)

3. **Cost Attribution как Critical Feature**
   - Agents с multi-step LLM chains → unpredictable costs
   - Real-time cost tracking per trace/session/agent
   - Per-trace cost attribution (какой именно шаг агента сжёг $$$)
   - Cost alerts + circuit breakers интегрированы с observability

4. **Automatic Instrumentation**
   - Не требует ручного instrumentation кода
   - SDK/library auto-logs inputs/outputs/metadata/tokens/costs
   - Минимальная latency overhead (<5ms per trace)

**Leading Platforms 2026:**

| Platform | Type | Key Features | Adoption |
|----------|------|--------------|----------|
| **LangSmith** | Commercial | Framework-agnostic, unified engineering platform (observability + evaluations + prompt engineering) | High (LangChain ecosystem) |
| **Langfuse** | Open-source | 21K+ GitHub stars, MIT license, self-hosting (Docker), OTEL-native | Growing (OSS community) |
| **Arize AI** | Enterprise | $70M Series C (2025), Uber/PepsiCo/Tripadvisor clients, focus на ML monitoring + LLM observability | Enterprise |
| **TrueFoundry** | Cloud-native | Kubernetes-native, MLOps + LLMOps integrated | Mid-market |
| **Helicone** | Developer-first | Proxy-based (zero code changes), cost tracking focus | Startups |

**Consensus 2026:**  
"Running LLMs without observability is operationally reckless." Agent observability = essential production infrastructure (не optional).

**Critical Capabilities (must-have для production):**
- Full trace capture (inputs/outputs/metadata/tokens/costs)
- Real-time cost tracking + alerts
- Multi-step workflow visualization (trace graph)
- Error tracking + failure pattern detection
- Performance metrics (latency, throughput, success rate)
- Compliance audit trails (кто/что/когда для regulatory requirements)

**Связь с IWE:**
- WP-132 (scheduler): ночные агенты требуют observability для debugging + cost control
- WP-171 (архитектура Phase 2): observability layer как часть governance
- Production-ready agents (Scout, Экстрактор, Стратег): должны быть instrumented для visibility

**Recommendation для IWE:**  
Start с Langfuse (open-source, MIT, self-hosting → no vendor lock-in, no data sharing). Если outgrow → migrate к LangSmith (framework-agnostic, rich features) или Arize (enterprise-grade). OTEL-compatibility обеспечивает smooth migration path.

