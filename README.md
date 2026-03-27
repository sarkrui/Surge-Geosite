<div align="center">
  <h1>Surge Geosite</h1>
  <p>Automatically converts <code>v2fly/domain-list-community</code> datasets into ready-to-use Surge rules.</p>
  <p>
    English | <a href="./README.zh-CN.md">中文</a>
  </p>
  <p>
    <a href="https://surge.bojin.co"><strong>Open Dashboard</strong></a>
  </p>
</div>

<p align="center">
  <img src="./docs/assets/panel-dashboard.png" alt="Surge Geosite Dashboard" />
</p>

## Direct Use

1. Open the dashboard: https://surge.bojin.co.
2. Search and select a dataset.
3. Copy the generated raw URL.
4. Paste it into your Surge rules.

If you want to use rule URLs directly, the format is:

- Rules path: `https://surge.bojin.co/geosite/:name_with_filter`

`name_with_filter` has two forms:

- Without filter: `apple`
  Returns the full rules for the `apple` dataset.
- With filter: `apple@cn`
  Returns only rules tagged with `@cn`.

Surge example:

```ini
[Rule]
RULE-SET,https://surge.bojin.co/geosite/apple@cn,DIRECT
RULE-SET,https://surge.bojin.co/geosite/strict/category-ads-all,REJECT
```

## Advanced Usage

### API

- `GET /geosite`
- `GET /geosite/:name_with_filter` (default mode: `balanced`)
- `GET /geosite/:mode/:name_with_filter`

### Mode Guide

- `strict`: only lossless regex conversion
- `balanced`: controlled downgrade (default)
- `full`: most permissive conversion (widest coverage, highest over-match risk)

## For Maintainers

Local dev:

```bash
pnpm install
pnpm build
pnpm test
pnpm panel:dev
pnpm worker:dev
```

Deploy:

```bash
pnpm worker:deploy
pnpm panel:deploy
```

## GitHub Automation

This repository includes GitHub Actions for:

- deploying `packages/panel` to Cloudflare Pages on every branch push
- syncing this fork with all upstream branches on a schedule or manual run

Repository configuration:

- Secrets:
  - `CLOUDFLARE_API_TOKEN`
  - `CLOUDFLARE_ACCOUNT_ID`
- Variables:
  - `CLOUDFLARE_PAGES_PROJECT` (optional, defaults to `surge-geosite-panel`)
  - `UPSTREAM_REPOSITORY` (required for sync, format `owner/repo`)
  - `SYNC_BRANCHES` (optional, comma/newline-separated; defaults to all upstream branches)

Technical architecture: [docs/architecture.md](./docs/architecture.md)
