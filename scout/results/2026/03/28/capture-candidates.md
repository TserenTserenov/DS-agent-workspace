# Capture Candidates — 2026-03-28

Черновики для Экстрактора (R2). Только Pack-знание (различения, методы, SOTA).

---

## Candidate #1: AS.D.009 — Bounded Autonomy ≠ Graduated Governance

**Pack:** PACK-autonomous-agents  
**Тип:** Различение  
**ID:** AS.D.009  
**Источник:** arxiv 2512.04123v1, MongoDB blog 2026  

### Черновик

```markdown
# Bounded Autonomy ≠ Graduated Governance

## Различение

| Аспект | Bounded Autonomy | Graduated Governance |
|--------|------------------|---------------------|
| **Суть** | Технические лимиты в runtime (step count, retry policy, cost ceiling, timeout) | Политика доверия по уровням зрелости агента (T0-T4) |
| **Уровень** | Execution-time constraints | Design-time trust framework |
| **Вопрос** | Что агент МОЖЕТ сделать технически? | Какому агенту мы ДОВЕРЯЕМ что делать? |
| **Пример** | Max 10 steps → fail → escalate human | T0 agent: read-only, T4 agent: write to prod DB |
| **Enforcement** | Runtime limits (code, framework) | Governance policy (human approval gates) |
| **Failure mode** | No limits → infinite loop, cost blowup | No graduation → T0 agent destroys prod |

## Контекст

Production agents в 2026: 46.7% выполняют 1-4 шага, 21.7% — 5-10 шагов (arxiv 2512.04123v1). Bounded autonomy = доминирующий паттерн: agent + clear operational limits + mandatory escalation paths + audit trails.

## Связь

- AS.M.001 (Trust Stack Design): bounded autonomy = runtime layer Trust Stack
- AS.M.004 (Graduated Governance): governance = политика, bounded = техническая реализация
- AS.FM.020 (Production Deployment Failure): bounded autonomy = mitigation

## Примеры

**Bounded Autonomy (технические лимиты):**
- Retry failed task 3 times → fail 4-й → escalate to human
- Cost ceiling $50/run → exceed → terminate + alert
- Timeout 5 min → no response → kill process
- Max steps 10 → step 11 → stop + log

**Graduated Governance (политика доверия):**
- T0 agent: read-only access, no external API calls
- T1 agent: read + write sandbox, external API with approval
- T4 agent: full prod access, autonomous decisions <$1K
```

**Reasoning для Экстрактора:** Это НОВОЕ различение (не в Pack Index). Bounded autonomy покрывает runtime constraints (технические), Graduated Governance = design-time policy (AS.M.004 существует). Два ортогональных измерения: политика × техника. Критично для WP-179 (GEPA Phase 2: deployment constraints).

---

## Candidate #2: ECO.D.007 Enrichment — Pedagogical Efficacy Framework

**Pack:** PACK-ecosystem  
**Тип:** Enrichment (ECO.D.007 существует)  
**Источник:** Nature s41599-025-05330-9, OpenFieldX 2026, WEF 2024/04  

### Что добавить к ECO.D.007

ECO.D.007 уже есть: "Pedagogical Market Fit (PMF-edu) ≠ Product-Market Fit (PMF)". Обогатить:

**Новая секция: "Операционализация Pedagogical Efficacy (2026)"**

```markdown
## Frameworks для измерения Pedagogical Efficacy

### 5Es Framework (Nature 2025)
- **Efficacy:** learning outcomes в controlled conditions (RCT, experimental studies)
- **Effectiveness:** teacher experience в real classrooms (everyday use, not lab)
- **Ethics:** data privacy, AI transparency, bias mitigation
- **Equity:** accessibility, inclusion (SES, disability, language)
- **Environment:** sustainability, digital waste

### MEII (Multiple EdTech Impact Index)
- 15 indicators impact
- 3 evidence weights: high (RCT), medium (quasi-experimental), low (observational)
- 5 domains (5Es)

### Efficacy vs Effectiveness (различение)
| Аспект | Efficacy | Effectiveness |
|--------|----------|---------------|
| Условия | Controlled (lab, RCT) | Real-world (classrooms) |
| Метрика | Learning outcomes (test scores, retention) | Teacher satisfaction, adoption rate |
| Вопрос | Does it work in ideal conditions? | Does it work in practice? |

### Тренд 2026: Efficacy Reckoning
- Инвесторы требуют proof of efficacy (не engagement metrics)
- EdTech без доказательств → fail budget scrutiny
- 65+ evaluation frameworks (хаос, нет стандарта)
- Opportunity для IWE: мы МОЖЕМ измерить (ЦД v3 + шедевры MIM.WP.002)

## Применение к IWE

IWE = Pedagogical Efficacy > PMF:
- **Efficacy:** шедевры (MIM.WP.002) = measurable learning outcomes
- ЦД v3.0 (WP-158) = характеристики созидателя → track progress
- FPF методология = evidence-based (не курс "trust me")
- Конкуренты: PMF (engagement, reach), IWE: efficacy (outcomes)

## Источники
- Nature Humanities: "Developing evidence indicators for evaluating K12 EdTech" (2025)
- OpenFieldX: "2026 EdTech Trends: Navigating the Efficacy Reckoning" (2026)
- WEF: "Why measuring impact effectively is so important in EdTech" (2024/04)
```

