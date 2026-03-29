# Принятые находки Scout (few-shot примеры)

> Этот файл обновляется автоматически через S54 (Feedback Loop).
> Scout использует его как few-shot для калибровки качества.

## 2026-03-20 #1: Автономия ≠ Автоматизация (WEF)

**Источник:** WEF «AI Agents in Action»
**Тип:** различение
**Куда:** PACK-autonomous-agents → AS.D.001

### Суть
WEF определяет автономию как «гибкость принятия решений» (агент выбирает что делать), а автоматизацию как «надёжное исполнение» (система делает что запрограммировано). Это разные классы систем с разными требованиями к governance.

### Reasoning
Прямо применимо к WP-132: scheduler.sh = автоматизация, новые агенты = автономия. Объясняет почему нужен Trust Stack, а не просто мониторинг. Содержит чёткое различение X ≠ Y.

---

## 2026-03-20 #2: WISC Framework (Context Engineering)

**Источник:** LangChain Blog, Victor Dibia Newsletter
**Тип:** SOTA-обновление
**Куда:** PACK-digital-platform → DP.SOTA.002 (расширение)

### Суть
Context Engineering детализируется в WISC: Write (формирование контекста), Isolate (изоляция контекстов между агентами), Select (выбор релевантного), Compress (сжатие для вместимости). Конкретнее чем общий SOTA.002.

### Reasoning
Прямо применимо к управлению trajectory cache в Scout и к проектированию multi-agent pipeline.

### Правка (2026-03-23)
Добавлена детализация по Anthropic Cookbook: конкретный маппинг на IWE-агентов (Scout→Write, scheduler→Isolate, dispatcher→Select, trajectory-cache→Compress). Ценное: переход от абстрактного фреймворка к конкретным ролям. Подтверждает: WISC = платформенный паттерн (DP.SOTA), не метод агента (AS.M).

---

## 2026-03-20 #3: GEPA Framework (Self-Improvement через Trajectory)

**Источник:** OpenAI Cookbook, Awesome-Self-Evolving-Agents
**Тип:** метод
**Куда:** PACK-autonomous-agents → AS.M.001 (расширение)

### Суть
Конкретный алгоритм self-improvement через trajectory: Generate → Evaluate → Prune → Augment.

### Reasoning
Прямая реализация для AS.M.001 (improvement loop design). Ценное: пошаговая процедура, не просто принцип.

### Правка (2026-03-23)
Обогащена конкретикой из ICLR 2026 Oral: (1) метрики GEPA vs GRPO/MIPROv2 (+40% task success, -30% hallucination), (2) failure modes FM.001 (Overfitting to positive trajectories) + FM.002 (Evaluation Function Misalignment), (3) mitigation через diverse seed examples + proxy metrics. Подтверждает: GEPA не просто «идея», а метод с измеримыми результатами. AS.M.001 существует → расширить его этими данными, не создавать AS.M.002.

---

## 2026-03-23 #4: Production Autonomous Agents — ROI и Operationalization Gap

**Источник:** McKinsey Digital, Singapore IMDA
**Тип:** SOTA-обновление + Failure Mode
**Куда:** (1) PACK-autonomous-agents → AS.SOTA.002, (2) AS.FM.008

### Суть
Конкретные ROI benchmarks: 200–500% ROI в customer service (McKinsey), 30–60% reduction in manual review (Singapore IMDA). Критический failure mode: 40% проектов провалились из-за организационных причин (Operationalization Gap), не технических. Governance + change management = необходимость, не опция.

### Reasoning
Прямая релевантность для WP-142 (fundraising pitch). Отвечает на вопрос «а сколько это стоит и что даёт?». AS.FM.008 объясняет, почему хорошая технология может провалиться. Ценное: количественные данные для стратегических решений.

---

## 2026-03-23 #5: WEF Trust Stack — 5-Layer Model + Progressive Governance

**Источник:** WEF «AI Agents in Action», Singapore IMDA
**Тип:** метод
**Куда:** PACK-autonomous-agents → AS.M.001 (расширение Trust Stack Design)

### Суть
Детализация Trust Stack в 5 слоёв: (1) Legible Reasoning, (2) Bounded Agency, (3) Goal Transparency, (4) Contestability, (5) Oversight. Progressive Governance: T0 (no autonomy) → T4 (full autonomy), safeguards пропорционально уровню.

### Reasoning
AS.M.001 уже содержит Trust Stack Design. Это расширение с конкретной структурой и континуумом governance. Ценное: переход от чеклиста к проектируемой системе. Правило: не создавать AS.M.003, расширить AS.M.001.

### Правка (2026-03-24)
Обогащение: CSA ATF framework (Zero Trust для AI agents), IWE Audit таблица (текущий статус по 5 слоям), action items (formalize Scout feedback loop, narrow Strategist scope, override logging).

