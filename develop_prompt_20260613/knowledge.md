# ナレッジベース

このファイルはこのプロンプト集の運用で得た知見をまとめたものです。
ナビゲーターは起動時に自動で読み込みます。新しい知見が生まれたら追記してください。

---

## このプロンプト集の特徴・前提

### 元になったプロンプトとの違い
このプロンプト集は基本プロンプトをベースに、
以下の3点を独自に強化しています。

| 強化ポイント | 内容 |
|---|---|
| 中間成果物の保存 | 各ステップ完了ごとに必ずファイル保存。どのフェーズからでも再開可能 |
| アクターレビュー（Phase 1c） | Phase 1 で定義したアクター視点で行動の自然さ・目的・抜け漏れを確認 |
| 専門家ペルソナレビュー（Phase 1d） | PM・UX・技術・法務・マーケターから使うペルソナを選択可。スキップも可 |
| I/F手戻り防止 | Phase 3〜6 にわたる `if_precheck.md` 連鎖で設計上の合意を事前形成 |
| 強化版 Question フォーマット | 問い・背景・選択肢・影響を必ず明示 |
| ナレッジログ | 各フェーズ完了時に `knowledge_log.md` へ再利用可能な知見を蓄積 |

---

## Claude の制限・特性（運用上の注意）

### Web取得の制限
- `raw.githubusercontent.com` のURLはClaudeのWeb fetchで取得不可
- GitHub PagesのURLも個人リポジトリは検索インデックスに載らないため取得不可
- **解決策**：ローカルファイルを使うClaude Codeで対応する（このプロンプト集はその前提で設計済み）

### Claude ChatとClaude Codeの使い分け
| | Claude Chat | Claude Code |
|---|---|---|
| ファイルアクセス | 不可 | ローカルファイルを直接読み書き可能 |
| Git操作 | 不可 | 可能 |
| 用途 | 会話・相談 | 開発作業全般 |

→ **ファイルを参照しながら開発する作業はすべてClaude Codeで行う**

### Claude Codeでのファイル参照
- `%USERNAME%` はClaude Codeのシェルで正常に展開される（動作確認済み）
- ホームディレクトリ（`C:\Users\%USERNAME%\`）にリポジトリを固定することでパスをナビゲーターに埋め込める

### トークン効率の設計原則
- フェーズごと・セッションごとにコンテキストをクリアして不要な文脈を持ち越さない
- ナビゲーターを用途別（インセプション／コンストラクション）に分割して1セッションの読み込み量を最小化
- 不要なファイルを読み込ませない（必要なフェーズのmdファイルだけを参照する）

### AIへの効果的な指示のコツ
- 「あなた自身でレビューしてください」という指示で、AIが見落としを自己発見できる
- 複数のファイルにまたがる場合は「全ファイルの整合性を確認してください」と明示的に指示する
- プロンプトを一度生成してそのまま使うのではなく、必ずレビューと修正を繰り返す

### Claude Codeの使用量確認

```
/usage    # 現在のセッションのトークン消費量と推定コストを表示
/context  # コンテキストウィンドウの占有状況を確認
```

- claude.ai・Claude Code・Claude Desktopの使用量はすべて同じ制限にカウントされる
- 制限に近づくとメッセージ入力欄付近に警告が表示される

### Git運用

```
# 初回セットアップ
git clone https://github.com/YNimrod/soft_dev_prompt.git %USERPROFILE%\soft_dev_prompt

# 更新時
cd %USERPROFILE%\soft_dev_prompt
git pull

# スキル更新時
copy %USERPROFILE%\soft_dev_prompt\SKILL.md %USERPROFILE%\.claude\skills\dev-navigator\SKILL.md
```

---

## フェーズの流れと成果物の全体像

```
Inception フェーズ
  Phase 0  → system_overview.md / knowledge_log.md
           ↓  [セッションクリア]
  Phase 1  → user_stories_plan.md / user_stories.md / knowledge_log.md
  Phase 1b → user_stories.md（整合性修正済）/ consistency_check.md / phase1b_handover.md / knowledge_log.md
  Phase 1c → actor_review.md / user_stories.md（修正あれば）/ knowledge_log.md
  Phase 1d → multi_perspective_review.md / user_stories.md（修正あれば）/ knowledge_log.md  ※オプション
           → inception_summary.md（セッションクリア前にナビゲーターが生成）
  Phase 2  → screen_mock.html / knowledge_log.md
  Phase 3  → units_plan.md
           → unit_XX_<名前>.md × N（冒頭にユニット概要・目的・境界の根拠を含む）
           → if_precheck.md（確定済み・未解決を明記）/ knowledge_log.md

