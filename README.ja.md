<p align="center">
    <img width="400" alt="Technical Decision Record Skill Logo" src="https://github.com/user-attachments/assets/3af14b51-33a3-4944-936a-4748d2aaffd7" />
</p>

<h1 align="center" style="border-bottom: none;">
    <code>Technical Decision Record Skill</code>
</h1>

<p align="center">
  技術的な意思決定を再利用可能な Markdown の記録としてまとめるための Codex Skill です。
</p>

<p align="center">
  <a href="./README.md">English</a> |
  <a href="./README.ko.md">한국어</a> |
  <a href="./README.ja.md">日本語</a> |
  <a href="./README.zh-CN.md">简体中文</a>
</p>

## 概要

`technical-decision-record` は、技術的な選択を再利用可能な意思決定記録に変換するための Skill です。

次のような内容を記録したいときに役立ちます。

- なぜ特定の実装を選んだのか
- どのような代替案を検討したのか
- なぜそれらの代替案を採用しなかったのか
- どのような trade-off を受け入れたのか
- どのような根拠や結果がその決定を支えているのか
- 次回は何を改善できるのか

この Skill は、プロジェクトの振り返り、Issue コメント、Pull Request の説明、アーキテクチャノート、ポートフォリオ、ブログ記事、技術面接の準備に利用できます。

## インストール

このリポジトリを Codex plugin marketplace として追加します。

```bash
codex plugin marketplace add electrohyun/technical-decision-record --ref main
```

次に plugin をインストールします。

```bash
codex plugin add technical-decision-record@technical-decision-record
```

Codex を再起動し、Skill が利用可能か確認します。

```txt
/skills
```

次の Skill が表示されれば完了です。

```txt
technical-decision-record
```

## ローカルインストール

このリポジトリをローカルに clone している場合は、ローカルの marketplace として追加できます。

```bash
codex plugin marketplace add /path/to/technical-decision-record
```

その後、plugin をインストールします。

```bash
codex plugin add technical-decision-record@technical-decision-record
```

## 更新

リポジトリの最新変更を取得し、必要に応じて plugin を再インストールします。

```bash
git pull
codex plugin remove technical-decision-record
codex plugin add technical-decision-record@technical-decision-record
```

## Plugin 構成

```txt
technical-decision-record/
├─ .codex-plugin/
│  └─ plugin.json
├─ .agents/
│  └─ plugins/
│     └─ marketplace.json
├─ skills/
│  └─ technical-decision-record/
│     └─ SKILL.md
├─ README.md
├─ README.ko.md
├─ README.ja.md
└─ README.zh-CN.md
```

## 使い方

技術的な意思決定を記録したいときに、Codex で Skill を明示的に呼び出します。

```txt
$technical-decision-record

今回の #45 issue では、サーバー側のデータ取得構造は大きく変更せず、
まずサウンドとモーダルのコードを lazy loading する方針にします。

画像の priority/sizes は、実際の LCP element を確認したうえで、
重要な画像にのみ適用します。

改善結果は Lighthouse Mobile Navigation の LCP breakdown と
unused JavaScript の項目で確認します。

この方針で技術的な意思決定ドキュメントを作成してください。
```

## 出力例

```md
## Decision summary

`/lobby` の初期レンダリング性能を改善するため、今回の issue ではサーバー側のデータ取得構造を大きく変更せず、サウンドとモーダルコードを lazy loading する方針に決定した。

画像の `priority` と `sizes` は、実際の LCP element を確認したうえで重要な画像にのみ適用する。

## Problem

`/lobby` の初期レンダリングでは、client bundle、画像読み込みの優先度、モーダルコードの読み込みタイミングが性能低下の候補として確認された。

## Chosen solution

- サウンド関連コードを初期 bundle から分離する。
- モーダル内部のコードは、実際にモーダルが開かれるタイミングで読み込む。
- 画像の `priority` と `sizes` は、実際の LCP element を確認したうえで適用する。
- サーバー側のデータ取得構造は、今回の issue では大きく変更しない。

## Trade-offs accepted

初期レンダリングのコストは削減できるが、ユーザーが初めてモーダルやサウンド機能を使うときに、わずかな遅延が発生する可能性がある。

## Evidence

変更前後の Lighthouse Mobile Navigation の結果を比較する。

特に次の項目を確認する。

- LCP breakdown
- unused JavaScript
- actual LCP element
- client bundle changes
```

## いつ使うべきか

次のような場面で使えます。

- ライブラリやフレームワークを選ぶとき
- アーキテクチャを変更するとき
- 意味のある実装判断を含むバグ修正を行うとき
- リファクタリングを行うとき
- Issue や PR のスコープを定義するとき
- 実装方針を決めるとき
- PR や Issue の説明を準備するとき
- 振り返り、ポートフォリオ、ブログ記事、技術面接の回答を準備するとき

## Notes

この Skill は、すべての小さなコード変更を記録するためのものではありません。

代替案、trade-off、制約、測定可能な結果など、意味のある判断理由がある決定を記録するときに最も役立ちます。
