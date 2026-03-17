# AI Dev OS Plugin for Cursor — 運用ガイド

[English](../../operation-guide.md) | 日本語 | [简体中文](../zh-CN/operation-guide.md) | [한국어](../ko/operation-guide.md) | [Español](../es/operation-guide.md)

## 前提条件

- [Cursor](https://cursor.sh/) （AI機能が有効であること）
- プロジェクトに AI Dev OS のレイヤーファイル（L1-L3）がセットアップ済みであること（ルール: [TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python)）

## インストール

### 方法A: 直接コピー

```bash
git clone https://github.com/yunbow/ai-dev-os-plugin-cursor.git
cp -r ai-dev-os-plugin-cursor/rules/ .cursor/rules/
cp -r ai-dev-os-plugin-cursor/checklist-templates/ .cursor/checklist-templates/
```

### 方法B: Git Submodule

```bash
git submodule add https://github.com/yunbow/ai-dev-os-plugin-cursor.git .cursor/plugins/ai-dev-os
```

ルールをコピーまたはシンボリックリンク:
```bash
cp -r .cursor/plugins/ai-dev-os/rules/ .cursor/rules/
```

## 初期セットアップ

1. Cursor チャットで `@ai-dev-os-init` を実行
2. ウィザードに従って技術スタックを設定
3. 生成されたディレクトリ構成を確認

## 日常のワークフロー

### 4.1 実装前の計画

コーディングを始める前に、`@ai-dev-os-plan` を使用してガイドラインを考慮した実装計画を作成します。

### 4.2 チケットの作成

`@ai-dev-os-ticket` を使用して、コンプライアンスチェックリスト付きの構造化されたチケットを生成します。

### 4.3 コーディング

ファイルスコープルール（`guideline-compliance`、`layer-dependency`）は、マッチするファイルを編集すると自動的に起動し、リアルタイムでガイダンスを提供します。

### 4.4 コミット前

`@ai-dev-os-check` を実行して、すべての変更がガイドラインに準拠していることを確認します。

プロジェクト全体のスキャンが必要な場合は `@ai-dev-os-scan` を使用して、全ソースファイルの準拠状況を確認できます。

PR を作成する前に `@ai-dev-os-review` を実行して、L3 準拠チェック・L2 設計レビュー・L1 整合性確認を統合したセルフレビューを行います。

### 4.5 コードレビュー後

`@ai-dev-os-extract` を実行して、レビューのフィードバックから新しいルールを抽出します。

### 4.6 ルールの理解

`@ai-dev-os-why` を使用して、任意のルールをその哲学的起源まで遡ってトレースします。

## 定期メンテナンス

| 頻度 | アクション | 説明 |
|------|-----------|------|
| 月次 | `@ai-dev-os-audit` | 4層の健全性チェック |
| 四半期 | `@ai-dev-os-evolve` | SECI スパイラルフィードバック |
| 週次/月次 | `@ai-dev-os-report` | コンプライアンスレポート |

## チームオンボーディング

1. 新メンバーがプロジェクトをクローン
2. `.cursor/rules/` 内のルールが自動的に利用可能になる
3. 主要なルールに対して `@ai-dev-os-why` を実行し、根拠を理解することを推奨
4. 基盤となる価値観を理解するために `ai-dev-os/01_philosophy/` を読むことを推奨

## トラブルシューティング

### ルールが有効にならない
- `.cursor/rules/` ディレクトリに `.mdc` ファイルが存在するか確認
- Cursor の AI 機能が有効か確認
- ルール追加後は Cursor を再起動

### guideline-compliance の誤検知
- 明確な違反のみフラグするルールです
- 継続的な誤検知は `ai-dev-os/03_guidelines/` の該当ガイドラインを調整してください

### パフォーマンス
- ファイルスコープルールはマッチするファイルパターンでのみ起動します
- 手動ルールは明示的に @メンション された場合のみ起動します

---

Languages: [English](../../operation-guide.md) | 日本語 | [简体中文](../zh-CN/operation-guide.md) | [한국어](../ko/operation-guide.md) | [Español](../es/operation-guide.md)