---

## 2026-03-24 #6: EdTech Seed Funding ROI vs Reality Gap

**Источник:** Failory, Qubit Capital, OpenVC
**Тип:** метод + failure mode
**Куда:** ECO.M.001 (обогащение fundraising method), ECO.FM.001

### Суть
EdTech funding 89% decline. Average check $7.8M. YC seed 2026: proof of traction (20%+ MoM OR early contracts). Failure mode: pitch без metrics = автоотказ. Bottom-up projections обязательны.

### Reasoning
Прямое попадание в WP-145. Конкретные цифры для калибровки ask и narrative. Применено: deck v0.3 → ask $3-5M, traction reframe ($240K ARR @ $0 CAC + 10 корп. клиентов).

---

## 2026-03-24 #7: EdTech B2B SaaS Unit Economics

**Источник:** Maxio 2025 Benchmarks, SaaS Capital
**Тип:** метрика
**Куда:** ECO.M.002 (расширение)

### Суть
EdTech = highest churn (9.6% monthly). Expansion revenue = 40% new ARR. NRR >106% → 2.5x faster growth. CAC $1,143 benchmark. Применено: deck v0.3 слайд 10 — benchmarks + retention strategy.

---

## 2026-03-24 #8: JTBD в EdTech: 5 Stakeholders, Workforce Upskilling

**Источник:** jobstobedone.org, Christensen Institute
**Тип:** метод
**Куда:** ECO.M.003 (новый)

### Суть
JTBD для EdTech: 5 стейкхолдеров. Workforce upskilling 44.8% CAGR. Christensen: disruptive innovation. IWE позиционирование: corporate upskilling через systems thinking.

---

## 2026-03-24 #9: Inbound Fundraising: Visibility > Pitching

**Источник:** fleeting-notes.md (23 мар)
**Тип:** стратегия
**Куда:** ECO.M.001 (секция Inbound Strategy)

### Суть
5-step: экспертная видимость, публичный трекшн, EN-площадки, «умные списки», стратегические советники. Принцип: «поезд, который уже едет».

---

## 2026-03-23 #10: Failure Modes — Loop of Death, Self-Consistency Trap, Hallucination in Action

**Источник:** Medium (Loop of Death), Unite.AI (Hidden Failure Modes), GitHub (Awesome Agent Failures)
**Тип:** failure modes (3 новых)
**Куда:** PACK-autonomous-agents → AS.FM.009, AS.FM.010, AS.FM.011

### Суть
Три конкретных production failure modes:
- **FM.009 Loop of Death** (критический): агент в retry loop, сжигает $ за минуты. 90% production failures — не hallucination, а это. Mitigation: timeout, max_retries=3-5, divergence detection, cost circuit breaker.
- **FM.010 Self-Consistency Trap** (средний): majority vote даёт wrong consensus. Mitigation: external validation, diversity check, связь с GEPA (Pareto > majority vote).
- **FM.011 Hallucination in Action** (критический): false text → annoying, false action → irreversible. Mitigation: read/write separation, dry-run, rollback, source-of-truth anchoring.

### Reasoning
Правило #12: FM с конкретикой = высокая ценность. Все три с именами, сценариями, severity, mitigation, примерами. Прямая связь с scheduler.sh (WP-132) и Trust Stack (AS.M.001).

---

## 2026-03-27 #11: AS.FM.019 — Behavioral Drift in Multi-Agent Systems

**Источник:** CIO, Machine Learning Mastery
**Тип:** failure mode
**Куда:** PACK-autonomous-agents → AS.FM.019

### Суть
Постепенная деградация поведения агентной системы в production (недели-месяцы). Причина: incremental changes (обновление модели, промпта, инструментов). Каждое изменение individually safe, но cumulatively = behavior shifts. Различение vs DP.FM.005: внутренний drift системы ≠ устаревание модели от внешних изменений.

### Reasoning
Новый класс FM. Не дубль существующих (012-018 = технические, FM.005 = external drift). Конкретные mitigation: behavioral snapshots, prompt versioning, staged rollouts, circuit breakers. Применимо к WP-132 (scheduler), WP-179 (GEPA → drift detection).

---

## 2026-03-27 #12: AS.FM.020 — Production Deployment Failure (Organizational)

**Источник:** Digital Applied, HBR, Use Apify
**Тип:** failure mode
**Куда:** PACK-autonomous-agents → AS.FM.020

### Суть
88% агентных проектов не доходят до production. Причина не технические ошибки, а organizational readiness gap: нет governance, нет accountability framework, нет observability, legacy incompatibility. Gartner: 40% agentic AI projects отменены к 2027. Различение: Technical FM (012-018) ≠ Organizational FM (020).

