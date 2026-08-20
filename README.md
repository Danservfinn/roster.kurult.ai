# roster.kurult.ai

The stamped seat roll of the [Kurultai](https://kurult.ai) agent fleet. One static page: fourteen named seats, one role each, stamped by hand. The public lab front is [kurult.ai](https://kurult.ai); this host is gated (unauth 302), not public.

## Invariants

- No build system, no framework, no client JavaScript, no webfonts. The committed files are the artifact.
- No live counters, rates, or current-state claims. The stamp may lag the sidebar; that is expected.
- No legal-entity claims ("LLC") until the NC certificate exists.
- `llms.txt` lists durable public surfaces only — never gated hostnames.
- Hermes agents named Kublai and Hülegü sit elsewhere; they are not this roster.
- Design test for any edit: the page must remain correct if never touched again.

## Deploy

Cloudflare Pages, direct upload of the repo root:

```sh
CLOUDFLARE_API_TOKEN=$(cat ~/.kublai/secrets/cloudflare-pages-api-token) \
  npx wrangler@latest pages deploy . --project-name roster-kurult-ai
```

Break-glass (no CLI): Cloudflare dashboard → Workers & Pages → roster-kurult-ai → Create deployment → drag this folder in.

Custom domain: attach `roster.kurult.ai` in Pages → Custom domains. Do not touch `kurult.ai` MX / mail records.

Rollback: redeploy any prior deployment from the Pages dashboard (one click).

## Verify after deploy

```sh
curl -sI https://roster.kurult.ai/            # unauth 302 — gated, not public
curl -sI https://roster.kurult.ai/llms.txt    # unauth 302 — gated, not public
dig +short kurult.ai MX                        # unchanged — mail records are never touched
```
