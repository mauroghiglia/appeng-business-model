# When Not to Use an Observability Tool

## Purpose of this document

Observability tools are often presented as universal solutions: install the platform, ingest data, and insight will follow.

This assumption is false.

Every observability tool embodies **trade-offs and assumptions**. Using the wrong tool—or using the right tool in the wrong context—can increase cost, complexity, and risk without improving understanding.

This document describes **when not to use** certain classes of observability tools, based on practical experience with Grafana/Loki, Graylog, and Dynatrace.

---

## Do not use observability tools to compensate for missing ownership

### The anti-pattern

- No clear service ownership
- No on-call responsibility
- Incidents resolved by “whoever is available”

### Why tools fail here

Observability tools expose problems; they do not resolve accountability.

Without ownership:
- Alerts are ignored
- Dashboards are unused
- Logs accumulate without analysis

### Better alternative

Establish ownership and escalation paths **before** investing in tooling.

---

## When not to use Grafana / Loki

### Do not use when:

- Logs are required as **evidence**
- Strict access control is mandatory
- Long-term forensic retention is needed
- Structured, schema-driven logging is absent

### Why

Grafana/Loki optimizes for:
- Cost efficiency
- Searchability
- Fast exploration

It does **not** optimize for:
- Strong governance
- Audit trails
- Legal defensibility

Using Loki as a compliance or forensic system is a category error.

---

## When not to use Graylog

### Do not use when:

- Teams are unwilling to design logs deliberately
- Logging is treated as a side effect of debugging
- There is no agreement on schemas or context
- Minimal operational effort is expected

### Why

Graylog is powerful but opinionated:
- It rewards structured logging
- It assumes intentional pipelines
- It exposes weaknesses in log design

Without discipline, Graylog becomes an expensive log dump.

---

## When not to use Dynatrace

### Do not use when:

- Budgets are tight or unstable
- Vendor lock-in is unacceptable
- Custom or legacy environments dominate
- The organization cannot absorb opinionated tooling

### Why

Dynatrace excels when:
- Its assumptions align with the environment
- Automation is preferred over flexibility
- Cost is justified by impact

It becomes a liability when imposed on systems it cannot model well.

---

## When not to centralize everything

### The anti-pattern

- All logs, metrics, and traces sent everywhere
- No data tiering or retention strategy
- Central platforms overloaded with low-value data

### Why this fails

- Costs grow faster than insight
- Signal is drowned in noise
- Governance becomes unmanageable

### Better alternative

Centralize **what matters**, not **everything that exists**.

---

## When not to add more telemetry

### Warning sign

- “We need more data” is the default reaction to incidents

### Why this fails

More data without context increases:
- Storage cost
- Cognitive load
- Analysis time

Better observability often comes from **better context**, not higher volume.

---

## The cost of the wrong tool

Using an inappropriate observability tool results in:

- False confidence
- Slower incident response
- Increased operational cost
- Audit and compliance exposure

These costs are often hidden until failure occurs.

---

## Practical takeaway

Observability tools do not create understanding.  
They amplify the quality of the system and organization they observe.

Choosing **not** to use a tool can be the most responsible decision.

A good observability strategy includes:
- Knowing what to deploy
- Knowing what to delay
- Knowing what to avoid

Restraint is a form of expertise.

---

