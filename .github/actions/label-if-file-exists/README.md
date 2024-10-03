# {{workflow_name}}

## 概要

PRの変更に特定のファイルが含まれている場合、指定されたラベルを追加します。

## 使い方

以下は、アクションを使用する際の例です。

```yaml
name: Label if file exists in PR

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  label:
    runs-on: ubuntu-latest
    steps:
      - name: Label if file exists in PR
        uses: ./.github/actions/label-if-file-exists
        with:
          file_pattern: 'your-regex-pattern'
          label_name: 'your-label'
```

## 入力パラメーター

| パラメーター名 | 必須 | デフォルト値 | 説明 |
| ---------------- | ---- | ------------ | ---- |
| file_pattern | 必須 |  | ファイルパスを指定する(正規表現) |
| label_name | 必須 |  | ファイルが存在する場合に追加するラベルを指定する |
