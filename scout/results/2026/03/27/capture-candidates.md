# Capture Candidates — 2026-03-27

Черновики для Экстрактора (R2). Приоритет: критические → высокие.

---

## Candidate #1: AS.FM.019 — Behavioral Drift in Multi-Agent Systems [CRITICAL]

### Metadata

- **Type:** Failure Mode
- **Severity:** Critical
- **Pack:** AS (Autonomous Agents)
- **Proposed ID:** AS.FM.019
- **Sources:** 
  - [Agentic AI Systems Don't Fail Suddenly — They Drift Over Time (CIO)](https://www.cio.com/article/4134051/agentic-ai-systems-dont-fail-suddenly-they-drift-over-time.html)
  - [5 Production Scaling Challenges for Agentic AI](https://machinelearningmastery.com/5-production-scaling-challenges-for-agentic-ai-in-2026/)

### Definition

**Behavioral Drift** — постепенная деградация поведения агентной системы в production (месяцы), вызванная incremental changes: обновления моделей, изменения промптов, добавление инструментов, изменение зависимостей. Cloud Security Alliance (CSA) классифицирует как **cognitive degradation** — системный риск, возникающий градуально, не внезапно.

### Distinction

**DP.FM.005 (Model-Reality Drift) ≠ AS.FM.019 (Behavioral Drift):**

| Aspect | DP.FM.005 | AS.FM.019 |
|--------|-----------|-----------|
| Объект | Статичная модель (representation) | Динамичная система агентов (behavior) |
| Причина | Реальность меняется, модель устаревает | Система меняется изнутри (updates, config drift) |
| Временная шкала | Месяцы-годы (медленный external drift) | Недели-месяцы (fast internal drift) |
| Детектируется | Метрики качества модели (accuracy drop) | Поведенческие аномалии (execution path changes) |
| Mitigation | Ретренинг модели | Version control, regression testing, observability |

### Scenario

1. Multi-agent система работает стабильно 3 месяца
2. Постепенно: LLM provider обновляет модель (minor version), разработчик добавляет новый tool, меняет промпт для clarity, обновляет dependency
3. Каждое изменение **individually safe**, но **cumulatively** → behavior shifts
4. Результат: agents waiting on agents, race conditions, cascading failures, non-deterministic execution paths **impossible to reproduce in staging**
5. Symptoms: latency increase, completion rate drop, user complaints о "weird behavior" — но **нет явной ошибки в логах**

### Mitigation

- **Deep observability:** Трассировка execution paths, behavior snapshots, drift detection metrics
- **Prompt/tool versioning:** Git-like version control для всех agent configurations
- **Behavioral regression testing:** Baseline behavior snapshots + periodic validation против новых deployments
- **Staged rollouts:** Canary deployments с behavior monitoring перед full rollout
- **Circuit breakers:** Automatic rollback если behavior divergence exceeds threshold

### Related Entities

- **DP.FM.005** (Model-Reality Drift) — смежный drift, но другой объект
- **AS.FM.013** (Reasoning Loops and Hallucination Cascades) — может быть следствием behavioral drift
- **WP-179** (GEPA Test Framework) — должен включать drift detection
- **WP-132** (scheduler.sh) — vulnerable to behavioral drift без monitoring

---

## Candidate #2: AS.FM.020 — Production Deployment Failure (Organizational) [CRITICAL]

### Metadata

- **Type:** Failure Mode
- **Severity:** Critical
- **Pack:** AS (Autonomous Agents)
- **Proposed ID:** AS.FM.020
- **Sources:**
  - [Why 88% of AI Agents Fail Production (Digital Applied)](https://www.digitalapplied.com/blog/88-percent-ai-agents-never-reach-production-failure-framework)
  - [Agentic AI in Production (Use Apify)](https://use-apify.com/blog/agentic-ai-enterprise-adoption-2026)
  - [HBR: Why Agentic AI Projects Fail](https://hbr.org/2025/10/why-agentic-ai-projects-fail-and-how-to-set-yours-up-for-success)

### Definition

**Production Deployment Failure — Organizational Readiness Gap** — failure mode, при котором агентный проект **технически валиден** (проходит все тесты, GEPA validation), но **не достигает production** или **quietly shut down** из-за inadequate organizational infrastructure: governance gaps, observability limitations, legacy system incompatibility, отсутствие accountability frameworks.

**Статистика:** 88% AI agent projects never reach production (Digital Applied). Gartner: 40% agentic AI projects будут отменены к концу 2027.

### Distinction

**Technical Failure Modes (AS.FM.012-018) ≠ AS.FM.020 (Organizational):**

| Aspect | Technical FM | Organizational FM |
|--------|--------------|-------------------|
| Причина | Agent behavior (reasoning, memory, tools) | Enterprise readiness (governance, infra, observability) |
| Детектируется | Unit tests, integration tests, GEPA | Pre-deployment audit, governance checklist |
| Severity point | Runtime (production errors) | Pre-production (never deployed) |
| Owner | AI Engineer, Agent Developer | CTO, Program Manager, Compliance |
| Mitigation | Code fixes, prompt tuning, tool redesign | Governance frameworks, organizational change management |

### Scenario

1. Team разрабатывает multi-agent систему для automation workflow
2. Agents проходят все technical validations: GEPA tests (quality >0.8), unit tests, integration tests
3. **Deployment blocked** из-за:
   - **Governance gap:** No clear accountability framework (who approves agent decisions? who escalates failures?)
   - **Observability gap:** Existing monitoring stack не поддерживает agent tracing (no visibility into non-deterministic execution paths)
   - **Legacy integration:** API authentication edge cases, rate limiting incompatibility, async coordination issues
   - **Risk aversion:** Leadership не уверена в governance → pilot freezes
4. Результат: Project **quietly shut down** через 6-12 месяцев, not because model failed, but because **enterprise failed to govern execution**

### Mitigation

- **Pre-deployment governance checklist:**
  - Accountability matrix (decision authority, escalation paths, human-in-the-loop triggers)
  - Observability plan (tracing stack, behavior monitoring, drift detection)
  - Legacy system compatibility assessment (API contracts, auth flows, rate limits, versioning)
  - Risk tolerance definition (what level of autonomy is acceptable, rollback triggers)
- **Organizational readiness audit:** Separate gate после technical validation (GEPA), проводит CTO/Program Manager, не AI Engineer
- **Staged rollout governance:** Start with low-risk workflows (internal tools, non-customer-facing), prove governance works, scale up
- **Graduated Governance (AS.M.004):** Use tiered autonomy model (L0-L3) to de-risk deployment

### Related Entities

- **AS.M.004** (Graduated Governance) — mitigation framework
- **AS.SOTA.003** (WEF/Singapore Governance) — external governance standards
- **WP-179** (GEPA Test Framework) — должен включать organizational readiness gate
- **AS.FM.012-018** — technical failure modes (complements, не заменяет)

---

## Candidate #3: AS.M.007 (or DP.M.010) — ACE: Agentic Context Engineering [HIGH]

### Metadata

- **Type:** Method
- **Pack:** AS (if agent-specific) or DP (if platform-wide pattern)
- **Proposed ID:** AS.M.007 или DP.M.010
- **Sources:**
  - [Agentic Context Engineering (arxiv 2510.04618)](https://arxiv.org/abs/2510.04618)
  - [State of Context Engineering 2026](https://www.newsletter.swirlai.com/p/state-of-context-engineering-in-2026)

### Definition

**ACE (Agentic Context Engineering)** — фреймворк оптимизации контекстов для LLM-based систем, трактующий контексты как **evolving playbooks**: агенты/системы накапливают, рефлексируют и курируют стратегии через модульный процесс **generation → reflection → curation**. Оптимизирует контексты **offline (system prompts) и online (agent memory)** одновременно.

**Результаты (arxiv 2510.04618):**
- +10.6% на агентных задачах (vs strong baselines)
- +8.6% на финансовых датасетах

### Procedure (Draft)

#### Phase 0: Baseline Context

1. Определить типы контекстов:
   - **Offline:** System prompts, role definitions, tool descriptions (static или semi-static)
   - **Online:** Agent working memory, conversation history, task state (dynamic)
2. Зафиксировать baseline performance (без ACE)

#### Phase 1: Generation

1. **For offline contexts:** Generate multiple candidate system prompts/role definitions через:
   - LLM-based prompt optimization (self-refinement)
   - Few-shot examples from production logs
   - Domain-specific templates
2. **For online contexts:** Agent генерирует memory entries на основе task execution (observations, reflections, intermediate results)

#### Phase 2: Reflection

1. Agent рефлексирует над execution paths:
   - What worked? (successful strategies → keep)
   - What failed? (unsuccessful patterns → prune)
   - What's missing? (gaps in context → expand)
2. Reflection outputs:
   - Quality scores для context elements (relevance, utility, clarity)
   - Conflict detection (contradictory strategies)

#### Phase 3: Curation

1. **Pruning:** Remove low-quality or obsolete context elements (quality score < threshold)
2. **Ranking:** Prioritize high-utility elements для limited context window
3. **Compression:** Summarize redundant information (e.g., 3 similar strategies → 1 generalized pattern)
4. **Update:** Commit curated context → next iteration baseline

#### Phase 4: Validation

1. Run task suite с curated contexts
2. Measure performance delta vs baseline
3. If improvement > threshold → promote to production
4. If degradation → rollback, analyze failure mode

### Tools/Inputs

- **LLM API:** For generation, reflection, curation
- **Eval suite:** Benchmark tasks для validation
- **Context storage:** Version-controlled prompts/memory (e.g., git for offline, DB for online)
- **Metrics:** Task success rate, latency, cost (token usage)

### Outputs

- **Curated system prompts** (offline)
- **Optimized memory structures** (online)
- **Performance delta report** (baseline vs ACE)

### Distinctions

**Prompt Engineering ≠ Context Engineering:**

| Aspect | Prompt Eng | Context Eng (ACE) |
|--------|-----------|-------------------|
| Scope | Single prompt optimization | System-wide context (prompts + memory + tools) |
| Process | Manual/one-shot | Iterative/evolutionary (gen → reflect → curate) |
| Temporal | Static | Dynamic (offline + online) |
| Target | Human writes, LLM executes | LLM writes, LLM curates (agentic) |

**Static RAG ≠ Context Engines (ACE):**

| Aspect | Static RAG | Context Engine (ACE) |
|--------|-----------|---------------------|
| Retrieval | Query → fixed retrieval (no evolution) | Query → adaptive retrieval + curation |
| Memory | External DB (no self-improvement) | Self-curating memory (learns from execution) |
| Playbook | None (each query independent) | Evolving playbook (strategies accumulate) |

### Related Entities

- **DP.M.003** (Context Engineering Protocol) — parent concept, ACE = specific technique
- **DP.SOTA.002** (Context Engineering) — SOTA update (add ACE as leading method 2026)
- **WP-179** (GEPA Test Framework) — apply ACE для context optimization в GEPA validation
- **AS.M.005** (Agentic Plan Caching) — synergy: cached plans + curated contexts = faster + better agents

---

## Candidate #4: ECO.SOTA.001 Enrichment — The Efficacy Reckoning (2026) [HIGH]

### Metadata

- **Type:** SOTA Update (enrichment existing entity)
- **Target:** ECO.SOTA.001 (EdTech Seed Funding Environment 2024-2026)
- **Sources:**
  - [2026 EdTech Trends: Efficacy Reckoning (OpenFieldX)](https://openfieldx.com/edtech-trends-2026/)
  - [EdTech Funding News 2026 (Talks Android)](https://talksandroid.com/edtech-funding-news-2026-trends/)

### New Section for ECO.SOTA.001

#### The Efficacy Reckoning (Q4 2025 — Q1 2026)

**Dominant trend:** Инвесторы и buyers требуют **Pedagogical Efficacy и Verifiable Skill Acquisition** вместо platform reach или engagement metrics. Это represents фундаментальный shift в EdTech evaluation criteria.

**Key Shifts:**

1. **From Engagement → Outcomes:**
   - Old: MAU, completion rates, time-on-platform
   - New: Measurable learning outcomes, skill assessments, job placement rates, certification pass rates

2. **From Passive Content → Agentic Systems:**
   - Old: Video lectures, quizzes, static content
   - New: Autonomous "Agentic AI" systems managing student feedback loops, personalization, workflows, admin tasks

3. **From Reach → Impact:**
   - Old: "10M users reached"
   - New: "X% skill acquisition verified, Y% job placement rate"

4. **Interoperability as Buying Requirement:**
   - 2025: Best practice
   - 2026: **Buying requirement** (buyers reject platforms that don't integrate with existing LMS/HRIS/skills ecosystems)

5. **Workforce Upskilling Focus:**
   - Corporate buyers prioritize **micro-credentials + simulation-based training** over traditional degree programs
   - 44.8% CAGR in workforce upskilling market (2026-2034)

**Investor Criteria (2026 Update):**
- **Capital efficiency:** Clear path to profitability (not "growth at all costs")
- **Pedagogical efficacy proof:** Evidence of learning impact (not anecdotes)
- **Verifiable skill acquisition:** Assessments, certifications, employer validation
- **Interoperability:** API-first, integrates with existing ecosystems

**Implication for fundraising (WP-145):**
Success depends on demonstrating **Pedagogical Efficacy** and **Verifiable Skill Acquisition**, not platform reach or simple engagement metrics. Founders must shift narrative от "X million students engaged" к "Y% skill mastery achieved, verified by Z assessments."

### Related Entities

- **ECO.D.007** (PMF-edu ≠ PMF) — усиливает: PMF-edu = efficacy, не adoption
- **ECO.M.001** (Fundraising) — updates investor criteria
- **WP-145** (Investor Deck) — narrative input: IWE = anti-efficacy-theater (FPF framework + ЦД metrics = verifiable intelligence development)

---

## Candidate #5: ECO Positioning Insight — Systems Thinking as Top Workforce Capability [HIGH]

### Metadata

- **Type:** Positioning Insight (narrative, не Pack entity)
- **Target:** ECO.M.004 (GTM Strategy) enrichment + WP-145 (Investor Deck) input
- **Sources:**
  - [Upskilling for 2026 (Upside Learning)](https://blog.upsidelearning.com/2025/12/22/upskilling-vs-reskilling-what-your-learning-strategy-should-focus-on-in-2026/)
  - [Six Shifts in Professional Upskilling 2026](https://www.univad.org/post/the-six-biggest-shifts-in-professional-upskilling-in-2026)
  - [WEF Work Transformation](https://www.weforum.org/stories/2025/12/work-transformation-skills-agility-growth/)

### Key Data

**Systems Thinking = Top Workforce Capability 2026:**
- Recognized as **one of most valuable long-term capabilities** because it:
  - **Transfers** across roles and industries
  - **Stretches** into new situations
  - **Amplifies** other skills
  - Enables people to **move internally** (not replaced)

**Workforce Upskilling Context (2026):**
- Skills shelf life **compressed** → upskilling now **continuous, strategic** (not side activity)
- Roles require **50-50 split: tech + human capabilities** (AI/data/cloud + leadership/EQ/adaptability/judgment)
- States (USA) creating **coordinated skills ecosystems** (education + employers + workforce support) with **real-time labor market insights**
- Skills-first procurement: AI literacy + problem-solving + creative thinking **embedded** в каждую программу

### Positioning for IWE (WP-145 Investor Deck)

**Old Narrative (generic EdTech):**
"IWE is an EdTech platform for systems thinking education."

**New Narrative (workforce intelligence infrastructure):**
"IWE is workforce intelligence infrastructure. We're not EdTech—we're the operating system for intelligence development. While traditional EdTech delivers content, IWE develops the #1 capability businesses need in 2026: systems thinking.

- **Market:** Workforce upskilling, 44.8% CAGR. Corporate buyers prioritize verifiable skill acquisition over degrees.
- **Unique approach:** FPF (10+ years, 5400+ docs) = framework корректности, не course library. You can't learn systems thinking from videos—you need operational framework.
- **Proof:** Digital twin tracks measurable intelligence characteristics (не engagement theater). Efficacy > reach.
- **Agentic AI:** Personalization based on learner state (PD characteristics), not content recommendations."

**Positioning Matrix:**

| Dimension | Traditional EdTech | IWE |
|-----------|-------------------|-----|
| Market | Education (B2C/B2B2C) | Workforce Intelligence (B2B) |
| Product | Content delivery | Intelligence infrastructure |
| Value Prop | Learn skills | Develop thinking capability |
| Proof | Completion rates | Measurable characteristics (ЦД) |
| Differentiation | Content library size | Operational framework (FPF) |
| AI Role | Content recommendations | Cognitive exoskeleton (персонализация по состоянию) |

### Application to WP-145

**Slides to update:**
1. **Market slide:** Workforce upskilling 44.8% CAGR, systems thinking = top capability 2026 (sources)
2. **Problem slide:** "The Efficacy Problem" — engagement ≠ learning, reach ≠ impact
3. **Solution slide:** IWE = anti-efficacy-theater (FPF framework + ЦД metrics)
4. **Positioning slide:** "We're not EdTech—we're workforce intelligence infrastructure"
5. **Traction slide:** Reframe users as "verified intelligence development" (ЦД metrics), не "X students enrolled"

### Related Entities

- **ECO.M.004** (GTM Strategy) — add workforce upskilling positioning
- **ECO.D.003** (Education ≠ Intelligence Development) — reinforces distinction
- **ECO.SOTA.001** (Efficacy Reckoning) — synergy: efficacy demand + systems thinking supply
- **WP-145** (Investor Deck) — narrative input

