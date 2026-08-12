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
| Versions | `1` by default |
| Workloads | `main` (Deployment, primary) |
| Containers | `node` using `wodby/node`, build target |
| Endpoints | `slack-inviter`: HTTP 3000 (main) |
| Service links | None |
| Application build | Git source connection enabled; Dockerfile: `Dockerfile`; boilerplates: [Slack Inviter](https://github.com/wodby/slack-inviter) |
| Helm | chart `oci://registry-1.docker.io/wodby/node`; version `0.2.1` |
| Configuration and operations | 13 settings, 2 integration slots |

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
