# RoleWeave site

Official marketing site for **RoleWeave** — a desktop workspace for organizing
and working with AI employees.

**Live:** https://bytefolk.github.io/ordane/

RoleWeave itself lives in [`roleweave`](https://github.com/bytefolk/roleweave):
the file tree is the org chart, roles live in folders, and nested folders define
reporting relationships. This repository holds only the public site (static
HTML, no build step) and is deployed via GitHub Pages.

Every product claim on the page must be backed by the `roleweave` repository —
its README, release notes, or docs. Anything not yet delivered reads as
planned or preview, never as shipped.

## Verify

```bash
npm ci
npx --no-install playwright-core install chromium
npm run verify
```

`verify:contrast` audits every text/background pair the page renders, in both
themes, against the WCAG thresholds; tokens are parsed out of `index.html`, so
the audit cannot drift from the file. `verify:render` renders the page,
screenshots hero / `#runtime` / `#ladder`, asserts the reveal blocks and the
tab switcher, and fails closed on page errors. `verify:failclose` proves that
fail-close path still exits non-zero.

## Contributing

This repository follows ByteFolk's organization-wide contribution flow:
issue → branch → pull request → CI → independent review → squash merge.
See [CONTRIBUTING.md](https://github.com/bytefolk/.github/blob/main/CONTRIBUTING.md)
and [GOVERNANCE.md](https://github.com/bytefolk/.github/blob/main/GOVERNANCE.md).

## License

Apache-2.0 — see [LICENSE](LICENSE).
