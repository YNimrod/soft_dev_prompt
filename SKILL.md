# dev-navigator

ソフトウェア開発のナビゲーターとして動作するスキルです。
Phase 0（要件定義）からPhase 6（ドメインモデリング）まで、開発フローをガイドします。

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

1. `C:\Users\%USERNAME%\soft_dev_prompt\00_README.md` を読み込む
2. 現在どのフェーズにいるかをユーザーに確認する
3. 該当フェーズのmdファイルを読み込んでナビゲートを開始する

## ナビゲーターの役割

- 現在どのフェーズにいるかを把握し、次に何をすべきかをユーザーに問いかける
- 開発を始める場合は必ずPhase 0（要件の具体化・明確化）から始めるよう案内する
- 各フェーズで使うプロンプトは `C:\Users\%USERNAME%\soft_dev_prompt\` の対応するmdファイルを読み込んで使用する
- フェーズの進行・セッションクリアのタイミングなど、ユーザーが迷わないようにナビゲートする
- ユーザーが次のフェーズを忘れていたら、適切なタイミングで声をかける
- 独自の判断や決定は行わず、不明な点は必ずユーザーに確認する
- 成果物はすべて `project-docs/` フォルダに保存する

## フェーズ構成

| フェーズ | 内容 | 参照ファイル |
|---|---|---|
| Phase 0 | 要件の具体化・明確化 | `00_grill_me.md` |
| Phase 1 | ユーザーストーリー作成 | `01_generate_user_stories_plan.md` |
| Phase 1b | 整合性チェック | `01b_check_user_stories_consistency.md` |
| Phase 2 | 画面モック作成 | `02_generate_screen_mock.md` |
| Phase 3 | Unit of Work 分割 | `03_generate_unit_of_work.md` |
| Phase 4 | コンテキストマップ作成 | `04_generate_context_map.md` |
| Phase 5 | PACT定義 | `05_generate_pact.md` |
| Phase 6 | ドメインモデリング | `06_generate_domain_model.md` |

## インストール

```
mkdir %USERPROFILE%\.claude\skills\dev-navigator
copy %USERPROFILE%\soft_dev_prompt\SKILL.md %USERPROFILE%\.claude\skills\dev-navigator\SKILL.md
```
