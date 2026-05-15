# Specvera

> Spec-driven system for building and continuously verifying software features.

---

## 🧠 What is Specvera?

Specvera is a **declarative runtime for defining, implementing, and verifying software features**.

It allows you to describe what your system should do — and uses this specification to:

- guide implementation (human or AI agents)
- define expected behavior
- continuously verify real runtime behavior

---

Instead of separating design, development, and testing, Specvera unifies them:

## ⚡ Core Idea

PLAN (human or AI)

↓

Declarative Spec (expected behavior)

↓

ACT Engine (deterministic)

↓

Continuous Reconciliation

↓

Actual vs Expected


---

## 📦 Example: AI Summary Feature (Spec as Source of Truth)

Imagine your system provides this feature:

> “Users can generate concise summaries from long text inputs.”

This spec is not only used for verification —  
it also provides enough structure for an AI agent to **implement the feature**.

### 🧾 1. Define the feature

```yaml
id: summary_feature
name: AI Text Summary
version: 1.0.0

goal:
  description: Generate concise and relevant summaries from user-provided text

behavior:
  input:
    text: string
  output:
    summary: string
  constraints:
    - summary must not be empty
    - summary should be shorter than input
    - summary should capture key information

context:
  base_url: http://localhost:3000

implementation_hint:
  endpoint: /api/summarize
  method: POST
  expected_stack:
    - llm
    - text-processing

heartbeat:
  interval_seconds: 120

checks:
  - id: summary_api_status
    type: http
    request:
      method: POST
      url: /api/summarize
      body:
        text: "Specvera enables continuous verification of software systems."
    expect:
      status: 200

  - id: summary_not_empty
    type: content
    source: previous_response.body.summary
    expect:
      not_empty: true

  - id: summary_shorter_than_input
    type: content
    source: previous_response.body.summary
    compare_to: request.body.text
    expect:
      shorter_than: true

failure:
  severity: medium

observability:
  store_history: true
```

---

## 🔁 How it works

Specvera continuously compares:

- expected state (spec)
- actual state (runtime)

→ detects regressions immediately

---

## 🚀 Use Cases

- continuous feature verification
- alternative to synthetic monitoring
- runtime validation in production-like environments
- regression detection
- validating AI system outputs

---

## 🧱 Architecture

plan/   → spec generation (optional AI)

act/    → execution engine

specs/  → feature definitions

core/   → schema + validation

---

## 🚀 Getting Started

Run with Docker

```
docker-compose up --build
```
