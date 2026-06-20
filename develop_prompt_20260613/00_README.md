# ソフトウェア開発プロンプト集 — 使い方ガイド

## ファイル構成

| ファイル | フェーズ | 内容 |
|---|---|---|
| `00_grill_me.md` | Phase 0 | 要件の具体化・明確化 |
| `01_generate_user_stories_plan.md` | Phase 1 | ユーザーストーリー作成（粒度A/B/C選択） |
| `01b_check_user_stories_consistency.md` | Phase 1b | 整合性チェック（AC評価・粒度確認・申し送り） |
| `01c_actor_review.md` | Phase 1c | アクターレビュー |
| `01d_multi_perspective_review.md` | Phase 1d | 専門家ペルソナレビュー ※オプション・ペルソナ選択可 |
| `02_generate_screen_mock.md` | Phase 2 | 画面モック作成 |
| `03_generate_unit_of_work.md` | Phase 3 | Unit of Work 分割 |
| `04_generate_context_map.md` | Phase 4 | コンテキストマップ作成 |
| `05_generate_pact.md` | Phase 5 | PACT（契約テスト）定義 |
| `06_generate_domain_model.md` | Phase 6 | ドメインモデリング |

---

## 全体フロー と 中間成果物マップ

```
Phase 0  ──→ inception/system_overview.md          ★Phase1への引き継ぎ要件
         ──→ knowledge_log.md（追記）               ★ナレッジ記録
              ↓  [コンテキストクリア]
Phase 1  ──→ inception/user_stories_plan.md
         ──→ inception/user_stories.md          ★粒度A/B/Cをユーザーが選択して生成
         ──→ knowledge_log.md（追記）               ★ナレッジ記録
              ↓  [同一セッションで継続]
Phase 1b ──→ inception/user_stories.md（整合性修正済）
         ──→ inception/consistency_check.md         ★整合性確認レポート（問題なし時も保存）
         ──→ inception/phase1b_handover.md           ★後工程への申し送り事項
         ──→ knowledge_log.md（追記）               ★ナレッジ記録
              ↓  [同一セッションで継続]
Phase 1c ──→ inception/actor_review.md               ★アクターレビュー
         ──→ inception/user_stories.md（修正があれば更新）
         ──→ knowledge_log.md（追記）               ★ナレッジ記録
              ↓  [全Questionへの回答が揃ってからクリア]
Phase 1d ──→ inception/multi_perspective_review.md   ★専門家ペルソナレビュー（オプション・スキップ可）
         ──→ inception/user_stories.md（修正があれば更新）
         ──→ knowledge_log.md（追記）               ★ナレッジ記録
              ↓  [セッションクリア前にナビゲーターが inception_summary.md を生成]
         ──→ inception/inception_summary.md          ★Phase 2 への引き継ぎサマリー
              ↓  [コンテキストクリア]
Phase 2  ──→ inception/screen_flow.md（[F] 選択時のみ）  ★フローチャート＋未決事項一覧
         ──→ inception/screen_mock.html
         ──→ knowledge_log.md（追記）               ★ナレッジ記録
              ↓  [コンテキストクリア]
Phase 3  ※参照: user_stories.md / inception_summary.md / actor_review.md / screen_flow.md（存在する場合）
         ──→ inception/units/units_plan.md
         ──→ knowledge_log.md（追記）               ★ナレッジ記録
         ──→ inception/units/unit_XX_<名前>.md  × N本（冒頭にユニット概要・目的・境界の根拠を含む）
         ──→ inception/units/if_precheck.md        ★I/F事前確認レポート（確定済み・未解決を明記）
              ↓  [全Questionへの回答が揃ってからクリア]
Phase 4  ──→ inception/context_map.md（コンテキストマップ＋連携一覧テーブル＋シーケンス図）
         ──→ knowledge_log.md（追記）               ★ナレッジ記録
         ──→ inception/if_precheck_p4.md            ★I/F事前確認レポート（確定済み・未解決を明記）
              ↓  [全Questionへの回答が揃ってからクリア]
Phase 5  ──→ inception/pacts/pact_<consumer>_<provider>.md  × N本（I/F確認チェックリスト含む）
         ──→ knowledge_log.md（追記）               ★ナレッジ記録
         ──→ inception/pacts/pact_index.md（未解決Question欄付き）
              ↓  [未解決Questionがゼロになってからクリア]
Phase 6  ※参照: unit_XX.md / pact_index.md / pact_xxx.md（全関連PACT）/ context_map.md / if_precheck.md
         ──→ construction/<ユニット名>/domain_model_plan.md（I/F確認セクション含む）
         ──→ knowledge_log.md（追記）               ★ナレッジ記録
         ──→ construction/<ユニット名>/docs/<コンポーネント名>.md  × N本
              （ユニット数分を繰り返し）
```

