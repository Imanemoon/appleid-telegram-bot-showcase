# FAQ

### What is this project?
A production-oriented Telegram platform for Apple ID workflows: email
availability checks, ready-account purchases, personalized account orders,
wallet and payments, inventory, fulfillment, and recovery — presented here as a
public engineering showcase.

### Is the source code available?
No. The production implementation is private. This repository is a curated
showcase: documentation, verified metrics, and conceptual architecture only.

### Is this affiliated with Apple?
No. This is an independent project, not affiliated with or endorsed by Apple
Inc. See the disclaimer in the [README](../README.md).

### How do I use the bot?
Open [t.me/Theappleidbot](https://t.me/Theappleidbot), tap **Start**, and pick a
service. The interface is in Persian (Farsi).

### Is the bot free?
Checking email availability is available with tiered rate limits; purchases use
the wallet or receipt-based payment paths. Availability and pricing are
controlled by the live service and may change.

### Is the bot always available?
No availability guarantee is made. It is actively operated and developed
(latest activity November 2026), but service availability may change.

### Why is the interface in Persian?
The product's audience is Persian-speaking Telegram users. The engineering
conversation here is in English; the product conversation is in Farsi.

### How were the metrics in the README produced?
They were recomputed from the project's `main` branch with documented counting
methods (`git rev-list` / `git ls-tree`, physical line counts, `def test_`
counts). See [Project Scale & Verified Metrics](../README.md#project-scale--verified-metrics)
and the methodology notes there.

### Why describe architecture only conceptually?
The public repository must not expose implementation details, infrastructure,
or configuration of a running production system. Conceptual-level descriptions
are enough to evaluate the engineering without creating risk.

### What does "AI-assisted engineering" mean here?
The project was developed iteratively with AI coding/investigation agents under
human technical direction, with review, regression testing, and CI gating on
every change. It is not claimed that AI built the product unattended, nor that
all code was hand-written — see
[AI-Assisted Engineering Workflow](../README.md#ai-assisted-engineering-workflow).

### Can I self-host it?
Not from this repository. This showcase intentionally contains no deployment
instructions, configuration, or infrastructure details.