**Reasoning для Экстрактора:** ECO.D.007 существует (PMF-edu ≠ PMF), но без операционализации. Enrichment: добавить frameworks (5Es, MEII), различение efficacy vs effectiveness, тренд 2026 (efficacy reckoning), применение к IWE (шедевры + ЦД = measurable outcomes). Критично для WP-145 (investor deck narrative).

---

## Candidate #3: ECO.M.XXX — Pedagogical Efficacy Measurement Method

**Pack:** PACK-ecosystem  
**Тип:** Метод (новый)  
**ID:** ECO.M.XXX (следующий свободный номер после ECO.M.019)  
**Источник:** Nature s41599-025-05330-9, WEF 2024/04  

### Черновик

```markdown
# ECO.M.XXX — Pedagogical Efficacy Measurement

## Метод

**Цель:** Измерение педагогической эффективности (pedagogical efficacy) образовательных продуктов и программ.

## Шаги

### 1. Определение Evidence Type
- High evidence: RCT (randomized controlled trial), experimental studies
- Medium evidence: quasi-experimental (control group, no randomization)
- Low evidence: observational, correlational, self-reported

### 2. Выбор Indicators (5Es Framework)

**Efficacy (learning outcomes):**
- Pre-post test scores (knowledge gain)
- Skill demonstration (performance tasks)
- Retention rate (long-term memory)
- Transfer (apply to new contexts)

**Effectiveness (real-world use):**
- Teacher satisfaction (survey, interviews)
- Adoption rate (% active users)
- Fidelity of implementation (as designed?)

**Ethics:**
- Data privacy compliance (GDPR, FERPA)
- AI transparency (explainability)
- Bias audit (demographic parity)

**Equity:**
- Accessibility (WCAG, screen reader compatible)
- Performance gaps (SES, disability, language)
- Inclusion metrics (diverse learner success)

**Environment:**
- Carbon footprint (cloud compute)
- Digital waste (obsolete content)

### 3. Data Collection
- Quantitative: test scores, usage logs, surveys (Likert scale)
- Qualitative: interviews, observations, work products (шедевры)
- Mixed methods: triangulation

### 4. Analysis & Reporting
- Effect size (Cohen's d, Hedges' g) для efficacy
- Statistical significance (p-value) + practical significance
- Contextualized interpretation (не только цифры)

### 5. Decision Framework
- Green: high evidence + positive outcomes → scale
- Yellow: medium evidence or mixed outcomes → iterate
- Red: low evidence or negative outcomes → discontinue

## Применение к IWE

**IWE Efficacy Measurement:**

1. **Pre-Assessment:** диагностика созидателя (ЦД v3.0, WP-158)
   - Baseline characteristics (agency, deliberate practice, etc.)
   - Starting point по МПМ (модель профиля мышления)

2. **Intervention:** программа развития (MIM.PRG.001-003)
   - Deliberate practice (MIM.M.001)
   - Scaffolding (MIM.M.006)
   - Retrieval practice (MIM.M.011)

3. **Post-Assessment:** шедевры (MIM.WP.002) + ЦД update
   - Measurable outcome: шедевр = конкретный артефакт
   - ЦД v3.0 delta: изменение характеристик (до/после)

4. **Long-term Follow-up:** career success, system creation
   - Рабочие продукты (WP-Registry)
   - Проекты (целевые системы)

**Evidence Level:** Medium-to-High
- Quasi-experimental (cohort comparison: control vs IWE users)
- Work products (шедевры) = objective artifacts
- ЦД v3.0 = quantified characteristics

**Indicators:**
- Efficacy: шедевр quality (rubric MIM.WP.005), ЦД delta
- Effectiveness: user satisfaction, retention rate (>6 месяцев engagement)
- Ethics: privacy (ЦД = user-owned), transparency (open FPF)
- Equity: accessibility (multiple formats: текст, видео, практикумы)

## Failure Modes

- **FM1:** Vanity metrics (engagement ≠ learning)
- **FM2:** Self-reported bias (students overestimate learning)
- **FM3:** Hawthorne effect (improvement = attention, not intervention)
- **FM4:** Confounding variables (external learning sources)

## Связь

- ECO.D.007 (PMF-edu ≠ PMF): efficacy = отличие от PMF
- MIM.WP.002 (Шедевр): measurable outcome
- MIM.WP.005 (Rubric): assessment tool
- DP.ARCH.003 (ЦД архитектура): data source для measurement

## Источники
- Nature Humanities: s41599-025-05330-9 (MEII framework)
- WEF 2024: "Why measuring impact effectively is so important in EdTech"
- Stanford GSE: "What makes digital learning products effective" (2024)
```