---

## 前のフェーズへ戻る方法

各フェーズの成果物ファイルが手元にあれば、任意のフェーズから再開できます。

| 戻りたいフェーズ | 必要な成果物 |
|---|---|
| Phase 0 | （会話の冒頭からやり直し） |
| Phase 1 の途中 | `user_stories_plan.md`（チェック状態）+ `user_stories.md`（途中版） |
| Phase 1b | `user_stories.md`（Phase 1 完成版） |
| Phase 1c | `user_stories.md` + `consistency_check.md` + `phase1b_handover.md`（Phase 1b 完成版） |
| Phase 1d | `user_stories.md` + `actor_review.md`（Phase 1c 完成版） |
| Phase 2 | `inception_summary.md`（ナビゲーターが生成）|
| Phase 3 | `user_stories.md` + `units_plan.md`（チェック状態）+ 完成済み `unit_XX.md` |
| Phase 4 | `unit_XX.md` 群 + `if_precheck.md`（Phase 3 完成版） |
| Phase 5 | `context_map.md` + `if_precheck_p4.md` + `unit_XX.md` 群（Phase 4 完成版） |
| Phase 6 の途中 | `unit_XX.md`（対象ユニット）+ `domain_model_plan.md`（チェック状態）+ 完成済み `docs/*.md` |

> **再開手順:** 新しいチャットを開き、対応するフェーズのプロンプトと上記ファイルの内容を貼り付けて開始してください。

---

## セッションクリアのタイミング

各フェーズの中間成果物をすべてファイルに保存した後、Claude Codeのセッションを
新しく開始してから次フェーズのプロンプトを使用してください。
これにより前フェーズの文脈による混乱を防ぎます。

---

## AIへの歯止めルール（全フェーズ共通）

各フェーズのプロンプトに組み込まれている歯止めルールの一覧です。

| # | ルール | 目的 |
|---|---|---|
| 1 | **計画作成後は必ず停止・承認待ち** | 意図しない先行実行を防ぐ |
| 2 | **1ステップ（1ユニット／1コンポーネント）完了ごとに停止・レビュー待ち** | 細かい単位でのレビューを保証する |
| 3 | **Questionが1件でも発生したら即停止・Answer待ち** | 不明点を曖昧なまま進めさせない |
| 4 | **フェーズのスコープ外の成果物を生成しない** | 余計な先読み・過剰設計を防ぐ |
| 5 | **ファイル保存後は完了報告して停止・次の指示待ち** | 保存完了を確認してから次へ進む |
| 6 | **コード・アーキテクチャ設計は該当フェーズ以外では生成しない** | フェーズをまたいだオーバーワークを防ぐ |

---

## 整合性確認（自己チェック）の仕組み

各フェーズのプロンプトには、レビュー依頼の前にAIが必ず実施する「整合性確認」が組み込まれています。
AIは確認結果を「整合性確認レポート」として提示し、問題があれば自己修正してからレビューを求めます。

