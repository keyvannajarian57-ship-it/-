# KARBON deployment access diagnostic

Date: 2026-11-03

## Current deployment
- Website: https://karbon-store.higgsfield.app
- Hosting status reported: deployed
- Community listing: disabled

## Observed public-access issue
A fresh deployment was triggered, but public HTTP requests to the homepage and product/static asset routes continued to return HTTP 401 with JSON body {"error":"unauthenticated"}. The managed /robots.txt route returned HTTP 200.

## Initial diagnosis
The application source reviewed so far did not show a visitor-facing authentication gate. The inspected server setup included CSRF handling for server functions and error middleware, but no obvious rule requiring visitors to sign in.

Because the same 401 response was observed from an external test environment, the issue cannot yet be attributed specifically to Iranian ISP filtering. The leading area to investigate is the hosting/platform access layer, Worker routing, or deployment-level authentication.

## Recommended next checks
1. Inspect hosting project access/privacy/deployment settings for visitor-authentication or preview-only restrictions.
2. Verify that the production hostname is mapped to the intended public deployment and Worker.
3. Inspect platform/Worker logs for the source of the unauthenticated response.
4. After public access works externally, test from multiple Iranian networks without a VPN.
5. Keep community-feed listing disabled.

## Cost and approval constraint
Do not enable paid services, purchase a domain, consume paid credits, or incur any cost without the owner's explicit approval.
