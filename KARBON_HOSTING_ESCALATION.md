# KARBON hosting escalation

Date: 2026-11-03

## Deployment
- Website ID: a783836e-ed46-4493-ac33-48712fd12512
- Production URL: https://karbon-store.higgsfield.app
- Hosting-reported status after a fresh deploy: `deployed`
- Community feed listing: `false` (intentionally kept private from the feed)

## Reproduction
From an external test environment in Frankfurt, Germany, immediately after a fresh successful deploy:

| Request | HTTP | Result |
|---|---:|---|
| `GET /` | 401 | `{"error":"unauthenticated"}` |
| `GET /product/p-1` | 401 | `{"error":"unauthenticated"}` |
| `GET /icon.png` | 401 | `{"error":"unauthenticated"}` |
| `GET /robots.txt` | 200 | Managed robots.txt body |

Relevant Cloudflare Ray IDs:
- Homepage: `a54d94e4d9fcdbad-FRA`
- Product route: `a54d94e688f9eb42-FRA`
- Icon route: `a54d94e92e624db9-FRA`

The response is served by Cloudflare and contains only a 27-byte JSON body. Re-deploying the same site again did not change the result.

## Source review
- No visitor-facing authentication middleware or login gate was found in the application source.
- `src/start.ts` applies CSRF protection only to server functions and wraps errors; it does not require visitors to authenticate.
- `app.manifest.json` declares no D1, R2, KV or Durable Object resources.
- `wrangler.jsonc` documents the intended public Workers for Platforms deployment model.
- The same 401 was observed from an external location, so this is not presently attributable only to Iranian ISP filtering.

## Requested investigation by Higgsfield
Please inspect the hosting/platform routing and authorization layer for this website ID and hostname:
1. Confirm the production worker is publicly reachable without a Higgsfield session.
2. Check whether a tenant-level access policy, auth middleware, route binding, or deployment metadata is incorrectly requiring authentication.
3. Identify why `/robots.txt` is served publicly while the homepage, product routes and static assets return 401.
4. Restore anonymous public GET access to the deployed website.

## Cost and privacy constraints
- Do not list the website in the public Higgsfield community feed.
- Do not enable paid services, purchase a domain, consume paid credits, or incur any cost without the owner's explicit approval.
