# Slack Inviter service for Kubernetes on Wodby

Build and run Slack Inviter applications on Kubernetes with Wodby.

This repository defines the Wodby service manifests and operational
configuration for Slack Inviter.

- [Slack Inviter service on Wodby](https://wodby.com/services/slack-inviter)
- [Browse Wodby services](https://wodby.com/services)
- [Wodby service documentation](https://wodby.com/docs/2.0/services/)
- [Service manifest reference](https://wodby.com/docs/2.0/services/template/)

## Start with a boilerplate

Use one of the boilerplates exposed by this service to start with compatible
build configuration and Wodby CI:

- [Slack Inviter](https://github.com/wodby/slack-inviter)

## Wodby stacks using this service

- [Slack Inviter application stack](https://github.com/wodby/stack-slack-inviter)

## Service overview

| Property | Manifest configuration |
| --- | --- |
| Service name | `slack-inviter` |
| Type | Application service |
| Base service | [Node.js](https://github.com/wodby/service-node) `2.0.0`, compatible with future `2.x` revisions |
| Runtime versions | Node.js 22 and newer options inherited from the Node.js service |
| Workloads and endpoint | Inherited Node.js deployment and HTTP port 3000 |
| Service links | Optional database, SMTP, and Redis/Valkey links inherited from Node.js |
| Application build | Git source connection enabled; Dockerfile: `Dockerfile`; boilerplates: [Slack Inviter](https://github.com/wodby/slack-inviter) |
| Helm | Inherited from the Node.js service |
| Configuration and operations | 13 settings, 2 integration slots |

> [!WARNING]
> This service requires an existing Slackin-compatible legacy administrator API
> token. Slack no longer issues these tokens, and ordinary Slack app or bot
> tokens do not work with the legacy invitation endpoint. Use this service only
> when migrating a working Slackin installation whose token is still active.

The required `Slack legacy API token` integration exports `SLACK_TOKEN`. The
Slack workspace subdomain is configured separately through the required `Slack
workspace` setting. Cloudflare Turnstile is optional; enable it by attaching a
Cloudflare integration with its Turnstile kind selected. That kind exports
`TURNSTILE_SITE_KEY` and `TURNSTILE_SECRET_KEY` directly, and unrelated
Cloudflare Application Access fields are not exposed to this service.

## Use this service

Use this service through [Slack Inviter application stack](https://github.com/wodby/stack-slack-inviter), or reference `slack-inviter` from
a custom Wodby stack.

A service is a reusable component and does not deploy by itself. The stack
defines its links, settings, versions, resources, and relationship to the rest
of the application.

## Maintain a custom version

1. Fork this repository.
2. Edit the service manifest and referenced files.
3. Import the repository as a [Git-backed service](https://wodby.com/docs/2.0/services/create/#create-a-git-backed-service).
4. Reference the service from a stack manifest.

Keep service, workload, container, endpoint, link, volume, config, and
derivative names stable unless dependent stacks and app-level overrides are
updated at the same time.

Validate the manifests with:

```bash
wodby service validate-manifest service.yml --org <org-id>
```

See the [service manifest reference](https://wodby.com/docs/2.0/services/template/) and the [managed services index](https://github.com/wodby/services).