| フェーズ | 確認タイミング | 主な確認内容 |
|---|---|---|
| Phase 1（計画） | 計画作成後・承認前 | ステップ順序の依存矛盾、Questionの抜け漏れ、タスク内容の反映 |
| Phase 1（各ステップ） | ステップ完了後・レビュー前 | タスクとの対応、前ステップとの矛盾、未回答Questionの残存 |
| Phase 1b | 修正案提示前 | 用語統一、ストーリー間の重複・矛盾、AC品質（明確性・完全性・粒度）、修正の波及影響 |
| Phase 1c | アクターごとのレビュー前 | 行動の自然さ・目的との対応・抜け漏れ |
| Phase 1d | ペルソナごとのレビュー前（選択時のみ） | PM/UX/ARCH/LEGAL/MKT 各視点の懸念 |
| Phase 2（STEP 1a） | フローチャート完成後・提示前 | 全ストーリー・全アクター・主要異常系・inception_summary.md の引き継ぎ事項の網羅性確認 |
| Phase 2（STEP 1b） | 未決事項一覧提示後・判断前 | フローチャート上の未決事項を「今決める／仮決め／後回し可」でユーザーが判断 |
| Phase 2（STEP 2） | モック完成後・保存前 | 全ストーリーの画面対応・アクター別画面・screen_flow.md との整合・inception_summary.md 引き継ぎの反映 |
| Phase 3（STEP 0） | 作業開始前 | 前工程成果物（inception_summary / actor_review / screen_flow）の影響項目を抽出しユーザーが判断 |
| Phase 3（計画） | 計画作成後・承認前 | 全ストーリーのユニット割り当て漏れ・重複、境界の妥当性 |
| Phase 3（各ユニット概要） | 概要作成後・承認前 | 目的・責務・境界の根拠がストーリー群と整合しているか |
| Phase 3（各ユニット完了） | ユニット定義後・レビュー前 | 凝集性、受け入れ基準との対応、ユニット間の概念矛盾 |
| Phase 3（I/F事前確認） | 全ユニット完了後 | 連携データ・種別・トリガー・エラー振る舞い・境界妥当性を一覧提示しユーザーが判断 |
| Phase 4（STEP 1） | コンテキストマップ完成後・承認前 | 全ユニットの登場・依存方向・連携一覧テーブルと if_precheck.md の整合・循環依存・PACT定義間の依存関係（パターンA/B/C）の識別 |
| Phase 4（STEP 2） | シーケンス図完成後・承認前 | メッセージ方向・unit_XX.md との整合・異常系の扱い方針の明示 |
| Phase 4（STEP 3） | I/F事前確認後 | 連携網羅性・例外系の扱い方針・順序制約を一覧提示しユーザーが判断 |
| Phase 5（計画） | 計画作成後・承認前 | 連携一覧テーブルの全連携を網羅・着手順序の提案（未解決事項を後回し・共有ユニット連続着手） |
| Phase 5（STEP A） | I/F確認提示後・承認前 | 契約の対象・フィールド仕様・異常系振る舞い・非機能要件の確定済み/未確定を一覧提示 |
| Phase 5（STEP B） | PACT定義後・レビュー前 | Consumer/Provider方向・AC充足・主な責務の範囲内・if_precheck整合・用語統一 |
| Phase 6（STEP A） | I/F確認後・承認前 | PACTとの接続点・ACL要否・ドメインモデル独立性を確定済み/未確定の一覧で提示しユーザーが判断 |
| Phase 6（STEP B） | 計画作成後・承認前 | 全ストーリーカバレッジ・主な責務の範囲内・ACLコンポーネントの明示 |
| Phase 6（STEP C） | コンポーネント定義後・レビュー前 | AC充足・主な責務の範囲内・ACL変換ロジックの明示・アーキテクチャ混入の排除 |

---

## I/F手戻り防止の仕組み

Phase 3〜6 にわたって「I/F事前確認」の問いが連鎖的に引き継がれます。
各フェーズで未解決の問いが残っている場合は次フェーズへ進まないことがルールです。

```
Phase 3: if_precheck.md
  └─ ユニット間のデータ受け渡し・連携種別・トリガー・エラー振る舞い・境界の妥当性
       ↓ 引き継ぎ
Phase 4: if_precheck_p4.md
  └─ 連携網羅性・例外系の可視化・順序制約・循環依存
       ↓ 引き継ぎ
Phase 5: pact_<x>_<y>.md（各連携）
  └─ 影響ストーリー・フィールド仕様・異常系・べき等性・バージョニング
       ↓ 引き継ぎ
Phase 6: domain_model_plan.md（各ユニット）
  └─ PACTとの接続点・概念変換の担当・ドメインモデルの独立性
```

| フェーズ | 生成する引き継ぎ文書 | 次フェーズへの主な引き継ぎ情報 |
|---|---|---|
| Phase 3 | `if_precheck.md` | データ受け渡し一覧・概念の異名・連携種別 |
| Phase 4 | `if_precheck_p4.md` | 例外系の扱い方針・順序制約・連携の網羅確認 |
| Phase 5 | `pact_index.md`（未解決Question欄） | 未合意の非機能要件・バージョニング方針 |
| Phase 6 | `domain_model_plan.md`（チェックリスト） | PACTとの接続コンポーネント・変換ロジックの所在 |

---

## 統合の経緯（強化ポイントまとめ）

### ① Phase 0: 要件の具体化・明確化（新設）

Phase 1（ユーザーストーリー作成）の前に実施。ユーザーが思いつくままに話した内容をAIが
整理・質問し、共通認識に達するまで要件を固めます。固まった内容は `system_overview.md` として
Phase 1 に引き継がれます。

