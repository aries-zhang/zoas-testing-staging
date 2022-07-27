# Zendesk OpenAPI Service (ZOAS) - Staging Testing
This is a supporting test repository for the [ZOAS](https://github.com/zendesk/zoas) application and [api-docs](https://github.com/zendesk/api-docs) workflow in staging environment only.

## Owners

This repository is maintained by the **API Experience** team.

| Ref    | Link                                                              |
|:-------|:------------------------------------------------------------------|
| Wiki   | https://zendesk.atlassian.net/wiki/spaces/RED                     |
| Slack  | [#redback-team](https://zendesk.slack.com/messages/CL45RMA92)     |
| GitHub | [@zendesk/redback](https://github.com/orgs/zendesk/teams/redback) |

## Simulate a call to publish documentation - This copies markdown files to api-docs in staging branch.
- You can create PR in this repository and test all the features you need.
- This repository has an installed Github application [zoas-server-staging](https://github.com/apps/zoas-server-staging) which is deployed in [Pod998](https://spinnaker.zende.sk/#/applications/zoas/executions?pipeline=pod998). [Pod998](https://spinnaker.zende.sk/#/applications/zoas/executions?pipeline=pod998) is the staging environment for ZOAS
- Created PR (unmerged) will trigger the check suite against ZOAS server in [Pod998](https://spinnaker.zende.sk/#/applications/zoas/executions?pipeline=pod998) and you should be able to see the result in checks details section
- Any merged PRs will trigger documentation publish flow against [api-docs](https://github.com/zendesk/api-docs) repository with `staging branch only`. You should be able to see the published docs in [zoas-testing-staging in api-docs staging branch](https://github.com/zendesk/api-docs/tree/staging/docs/zendesk/zoas-testing-staging)
- PRs in [zoas-testing-staging](https://github.com/zendesk/zoas-testing-staging) does not support documentation publish in [developer-docs](https://github.com/zendesk/developer-docs) repository

## Testing zendesk/redback-github-action changes
This repository can be used for testing changes in shell script and action yaml in [zendesk/redback-github-actions](https://github.com/zendesk/redback-github-actions) by editing the `.github/workflows/zoas_doc_publish.yaml` in this repository.

- Add pull_request as the trigger for the action

```
    name: ZOAS documentation publish
    on:
    repository_dispatch:
        types: publish
    pull_request:
        types: [opened, reopened, synchronize]
```

- Change branch name to your development branch

```
    -  name: Checkout action
        uses: zendesk/checkout@v2
        with:
          repository: zendesk/redback-github-actions
          token: ${{ secrets.ORG_GITHUB_TOKEN }}
          path: .github/redback-github-actions
          ref: your-development-branch
```

