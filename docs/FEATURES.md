# Features

A public-safe breakdown of what the Apple ID Telegram Bot does. Internal
implementation details are intentionally omitted.

> **Try it:** [t.me/Theappleidbot](https://t.me/Theappleidbot) — the interface is
> localized in Persian (Farsi).

## User-facing workflows

### Email availability check
- Users submit an email and the platform reports whether it can be used for Apple ID registration.
- Requests pass through validation, tiered rate limits (free vs. registered tiers), caching, and abuse protection before any automation runs.
- Results are delivered in the same conversation, with status updates while the check is in flight.

### Ready-account purchase
- Buyers pick a prepared Apple ID from managed stock.
- Inventory is **reserved** for the buyer during checkout, so stock cannot be double-sold.
- Payment can be made from a stored wallet balance or through receipt-based payment reviewed by an administrator; delivery follows confirmation.

### Personalized (custom) Apple ID order
- Buyers specify their preferences through a guided conversation.
- The platform creates the account through automated browser workflows, including verification steps, and delivers it once complete.
- The order is resumable: if any step is interrupted, it continues from where it stopped rather than restarting from scratch.

### Wallet & payments
- Users hold a balance, top it up, and pay for orders from the wallet.
- Payment approvals include safeguards: idempotent processing, audited admin approvals/rejections, and refund handling.
- Receipt-based payment paths (including card-to-card submission) are supported for users who do not pay from the wallet.

### Account & order self-service
- Users can review their orders, follow live status updates, and interact with delivery material.
- Warranty options may be offered per product type, with clear pricing shown before confirmation.

### Support & moderation
- Support tickets, broadcasts, and bans give the operator a full administration surface.
- Admin panels cover catalog management, inventory, payment review, user management, and reporting.

## Operator-facing capabilities

| Capability | Description |
|---|---|
| **Product catalog** | Persistent catalog of product types with per-type pricing, warranty options, and promotional pricing, plus fail-closed fallbacks for legacy compatibility |
| **Inventory management** | Stock tracking with reservation/lease semantics and expiry so abandoned reservations free up automatically |
| **Discounts & coupons** | Coupon redemption with a dedicated authority and per-user limits |
| **Payment review** | Approve/reject workflows with integrity guarantees and complete auditability |
| **Fulfillment orchestration** | Distinct ready-stock and personalized fulfillment pipelines, including compensation logic for edge cases |
| **Financial & inventory reporting** | Reporting surfaces with Excel export support (OpenPyXL) |
| **Backup & restore** | Daily automated database backups with retention, a staged restore flow with typed confirmations, and post-restore validation |
| **Recovery tooling** | Recovery bundles, restart-when-idle deployment gates, and documented runbooks |

## Platform qualities

- **Resumable conversations.** Workflow state is durable; restarts and interruptions do not strand users mid-flow.
- **Rate limiting & abuse protection.** Tiered limits and request guards protect the automation from abuse and runaway costs.
- **Localized UI.** The entire user experience runs in Persian with consistent keyboards and message templates.
- **Observability.** Structured logging with secret redaction and production metrics counters.
