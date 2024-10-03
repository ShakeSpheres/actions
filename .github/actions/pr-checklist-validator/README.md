# PR Checklist Validator

## 概要

PR Checklist Validator アクションは、プルリクエストの指定セクション内に含まれるチェックリストがすべてチェックされているかを確認し、未チェック項目がある場合はマージを防ぎます。特定のコメントタグの間に記載されたチェックリストを対象にしているため、柔軟なチェックが可能です。

## 使い方

以下は、アクションを使用する際の例です。

```yaml
name: PR Checklist Validator

on:
  pull_request:
    types: [opened, edited, reopened]

jobs:
  validate-checklist:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Run PR Checklist Validator
        uses: ./.github/actions/pr-checklist-validator
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
```

## 入力パラメーター

| パラメーター名 | 必須 | デフォルト値 | 説明 |
| ---------------- | ---- | ------------ | ---- |
| github_token     | はい | なし         | リポジトリのGitHub Token（${{ secrets.GITHUB_TOKEN }}）を指定します。 |

## その他

このアクションを利用することで、プルリクエストのレビュー時にチェックリスト項目の確認を自動化し、未チェック項目の見逃しを防ぐことができます。対象となるチェックリストは、PR本文の中で `<!-- PR-CHECKLIST-VALIDATOR:START -->` と `<!-- PR-CHECKLIST-VALIDATOR:END -->` で囲まれた範囲内の内容のみを対象とします。

### 例

```markdown
<!-- PR-CHECKLIST-VALIDATOR:START -->
- [ ] チェックリスト項目1
- [ ] チェックリスト項目2
<!-- PR-CHECKLIST-VALIDATOR:END -->
```

## リポジトリにブランチの保護ルールを設定する

1. リポジトリの設定にアクセスする
2. Settings（設定） タブをクリックする
3. 左側のサイドバーで Code and automation セクションの Branches をクリックする
4. new ruleset をクリックする
5. Add branch rule（ブランチルールを追加） ボタンをクリックする
6. ルール名を記入 (例: PR Checklist Validator)
7. Enforcement status を Enabled にする
8. Target branchesのadd target で対象ブランチを指定する
9. 「Require status checks to pass」にcheckを入れる
10. 「Require branches to be up to date before merging」にcheckを入れる
11. 「Status checks that are required」の 「+ Add checks」を押下
12. 導入したworkflowの名称を選択(例:validate-checklist)
13. 「Svae changes」を押下
