# AI Dev OS Plugin — Cursor への貢献

貢献に興味を持っていただきありがとうございます！

## 貢献方法

### 問題の報告

- [GitHub Issues](https://github.com/yunbow/ai-dev-os-plugin-cursor/issues) をご利用ください
- 影響を受けるルールまたはテンプレートを明記してください

### プルリクエスト

1. リポジトリをフォークする
2. フィーチャーブランチを作成する
3. 変更を加える
4. わかりやすいメッセージでコミットする
5. プルリクエストを開く

### 貢献できる内容

| ディレクトリ | 求めている貢献 | ガイドライン |
|-----------|-------------|------------|
| `rules/` | ルールの改善、新しい .mdc ルール | .mdc フォーマット（`description`, `globs`, `alwaysApply` を含む YAML フロントマター）に従ってください。ルールは焦点を絞り簡潔にしてください。 |
| `templates/` | テンプレートの改善 | テンプレートは Two-Tier Context Strategy（10-15 個の重要なルールのみ）に従ってください。 |
| `checklist-templates/` | 新しい言語のチェックリスト、改善 | チェックリストは実行可能かつ検証可能なものにしてください。 |

### ルール開発ガイドライン

- 各ルールは `rules/{name}.mdc` に配置します
- 必須フロントマター: `description`, `globs`, `alwaysApply`
- `globs` はルールが適用されるファイルを定義します（例: `"**/*.ts"`, `"**/*.py"`）
- `alwaysApply: true` は常にアクティブであるべきルールに使用します
- ルールの内容は明確で実行可能なものにしてください
- ルールは単一の関心事に焦点を当ててください
- 可能な限り具体的な例を使用してください

### クロスプラグイン機能の同等性

このプラグインに新機能を追加する際は、以下への同等機能の追加も検討してください：

- [ai-dev-os-plugin-claude-code](https://github.com/yunbow/ai-dev-os-plugin-claude-code)（スキルまたはフックとして）
- [ai-dev-os-plugin-kiro](https://github.com/yunbow/ai-dev-os-plugin-kiro)（ステアリングルールとして）

### 翻訳ガイド

- 翻訳は `docs/i18n/{lang}/` にあります
- 現在サポートされている言語: `ja`, `zh-CN`, `ko`, `es`

## 行動規範

敬意を持ち、建設的で、包括的であること。

---

Languages: [English](../../../CONTRIBUTING.md) | 日本語
