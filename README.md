# Wiz formatter and linter

This repository contains the source-aware formatter and semantic linter for the Wiz language.

Published packages:

- [`@wiz-sh/formatter`](https://www.npmjs.com/package/@wiz-sh/formatter) formats whole files and ranges, checks formatting, and produces deterministic minified output.
- [`@wiz-sh/linter`](https://www.npmjs.com/package/@wiz-sh/linter) runs correctness, safety, suspiciousness, and style rules with precise ranges and classified fixes.

Both packages consume the compiler’s lossless syntax and semantic APIs. They do not maintain a second parser or duplicate name resolution.

## Guarantees

- Formatting is deterministic and idempotent.
- Quote style is preserved unless a rewrite is semantically proven safe.
- Heredocs, comments, arrays, redirections, expansions, typed declarations, and incomplete editor input remain structurally represented.
- Safe and unsafe fixes remain distinguishable.
- Minification preserves shell semantics and is tested separately from normal formatting.

## API

```ts
import { formatSource, minifySource } from "@wiz-sh/formatter";
import { applyLintFixes, lintSourceFile } from "@wiz-sh/linter";
```

## Development

Place the compiler and types repositories beside this checkout:

```console
bun install
bun run check
bun run build
```

Tests cover formatter idempotency, ranges, malformed input, every registered lint category, exact diagnostics, configuration overrides, and fix safety. CLI integration is owned by [`wiz-sh/wiz`](https://github.com/wiz-sh/wiz), while editor integration is owned by [`wiz-sh/lsp`](https://github.com/wiz-sh/lsp).

Licensed under [MIT](LICENSE).