Construction フェーズ
  Phase 4  → context_map.md（コンテキストマップ＋連携一覧テーブル＋シーケンス図）/ if_precheck_p4.md（確定済み・未解決明記）/ knowledge_log.md
  Phase 5  → pact_<consumer>_<provider>.md × N / pact_index.md / knowledge_log.md
  Phase 6  → domain_model_plan.md（I/F確認セクション含む）/ docs/<コンポーネント名>.md × N / knowledge_log.md
             （ユニット数分繰り返し）
```

---

## セッションクリアのルール

### クリアするタイミング
- **Phase 0 完了後**（要件確定後、Phase 1 開始前）
- **Phase 1b 完了後**（Phase 1c 開始前）
- **Phase 1c 完了後 かつ 全 Question 回答済み後**（Phase 1d 開始前）
- **Phase 1d 完了後**（スキップした場合も含む）セッションクリア前にナビゲーターが inception_summary.md を生成する（Phase 2 開始前）
- **Phase 2 完了後**（Phase 3 開始前）
- **Phase 3 完了後 かつ if_precheck.md の全 Question 回答済み後**
- **Phase 4 完了後 かつ if_precheck_p4.md の全 Question 回答済み後**
- **Phase 5 完了後 かつ pact_index.md の未解決 Question がゼロになった後**
- **Phase 6 の各ユニット完了後**（次のユニット開始前）

### ⚠️ クリアしてはいけないタイミング
- Phase 1・Phase 1b・Phase 1c は**同じセッション**で続けて実施する
- Phase 1d はオプション。スキップ可能だが、実施する場合は Phase 1c と別セッションでも可
- Question への回答がまだ揃っていない状態でクリアしない

---

## AIへの効果的な指示

### 歯止めルール（全フェーズ共通）
各フェーズのプロンプトに以下の歯止めが組み込まれています。

| ルール | 目的 |
|---|---|
| 計画作成後は停止・承認待ち | 意図しない先行実行を防ぐ |
| 1ステップ完了ごとに停止・レビュー待ち | 細かい単位でのレビューを保証 |
| Question 発生時点で即停止・Answer 待ち | 不明点を曖昧なまま進めさせない |
| フェーズスコープ外の生成禁止 | 余計な先読み・過剰設計を防ぐ |
| ファイル保存後は停止・次の指示待ち | 保存完了を確認してから次へ |

### Question フォーマット（強化版）
このプロンプト集では以下の形式で Question を記載します。

```
[Question 番号]
・問い   : 何を決める必要があるか（一文で）
・背景   : なぜこれが未決定なのか、なぜ問題になりうるか
・選択肢 : A案 / B案 /（不明な場合は「要調査」）
・影響   : 未決定のままだと〇〇フェーズの〇〇が進められない
[Answer 番号]
```

### 整合性確認レポート
各フェーズでレビューを依頼する前に AI が自己チェックを行い、
「整合性確認レポート」として結果を提示します。
問題があれば自動で修正してからレビューを求めます。

---

## I/F 手戻り防止の連鎖

Phase 3〜6 にわたって事前確認の問いが連鎖します。
未解決の Question が残っている限り次フェーズへ進みません。

```
Phase 3 → if_precheck.md
  「何を・どの形式で・誰から誰へ渡すか」「概念の異名」「エラー振る舞い」

Phase 4 → if_precheck_p4.md
  「例外系の扱い方針」「順序制約」「循環依存」

Phase 5 → pact_index.md（未解決 Question 欄）
  「フィールド仕様」「異常系 3 種」「べき等性」「バージョニング」

Phase 6 → domain_model_plan.md（I/F 確認チェックリスト）
  「PACT 接続コンポーネント」「概念変換の担当」「独立性確認」
```

---

## ナレッジログについて

各フェーズ完了時に `{{ドキュメントルート}}/knowledge_log.md` へ知見を追記します。
蓄積される内容の例：

- ユニット分割の判断根拠
- 境界設計で迷った場合のパターン
- 法務・技術観点で発見したリスクパターン
- PACT 設計での異常系パターン
- Anti-Corruption Layer が必要になった条件

---

## 更新履歴

| 日付 | 内容 |
|---|---|
| 2026-06-13 | 初版作成（Claude Code運用ノウハウ：GitHub取得制限・トークン効率・%USERNAME%動作確認） |
| 2026-06-15 | プロンプト内容の大幅強化（ワークショップ基本プロンプト + 別チャット成果物の統合） |
| 2026-06-17 | Phase 1 粒度選択（A/B/C）・Phase 1b 大幅拡充・Phase 1c アクターレビュー新設・Phase 1d（旧1c）オプション化 |
| 2026-06-19 | Phase 0（要件の具体化・明確化）を追加し、Claude Code運用ノウハウとプロンプト内容強化版を統合 |
