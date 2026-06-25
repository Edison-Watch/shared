# Security Policy

## Supported versions

`@edison-watch/shared` is pre-1.0 and is consumed from source (including as a Git
submodule) rather than as a versioned npm release. Security fixes land on the
latest `main`; pin a specific commit if you need stability.

| Version | Supported |
| --- | --- |
| latest `main` | ✅ |
| older commits | ❌ |

## Reporting a vulnerability

**Please do not report security issues through public GitHub issues, pull
requests, or discussions.**

Instead, report privately through either channel:

- **GitHub private advisory** — open the repository's **Security** tab and click
  **"Report a vulnerability"** ([private vulnerability reporting](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing-information-about-vulnerabilities/privately-reporting-a-security-vulnerability)).
- **Email** — <security@edison.watch>.

Please include enough detail to reproduce: affected commit, the consuming
context (which entrypoint/component), and a description of the impact. We aim to
acknowledge reports within a few business days and support coordinated
disclosure. We're happy to credit reporters.

## Security model and notes

`@edison-watch/shared` is a library of browser-side React components, design tokens,
and client utilities. It is not a server and ships no backend code, so a few
properties are worth understanding:

- **Browser-safe configuration only.** `src/config/env-config.ts` intentionally
  contains Edison Watch service endpoints and browser-facing configuration (e.g.
  publishable Supabase keys, a Sentry DSN, a PostHog project key). These are
  values that are designed to ship in client bundles and are already exposed in
  any shipped Edison Watch client. **No server credentials, private keys,
  privileged tokens, or other secrets belong in this repository** — see the
  "Configuration Scope" section of the [README](README.md). If you believe a
  value here is *not* safe to expose in a browser, treat it as a vulnerability
  and report it privately.
- **Consumer-supplied dependencies.** The UI and auth modules declare peer
  dependencies (React, React DOM, React Router, Supabase JS). Authentication and
  crypto behavior depend on the consuming application wiring these correctly; the
  package itself stores no credentials.
- **No independent audit.** This code has not undergone an external security
  review. Treat it as experimental.

If you are unsure whether something is a security issue, err on the side of
reporting it privately.
