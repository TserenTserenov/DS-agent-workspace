# Scout Report — 2026-03-29

> Автоматический отчёт. Модель: sonnet. Бюджет: $10.0.
> Находок: 4 | Capture-кандидатов: 2 | WP-предложений: 0
> **Статус ревью:** ✅ проверен (29 мар, разбор #6: 1 новая сущность + 7 enrichments, 100% конверсия)

## Статус заданий (backlog)

  - id: rt-001	    title: "Реальные кейсы автономных агентов в проде"	    status: done
  - id: rt-002	    title: "SOTA методы написания текстов для соцсетей (антидетект AI)"	    status: moved_to_session
  - id: rt-003	    title: "Fundraising best practices для seed-раунда EdTech/Intelligence Platform"	    status: done
  - id: rt-004	    title: "SOTA методы бизнес-моделирования для EdTech/SaaS"	    status: done

## Находки (ТОП-4)

# Scout Morning Report — 2026-03-29

**Сессия:** Headless run (auto)
**Источников:** 13 web searches (arxiv, industry reports, WEF, McKinsey, EdTech VCs)
**Находок:** 8 релевантных (2 новые сущности, 6 enrichments, 1 dedup_skip)
**Метрики:** dedup_filtered=1, enrichments=6, new_entities=2

---

## ТОП-5 находок (ранжировано по приоритету)

### 1. Efficacy Reckoning — EdTech Paradigm Shift 2026

**Источник:** [OpenFieldX EdTech Trends 2026](https://openfieldx.com/edtech-trends-2026/), [Talks Android EdTech Funding 2026](https://talksandroid.com/edtech-funding-news-2026-trends/)

**Релевантность:** КРИТИЧЕСКАЯ  
**Связь:** WP-145 (investor deck), WP-142 (fundraising), ECO.SOTA.001

**Суть:**  
"Efficacy Reckoning" — фундаментальный сдвиг в EdTech 2026: инвесторы и институциональные покупатели требуют verifiable proof of learning outcomes, не engagement metrics. Engagement → Outcomes, Reach → Impact, Content → Measurable Gains. Founders обязаны предоставить Logic Models или third-party research с доказательством улучшения на ≥10% (student mastery / teacher productivity). Products без proof-of-impact не проходят budget scrutiny. Skills transparency = новый buying requirement. Capital efficiency > growth-at-all-costs.

**Reasoning:**  
Прямое влияние на WP-145 (investor narrative). IWE позиционируется как intelligence development, не education → это competitive advantage в Efficacy Reckoning (у нас есть цифровой двойник = measurable characteristics, не просто engagement). Enrichment ECO.SOTA.001 + input для WP-145 pitch.

**Предложение:**  
- **Тип:** SOTA-обновление (enrichment)
- **Куда:** PACK-ecosystem → ECO.SOTA.001 (новая секция "Efficacy Reckoning Q1 2026")
- **Действие:** Обогатить ECO.SOTA.001 данными: 10% improvement threshold, Logic Models requirement, skills transparency as buying requirement, proof-of-impact > engagement

---

### 2. Agent Drift Taxonomy — Semantic, Coordination, Behavioral

**Источник:** [arxiv:2601.04170](https://arxiv.org/pdf/2601.04170) "Agent Drift: Quantifying Behavioral Degradation", [Prompt-Based Semantic Shift (PBSS)](https://arxiv.org/html/2506.10095), [Maxim AI Guide](https://www.getmaxim.ai/articles/a-comprehensive-guide-to-preventing-ai-agent-drift-over-time/)

**Релевантность:** ВЫСОКАЯ  
**Связь:** WP-179 (GEPA Phase 2), AS.FM.* (новый failure mode), DP.M.003 (Context Engineering)

**Суть:**  
Agent drift — progressive degradation агента через extended interaction. Новая таксономия (2601.04170, Jan 2026): (1) **Semantic drift** — deviation from original intent, (2) **Coordination drift** — breakdown multi-agent consensus, (3) **Behavioral drift** — emergence of unintended strategies. Prompt behavior дрейфует БЕЗ EDITS (versioning недостаточен → continuous evaluation обязательна). PBSS framework: semantically equivalent prompts → разные ответы (tokenization/decoding artifacts). Mitigation: behavioral snapshots, staged rollouts, circuit breakers, prompt versioning + observability (не только text diffs).

**Reasoning:**  
Новый класс FM, дополняет AS.FM.012-020 (технические) и AS.FM.020 (organizational). Конкретные mitigation strategies. Применимо к WP-132 (scheduler drift detection), WP-179 (GEPA Phase 2 = runtime verification), WP-171 (Activity Hub agents). Различение: Semantic Drift (agent) ≠ Model-Reality Drift (DP.FM.005, external).

**Предложение:**  
- **Тип:** failure mode (новая сущность)
- **Куда:** PACK-autonomous-agents → AS.FM.021
- **Действие:** Capture новый FM с таксономией (3 типа), PBSS framework ref, mitigation (behavioral snapshots, continuous eval, circuit breakers)

---

### 3. Agentic Reasoning — Three-Layer Framework (arxiv 2601.12538)

**Источник:** [arxiv:2601.12538](https://arxiv.org/abs/2601.12538) "Agentic Reasoning for Large Language Models"

**Релевантность:** ВЫСОКАЯ  
**Связь:** WP-179 (GEPA), AS.SOTA.* (новый паттерн), WP-171 (Activity Hub architecture)

**Суть:**  
Agentic reasoning = paradigm shift от reactive LLMs к autonomous agents (plan, act, learn через continual interaction). Three-layer framework: (1) **Foundational agentic reasoning** — core single-agent capabilities (planning, tool use, reasoning), (2) **Self-evolving agentic reasoning** — agents refine capabilities через feedback loops (improvement loop), (3) **Collective multi-agent reasoning** — collaborative intelligence, coordination, consensus. Отличается от простой prompt engineering тем, что агент = actor in environment, не text generator.

**Reasoning:**  
Архитектурный паттерн (не пошаговый метод) → SOTA. Не покрыт существующими AS.SOTA.*. Связь: AS.D.006 (Execution Loop ≠ Improvement Loop) — layer 2 framework = формализация improvement loop. Применимо к WP-179 (GEPA design), WP-171 (Hub agents = collective reasoning).

**Предложение:**  
- **Тип:** SOTA (новая сущность)
- **Куда:** PACK-autonomous-agents → AS.SOTA.006
- **Действие:** Capture three-layer framework как архитектурный паттерн для проектирования агентных систем

---

### 4. Context Engineering 2026 — Information Discipline over Window Size

**Источник:** [SwirlAI Newsletter](https://www.newsletter.swirlai.com/p/state-of-context-engineering-in-2026), [LogRocket LLM Context Problem](https://blog.logrocket.com/llm-context-problem-strategies-2026), [Comet ML Best Practices](https://www.comet.com/site/blog/context-engineering/)

**Релевантность:** СРЕДНЯЯ  
**Связь:** DP.SOTA.002, DP.M.003, WP-132 (scheduler context management)

**Суть:**  
Context engineering 2026 = information discipline > window size. Проблема НЕ в capability (models handle 1M+ tokens) — проблема в providing right info, right time, right amount. Best practices: (1) **Sliding window + summarization hybrid** (keep recent turns full, compress old), (2) **Context routing** (classify query → load relevant KB only), (3) **Tool loadout optimization** (>30 tools = confusion, dynamic selection), (4) **RAG not obsolete** (Anthropic: >100k degrades reasoning). Challenges: context rot (poorly curated info degrades performance), mode collapse (alignment reduces diversity).

**Reasoning:**  
Обогащает DP.SOTA.002 (Context Engineering) конкретными 2026 best practices. Применимо к DP.M.003 (CE Protocol — добавить tool loadout + sliding window patterns). Связь с WP-132 (scheduler = context routing для задач).

**Предложение:**  
- **Тип:** SOTA-обновление (enrichment)
- **Куда:** PACK-digital-platform → DP.SOTA.002 (новая секция "Best Practices 2026")
- **Действие:** Enrichment с patterns: sliding window + summarization, context routing, tool loadout, RAG necessity

---

### 5. MCP 2026 Roadmap — Governance, Transport, Agent Communication

**Источник:** [MCP Blog 2026 Roadmap](http://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/), [The New Stack MCP Production Pains](https://thenewstack.io/model-context-protocol-roadmap-2026/), [Use Apify MCP 2026](https://use-apify.com/blog/mcp-standard-ecosystem-2026)

**Релевантность:** СРЕДНЯЯ  
**Связь:** DP.SOTA.014, WP-187 (Ory integration), WP-171 (Activity Hub MCP servers)

**Суть:**  
MCP 2026 roadmap = 4 приоритета (core maintainers): (1) **Transport scalability** — stateful sessions × load balancers problem, horizontal scaling workarounds → streamable HTTP improvements, (2) **Agent communication** — longer-running work (agents trigger multi-day tasks), (3) **Governance maturation** — audit trails, SSO, gateway behavior, config portability для enterprise, (4) **Enterprise readiness**. 1000+ connectors, major vendors (OpenAI, Anthropic, Google, Amazon) adopted. Market $1.8B 2025. NOT ISO/IEC standard (open specification with growing adoption).

**Reasoning:**  
Обогащает DP.SOTA.014 (MCP стандарт) roadmap priorities. Governance = критический фокус IWE (R2 2026). Transport scalability влияет на WP-187 (Ory + MCP integration), agent communication = WP-171 (Hub agents multi-day orchestration).

**Предложение:**  
- **Тип:** SOTA-обновление (enrichment)
- **Куда:** PACK-digital-platform → DP.SOTA.014 (новая секция "2026 Roadmap Priorities")
- **Действие:** Enrichment с 4 priorities + governance focus + NOT formal standard clarification

---

## Другие находки (средний приоритет)

### 6. Trust Stack — WEF + CSA Agentic Trust Framework (ATF)

**Источник:** [WEF Trust Stack](https://www.weforum.org/stories/2026/02/how-to-design-for-trust-in-the-age-of-ai-agents/), [CSA ATF](https://cloudsecurityalliance.org/blog/2026/02/02/the-agentic-trust-framework-zero-trust-governance-for-ai-agents)

**Enrichment:** AS.M.001 (Trust Stack Design) + AS.SOTA.003 (Global Governance)  
WEF "trust stack" = legible reasoning paths + bounded agency + transparent decision records. CSA ATF = Zero Trust для AI agents, four-layer defense-in-depth governance (LGA). Maturity avg 2.3 (2026), только 1/3 orgs ≥3. Nvidia GTC 2026: vendors НЕТ complete answers (agent-to-agent trust, memory poisoning, cryptographic binding).

**Применимо:** WP-179 (GEPA governance layer design), WP-171 (Hub trust model)

---

### 7. World Models Race — Genie 3, World Labs Marble, AMI Labs

**Источник:** [Introl World Models Race](https://introl.com/blog/world-models-race-agi-2026), [Built In World Models](https://builtin.com/articles/ai-world-models-explained)

**Enrichment:** DP.SOTA.013 (World Models)  
Late 2025 / early 2026 explosion: Yann LeCun → AMI Labs (€500M), Google DeepMind Genie 3 (real-time 3D, 24 fps), Fei-Fei Li World Labs Marble. World models = AI understands physics (gravity, inertia, impact). Agents НЕ могут generalize БЕЗ predictive model ("no model-free shortcut"). Agentic reasoning paper (2601.12538) = world models central to planning.

**Применимо:** Будущие Hub agents (embodied reasoning), DP.ARCH.003 (ЦД layer 3 = world model?)

---

### 8. Multi-Agent Framework Comparison — AutoGen (maintenance), CrewAI (TTM), LangGraph (production)

**Источник:** [o-mega Framework Comparison](https://o-mega.ai/articles/langgraph-vs-crewai-vs-autogen-top-10-agent-frameworks-2026), [DataCamp Comparison](https://www.datacamp.com/tutorial/crewai-vs-langgraph-vs-autogen)

**Enrichment:** AS.SOTA.002 (Multi-Agent Orchestration Frameworks)  
AutoGen → Microsoft Agent Framework (maintenance mode). CrewAI = fastest time-to-production (role-based teams, 40% faster than LangGraph for standard workflows). LangGraph = production leader (graph-based, stateful, battle-tested). AutoGen slowest (chat-heavy consensus overhead). Choose: CrewAI = prototyping, LangGraph = production, AutoGen = multi-party conversations.

**Применимо:** Архитектурные решения WP-171 (Hub orchestration — LangGraph candidate), WP-179 (GEPA evaluation framework)

---

## Статистика сессии

- **Scanned:** 13 web searches, 8 domains (arxiv, WEF, McKinsey, industry reports)
- **Candidates:** 10 initial findings
- **Dedup filtered:** 1 (AS.FM.020 already accepted #12)
- **Enrichments:** 6 (ECO.SOTA.001, DP.SOTA.002, DP.SOTA.013, DP.SOTA.014, AS.M.001, AS.SOTA.002, AS.SOTA.003)
- **New entities:** 2 (AS.FM.021, AS.SOTA.006)
- **Top priority:** Efficacy Reckoning (critical for WP-145 investor narrative)

---

## Рекомендации

1. **WP-145 (investor deck):** Использовать Efficacy Reckoning narrative — IWE = measurable intelligence development (ЦД characteristics), не engagement-driven education. Competitive advantage в 2026 climate.

2. **WP-179 (GEPA Phase 2):** Добавить Agent Drift detection (behavioral snapshots, PBSS framework) + Agentic Reasoning three-layer framework как design input.

3. **DP.M.003 (Context Engineering Protocol):** Обогатить 2026 best practices (sliding window, tool loadout, context routing).

4. **WP-171 (Activity Hub):** Рассмотреть LangGraph для orchestration (production-ready), Trust Stack WEF/CSA для governance design.

5. **Формализация:** Передать Экстрактору (R2) для capture AS.FM.021 + AS.SOTA.006 в Pack-autonomous-agents.


## Capture-кандидаты

> Решение: ✅ принять → Экстрактор формализует в Pack | ❌ отклонить → trajectory | 🔄 доработать → backlog

# Capture Candidates — 2026-03-29

Черновики для Экстрактора (R2). Только новые сущности (enrichments НЕ включены — обогащать напрямую).

---

## AS.FM.021 — Agent Drift (Semantic, Coordination, Behavioral)

**Тип:** Failure Mode  
**Pack:** PACK-autonomous-agents  
**Источники:**  
- arxiv:2601.04170 "Agent Drift: Quantifying Behavioral Degradation in..." (Jan 2026)
- arxiv:2506.10095 "When Meaning Stays the Same, but Models Drift: Token-Level Behavioral Instability"
- Maxim AI "Guide to Preventing AI Agent Drift Over Time" (2026)

### Черновик сущности

**Название:** Agent Drift — Semantic, Coordination, Behavioral

**Суть:**  
Progressive degradation агентного поведения, decision quality, и inter-agent coherence через extended interaction sequences. Три типа дрейфа (arxiv 2601.04170):

1. **Semantic drift** — progressive deviation from original intent (агент постепенно отклоняется от исходной задачи)
2. **Coordination drift** — breakdown в multi-agent consensus mechanisms (агенты теряют синхронизацию)
3. **Behavioral drift** — emergence of unintended strategies (появление непредусмотренных паттернов поведения)

**Отличие от других FM:**  
- **DP.FM.005 (Model-Reality Drift)** — external drift (модель vs реальность). Agent Drift = internal drift (поведение агента vs исходный design).
- **AS.FM.019 (Behavioral Drift in Multi-Agent Systems)** — если уже существует, AS.FM.021 = расширение таксономией (semantic + coordination). ПРОВЕРИТЬ дубликат перед capture.

**Механизм:**  
Prompt behavior дрейфует БЕЗ ИЗМЕНЕНИЙ промпта. PBSS (Prompt-Based Semantic Shift): semantically equivalent prompts → разные outputs из-за tokenization/decoding artifacts. Versioning текста промпта недостаточен — нужна **behavioral observability**.

**Mitigation:**

| Стратегия | Описание | Инструменты |
|-----------|----------|-------------|
| Behavioral snapshots | Периодические snaps expected behavior как regression test | Maxim AI, LangSmith |
| Continuous evaluation | Real-time monitoring outputs vs expected patterns | Staged rollouts, A/B testing |
| Circuit breakers | Auto-rollback при детекции drift >threshold | Observability платформы |
| Prompt versioning + observability | Version tracking + behavioral metrics (не только text diffs) | PromptLayer, Langfuse |

**Severity:** High (production agents деградируют незаметно)

**Индикаторы:**
- Outputs семантически корректны, но intent drift (PBSS)
- Multi-agent consensus failures без infra changes (coordination drift)
- Emergent strategies не в design spec (behavioral drift)

**Примеры:**
- Agent scheduler (WP-132): semantic drift → приоритизирует urgent над important без явного указания
- Multi-agent Hub (WP-171): coordination drift → агенты дублируют задачи, теряя consensus

**Связь с другими сущностями:**
- AS.M.001 (Trust Stack Design) — drift detection = runtime layer Trust Stack
- AS.D.006 (Execution Loop ≠ Improvement Loop) — drift происходит в execution, детектируется в improvement
- DP.M.003 (Context Engineering Protocol) — context rot = contributor к semantic drift

**Use cases:**
- WP-132 (Scheduler) — behavioral snapshots для drift detection
- WP-179 (GEPA Phase 2) — continuous evaluation = post-deployment gate
- WP-171 (Activity Hub) — coordination drift monitoring для multi-agent system

---

## AS.SOTA.006 — Agentic Reasoning: Three-Layer Framework

**Тип:** SOTA (архитектурный паттерн)  
**Pack:** PACK-autonomous-agents  
**Источник:** arxiv:2601.12538 "Agentic Reasoning for Large Language Models" (Jan 2026)

### Черновик сущности

**Название:** Agentic Reasoning — Three-Layer Framework (2026)

**Суть:**  
Agentic reasoning = paradigm shift от reactive LLMs (text generation) к autonomous agents (plan, act, learn через continual environment interaction). LLMs reframed как actors, не generators.

**Three-Layer Framework:**

1. **Foundational Agentic Reasoning**  
   Core single-agent capabilities:
   - Planning (task decomposition, sequencing)
   - Tool use (function calling, API interaction)
   - Reasoning (chain-of-thought, reflection)
   - Memory (episodic, semantic, procedural — см. AS.M.006)

2. **Self-Evolving Agentic Reasoning**  
   Agents refine capabilities через feedback:
   - Improvement loop (AS.D.006: Execution Loop ≠ Improvement Loop)
   - Reflexion (self-critique + retry)
   - Self-challenging (generate harder tests)
   - Trajectory caching (AS.M.005: plan reuse)

3. **Collective Multi-Agent Reasoning**  
   Collaborative intelligence:
   - Multi-agent coordination (consensus, negotiation)
   - Distributed problem-solving
   - Knowledge sharing (cross-agent memory sync)
   - Emergent capabilities (whole > sum of parts)

**Ключевое различение:**  
Agent = actor in environment (state → action → new state loop), LLM = text predictor (prompt → completion).

**Связь с существующими сущностями:**

| Сущность | Связь |
|----------|-------|
| AS.D.006 (Execution ≠ Improvement Loop) | Layer 2 = формализация improvement loop |
| AS.M.006 (Four-Type Memory) | Layer 1 foundational capability (memory types) |
| AS.M.005 (Agentic Plan Caching) | Layer 2 self-evolution (trajectory reuse) |
| AS.SOTA.002 (Multi-Agent Orchestration) | Layer 3 collective reasoning (frameworks как реализация) |
| AS.M.001 (Trust Stack Design) | Все 3 layers требуют Trust Stack governance |

**Применение:**  
Архитектурный паттерн для проектирования агентных систем. Определяет capability layers для roles (AS.D.002: Агент = Исполнитель + Роль).

**Use cases:**
- **WP-179 (GEPA):** Design input — какие layers проверять на каждой фазе (Ф0-Ф6)
  - Ф0-Ф2: Layer 1 (foundational capabilities)
  - Ф3-Ф4: Layer 2 (improvement loop)
  - Ф5-Ф6: Layer 3 (multi-agent coordination, если применимо)

- **WP-171 (Activity Hub):** Layer 3 collective reasoning = design principle для Hub orchestration

- **WP-132 (Scheduler):** Single-agent = Layers 1+2, не Layer 3

**SOTA status (Jan 2026):**  
Формализация shift от prompt engineering к agentic systems. Research community converges на three-layer taxonomy. Production implementations: AutoGen (conversations), CrewAI (role-based Layer 3), LangGraph (graph-based all layers).

**Различение от DP.SOTA.006 (Agentic Development):**  
DP.SOTA.006 = agents помогают разработке (coding assistants). AS.SOTA.006 = agents как autonomous reasoners (domain-agnostic framework).

**Failure modes (связь с AS.FM.*):**  
- Layer 1 failures → AS.FM.012 (specification), AS.FM.016 (tool misuse)
- Layer 2 failures → AS.FM.021 (agent drift — improvement loop не детектирует degradation)
- Layer 3 failures → AS.FM.015 (multi-agent communication), AS.FM.019 (behavioral drift multi-agent)

**Governance (связь с AS.M.004, AS.SOTA.003):**  
Graduated Governance применяется по layers:
- Layer 1 (foundational): Tier 1 governance (full human oversight)
- Layer 2 (self-evolving): Tier 2 (approval required for self-modifications)
- Layer 3 (collective): Tier 3 (consensus mechanisms + audit trail)


