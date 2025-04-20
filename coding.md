# **Coding Prompt Template – Variable‑Driven Edition**

> **How to use:**
> 1. Fill in the **VARIABLES** block at the top (YAML style or simple `KEY=VALUE`).  
> 2. Copy the **Prompt Skeleton**. All placeholders like `${GOAL}` will auto‑expand.  
> 3. Send to ChatGPT and iterate.
>
> *Keep unused variables blank or delete them.*

---

## 1. VARIABLES (edit here)
```yaml
# Mandatory
GOAL: "Generate a RESTful API client"
LANGUAGE: "Python"
ARTIFACT: "module with unit tests"
RUNTIME: "CPython 3.12"

# Context (pick any)
EXISTING_CODE: |
  # Paste relevant snippets or repo links
ENVIRONMENT: "Ubuntu 24.04, Docker, VS Code"
ERROR_LOGS: |
  # Stack traces or compiler errors

# Constraints & Standards
STYLE_GUIDE: "PEP‑8 + Black formatting"
ARCH_PRINCIPLES: "SOLID, KISS, YAGNI"
ALLOWED_LIBS: ["requests", "pydantic"]
FORBIDDEN_LIBS: ["urllib3"]
LICENSE: "MIT"
SECURITY_REQS: "No hard‑coded secrets, OWASP Top‑10 safe"
PERFORMANCE_TARGET: "<50 ms avg latency"
MEMORY_BUDGET_MB: 128
SCALABILITY_REQ: "Handle 10k concurrent users"
TEST_COVERAGE: 95  # percent
DOC_STANDARD: "Google‑style docstrings"
LOGGING_FORMAT: "JSON structured"
I18N: "English only"

# Deliverable
OUTPUT_FORMAT: "Return *only* a markdown code block"
TONE: "Concise but technical"

# Optional extras
EXAMPLE_DATA: |
  # Sample payloads or inputs
OPTIMISATION_METRIC: "CPU cycles"
DEPLOY_TARGET: "AWS Lambda"
NEED_EXPLANATION: true  # true = include short rationale after code block
ASK_CLARIFY_IF_MISSING: true
```

---

## 2. PROMPT SKELETON (paste below variables)
```text
# === System Role ===
You are ChatGPT, an elite ${LANGUAGE} architect.
${ASK_CLARIFY_IF_MISSING?{If any critical info is missing, ask clarifying questions before answering.}:}

# === Task ===
**Goal**: ${GOAL}

# === Context ===
${EXISTING_CODE?{Existing code:
```${LANGUAGE}
${EXISTING_CODE}
```}:}
Environment: ${ENVIRONMENT}
${ERROR_LOGS?{Error logs:
```
${ERROR_LOGS}
```}:}

# === Requirements ===
- Target runtime: ${RUNTIME}
- Follow style: ${STYLE_GUIDE}
- Architectural principles: ${ARCH_PRINCIPLES}
- Allowed libs: ${ALLOWED_LIBS}
- Forbidden libs: ${FORBIDDEN_LIBS}
- License: ${LICENSE}
- Security: ${SECURITY_REQS}
- Performance < ${PERFORMANCE_TARGET}
- Memory ≤ ${MEMORY_BUDGET_MB} MB
- Scalability: ${SCALABILITY_REQ}
- Test coverage ≥ ${TEST_COVERAGE}% using your choice of framework
- Documentation: ${DOC_STANDARD}
- Logging: ${LOGGING_FORMAT}
- Internationalisation: ${I18N}

# === Deliverable ===
Produce ${ARTIFACT}.
Return ${OUTPUT_FORMAT}.
${NEED_EXPLANATION?{After the code, include a brief explanation (<200 words).}:}
```

---

## 3. ONE‑LINER QUICK START
```text
Generate a robust ${LANGUAGE} ${ARTIFACT} to ${GOAL} under ${RUNTIME} using ${STYLE_GUIDE}, ${ARCH_PRINCIPLES}, coverage ${TEST_COVERAGE}%.
```

