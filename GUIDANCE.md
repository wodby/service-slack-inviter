# Slack Inviter on Wodby

What this service adds to the Node.js service it is based on. The application is the public `wodby/slack-inviter` project: an invitation page for a Slack community. It is configured entirely through environment variables; the source needs no edits.

## Where each variable comes from

| Source | Variables |
| --- | --- |
| Set by the service | `PUBLIC_URL` (the environment's primary URL), `TURNSTILE_EXPECTED_HOSTNAME` (the primary host), `TRUST_PROXY` (`true`) |
| Service settings | `SLACK_TEAM` (required), `COMMUNITY_NAME`, `COMMUNITY_HEADLINE`, `COMMUNITY_DESCRIPTION`, `COMMUNITY_WEBSITE_URL`, `COMMUNITY_LOGO_URL`, `COMMUNITY_SUPPORT_URL`, `COMMUNITY_PRIVACY_URL`, `SOCIAL_IMAGE_URL`, `RATE_LIMIT_IP_MAX`, `RATE_LIMIT_IP_WINDOW_SECONDS`, `RATE_LIMIT_EMAIL_MAX`, `RATE_LIMIT_EMAIL_WINDOW_SECONDS` |
| Slack integration (required) | `SLACK_TOKEN` |
| Cloudflare Turnstile integration (optional) | `TURNSTILE_SITE_KEY`, `TURNSTILE_SECRET_KEY` |

Change the page's texts, links and limits through the service's settings, and the token and keys through the attached integrations. Do not put them in the repository or in a `.env` file.

## What the application requires

- It refuses to start without `SLACK_TEAM` and `SLACK_TOKEN`, and without `PUBLIC_URL` unless `NODE_ENV` is `development` or `test`.
- `SLACK_TEAM` is the workspace subdomain only, not a URL.
- `PUBLIC_URL` must be an origin only: scheme and host, no path.
- Turnstile verification is on when both Turnstile variables are present. Only one of them makes the application refuse to start.
- `COMMUNITY_LOGO_URL` and `SOCIAL_IMAGE_URL` accept an HTTPS URL or a root-relative path.
- A failed start reports the offending variable by name in the container's log.

## Running

- The application listens on `NODE_PORT`, which the Node.js service sets to 3000. It has no dependencies to install.
- `/healthz` and `/.healthz` answer the health check.
- The rate limiter keeps its counters in the memory of one process. They are not shared between replicas and are reset by a restart.
- The service uses none of the database, mail or Redis variables of the Node.js service.
