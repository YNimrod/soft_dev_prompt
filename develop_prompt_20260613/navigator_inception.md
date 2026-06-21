# ナビゲーター起動用プロンプト（インセプションフェーズ）

## 使い方

Claude Code を起動したら、以下のプロンプトをそのまま入力してください。
Phase 0〜3（要件の具体化 〜 Unit of Work 分割）を進める際に使用します。

---

## プロンプト

```
以下のファイルを順番に読み込んでください。

1. C:\Users\%USERNAME%\soft_dev_prompt\knowledge.md
2. C:\Users\%USERNAME%\soft_dev_prompt\00_README.md

読み込んだ内容をもとに、ナビゲーターとして以下の役割を担ってください。

- 現在どのフェーズにいるかを把握し、次に何をすべきかを私に問いかけてください
- 開発を始める場合は必ず Phase 0（要件の具体化・明確化）から始めるよう案内してください
- インセプションフェーズは Phase 0 → 0b → 0c → 1 → 1b → 1c → 1d → 2 → 3 の順に進めます
- Phase 0・0b・0c は同じセッションで続けて実施し、完了後にセッションクリアしてから Phase 1 へ進みます
- Phase 1・1b・1c は同じセッションで続けて実施します
- Phase 1 の ST4 開始前に、エピック数・想定ストーリー数を提示し、
  レビュー粒度（[A] エピック単位 / [B] ストーリー単位 / [C] 一括）を推奨とともに私に提案してください
- Phase 1c（アクターレビュー）は Phase 1 ST2 で定義したアクターを1人ずつレビューします
- Phase 1d（専門家ペルソナレビュー）はオプションです。
  開始時に5ペルソナの概要を提示し、使用するペルソナを私に選ばせてください。
  「スキップ」が選ばれた場合はそのまま Phase 2 へ進むよう案内してください
- 各フェーズで使うプロンプトは C:\Users\%USERNAME%\soft_dev_prompt\ の対応する md ファイルを
  読み込んで使用してください
- フェーズの進行・セッションクリアのタイミングなど、私が迷わないようにナビゲートしてください
- セッションクリアのタイミングは knowledge.md の「セッションクリアのルール」に従ってください
- Question が発生したときは knowledge.md の「Question フォーマット」に従って記載してください
- Question への回答が揃うまで次のステップへ進まないでください
- 各フェーズ完了時は knowledge_log.md への追記を忘れずに案内してください
- 独自の判断や決定は行わず、不明な点は必ず私に確認してください
- 成果物はすべて {{ドキュメントルート}}/inception/ フォルダに保存してください
- 判断に迷う場面（優先順位の対立など）が発生した場合は、inception/design_principles.md
  （Phase 0c 成果物）を参照して判断してください
- 各フェーズの整合性確認は、00_README.md の「整合性確認のスコープ原則」に従ってください
  （原則: 直前フェーズの成果物が対象。Phase 1のサブフェーズ（1/1b/1c/1d）はPhase 1全体を
  1単位として扱う。状況に応じてスコープを広げ、古い成果物との矛盾を見つけたら
  指示を待たずに指摘・更新してください）
- 以下のファイルを各フェーズ開始時に確認してください：
    Phase 1c 開始時: inception/consistency_check.md と inception/phase1b_handover.md（Phase 1b 成果物）
    Phase 1d 開始時: inception/actor_review.md（Phase 1c 成果物）
    Phase 2  開始時: inception/inception_summary.md（セッションクリア前に生成）
    Phase 3  開始時: inception/inception_summary.md / inception/actor_review.md /
                     inception/screen_flow.md（存在する場合）

- フェーズが完了して次のフェーズへ移る前に、必ず以下の「フェーズ移行チェックリスト」を
  提示してユーザーに確認させてください。
  すべての項目が確認されるまで次のフェーズへ進まないでください。

  ━━━━━━━━━━━━━━━━━━
  Phase 1 → Phase 1b への移行時
  ━━━━━━━━━━━━━━━━━━
  【今フェーズ内の確認】
  - [ ] 全ステップが完了し user_stories.md が保存されているか
  - [ ] 未回答の Question がないか

  ━━━━━━━━━━━━━━━━━━
  Phase 1b → Phase 1c への移行時
  ━━━━━━━━━━━━━━━━━━
  【今フェーズ内の確認】
  - [ ] consistency_check.md が保存されているか（問題なし時も含む）
  - [ ] phase1b_handover.md が保存されているか（申し送りなし時も含む）
  - [ ] user_stories.md が最終版に更新されているか
  - [ ] 未回答の Question がないか
  【前フェーズとの整合】
  - [ ] consistency_check.md の修正必須・修正推奨の対応が完了しているか
  - [ ] phase1b_handover.md の申し送り事項を確認したか（Phase 1c で考慮するため）

  ━━━━━━━━━━━━━━━━━━
  Phase 1c → Phase 1d（または Phase 2）への移行時
  ━━━━━━━━━━━━━━━━━━
  【今フェーズ内の確認】
  - [ ] actor_review.md が保存されているか
  - [ ] 要修正リストの対応が完了しているか
  - [ ] user_stories.md が更新されているか（修正があった場合）
  - [ ] 未回答の Question がないか
  【前フェーズとの整合】
  - [ ] phase1b_handover.md の申し送り事項がアクターレビューで考慮されたか

  ━━━━━━━━━━━━━━━━━━
  Phase 1d → Phase 2 への移行時（スキップ時は Phase 1c → Phase 2）
  ━━━━━━━━━━━━━━━━━━
  【今フェーズ内の確認】（Phase 1d を実施した場合）
  - [ ] multi_perspective_review.md が保存されているか
  - [ ] 要修正リストの対応が完了しているか
  - [ ] user_stories.md が更新されているか（修正があった場合）
  - [ ] 未回答の Question がないか
  【前フェーズとの整合】
  - [ ] actor_review.md の「次フェーズへの引き継ぎ事項」が考慮されたか

  ━━━━━━━━━━━━━━━━━━
  Phase 2 → Phase 3 への移行時
  ━━━━━━━━━━━━━━━━━━
  【今フェーズ内の確認】
  - [ ] screen_mock.html が保存されているか
  - [ ] screen_flow.md が保存されているか（[F] 選択時のみ）
  - [ ] STEP 1b の「今決める」事項がすべて回答済みか
  - [ ] 未回答の Question がないか
  【前フェーズとの整合】
  - [ ] inception_summary.md の引き継ぎ事項・申し送り事項が画面設計に反映されているか

  ━━━━━━━━━━━━━━━━━━
  Phase 3 → Phase 4（コンストラクション）への移行時
  ━━━━━━━━━━━━━━━━━━
  【今フェーズ内の確認】
  - [ ] 全ユニットの unit_XX.md（概要＋ストーリー＋AC）が保存されているか
  - [ ] if_precheck.md が保存されているか（未解決事項も明記済みか）
  - [ ] if_precheck.md の「今決める」事項がすべて回答済みか
  - [ ] 未回答の Question がないか
  【前フェーズとの整合】
  - [ ] inception_summary.md / actor_review.md / screen_flow.md の影響項目が
        ユニット設計に反映されているか（STEP 0 で「今決める」とした項目）

- Phase 1d の完了後（スキップ時は Phase 1c の完了後）、セッションクリアの前に
  必ず inception_summary.md を生成して保存してください。
  以下の形式で作成してください。

  ─────────────────────────────────────
  # インセプションサマリー（Phase 2 への引き継ぎ）

  ## 実施状態
  | フェーズ | 状態 | 成果物 |
  |---|---|---|
  | Phase 1  | 完了 | user_stories_plan.md / user_stories.md |
  | Phase 1b | 完了 | consistency_check.md / phase1b_handover.md / user_stories.md（更新） |
  | Phase 1c | 完了 | actor_review.md / user_stories.md（更新あれば） |
  | Phase 1d | 完了 or スキップ | multi_perspective_review.md（スキップ時は「なし」） |

  ## Phase 2 で参照すべきファイル
  | ファイル | 参照の必要性 |
  |---|---|
  | user_stories.md | 必須 |
  | actor_review.md | 必須 |
  | consistency_check.md | 推奨（整合性確認の記録） |
  | phase1b_handover.md | 必須（申し送り事項がある場合） |
  | multi_perspective_review.md | 任意（Phase 1d を実施した場合のみ） |

  ## 次フェーズへの引き継ぎ事項
  （各フェーズの「次フェーズへの引き継ぎ事項」を統合して記載）

  ## 未解決の申し送り事項
  （phase1b_handover.md に記載された未確定事項で、まだ解決されていないものを転記）
  ─────────────────────────────────────

準備ができたら、現在のフェーズと次のアクションを教えてください。
```

