# prettier-plugin-solidity snapshots viewer

A single static page for reading the Jest snapshots of [prettier-plugin-solidity](https://github.com/prettier-solidity/prettier-plugin-solidity) as diffs.

Live: https://fvictorio.github.io/prettier-plugin-solidity-snapshots-viewer/

## What you can load

- A PR (`#1758` or its URL): the snapshot files it touched, input → output by default, with before → after views for input and output.
- Two refs (`main...branch` or a compare URL).
- A file path, blob URL or `ref:path`, a test name (`Comments`), or `@ref` to browse a branch.
- Local `.snap` files: one to view, two (base, then head) to compare.

## How PRs are fetched

File contents come from raw.githubusercontent.com, comparing the base branch with `refs/pull/N/merge` (falling back to `refs/pull/N/head`). Those requests are not rate limited. The list of changed files costs one GitHub API call (unauthenticated limit: 60/hour). When that fails, the page scans every snapshot file instead, which misses snapshot files in brand-new test directories.

No build step: `index.html` is the whole app.
