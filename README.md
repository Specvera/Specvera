# Specvera

> Continuous feature verification using declarative specs and reconciliation loops.

---

## 🧠 What is Specvera?

Specvera is a **declarative runtime for continuous feature verification**.

Define how your system should behave — and continuously verify that it actually does in real environments.

---

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

## 📦 Example

```yaml
features:
  - id: login_feature
    heartbeat:
      interval_seconds: 60
    checks:
      - type: http
        request:
          method: GET
          url: http://localhost:3000/login
        expect:
          status: 200
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
