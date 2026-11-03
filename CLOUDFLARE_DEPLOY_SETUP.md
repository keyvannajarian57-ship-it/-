# KARBON — Free Cloudflare deployment setup

The repository contains a GitHub Actions workflow that builds the saved KARBON source archive and deploys it to Cloudflare Workers.

## One-time account setup

1. Create/sign in to a Cloudflare account: https://dash.cloudflare.com/
2. Open **Workers & Pages** and configure the account's free `workers.dev` subdomain if Cloudflare asks.
3. Open **My Profile → API Tokens → Create Token → Custom Token**.
4. Create a token with the minimum practical permissions for the first deployment:
   - Account → Workers → **Admin** (product-level; the first deploy creates the Worker).
   - Account → Account Settings → **Read**.
   - If the token editor offers them and Wrangler requests them: User → User Details → **Read**, and User → Memberships → **Read**.
   - Do not add Zone permissions; this deployment uses the free `workers.dev` address and does not configure a custom domain.
5. Copy the token once. Do not paste it into chat, source files, or commits.

## Add two GitHub Actions secrets

In this repository open **Settings → Secrets and variables → Actions → New repository secret** and add:

- `CLOUDFLARE_API_TOKEN` — the API token you just created.
- `CLOUDFLARE_ACCOUNT_ID` — the Account ID shown on the Cloudflare account overview page.

Keep both values private. Do not commit them.

## Run the deployment

1. Open the repository's **Actions** tab.
2. Select **Deploy KARBON to Cloudflare Workers**.
3. Select **Run workflow** and confirm.
4. When the job succeeds, the Worker should be available at:
   `https://karbon-store.<your-workers-dev-subdomain>.workers.dev`

## Notes

- This deploys the current backed-up source; it does not delete or modify the existing Higgsfield website.
- The deployment workflow is manual-only; a normal GitHub push will not deploy automatically.
- Cloudflare Workers Free currently documents 100,000 requests/day and 10 ms CPU time per request. SSR pages must stay within the CPU limit.
- A `workers.dev` address is useful for a free trial, but Cloudflare recommends a custom domain or route for business-critical production. A custom domain requires a domain/zone and may cost money.
- Cloudflare cannot guarantee that every ISP or country can reach its shared network IPs. Before treating this as the production store, test the new URL from multiple Iranian networks without VPN.
- No paid plan, domain, or add-on is enabled by this workflow.
