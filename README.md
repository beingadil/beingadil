<div align="center">

# Muhammad Adil Shahzad

**Solo developer · Dental laboratory software · Local-first desktop & web apps**

[![Dental Solutions](https://img.shields.io/badge/Dental%20Solutions-v2.28.2-2f6bff?style=for-the-badge)](https://github.com/beingadil/Dental-Clinic-Management)
[![Live Demo](https://img.shields.io/badge/Live%20Demo-running-2ea44f?style=for-the-badge)](https://beingadil.github.io/Dental-Clinic-Management/)
[![MIT](https://img.shields.io/badge/License-MIT-2ea44f.svg)](https://github.com/beingadil/Dental-Clinic-Management/blob/master/LICENSE)

📧 [adilmaher990@gmail.com](mailto:adilmaher990@gmail.com) · 📱 +92 300 8662319 · 🌐 [Pakistan](https://www.google.com/search?q=Pakistan)

</div>

---

## What I build

Software for people who do a technical job, the paperwork for that job, and
the books for the business — usually all three in the same session, on one
machine.

My main project is **[Dental Solutions](https://github.com/beingadil/Dental-Clinic-Management)**,
a clinic and dental-laboratory management system: receive a case from a clinic,
chart exactly which teeth on an FDI odontogram, move it through production
under an SLA, print the job slip the technician works from, and invoice the
clinic. It runs fully offline on a real SQLite database, and it ships as both a
Windows desktop app and a web build.

## Current work

| | |
|---|---|
| **[Dental Solutions](https://github.com/beingadil/Dental-Clinic-Management)** — v2.28.2 · MIT | Dental lab & clinic management: FDI odontogram charting, production workflow, job-slip printing, double-entry ledger, offline-first SQLite, Tauri 2 desktop shell |
| **[Live demo](https://beingadil.github.io/Dental-Clinic-Management/)** | The real web build — first run asks you to create an administrator, then the seeded material catalogue is browsable |
| **[Windows installer](https://github.com/beingadil/Dental-Clinic-Management/releases/latest)** | NSIS build with a SHA-256 checksum and a five-step verified self-updater |

## How I work

I build with **AI coding agents** (Claude through Claude Code / OpenCode) against
a written specification, and I hold the output to machine-checkable gates
rather than to my own say-so.

- **A real spec, not a prompt** — constraints written down first: who the user
  is, what hardware they have, what the vocabulary is, what must never happen.
- **Gates decide** — typecheck, tests, contrast audit and token-solver checks
  determine whether something is done. Several real defects were caught by the
  gates *after* the agent's own summary had already declared them fixed.
- **Bounded loops that can fail** — automated loops measure the live DOM
  (`scrollWidth > clientWidth` overflow) instead of trusting a screenshot, and
  keep going until the measured count reaches zero.
- **Adversarial verification** — findings get re-tested against the running app
  before I write them down. That is how the worst bug in the project surfaced.

The one rule I hold to: **the shipped product makes no model calls where
correctness matters.** Software holding patient records and real money should
not have a model quietly mis-price an invoice. So the running system is
deterministic and auditable, and the AI is in the engineering, not in the data
path.

## Stack

React 19 · TypeScript (strict) · Vite 6 · Tailwind CSS 4 · SQLite (sql.js WASM)
· Tauri 2 / Rust · Vitest · Playwright · GitHub Actions

## Currently interested in

- Local-first software that stays useful with the network unplugged
- Domain modelling that removes a whole class of manual reconciliation
- White-label design systems where the end user picks the accent colour
- Making print output a first-class deliverable rather than an export

---

<div align="center">
<sub>Open to collaborations, bug reports and pull requests on
<a href="https://github.com/beingadil/Dental-Clinic-Management">Dental Solutions</a>.</sub>
</div>
