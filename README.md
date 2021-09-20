# Zendesk OpenAPI Service (ZOAS) - Staging Testing
This is a supporting test repository for the [ZOAS](https://github.com/zendesk/zoas) application and [api-docs](https://github.com/zendesk/api-docs) workflow in staging environment only.

## Owners

This repository is maintained by the **API Experience** team.

| Ref    | Link                                                              |
|:-------|:------------------------------------------------------------------|
| Wiki   | https://zendesk.atlassian.net/wiki/spaces/RED                     |
| Slack  | [#redback-team](https://zendesk.slack.com/messages/CL45RMA92)     |
| GitHub | [@zendesk/redback](https://github.com/orgs/zendesk/teams/redback) |

## Simulate a call to publish documentation only - This copies markdown files to api-docs and developer-docs in staging branch.

Notes:

- You will need a [personal access token](https://github.com/settings/tokens) generated for your GitHub account, which is then enabled for SSO against the https://github.com/zendesk organization. Use this in place of `PAT_TOKEN` in the `curl` call below.
- Call is simulated against the following `foodjira/recipes` repository OpenAPI [commit](https://github.com/foodjira/recipes/commit/f4b0368aab44634d7c6ebb0740ae7c37af1382aa).

```sh
curl \
  --data '{"event_type":"publish","client_payload": {"repository":"foodjira/recipes","commitSha1":"f4b0368aab44634d7c6ebb0740ae7c37af1382aa","publishBranch":"staging"}}' \
  --header "Accept: application/vnd.github.v3+json" \
  --header "Authorization: token PAT_TOKEN" \
  --request POST \
    https://api.github.com/repos/zendesk/zoas-testing-staging/dispatches
```
