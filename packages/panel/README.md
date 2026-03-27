# @surge-geosite/panel

SvelteKit SSR panel for Surge Geosite.

## Routes

- `/:lang/` where `lang = zh | en`
- Root `/` redirects to locale based on `Accept-Language`
- `/geosite*` proxy endpoints for local development and SSR data fetching

## Scripts

- `pnpm --filter @surge-geosite/panel run dev`
- `pnpm --filter @surge-geosite/panel run typecheck`
- `pnpm --filter @surge-geosite/panel run build`
- `pnpm --filter @surge-geosite/panel run cf:deploy`

## Cloudflare Pages

`wrangler.toml` is configured for Pages direct upload:

- `pages_build_output_dir = ".svelte-kit/cloudflare"`
- `services.GEOSITE_API -> surge-geosite` (required internal service binding)

Useful commands:

- `pnpm --filter @surge-geosite/panel run cf:dev`
- `pnpm --filter @surge-geosite/panel run cf:deploy`