### Reasoning
Дополняет технические FM организационным классом. Статистика сильная (HBR, Gartner). Mitigation: pre-deployment governance checklist, organizational readiness audit (отдельный gate после GEPA). Прямо применимо к WP-179 Phase 2.

---

## 2026-03-27 #13: ECO.SOTA.001 enrichment — Efficacy Reckoning Q1 2026

**Источник:** OpenFieldX, Talks Android
**Тип:** SOTA-обновление (обогащение)
**Куда:** PACK-ecosystem → ECO.SOTA.001 (новая секция)

### Суть
Фундаментальный сдвиг: инвесторы требуют Pedagogical Efficacy, не platform reach. Engagement → Outcomes, Reach → Impact, Content → Agentic Systems. Interoperability = buying requirement (не best practice). Workforce upskilling 44.8% CAGR.

### Reasoning
ECO.SOTA.001 существует, это обогащение (не новая сущность). Данные свежие (Q1 2026). Прямое влияние на WP-145 (investor deck narrative).

---

## 2026-03-28 #14: AS.SOTA.005 — Cognitive Runtime (ElephantBroker)

**Источник:** arXiv:2603.25097, Lupascu & Lupascu, March 2026
**Тип:** SOTA (архитектурный паттерн, не пошаговый метод)
**Куда:** PACK-autonomous-agents → AS.SOTA.005

### Суть
ElephantBroker — cognitive runtime, объединяющий: 6-фазный когнитивный цикл (store→retrieve→score→compose→protect→learn), 4-state evidence verification model (Unverified→Self-Supported→Tool-Supported→Supervisor-Verified), 11-мерную систему скоринга контекста, 6-слойный guard pipeline с AI firewall и tool-call interception, 9-стадийную консолидацию памяти. Ключевое различение: runtime verification ≠ pre-deployment testing.

### Reasoning
Paper прочитан полностью. Это SOTA (архитектура), не метод (нет пошагового алгоритма для пользователя). Не дубль — ни один Pack-документ не покрывает runtime verification для агентов. Прямая связь с AS.M.001 (Trust Stack — missing runtime layer), WP-179 (GEPA = pre-deployment, ElephantBroker = runtime complement), AS.FM.019 (behavioral drift detection через consolidation engine).

---

## 2026-03-28 #15: AS.SOTA.001 enrichment — Enterprise Q1 2026 Metrics

**Источник:** kore.ai, reinventing.ai, multimodal.dev
**Тип:** SOTA-обновление (обогащение)
**Куда:** PACK-autonomous-agents → AS.SOTA.001 (новая секция)

### Суть
72% Global 2000 beyond pilots. ROI: 20% cost savings (industrial), 85% tier-1 support automation. 79% organizations report productivity gains. Gartner: 40% enterprise apps embed agents by 2026.

### Reasoning
AS.SOTA.001 существует, свежие метрики Q1 2026. Количественные данные для стратегических решений.

---

## 2026-03-29 #16: AS.SOTA.006 — Agentic Reasoning Three-Layer Framework

**Источник:** arxiv:2601.12538 (Jan 2026)
**Тип:** SOTA (новая сущность)
**Куда:** PACK-autonomous-agents → AS.SOTA.006

### Суть
Архитектурный паттерн: три слоя способностей агента. Layer 1 (Foundational): planning, tool use, reasoning, memory. Layer 2 (Self-Evolving): improvement loop, reflexion, trajectory caching. Layer 3 (Collective): coordination, distributed problem-solving, emergent capabilities. Agent = actor in environment, не text predictor.

### Reasoning
Не покрыт существующими AS.SOTA.001-005. Формализует то, что уже неявно используется (AS.D.006 = Layer 2, AS.M.005 = Layer 2 mechanism). Чёткое различение от DP.SOTA.006 (development tools). Применимо к WP-179 (GEPA design), WP-171 (Hub architecture), WP-132 (scheduler = L1+L2).

---

## 2026-03-29 #17: AS.FM.019 enrichment — Agent Drift Taxonomy (3 типа + PBSS)

**Источник:** arxiv:2601.04170, arxiv:2506.10095, Maxim AI Guide
**Тип:** failure mode (обогащение)
**Куда:** PACK-autonomous-agents → AS.FM.019 (существующий)

### Суть
Три типа дрейфа: semantic (отклонение от intent), coordination (разрушение consensus), behavioral (непредусмотренные стратегии). PBSS Framework: дрейф БЕЗ изменений промпта из-за tokenization/decoding artifacts. Два механизма: config-driven (уже в FM.019) + spontaneous (PBSS, новое).

