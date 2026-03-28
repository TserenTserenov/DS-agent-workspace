# Capture Candidates — 2026-03-28

> Черновики для Экстрактора (R2). Формат: название, тип, куда, источник, ключевые элементы.

---

## Candidate #1: Cognitive Runtime for Agent Verification

**Тип:** Метод или SOTA (requires детальное чтение)  
**Куда:** AS.M.XXX (новый метод) или AS.SOTA.XXX (архитектурный паттерн)  
**Источник:** ElephantBroker paper, arXiv:2603.25097, 27 марта 2026

**Ключевые элементы (предварительные):**
- **Суть:** Когнитивная среда исполнения (cognitive runtime) для верификации AI-агентов во время выполнения (runtime), не только pre-deployment
- **Подход:** Knowledge-grounded — использование знаний для проверки корректности поведения
- **Цель:** Trustworthy AI agents через runtime verification
- **Архитектура:** (требует чтения paper — как встраивается в agent execution loop)
- **Связь:** AS.M.001 (Trust Stack Design) — missing runtime layer. VR.M.001 (Верификация по эталону) — может использовать этот runtime

**Действия для Экстрактора:**
1. Прочитать paper полностью
2. Извлечь: архитектуру cognitive runtime, методы runtime verification, integration patterns
3. Различить: runtime verification ≠ pre-deployment testing (может быть новое различение AS.D.XXX)
4. Если метод (пошаговый алгоритм) → AS.M.XXX
5. Если архитектурный паттерн (SOTA) → AS.SOTA.XXX
6. Связать с Trust Stack (AS.M.001) и Verification Pack (VR.M.001)

**Черновик различения (если применимо):**
```
AS.D.XXX | Runtime Verification ≠ Pre-Deployment Testing

| Аспект | Runtime Verification | Pre-Deployment Testing |
|--------|---------------------|----------------------|
| Когда | Во время выполнения агента | До деплоя |
| Что проверяет | Actual behavior в production | Expected behavior в test environment |
| Реакция на ошибку | Intervention / circuit breaker | Fix & redeploy |
| Coverage | Все edge cases (включая неожиданные) | Предусмотренные тест-кейсы |
| Overhead | Runtime cost (latency, compute) | No production overhead |
| Пример | ElephantBroker cognitive runtime | Unit tests, integration tests |
```

---

## Candidate #2: Formal Semantics for Agent Tool Protocols

**Тип:** SOTA (формальные методы)  
**Куда:** DP.SOTA.XXX (новая сущность) или enrichment DP.SOTA.003/014  
**Источник:** arXiv:2603.24747, Andreas Schlapbach, 27 марта 2026

**Ключевые элементы (предварительные):**
- **Суть:** Формальная семантика для tool protocols на основе process calculus (исчисление процессов)
- **Цель:** Математически строгое описание agent ↔ tool взаимодействия
- **Применимость:** MCP, другие agent protocols
- **Benefit:** Верификация корректности протокола, обнаружение deadlocks/race conditions
- **Связь:** DP.SOTA.003 (Open API Specs), DP.SOTA.014 (MCP), VR (verification methods)

**Действия для Экстрактора:**
1. Прочитать paper полностью
2. Извлечь: какие протоколы покрывает (MCP-specific или general), формализм (какой process calculus), примеры применения
3. Оценить применимость к IWE: можем ли верифицировать наши MCP servers через эту семантику?
4. Если general framework → новый DP.SOTA.XXX "Formal Methods for Agent Protocols"
5. Если MCP-specific → enrichment DP.SOTA.014 (добавить секцию "Formal Verification")
6. Связать с VR Pack (формальная верификация как метод)

**Черновик SOTA (если новая сущность):**
```
DP.SOTA.XXX | Formal Methods for Agent Tool Protocols (2026)

**Описание:**  
Применение формальных методов (process calculus) для математически строгого описания и верификации протоколов взаимодействия agent ↔ tool. Позволяет обнаруживать deadlocks, race conditions, protocol violations до runtime.

**Источник:** arXiv:2603.24747 (Schlapbach, 2026)

**Ключевые концепции:**
- Process calculus для agent protocols
- Формальная семантика tool invocation
- Верификация корректности протокола
- Применимость к MCP и другим стандартам

**Применение в IWE:**
(заполнить после чтения paper — как использовать для верификации MCP servers)

**Связь:**
- DP.SOTA.014 (MCP) — формальная верификация MCP-протокола
- VR.M.001 (Верификация по эталону) — формальные методы как вид верификации
- AS (tool use patterns) — корректность tool invocation
```

---

## Enrichment Candidates (не требуют новых файлов)

### Enrichment #1: AS.SOTA.001 — Enterprise AI Agents Production (Q1 2026 Update)

**Что добавить:**  
Секция "Q1 2026 Production Metrics" в AS.SOTA.001

**Данные:**
- 72% Global 2000 beyond pilots (vs XX% в предыдущей версии)
- ROI metrics: 20% cost savings (industrial), 15% uptime (manufacturing), 85% tier-1 support automation (Salesforce)
- 79% organizations report productivity gains, 62% expect ROI >100%
- Gartner forecast: 40% enterprise apps embed agents by 2026
- Key domains: IT ops, finance, onboarding, support

**Источники:**
- kore.ai/blog/ai-agents-in-2026-from-hype-to-enterprise-reality
- insights.reinventing.ai/articles/openclaw-enterprise-adoption-march-2026-03-16
- multimodal.dev/post/agentic-ai-statistics

---

### Enrichment #2: ECO.SOTA.001 — EdTech Seed Funding Environment (2026 Update)

**Что добавить:**  
Секция "2026 Q1 Benchmarks" в ECO.SOTA.001

**Данные:**
- $2.8B seed-growth funding globally (flat vs 2024, stabilized)
- Workforce Upskilling: 44.8% CAGR → 2030
- Investor priorities: capital efficiency, measurable outcomes, "Efficacy Reckoning" (proof of pedagogical impact)
- Agentic AI + personalization = top trend
- EdTech avg revenue multiples: 8.1x (2025)
- Seed/Series A resilient for high NRR companies

**Источники:**
- tracxn.com/d/sectors/edtech
- qubit.capital/blog/edtech-funding-sources
- openfieldx.com/edtech-trends-2026

---

### Enrichment #3: DP.SC.019 — Автономная работа IWE (Multi-Day Patterns)

**Что добавить:**  
Секция "Multi-Day Orchestration Patterns" в DP.SC.019

**Паттерны (из Anthropic Science Blog):**
1. **Test Oracles** — проверка корректности промежуточных результатов длительной задачи
2. **Persistent Memory** — сохранение состояния между сессиями (связь с AS.M.006 Four-Type Memory)
3. **Orchestration** — координация этапов multi-day процесса

**Применение в IWE:**
- WP-132 (scheduler) — orchestration для ночных агентов
- Future autonomous extractors/strategists — multi-day research tasks
- Связь с VR.M.001 (test oracles = runtime verification)

**Источник:**
- anthropic.com/news/long-running-claude-for-scientific-computing (23 марта 2026)