---

## 4. READY‑MADE EXAMPLE
```yaml
GOAL: "Build a CLI that batch‑renames images using EXIF creation date"
LANGUAGE: "Python"
ARTIFACT: "stand‑alone script + pytest suite"
RUNTIME: "CPython 3.12"
ENVIRONMENT: "macOS 14, Homebrew"
STYLE_GUIDE: "PEP‑8"
ALLOWED_LIBS: ["Pillow", "typer"]
FORBIDDEN_LIBS: []
TEST_COVERAGE: 90
OUTPUT_FORMAT: "Return only the code block"
NEED_EXPLANATION: true
```

Paste the **Prompt Skeleton** below this block → ChatGPT will output the script and tests.

---

## 5. MODEL‑SPECIFIC OPTIMISERS
| Model | Tip |
|-------|-----|
| **GPT‑4o (128k)** | Embed entire repo in `EXISTING_CODE` – it can digest huge contexts. |
| **GPT‑4 Turbo 32k** | Chunk code and set `ASK_CLARIFY_IF_MISSING` so the model requests next chunks. |
| **GPT‑3.5 Turbo** | Trim variables; keep prompt ≤ 4k tokens. Paraphrase requirements concisely. |

---

## 6. REFACTORING PROMPT TEMPLATE – Variable‑Driven Edition

A specialised template for safe, principled code transformations.

### VARIABLES (edit here)
```yaml
GOAL: "Refactor legacy service layer to introduce dependency injection"
LANGUAGE: "Java 21"
EXISTING_CODE: |
  // Paste the service class and related files
ARCHITECTURE_GOALS: "Reduce coupling, improve unit‑test isolation, apply SOLID"
RUNTIME: "OpenJDK 21 on Ubuntu 24.04"
STYLE_GUIDE: "Google Java Style"
TEST_SUITE_PRESENT: true        # set false if no tests exist yet
PERFORMANCE_BUDGET: "≤ 5 % regression in p95 latency"
BREAKING_API_ALLOWED: false     # true = can change public signatures
STRICT_BEHAVIOUR_PRESERVATION: true  # if true, functional output must remain identical
METRICS_TO_IMPROVE: ["cyclomatic complexity", "file length"]
OUTPUT_FORMAT: "Return a unified diff followed by the full refactored files"
NEED_EXPLANATION: true          # include reasoning after code
ASK_CLARIFY_IF_MISSING: true
```

---

### PROMPT SKELETON
```text
# === System Role ===
You are ChatGPT, a veteran ${LANGUAGE} refactoring expert.
${ASK_CLARIFY_IF_MISSING?{Before answering, ask clarifying questions if critical information is missing.}:}

# === Task ===
**Goal**: ${GOAL}

# === Context ===
${EXISTING_CODE?{Here is the existing code:
```${LANGUAGE}
${EXISTING_CODE}
```}:}
Runtime: ${RUNTIME}
Tests present: ${TEST_SUITE_PRESENT}

# === Refactoring Objectives ===
- Architectural goals: ${ARCHITECTURE_GOALS}
- Style guide: ${STYLE_GUIDE}
- Behaviour preservation: ${STRICT_BEHAVIOUR_PRESERVATION}
- Breaking API allowed: ${BREAKING_API_ALLOWED}
- Performance budget: ${PERFORMANCE_BUDGET}
- Metrics to improve: ${METRICS_TO_IMPROVE}

# === Deliverable ===
Return ${OUTPUT_FORMAT}.
${NEED_EXPLANATION?{After the code, include a concise explanation (<250 words) covering the key changes and why they meet the objectives.}:}
```

---

### ONE‑LINER QUICK START
```text
Refactor the following ${LANGUAGE} code to ${ARCHITECTURE_GOALS} without breaking the public API.
```

---

