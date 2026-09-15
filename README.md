# LLM Prompt Injection Red-Team Harness

An automated red-team framework for evaluating the security of LLM applications against prompt-injection attacks.

The project generates adversarial inputs against a controlled target LLM application, evaluates whether attacks successfully bypass the application's defenses, and tracks attack success rates across successive guardrail iterations.

## Objective

The goal is to answer:

> How resilient is an LLM application to prompt injection, and do our defenses actually make it better?

Rather than evaluating a single prompt manually, this project treats prompt-injection defense as an iterative security evaluation problem:

```text
Generate Attacks
       ↓
Attack Target LLM
       ↓
Evaluate Response
       ↓
Measure Attack Success Rate
       ↓
Identify Failure Modes
       ↓
Improve Guardrails
       ↓
Re-run Attacks
       ↓
Compare Results
```

## Attack Categories

The red-team harness will evaluate multiple classes of adversarial behavior:

* Instruction override
* Role manipulation
* Context manipulation
* Encoding and obfuscation
* Multi-turn attacks
* Indirect prompt injection
* RAG/document-based injection
* Adversarial variations and mutations

## Evaluation

Each attack is recorded with:

* Attack category
* Attack payload
* Target model
* Target configuration
* Model response
* Attack result
* Judge decision
* Confidence
* Failure category
* Guardrail version
* Experiment iteration

The primary metric is:

```text
Attack Success Rate =
Successful Attacks / Total Attacks
```

## Iterative Defense Evaluation

The project measures whether security improvements actually reduce attack success.

Example:

```text
                 Attack Success Rate

Iteration 0          42%
Iteration 1          27%
Iteration 2          14%
Iteration 3           8%
```

This allows guardrail changes to be evaluated experimentally rather than based on individual examples.

## Architecture

```text
                    ┌──────────────────┐
                    │   Attack Library │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │  Red-Team Engine │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │   Target LLM App │
                    │                  │
                    │ Prompt           │
                    │ Guardrails       │
                    │ RAG              │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Response Judge   │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Metrics & Logs   │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │    Dashboard     │
                    └──────────────────┘
```

## Technology Stack

* Python
* FastAPI
* PostgreSQL
* Docker
* LLM API
* Automated evaluation
* Experiment tracking

## Project Status

### Phase 1 — Foundation

* [ ] Repository setup
* [ ] Vulnerable target LLM application
* [ ] Attack schema
* [ ] Basic attack runner

### Phase 2 — Red Team Engine

* [ ] Attack templates
* [ ] Attack mutations
* [ ] Multi-category test suites
* [ ] Automated execution

### Phase 3 — Evaluation

* [ ] Attack-success classifier
* [ ] LLM judge
* [ ] Confidence scoring
* [ ] Failure categorization

### Phase 4 — Defense Iterations

* [ ] Baseline evaluation
* [ ] Guardrail iteration 1
* [ ] Guardrail iteration 2
* [ ] Regression testing

### Phase 5 — Analysis

* [ ] Success-rate metrics
* [ ] Attack-category breakdown
* [ ] Iteration comparison
* [ ] Success-rate curve

### Phase 6 — Dashboard

* [ ] Experiment overview
* [ ] Attack results
* [ ] Failure analysis
* [ ] Guardrail comparison

## Security Note

This project is designed for controlled security research and evaluation of LLM applications that you own or are authorized to test.

The target application is intentionally vulnerable so that attacks can be studied safely and defenses can be evaluated systematically.

## Final Goal

Build a repeatable evaluation system that can answer:

> **"Did our LLM security defenses actually get better?"**
