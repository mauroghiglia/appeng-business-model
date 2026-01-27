# Running Graylog on a VPS: A Pragmatic Architecture Guide

## Purpose of this document

Graylog is often perceived as a heavy, enterprise-only platform.  
In reality, it can be deployed effectively on a **Virtual Private Server (VPS)** when constraints and expectations are clearly understood.

This document describes **when and how Graylog can be run on a VPS**, the architectural trade-offs involved, and the limits beyond which a VPS-based deployment becomes inappropriate.

The focus is on **practical, budget-aware deployments**, not theoretical maximum scale.

---

## Why a VPS-based Graylog deployment makes sense

A VPS-based deployment is appropriate when:

- Budget does not allow managed log platforms
- Full Splunk-class infrastructure is unjustifiable
- Centralized logging is still operationally or legally required
- The environment is small to medium in scale
- Operational responsibility is accepted

Typical use cases include:
- SMEs
- Internal platforms
- Regulated but low-volume environments
- Transitional architectures

A VPS is not a shortcut; it is a **deliberate constraint**.

---

## Minimum architectural components

Even on a VPS, Graylog requires a **complete pipeline**.

At minimum:

- Graylog server
- OpenSearch or Elasticsearch
- MongoDB
- Persistent storage
- Reliable time synchronization

Collapsing components is possible, but responsibilities must remain explicit.

---

## Resource sizing guidelines (practical, not theoretical)

### Baseline VPS profile

A realistic minimum for production use:

- 2 vCPU
- 4–8 GB RAM
- Fast SSD storage
- Stable network connectivity

This supports:
- Structured logs
- Moderate ingestion rates
- Short to medium retention

Anything smaller is a **proof of concept**, not production.

---

## Storage considerations

Storage is the **first real bottleneck** on a VPS.

Key principles:

- Retention must be policy-driven
- Index rotation must be enforced
- Disk usage must be monitored

Recommendations:
- Separate data and system partitions if possible
- Prefer fewer, larger indices over many small ones
- Plan disk growth before ingestion growth

Running out of disk is a catastrophic failure mode.

---

## Ingestion strategy

On a VPS, ingestion must be **intentional**.

Avoid:
- Shipping debug-level logs
- Ingesting unstructured noise
- Forwarding everything “just in case”

Prefer:
- Structured application logs
- Explicit sources
- Predictable volumes

Graylog pipelines should **reduce entropy**, not increase it.

---

## Security and exposure

A VPS is often internet-facing. This changes the threat model.

Minimum requirements:

- Graylog web interface not publicly exposed
- TLS everywhere
- Firewall rules limiting ingestion sources
- Strong authentication
- Regular updates

Logs often contain sensitive operational data.  
A compromised Graylog instance is a serious incident.

---

## Operational risks and mitigations

### Single point of failure

A single VPS is, by definition, not highly available.

Mitigation:
- Accept the risk explicitly
- Use backups
- Document recovery procedures

---

### Performance saturation

As ingestion grows:
- JVM pressure increases
- Indexing latency rises
- Search performance degrades

Mitigation:
- Monitor ingestion rates
- Enforce retention limits
- Scale vertically before horizontally

---

### Hidden cost growth

Graylog itself is free, but:
- Storage grows
- Backup costs grow
- Operational time grows

A VPS keeps costs visible but does not eliminate them.

---

## When a VPS is no longer sufficient

A VPS-based Graylog deployment becomes inappropriate when:

- Ingestion volume grows unpredictably
- Retention requirements exceed available storage
- High availability is mandatory
- Multiple teams depend on the platform
- Logs become legally critical evidence

At that point, the architecture—not the tool—must evolve.

---

## What this approach enables

Despite its limits, Graylog on a VPS enables:

- Centralized, structured logging
- Governance-aware log handling
- Incident reconstruction
- Incremental observability maturity

Most importantly, it enables **learning before scaling**.

---

## Practical takeaway

Running Graylog on a VPS is not about doing things cheaply.  
It is about doing the **right amount of architecture for the problem at hand**.

A VPS enforces discipline:
- In what you log
- How long you keep it
- Why it exists

Used deliberately, it is a powerful starting point.