### READY‑MADE EXAMPLE
```yaml
GOAL: "Introduce async/await and remove callback hell"
LANGUAGE: "TypeScript 5.4"
EXISTING_CODE: |
  export function fetchData(url: string, cb: (err: Error|null, data?: any)=>void) {
      http.get(url, res => { ... });
  }
ARCHITECTURE_GOALS: "Use Promises, improve readability"
RUNTIME: "Node 20"
STYLE_GUIDE: "Airbnb TypeScript"
TEST_SUITE_PRESENT: false
BREAKING_API_ALLOWED: true
OUTPUT_FORMAT: "Return only the refactored code block"
NEED_EXPLANATION: true
```

Paste the **Prompt Skeleton** below this block → ChatGPT will output the modernised async version plus rationale.

---

### MODEL‑SPECIFIC TIPS
Use the same guidance as the main template above – larger contexts for GPT‑4o, chunked feeds for 32k models, and tighter prompts for 3.5 Turbo.

---

## 7. ARCHITECTURE & SYSTEM DESIGN TEMPLATE

Use this when you need high‑level design docs, diagrams, or component breakdowns before coding.

### VARIABLES (edit here)
```yaml
GOAL: "Design a scalable URL shortening service like bit.ly"
DOMAIN: "Web service"
LANGUAGE_PREFERENCE: "Polyglot (Java/Kotlin microservices)"
CONTEXT: |
  # Current state, legacy systems, or greenfield notes
STAKEHOLDERS: ["product", "ops", "security", "mobile teams"]
USERS_PER_DAY: 10_000_000
PEAK_RPS: 25_000
DATA_VOLUME: "~500 GB/month new data"
LATENCY_SLA_MS: 100
AVAILABILITY_TARGET: "99.99%"

# Constraints
BUDGET: "<$2k/month infra"
DEPLOY_TARGET: "AWS us‑west‑2"
COMPLIANCE: ["GDPR", "SOC2"]
TECH_STACK_MUST: ["PostgreSQL", "Redis"]
TECH_STACK_BANNED: ["DynamoDB"]
PATTERNS: ["CQRS", "Event sourcing"]
ARCH_STYLES: ["Microservices", "Hexagonal"]
DIAGRAM_TYPE: "C4 level‑2+3"
NEED_SEQUENCE_DIAGRAM: true
NEED_API_SPEC: true
RISK_AREAS: ["Hot key traffic", "URL abuse"]
COMPARABLE_SYSTEMS: ["Bitly", "TinyURL"]
ASK_CLARIFY_IF_MISSING: true
OUTPUT_FORMAT: "Markdown with embedded PlantUML for diagrams"
NEED_EXPLANATION: true
```

---

### PROMPT SKELETON
```text
# === System Role ===
You are ChatGPT, a senior software architect.
${ASK_CLARIFY_IF_MISSING?{Ask clarifying questions if any critical design detail is missing.}:}

# === Design Brief ===
**Goal**: ${GOAL}
Domain: ${DOMAIN}
Comparable systems: ${COMPARABLE_SYSTEMS}

# === Context ===
${CONTEXT}
Stakeholders: ${STAKEHOLDERS}

# === Non‑Functional Requirements ===
- Peak RPS: ${PEAK_RPS}
- Daily users: ${USERS_PER_DAY}
- Data volume: ${DATA_VOLUME}
- Latency SLA: ${LATENCY_SLA_MS} ms
- Availability: ${AVAILABILITY_TARGET}
- Budget: ${BUDGET}
- Compliance: ${COMPLIANCE}

# === Constraints & Preferences ===
- Deploy target: ${DEPLOY_TARGET}
- Must‑use tech: ${TECH_STACK_MUST}
- Forbidden tech: ${TECH_STACK_BANNED}
- Preferred patterns: ${PATTERNS}
- Architectural style: ${ARCH_STYLES}

# === Deliverables ===
1. **High‑level component diagram** (${DIAGRAM_TYPE})
2. ${NEED_SEQUENCE_DIAGRAM?{Sequence diagram of critical path}:}
3. ${NEED_API_SPEC?{REST/GRPC API spec}:}
4. Risk analysis & mitigations for: ${RISK_AREAS}

Return as ${OUTPUT_FORMAT}. ${NEED_EXPLANATION?{Include rationale (≤300 words) after diagrams.}:}
```

