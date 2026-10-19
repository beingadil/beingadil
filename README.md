<div align="center">
  <img src="https://raw.githubusercontent.com/beingadil/Dental-Clinic-Management/master/public/icon.svg" width="96" height="96" alt="Dental Solutions logo" />
  <h1>Muhammad Adil Shahzad</h1>
  <p><strong>Solo developer &middot; Local-first desktop &amp; web software</strong></p>
  <p>Dental laboratory systems &middot; Offline SQLite &middot; Offline-first ERP</p>
</div>

<div align="center">

[![Email](https://img.shields.io/badge/Email-adilmaher990@gmail.com-EA4335?logo=gmail&logoColor=white&style=flat-square)](mailto:adilmaher990@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-beingadil-181717?logo=github&style=flat-square)](https://github.com/beingadil)
[![Release](https://img.shields.io/github/v/release/beingadil/Dental-Clinic-Management?include_prereleases&style=flat-square)](https://github.com/beingadil/Dental-Clinic-Management/releases/latest)
[![License: MIT](https://img.shields.io/github/license/beingadil/Dental-Clinic-Management?style=flat-square)](https://github.com/beingadil/Dental-Clinic-Management/blob/master/LICENSE)

[![Live Demo](https://img.shields.io/badge/Live_Demo-Online-2F6BFF?logo=googlechrome&style=flat-square)](https://beingadil.github.io/Dental-Clinic-Management/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6?logo=typescript&logoColor=white&style=flat-square)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-19-087EA4?logo=react&logoColor=white&style=flat-square)](https://react.dev/)
[![SQLite](https://img.shields.io/badge/SQLite-sql.js%20WASM-003B57?logo=sqlite&logoColor=white&style=flat-square)](https://sql.js.org/)
[![Tauri](https://img.shields.io/badge/Tauri-2-FFC131?logo=tauri&logoColor=black&style=flat-square)](https://tauri.app/)

</div>

---

I build software for people who do a technical job, the paperwork for that job, and the books for
the business &mdash; usually all three in the same session, on one machine.

Two of my projects are the same idea applied to two industries: **put the whole operation in one
local-first application that keeps working when the network does not.**

## Contents

- [Projects](#projects)
- [How I build](#how-i-build)
- [Tech stack](#tech-stack)
- [What I care about](#what-i-care-about)
- [Contact](#contact)

## Projects

### 🦷 Dental Solutions &mdash; Clinic &amp; Dental Laboratory Management

**v2.28.2 &middot; MIT &middot; [Live demo](https://beingadil.github.io/Dental-Clinic-Management/) &middot;
[Source](https://github.com/beingadil/Dental-Clinic-Management) &middot;
[Windows installer](https://github.com/beingadil/Dental-Clinic-Management/releases/latest)**

```
        +---------------------------------------------+
        |  Receive case  ->  Chart FDI teeth  ->  Print  |
        |      from           + shade on the     job    |
        |     clinic             odontogram      slip   |
        +---------------------------------------------+
                              |
        +---------------------------------------------+
        |  Invoiced automatically  ->  Double-entry      |
        |  at registration, priced from the     ledger  |
        |  clinic's agreed rate            + PKR       |
        +---------------------------------------------+
```

A desktop and web application for dental laboratories and the clinics that send them work. It
runs entirely offline on Windows, stores everything in a single local SQLite database, and covers
the full operational loop: receive a case &rarr; chart exactly which teeth and which shade &rarr;
move it through production under an SLA &rarr; print the job slip the technician works from &rarr;
bill the clinic.

No server, no cloud account, no monthly fee. Patient data never leaves the operator's machine.

| | |
| --- | --- |
| **The core idea** | A case's identity is its **charted teeth and shade**, not a free-text note. The price multiplies by charted units, the job slip prints the teeth, the invoice prints the teeth, and the ledger posts from the invoice &mdash; one derivation, four surfaces, no possibility of drift. |
| **Invoicing is not a separate step** | An invoice is raised the moment a case is registered and stays bound to it for life. Other products make you re-enter the case into a second system and keep the two in sync by hand. Here the case and its money are the same record. |
| **Real dental vocabulary** | FDI 11&ndash;48 numbering, the Vita shade guide, per-tooth restoration type and material. A retainer has no teeth, isn't charted, and never appears as teeth on a slip or an invoice. |
| **Offline by design** | Real SQLite (WebAssembly in the browser, a real file on desktop). Zero runtime network calls after load. |
| **Print is a deliverable** | Job slips and invoices are designed for paper, not exported to it &mdash; monospace, unambiguous, no reliance on colour alone, because a technician reads the slip and not the screen. |
| **Auditable by construction** | A real double-entry ledger with balanced journal entries, opening balances that reconcile, and payment allocation across invoices. Every figure comes from a SQL query, never a hardcoded number. |
| **Scale** | 53k lines across 185 source files &middot; 137 test files &middot; 23 database migrations &middot; 201 commits |

---

### 🏭 Manufacturing ERP &mdash; Metalware &amp; Cutlery Production

**MIT &middot; [Source](https://github.com/beingadil/manufacturing-erp)**

A desktop ERP for metalware and cutlery plants, running entirely offline on Windows: raw material
procurement &rarr; job-work processing &rarr; inventory &rarr; double-entry accounting.

The interesting part is the job-work loop that generic ERPs do not model. Sheet and wire go
**out** to an outside processor for stamping, polishing or plating, come back as semi-finished
pieces with real wastage, and only then become finished goods. Most ERPs model none of that, so
the wastage and the processing charges silently disappear from the books. This one models the
loop explicitly and posts all of it to a real double-entry ledger.

---

## How I build

I develop with **AI coding agents** (Claude via Claude Code / OpenCode) against a written
specification &mdash; and I hold the output to machine-checkable gates rather than to my own
say-so.

| Principle | What it means in practice |
| --- | --- |
| **A real spec, not a prompt** | Constraints are written down *before* the code: who the user is, what hardware they have, what the vocabulary is, what must never happen. The agent reasons against a contract, which is why the output stayed coherent across hundreds of commits. |
| **Gates decide, not the agent** | Typecheck, tests, a contrast auditor and a token-solver check determine whether something is done. Several real defects were caught by those gates *after* the agent's own summary had already declared them fixed. |
| **Loops that can fail** | Automated loops measure the **live DOM** (`scrollWidth > clientWidth` overflow) rather than trusting a screenshot, and keep going until the measured count hits zero. It caught a duplicated currency prefix and four clipped labels that visual review had passed. |
| **Adversarial verification** | Findings are re-tested against the running application before I write them down. That is how the worst bug in Dental Solutions surfaced: `sql.js`'s `export()` silently resets `PRAGMA foreign_keys` to OFF, so every FK and cascade guarantee died after the first snapshot save. |

> **The rule I hold to:** the shipped product makes **no model calls where correctness matters**. Software holding patient records and real money should not have a model quietly mis-price an invoice. So the running system is deterministic and auditable &mdash; and the AI lives in the engineering, not in the data path.

## Tech stack

| Layer | Choice |
| --- | --- |
| UI | React 19, TypeScript 5.8 (strict) |
| Build | Vite 6, Tailwind CSS 4, Electron 43 |
| Desktop shell | Tauri 2 (Rust), Electron 43, NSIS installers with verified auto-updates |
| Persistence | SQLite &mdash; `sql.js` (WebAssembly) in the browser, `better-sqlite3` on desktop |
| Schema | Transactional migrations, foreign keys enforced, `CHECK` constraints, gap-free document sequences |
| Charts | Recharts |
| Icons | Lucide React |
| Export &amp; print | Browser print pipeline, jsPDF, SheetJS (`xlsx`), CSV export |
| Auth | PBKDF2-SHA256, WebCrypto session tokens, role-based access control, audit logs |
| Testing | Vitest, Testing Library, Playwright, Electron integration scripts |
| Quality | `tsc --noEmit` (strict), Biome, WCAG AA contrast audit in CI, `npm audit` + `cargo audit` |
| CI/CD | GitHub Actions &mdash; lint-and-test gate, Windows installer build, releases, update manifests |

## What I care about

- **Local-first software** that stays genuinely useful with the network unplugged
- **Domain modelling** that removes a whole class of manual reconciliation
- **White-label design systems** where the end user picks the accent colour &mdash; and contrast has to hold anyway
- **Print output as a first-class deliverable**, not an afterthought
- **Data integrity** in systems that handle real money and real records
- **Print, paper and proof** &mdash; the technology the operator actually has

## Contact

<div align="center">

[![Email](https://img.shields.io/badge/Email-adilmaher990@gmail.com-EA4335?logo=gmail&logoColor=white&style=flat-square)](mailto:adilmaher990@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-beingadil-181717?logo=github&style=flat-square)](https://github.com/beingadil)
[![Live Demo](https://img.shields.io/badge/Live_Demo-Dental_Solutions-2F6BFF?logo=googlechrome&style=flat-square)](https://beingadil.github.io/Dental-Clinic-Management/)

</div>

<div align="center">

<sub>Open to pull requests, bug reports and collaborations.
&copy; 2026 Muhammad Adil Shahzad</sub>

</div>