### ② Phase 1c: アクターレビュー（新設）

Phase 1b の整合性チェック後に実施。Phase 1 ST2 で定義したアクター自身の視点で
「行動の自然さ・目的との対応・抜け漏れ」の3観点でストーリーを評価します。

### ③ Phase 1d: 専門家ペルソナレビュー（旧 1c・オプション化）

Phase 1c のアクターレビュー後に実施（スキップ可）。
**PM・ユーザー代表・技術アーキテクト・法務・マーケター**の5ペルソナから使用するものを選択できます。
外部レビューが不要な場合はフェーズ全体をスキップして Phase 2 へ進めます。

### ④ 強化版 [Question] フォーマット（全フェーズ共通）

従来の「問いを出すだけ」から、**背景・選択肢・影響範囲**を必ず明示する形式に変更。
回答者が判断しやすくなり、未決定事項の管理精度が向上します。

```
[Question 番号]
・問い   : 何を決める必要があるか（一文で）
・背景   : なぜこれが未決定なのか、なぜ問題になりうるか
・選択肢 : A案 / B案 /（不明な場合は「要調査」）
・影響   : 未決定のままだと〇〇フェーズの〇〇が進められない
[Answer 番号]
```

### ⑤ ナレッジログ（knowledge_log.md）の記録（全フェーズ共通）

各フェーズ完了時に `knowledge_log.md` への追記を義務化。
セッションをまたいで知見が蓄積され、**類似プロジェクトへの転用・手戻り防止パターンの共有**が可能になります。

| フェーズ | 追記内容の例 |
|---|---|
| Phase 0 | 要件定義で漏れやすかった観点・確認パターン |
| Phase 1 | 要件整理フレームワーク・優先度判断の根拠 |
| Phase 1b | 発見した整合性パターン・表記ゆれの傾向 |
| Phase 1c | アクター行動フローの抜け漏れパターン・目的とのズレの傾向 |
| Phase 1d | 法務・技術・マーケの観点で発見したリスクパターン（実施した場合） |
| Phase 2 | 画面構成パターン・UX上の発見 |
| Phase 3 | ユニット分割の判断根拠・境界設計パターン |
| Phase 4 | 連携依存方向の判断根拠・循環依存の解消パターン |
| Phase 5 | 異常系設計パターン・べき等性の判断基準 |
| Phase 6 | コンポーネント責務分割パターン・ACL要否の判断基準 |

---

## Claude Code での運用

このプロンプト集はすべて Claude Code 上での利用を前提としています。
Claude Chat は GitHub 上の生ファイル（RAW URL）を直接取得できないため、
ローカルファイルを直接読み書きできる Claude Code に統一しています。

### 初回セットアップ

```
git clone https://github.com/YNimrod/soft_dev_prompt.git %USERPROFILE%\soft_dev_prompt
mkdir %USERPROFILE%\.claude\skills\dev-navigator
copy %USERPROFILE%\soft_dev_prompt\SKILL.md %USERPROFILE%\.claude\skills\dev-navigator\SKILL.md
```

### 起動方法

プロジェクトフォルダで Claude Code を起動し、以下のいずれかを使用します。

| 用途 | 方法 |
|---|---|
| スキル経由（推奨） | `/dev-navigator` |
| インセプションフェーズのみ | `navigator_inception.md` のプロンプトを入力 |
| コンストラクションフェーズのみ | `navigator_construction.md` のプロンプトを入力 |

### 更新時

```
cd %USERPROFILE%\soft_dev_prompt
git pull
copy %USERPROFILE%\soft_dev_prompt\SKILL.md %USERPROFILE%\.claude\skills\dev-navigator\SKILL.md
```

### 共通変数一覧

| 変数 | 説明 | 例 |
|---|---|---|
| `{{言語}}` | 出力言語 | 日本語 |
| `{{ドキュメントルート}}` | ドキュメントの保存先ルートパス | `project-docs` |
| `{{構築したいシステムの概要}}` | プロジェクトの説明（Phase 0 の成果物から引き継ぐ） | 「SRSをもとにテスト仕様書を生成するエージェントを構築したい」 |
| `{{対象ユニットのmdファイル名}}` | Phase 6 で参照するユニットファイル名 | `unit_01_browsing.md` |
| `<ユニット名>` | Phase 6 の出力先フォルダ名 | `unit_01_browsing` |
