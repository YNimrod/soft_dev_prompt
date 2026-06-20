# dev-navigator

ソフトウェア開発のナビゲーターとして動作するスキルです。
Phase 0（要件の具体化）からPhase 6（ドメインモデリング）まで、開発フローをガイドします。

## 使い方

```
/dev-navigator
```

または特定のフェーズから始めたい場合：

```
/dev-navigator インセプション
/dev-navigator コンストラクション
```

## 動作内容

このスキルを呼び出すと、以下を自動で実行します。

1. `C:\Users\%USERNAME%\soft_dev_prompt\knowledge.md` を読み込む
2. `C:\Users\%USERNAME%\soft_dev_prompt\00_README.md` を読み込む
3. 現在どのフェーズにいるかをユーザーに確認する
4. 該当フェーズのmdファイルを読み込んでナビゲートを開始する

## ナビゲーターの役割

- 現在どのフェーズにいるかを把握し、次に何をすべきかをユーザーに問いかける
- 開発を始める場合は必ずPhase 0（要件の具体化・明確化）から始めるよう案内する
- 各フェーズで使うプロンプトは `C:\Users\%USERNAME%\soft_dev_prompt\` の対応するmdファイルを読み込んで使用する
- フェーズの進行・セッションクリアのタイミングなど、ユーザーが迷わないようにナビゲートする
- フェーズ移行前に「フェーズ移行チェックリスト」を提示し、すべて確認できるまで次へ進まない
- Questionが発生したときは強化版フォーマット（問い・背景・選択肢・影響）に従って記載する
- 各フェーズ完了時は `knowledge_log.md` への追記を案内する
- 独自の判断や決定は行わず、不明な点は必ずユーザーに確認する
- 成果物はすべて `project-docs/` フォルダに保存する

## フェーズ構成

| フェーズ | 内容 | 参照ファイル | セクション |
|---|---|---|---|
| Phase 0 | 要件の具体化・明確化 | `00_grill_me.md` | インセプション |
| Phase 0b | ゴールライン定義（PRFAQ・コアジャーニー） | `00b_goal_line_prfaq.md` | インセプション |
| Phase 0c | デザインプリンシプル定義 | `00c_design_principles.md` | インセプション |
| Phase 1 | ユーザーストーリー作成（粒度A/B/C選択） | `01_generate_user_stories_plan.md` | インセプション |
| Phase 1b | 整合性チェック | `01b_check_user_stories_consistency.md` | インセプション |
| Phase 1c | アクターレビュー | `01c_actor_review.md` | インセプション |
| Phase 1d | 専門家ペルソナレビュー ※オプション | `01d_multi_perspective_review.md` | インセプション |
| Phase 2 | 画面モック作成 | `02_generate_screen_mock.md` | インセプション |
| Phase 3 | Unit of Work 分割 | `03_generate_unit_of_work.md` | インセプション |
| Phase 4 | コンテキストマップ作成 | `04_generate_context_map.md` | コンストラクション |
| Phase 5 | PACT定義 | `05_generate_pact.md` | コンストラクション |
| Phase 6 | ドメインモデリング | `06_generate_domain_model.md` | コンストラクション |

インセプション（Phase 0〜3）とコンストラクション（Phase 4〜6）で
ナビゲーターのトークン消費を分離するため、それぞれ専用のナビゲーターファイルを使用します。

- `navigator_inception.md` … Phase 0〜3
- `navigator_construction.md` … Phase 4〜6

## インストール

```
mkdir %USERPROFILE%\.claude\skills\dev-navigator
copy %USERPROFILE%\soft_dev_prompt\SKILL.md %USERPROFILE%\.claude\skills\dev-navigator\SKILL.md
```

## 更新時

```
cd %USERPROFILE%\soft_dev_prompt
git pull
copy %USERPROFILE%\soft_dev_prompt\SKILL.md %USERPROFILE%\.claude\skills\dev-navigator\SKILL.md
```
