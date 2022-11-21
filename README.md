# pull-request-json
プルリクエストの情報を収集するためのWorkflow

## sample
プルリクエストのClose時にデータをJson形式で受け取る

``` yaml
name: Closed

on:
  pull_request:
    types: [ closed ]

jobs:
  PullRequestClosed:
    runs-on: ubuntu-latest
    steps:
      - name: Get PullRequest number
        id: pr-number
        uses: actions/github-script@v6
        with:
          script: return context.issue.number;
      - name: Run
        id: set-result
        uses: iwata-n/actions-pull-request-json@main
        with:
          pullRequestNumber: ${{steps.pr-number.outputs.result}}
      - name: Get result steps
        run: echo ${{steps.set-result.outputs.result}}
```

結果のJsonサンプル

``` json
{
    "owner":"iwata-n",
    "repo":"actions-pull-request-json",
    "pull_number":"3",
    "title":"Create test",
    "user":"iwata-n",
    "created_at":"2022-11-21T09:40:08Z",
    "merged_at":null,
    "first_ready_for_review_at":"2022-11-21T09:40:16Z",
    "last_ready_for_review_at":"2022-11-21T09:40:16Z",
    "head":"test",
    "base":"main",
    "commits":1,
    "additions":1,
    "deletions":0,
    "changed_files":1
}
```