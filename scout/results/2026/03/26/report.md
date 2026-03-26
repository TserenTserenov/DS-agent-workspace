# Scout Report — 2026-03-26

> Автоматический отчёт. Модель: sonnet. Бюджет: $10.0.
> Находок: 21 | Capture-кандидатов: 72 | WP-предложений: 0
> **Статус ревью:** ✅ проверен (26 мар, WP-170 разбор #3)

## Статус заданий (backlog)

  - id: rt-001	    title: "Реальные кейсы автономных агентов в проде"	    status: done
  - id: rt-002	    title: "SOTA методы написания текстов для соцсетей (антидетект AI)"	    status: moved_to_session
  - id: rt-003	    title: "Fundraising best practices для seed-раунда EdTech/Intelligence Platform"	    status: done
  - id: rt-004	    title: "SOTA методы бизнес-моделирования для EdTech/SaaS"	    status: done

## Находки (ТОП-21)

# Scout Report: 2026-03-26
# Priority Findings from Reconnaissance

**Status:** Complete  
**Sources scanned:** 13 web searches (arxiv, industry reports, technical blogs)  
**Time range:** Recent 2026 publications + late 2025 foundational research  
**Total findings:** 10 (ranked by strategic value)

---

## TOP-1: Context Engineering Replaces Prompt Engineering (PARADIGM SHIFT)

**Source:** Gartner 2026, SDG Group, KDnuggets, DEV Community  
**Relevance:** КРИТИЧЕСКАЯ  
**Связь:** WP-144 (autonomous agents), DP.SOTA (platform architecture), AS (agent design)

### Суть
Context engineering officially replaced prompt engineering as the dominant paradigm in 2026. 57% of organizations now have AI agents in production, but 32% cite quality as top barrier — traced to poor context management, not LLM capabilities. Gartner defines it as "programmatic assembly of the Context Package" (data, workflows, environment) enabling AI to understand intent without manual prompts.

**Core shift:** From "how you ask" (prompt) → "what information surrounds request" (schemas, files, retrieval architecture).

**Impact metrics:**
- 50% improvement in response times
- 40% higher quality outputs
- LangChain 2025 report: most failures = poor context, not model limits

### Reasoning
Rule #11: platform-level SOTA. This is NOT agent-specific method — it's architectural paradigm for entire IWE platform. Affects how ALL system components (agents, MCP servers, deterministic systems) handle information. Direct hit on WP-144 (autonomous agents v3.0) and platform modernization roadmap.

**Strategic fit:** Q2 2026 goal = 3x efficiency multiplier. Context engineering = foundation for that multiplier.

### Предложение
- **Тип:** SOTA-update (paradigm shift)
- **Куда:** PACK-digital-platform → DP.SOTA.008 "Context Engineering paradigm"
- **Действие:** Capture comprehensive framework: WISC pattern (Write/Isolate/Select/Compress), Context Package assembly, failure modes (context drift kills 65% of agents before token limits), implementation patterns for IWE

**Черновик для Экстрактора:**

```markdown
# DP.SOTA.008: Context Engineering Paradigm (2026)

**Статус:** Established (Gartner, 2026)  
**Заменяет:** Prompt engineering as primary AI interface discipline

## Суть различения
Prompt Engineering ≠ Context Engineering

| Аспект | Prompt Engineering | Context Engineering |
|--------|-------------------|---------------------|
| **Фокус** | Как спросить (wording) | Какая информация окружает запрос |
| **Единица работы** | Текст промпта | Context Package (schemas, data, retrieval) |
| **Динамика** | Статичный snapshot | Эволюционирующее состояние |
| **Scope** | Один запрос-ответ | Весь lifecycle агента |
| **Failure mode** | Плохая формулировка | Context drift, информационный голод |

## Архитектура Context Package
1. **Write:** Структурировать данные для LLM (не свалка токенов)
2. **Isolate:** Границы контекста (что релевантно сейчас)
3. **Select:** Динамический выбор источников
4. **Compress:** Минимизация без потери смысла

## Метрики эффективности (2026 benchmarks)
- Response time: +50% improvement
- Output quality: +40%
- 65% enterprise failures = context drift, не token limits

## Источники
- Gartner 2026: Context Engineering definition
- LangChain State of Agent Engineering 2025
- [Context Engineering: Why It's Replacing Prompt Engineering in 2026](https://dextralabs.com/blog/context-engineering-vs-prompt-engineering/)
```

**Sources:**
- [Context Engineering is the New Prompt Engineering in 2026](https://dextralabs.com/blog/context-engineering-vs-prompt-engineering/)
- [The Evolution of Prompt Engineering to Context Design in 2026](https://www.sdggroup.com/en/insights/blog/the-evolution-of-prompt-engineering-to-context-design-in-2026)
- [Context Engineering: Why It's Replacing Prompt Engineering in 2026](https://dev.to/serenitiesai/context-engineering-why-its-replacing-prompt-engineering-in-2026-1b4g)

---

## TOP-2: Agentic Plan Caching — 50% Cost Reduction, 27% Latency Drop

**Source:** NeurIPS 2025, arXiv 2506.14852 (updated Jan 2026)  
**Relevance:** ВЫСОКАЯ  
**Связь:** WP-144 (autonomous agents), WP-132 (scheduler.sh optimization), AS.M (methods)

### Суть
Agentic Plan Caching (APC) — test-time memory система, которая извлекает, хранит, адаптирует и переиспользует структурированные plan templates из прошлых executions для семантически похожих задач.

**Performance (production benchmarks):**
- **Cost reduction:** 50.31% в среднем
- **Latency reduction:** 27.28%
- **Quality retention:** 96.61% от оптимальной производительности
- **Overhead:** 1.04% от total serving cost (negligible)

**Mechanism:** В отличие от semantic caching (кэширует результаты), APC кэширует планы выполнения:
1. Извлекает plan template из завершённых executions
2. Использует keyword extraction для матчинга новых запросов
3. Адаптирует template через lightweight модели

### Reasoning
Rule #12: высокая ценность = конкретика + mitigation. Точные цифры production performance. Прямое попадание в WP-132 (scheduler optimization) и WP-144 (ночные агенты — там именно повторяющиеся task patterns, идеальный use case для APC).

**Strategic fit:** Q2 цель = мультипликатор 3x. APC даёт ~2x на повторяющихся задачах.

### Предложение
- **Тип:** Метод (с production benchmarks)
- **Куда:** PACK-autonomous-agents → AS.M.005 "Agentic Plan Caching"
- **Действие:** Capture как метод оптимизации test-time execution для task patterns. Связать с scheduler.sh (WP-132) — там именно repetitive tasks (daily rituals, weekly reviews).

**Черновик:**

```markdown
# AS.M.005: Agentic Plan Caching

**Источник:** NeurIPS 2025, arXiv:2506.14852  
**Статус:** Production-ready (2026)

## Проблема
Агенты при каждом похожем task-е переделывают planning с нуля → высокая latency + cost. Среднее решение GitHub issue: 48.4K tokens trajectory, 1.0M accumulated tokens.

## Решение
Test-time memory система: кэшируй структурированные планы (не результаты), адаптируй под новый контекст.

## Алгоритм
1. **Extract:** После завершения task → извлечь plan template
2. **Store:** Индексировать по keyword embeddings
3. **Match:** Новый request → keyword-based retrieval
4. **Adapt:** Lightweight LLM подгоняет template под специфику задачи

## Performance (production benchmarks)
- Cost: -50.31%
- Latency: -27.28%
- Quality: 96.61% retention
- Overhead: 1.04% (negligible)

## Use cases в IWE
- **Scheduler.sh (WP-132):** Daily/weekly rituals — одинаковые паттерны задач
- **Scout (R23):** Reconnaissance patterns (источники → findings pipeline)
- **Экстрактор (R2):** Entity extraction workflows

## Failure modes
- **Overfitting к старым планам:** Если контекст изменился, cached plan может быть субоптимальным. Mitigation: similarity threshold, expiration TTL.
- **Cold start:** Первые N executions без кэша. Mitigation: seed cache с exemplar plans.
```

**Sources:**
- [Agentic Plan Caching: Test-Time Memory for Fast and Cost-Efficient LLM Agents](https://arxiv.org/abs/2506.14852)
- [NeurIPS 2025 Poster](https://neurips.cc/virtual/2025/poster/116166)

---

## TOP-3: GEPA Performance Update — Outperforms GRPO by 6-20%, 35x Fewer Rollouts

**Source:** arXiv 2507.19457, Comet ML, ICLR 2026  
**Relevance:** СРЕДНЯЯ (обогащение accepted AS.M.001)  
**Связь:** WP-144 (autonomous agents), existing AS.M.001 (GEPA already captured)

### Суть
**НЕ НОВАЯ НАХОДКА** — GEPA уже в accepted.md (2026-03-23, AS.M.001). Новые данные: конкретные benchmarks с ICLR 2026.

**Новые метрики:**
- **HotpotQA:** GEPA 42% → 62% (6,438 rollouts) vs GRPO 24,000 rollouts → 43%
- **Across 6 tasks:** GEPA outperforms GRPO by 6% average, up to 20% on specific tasks
- **Efficiency:** 35x fewer rollouts than GRPO
- **AIME-2025:** GEPA beats MIPROv2 by +12% accuracy

**ACE comparison (новое):** ACE (конкурент GEPA) показал:
- 82.3% reduction in offline adaptation latency
- 75.1% fewer rollouts needed

### Reasoning
Rule #13: повторная тема = enrichment, не новая находка. AS.M.001 уже существует. Добавляю конкретные цифры ICLR 2026 + comparison с ACE (раньше не было). Это НЕ TOP-N finding — это enrichment для уже accepted knowledge.

### Предложение
- **Тип:** Enrichment (accepted AS.M.001)
- **Действие:** Добавить раздел "Performance Benchmarks (ICLR 2026)" в AS.M.001 с HotpotQA, AIME-2025 метриками + ACE comparison

**Sources:**
- [GEPA: Reflective Prompt Evolution Can Outperform Reinforcement Learning](https://arxiv.org/abs/2507.19457)
- [GEPA AI Optimization](https://www.comet.com/site/blog/gepa-ai-optimization/)

---

## TOP-4: LangGraph Production Deployment — 40% Enterprise Adoption, 10-15% Pilot Success Rate

**Source:** Iterathon 2026, MarkTechPost, Medium  
**Relevance:** СРЕДНЯЯ  
**Связь:** WP-144 (autonomous agents), DP (platform architecture)

### Суть
**Adoption stats (2026):**
- 40% of enterprise apps will feature task-specific agents (up from <5% in 2025)
- BUT: only 10-15% of pilots reach production
- 86% of copilot spending ($7.2B) → agent-based systems
- 75% of multi-agent systems become unmanageable beyond 5 agents

**Production-grade patterns:**
- **State management:** SQLite-based persistence, checkpoint recovery
- **Monitoring:** Human-in-the-loop checks, observability (LangSmith)
- **Architecture:** Structured message bus (LangGraph + Pydantic), ACP logging

**Failure modes:**
- Complexity explosion at 5+ agents (coordination cost)
- Lack of observability → debugging nightmare
- State loss on failures

### Reasoning
Конкретика production challenges + архитектурные паттерны. Релевантно для WP-144 (autonomous agents v3.0) — там планируется multi-agent coordination. Эти данные = input для design decisions.

### Предложение
- **Тип:** SOTA-update + production best practices
- **Куда:** AS.SOTA.003 "Multi-Agent Orchestration Production Patterns"
- **Действие:** Capture LangGraph best practices, failure modes (complexity at 5+ agents), state management patterns

**Sources:**
- [Agent Orchestration 2026: LangGraph, CrewAI & AutoGen Guide](https://iterathon.tech/blog/ai-agent-orchestration-frameworks-2026)
- [Production-Grade Multi-Agent Communication System Using LangGraph](https://www.marktechpost.com/2026/03/01/how-to-design-a-production-grade-multi-agent-communication-system-using-langgraph-structured-message-bus-acp-logging-and-persistent-shared-state-architecture/)

---

## TOP-5: AI Agent Memory Systems 2026 — 4 Memory Types, Production Challenges

**Source:** Oracle Developers Blog, 47billion, MachineLearningMastery  
**Relevance:** СРЕДНЯЯ  
**Связь:** WP-144 (autonomous agents memory), AS (agent design)

### Суть
Field converged on **4 memory types** mapping to human cognition:
1. **Working Memory:** Current context window (most agents have ONLY this)
2. **Episodic Memory:** What happened (timestamped events, conversation turns, tool calls)
3. **Semantic Memory:** What I know (facts, policies, domain knowledge)
4. **Procedural Memory:** How to do things (workflows, playbooks)

**Production challenges (2026):**
- **Storage vs Inference trade-off:** Full history = cost explosion. Solution: hierarchical memory + importance scoring + dynamic forgetting
- **Latency:** Constant retrieve/store decisions slow response
- **Forgetting:** Hardest challenge — when/what to delete?

**Database architecture patterns:**
- Vector DB: semantic similarity (weak multi-hop)
- Graph DB: fast traversal (ideal for episodic + procedural)
- SQL/Postgres: ACID compliance, auditable

**Use case (customer service):**
- 26.5% of production agents (LangChain 2025)
- Needs all 4 types: episodic (past tickets), semantic (preferences), working (live convo), procedural (resolution workflows)

### Reasoning
Comprehensive taxonomy памяти агентов + production challenges. Релевантно для WP-144 (autonomous agents v3.0 design). Сейчас в IWE memory = хаотичная (files, not structured). Эта структура = blueprint для архитектуры.

### Предложение
- **Тип:** Метод (memory architecture design)
- **Куда:** AS.M.006 "Four-Type Memory Architecture for Autonomous Agents"
- **Действие:** Capture taxonomy + implementation patterns + failure modes (forgetting, latency)

**Sources:**
- [Agent Memory: Why Your AI Has Amnesia and How to Fix It](https://blogs.oracle.com/developers/agent-memory-why-your-ai-has-amnesia-and-how-to-fix-it)
- [AI Agent Memory: Types, Implementation, Best Practices 2026](https://47billion.com/blog/ai-agent-memory-types-implementation-best-practices/)
- [Beyond Short-term Memory: The 3 Types of Long-term Memory AI Agents Need](https://machinelearningmastery.com/beyond-short-term-memory-the-3-types-of-long-term-memory-ai-agents-need/)

---

## TOP-6: Graduated Governance & Trust Stack for AI Agents

**Source:** WEF Feb 2026, Cloud Security Alliance (ATF), Microsoft Community Hub  
**Relevance:** СРЕДНЯЯ  
**Связь:** WP-144 (autonomous agents governance), AS (bounded agency design)

### Суть
Leaders implementing **layered trust stack** for agent autonomy:
1. **Legible Reasoning:** Agent explains outputs at appropriate detail
2. **Bounded Agency:** Clear limits on what agent can do/decide (no silent escalation)
3. **Goal Transparency:** User understands agent's objectives
4. **Contestability:** Override capability
5. **Governance by Design:** Embedded logging, auditability

**Agentic Trust Framework (ATF, CSA):**
- Open governance spec for autonomous agents
- Graduated maturity levels:
  - **Foundation:** Observe, report, recommend (human approval)
  - **Advanced:** Post-action notification under governance
- Zero-trust principles for agents

**Trust boundary:** Rigorously defined, measured, managed (Microsoft framework)

### Reasoning
Governance framework для autonomous agents. Релевантно для WP-144 — там designing agent roles с разной степенью автономности (R23 Scout vs R1 Strategist). ATF = structured approach для calibration автономии.

**Strategic fit:** Rule #7 не нарушен — это не новость ("X выпустил Y"), а методология governance с конкретными уровнями зрелости.

### Предложение
- **Тип:** Метод (governance framework)
- **Куда:** AS.M.007 "Graduated Governance for Agent Autonomy"
- **Действие:** Capture Trust Stack + ATF maturity levels, связать с AS.D.007 (autonomy distinctions)

**Sources:**
- [How to design for trust in the age of AI agents](https://www.weforum.org/stories/2026/02/how-to-design-for-trust-in-the-age-of-ai-agents/)
- [Agentic Trust Framework: Zero Trust for AI Agents](https://cloudsecurityalliance.org/blog/2026/02/02/the-agentic-trust-framework-zero-trust-governance-for-ai-agents)

---

## TOP-7: EdTech B2B SaaS Benchmarks 2026 — Churn 9.6%, CAC $1,143, NRR >106%

**Source:** Data-Mania, Proven SaaS, WeAreFounders  
**Relevance:** ВЫСОКАЯ  
**Связь:** WP-145 (fundraising deck), ECO (ecosystem business model)

### Суть
**EdTech-specific metrics (2026):**
- **Churn:** 9.6% monthly (highest among SaaS verticals, 38x difference vs enterprise 0.25%)
- **CAC:** $1,143 average (but education segment: $42 with 3.8mo payback — fast profitability)
- **Expansion revenue:** 40% of new ARR (NRR >106% = 2.5x faster growth)
- **LTV:CAC:** >3:1 (healthy)
- **CAC payback:** Median 6.8mo (EdTech segment: 3.8mo best-in-class)

**Conversion rates:**
- Visitor-to-trial: 10.3% (EdTech)
- MQL-to-SQL: 40% (B2B SaaS average)

**Market reality:**
- Seed-to-Series A graduation: 41% (Q3 2020) → 12% (Q1 2023)
- Focus shift: potential → proof (traction, leadership, capital efficiency)

### Reasoning
Конкретные benchmarks для WP-145 (fundraising deck v0.3). Использовано частично (churn, CAC), но expansion revenue 40% и NRR >106% = новая информация. Можно обогатить слайд 10 (unit economics).

**Strategic fit:** Q2 2026 goal = fundraising prep. Эти метрики = ammunition для deck.

### Предложение
- **Тип:** Метрика (industry benchmarks)
- **Куда:** ECO.M.002 (business model benchmarks), use in WP-145
- **Действие:** Update deck v0.3 slide 10 с expansion revenue + NRR benchmarks

**Sources:**
- [SaaS Churn Rates and Customer Acquisition Costs by Industry: 2026 Benchmarks](https://www.wearefounders.uk/saas-churn-rates-and-customer-acquisition-costs-by-industry-2025-data/)
- [CAC Benchmarks for B2B Tech Startups 2026](https://www.data-mania.com/blog/cac-benchmarks-for-b2b-tech-startups-2025/)

---

## TOP-8: World Models for Embodied AI — ICLR 2026 Workshop, Genie 3, Cosmos 2M Downloads

**Source:** ICLR 2026 Workshop, arXiv surveys (2510.16732), Introl Blog  
**Relevance:** НИЗКАЯ (outside IWE scope, но технологический тренд)  
**Связь:** Косвенно к AS (future agent architectures)

### Суть
World models = internal simulators для embodied agents, enabling:
- Forward/counterfactual rollouts
- Physics simulation
- Agent planning without real-world interaction

**2026 developments:**
- Google DeepMind: Genie 3 (first real-time interactive world model, 24 fps, persistent 3D environments)
- NVIDIA Cosmos: 2M downloads
- Fei-Fei Li's World Labs: Marble release

**Research focus (ICLR 2026 workshop):**
- Scalable engines for dynamic interaction modeling
- Intersection: generative modeling, RL, computer vision, robotics

### Reasoning
Технологический тренд, но IWE = не embodied AI (нет роботов, физических агентов). World models могут быть релевантны для future agent architectures (симуляция последствий действий), но сейчас = outside scope.

**Решение:** Отметить как тренд, но НЕ capture в Pack (not actionable for IWE roadmap 2026).

---

## TOP-9: MCP (Model Context Protocol) — Industry Standard, 40% Enterprise Adoption Goal

**Source:** Wikipedia, Anthropic Skilljar, Pento Blog, OneReach  
**Relevance:** СРЕДНЯЯ  
**Связь:** DP (MCP servers already in use), platform architecture

### Суть
MCP donated to Agentic AI Foundation (AAIF, Linux Foundation) в Dec 2025. Co-founded by Anthropic, Block, OpenAI.

**2026 status:**
- De facto protocol для connecting AI systems to real-world data/tools
- Gartner prediction: 40% of enterprise apps with AI agents by end of 2026 (up from <5%)
- Adopted by OpenAI, Google DeepMind, Microsoft, thousands of developers

**Core primitives:**
- Tools (model-controlled)
- Resources (app-controlled)
- Prompts (user-controlled)

**Architecture:** JSON-RPC 2.0, inspired by Language Server Protocol (LSP)

### Reasoning
MCP уже используется в IWE (MCP servers для Gmail, Calendar, Digital Twin). Эта информация = подтверждение правильности выбора (industry standard). Новизна = donation к AAIF (governance shift), но не влияет на текущую архитектуру.

**Решение:** Обогатить DP.SOTA (MCP adoption data), но НЕ новая сущность.

---

## TOP-10: Multi-Agent Coordination Cost — 45% Process Hand-off Reduction, 3x Decision Speed

**Source:** Kanerika, Codebridge, IBM Research  
**Relevance:** СРЕДНЯЯ  
**Связь:** WP-144 (autonomous agents), DP (platform coordination)

### Суть
**Coordination challenge:** As agents increase, interaction count increases rapidly → coordination cost explodes, learning/decision-making slows.

**Mitigation strategies:**
- **Intelligent routing:** Cost optimization (different models for different complexity)
- **Team size limits:** 3-7 agents per workflow, hierarchical beyond that
- **Centralized vs decentralized:** Supervisor pattern (clear control, potential bottleneck) vs autonomous (flexibility, complexity)

**Performance gains (IBM research):**
- Process hand-offs: -45%
- Decision speed: 3x improvement

**Economic impact:** McKinsey estimates generative AI could add $2.6-4.4T annually to global GDP.

### Reasoning
Coordination cost = known problem (already captured in DP.SOTA.006). Новые данные: IBM research metrics (45% reduction, 3x speed). Обогащение, не новая находка.

---

## SUMMARY STATISTICS

**Total findings:** 10  
**Critical priority:** 1 (Context Engineering paradigm shift)  
**High priority:** 2 (Agentic Plan Caching, EdTech benchmarks)  
**Medium priority:** 6  
**Low priority:** 1 (World Models — outside scope)

**Enrichments (not new findings):** 2 (GEPA benchmarks, MCP adoption data)

**Strategic alignment:**
- WP-144 (autonomous agents): 7 findings
- WP-145 (fundraising): 1 finding
- DP (platform architecture): 4 findings
- ECO (business model): 1 finding

**Recommended immediate actions:**
1. Capture Context Engineering paradigm (DP.SOTA.008) — блокирующее для platform modernization
2. Evaluate Agentic Plan Caching для scheduler.sh (WP-132) — potential 2x efficiency gain на repetitive tasks
3. Update fundraising deck v0.3 с EdTech NRR/expansion revenue benchmarks (slide 10)


## Capture-кандидаты

> Решение: ✅ принять → Экстрактор формализует в Pack | ❌ отклонить → trajectory | 🔄 доработать → backlog

# Capture Candidates for Extractor (R2)
# Scout → Extractor pipeline: черновики для формализации в Pack-knowledge

**Date:** 2026-03-26  
**Scout run:** morning reconnaissance  
**Total candidates:** 7

---

## CANDIDATE #1: Context Engineering Paradigm (DP.SOTA.008)

**Pack:** PACK-digital-platform  
**Type:** SOTA-update (paradigm shift)  
**Priority:** КРИТИЧЕСКАЯ

### Предварительная формулировка

```markdown
---
id: DP.SOTA.008
type: sota
title: Context Engineering Paradigm
status: established
source: Gartner 2026, LangChain State of Agent Engineering 2025
date: 2026
replaces: Prompt engineering as primary AI interface discipline
---

# Context Engineering Paradigm

## Суть различения

**Prompt Engineering ≠ Context Engineering**

Prompt engineering фокусируется на "как спросить" (wording of instruction).  
Context engineering фокусируется на "какая информация окружает запрос" (data architecture).

| Аспект | Prompt Engineering | Context Engineering |
|--------|-------------------|---------------------|
| **Единица работы** | Текст промпта (статичный) | Context Package (динамический) |
| **Scope** | Один запрос-ответ | Весь lifecycle агента/системы |
| **Компоненты** | Instruction + examples | Schemas, data sources, retrieval architecture, workflows |
| **Динамика** | Snapshot at inference time | Evolving state across interactions |
| **Failure mode** | Плохая формулировка → плохой ответ | Context drift → degradation over time |
| **Масштабируемость** | Не масштабируется (каждый промпт = ручная работа) | Масштабируется (программируемая архитектура) |

## Определение (Gartner 2026)

> Context engineering is designing and structuring the relevant data, workflows and environment so AI systems can understand intent, make better decisions and deliver contextual, enterprise-aligned outcomes — without relying on manual prompts.

Context Engineering = programmatic assembly of "Context Package" — точный bundle токенов, отправляемых LLM at inference time.

## Архитектура Context Package

**WISC pattern** (Write/Isolate/Select/Compress):

1. **Write:** Структурировать данные для LLM  
   - Не "свалка токенов", а schemas, metadata, typed information
   
2. **Isolate:** Определить границы контекста  
   - Что релевантно для текущей задачи (scope control)
   
3. **Select:** Динамический выбор источников информации  
   - Retrieval architecture, source prioritization
   
4. **Compress:** Минимизация токенов без потери смысла  
   - Summarization, deduplication, context window management

## Почему смена парадигмы произошла в 2026

**Adoption stats:**
- 57% organizations have AI agents in production (LangChain 2025)
- 32% cite quality as top barrier
- Root cause analysis: failures traced to poor context management, NOT LLM capabilities

**Context drift kills agents:**
- 65% of enterprise AI failures (2025) = context drift or memory loss during multi-step reasoning
- NOT raw context window exhaustion

## Production performance (2026 benchmarks)

Organizations investing in context architectures report:
- **Response time:** +50% improvement
- **Output quality:** +40% higher
- **ROI:** Measurable, justifies AI investments

## Ключевое различение от prompt engineering

Prompt engineering treats AI as chatbot (needs clever instructions).  
Context engineering treats AI as reasoning engine (needs comprehensive information architecture).

## Failure modes

### FM.001: Context Drift
**Severity:** Критический  
**Scenario:** Агент в multi-step reasoning теряет релевантную информацию из более ранних шагов → решения становятся субоптимальными или неверными.  
**Mitigation:**
- Hierarchical memory (working + episodic + semantic)
- Importance scoring (что хранить, что забыть)
- Periodic context refresh

### FM.002: Information Starvation
**Severity:** Средний  
**Scenario:** Context Package недостаточен → агент hallucinating или asking for missing info on every step.  
**Mitigation:**
- Pre-analysis requirements (какие источники нужны)
- Proactive data injection
- Dynamic source expansion

### FM.003: Token Budget Explosion
**Severity:** Средний  
**Scenario:** Context Package слишком велик → latency + cost escalation.  
**Mitigation:**
- Compression strategies (summarization, deduplication)
- Lazy loading (fetch on-demand)
- Tiered context (core + extended)

## Связь с другими сущностями Pack'ов

- **DP.SOTA.006:** Coordination cost reduction → context engineering снижает coordination overhead (agents share structured context, not free-form text)
- **AS.M.001 (GEPA):** Reflective optimization → context = learning signal (не scalar reward)
- **AS.M.005 (Agentic Plan Caching):** Caching требует structured context для similarity matching

## Источники

1. Gartner (2026): "Context engineering: Why it's Replacing Prompt Engineering for Enterprise AI Success"  
   URL: https://www.gartner.com/en/articles/context-engineering

2. LangChain (2025): "State of Agent Engineering" report  
   57% production adoption, 32% quality barrier = poor context management

3. SDG Group (2026): "The Evolution of Prompt Engineering to Context Design in 2026"  
   URL: https://www.sdggroup.com/en/insights/blog/the-evolution-of-prompt-engineering-to-context-design-in-2026

4. DEV Community (2026): "Context Engineering: Why It's Replacing Prompt Engineering in 2026"  
   URL: https://dev.to/serenitiesai/context-engineering-why-its-replacing-prompt-engineering-in-2026-1b4g
```

---

## CANDIDATE #2: Agentic Plan Caching (AS.M.005)

**Pack:** PACK-autonomous-agents  
**Type:** Method  
**Priority:** ВЫСОКАЯ

### Предварительная формулировка

```markdown
---
id: AS.M.005
type: method
title: Agentic Plan Caching
status: production-ready
source: NeurIPS 2025, arXiv:2506.14852
date: 2026-01
---

# Agentic Plan Caching (APC)

## Проблема

Autonomous agents при каждом похожем task-е переделывают planning с нуля:
- Высокая latency (re-planning overhead)
- Высокий cost (LLM calls for planning on every execution)
- Inefficiency на repetitive tasks

**Example:** Среднее решение GitHub issue через агента:
- Trajectory: 48.4K tokens в 40 шагов
- Accumulated token usage: 1.0M tokens per issue

## Решение

**Test-time memory система:** Extract, store, adapt, reuse structured plan templates.

**Key distinction:** Semantic caching vs Plan caching

| Аспект | Semantic Caching | Agentic Plan Caching |
|--------|------------------|---------------------|
| **Что кэшируется** | Результаты (outputs) | Планы выполнения (plans) |
| **Когда применимо** | Идентичные запросы | Семантически похожие задачи |
| **Адаптация** | Нет (используется as-is) | Да (template → specific plan) |
| **Scope** | Single-turn | Multi-step execution |

## Алгоритм

### Phase 1: Plan Extraction
После завершения task execution:
1. Analyze completed trajectory
2. Extract abstract plan structure (steps, dependencies, decision points)
3. Remove task-specific details → template

### Phase 2: Plan Storage
1. Index plan template by:
   - Keyword embeddings (task description)
   - Structural features (plan complexity, step count)
2. Store in plan cache with metadata (success rate, average execution time)

### Phase 3: Plan Matching
При новом task request:
1. Keyword-based retrieval (top-K similar plans)
2. Structural similarity check (is plan architecture applicable?)
3. Select best match

### Phase 4: Plan Adaptation
1. Lightweight LLM reads:
   - Cached plan template
   - New task specifics
2. Adapts template:
   - Fill task-specific parameters
   - Adjust constraints
   - Modify step details
3. Output: Task-specific plan (ready for execution)

## Performance (Production Benchmarks, 2026)

**Metrics across diverse agentic applications:**
- **Cost reduction:** 50.31% в среднем
- **Latency reduction:** 27.28%
- **Quality retention:** 96.61% от optimal performance (no caching)
- **Overhead:** 1.04% от total serving cost (negligible)

**Efficiency gain:** ~2x на повторяющихся task patterns.

## Use Cases в IWE

### 1. Scheduler.sh (WP-132)
**Task patterns:**
- Daily rituals (morning review, planning)
- Weekly reviews (reflection, next week planning)
- Monthly retrospectives

**Benefit:** Одинаковые структуры планов → APC даст ~2x speedup.

### 2. Scout (R23) — Reconnaissance
**Task pattern:**
- Source scan → findings extraction → relevance assessment → capture candidates
- Повторяется каждую ночь

**Benefit:** Plan для reconnaissance pipeline кэшируется, адаптируется под новые sources.

### 3. Экстрактор (R2) — Entity Extraction
**Task pattern:**
- Read capture candidate → identify entity type → extract fields → format as Pack entity
- Повторяется для каждого candidate

**Benefit:** Plan template per entity type (Distinction, Method, SOTA, FM).

## Failure Modes

### FM.001: Overfitting to Cached Plan
**Severity:** Средний  
**Scenario:** Context изменился (новый тип задачи, другие constraints), но cached plan всё ещё матчится → субоптимальное выполнение.  
**Mitigation:**
- Similarity threshold (reject если similarity < 0.7)
- Expiration TTL (cache invalidation after N days)
- Performance monitoring (if adapted plan performs poorly, invalidate cache entry)

### FM.002: Cold Start Problem
**Severity:** Низкий  
**Scenario:** Первые N executions нового task type → no cached plans → нет speedup.  
**Mitigation:**
- Seed cache с exemplar plans (pre-populate для known task types)
- Fast learning (после 1-2 executions уже есть plan template)

### FM.003: Cache Pollution
**Severity:** Низкий  
**Scenario:** Неудачные executions попадают в cache → последующие tasks адаптируются из bad plans.  
**Mitigation:**
- Quality filter (кэшируй только successful executions)
- Success rate tracking (evict plans с low success rate)

## Сравнение с другими методами

### vs AgentDiet (Trajectory Reduction)
- **AgentDiet:** Reduce trajectory content (remove useless/redundant info)
- **APC:** Cache plans (avoid re-planning)
- **Complementary:** Can be combined (reduce + cache)

### vs TrajTune (Trajectory-Based Prompt Optimization)
- **TrajTune:** Optimize prompts based on execution traces
- **APC:** Cache and reuse plans
- **Difference:** TrajTune = offline optimization, APC = online reuse

## Связь с другими сущностями Pack'ов

- **DP.SOTA.008 (Context Engineering):** APC requires structured context для plan matching
- **AS.M.001 (GEPA):** GEPA optimizes plans through reflection; APC reuses optimized plans
- **DP.SOTA.006 (Coordination Cost):** APC снижает coordination overhead (agents share cached plans)

## Источники

1. arXiv:2506.14852 (updated Jan 2026): "Agentic Plan Caching: Test-Time Memory for Fast and Cost-Efficient LLM Agents"  
   URL: https://arxiv.org/abs/2506.14852

2. NeurIPS 2025 Poster: "Agentic Plan Caching"  
   URL: https://neurips.cc/virtual/2025/poster/116166

3. OpenReview (2025): Discussion and reviews  
   URL: https://openreview.net/forum?id=n4V3MSqK77
```

---

## CANDIDATE #3: Four-Type Memory Architecture for Autonomous Agents (AS.M.006)

**Pack:** PACK-autonomous-agents  
**Type:** Method (memory architecture design)  
**Priority:** СРЕДНЯЯ

### Предварительная формулировка

```markdown
---
id: AS.M.006
type: method
title: Four-Type Memory Architecture for Autonomous Agents
status: production-converged
source: Oracle Developers Blog, 47billion, CoALA framework
date: 2026
---

# Four-Type Memory Architecture for Autonomous Agents

## Проблема

Most agents today have ONLY working memory (current context window).

> "That's like trying to do your job using nothing but a whiteboard that gets wiped clean every evening."

**Production failures (2026):**
- Agents forget user preferences across sessions
- Repeat mistakes (no learning from past errors)
- Cannot build domain expertise over time
- Inefficient (re-learn procedures on every task)

## Решение

Field converged on **4 memory types**, mapping to human cognition (CoALA framework):

1. **Working Memory**
2. **Episodic Memory**
3. **Semantic Memory**
4. **Procedural Memory**

## Архитектура

### 1. Working Memory

**Суть:** Current context window  
**Содержимое:** Live conversation, active task state, temporary variables  
**Lifetime:** Single session (wiped on termination)  
**Характеристика:** Fast access, limited capacity

**Аналогия:** Whiteboard — short-term scratchpad.

### 2. Episodic Memory

**Суть:** What happened (timestamped events)  
**Содержимое:**
- Conversation turns
- Tool invocations
- API results
- User corrections
- Failures and successes

**Lifetime:** Long-term (queryable timeline)  
**Характеристика:** Chronological, context-rich

**Аналогия:** Diary — "I remember when..."

**Query patterns:**
- "What did user ask last Tuesday?"
- "When did this error first occur?"
- "What was the outcome of previous similar task?"

### 3. Semantic Memory

**Суть:** What I know (stable knowledge)  
**Содержимое:**
- Facts
- Policies
- Domain definitions
- Product knowledge
- Business rules
- Reference information

**Lifetime:** Long-term (evolves slowly)  
**Характеристика:** Declarative, structured

**Аналогия:** Encyclopedia — domain knowledge base.

**Query patterns:**
- "What is company policy on X?"
- "What are product features of Y?"
- "What does term Z mean in this domain?"

### 4. Procedural Memory

**Суть:** How to do things (workflows)  
**Содержимое:**
- Standard operating procedures
- Playbooks
- Action sequences
- Policy-driven processes
- Repeated operational patterns

**Lifetime:** Long-term (improves with experience)  
**Характеристика:** Executable, pattern-based

**Аналогия:** Recipe book — "Here's how I do X."

**Query patterns:**
- "How do I resolve ticket type A?"
- "What's the workflow for onboarding?"
- "What steps did I take last time this happened?"

## Production Use Case: Customer Service

**Context:** Customer service = most common use case for production agents (26.5% of deployments, LangChain 2025)

**Memory requirements:** Needs ALL 4 types working together.

| Memory Type | Role in Customer Service |
|-------------|-------------------------|
| **Working** | Track live conversation (current issue) |
| **Episodic** | Recall past tickets, interactions with this customer |
| **Semantic** | Store customer preferences, account details, product knowledge |
| **Procedural** | Encode resolution workflows, escalation rules |

**Without 4-type memory:**
- Agent asks same questions every session (no episodic)
- Doesn't know customer preferences (no semantic)
- Inefficient resolution (no procedural patterns)

## Database Architecture Patterns

Разные типы памяти → разные database strengths:

| Memory Type | Best Database | Why |
|-------------|---------------|-----|
| **Working** | In-memory (Redis) | Fast access, temporary |
| **Episodic** | Graph DB (Neo4j) | Fast traversal, relationships (event → event) |
| **Semantic** | Vector DB (Pinecone, Weaviate) | Semantic similarity search |
| **Procedural** | Graph DB or SQL | Workflow dependencies, ACID compliance |

**Unified approach (2026 trend):**
- One database connection for complete context windows
- ACID guarantees across memory types
- Single query spans episodic + semantic + procedural

**Example (Postgres):**
- Episodic: Timestamped events table
- Semantic: JSON/JSONB columns for facts
- Procedural: Stored procedures or workflow tables
- Vector extension (pgvector) for semantic search

## Challenges and Mitigations

### Challenge #1: Storage vs Inference Trade-off
**Problem:** Full history = cost explosion  
**Mitigation:**
- Hierarchical memory (hot vs cold storage)
- Importance scoring (what to keep, what to archive)
- Dynamic forgetting (time-based decay, relevance-based eviction)

### Challenge #2: Latency
**Problem:** Constant retrieve/store decisions slow response  
**Mitigation:**
- Lazy loading (fetch on-demand)
- Prefetching (predict what will be needed)
- Caching layer (frequently accessed memories)

### Challenge #3: Forgetting
**Problem:** When/what to delete? (hardest challenge, 2026)  
**Mitigation:**
- Automated decay functions (temporal forgetting)
- Relevance-based pruning (low-importance → archive)
- User-controlled retention policies (regulatory compliance)

## Memory Tools and Frameworks (2026)

### LangMem
- Native integration as long-term memory layer
- Supports semantic, episodic, procedural types
- Handles fact extraction + behavior-level memory

### Mem0, Zep, Hindsight
- Production memory systems with different trade-offs
- Comparison: Mem0 (ease of use), Zep (performance), Hindsight (customization)

## Failure Modes

### FM.001: Memory Pollution
**Severity:** Средний  
**Scenario:** Agent stores incorrect facts or failed procedures → contaminates future decisions.  
**Mitigation:**
- Validation before storage (don't memorize hallucinations)
- Confidence scoring (low-confidence memories = tentative)
- Correction mechanism (user can fix stored memories)

### FM.002: Memory Overload
**Severity:** Средний  
**Scenario:** Agent accumulates too much → retrieval becomes slow, relevance drops.  
**Mitigation:**
- Periodic cleanup (archive old episodic memories)
- Importance-based eviction (keep high-value, discard low-value)

### FM.003: Context Window Starvation
**Severity:** Критический  
**Scenario:** Working memory filled with retrieved long-term memories → no space for current task.  
**Mitigation:**
- Summarization (compress retrieved memories)
- Tiered retrieval (fetch headlines first, details on-demand)

## Связь с другими сущностями Pack'ов

- **DP.SOTA.008 (Context Engineering):** Memory architecture = foundation for Context Package assembly
- **AS.M.005 (Agentic Plan Caching):** Procedural memory stores cached plans
- **AS.M.001 (GEPA):** Episodic memory = full execution traces for reflection

## Источники

1. Oracle Developers Blog (2026): "Agent Memory: Why Your AI Has Amnesia and How to Fix It"  
   URL: https://blogs.oracle.com/developers/agent-memory-why-your-ai-has-amnesia-and-how-to-fix-it

2. 47billion (2026): "AI Agent Memory: Types, Implementation, Best Practices 2026"  
   URL: https://47billion.com/blog/ai-agent-memory-types-implementation-best-practices/

3. MachineLearningMastery (2026): "Beyond Short-term Memory: The 3 Types of Long-term Memory AI Agents Need"  
   URL: https://machinelearningmastery.com/beyond-short-term-memory-the-3-types-of-long-term-memory-ai-agents-need/

4. LangChain (2025): "State of Agent Engineering" — customer service use case (26.5%)
```

---

## CANDIDATE #4: Graduated Governance for Agent Autonomy (AS.M.007)

**Pack:** PACK-autonomous-agents  
**Type:** Method (governance framework)  
**Priority:** СРЕДНЯЯ

### Предварительная формулировка

```markdown
---
id: AS.M.007
type: method
title: Graduated Governance for Agent Autonomy
status: emerging-standard
source: WEF Feb 2026, Cloud Security Alliance (ATF)
date: 2026-02
---

# Graduated Governance for Agent Autonomy

## Проблема

Autonomous agents с неограниченной автономией = high risk:
- Silent escalation of authority (agent делает больше, чем разрешено)
- Opaque decision-making (user не понимает, почему агент сделал X)
- Governance gaps (нет audit trail, accountability)

**Production challenge:** How to safely increase agent autonomy from "recommend actions" to "take actions autonomously"?

## Решение

**Layered Trust Stack** (WEF 2026) + **Agentic Trust Framework** (ATF, Cloud Security Alliance)

Graduated approach: агент проходит maturity levels с чёткими критериями и контролями на каждом уровне.

## Trust Stack Architecture (5 Layers)

### Layer 1: Legible Reasoning
**Requirement:** Agent explains outputs at appropriate detail level.  
**Control:** Reasoning traces available for inspection (not black box).  
**User capability:** "Why did you do X?" → agent provides justification.

### Layer 2: Bounded Agency
**Requirement:** Clear limits on what agent can do/decide/recommend.  
**Control:** No silent escalation of autonomy.  
**Mechanism:**
- Permission model (read vs write vs execute)
- Scope boundaries (what domains agent can operate in)
- Approval gates (certain actions require human confirmation)

### Layer 3: Goal Transparency
**Requirement:** User understands agent's objectives.  
**Control:** Agent declares its goals upfront.  
**Example:** "My goal is to optimize X within constraints Y, Z."

### Layer 4: Contestability & Override
**Requirement:** User can challenge agent's decisions and override.  
**Control:** Rollback capability, manual intervention.  
**Mechanism:**
- Undo action (if reversible)
- Stop execution (if in-progress)
- Correct agent (if mistaken)

### Layer 5: Governance by Design
**Requirement:** Embedded logging, auditability.  
**Control:** All agent actions logged with context.  
**Audit trail:**
- What action taken
- When
- Why (reasoning)
- Who authorized (user or policy)

## Agentic Trust Framework (ATF) — Graduated Maturity Levels

**ATF = open governance specification** for autonomous agents (CSA, Feb 2026).

| Level | Name | Autonomy | Human Role | Controls |
|-------|------|----------|-----------|----------|
| **0** | Manual | None | Performs all actions | Agent observes only |
| **1** | Observe & Report | Minimal | Reviews reports, decides | Logging, monitoring |
| **2** | Recommend | Low | Approves actions | Pre-action approval gate |
| **3** | Act with Notification | Medium | Post-action review | Audit trail, rollback |
| **4** | Act Autonomously | High | Exception handling only | Governance policies, circuit breakers |

### Level 1: Foundation (Observe & Report)
**Agent capabilities:**
- Observe environment (read access)
- Analyze data
- Report findings
- Recommend actions (human approval required)

**Controls:**
- No write access
- No execution authority
- Logging of all observations

**Use case:** Scout (R23) в текущей форме — reconnaissance only, no writes.

### Level 2: Assisted (Recommend with Approval)
**Agent capabilities:**
- + Propose specific actions
- + Provide reasoning
- Human approves before execution

**Controls:**
- Pre-action approval gate (explicit user confirmation)
- Action preview (show what will happen)

**Use case:** Экстрактор (R2) — предлагает entity captures, пользователь утверждает.

### Level 3: Supervised (Act with Notification)
**Agent capabilities:**
- + Execute actions autonomously
- Post-action notification (user informed after)

**Controls:**
- Bounded scope (only certain actions allowed)
- Audit trail (all actions logged)
- Rollback capability

**Use case:** Scheduler.sh (WP-132) — автоматически создаёт daily plan, уведомляет пользователя.

### Level 4: Autonomous (Act Independently)
**Agent capabilities:**
- + Full execution authority within domain
- + Exception handling
- Human intervention only for edge cases

**Controls:**
- Governance policies (embedded rules)
- Circuit breakers (stop if anomaly detected)
- Periodic review (human audits performance)

**Use case:** Future R1 (Strategist) с delegation authority для tactical decisions.

## Progression Criteria (How to Graduate to Next Level)

**Level 1 → 2:**
- Demonstrate reliable observation (low false positive rate)
- Recommendations consistently aligned with user intent

**Level 2 → 3:**
- High approval rate (>90% of recommendations accepted)
- No significant errors in past N executions

**Level 3 → 4:**
- Post-action interventions rare (<5%)
- Trust earned over time (track record)
- Governance policies validated

## Trust Boundary (Microsoft Framework, 2026)

**Definition:** Rigorously defined, measured, managed perimeter of agent authority.

**Components:**
1. **Inputs:** What data agent can access
2. **Outputs:** What actions agent can take
3. **Environment:** Where agent operates (sandbox vs production)
4. **Audit:** How actions are logged and reviewed

**Measurement:**
- Boundary violations (attempted unauthorized actions)
- Escalation requests (agent asks for permission)
- Override frequency (how often human intervenes)

## Failure Modes

### FM.001: Silent Escalation
**Severity:** Критический  
**Scenario:** Agent начинает делать больше, чем разрешено, без уведомления пользователя.  
**Mitigation:**
- Explicit permission model (check before every action)
- Logging всех попыток выхода за границы
- Alert на boundary violations

### FM.002: Brittle Governance
**Severity:** Средний  
**Scenario:** Governance rules слишком строгие → agent blocked на легитимных действиях.  
**Mitigation:**
- Adaptive policies (learn from override patterns)
- Graduated exceptions (user can grant one-time permissions)

### FM.003: Audit Fatigue
**Severity:** Низкий  
**Scenario:** Слишком много логов → человек перестаёт их проверять.  
**Mitigation:**
- Summarization (highlight anomalies, not routine actions)
- Anomaly detection (AI reviews AI — meta-oversight)

## Связь с другими сущностями Pack'ов

- **AS.D.007 (Bounded Agency ≠ Automation):** Trust Stack implements bounds на agent autonomy
- **DP (Platform Architecture):** Permission model, audit trail = platform services
- **VR (Verification & Acceptance):** Post-action review = verification step

## Источники

1. World Economic Forum (Feb 2026): "How to design for trust in the age of AI agents"  
   URL: https://www.weforum.org/stories/2026/02/how-to-design-for-trust-in-the-age-of-ai-agents/

2. Cloud Security Alliance (Feb 2026): "The Agentic Trust Framework: Zero Trust Governance for AI Agents"  
   URL: https://cloudsecurityalliance.org/blog/2026/02/02/the-agentic-trust-framework-zero-trust-governance-for-ai-agents

3. Microsoft Community Hub (Jan 2026): "Architecting Trust: A NIST-Based Security Governance Framework for AI Agents"  
   URL: https://techcommunity.microsoft.com/blog/microsoftdefendercloudblog/architecting-trust-a-nist-based-security-governance-framework-for-ai-agents/4490556
```

---

## CANDIDATE #5: Multi-Agent Orchestration Production Patterns (AS.SOTA.003)

**Pack:** PACK-autonomous-agents  
**Type:** SOTA-update (production best practices)  
**Priority:** СРЕДНЯЯ

### Предварительная формулировка

```markdown
---
id: AS.SOTA.003
type: sota
title: Multi-Agent Orchestration Production Patterns
status: converging
source: Iterathon 2026, MarkTechPost, Medium
date: 2026-03
---

# Multi-Agent Orchestration Production Patterns

## Adoption Stats (2026)

- **40% of enterprise apps** will feature task-specific agents by end of 2026 (up from <5% in 2025) — Gartner prediction
- **BUT: 10-15% pilot success rate** — только каждый 10-й pilot выходит в production
- **86% of copilot spending ($7.2B)** → agent-based systems
- **75% of multi-agent systems** become unmanageable beyond 5 agents

## Production-Grade Architecture

### Core Primitives (LangGraph model)

1. **Stateful Nodes**
   - Each agent = node в graph
   - State persists across executions (SQLite-based persistence)

2. **Cyclical Workflows**
   - Agents critique and improve own outputs (impossible in DAG-based engines)
   - Reflexion loops, self-correction

3. **Runtime Graph Mutation**
   - Workflow structure адаптируется dynamically based on results

4. **Checkpoint Recovery**
   - If agent fails → reassign or replay node using preserved state
   - Graceful failover

### Communication: Structured Message Bus

**Pattern (MarkTechPost, Mar 2026):**
- LangGraph + Pydantic for type-safe messages
- All inter-agent communication через centralized bus (not direct calls)
- Benefits:
  - Modularity (agents decoupled)
  - Traceability (all messages logged)
  - Auditability (ACP logging — Agent Communication Protocol)

## Coordination Patterns

### Centralized (Supervisor)
**Architecture:** Supervisor agent coordinates subagents.  
**Pros:** Clear control, simple debugging.  
**Cons:** Potential bottleneck, single point of failure.

**Use case:** Workflow с чёткой последовательностью (data pipeline, где каждый шаг зависит от предыдущего).

### Decentralized (Peer-to-peer)
**Architecture:** Agents operate autonomously, communicate directly.  
**Pros:** Flexibility, resilience (no single point of failure).  
**Cons:** Complexity (coordination overhead), hard to debug.

**Use case:** Emergent behavior желателен (creative tasks, brainstorming).

### Hierarchical (Teams + Leaders)
**Architecture:** Small teams (3-7 agents) with team leaders, coordinating subgroups.  
**Pros:** Scales beyond 5 agents (avoid coordination explosion).  
**Cons:** Multi-level overhead, latency.

**Use case:** Large-scale workflows (enterprise automation).

## Failure Modes (Production Reality)

### FM.001: Complexity Explosion at 5+ Agents
**Severity:** Критический  
**Scenario:** Coordination cost растёт квадратично (N agents → N*(N-1)/2 interactions). Beyond 5 agents → system becomes unmanageable.  
**Mitigation:**
- Keep teams small (3-7 agents per workflow)
- Hierarchical structures beyond that
- Clear role definitions (avoid overlap)

**Источник:** 75% of multi-agent systems fail this way (Iterathon 2026).

### FM.002: State Loss on Failures
**Severity:** Высокий  
**Scenario:** Agent crashes mid-execution → state lost → workflow restart from scratch.  
**Mitigation:**
- Persistent state (SQLite, database-backed)
- Checkpoint recovery (LangGraph model)
- Idempotent operations (safe to retry)

### FM.003: Observability Black Hole
**Severity:** Высокий  
**Scenario:** Multi-agent workflow fails, but no clear indication where/why (debugging nightmare).  
**Mitigation:**
- Human-in-the-loop checks (critical decision points)
- LangSmith observability (debug every agent decision)
- Structured logging (ACP — all messages logged)

## Performance Benchmarks (IBM Research, 2026)

**With proper orchestration:**
- **Process hand-offs:** -45%
- **Decision speed:** 3x improvement

**Economic impact (McKinsey):** Generative AI could add $2.6-4.4T annually to global GDP.

## Best Practices

### 1. Start Small
- 2-3 agents per workflow initially
- Prove value before scaling

### 2. Clear Role Definitions
- Each agent has specific responsibility (no overlap, no gaps)
- Contract: inputs, outputs, side effects

### 3. Monitoring First
- Instrument before deploying
- Alerts on anomalies (latency spikes, error rates)

### 4. Human-in-the-Loop for Critical Paths
- Autonomous agents for routine tasks
- Human approval for high-stakes decisions (financial transactions, user-facing actions)

## Tools and Platforms (2026)

### LangGraph Platform
- Comprehensive solution for deploying/managing agentic applications at scale
- Production-ready infrastructure
- Developer tools (LangSmith for debugging)

### LangSmith
- Agent engineering platform
- Debug every agent decision
- Eval changes
- Deploy in one click

## Связь с другими сущностями Pack'ов

- **DP.SOTA.006 (Coordination Cost):** Multi-agent orchestration = coordination cost mitigation through structured patterns
- **AS.M.005 (Agentic Plan Caching):** Agents share cached plans → coordination efficiency
- **AS.M.007 (Graduated Governance):** Supervisor pattern implements Level 3-4 autonomy with oversight

## Источники

1. Iterathon (2026): "Agent Orchestration 2026: LangGraph, CrewAI & AutoGen Guide"  
   URL: https://iterathon.tech/blog/ai-agent-orchestration-frameworks-2026

2. MarkTechPost (Mar 2026): "How to Design a Production-Grade Multi-Agent Communication System Using LangGraph"  
   URL: https://www.marktechpost.com/2026/03/01/how-to-design-a-production-grade-multi-agent-communication-system-using-langgraph-structured-message-bus-acp-logging-and-persistent-shared-state-architecture/

3. Medium (2026): "Agent Orchestration: When to Use LangChain, LangGraph, AutoGen"  
   URL: https://medium.com/@akankshasinha247/agent-orchestration-when-to-use-langchain-langgraph-autogen-or-build-an-agentic-rag-system-cc298f785ea4
```

---

## CANDIDATE #6: EdTech B2B SaaS Unit Economics Benchmarks (ECO.M.002 enrichment)

**Pack:** PACK-ecosystem  
**Type:** Metric (industry benchmarks)  
**Priority:** СРЕДНЯЯ (для WP-145)

### Предварительная формулировка

```markdown
---
id: ECO.M.002
type: metric
title: EdTech B2B SaaS Unit Economics Benchmarks
status: updated
source: Data-Mania 2026, Proven SaaS, WeAreFounders
date: 2026-03
---

# EdTech B2B SaaS Unit Economics Benchmarks (2026)

## Churn Rates

**EdTech = highest churn among SaaS verticals:**
- **EdTech monthly churn:** 9.6%
- **Enterprise SaaS:** 0.25%
- **38x difference** (EdTech vs enterprise)

**Average B2B SaaS:** 3.5% monthly churn

**Interpretation:** EdTech высокая volatility → retention стратегия критична.

## Customer Acquisition Cost (CAC)

**Average B2B SaaS:** $536 per customer  
**EdTech segment (education-specific):** $42 CAC (best-in-class)  
**EdTech general:** $1,143 CAC (when targeting institutions/enterprises)

**CAC Payback Period:**
- **Education segment:** 3.8 months (fastest profitability path)
- **B2B SaaS median:** 6.8 months
- **Healthy benchmark:** <12 months

## Expansion Revenue & NRR

**Expansion revenue:** 40% of new ARR (existing customers upsell/cross-sell)  
**Net Revenue Retention (NRR):** >106% → 2.5x faster growth

**Rule of thumb:**
- NRR >100% = expansion offsets churn
- NRR >106% = significant growth multiplier

## LTV:CAC Ratio

**Healthy benchmark:** >3:1  
**Interpretation:** Lifetime value должна быть минимум 3x от acquisition cost.

## Annual Churn Targets

**For established B2B SaaS:** <5% annual churn is vital for strong unit economics.

**EdTech challenge:** 9.6% monthly = ~100%+ annual (если не предотвратить) → retention programs обязательны.

## Net Retention

**B2B SaaS average:** 100% net retention (ideal benchmark).

**Components:**
- Gross retention (existing customers stay)
- Expansion revenue (existing customers grow)

## Conversion Rates

**Visitor-to-Trial:**
- **EdTech:** 10.3%
- **CRM software:** 9.7%
- **Cybersecurity:** 7.4%

**MQL-to-SQL (B2B SaaS):**
- **Average:** 40% (far exceeds overall B2B average of 13%)

## Market Funding Reality (2026)

**EdTech funding decline:**
- **2024:** $270M across 48 rounds
- **2025 (until Dec):** $35.8M across 21 rounds
- **Drop:** 86.75%

**Interpretation:** Investors focus on proven traction, not hype. Metrics = ammunition.

## Связь с WP-145 (Fundraising Deck)

**Используемые метрики в deck v0.3:**
- Churn: 9.6% (challenge acknowledged)
- CAC: $1,143 benchmark (IWE currently $0 — highlight efficiency)
- NRR: >106% target (expansion strategy in roadmap)

**Обогащение deck:**
- Slide 10 (Unit Economics): добавить expansion revenue 40% benchmark + NRR >106% as growth multiplier
- Narrative: "IWE designed for retention through personalization + community" (counteract EdTech high churn)

## Источники

1. WeAreFounders (2026): "SaaS Churn Rates and Customer Acquisition Costs by Industry: 2026 Benchmarks"  
   URL: https://www.wearefounders.uk/saas-churn-rates-and-customer-acquisition-costs-by-industry-2025-data/

2. Data-Mania (2026): "CAC Benchmarks for B2B Tech Startups 2026"  
   URL: https://www.data-mania.com/blog/cac-benchmarks-for-b2b-tech-startups-2025/

3. Proven SaaS (2026): "CAC Payback Benchmarks 2026"  
   URL: https://proven-saas.com/benchmarks/cac-payback-benchmarks
```

---

## CANDIDATE #7: AgentDiet & TrajTune — Trajectory Optimization Methods (AS.M.008, AS.M.009)

**Pack:** PACK-autonomous-agents  
**Type:** Method (2 related methods)  
**Priority:** НИЗКАЯ (дополняют AS.M.005 Agentic Plan Caching)

### Предварительная формулировка

```markdown
---
id: AS.M.008
type: method
title: AgentDiet — Trajectory Reduction
status: emerging
source: arXiv 2509.23586
date: 2025
---

# AgentDiet — Trajectory Reduction

## Проблема

Agent trajectories accumulate massive token usage:
- **Average GitHub issue resolution:** 48.4K tokens trajectory (40 steps)
- **Accumulated usage:** 1.0M tokens per issue

**Cost inefficiency:** Много useless, redundant, expired information в trajectory.

## Решение

**AgentDiet:** Reduce trajectory content in real-time.

**Mechanism:**
1. Cost-efficient LLM (lightweight) reads trajectory
2. Identifies and removes:
   - Useless information (не влияет на решение)
   - Redundant information (duplicates)
   - Expired information (no longer relevant)
3. Compresses trajectory → shorter, cheaper

## Comparison with APC (AS.M.005)

| Аспект | AgentDiet | Agentic Plan Caching |
|--------|-----------|---------------------|
| **Фокус** | Reduce content (compression) | Reuse plans (caching) |
| **When** | During execution (real-time) | After execution (test-time) |
| **Goal** | Lower cost per execution | Avoid re-planning |

**Complementary:** Can combine (AgentDiet reduces trajectory size → APC caches reduced plans).

## Источники

1. arXiv:2509.23586: "Reducing Cost of LLM Agents with Trajectory Reduction"  
   URL: https://arxiv.org/html/2509.23586v2
```

```markdown
---
id: AS.M.009
type: method
title: TrajTune — Trajectory-Based Prompt Optimization
status: emerging
source: OpenReview (ACL 2024), arXiv ETO
date: 2025
---

# TrajTune — Trajectory-Based Prompt Optimization

## Проблема

Agents hallucinate, fail tools, make mistakes → prompts need optimization.

**Traditional approach:** Manual prompt tuning (slow, не масштабируется).

## Решение

**TrajTune:** Trajectory-aware prompt optimization framework.

**Mechanism:**
1. Capture structured execution traces (trajectories)
2. Compute fine-grained error metrics (где именно ошибка)
3. Compare против adaptive thresholds
4. If issue detected → multi-LLM feedback loop iteratively refines prompts

## Performance (Benchmarks)

- **Hallucination rates:** -40%
- **Tool success rates:** +30%
- **Software engineering task accuracy:** +25%
- **IT-ops success rates:** +20%

## Comparison with APC (AS.M.005)

| Аспект | TrajTune | Agentic Plan Caching |
|--------|----------|---------------------|
| **Фокус** | Optimize prompts (offline) | Reuse plans (online) |
| **When** | Offline (training phase) | Online (execution time) |
| **Goal** | Better prompts → fewer errors | Faster execution → lower latency |

**Complementary:** TrajTune optimizes prompts → APC caches plans based on those optimized prompts.

## Источники

1. OpenReview (ACL 2024): "Trial and Error: Exploration-Based Trajectory Optimization of LLM Agents"  
   URL: https://openreview.net/forum?id=jyG14i5vQ5

2. OpenReview: "TrajTune: Trajectory-Based Prompt Optimization for LLM Agents"  
   URL: https://openreview.net/forum?id=vXrOyzt0Ea
```


