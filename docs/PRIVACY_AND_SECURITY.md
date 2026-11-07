# Privacy & Security

This repository is a **public showcase** of a private production system. This
document states exactly what is and is not public, and how security is handled.

## What this repository contains

- Conceptual documentation of the product and its architecture
- Aggregate, verified engineering metrics (commits, file and line counts, test counts)
- Sanitized engineering narratives with no operational details
- Original diagrams and visual assets created for this showcase

## What this repository deliberately does NOT contain

- **No production source code.** The implementation remains in the private repository.
- **No secrets.** No tokens, API keys, passwords, cookies, session identifiers,
  encrypted blobs, or environment files — nothing to leak.
- **No private configuration.** No server addresses, hostnames, network
  configuration, proxy endpoints or credentials, or infrastructure identifiers.
- **No user data.** No user records, identifiers, orders, transaction data, logs,
  screenshots, or OTP material.
- **No database schemas or internal interfaces.** Architecture is described
  conceptually only.
- **No private history.** No internal branch names, commit messages, or private
  workflows from the production repository; this showcase was initialized as a
  fresh repository with its own history.

## How the production system handles secrets

- Configuration and secrets are supplied at runtime through the environment;
  **nothing sensitive is committed to Git**.
- Encrypted secret material is managed with **SOPS using age encryption**, and
  materialized only on the production host by a controlled bootstrap process.
- Structured logging includes **secret redaction**, and diagnostic capture for
  external services is built around a strict **never-log contract** with
  bounded, scrubbed payloads.
- Daily automated backups are encrypted-at-rest-by-default artifacts managed
  outside the application, with retention and a validated, staged restore flow.

## Guidance for users of the bot

- The bot asks only for what a chosen workflow requires (for example, an email
  address or account preferences) and explains each step in the conversation.
- Do not send information the bot does not explicitly request for the workflow
  you selected.
- Service availability may change; nothing in this showcase is a guarantee of
  uptime or availability.

## Security policy

See [SECURITY.md](../SECURITY.md) for how to report a security concern in this
showcase repository. Concerns about the production service itself should be
raised privately with the operator via the bot's support conversation.
