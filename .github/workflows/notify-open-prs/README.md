# Notify Open PRs Workflow

## 概要

このワークフローは、リポジトリにOpen Pull Requestがあるかを定期的に確認し、存在する場合にはSlackにインタラクティブなメッセージで通知します。

## 使い方

以下は、アクションを使用する際の例です。

```yaml
# スケジュールで毎日1時間おきにPRをチェック
name: Daily PR Check and Slack Notification

on:
  schedule:
    - cron: '0 * * * *'
  workflow_dispatch:

jobs:
  notify-open-prs:
    uses: ./.github/workflows/notify-open-prs.yml
```

## 入力パラメーター

| パラメーター名 | 必須 | デフォルト値 | 説明 |
| ---------------- | ---- | ------------ | ---- |
| SLACK_WEBHOOK_URL | はい | N/A | SlackのWebhook URL (GitHub Secretsに設定) |

## その他

- PRが存在する場合のみSlack通知が行われます。
- メッセージはBlock Kitを使ってリッチに表示され、各PRに「View PR」ボタンが付きます。
