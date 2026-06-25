# Contributing to @edison-watch/shared

Thanks for your interest in improving `@edison-watch/shared`! Issues and focused
contributions are welcome. This is an Edison Watch package rather than a generic
component library, so changes should fit the needs of the Edison Watch clients
that consume it.

## Getting started

You'll need Node.js 22 or later and npm. The [README](README.md#development) has
the full development workflow; the short version:

```sh
git clone https://github.com/Edison-Watch/shared.git
cd shared
npm ci
npm run build
```

## Before you open a pull request

Please make sure the same checks CI runs pass locally:

```sh
npm run typecheck       # TypeScript, no emit
npm run lint            # ESLint
npm run format:check    # Prettier
npm run knip            # unused files / exports / dependencies
npm run test            # vitest
npm run build           # tsdown — ESM + CJS + d.ts
```

If your change affects UI, also review visual regressions and update the
committed baselines when the change is intentional:

```sh
npm run build-storybook
npm run test:visual         # check against committed snapshots
npm run test:visual:update  # update + commit baselines after intentional changes
```

## Guidelines

- **Keep changes focused.** Small, single-purpose PRs are easier to review.
- **Match the surrounding style.** Follow the existing naming, comment density,
  and module layout; `npm run format` handles formatting.
- **Add a story.** New UI components ship with a sibling `*.stories.tsx`.
- **Browser-safe values only.** Never add server credentials, private keys, or
  secrets to `src/config/env-config.ts` — see "Configuration Scope" in the
  [README](README.md#configuration-scope).
- **Describe the why.** A short explanation of the motivation and approach in the
  PR description goes a long way.

## Reporting bugs and security issues

- For ordinary bugs and feature requests, open a
  [GitHub issue](https://github.com/Edison-Watch/shared/issues).
- For **security vulnerabilities**, do **not** open a public issue — follow
  [`SECURITY.md`](SECURITY.md) instead.

## License

By contributing, you agree that your contributions will be licensed under the
[GNU Affero General Public License v3.0](LICENSE) that covers this project.
