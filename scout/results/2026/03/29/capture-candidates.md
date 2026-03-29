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

