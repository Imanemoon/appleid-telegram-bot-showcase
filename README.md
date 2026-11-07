<div align="center">

  <a href="README.fa.md">🇮🇷 فارسی</a> · <strong>🇬🇧 English</strong>

</div>

<div align="center">
  <img src="assets/banner.svg" alt="Apple ID Telegram Bot — banner" width="100%" />

  # Apple ID Telegram Bot

  **A production Telegram platform for Apple ID workflows — email availability checks, orders, payments, inventory, and automated account delivery.**

  [![Try the bot](https://img.shields.io/badge/%F0%9F%92%AC-Try%20the%20Telegram%20Bot%20%E2%86%92%20%40Theappleidbot-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/Theappleidbot)

  [![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)](docs/ARCHITECTURE.md)
  [![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI-2088FF?logo=githubactions&logoColor=white)](docs/TESTING_AND_QUALITY.md)
  [![pytest](https://img.shields.io/badge/pytest-regression%20suite-0A9EDC?logo=pytest&logoColor=white)](docs/TESTING_AND_QUALITY.md)

  **Status:** Production · actively developed since September 2025 · latest activity November 2026
</div>

## What the Product Does

The bot turns multi-step Apple ID work into guided, resumable Telegram conversations. Users can:

- **Check email availability** for Apple ID registration — rate-limited, cached, and abuse-protected
- **Buy ready-made Apple IDs** from managed stock, with reservation-safe inventory
- **Order personalized accounts** created through automated, verified browser workflows
- **Pay by wallet or receipt** — idempotent payment processing with admin-reviewed approvals
- **Follow every step live** — OTP verification, order status, and clear delivery updates
- **Recover from interruptions** — resumable operations, daily backups, and a validated restore flow

The user interface is fully localized in Persian (Farsi).

## User Journey

![User journey flowchart](assets/user-flow.svg)

1. Open [t.me/Theappleidbot](https://t.me/Theappleidbot) and tap **Start**.
2. Pick a service from the menu.
3. Follow the guided conversation — every step is validated.
4. The system reserves inventory, checks payment, and runs the automation.
5. Receive the account or clear status updates at every stage.

## Architecture

![High-level architecture](assets/architecture.svg)

A layered design with an enforced dependency direction: Telegram handlers deliver conversations, application services orchestrate use cases, and domain authorities own the invariants for payments, inventory, OTP, catalog, and backups — backed by MySQL, Dockerized browser automation with a warm session pool, and background task processing. Operations run on Linux under systemd with SOPS-encrypted secrets and daily automated backups.

Proxy support exists in the codebase as an optional integration; it is **disabled in the current production runtime** (verified November 3, 2026).

Conceptual walkthrough: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

## Engineering Highlights

- **Warm browser sessions that stay reliable.** A configuration conflict killed the first pre-warmed browser slot, stretching email checks toward minutes → fixed the conflict, added eager page loads and in-session soft retries, refilled idle slots in the background → dependable warm slots, with a repeatable instrumented bench harness.
- **Deploy restarts that never race live work.** The restart gate probed signals that were never written, so it could interrupt jobs or skip restarts forever → probe only real runtime signals, exclude orphaned leases, bound the wait with an injected clock → restarts happen only when provably idle, with a forced-restart safety bound.
- **From hardcoded products to a real catalog.** Every new product type required touching pricing, payment, inventory, and fulfillment paths → persistent per-type catalog, pricing kept with its own authority, fail-closed legacy fallbacks, write-once order snapshots → additive-only schema changes and immutable historical pricing.

Full narratives with investigation details: [docs/ENGINEERING_HIGHLIGHTS.md](docs/ENGINEERING_HIGHLIGHTS.md).

## Technology & Quality

**Stack:** Python 3.12 · python-telegram-bot 22.8 · MySQL/MariaDB · Selenium Grid in Docker (warm session pool) · OpenPyXL/pandas · pytest · GitHub Actions · Linux + systemd · SOPS (age).

An extensive pytest suite — unit, integration, and database-backed tests guarding payment integrity, inventory reservations, and backup/restore — runs as a CI gate on every push, and automated PRs merge only after the full run passes on the exact commit. The latest CI run on main (November 7, 2026) is green.

Details, scale metrics, and counting methodology: [docs/TESTING_AND_QUALITY.md](docs/TESTING_AND_QUALITY.md) · [docs/DEVELOPMENT_TIMELINE.md](docs/DEVELOPMENT_TIMELINE.md).

## Project Documentation

| Document | Contents |
|---|---|
| [Features](docs/FEATURES.md) | Public-safe feature breakdown |
| [Architecture](docs/ARCHITECTURE.md) | Conceptual architecture and design principles |
| [Engineering Highlights](docs/ENGINEERING_HIGHLIGHTS.md) | Complete technical narratives |
| [Development Timeline](docs/DEVELOPMENT_TIMELINE.md) | Verified milestones, activity, and project-scale metrics |
| [Testing & Quality](docs/TESTING_AND_QUALITY.md) | Test strategy and CI evidence |
| [Privacy & Security](docs/PRIVACY_AND_SECURITY.md) | What is and isn't public, and how secrets are handled |
| [FAQ](docs/FAQ.md) | Common questions |

## Attribution & Disclaimer

- **AI-assisted, human-directed.** AI agents implemented reviewed designs and investigated failures; architectural decisions, review, integration, and validation are owned by the project author. Neither autopilot nor hand-written-only — a deliberate, CI-gated engineering workflow.
- **Independent project.** Not affiliated with or endorsed by Apple Inc. Apple, Apple ID, and related marks are trademarks of Apple Inc. Service availability may change.
- **Showcase only.** The production implementation, configuration, and operational data remain private; this repository intentionally contains no production source code, secrets, or user data.

---

<div align="center">

**Built and maintained by [Imanemoon](https://github.com/Imanemoon)**

</div>