---

### ONE‑LINER QUICK START
```text
Design a ${DOMAIN} to ${GOAL} satisfying ${PEAK_RPS} RPS and ${AVAILABILITY_TARGET} availability on ${DEPLOY_TARGET}.
```

---

### READY‑MADE EXAMPLE
```yaml
GOAL: "Architect a real‑time chat application supporting 1M concurrent users"
DOMAIN: "Realtime messaging"
TECH_STACK_MUST: ["WebSocket", "Kafka", "Kubernetes"]
PEAK_RPS: 50_000
LATENCY_SLA_MS: 50
AVAILABILITY_TARGET: "99.999%"
OUTPUT_FORMAT: "Markdown + PlantUML"
NEED_SEQUENCE_DIAGRAM: true
```

Paste the skeleton under the variable block and ChatGPT will output diagrams and rationale.

---

## 8. CODE REVIEW TEMPLATE

Solicit a structured, high‑signal review for any codebase.

### VARIABLES (edit here)
```yaml
GOAL: "Get an expert review of my payment‑processing module"
LANGUAGE: "Go 1.22"
EXISTING_CODE: |
  // Paste file(s) or Git diff
RUNTIME: "Linux, Alpine 3.19"
STYLE_GUIDE: "Uber Go style"
REVIEW_FOCUS: ["concurrency", "security", "idiomatic style"]
CRITICALITY: "Production service — zero downtime"
DIFF_AVAILABLE: true           # true = code shown is a diff; false = full file
TEST_RESULTS: |
  # Output of `go test ./...` if any failures
ASK_CLARIFY_IF_MISSING: true
OUTPUT_FORMAT: "Markdown with line‑numbered suggestions + summary table"
```

---

### PROMPT SKELETON
```text
# === System Role ===
You are ChatGPT, a principal ${LANGUAGE} code reviewer.
${ASK_CLARIFY_IF_MISSING?{Ask clarifying questions if key context is missing before reviewing.}:}

# === Review Brief ===
Goal: ${GOAL}
Criticality: ${CRITICALITY}

# === Code Under Review ===
${EXISTING_CODE?{```${LANGUAGE}
${EXISTING_CODE}
```}:}
Runtime/Env: ${RUNTIME}
DIFF provided: ${DIFF_AVAILABLE}

# === Review Focus Areas ===
- ${REVIEW_FOCUS}
- Style guide adherence: ${STYLE_GUIDE}
- Test results provided: ${TEST_RESULTS?{see failures above}:"(none)"}

# === Deliverable ===
Return ${OUTPUT_FORMAT} including:
1. **High‑priority issues** (bugs, security, data races)
2. **Performance bottlenecks**
3. **Style & readability** suggestions
4. **Maintainability** & architectural notes
5. **Summary table** with severity, location, recommendation
```

---

### ONE‑LINER QUICK START
```text
Review the following ${LANGUAGE} code focusing on ${REVIEW_FOCUS}, production critical.
```

---

### READY‑MADE EXAMPLE
```yaml
GOAL: "Identify race conditions and propose fixes"
LANGUAGE: "Rust 1.78"
EXISTING_CODE: |
  // truncated
REVIEW_FOCUS: ["thread safety"]
STYLE_GUIDE: "Rust 2024 edition idioms"
OUTPUT_FORMAT: "Markdown suggestions"
```

Paste the skeleton after the variable block to get a structured review with severity tags.

---

## 9. CHANGELOG
| Date | Notes |
|------|-------|
| 2025‑04‑19 | Added code‑review template v1. |
| 2025‑04‑19 | Added architecture & design template v1. |
| 2025‑04‑19 | Added refactoring template v1. |
| 2025‑04‑19 | Robust variable‑driven template v2 (code generation & others). |