**Reasoning для Экстрактора:** Новый метод (не в Pack Index). ECO.D.007 = различение (что такое pedagogical efficacy), ECO.M.XXX = КАК измерять. Прямое применение к IWE: шедевры + ЦД v3.0 = measurable efficacy. Критично для WP-145 (investor deck: доказать efficacy, не только PMF).

---

## Candidate #4: AS.M.001 Enrichment — Bounded Autonomy Layer

**Pack:** PACK-autonomous-agents  
**Тип:** Enrichment (AS.M.001 Trust Stack Design существует)  
**Источник:** arxiv 2512.04123v1, MongoDB blog 2026  

### Что добавить к AS.M.001

AS.M.001 = Trust Stack Design (4 layers: Verification, Validation, Monitoring, Governance). Обогатить новым runtime layer:

**Новая секция: "Layer 5: Bounded Autonomy (Runtime Constraints)"**

```markdown
## Layer 5: Bounded Autonomy (Runtime Constraints)

**Суть:** Технические лимиты, enforced в runtime (не политика, а код).

### Компоненты Bounded Autonomy

1. **Step Limits**
   - Max iterations per task (e.g., 10 steps → terminate)
   - Loop detection (same state 3 times → break)
   - Production data: 46.7% agents = 1-4 steps, 21.7% = 5-10 steps

2. **Retry Policies**
   - Max retries per failed operation (e.g., 3 retries → escalate)
   - Exponential backoff (1s, 2s, 4s, 8s → stop)
   - Circuit breaker (5 failures → disable service)

3. **Resource Bounds**
   - Cost ceiling (e.g., $50/run → exceed → terminate + alert)
   - Time limit (e.g., 5 min timeout → kill process)
   - Memory limit (e.g., 2GB → OOM → crash gracefully)

4. **Escalation Paths**
   - Mandatory human-in-the-loop для high-stakes decisions (>$1K, production write)
   - Approval queue (agent proposes → human approves → execute)
   - Audit trail (log every decision, reason, outcome)

### Implementation Patterns

**Event-Driven Step-Based Execution:**
```python
class BoundedAgent:
    def __init__(self, max_steps=10, cost_ceiling=50, timeout=300):
        self.max_steps = max_steps
        self.cost_ceiling = cost_ceiling
        self.timeout = timeout
        self.step_count = 0
        self.cost_spent = 0
    
    def execute(self, task):
        start_time = time.time()
        while self.step_count < self.max_steps:
            if time.time() - start_time > self.timeout:
                return self.escalate("Timeout exceeded")
            if self.cost_spent > self.cost_ceiling:
                return self.escalate("Cost ceiling exceeded")
            
            result = self.step(task)
            self.step_count += 1
            
            if result.is_terminal():
                return result
        
        return self.escalate("Max steps exceeded")
    
    def escalate(self, reason):
        # Log + alert human + return partial result
        pass
```

**Sandbox Environments:**
- Permitted access rights (read-only, sandboxed writes)
- Pre-approved premises (allowed API endpoints, DBs)
- Network isolation (no external calls without approval)

### Связь с другими layers

- Layer 1 (Verification): bounded autonomy = constraint для verification (verify within bounds)
- Layer 2 (Validation): политика → bounded autonomy реализует
- Layer 3 (Monitoring): мониторим нарушения bounds (alerts)
- Layer 4 (Governance): Graduated Governance (AS.M.004) = политика, Bounded Autonomy = техника

### Пример: Case $47K API Loop

**Failure (без bounded autonomy):**
- 2 agents recursive clarification loop
- 11 days undetected
- $47K API bill

**Mitigation (с bounded autonomy):**
- Step limit: 100 steps → terminate (loop detected day 1)
- Cost ceiling: $100/day → alert (day 1, cost $100 → escalate human)
- Loop detection: same question 3 times → break loop

## Источники
- arxiv 2512.04123v1: "Measuring Agents in Production" (Dec 2025)
- MongoDB Blog: "The Case for Bounded Autonomy" (2026)
- arxiv 2601.08815: "Agent Contracts" (Jan 2026)
```

**Reasoning для Экстрактора:** AS.M.001 (Trust Stack) существует, но без runtime constraints layer. Bounded Autonomy = Layer 5 (или расширение Layer 3 Monitoring). Критично для WP-179 (GEPA Phase 2: deployment constraints = bounded autonomy implementation). Case $47K loop = конкретный пример mitigation.

