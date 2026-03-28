# Scout Report — 2026-03-28

> Автоматический отчёт. Модель: sonnet. Бюджет: $10.0.
> Находок: 4 | Capture-кандидатов: 3 | WP-предложений: 0
> **Статус ревью:** ✅ проверен (28 мар, разбор #5)

## Статус заданий (backlog)

  - id: rt-001	    title: "Реальные кейсы автономных агентов в проде"	    status: done
  - id: rt-002	    title: "SOTA методы написания текстов для соцсетей (антидетект AI)"	    status: moved_to_session
  - id: rt-003	    title: "Fundraising best practices для seed-раунда EdTech/Intelligence Platform"	    status: done
  - id: rt-004	    title: "SOTA методы бизнес-моделирования для EdTech/SaaS"	    status: done

## Находки (ТОП-4)

# Scout Report — 2026-03-28

## Метрики

- **Сканировано источников:** 6 (arXiv, Anthropic, HN, 4 web searches)
- **Потенциальных находок:** 11
- **Dedup filtered:** 1 (World Models — вне scope)
- **Enrichments:** 3 (DP.SC.019, ECO.SOTA.001, AS.SOTA.001)
- **Новых сущностей:** 5
- **Итого выбрано:** TOP-5

---

## TOP-5 Находок (ранжировано по приоритету)

### #1: Enterprise AI Agents Production: 72% G2000 Beyond Pilots (2026)

**Источник:** [AI Agents in 2026: From Hype to Enterprise Reality](https://www.kore.ai/blog/ai-agents-in-2026-from-hype-to-enterprise-reality), [Enterprise AI Agent Adoption Accelerates](https://insights.reinventing.ai/articles/openclaw-enterprise-adoption-march-2026-03-16), [Multimodal AI Statistics](https://www.multimodal.dev/post/agentic-ai-statistics)

**Релевантность:** Высокая  
**Связь:** AS.SOTA.001 (enrichment), WP-144 (investor deck — proof of SOTA adoption)

**Суть:**  
Март 2026: 72% Global 2000 перешли от пилотов к production AI agents. Конкретные метрики ROI: 20% cost savings (industrial maintenance), 15% uptime (manufacturing), 85% tier-1 support automation (Salesforce), 79% organizations report measurable productivity gains, 62% expect ROI >100%. Gartner: 40% enterprise apps embed agents by 2026. Ключевые домены: IT ops, finance, onboarding, support.

**Reasoning:**  
Критерий: обновление SOTA + связь с РП. AS.SOTA.001 датирован 2026 but needs Q1 data. Эти метрики — proof для investor pitch (WP-145): autonomous agents не hype, а production reality с измеримым ROI. Конкретные цифры для калибровки IWE narrative: "мы в mainstream adoption wave".

**Предложение:**
- **Тип:** SOTA-обновление (enrichment)
- **Куда:** AS.SOTA.001
- **Действие:** Enrichment AS.SOTA.001 — добавить Q1 2026 metrics + case studies (Salesforce, industrial, finance). Источники: kore.ai, reinventing.ai, multimodal.dev

---

### #2: EdTech Funding 2026 — Workforce Upskilling 44.8% CAGR, Seed Resilient

**Источник:** [EdTech 2026 Trends](https://tracxn.com/d/sectors/edtech/__fPwPVORWpMV0ZBc8pzbBQuRHbHgOhpGTjddL4QIjHg8), [EdTech Funding Sources](https://qubit.capital/blog/edtech-funding-sources), [OpenFieldX EdTech Trends](https://openfieldx.com/edtech-trends-2026/)

**Релевантность:** Высокая  
**Связь:** ECO.SOTA.001 (enrichment), WP-145 (deck positioning), WP-183 (CRM — target segment)

**Суть:**  
2026 данные: $2.8B seed-growth funding (flat vs 2024, stabilized). Seed/Series A resilient для high NRR. Workforce Upskilling 44.8% CAGR → 2030. Investor priorities: capital efficiency, measurable outcomes, "Efficacy Reckoning" (proof of pedagogical impact). Agentic AI + personalization = top trend. EdTech avg 8.1x revenue multiples (2025). IWE positioning: corporate upskilling через systems thinking.

**Reasoning:**  
Критерий: обновление SOTA + прямая связь с РП. WP-145 (investor deck) нуждается в fresh benchmarks для ask calibration. 44.8% CAGR workforce upskilling = IWE's TAM narrative. "Efficacy Reckoning" = наше конкурентное преимущество (методология FPF, measurable progress через ЦД). ECO.SOTA.001 нуждается в 2026 update.

**Предложение:**
- **Тип:** SOTA-обновление (enrichment)
- **Куда:** ECO.SOTA.001
- **Действие:** Enrichment ECO.SOTA.001 — добавить 2026 Q1 benchmarks: $2.8B, workforce upskilling CAGR, Efficacy Reckoning. Источники: Tracxn, Qubit Capital, OpenFieldX

---

### #3: ElephantBroker — Cognitive Runtime for Trustworthy AI Agents

**Источник:** [arXiv:2603.25097](https://arxiv.org/abs/2603.25097) — Cristian Lupascu, Alexandru Lupascu (27 марта 2026)

**Релевантность:** Высокая  
**Связь:** AS.M.001 (Trust Stack), AS (verification), WP-179 (testing agents)

**Суть:**  
Новая система: когнитивная среда исполнения (cognitive runtime) для верификации и обеспечения надежности поведения ИИ-агентов. Knowledge-grounded approach. Цель: trustworthy AI agents через runtime verification, не только pre-deployment testing. Архитектурный паттерн для production agents.

**Reasoning:**  
Критерий: новый метод, применимый к IWE. AS.M.001 (Trust Stack) описывает дизайн governance, но нет runtime verification layer. ElephantBroker = missing piece: как верифицировать агента **во время выполнения**, не только при деплое. Релевантно для WP-179 (E2E agent testing) и будущего Trust Stack implementation. Может быть AS.M.XXX (новый метод) или AS.SOTA.XXX (архитектурный паттерн).

**Предложение:**
- **Тип:** Метод или SOTA (требует детального чтения paper)
- **Куда:** AS (новая сущность или enrichment AS.M.001)
- **Действие:** Capture candidate — прочитать paper, извлечь: (1) архитектуру cognitive runtime, (2) методы runtime verification, (3) integration pattern с существующими agents. Если метод → AS.M.XXX. Если архитектурный SOTA → AS.SOTA.XXX. Связь с Trust Stack Design.

---

### #4: Long-Running Claude for Scientific Computing — Multi-Day Tasks

**Источник:** [Anthropic Science Blog](https://www.anthropic.com/news/long-running-claude-for-scientific-computing) (23 марта 2026)

**Релевантность:** Средняя  
**Связь:** DP.SC.019 (Cloud Runtime), AS (длительные автономные задачи), WP-132 (scheduler)

**Суть:**  
Anthropic публикует практическое руководство: как запускать Claude Code на multi-day задачах. Паттерны: test oracles (проверка корректности), persistent memory (состояние между сессиями), orchestration (координация длительных процессов). Применение: научные вычисления, но паттерны универсальны.

**Reasoning:**  
Критерий: enrichment существующего SC + применимо к текущим РП. DP.SC.019 (Автономная работа IWE) описывает концепцию, но lacks конкретные паттерны. Anthropic guide = actionable how-to для multi-day agents (WP-132 scheduler, future autonomous extractors/strategists). Test oracles = verification pattern (связь с VR.M.001). Persistent memory = AS.M.006 (Four-Type Memory). Orchestration = multi-agent coordination.

**Предложение:**
- **Тип:** Enrichment (паттерны для существующего SC)
- **Куда:** DP.SC.019 + возможно новый DP.M.XXX (Multi-Day Orchestration)
- **Действие:** Enrichment DP.SC.019 — добавить секцию "Multi-Day Patterns" с: test oracles, persistent memory, orchestration. Источник: Anthropic Science Blog. Рассмотреть новый метод DP.M.XXX если паттернов >3.

---

### #5: Formal Semantics for Agentic Tool Protocols

**Источник:** [arXiv:2603.24747](https://arxiv.org/abs/2603.24747) — Andreas Schlapbach (27 марта 2026)

**Релевантность:** Средняя  
**Связь:** DP.SOTA (протоколы), MCP, AS (tool use)

**Суть:**  
Формальная семантика для инструментальных протоколов агентов на основе исчисления процессов (process calculus). Цель: математически строгое описание взаимодействия agent ↔ tool. Может быть применимо к MCP или другим agent tool protocols.

**Reasoning:**  
Критерий: новый SOTA в протоколах. DP.SOTA.003 (Open API Specs) + DP.SOTA.014 (MCP) описывают протоколы, но lacks формальная семантика. Process calculus = верификация корректности протокола (связь с VR). Может быть полезно для governance MCP или будущих протоколов IWE. Средний приоритет — requires чтение paper для оценки применимости.

**Предложение:**
- **Тип:** SOTA (формальные методы)
- **Куда:** DP.SOTA.XXX (новая сущность) или enrichment DP.SOTA.003/014
- **Действие:** Capture candidate — прочитать paper, извлечь: (1) какие протоколы покрывает, (2) применимость к MCP, (3) как использовать для верификации tool protocols. Если general framework → новый DP.SOTA.XXX. Если MCP-specific → enrichment DP.SOTA.014.

---

## Отклонённые находки (не вошли в TOP-5)

### World Models for Embodied AI (ICLR 2026 Workshop)
**Причина:** DEDUP_SKIP — вне scope IWE. IWE не использует embodied AI (нет роботов, физических агентов). Workshop focus: robotics, simulation, 3D reconstruction. Не применимо к knowledge work platform. Правило #5: ценность = что можно применить.

### MCP → AAIF Donation (Governance Shift)
**Причина:** Низкая приоритет. MCP уже используется в IWE (Gmail, Calendar, DDT MCP servers). AAIF governance = organizational shift, не влияет на текущую архитектуру или методы. DP.SOTA.014 уже описывает MCP как де-факто стандарт 2026. Donation to Linux Foundation = confirmation, не новая информация.

### IRC Agent on $7/month VPS (HN)
**Причина:** Низкая приоритет. Интересный минималистичный подход (AS — minimal footprint agents), но lacks методологической глубины. Пока нет concrete patterns или failure modes. Может вернуться если HN thread раскроет архитектурные детали.

### .claude/ Folder Anatomy (HN)
**Причина:** Низкая приоритет. Может быть релевантно для DP.EXOCORTEX.001 (структура локального хранилища), но thread пока без substance. Если появится детальный разбор структуры → вернуться.

### GitHub Training Opt-Out Controversy
**Причина:** Governance/policy, не методологическая ценность. Не применимо к IWE architecture или methods. Мониторить как тренд (IP protection), но не захватывать.

### Anthropic Economic Index (Learning Curves)
**Причина:** Интересно, но нет actionable insights. "Learning curves" = usage patterns Claude, но report за paywall или summary недоступен. Если получу детали (например, какие use cases растут fastest) — может стать finding.

---

## Метрики сессии

- **Dedup filtered:** 1
- **Enrichments:** 3 (AS.SOTA.001, ECO.SOTA.001, DP.SC.019)
- **Новых capture candidates:** 2 (ElephantBroker, Formal Semantics)
- **Конверсия потенциальных → TOP-5:** 5/11 = 45%


## Capture-кандидаты

> Решение: ✅ принять → Экстрактор формализует в Pack | ❌ отклонить → trajectory | 🔄 доработать → backlog

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


