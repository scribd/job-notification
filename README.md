# job-notification

[![CI](https://github.com/scribd/job-notification/actions/workflows/ci.yml/badge.svg?branch=main&event=push)](https://github.com/scribd/job-notification/actions/workflows/test.yml) [![semantic-release: angular](https://img.shields.io/badge/semantic--release-angular-e10079?logo=semantic-release)](https://github.com/semantic-release/semantic-release)

A GitHub Action for sending job notifications

## Table of contents

- [Quick Start](#quick-start)
- [Advanced usage](#advanced-usage)
  - [Customize message](#customize-message)
  - [Overwrite repository link](#overwrite-repository-link)
- [Development](#development)
  - [Testing](#testing)
- [Maintainers](#maintainers)

## Quick Start

```yaml
steps:
  - name: Send notification 
    if: always() # Always send notification regardless of the job status.
    uses: scribd/job-notification@main
    with:
      token: ${{ secrets.SCRIBD_SLACK_GENERIC_TOKEN }}
      channel: test-release-notification
```

## Advanced usage

### Customize message

By default, the notification uses the latest commit message. You can overwrite that using the `message` field. 

To test the message formating, use the [Block Kit Builder](https://app.slack.com/block-kit-builder/).

```yaml
steps:
  - name: Send notification 
    if: always()
    uses: scribd/job-notification@main
    with:
      token: ${{ secrets.SCRIBD_SLACK_GENERIC_TOKEN }}
      channel: test-release-notification
      message: <https://github.com/${{ github.repository }}|Released update>
```

### Overwrite repository and status

By default, the notification links to the repository that triggers the job. You can overwrite that using the `repository` field, which is useful for managing the release for multiple repositories in one place. See [scribd-api-proto](https://github.com/scribd/scribd-api-proto) for example.

```yaml
# Example: release.yml in scribd-api-proto
steps:
  - name: Send notification 
    if: always()
    uses: scribd/job-notification@main
    with:
      token: ${{ secrets.SCRIBD_SLACK_GENERIC_TOKEN }}
      channel: test-release-notification
      repository: scribd/scribd-api-ruby
```
Additionally, `status` can be set explicitly to `success`, `failure` or another custom value to override the default behavior of using status of the job calling this action.

```yaml
steps:
  - name: Send notification
    uses: scribd/job-notification@main
    with:
      token: ${{ secrets.SCRIBD_SLACK_GENERIC_TOKEN }}
      channel: test-release-notification
      status: warning
```

## Development

### Testing

You can test your changes by pushing them to a branch, which will trigger the [test](.github/workflows/test.yml) workflow to send the notifications to the [test-release-notification](https://scribd.slack.com/archives/C04U68KR6CU) channel on Slack.

## Maintainers

Made with ❤️ by the Service Foundations teams.
