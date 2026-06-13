# ソフトウェア開発プロンプト集 — 使い方ガイド

## ファイル構成

| ファイル | フェーズ | 内容 |
|---|---|---|
| `00_grill_me.md` | Phase 0 | 要件の具体化・明確化 |
| `01_generate_user_stories_plan.md` | Phase 1 | ユーザーストーリー作成 |
| `01b_check_user_stories_consistency.md` | Phase 1b | ユーザーストーリー整合性チェック |
| `02_generate_screen_mock.md` | Phase 2 | 画面モック作成 |
| `03_generate_unit_of_work.md` | Phase 3 | Unit of Work 分割 |
| `04_generate_context_map.md` | Phase 4 | コンテキストマップ作成 |
| `05_generate_pact.md` | Phase 5 | PACT（契約テスト）定義 |
| `06_generate_domain_model.md` | Phase 6 | ドメインモデリング |

---

## 全体フロー

```
Phase 0  → [コンテキストクリア]
         ↓
Phase 1  → Phase 1b → [コンテキストクリア]
         ↓
Phase 2  → [コンテキストクリア]
         ↓
Phase 3  → [コンテキストクリア]
         ↓
Phase 4  → [コンテキストクリア]
         ↓
Phase 5  → [コンテキストクリア]
         ↓
Phase 6  （ユニット数分を繰り返し）
```

> **コンテキストクリアのタイミング**  
> 各フェーズの成果物をファイルに保存した後、Claude Codeのセッションを新しく開始してから次フェーズのプロンプトを使用してください。  
> これにより、前フェーズの文脈による混乱を防ぎます。ローカルファイルへの成果物の保存は必ず行ってからセッションを切ってください。

> **Phase 0 について**
> Phase 0 ではシステムの要件を徹底的に具体化・明確化します。このフェーズで固まった内容を `{{構築したいシステムの概要}}` として Phase 1 に引き継いでください。

> **Phase 1 の成果物について**  
> Phase 1 では2つのファイルが生成されます。
> - `user_stories_plan.md` … ユーザーストーリーを作成するための作業計画
> - `user_stories.md` … 計画に沿って実際に作成されたユーザーストーリーの成果物  
>
> Phase 2 以降が参照するのは `user_stories.md` です。Phase 1 完了後に必ず保存してください。

---

## 初回セットアップ

このリポジトリをホームディレクトリにcloneしてください。

```
git clone https://github.com/YNimrod/soft_dev_prompt.git
```

clone後のパス: `C:\Users\%USERNAME%\soft_dev_prompt\`

---

## ナビゲーターの使い方

すべての作業はClaude Codeで行います。プロジェクトのフォルダでClaude Codeを起動し、以下のナビゲーターのプロンプトを入力してください。

| ファイル | 対象フェーズ | 用途 |
|---|---|---|
| `navigator_inception.md` | Phase 0〜3 | 要件定義・設計フェーズ |
| `navigator_construction.md` | Phase 4〜6 | 実装フェーズ |
| `navigator_prompt.md` | Phase 0〜6 | 全フェーズを通しで進める場合 |

Claude Codeがローカルの `soft_dev_prompt\` フォルダのmdファイルを直接読み込んで進めます。

---

## プロンプト更新時

GitHubでmdファイルを更新したら、以下でローカルに反映してください。

```
git pull
```

---

## 共通変数一覧

| 変数 | 説明 | 例 |
|---|---|---|
| `{{言語}}` | 出力言語 | 日本語 |
| `{{ドキュメントルート}}` | ドキュメントの保存先ルートパス | `project-docs` |
| `{{構築したいシステムの概要}}` | プロジェクトの説明（背景・目的を含めると質問が減る） | 「SRSをもとにテスト仕様書を生成するエージェントを構築したい」 |
| `{{対象ユニットのmdファイル名}}` | Phase 6 で参照するユニットファイル名 | `unit_01_browsing.md` |
| `<ユニット名>` | Phase 6 の出力先フォルダ名 | `unit_01_browsing` |