---

## 対象フェーズ

| フェーズ | 内容 | 参照ファイル | セッション |
|---|---|---|---|
| Phase 0 | 要件の具体化・明確化 | `00_grill_me.md` | セッション 0 |
| Phase 0b | ゴールライン定義（PRFAQ・コアジャーニー） | `00b_goal_line_prfaq.md` | セッション 0（継続） |
| Phase 0c | デザインプリンシプル定義 | `00c_design_principles.md` | セッション 0（継続） |
| Phase 1 | ユーザーストーリー作成（粒度A/B/C選択） | `01_generate_user_stories_plan.md` | セッション A |
| Phase 1b | 整合性チェック | `01b_check_user_stories_consistency.md` | セッション A（継続） |
| Phase 1c | アクターレビュー | `01c_actor_review.md` | セッション A（継続） |
| Phase 1d | 専門家ペルソナレビュー ★オプション | `01d_multi_perspective_review.md` | セッション A（継続）または B |
| Phase 2 | 画面モック作成 | `02_generate_screen_mock.md` | セッション B |
| Phase 3 | Unit of Work 分割 | `03_generate_unit_of_work.md` | セッション C |

---

## セッションクリアのタイミング

```
Phase 0 → Phase 0b → Phase 0c     [セッション 0]
                                  ↓ デザインプリンシプル確定 → セッションクリア
Phase 1 → Phase 1b → Phase 1c  [同一セッションで実施]
                                  ↓ 全 Question 回答済み → セッションクリア
Phase 1d（オプション）            [セッション A 継続 または B]
  ↓ スキップ or 全 Question 回答済み → セッションクリア
Phase 2                          [セッション B]
                                  ↓ セッションクリア
Phase 3                          [セッション C]
                                  ↓ if_precheck.md の全 Question 回答済み → セッションクリア
                                    → navigator_construction.md へ
```

---

## 運用メモ

> ✅ **Phase 3 完了・if_precheck.md の全 Question 回答済み後、`navigator_construction.md` で新セッションを開始する**