### Reasoning
FM.019 уже существует (28 мар). Обогащение таксономией лучше, чем новый FM.021 — избегаем дублирования. PBSS = новый механизм дрейфа (без триггера), дополняет config-driven drift.

---

## 2026-03-29 #18: ECO.SOTA.001 enrichment — Logic Models + 10% Threshold

**Источник:** OpenFieldX, Talks Android
**Тип:** SOTA-обновление (обогащение)
**Куда:** PACK-ecosystem → ECO.SOTA.001

### Суть
Logic Models requirement: founders обязаны предоставить third-party research с доказательством улучшения ≥10%. Skills transparency = buying requirement. Capital efficiency > growth-at-all-costs.

### Reasoning
ECO.SOTA.001 уже содержит Efficacy Reckoning секцию. Добавлены конкретные thresholds (10%, Logic Models), которых ранее не было.

---

## 2026-03-29 #19: DP.SOTA.002 enrichment — CE Best Practices 2026

**Источник:** SwirlAI Newsletter, LogRocket, Comet ML
**Тип:** SOTA-обновление (обогащение)
**Куда:** PACK-digital-platform → DP.SOTA.002

### Суть
4 паттерна: sliding window + summarization, context routing, tool loadout optimization (>30 = confusion), RAG not obsolete (>100K degrades reasoning). Challenges: context rot, mode collapse.

### Reasoning
DP.SOTA.002 содержит WISC framework и Gartner data, но не конкретные 2026 patterns. Обогащение actionable.

---

## 2026-03-29 #20: DP.SOTA.014 enrichment — MCP 2026 Roadmap (4 приоритета)

**Источник:** MCP Blog, The New Stack, Use Apify
**Тип:** SOTA-обновление (обогащение)
**Куда:** PACK-digital-platform → DP.SOTA.014

### Суть
4 приоритета core maintainers: transport scalability, agent communication (multi-day), governance maturation (audit, SSO), enterprise readiness. Market $1.8B. NOT ISO standard — open specification.

### Reasoning
DP.SOTA.014 содержал только текущий статус. Roadmap = forward-looking, влияет на архитектурные решения (WP-187, WP-171).

---

## 2026-03-29 #21: AS.M.001 enrichment — WEF Trust Stack + CSA ATF

**Источник:** WEF Trust Stack (2026), CSA ATF
**Тип:** метод (обогащение)
**Куда:** PACK-autonomous-agents → AS.M.001

### Суть
WEF: 3 компонента trust stack (legible reasoning, bounded agency, transparent decision records). CSA ATF: 4-layer defense-in-depth. Industry maturity 2.3/5. Nvidia GTC: нет решений для agent-to-agent trust, memory poisoning, cryptographic binding.

### Reasoning
AS.M.001 уже содержит Trust Stack Design. Обогащение: конкретные CSA layers, maturity data, открытые проблемы.

---

## 2026-03-29 #22: AS.SOTA.002 enrichment — Framework Status Q1 2026

**Источник:** o-mega.ai, DataCamp
**Тип:** SOTA-обновление (обогащение)
**Куда:** PACK-autonomous-agents → AS.SOTA.002

### Суть
AutoGen → maintenance mode (Microsoft Agent Framework). CrewAI: 40% faster TTM. LangGraph: production leader. Обновлённая рекомендация по use cases.

### Reasoning
AS.SOTA.002 содержал LangGraph vs CrewAI. AutoGen status change = значительный shift. Добавлена 3-way comparison.

---

## 2026-03-29 #23: AS.SOTA.003 enrichment — CSA ATF Maturity + Nvidia GTC Gaps

**Источник:** CSA ATF, Nvidia GTC 2026
**Тип:** SOTA-обновление (обогащение)
**Куда:** PACK-autonomous-agents → AS.SOTA.003

### Суть
Maturity 2.3/5, только 1/3 ≥3. Nvidia GTC: нерешённые проблемы (agent-to-agent trust, memory poisoning, cryptographic binding). CSA ATF: 4-layer defense-in-depth.

### Reasoning
AS.SOTA.003 содержал WEF/Singapore framework. Добавлены quantitative maturity data и открытые проблемы.

---

## 2026-03-29 #24: DP.SOTA.013 enrichment — World Models Race Q1 2026

**Источник:** Introl, Built In
**Тип:** SOTA-обновление (обогащение)
**Куда:** PACK-digital-platform → DP.SOTA.013

### Суть
AMI Labs (€500M, LeCun), Genie 3 (DeepMind, 24fps 3D), World Labs Marble (Fei-Fei Li). Consensus: no model-free shortcut. Связь с AS.SOTA.006 Layer 1.

### Reasoning
DP.SOTA.013 содержал теоретический фреймворк. Добавлены конкретные инвестиции и консенсус 2026.

