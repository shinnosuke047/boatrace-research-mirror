# KYOTEI-AI RESEARCH MIRROR(外部AI共有用・読み取り専用)
生成日: 2026-09-04 / 正本: kyotei-ai リポジトリ /research/ 配下(本ファイルはその連結コピー)
注意: 数値の正直ルール(小標本=断定禁止・確定オッズ由来=diagnostic)を前提に読むこと。本文書には市場の歪みの所在(研究エッジ)が含まれる — 取り扱いは Owner(shin)の指示に従う。
---


# ===== RESEARCH_STATUS.md =====

# RESEARCH_STATUS — 研究状態の正本

- 最新更新: **2026-09-04**(更新者: Claude / セッション: v2.1 freeze)
- 本ファイルは Canonical Research State の入口。機械可読版 = `research_state.json`。人間向け表示 = 研究コンソール(Artifact 494f0be1… — 本ファイル群から生成される view であり正本ではない)

## 現在の研究フェーズ

**第1波(W1)直前** — Architecture Freeze v2.1 制定済み(2026-09-04)。土台(W0: 節IDマスタ・コース方位・ERA5・静的マップ・欠落データ回収)完了。実験登録簿 = registered 5本 + filed 1本(第1波の実行対象は4本)。

## Current Best Model / Baseline

- **Best = Baseline = `b2f41_prod2026_prod3`**(現状同一。v2.1 新アーキは未着工のため「最新=最良」)
- 実体: B2構造化着順NN(41特徴・6艇self-attention・120通り直接softmax・3seed平均)+ exh120展示補正層(θ9本)+ 市場ブレンド(w=0.85・推論後段/表示用)
- 主要指標: 全国 fold2 NLL 3.7565 / Hit@1 10.20% / 単勝Acc 57.46%。市場(確定オッズde-vig)との残距離 NLL +0.06〜0.07

## 現在実行中の Experiment

**なし**(適用パッケージ5点の Owner 判断待ち)。次 = NG-E10(まくり筋再検証+選手externality)。登録簿 = registered 5本(NG-E10 / NG-E1 / NG-E23 / NG-E5W / NG-E19SG)+ filed 1本(NG-E8SWAP=起票のみ)(registry: `artifacts/research/experiment_registry.jsonl`)

## 主要な研究成果(直近)

1. **SG桐生 8/30 実戦**: 頭的中9/12(市場と同着)、勝者確率で AI>市場 11/12(NLL 0.818 vs 0.981・n=12逸話)。展示補正は11/12正方向・量が保守的
2. **23項目監査**: 風向6.5年未使用 / live気象ゼロ(P0) / 未使用データの山(格ラベル・気温水温・チルト・部品交換・決まり手・支部)
3. **分離構造の実証**: 予測(オッズ非入力)/市場評価(純関数7本・shadow専用)/購入判断(NO BET fail-closed)の3層分離が既に de-facto 実装済みと実コード確認
4. 実験史の憲法: **モデル改造12連敗・情報追加と推論工夫のみ有効**

## 現在の問題

- **P0**: live予測の気象入力がゼロ(常時「無風・波ゼロ」で予想)— 修復パッチ済み・適用判断待ち
- conditional_finish に class_code 残留(再利用前に再GATE必須)
- 適用パッケージ5点が Owner 判断待ちのまま(推奨: 1,2,3,4適用・5見送り)
- 全成果物が未コミット

## 次にやること

`NEXT_ACTIONS.md` 参照(5件・優先理由・情報利得つき)。1行版: 適用判断 → NG-E10 → NG-E1/E23 → NG-E5W → 常時E19SG。

## 更新ルール(2026-09-04 Owner 指示で制定)

コード・実験・研究状態を更新したら、**Artifact だけでなく /research/ 配下の本ファイル群と research_state.json を必ず同期する**。他のAI・人間はまずここを読む。



# ===== NEXT_ACTIONS.md =====

# NEXT_ACTIONS — 現在優先すべき研究(3〜5件だけ)

最新更新: 2026-09-04。優先度 = Expected Information Gain × 予測価値 ÷ 実装コスト。

## 1. 適用パッケージ5点の Owner 判断(研究ではないが全実験の前提)

- **理由**: P0(live気象ゼロ)を直さない限り、環境系の全研究が「学習では見るが本番で見ない」矛盾を抱える
- 必要データ: なし(パッチ・検証済み)。**Expected Gain: 実験でなく基盤 — 本番と研究の整合回復**
- 状態: 推奨 = 1,2,3,4 適用・5 見送り(詳細 lane-reports/nextgen_audit_20260903.md §23)

## 2. NG-E10 — まくり筋再検証 + 選手externality実在判定

- **理由**: ①まくり筋+29%見落としは唯一の生存歪み(z≈8.4)で、再検証だけで確定する最短案件 ②「6艇相互作用が選手固有現象として実在するか」は v2.1 の心臓の go/no-go — 不在なら GAT/Interaction 系を全中止でき、最大の無駄を防ぐ
- 必要データ: すべて手元(B2残差 + 全期間結果)。学習ゼロ・統計のみ
- **Expected Information Gain: 最大**(アーキ投資の可否がこの1本で決まる)

## 3. NG-E1 + NG-E23 — レース格カテゴリ & 勝負駆け utility curve

- **理由**: 格でSTが変わる実測(24/24場同符号)があるのに格カテゴリは F=41 未収載 = 確実に存在する未投入情報。SG現場で shin が読んでいた「条件が絡む心理」の機械化
- 必要データ: setsu_master.parquet(済)+ standing_panel(済)。月間開催日程(取得可能を確認済)があれば ex-ante 判定が完成
- Expected Gain: 高(市場が織り込みにくい情報の筆頭候補。ただし圏内バイナリ null の前例から utility curve 形式のみ)

## 4. NG-E5W — 風のコース成分

- **理由**: 風向は6.5年未使用の空白 + コース方位テーブル(high 19場)が完成し変換の前提が揃った
- 必要データ: venue_course_azimuth.json(済)+ K/beforeinfo風向(済)。評価はクリーン行のみ
- Expected Gain: 中〜高(季節焼き直し検査を通る必要あり — 気温水温の轍)

## 5. 常時 — NG-E19SG(SG/G1 祭り市場効率)

- **理由**: SG当日の AI>市場 実測(n=12)の一般化検証。当たれば「特定条件下エッジ」の本命
- 必要データ: 締切前オッズ(2026-07-10〜蓄積中)+ グレードラベル(開催日程ページ)
- Expected Gain: 中(検定1本・実装極小。ただし蓄積期間が浅く結論は先)



# ===== ARCHITECTURE.md =====

# ARCHITECTURE — Canonical Architecture の現在地

- **Architecture Version: v2.1**(制定 2026-09-04・shin freeze 指示)
- 最新更新: 2026-09-04(v2.1 freeze セッション)
- 詳細設計の正本: `docs/ARCHITECTURE_FREEZE_v2.1.md`(北極星 = `docs/NEXT_GEN_RESEARCH_CHARTER.md` / 現状実測 = `lane-reports/nextgen_audit_20260903.md` / 実験判定の正典 = `docs/MODEL_STRATEGY.md`)
- 本ファイルは freeze 文書の自己完結ダイジェスト。**このファイルだけ読めばアーキの現在地が全部分かる**ことを目的とする。矛盾したら `research_state.json` / `RESEARCH_STATUS.md` を正とする

---

## 0. 30秒サマリ(まずここだけ)

- 設計思想は v2.1 で「6艇の能力ランキング」から **Context-Aware Multi-Agent Dynamic System**(誰が攻めて誰に展開が向くかの構造理解)へ統合された。ただし **v2.1 の新アーキ(Expert 群・GAT・Master Integrator)はまだ1行も存在しない**。
- 現本番 = Baseline = Best = **`b2f41_prod2026_prod3`**。実体は「1つのモデル(B2)が全情報を41特徴+6艇 self-attention で暗黙に融合」+ 後段2層(exh120 展示補正・市場ブレンド w=0.85)。
- 現在値(全国 fold2・3seed 平均): **NLL 3.7565 / Hit@1 10.20% / 単勝Acc 57.46%**。市場(確定オッズ de-vig)との残距離 NLL +0.06〜0.07(diagnostic)。
- 実験史の憲法: **再学習を伴うモデル改造は12連敗で全滅。効いたのは情報追加(as-of 新特徴)と推論工夫(seed平均・市場ブレンド・薄い後段層)のみ**。唯一のアーキ勝利 = B2 構造化そのもの。→ v2.1 も「情報で勝ってから構造に投資」の順を厳守。
- 原則: v2.1 は「作り直せ」ではない。既存を Baseline として保持したまま KEEP/EXTEND/BASELINE/REFACTOR/NEW/DEFER を記録し、破壊ゼロ・全ブロック並走・PoC 先行で進める。

---

## 1. Canonical Architecture v2.1(概念フロー図)

ステータス凡例: 🟢 IMPLEMENTED(実装・実証済)/ 🟡 EXPERIMENTAL(データ・PoC あり・判定前)/ 🔵 PLANNED(設計のみ)/ ⚫ REJECTED(棄却済・同形再提案禁止)

```
RAW DATA ─────────────────────────────────────────────── 🟢 (収集稼働)
   │
   ▼ SPECIALIZED REPRESENTATIONS / EXPERTS
   ├ Player Evolution Expert (動的状態/trend/change-point)  🔵 PLANNED   [Priority A]
   ├ Player Technique/Tactical Expert (技術分解)            🟡 一部データ有 [A]
   ├ Start Expert                                          🟢 F41に内包
   ├ Motor Expert (historical)                             🟢 F41に内包
   ├ Maintenance/Adjustment Expert (整備/交換)             🔵 データ有・parser修理要 [B]
   ├ Propeller Latent Expert                               🔵 未取得依存 [C/DEFER]
   ├ Environment Expert (気象/風コース成分)                🟡 ERA5+方位表 構築済・E5判定前 [A]
   ├ Stage/Utility Expert (勝負駆け)                       🟡 節マスタ+utility70%済・E1/E23前 [A]
   ├ Track/Local Expert (当地適性)                         🟡 現特徴デッドウェイト・要REFACTOR [A/B]
   └ Relationship/Familiarity                              🔵 PLANNED [B/C]
   │
   ▼ CURRENT BOAT STATE × 6                                🟢 B2 boat_encoder(実証済コア)
   │
   ▼ CURRENT INTENT × 6                                    🔵 PLANNED (proxy有: 進入/チルト/展示ST) [A]
   │
   ▼ RACE INTERACTION GAT                                  🟡 前駆有: B2の6艇self-attention / GATは未 [A・E10ゲート]
   │
   ▼ 1M / SCENARIO MODEL                                   🔵 PLANNED (決まり手データ有) [B]
   │
   ▼ MASTER INTEGRATOR                                     🔵 PLANNED ★最重点 [A]
   │                                                          (現状=単一B2+後段2層の暗黙統合)
   ▼ FUNDAMENTAL RACE PROBABILITIES                        🟢 B2 120通りsoftmax(オッズ非入力)
   │
   ▼ CALIBRATION / UNCERTAINTY / TAIL                      🟡 T≈1.0のみ・領域別/Tailは未 [A]
   │
   ▼ MARKET EVALUATION                                     🟢 src/ev.py層設計済(純関数・分析専用) [KEEP/EXTEND]
   │
   ▼ BETTING DECISION / PORTFOLIO                          🟡 select_picks/NO BET有・portfolio凍結 [EXTEND]
```

**v2.1 が要求する分離のうち既に de-facto 実現しているもの(既存の強み)**:
- Fundamental はオッズ非入力 → B2 は既にそう。市場ブレンドは推論後段のみ。**予測がオッズに汚染されない構造は実装済み**。
- GAT の前駆 = B2 は既に6艇 Transformer self-attention を持つ(順列同変・lane 数値で対称性破り)。GAT はこの自然な発展。
- Market Evaluation = `src/ev.py` の分析レイヤ群が純関数 df→df で存在し、本番 predict に強制接続していない。**予測と市場評価の層分離は設計段階から守られている**。

---

## 2. ブロック別ステータス表(実装状態 × Migration 分類)

Migration 分類: **KEEP**=そのまま流用 / **EXTEND**=拡張で使える / **BASELINE**=比較用に残す / **REFACTOR**=設計と衝突・要改修 / **NEW**=新規 / **DEFER**=将来研究

| v2.1 ブロック | 状態 | 分類 | 現状の実装/資産 | Gap = 何が足りないか | 最初の一歩 |
|---|---|---|---|---|---|
| Fundamental 出力層(120softmax) | 🟢 | **KEEP** | B2 `B2Structured120`(464,817 params) | なし | E0再現(済) |
| Boat State Encoder×6 | 🟢 | **KEEP** | B2 boat_encoder(共有MLP 41→128) | なし | — |
| 予測/購入の分離原則 | 🟢 | **KEEP**(明文化) | ev.py層=純関数・本番非強制接続 | 3層の責務境界をコードの assert で機械強制 | 文書化のみ |
| Start Expert | 🟢 | **KEEP** | recent10_st・st_q10/std_prior(F41内包) | Start Consistency の latent 化は将来 | — |
| Motor Expert(historical) | 🟢 | **KEEP** | motor_2rate・motor_recent20_top2(F41内包) | 性能ベクトル(伸び/出足/回り足)latent は将来 | E6後 |
| Market Evaluation層 | 🟢 | **EXTEND** | ev.py(Fair/Market/Edge/ConsEV) | Odds uncertainty・Market edge confidence の出力追加 | W2以降 |
| Environment Expert | 🟡 | **EXTEND** | 気象4特徴(風向は死特徴)+ERA5+方位表 | 風コース成分・Motor×Env・気圧湿度の投入 | **E5W(W1)** |
| Stage/Utility Expert | 🟡 | **EXTEND** | setsu特徴+setsu_master+standing_panel | 格カテゴリ・qualification確率化・準優utility | **E1/E23(W1)** |
| Betting/Portfolio | 🟡 | **EXTEND** | select_picks・NO BET(ev_c=None)・conditional_finish | Robust EV・Scenario Support・ゴミ舟券禁止ルール | W3(予測層成熟後) |
| Calibration/Tail | 🟡 | **EXTEND→NEW** | 温度T≈1.0のみ | 領域別(Core/Secondary/Tail/ExtremeTail)較正 | W2(backlog 1-5/3-1) |
| Race Interaction(GAT) | 🟡 | **EXTEND→NEW** | B2の6艇self-attention(前駆) | Edge-aware GAT・Attention/Effect分離・因果検証 | **E10で現象確認→E11** |
| Track/Local Expert | 🟡 | **REFACTOR** | 当地4特徴(ablation でデッドウェイト) | 無条件平均をやめ条件付き(Local×難水面)へ | E7+E8(W2) |
| Player Evolution | 🔵 | **NEW** | recent form スカラーのみ | skill trend/velocity/acceleration/change-point | W2(E9系) |
| Player Technique | 🟡 | **NEW** | st分布・decimomari(racer_style) | latent skill分解・Attack/Disruption分離・Multi-task | E10後→W2 |
| Current Intent×6 | 🔵 | **NEW** | proxy有(進入/チルト/展示ST) | Intent latent(2重ゲート: 行動予測→着順上乗せ) | W2(E12-14) |
| Master Integrator ★最重点 | 🔵 | **NEW** | 単一B2+後段2層(暗黙統合) | Expert出力+confidence+GATを条件付き統合。単純加重を baseline に | W2/W3(各PoC後) |
| 1M/Scenario | 🔵 | **NEW** | 決まり手データ(未特徴化) | 観測ラベル→latent mixture・Scenario Entropy | W3(E16) |
| Maintenance/Adjustment | 🔵 | **NEW** | 部品交換データ(parser取り違え) | parser修理→Problem/Intervention/Response・Adjustment Skill | W2前提修理→W3 |
| Multi-task Learning | 🔵 | **NEW** | 単一target(trifecta CE) | ST/進入/決まり手/展示 の補助head | W2以降 |
| Relationship/Knowledge | 🔵 | **NEW/DEFER** | なし | 同走回数・支部・師弟の行動残差(理由断定せず) | W3以降 [B] |
| Propeller Latent | 🔵 | **DEFER** | なし(選手コメントNLP未取得) | 前向き収集が前提 | [C] |
| Race video / 1M映像 | 🔵 | **DEFER** | 打ち切り済 | — | 再提案は proxy 枯渇後 |
| 階級ラベル | ⚫ | **REJECTED** | 明示除外済 | 全棄却確定・再投入禁止(2026-06確定) | — |
| 明示的交互作用の積項 | ⚫ | **REJECTED** | 桐生で過学習方向 | 積項は作らず attention に委ねる | — |
| lambdarank portfolio | ⚫ | **BASELINE(凍結)** | Phase1 FAIL・コード残存・本番非接続 | 後継 = conditional_finish | — |

### 2-1. 3層分離の現況(2026-09-04 実コード検証で確定)

目標の3層(逆流禁止 = 下層が上層の確率を書き換えない): ① Fundamental Race Model(オッズ非入力で真の着順確率)→ ② Market Evaluation(確率確定後に初めてオッズを読む)→ ③ Betting Decision(確率もEVも変更不可・BUY/NO BET/点数/配分のみ)。

- **①は達成**: 入力列にオッズ由来ゼロ(dataset.py:16 / model.py:19-41、class_code 除外済み)。市場は推論後の表示用 blend のみ(scripts/predict_b2_live.py:501 `0.85*mkt+0.15*p`)。
- **②は実在・shadow専用**: 純関数レイヤ7本 = src/fair_odds.py・market_implied.py・edge_features.py・conservative_ev.py・tail_control.py・candidate_classifier.py・portfolio_ev.py(純関数 df→df)。接続は src/shadow_pipeline.py:33-39 → src/predict_live.py:319(記録のみ・本番推奨に影響しない)。「Odds uncertainty / Market edge confidence」は未出力 → EXTEND。
- **③は骨格あり**: select_picks(ev≥0.15, src/ev.py:172)+ NO BET fail-closed(cons_mult 欠損/例外→None→ raceday_decision_feed.py:64 で自動除外・EVC_THR=1.15)。領域別Tail較正 / Robust EV / ゴミ舟券禁止 / Scenario Support は未実装 → W3。
- 補足確定事項: conditional_finish は GATE PASS だが **borderline(CI 4/6)+ class_code 残留(conditional_finish.py:32)** — v2.1 で再利用する場合は class 除外の再GATE 必須。Dynamic Player State 系(trend/velocity/change-point)は src/scripts 内に未実装(recent form スカラーのみ)を grep 確認。multi-task は composite_loss(周辺化NLL加算・別ヘッドではない)がオプション実在、本番バンドルの学習設定は要確認。
- **v2.1 で足す機械強制**: 3層の関数境界に「Betting層は prob 列を read-only」を assert 化(逆流の構造的禁止)。

---

## 3. Architecture Changelog

| date | version | what changed | why | supporting evidence | migration impact |
|---|---|---|---|---|---|
| 2026-09-04 | **v2.1** | 「6艇の能力ランキング」から「Context-Aware Multi-Agent Dynamic System」へ設計思想を統合。予測/市場評価/購入判断の3層完全分離を明文化。Master Integrator・Intent・Dynamic Player State・Scenario・Relationship を正式研究ブロック化 | 能力スカラーの積み上げ(現B2)では「誰が攻めて誰に展開が向くか」を表現できない。SG桐生実測で頭当ては市場と互角・確率精度でのみ勝った=構造理解に伸びしろ | SG桐生 8/30 答え合わせ(NLL 0.818 vs 市場0.981・展示反映11/12正方向・n=12逸話)/ 23項目監査 / まくり筋過小評価(+29%見落とし・唯一の生存歪み) | 破壊ゼロ。現B2は Baseline として保持。新ブロックは全て並走・PoC 先行 |
| (基準) | v2.0相当 | B2構造化着順NN + exh120補正層 + 市場ブレンド(現本番) | — | results_summary.md 全採用/棄却履歴 | — |

今後の設計変更は `docs/ARCHITECTURE_FREEZE_v*.md` の Changelog に「なぜ / 旧設計の不足 / 支持する実験結果」を追記して version を上げ、本ファイルへ同期する(場当たり追記の禁止)。

---

## 4. 凍結される原則(v2.1 で変えないもの)

- **EV閾値 +15% 固定**。数字を盛らない(n小 / 確定オッズ=diagnostic / 実弾主張なし = 2026-08-10 決定)。
- 本番ログ md5 無傷・`models/latest` 非接触・boatrace.jp polite。
- **既存モデルは Baseline として削除しない**。新機能は一気統合せず ablation。
- 複雑さは目的でない・但し規模でも棄却しない。判断は常に「未来で予測改善 / 較正 / 汎化 / edge実在 / 説明可能」。

---

## 5. 参照(次に読むもの)

- 実験の登録・判定ゲート・待機中実験: `research/RESEARCH_STATUS.md` / `artifacts/research/experiment_registry.jsonl`(判定ゲート G0-G6・採用ライン 薄層ΔNLL≥0.003 は freeze 文書 §F)
- 仮説台帳・成果・リーク/過学習リスク: `research_state.json`(hypotheses / leakage_status / overfitting_status)
- 第一手 = **NG-E10**(選手 externality 統計PoC+まくり筋再検証): 学習ゼロ・モデル無改変で「6艇 interaction が実在するか」を判定する GAT 系の go/no-go ゲート。まくり筋過小評価(+0.001416・z≈8.4・AI相対 +29% 見落とし)は唯一どの補正でも生き残った歪み。



# ===== EXPERIMENTS.md =====

# EXPERIMENTS — 実験台帳(正本)

- 最終更新: 2026-09-04(セッション: v2.1 freeze)
- 位置づけ: Canonical Research State の実験台帳。機械可読 index = `artifacts/research/experiment_registry.jsonl`。矛盾時は `research_state.json` / `RESEARCH_STATUS.md` を正とする
- 主な出典: `docs/experiments/structured_order_model/results_summary.md` / `docs/MODEL_STRATEGY.md` / `docs/ARCHITECTURE_FREEZE_v2.1.md` / `lane-reports/nextgen_audit_20260903.md` / `lane-reports/hansei_sg_kiryu_20260903.md` / `artifacts/research/mkt/preregistration_20260806.md`
- 判定凡例: **ADOPT**(採用・本番/構成に反映)/ **REJECT**(棄却・同一形での再提案禁止)/ **FROZEN**(凍結・コード残存/Baseline扱い)/ **REGISTERED**(事前登録済み・未実行)
- 現行 Baseline = Best = **`b2f41_prod2026_prod3`**(B2構造化着順NN F=41・3seed平均 + exh120展示補正層θ9 + 市場ブレンド w=0.85 推論後段)。現在値: 全国 fold2 NLL **3.7565** / Hit@1 **10.20%** / 単勝Acc **57.46%**
- 実験史の憲法: **再学習を伴うモデル改造は12連敗で全滅。効いたのは情報追加(as-of新特徴)と推論工夫(seed平均・市場ブレンド・薄い後段層)のみ**(唯一のアーキ勝利 = B2構造化そのもの)
- 統治上の注意: fold1/fold2 は開発汚染済み = 採否の**最終**根拠にしない(G3 prod2026窓・G5市場・G6 segment を併用)。ROI 列は「real(締切前オッズ)」でのみ主張可。確定オッズ由来は **diagnostic** と明記する

---

## 1. 採用済み(ADOPT・8件)

### 1-1. B2 — 構造化120通り直接スコアリング

- **仮説**: 艇エンコーダ+role埋め込み+共有スコアラーの構造化は、naive 120クラス(B1)・LGB+PL(B0)・本番級 RaceNN を上回る
- **変更内容**: `B2Structured120`(464,817 params)。6艇×特徴 → 共有MLP → Transformer 2層×4head(6艇 self-attention)→ 120候補を共有スコアラーで直接スコア → softmax
- **指標(実測・3seed・同一 test set)**: fold2 NLL **3.785±0.0005** / Hit@1 **9.88%** / Hit@10 51.8% / 単勝Acc **57.1%** / MRR 0.226。fold1 NLL **3.824** / Hit@1 **9.54%** / 単勝Acc 57.05%
- **walk-forward**: 2fold 全指標で B2 > B1(3.816/3.850)> NN移植(3.898/3.942)> B0(4.039/4.066)— 順位が両 fold で再現
- **Calibration**: 記録なし(後の温度較正検証で T≈1.0 = 既に較正済みの診断のみ)
- **ROI**: 対象外(精度実験)
- **判定**: **ADOPT**(唯一のアーキ勝利。以後の全実験の土台)
- **考察**: earlier の「B0 優位」は smoke 274レースの小標本 artifact で、full test で消滅。「B2 > 本番級NN」も RaceNN 移植対決で証明済み

### 1-2. extra7 — 当地credibility + 節内フォーム(第1弾・7特徴)

- **仮説**: モデルが知らない情報(当地経験量・節内フォーム)の追加が伸びしろ
- **変更内容**: past-only 導出7特徴(n_local_prior / blended_local_win K=20収縮 / has_local / setsu_day / setsu_prior_{n,win,top2})。leakage guard 通過
- **指標(実測・3seed)**: fold2 NLL **3.777±0.001** / Hit@1 9.95% / 単勝Acc 57.24%。fold1 NLL **3.814±0.002** / Hit@1 9.59%
- **walk-forward**: vs 素の B2 で 2fold・全主要指標一貫改善(NLL −0.008 / −0.010 = seed 誤差の4〜10倍)
- **Calibration**: 記録なし
- **ROI**: 対象外
- **判定**: **ADOPT**
- **考察**: 同時期の B2H(embedding)が改善ゼロだった対照で「モデル改造より新情報」の路線が確立。ただし後の ablation で当地系4本は寄与ゼロ〜微マイナスの「デッドウェイト候補」(置換テーマ = NG-E8SWAP)

### 1-3. extra2 — 場×コース歴史率 + 直近5走(第2弾・+4列, F=37)

- **仮説**: 会場の個性(場×コース率)と直近フォームは数値でも効く
- **変更内容**: venue_lane_win/top2_prior + racer_recent5_win/top3 の4列追加。サニティ: 1号艇場別勝率 min 江戸川0.427 / max 徳山0.625 = ドメイン知識と一致
- **指標(実測・3seed)**: fold2 NLL **3.7719** / Hit@1 **10.07%** / 単勝Acc 57.34%。fold1 NLL 3.8089 / Hit@1 9.65%(Acc のみ横ばい)
- **walk-forward**: 2fold 一貫改善。3seed 平均と合わせ全国 Hit@1 9.88→**10.21%**
- **Calibration**: 記録なし
- **ROI**: 対象外
- **判定**: **ADOPT**
- **考察**: 特徴グループ ablation の寄与序列は ①直近5走系(主役)②場×コース系 ③節内系 ④当地系(ゼロ〜微マイナス)

### 1-4. extra3 — ST分布 + 節内得点(第3弾・+4列, F=41 完成)

- **仮説**: 選手×コースの ST 分布形状と節内得点文脈が確率の質を上げる
- **変更内容**: st_q10_prior / st_std_prior(expanding, min_periods=10)+ setsu_pts_avg / setsu_pts_rank_pct(唯一の対戦相手相対特徴)
- **指標(実測・レース単位 paired bootstrap 2000回・3seed平均確率同士)**:
  - fold2 NLL 3.76347→**3.75655**(差 −0.00691, CI95 [−0.00877, −0.00504])✅有意
  - fold1 NLL 3.80199→**3.79773**(差 −0.00426, CI95 [−0.00599, −0.00256])✅有意
  - Hit@1 / 単勝Acc は 2fold とも誤差圏(例: fold2 Hit@1 −0.004pp, CI ±0.2pp)
- **walk-forward**: NLL は 2fold 一貫有意。**prod2026窓(n=1064)は逆転気味**(3連単 NLL/Hit@1 は旧 prod 微優位・単勝Acc のみ prod3 +0.62pp)— 小標本(Hit@1 seed std ±0.49pp)でどちらも断定不可
- **Calibration**: 記録なし(G4 の「当てる率でなく見積もり精度の改善」明記の前例)
- **ROI**: 対象外
- **判定**: **ADOPT**(NLL のみ。「当てる率が上がった」とは言わない)
- **考察**: seed std ×3 基準だけでは fold1 が誤差圏で棄却されるところ、レース単位 bootstrap で実在改善と確定。誤差基準はレース bootstrap CI 併用が以後のプロトコル

### 1-5. seed3 — 3seed 確率平均アンサンブル

- **仮説**: seed 分散の除去はコストゼロの改善
- **変更内容**: seed 42/43/44 の softmax 確率算術平均(追加学習ゼロ)
- **指標(実測)**: fold2 全国 Hit@1 10.07→**10.21%**(+0.14pp)/ NLL 3.7719→**3.7635**(extra2 構成時点)
- **walk-forward**: 記録なし(fold2 での全面改善を確認して常時採用)
- **Calibration**: 記録なし
- **ROI**: 対象外
- **判定**: **ADOPT**(推論は常に3seed平均)
- **考察**: 3で飽和(5seed は不要 → §2)。EMA は per-seed では効くが 3seed 平均後は完全同値 = 同じ分散を消しており重複(不採用)

### 1-6. exh120 — 展示補正層(推論後段・薄層)

- **仮説**: 展示タイム/展示ST/展示F は市場が織り込みモデルが見えない直前情報 — 薄い後段補正で回収できる
- **変更内容**: θ9本(展示タイムz・展示STz・展示Fフラグ × 1着/2着/3着位置)で120通り分布を log-odds 補正。θ実測 exh_z_p1/p2/p3 = −0.234/−0.131/−0.092
- **指標(実測)**: 研究窓 ΔNLL **−0.0181**・24/24場改善。本番窓 holdout −0.015前後(−0.0154 CI[−0.0281,−0.0036] と −0.0148 CI[−0.0261,−0.0036] の記載差あり = 要確認。いずれも CI 0非跨ぎ)
- **walk-forward**: 研究窓+本番窓 holdout の2段で改善再現。SG桐生 8/30 実戦で展示反映が勝者確率を改善 **11/12**(悪化1・n=12逸話)
- **Calibration**: 記録なし。増幅は保守的(方向は正・量が不足 = Intent 層の存在理由)
- **ROI**: 対象外
- **判定**: **ADOPT**
- **考察**: 展示 z の上限処方3案(raw3 / gate@τ / shrink@τ)は 2fold 一貫で現行 z3 を超えず全て不採用。運用ルールのみ追加(展示 max-min ≤0.08秒のレースでは直前補正を単独の勝負根拠にしない)

### 1-7. mkt_blend — 市場ブレンド(Benter 型2段・w=0.85)

- **仮説**: one-step のオッズ直入れでなく、独立予測後の2段ブレンドで市場の集合知を取り込める(Benter 1994 / Sung&Johnson 2007)
- **変更内容**: 推論後段のみ `blend = 0.85*market + 0.15*model`(w は fold1 で 0.8-0.9 から選定・fold2 で評価)
- **指標(実測)**: fold2 住之江で **NLL 市場単独超え**(extra 構成: 3.5612 vs 市場 3.5640 / extra2 構成: 3.5618 vs 3.5640)。Hit@1 差(9.3-9.9%)は n=1083 のノイズ圏
- **walk-forward**: 2構成で再現。時系列厳守(重み選定=過去 fold1 / 評価=未来 fold2)
- **Calibration**: 記録なし
- **ROI**: 記録なし(確率精度の実験。ROI 主張なし)
- **判定**: **ADOPT**(表示用・推論後段のみ。予測層はオッズ非入力を維持)
- **考察**: 「市場より下がらない・確率精度は上回る」= AI が市場への増分情報を持つ存在証明

### 1-8. f41_skew_fix — 学習気象の beforeinfo 由来統一(train/serve skew 是正)

- **仮説**: 学習=K由来(レース後確定)気象 / 本番=beforeinfo という不一致(skew)が本番性能を損なう
- **変更内容**: 学習側の気象列を Kファイル由来 → beforeinfo(T1=展示後・締切前)由来に統一。バンドル `b2f41_prod2026_prod3`(2026-08-04 GATE PASS → 08-06 本番切替。md5 で research 側バンドルと同一を実測)
- **指標**: GATE PASS の個別数値は本台帳の出典内に記録なし
- **walk-forward**: 記録なし(GATE PASS 判定のみ)
- **Calibration**: 記録なし
- **ROI**: 対象外
- **判定**: **ADOPT**(2026-08-06 切替済み・現行本番バンドル)
- **考察**: ただし 23項目監査で **live 気象入力が実戦キャプチャ 96/96件 None**(常時「無風・波ゼロ」)の P0 が発見済み — 気象 skew は学習側で是正・本番 live 側は修復パッチ適用判断待ち

---

## 2. 棄却群(REJECT — 同一形での再提案禁止)

| 実験 | 仮説 | 変更内容 | 指標(実測) | walk-forward | 判定・考察 |
|---|---|---|---|---|---|
| **B2H embedding** | racer/jcd ID embedding で選手個性を追加表現 | 数値特徴に racer(16)/jcd(8) embedding 連結(B2 本体無改変) | fold2 NLL 3.787±0.002 / Hit@1 9.78%(B2 3.785 / 9.88% と同等〜僅下。NLL差 +0.002 = seed ばらつき圏内) | fold1 は完走前に停止(未測・結論は変わらない見込み) | **REJECT**。数値特徴が選手個性を既に表現済み・ID の追加情報が乗らない |
| **複合損失(B3)** | trifecta+exacta+win の複合損失で改善 | 周辺化 NLL の加算損失 | NLL 3.7729 vs 3.7719 = 全指標 seed 誤差圏 | 記録なし(fold2 で誤差圏につき打ち切り) | **REJECT** |
| **容量増** | d=192×3層への拡大で表現力向上 | パラメータ増のみ | 誤差圏(個別数値の記録なし) | 記録なし | **REJECT**。ボトルネックは容量でなく情報(B2H と一貫) |
| **4モデル混成** | B2+B1+NN+LGB の異種アンサンブルで改善 | 算術/幾何平均・重みは fold1 グリッド | 最適重みが B2 支配(0.7-0.8)で NLL +0.001 程度 = B2 単独 seed アンサンブルを超えず | 記録なし | **REJECT**。副産物: LGB アーム `build_lgb_pl_probs.py` を資産化 |
| **race_no 特徴** | レース番号(番組編成)が予測に効く | race_no を特徴追加 | fold2 NLL −0.002 / Hit@1 +0.06pp(改善方向)だが fold1 NLL +0.0002 / Hit@1 −0.03pp = 完全誤差圏 | **fold間不再現** — 2fold 一貫基準で棄却 | **REJECT**。2fold 規律が機能した代表例 |
| **5seed** | seed 数を増やせばさらに改善 | 3seed→5seed | 個別数値の記録なし(「3で飽和・5は不要」の判定記録のみ) | 記録なし | **REJECT** |
| **温度較正** | 温度スケーリングで較正改善 | 温度 T の最適化 | T≈1.0 = 既に較正済み(改善余地なし) | 記録なし | **REJECT**。明示的較正層なしが現行(領域別較正は W2 の別テーマ) |
| **気温水温(F43)** | 気温・水温の素値が予測に効く | F=41→43(temperature / water_temp 素値追加) | fold間符号反転。permutation で実体の8〜9割が季節の焼き直し | fold間符号反転 = 即棄却 | **REJECT**(再提案禁止)。新規性は差分系(air_water_gap 等)・季節統制後残差に限る |
| **潮汐/戦型/番組ギャップ薄層** | 潮汐・決まり手スタイル・相手強度の薄層補正が効く | 各 env パネル(tide 219,732R / racer_style 206万行 / program_gap 349,195R)の薄層 | ΔNLL −0.0006〜0.0011 = 採用ライン **0.003 未達** | 記録なし | **REJECT**(薄層単独)。交互作用(Local×Tide 等)・NN直接入力は未検証のまま |
| **階級(class_code)** | 階級ラベルが予測に効く | class_code 入力 | 全棄却(2026-06 確定)。市場側も「A1人気過剰」仮説は全級±0.7pp = 正確に織り込みで棄却 | — | **REJECT**(再投入禁止)。dataset.py で明示除外。conditional_finish に残留あり = 再利用時は再GATE必須 |
| **明示積項** | 交互作用を明示積項で与えると効く | 特徴間の積項追加(桐生) | 過学習方向(個別数値の記録なし) | — | **REJECT**。積項は作らず attention に委ねる(v2.1 でも凍結原則) |

補遺(判定完了・上記11件の外):
- **EMA**: per-seed 全指標改善(NLL −0.006)だが 3seed 平均後は完全同値 = 不採用(単seed 運用時のみの選択肢)
- **展示z 上限処方3案**(raw3 / gate@τ / shrink@τ): 2fold 一貫で現行超えなし・不採用(§1-6)
- **レース番号事前勝率(extra5)**: builder+parquet あり・**判定待ちのまま**(採用記録なし)

---

## 3. 凍結(FROZEN・1件)

### 3-1. lambdarank portfolio

- **仮説**: lambdarank 系ランキング学習でポートフォリオ選別を改善できる
- **変更内容**: portfolio_selector(lambdarank 経路)
- **指標**: Phase 1 **GATE FAIL**(個別数値は本台帳の出典内に記録なし)
- **walk-forward / Calibration / ROI**: 記録なし
- **判定**: **FROZEN**(コード残存・本番非接続・BASELINE 扱い。削除しない)
- **考察**: 後継 = conditional_finish(GATE PASS・ただし borderline CI 4/6 + class_code 残留 → v2.1 で再利用する場合は class 除外の再GATE 必須)

---

## 4. 事前登録済み・未実行(REGISTERED・6本)

registry(`artifacts/research/experiment_registry.jsonl` 2026-09-03 登録・git a759dac)からの転記。全て W1 以降・適用パッケージ5点の Owner 判断が前提。

| ID | テーマ / 仮説 | planned_test(登録内容) | decision_rule(登録内容) | 状態 |
|---|---|---|---|---|
| **NG-E10** | 選手 externality 統計PoC + まくり筋再検証。唯一の生存歪み(まくり筋 +0.001416, z≈8.4, AI相対+29%見落とし)の事前登録再検証 | P1=LGB expanding crossfit 全期間 / P2=fold2 バンドル推論 dump 2025-07..2026-06。BH-FDR + \|効果\|≥2pp。venue×grade×年 demean・比例配分帰無・自艇残差≈0層の別枠報告。主判定 = ①分散成分検定(選手ラベル permutation 帰無・Yes/No)②まくり筋セル: 前半抽出→後半+P2 符号再現 | 層1不通過 → 選手固有 externality は検出不能と結論し N1 以降を中止。まくり筋は z 再現 + CI95 0非跨ぎで確定 | registered |
| **NG-E1** | レース格カテゴリ(Stage)。動機 = 格で ST 変化(準優 −0.0094 / 優勝戦 −0.0065・24/24場同符号)・1号艇逃げ率 46.7→71.3%。格カテゴリは F=41 未収載 | 8カテゴリ決定表(title+series_header)。プラセボ = race_no 単独版必須。既存 F=41 との焼き直し検査を先行。主指標 = 凍結B2+薄層θ(stage×lane rank-1 圧縮)ΔNLL≥0.003・レース単位 paired bootstrap CI95 両fold 0非跨ぎ | プラセボ超えなければ棄却。本番昇格は ex-ante 判定器一致率 ≥98% が条件 | registered |
| **NG-E23** | 勝負駆け utility curve + レース集約(E2+E3 統合)。バイナリ圏内/圏外は統制後消滅 → 連続 utility で再挑戦 | q_k=P(projected_score_if_k≥B+ΔB)。ΔB=standing_panel 条件別経験分布。席数 K∈{12,18,24} 並走。RiskRewardAsymmetry 定義固定(主=q1−q6, 副=(q1−q2)−(q5−q6))。他者情報は day-start 固定。主指標 = ΔNLL(G1-G3)と市場edge(G5)の2軸を事前分離 | バイナリ圏内/圏外・現在ボーダーギャップ市場残差の同一形再提案禁止(null 済)。day-start 規約違反は即棄却 | registered |
| **NG-E5W** | 風コース成分(wind_along / wind_cross)。6.5年未使用の風向を場別コース方位テーブル(half-auto 完成)で座標変換 | race-level 2本の薄層 ΔNLL≥0.003 → 特徴昇格は CI95 両fold。プラセボ①場×月内 permutation ②季節クリマトロジー置換(場×月平均に置換して効果残存なら棄却)。採否評価はクリーン行(icon/bi由来)のみ・K回転行は wx_src=k_rotated で研究限定 | fold間符号反転 = 即棄却。符号の物理仮説は固定しない(two-sided) | registered |
| **NG-E19SG** | SG/G1 祭り日の市場効率 segment。一次証跡 = SG桐生 8/30(AI NLL 0.818 vs 市場 0.981・n=12逸話) | grade segment 別のモデル vs 市場 NLL/Brier 差(two-sided・登録済み1本)。SG/G1 開催日 vs 一般。real=締切前オッズ(national_v2 2026-07-10..)、確定オッズ使用時は diagnostic 明示。副次 = 織り込み済み棄却群(戦型/番組格差/F持ち/1-4-5)の SG 限定再判定(BH) | 前後半符号再現なしは探索止まり。ROI/EV 主張は real のみ | registered(常時) |
| **NG-E8SWAP** | 当地デッドウェイト3本の置換 ablation(起票のみ) | (実行時定義)当地系3本の除外/置換 2fold NLL。着手条件: Local×難水面3セル(W2-4)が全滅した場合のみ | −(登録上未定義) | filed(実行しない) |

---

## 5. 市場アノマリー3テーマ(事前登録済み・holdout 封印中)

- 登録書: `artifacts/research/mkt/preregistration_20260806.md`(2026-08-06 登録・**以後変更禁止**)
- **holdout 封印: 2026-09-01〜10-31。集計・閲覧は 2026-11-01 以降まで禁止**。in-sample 窓 = 収集開始〜2026-08-31。in-sample で閾値調整しても holdout は登録書の閾値のみで判定
- 大原則: 全テーマ「市場の歪みの存在検証」まで。**ROI/回収率の主張は strict_odds_replay を別途通すまで禁止**。bootstrap は seed=20260806・レース単位 cluster・10,000回

| テーマ | 仮説(検証可能形) | 判定基準(登録済み) |
|---|---|---|
| 1. 締切直前のオッズ急変 | 直前に単勝 implied が急上昇した艇(r≥log(1.30)・p≥0.02)は同人気帯の非急変艇と成績が異なる(賢い金/遅い金・両側) | in-sample と holdout の両方で同符号かつ cluster bootstrap CI95 が 0非跨ぎ。片方のみは「示唆どまり」 |
| 2. 系統的過剰/過小人気セル | 場(24)×R番号(12)×人気帯(3)の864セルで1番人気の較正ギャップが系統的に非ゼロ | n≥30 セルに BH-FDR 0.05 → 通過セルが holdout で同符号+素の p<0.05 を再現した場合のみ「系統的乖離あり」 |
| 3. 荒れ予報🔴ゾーン × 市場 | AI 荒れ指標(1−p_top18・オッズ不使用)と市場由来同型指標は荒れ予見の精度・利用可能時刻が異なる | CI 0跨ぎ=同等、非跨ぎ=優劣報告。in-sample→holdout の2段判定(テーマ1と同一) |

- 経緯メモ(HANDOFF より): 奇数分仮説は不支持で終了。テーマ3は in-sample 窓が 8/31 までのため「8/31 以降に一発本番」が推奨のまま shin 未回答。較正激変(7/20型レジーム)はテーマ3が事実上の追跡。W1 実験の検証期間はこの holdout に重ならないよう 2026-07-27 以前で切る

---

## 6. 市場・収益系実験(registry 記載・儲ける力レーン・完了分)

いずれも確定オッズ近似(0.75/imp)ベース = **diagnostic**。ROI 数値は実弾根拠にしない。

### EXP-001 — オッズ執行パネル + スリッページ(2026-07-23・done_primary)

- **仮説/内容**: 締切までの残時間別にオッズ比分布を実測(データ分析・モデルなし。timeseries 2026-04-26..07-22, jcd 01/12)
- **結果**: 単勝本命帯は median で上振れ・q25 で −13〜26%。3連単は30分前判定で median EV 0.916 = **楽観バイアス確定**、5分前で収束
- **判定**: 採用(知見)。conservative EV 移行を勧告
- **考察**: final=last snapshot / deadline=freeze-point proxy の近似前提

### EXP-004 — 購入領域の局所較正(2026-07-23・done_exploratory)

- **仮説/内容**: 購入領域の過信を乖離帯別に較正(6年 diag recs 住之江・LGB fold-pure quarterly)
- **結果**: 購入領域は全帯で約2倍過信。α(実在乖離率)=0.10(gap<0.23)→0.267(0.23+)。較正後 EV≥1.15 の95本は ROI 1.746(**in-sample fit = 探索扱い**)
- **判定**: 探索として採用 → walk-forward 確認を EXP-002 へ統合
- **考察**: ROI 1.746 は EXP-002 で in-sample 楽観と確定(下記)

### EXP-002 — nested threshold 検証 + cluster bootstrap(2026-07-23・done)

- **仮説/内容**: 閾値選択の nested 検証(outer 2024H1..2026H1 の5期間・date-cluster CI5%)
- **結果**: R023 が 5/5 期間で内側選択 = 安定。**outer pooled ROI 1.325 だが cluster CI 下限 0.943 < 1.0 = 収益証明未達**。RCAL(EXP-004 較正選別)は全敗 = ROI 1.746 は in-sample 楽観と確定。配当集中 53-93%
- **判定**: R023 をライブ凍結候補に採用 / RCAL 選別は棄却 / 実弾条件(cluster CI>1.0)未達を明記
- **考察**: オッズ近似 0.75/imp・確定オッズ diag。締切前オッズでの本測はライブ蓄積(national_v2 2026-07-10〜)で行う

---

## 7. 横断メモ(数値の読み方)

- 採用ライン(薄層): ΔNLL ≥ **0.003**(参考: exh120 −0.018 / extra3 −0.004〜0.007 / 棄却薄層群 −0.0006〜0.0011)
- 市場との残距離: NLL +0.06〜0.07(確定オッズ de-vig 比・**diagnostic**)。SG桐生 8/30 の AI NLL 0.818 vs 市場 0.981 は **n=12 の逸話**(能力断定禁止)
- 棄却の3類型を必ず明記: ①効果不在(CI跨ぎ)②実在するが焼き直し(統制で消滅)③実在するが織り込み済(市場残差ゼロ)。②③は Pattern Library に記録し廃棄しない



# ===== HYPOTHESES.md =====

# HYPOTHESES — 研究仮説台帳(正本)

- 最新更新: **2026-09-04**(更新者: Claude / セッション: v2.1 freeze)
- 位置づけ: Canonical Research State の一部。機械可読の骨格 = `research_state.json` の `hypotheses` 節(矛盾したらそちらが正)。表示用 view = 研究コンソール(Artifact)
- **目的**: shin(Owner)の現場感覚・人間の定説・データ由来の仮説を全て1つの台帳に載せ、「どの感覚が確認され、どれが否定されたか」を一目で分かるようにする
- 正直ラベルの規約: 小標本は「逸話」、確定オッズ由来は「diagnostic」、事後発見は「再登録要」と必ず付記。数値は出典ファイルから転記(捏造禁止・無い値は「記録なし」)
- 分類: **UNTESTED**(未検証)/ **TESTING**(事前登録済みで検証枠にある)/ **SUPPORTED**(支持)/ **PARTIALLY SUPPORTED**(部分支持)/ **REJECTED**(否定・同一形の再提案禁止)

---

## 一覧表(30秒版 — shin の感覚はどこまで確認されたか)

| # | 仮説(短縮) | 状態 | 一言証拠 | 次 |
|---|---|---|---|---|
| S-1 | 市場は本命を過小評価する | ✅支持 | implied 0.5+で−2.9pp(diagnostic) | 締切前オッズで再確認 |
| S-2 | 1号艇は全階級で買い得 | ✅支持 | B2級ですら−4.0pp | 同上 |
| S-3 | レースの格で走りが変わる | ✅支持(未特徴化) | 準優ST−0.0094・24/24場同符号 | NG-E1 |
| S-4 | 乖離は0.23を境に損益反転 | ✅支持(diagnostic) | 3独立証拠・ROI1.325(CI下限0.943) | 締切前オッズ本測 |
| P-1 | 勝負駆けで走りが変わる | 🌓部分 | バイナリは統制後消滅 | NG-E23(utility curve) |
| P-2 | F明けの1号艇は弱い | 🌓部分 | 現象−10pp実在・特徴化は無効 | Pattern Library 保持 |
| P-3 | 節内の勢いは終盤ほど効く | 🌓部分 | 素材7特徴は採用済・交互作用未分離 | 未起票 |
| T-1 | AIはまくり筋の荒れを見落とす | 🔄検証中 | +29%・z≈8.4(事後発見) | NG-E10 |
| T-2 | SG/G1は市場が甘くなる | 🔄検証中 | AI NLL 0.818 vs 市場0.981(n=12逸話) | NG-E19SG |
| T-3 | 4カド攻撃型は5・6に展開を作る | 🔄検証中 | 汎用タグは織り込み済・選手固有は空白 | NG-E10 |
| T-4 | 特定選手が隣の艇を殺す/活かす | 🔄検証中 | 選手個人単位は完全な空白 | NG-E10 |
| T-5 | 風はコース成分に分解すると効く | 🔄検証中 | 風向6.5年未使用・方位表完成 | NG-E5W |
| U-1 | 安定板+強風=イン受難 | ⬜未検証 | 尼崎3R連続一貫(n=3逸話) | 未起票 |
| U-2 | 地元経験は難水面でこそ効く | ⬜未検証 | 無条件当地はゼロ効果済 | E7+E8(W2) |
| U-3 | 部品交換は選手の潜在診断信号 | ⬜未検証 | パーサ修理待ち | W2修理→W3 |
| U-4 | 師弟・先輩後輩で行動が変わる | ⬜未検証 | 記録なし | W3以降(DEFER) |
| U-5 | ルーキー急成長を市場が遅れて評価 | ⬜未検証 | 記録なし | 未起票 |
| U-6 | 気温・気圧でモーター性能差が変わる | ⬜未検証 | 素値は棄却済・差分系のみ可 | E6(W2) |
| U-7 | 準優は2着保持が重要 | ⬜未検証 | ST変化の傍証のみ | E23後続(準優δ) |
| U-8 | 攻め気配で荒れを検知できる | ⬜未検証 | 展示補正は方向11/12正・量が保守的 | backlog 1-6→E12-14 |
| U-9〜U-13 | 市場残差学習/オッズ時系列/本命エッジ移植/不一致フィルタ/条件別較正 ほか | ⬜未検証 | 各項参照 | backlog 2-2/2-3/2-4/3-3/1-5 |
| U-14 | 高チルトは成功/失敗で影響反転 | ⬜未検証 | 記録なし(v2.1プロンプト由来) | 未起票 |
| U-15 | 元トップは名前で人気過大 | ⬜未検証 | 記録なし(v2.1プロンプト由来) | 未起票 |
| R-1 | 階級が予測に効く | ❌否定 | 全棄却(2026-06確定・再投入禁止) | — |
| R-2 | 高階級は市場で人気過剰 | ❌否定 | 全級±0.7pp=正確に織り込み | — |
| R-3 | 満潮=まくり有利 | ❌否定 | 実測は逆方向 | 再解釈のみ |
| R-4 | 汎用の攻撃タグ/番組格差/1-4-5筋にエッジ | ❌否定 | 実在するが市場織り込み済み | 選手固有はE10 |
| R-5 | 気温・水温の素値が効く | ❌否定 | 8-9割が季節の焼き直し | 差分系のみ(U-6) |
| R-6 | 当地・地元は無条件で効く | ❌否定 | ablationデッドウェイト | 条件付きはU-2 |

---

## 1. UNTESTED(未検証 — 感覚・逸話のまま。データでの検証はこれから)

### 1-a. shin の現場感覚系(憲章§62「人間の仮説は検証対象」)

#### U-1. 安定板+強風=イン受難(荒天ほど地力差が出る)
- 仮説文: 安定板使用+風5m級の荒天では、イン(1号艇)が受難し地力のある艇が浮上する
- なぜ有望か: 尼崎実弾(2026-08-26/27)で作業仮説が3レース連続一貫(8R的中・10R回避判断正解)。かつ AI は風・波は見るが「安定板使用」自体を特徴に持たない=織り込み不足が構造的に存在(`lane-reports/hansei_sg_kiryu_20260903.md` §5)
- 必要データ: beforeinfo の安定板フラグ(バックフィル済み・未特徴化。`lane-reports/nextgen_audit_20260903.md` §3B)+ 風速
- 現在の証拠: 尼崎3R連続で一貫(**n=3 逸話** — `research_state.json` untested)
- サンプル規模: n=3(判定に使用禁止)
- 確信度: 低(逸話のみ。ただし「AIが安定板を見ていない」事実は監査で確定)
- 次のアクション: 未起票(E5系環境実験の副次仮説として起票候補 — 監査§6 E5b の stabilizer 項)

#### U-2. 地元経験は難水面でこそ効く(無条件では効かない)
- 仮説文: 当地・地元の優位は平常時には存在せず、強風・高波・難場など「難条件」でのみ発現する(Local×難水面の条件付き効果)
- なぜ有望か: 既存の当地4特徴は ablation でデッドウェイト(寄与ゼロ〜微マイナス、`docs/MODEL_STRATEGY.md` §3)= 無条件平均は否定済み。憲章§18-19 は地元優位を「水面への慣れ/風への適応/調整知識」等に分解し、難条件でだけ効くなら平均に埋没する構造を指摘
- 必要データ: 既存データで構築可 — is_local_branch(支部県=開催県。**支部→県マップはリポジトリ内に無し・24行手作業**)/ career_races_at_track / track_residual_performance 等(監査§8)
- 現在の証拠: 無条件形はゼロ効果済み。条件付き形は記録なし
- サンプル規模: 検証未実施
- 確信度: 低〜中(構造仮説としては筋が良いが、細分によるサンプル枯渇が既知の危険地帯)
- 次のアクション: **E7+E8(W2)** — 難条件の操作的定義3本のみ事前登録(強風≥6m / 波≥5cm / 難場5場=KMeans客観化)、回帰の交互作用項で検定。全滅時は NG-E8SWAP(当地3本の置換 ablation・起票のみ済)が受け皿

#### U-3. 部品交換は選手の潜在診断信号
- 仮説文: 部品交換(リング/ピストン等)は「機体に問題がある」という選手自身の診断の表明であり、Problem/Intervention/Response の系列として着順に効く
- なぜ有望か: SG週の shin 現場観察(ピット速報・整備コメントを読みに使えた)+ 憲章§22-26 の Maintenance/Adjustment Expert 構想。市場が精読していない可能性のある一次情報
- 必要データ: beforeinfo 部品交換(非空56.3%だが値が 'R2' 等=**パーサ取り違え疑い・修理必須** — 監査§3B)+ 節内 Motor State 基盤
- 現在の証拠: 記録なし(データ自体が修理待ち)
- サンプル規模: 検証未実施
- 確信度: 低(未検証。「調整の流れ」系は平均回帰で棄却済みの前例があり、exh120 補正後の残差で増分を出す必要 — 監査§10)
- 次のアクション: W2 でパーサ修理 → W3(`docs/ARCHITECTURE_FREEZE_v2.1.md` D表 Maintenance/Adjustment = NEW)

#### U-4. 師弟・先輩後輩で行動が変わる(人間関係・知識伝播)
- 仮説文: 師弟・同支部・同期などの関係が同乗レースでの行動(忖度・道の譲り方・攻めの選択)や、調整知識の伝播を通じた成績に影響する
- なぜ有望か: shin の SG週の気づき「選手個人のプロファイリング(性格・戦略込み)」の延長。憲章§28-30 が Relationship/Familiarity を研究ブロック化
- 必要データ: 同走回数・支部(branch 18値・全行あり)は既存。師弟・練習グループは **Wish List(公開情報の構造化・MED)** — `research_state.json` data_status
- 現在の証拠: 記録なし
- サンプル規模: 検証未実施
- 確信度: 低(検証形は「行動残差」のみで理由断定せず、と freeze D表に明記)
- 次のアクション: W3以降 [B/C](NEW/DEFER)。実験ID未付与

#### U-5. ルーキー急成長を市場が遅れて評価する
- 仮説文: 急成長中の若手・ルーキーの実力向上を市場オッズが遅れて織り込むため、成長速度の速い選手に+EVが残る
- なぜ有望か: Player Evolution(成長/衰え/転機 — 憲章§10-12)の市場側の帰結。市場は「階級を正確に織り込む」ことが実証済みだが(R-2)、「変化速度」への追従はまた別の問題
- 必要データ: skill trend/velocity/change-point 特徴(W2 E9系・未実装 = recent form スカラーのみ)+ 締切前オッズ(2026-07-10〜蓄積中・期間浅い)
- 現在の証拠: 記録なし
- サンプル規模: 検証未実施
- 確信度: 低(逆風: 市場の階級織り込みは正確だった前例。ただし静的ラベルと動的変化は別物)
- 次のアクション: W2 E9系(Player Evolution)の市場残差サブ検定として起票候補。実験ID未付与

#### U-6. 気温・気圧・湿度の変化でモーター性能差が変わる(Motor×Env)
- 仮説文: 機体ごとに環境感応度(気温・気圧・空気密度への slope)が異なり、環境偏差×機体感応度が着順に効く
- なぜ有望か: 憲章§62「気温・気圧変化でモーター性能差が変わる」+ §49 Motor Signature 構想。ERA5 パネル(2020〜毎時24場・140万行)整備済みで材料が揃った。1物理機≈200走・11ヶ月=フル季節レンジを経験するため原理的に推定可能(監査§10)
- 必要データ: ERA5(済)+ モーター交換月テーブル(K 2連率リセット検出で全24場確定済 — `research_state.json` supported_findings)+ (jcd, motor_no, 年度) キー設計
- 現在の証拠: 記録なし(**素値の直接投入は R-5 で棄却済み** — 差分・slope 系のみ許可)
- サンプル規模: 検証未実施
- 確信度: 低〜中(季節直交化が生命線。x は場×月の気候平均を引いた偏差で入れる)
- 次のアクション: **E6(W2・E5 PASS 後)** — as-of 縮約 slope 特徴・積項禁止

#### U-7. 準優では2着保持が重要(守りの走りへの切替)
- 仮説文: 準優勝戦は「2着まで確保すれば優出」の構造のため、選手が2着保持の走り(無理をしない・差し受け)に切り替え、着順分布が予選と系統的に異なる
- なぜ有望か: 憲章§62 の明示リスト項目。傍証として格による行動変化は実証済み(準優ST−0.0094・1号艇逃げ率46.7→71.3% — S-3)だが、「2着保持」という着順形状の変化そのものは未検証
- 必要データ: setsu_master(5,311節・済)+ standing_panel(済)+ Stage 分類器(E1)
- 現在の証拠: 直接の検証記録なし(格によるST/逃げ率変化はあくまで傍証)
- サンプル規模: 検証未実施
- 確信度: 中(行動変化の実在は確定しており、その内訳仮説として自然)
- 次のアクション: E23 後続の「準優 Player×Stage utility(準優δ)」(監査§9 の順序: E1→E2→準優δ→Motor State)

### 1-b. 市場・EV系(ANALYSIS_BACKLOG 由来)

#### U-8. 攻め気配(展示ST前傾×外枠等)で荒れレースを検知できる
- 仮説文: exh120 層は方向精度が高いが増幅が保守的で、「攻め気配」(展示ST前傾の外枠・チルト上げ等)を条件にした荒れ検知で p120 順位が改善する
- なぜ有望か: 桐生SG 8/30 答え合わせ — 展示反映が勝者確率を 11/12 で正方向に動かしたが、荒れ3R(配当¥6,670〜14,800)は方向が合っても量が不足(例: 1R 4号の展示ST −0.02 の攻め気配に +0.2pp しか反応せず)— `docs/ANALYSIS_BACKLOG.md` 1-6
- 必要データ: 展示ST・チルト(充足95.1%)・進入(いずれも既存)
- 現在の証拠: 方向性の逸話のみ(11/12・n=12)。条件別残差の測定は未実施
- サンプル規模: n=12 逸話(検証は全期間データで可能)
- 確信度: 中(方向の実在は観測済み。ただし「展示の攻め気配は市場も同時に見ている」で終わるリスクを failure 条件に明記済み)
- 次のアクション: backlog 1-6 → 憲章§26 Intent 層の統計前段(**E12-14 / W2**・2重ゲート: 行動予測→着順上乗せ)

#### U-9. 市場残差学習が素の乖離判定を上回る(本命の一般解)
- 仮説文: 市場 implied prob を出発点(事前分布)にし、AI は超過分(残差)だけ主張する方が、過信が減り CI 下限問題に効く
- なぜ有望か: 市場との残距離 NLL +0.06〜0.07 = 市場情報のほぼ全てを独自再構成できている位置。ならば「市場+増分」の形が効率的(backlog 2-2 ★本命の一般解)
- 必要データ: 締切前オッズ蓄積(national_v2 2026-07-10〜)。確定配当混入は即リーク=厳禁
- 現在の証拠: 記録なし(市場ブレンド w=0.85 の採用が間接傍証: AI は市場への増分情報を持つ)
- サンプル規模: 検証未実施
- 確信度: 中
- 次のアクション: backlog 2-2。実験ID未付与(蓄積量が前提)

#### U-10. オッズ時系列=金の動きが情報(賢い金は直前に入る)
- 仮説文: オッズの変化速度・加速度(特に締切直前)が情報を持つ
- なぜ有望か: 締切5分前で乖離の73%が蒸発する実測(backlog 2-3)+ EXP-001: 3連単は30分前判定で median EV 0.916=楽観バイアス確定・5分前で収束(`artifacts/research/experiment_registry.jsonl` EXP-001)
- 必要データ: national_v2 の5分毎スナップショット時系列(蓄積中)
- 現在の証拠: 上記2点(いずれも「直前が正確」の証拠であり「速度が予測に効く」の証拠ではまだない)
- サンプル規模: EXP-001 = timeseries 2026-04-26〜07-22(jcd 01,12)
- 確信度: 低〜中
- 次のアクション: backlog 2-3(まず「直前変化量」1本から)。実験ID未付与

#### U-11. 本命過小エッジは流動性券種(3連単/2連単)に移植できる
- 仮説文: S-1 の「本命(1着)過小人気」は、1着固定の3連単/2連単で活かせる
- なぜ有望か: 単勝は自己購入でオッズを崩す(流動性低)ため、実運用は3連単主体になる方針(backlog 2-4b・shin 感覚 2026-07-12)
- 必要データ: 締切前オッズ(確定オッズは市場最効率=最悪条件)
- 現在の証拠(一次診断・**diagnostic**): isotonic 較正(fold-pure)で穴過大は是正されたが Brier 未改善(市場 0.00792 に未達)。確定オッズ上では本命ルート ROI 0.82 / AI-EVルート 0.71 CI[0.41,1.06] と**壁未達**(`docs/ANALYSIS_BACKLOG.md` 2-4)
- サンプル規模: 6年 diagnostic
- 確信度: 低(一次診断は不利条件下で未達。締切前オッズでの本測待ちで**⏸保留**)
- 次のアクション: backlog 2-4(national_v2 蓄積待ち)。教訓済み: 乖離は ai/de-vig 比でなく実EV=ai×生オッズで測る

#### U-12. モデル間不一致は「質の低い+EV」の検知器になる
- 仮説文: NN/LGB/PL で確率が大きく割れるレース=自信がないレースで、的中率/ROIが低い → 見送りフィルタに使える
- なぜ有望か: 買い目を減らすのではなく質の低い+EVを外す(CLAUDE.md §11 思想と一致)
- 必要データ: 既存モデル群の確率 dump
- 現在の証拠: 記録なし
- サンプル規模: 検証未実施
- 確信度: 低
- 次のアクション: backlog 3-3。実験ID未付与

### 1-c. モデル・較正系

#### U-13. 較正は条件別(オッズ帯/コース/荒天)にズレている
- 仮説文: 全体較正(T≈1.0)は帯別に見るとズレており、低確率帯・6コース・荒天で乖離判定が壊れている
- なぜ有望か: 較正の全体値と局所値は別物。EXP-004 の傍証: 購入領域は全帯で約2倍過信(in-sample・探索扱い)
- 必要データ: 既存 fold dump のみで可
- 現在の証拠: EXP-004(探索・in-sample)のみ。条件別 ECE の正式測定は記録なし
- サンプル規模: 検証未実施(正式には)
- 確信度: 中
- 次のアクション: backlog 1-5 + 3-1 → **W2 の領域別(Core/Secondary/Tail/ExtremeTail)較正**(freeze D表 Calibration/Tail = EXTEND→NEW)

#### U-14. コース×フォームの重み最適化で底上げできる
- 仮説文: 最強単変量シグナル「コース別直近20走勝率」(AUC 0.786・7/8診断)の重み・相互作用の最適化で改善余地がある
- なぜ有望か: backlog 1-1(2026-07-12 議論)。ただし以後の実験史で「モデル改造12連敗・情報追加のみ有効」が確定しており、重みいじり系は分が悪い
- 必要データ: 既存
- 現在の証拠: 記録なし(直近5走系が ablation 寄与①位という傍証はあり)
- サンプル規模: 検証未実施
- 確信度: 低(実験史の憲法に照らし優先度低)
- 次のアクション: 未起票(着手するなら G0 事前登録から)

#### U-15. 展開パターンの事前分類(展開クラスタ条件付き着順)
- 仮説文: 逃げ/差し/まくり/まくり差しの「なりやすさ」を事前情報のみで推定し、展開クラスタ条件付きの着順分布にすると精度が上がる
- なぜ有望か: 実例(2026-07-25 住之江4R): shin の展開読み「4カド攻め→3潰れ→5連れ込み=1-4-5」が的中。B2 は4絡みまで出したが3着連れ込みは出せず=「攻める意図の入力」+「展開因果の明示」の2欠落が明確化(backlog 1-4)
- 必要データ: 決まり手(209万行・ラベル用)+ 事前展開特徴(進入予想は C-6 stub のため不可)
- 現在の証拠: 逸話1件+決まり手予測のレース前情報純増は3.1%のみという上限の既知値(監査§14)
- サンプル規模: 検証未実施
- 確信度: 低〜中(「市場織り込み済み」再発見リスク最大のテーマと監査が明記)
- 次のアクション: **E16(W3・1M Scenario)** — まくり筋等 E10 で特定された歪みセル限定の混合が第一仕様

### 1-d. v2.1 プロンプト由来の新仮説(2026-09-04 freeze セッションで Owner が提示。リポジトリ内に一次記録なし)

#### U-16. 高チルトは成功/失敗で影響が反転する
- 仮説文: チルトを上げた(伸び型に振った)艇は、攻めが決まれば大きく展開を作るが、失敗すれば自艇もろとも沈む — 影響の符号が成功/失敗で反転するため、平均を取ると効果が消えて見える
- なぜ有望か: E10 の「4カド外恩恵」設計(ATTACK_SUCCESS / ATTACK_FAIL proxy の分離 — 監査§13)と同型の構造。平均で消える効果は既存特徴に乗らない
- 必要データ: チルト(beforeinfo 充足95.1%・未特徴化)+ 決まり手/着順ラベル
- 現在の証拠: 記録なし
- サンプル規模: 検証未実施
- 確信度: 低(感覚のみ)
- 次のアクション: 未起票(E10 の成功/失敗分離フレームの拡張として起票候補)

#### U-17. 元トップ選手は名前で人気過大になる
- 仮説文: かつての実績が大きい選手(元SG覇者等)は、現在の実力に対して市場が名前で過大に売れる(=消し・裏の妙味)
- なぜ有望か: 市場の心理バイアス系。ルーキー遅行(U-5)の鏡像
- 必要データ: 締切前オッズ + 選手キャリア実績時系列(全国勝率のピーク比等)
- 現在の証拠: 記録なし。**逆風の前例あり**: 市場は階級ラベルを正確に織り込む(R-2)— ただし「過去の栄光」への過剰反応は静的ラベルと別物
- サンプル規模: 検証未実施
- 確信度: 低
- 次のアクション: 未起票(市場残差系の副次検定として起票候補)

---

## 2. TESTING(事前登録済みで検証枠にある — 実行中の実験は現在なし)

#### T-1. AIはまくり筋の荒れを系統的に見落とす ★唯一の生存歪み
- 仮説文: まくり・まくり差しで決まる組をモデルが系統的に過小評価している
- なぜ有望か: **唯一どの補正でも生き残った歪み**(+0.001416・z≈8.4・AI相対+29%見落とし)。SG桐生 8/30 で外した3R(1R/3R/4R・配当¥6,670〜14,800)が全部まくり/差し系だった現場実感と一致(`docs/ARCHITECTURE_FREEZE_v2.1.md` §G / `lane-reports/hansei_sg_kiryu_20260903.md`)
- 必要データ: すべて手元(B2残差+全期間結果)。学習ゼロ・統計のみ
- 現在の証拠: +0.001416, z≈8.4, 相対+29%(**事後発見のため未採用 — 事前登録での再検証が必須**)
- サンプル規模: 全期間(z値は大標本由来)
- 確信度: 中〜高(効果量・再現の枠組みは強いが、事後発見バイアスの可能性を潰すまで断定しない)
- 次のアクション: **NG-E10**(registered・2026-09-03)— 前半抽出→後半+P2符号再現・CI95 0非跨ぎで確定

#### T-2. SG/G1 は観光マネーで市場が甘くなる(祭りの市場効率低下)
- 仮説文: 大型開催は場外流入の観光マネーが穴に散り、本命過小(favorite-longshot)が普段より増幅 → AI の相対エッジが拡大する
- なぜ有望か: SG桐生 8/30 実測 — 勝者への確率で AI>市場 11/12、NLL AI 0.818 vs 市場 0.981。AI 74-81% の鉄板を市場は 57-67% でしか売っていなかった(R5/R8/R9)。S-1 の条件付き増幅版(`lane-reports/hansei_sg_kiryu_20260903.md` §3 仮説A)
- 必要データ: 締切前オッズ(national_v2 2026-07-10〜・期間浅い)+ グレードラベル(月間開催日程ページ・取得可能確認済)
- 現在の証拠: **n=12・1日ぶんの逸話(断定禁止)**。単勝診断は AI頭で ROI 0.86 = 頭当てだけでは控除の壁は越えない、も併記
- サンプル規模: n=12 逸話
- 確信度: 低(効果は鮮明だが1日ぶん)
- 次のアクション: **NG-E19SG**(registered・常時)— two-sided・ROI/EV 主張は real(締切前)のみ。副次: 織り込み済み棄却群(戦型/番組格差/F持ち/1-4-5)の SG 限定再判定

#### T-3. 4カド攻撃型は5・6に展開を作る(外恩恵・選手固有の条件付き)
- 仮説文: 4カドに攻撃型の**特定選手**がいるとき、5・6コースに展開(外恩恵)が生まれる — 汎用タグでなく選手固有の現象として
- なぜ有望か: 汎用の攻撃タグ・1-4-5筋は「実在するが市場織り込み済み」で死んだ(R-4)。しかし**選手個人単位は完全な空白**(監査§13)。攻め失敗でも外恩恵があるか(ATTACK_FAIL proxy)の分離が新規性
- 必要データ: 手元(as-of まくり率@C4 等の事前プロファイル+事後ラベル)
- 現在の証拠: 汎用形の棄却記録のみ。選手固有形は記録なし
- サンプル規模: 検証未実施(選手固有形)
- 確信度: 低〜中
- 次のアクション: **NG-E10** の specific 分析(段A=攻め失敗でも外恩恵があるか/段B=AIは見落とすが市場は織り込むかの判定)

#### T-4. 特定選手が隣接コースを系統的に殺す/活かす(選手 externality)
- 仮説文: 「特定イン選手が2コースを殺す」「特定3コース選手が2・4両方に圧力」など、選手×コースが隣接艇の結果に与える系統的な影響(externality)が実在する(憲章§62)
- なぜ有望か: v2.1 の心臓「6艇 interaction」がそもそも実在するかを、学習ゼロ・モデル無改変で判定できる。不在なら GAT/Interaction 系を全中止でき最大の無駄を防ぐ(freeze §G)
- 必要データ: 手元(P1=LGB expanding crossfit 残差パネル+P2=fold2 バンドル推論 dump)
- 現在の証拠: 記録なし(死んだのは汎用タグ・ペア力学であり、選手個人単位は空白)
- サンプル規模: 検証未実施
- 確信度: 不明(だからこそ最初に測る — Expected Information Gain 最大)
- 次のアクション: **NG-E10** 層1 = 分散成分検定(選手ラベル並べ替え帰無)の Yes/No 主判定。不通過なら N1 以降(GAT系)を全中止
- ※ `research_state.json` の hypotheses には未収載(T-1/T-3 と同じ NG-E10 傘下のため本台帳で補完)

#### T-5. 風はコース成分(向かい/追い/横)に分解すると効く
- 仮説文: 風向をコンパス方位でなくコース座標系の成分(wind_along / wind_cross)に変換すれば、6.5年分未使用だった風向が予測情報になる
- なぜ有望か: 風向は本番全行 −1 の死に特徴=最大級の情報空白(監査§5)。風向アイコン解析の副産物で24場コース方位テーブルが半自動推定済み(high19/mid5)=変換の前提が完成(`research_state.json` static_assets)
- 必要データ: venue_course_azimuth.json(済)+ K/beforeinfo 風向(済)。採否評価はクリーン行(icon/bi由来)のみ
- 現在の証拠: 記録なし(効果自体は未測定)。符号の物理仮説(「向かい風=まくり有利」等)は**固定しない**(満潮定説が逆だった前例 — R-3)
- サンプル規模: 検証未実施
- 確信度: 中(情報の実在は確実・効くかは季節プラセボ次第 — 気温水温の轍)
- 次のアクション: **NG-E5W**(registered)— 薄層ΔNLL≥0.003・プラセボ2種(場×月内permutation+季節クリマトロジー置換)
- ※ `research_state.json` の hypotheses には未収載(実験は registered_waiting に収載済みのため本台帳で補完)

---

## 3. SUPPORTED(支持 — データが shin の感覚/定説を確認したもの)

#### S-1. 市場は本命を過小評価する(favorite-longshot)
- 仮説文: 市場は本命を過小に、穴を過大に売る(教科書的 favorite-longshot バイアス)
- なぜ有望と思ったか: 出発点は「A1人気しすぎ」の現地観察(→そちらは R-2 で否定)。診断の副産物として本命側の歪みが出た
- 必要データ: 確定オッズ+AI確率(取得済み)
- 現在の証拠: implied 0.5-0.7 で −2.9pp、0.7+ で −2.8pp 過小人気。中穴 0.1-0.2 は +0.9pp 過大(`docs/ANALYSIS_BACKLOG.md` 2-1 / lane-reports/favorite_longshot_diag_20260712.md)
- サンプル規模: 6年 diagnostic(**確定オッズ=diagnostic・3連単合成1着prob**)
- 確信度: 高(方向は堅い)— ただし締切前オッズ&単勝での再確認が残る(caveat 併記済み)
- 次のアクション: 締切前オッズでの再確認(U-11 と同じ蓄積待ち)。SG限定の増幅は T-2

#### S-2. 1号艇は全階級で買い得(イン利は階級を超える)
- 仮説文: 1号艇の過小人気は選手の階級によらず存在する
- なぜ有望と思ったか: S-1 の層別で発見(favorite-longshot 診断の派生)
- 現在の証拠: B2級ですら −4.0pp の過小人気(同上 2-1)
- サンプル規模: 6年 diagnostic(確定オッズ)
- 確信度: 高(同上の caveat)
- 次のアクション: なし(判断材料として確立。実弾は 2026-08-10 決定で対象外)

#### S-3. レースの格で走りが変わる(準優・優勝戦は別のレース)
- 仮説文: 同じ選手・同じコースでも、レースの格(予選/準優/優勝戦)で ST・逃げ率など走り自体が変わる
- なぜ有望と思ったか: shin が SG現場で見ていた「条件が絡む場面の心理」の機械化候補。憲章§62 の「予選最終日は勝負駆けで攻撃性が変わる」と同根
- 必要データ: レースタイトル=Stageラベル(予選126,105 / 準優14,735 / 優勝戦5,292 行・完全未使用だった)
- 現在の証拠: ST変化 準優 −0.0094秒 / 優勝戦 −0.0065秒・**24/24場同符号**・1号艇は −0.0203。1号艇逃げ率 予選46.7%→準優71.3%(`lane-reports/nextgen_audit_20260903.md` §9)
- サンプル規模: 全期間・24場一貫
- 確信度: 高(現象として)。**ただし格カテゴリは F=41 未収載=モデルはまだ知らない**
- 次のアクション: **NG-E1**(registered)— 格カテゴリの特徴化(プラセボ=race_no単独版必須・本番昇格は ex-ante 判定器一致率≥98%)

#### S-4. 乖離は用量反応であり 0.23 を境に損益が反転する
- 仮説文: AI と市場の乖離が大きいほど的中率が単調に上がり、ROI は乖離0.23 を境に損益割れ→プラス圏に反転する
- なぜ有望と思ったか: 「真の+EVはAIと市場の divergence」という設計思想の実証(hit率改善≠ROI改善の市場効率仮説)
- 現在の証拠: 的中率5帯単調増加・0.23+ で n=268 ROI≈1.53(`docs/MODEL_STRATEGY.md` §3)。EXP-002 nested 検証: R023 が 5/5 期間で内側選択=安定、外側プール ROI 1.325。**ただし date-cluster CI 下限 0.943 < 1.0 = 収益証明は未達**・配当集中53-93%(`artifacts/research/experiment_registry.jsonl` EXP-002)
- サンプル規模: 6年・3独立証拠(用量反応+シャドウ2期間+第2アーム)
- 確信度: 中〜高(方向・再現は強い。**diagnostic: オッズ近似0.75/imp・確定オッズ。収益主張はしない**)
- 次のアクション: 締切前オッズでの本測(ライブ蓄積)。実弾化は 2026-08-10 決定で対象外
- ※ `research_state.json` hypotheses 未収載(supported_findings 系の統合として本台帳に収載)

---

## 4. PARTIALLY SUPPORTED(部分支持 — 現象は在るが、当初の形では効かない)

#### P-1. 勝負駆けで走りが変わる
- 仮説文(当初): 予選ボーダーの圏内/圏外(バイナリ)で選手の攻撃性が変わり、着順に効く
- なぜ有望と思ったか: 現場定説の筆頭。shin も SG現場で「点数条件・ボーダーでの選手の思考」を実感(hansei §4)
- 現在の証拠: **バイナリ圏内/圏外は統制後消滅**(生差の94-97%が交絡 — 監査§9)。現在ボーダーギャップの市場残差も null 済み(Bonferroni下)。一方、格による行動変化(S-3)は堅い=「勝負条件で走りが変わる」の骨格自体は生きている
- サンプル規模: 全期間(統制検定済み)
- 確信度: 中(バイナリ形は死亡確定・連続 utility 形は未判定)
- 次のアクション: **NG-E23**(registered)— utility curve 形式(q_k=P(projected_score_if_k≥B+ΔB)・全6艇)で再挑戦。ΔNLL と市場edge の判定2軸を事前分離(「NLLには効くが edge には効かない」着地を想定内に)

#### P-2. F明けの1号艇は弱い
- 仮説文: フライング休み明けの選手(特にイン)はスタートが慎重になり勝率が下がる
- 現在の証拠: 現象は実在 — **F後1号艇 −10pp**(subgroup 探索の数少ない生存例 — 監査§15)。しかし**特徴化は無効**: flying_events + extra4 builder で特徴化済み・2fold改善なしで不採用(監査§3A)
- サンプル規模: 大(全期間)
- 確信度: 現象=高 / 特徴としての価値=否定済み
- 次のアクション: Pattern Library 保持(棄却も削除しない)。個人別 F後ST変化(f_dynamics)は Intent 系 I-1 で別形の再挑戦が設計済み(監査§11)

#### P-3. 節内の勢いは節が進むほど効く(最終日は読みやすい)
- 仮説文: 節内成績(勢い)の予測力は節進行とともに強まる(憲章§62「最終日は節内情報が豊富で読みやすい」)
- 現在の証拠: 節内素材7特徴(setsu_day / setsu_prior_n/win/top2 等)は 2fold 一貫改善で**採用済み**(fold2 NLL 3.785→3.777)。節進行の診断値: 初日0.55→最終日0.63→優勝戦0.80(`docs/ANALYSIS_BACKLOG.md` 1-3)。ただし**明示交互作用の純増分・優勝戦交絡の分離は未実施**(明示積項は桐生教訓で見送り・attention に委ねる方式)
- サンプル規模: 全期間(素材の採用検定は bootstrap CI 済み)
- 確信度: 中(素材が効くのは確定・「進行で効き方が変わる」の純増分は未分離)
- 次のアクション: 未起票(E4 節内履歴系列は「exh120 が回収していない増分≥0.003 の証明」が起動条件 — 監査§21 W2-2)

---

## 5. REJECTED(否定 — 同一形での再提案禁止)

#### R-1. 階級(A1/B1)が予測に効く
- 仮説文: 級別ラベルは選手実力の要約として予測に有効
- 判定: **全棄却(2026-06 確定・class_code の再投入禁止)**。階級は実績判断に無関係 — 実績系特徴が全てを回収する(`research_state.json` rejected / dataset.py:16 で機械的除外)
- 正しい解釈(shin 言語化・hansei §4): ラベルが無意味なだけで、**選手個人を立体的に見る方向はむしろ本命**(→ Player プロファイリング系 T-4/U-4 へ)
- 残タスク: conditional_finish に class_code 残留(conditional_finish.py:32)— 再利用前に class 除外の再GATE 必須

#### R-2. 高階級は市場で人気過剰になる(A1は人気しすぎ)
- 仮説文: A1 等の高階級は名前で売れすぎ、相手・穴側に EV が移る(現地観察由来)
- 判定: **否定** — 級別の過剰人気は無し(**全級 ±0.7pp**)。市場は階級を正確に織り込む(backlog 2-1・2026-07-12)
- 教訓: 市場の静的ラベル織り込みは正確。歪みは階級軸でなく本命/穴軸(S-1)にあった
- サンプル規模: 6年 diagnostic

#### R-3. 満潮=まくり有利(定説)
- 仮説文: 満潮時は水面が柔らかくまくりが決まりやすい(業界定説)
- 判定: **実測は逆方向**(`research_state.json` rejected)。環境→行動の人間メカニズム仮説を固定しない根拠になった前例(E5W の two-sided 設計・監査§7)
- 次のアクション: 再解釈のみ(潮汐×Local 等の交互作用は未検証のまま残っている — 監査§3A)

#### R-4. 汎用の攻撃タグ/番組格差/1-4-5筋に市場エッジがある
- 仮説文: 決まり手スタイルタグ・番組の相手強度ギャップ・1-4-5 の筋に+EVが残っている
- 判定: **実在するが市場織り込み済み**(棄却の3類型③)。薄層検証で ΔNLL −0.0006〜0.0011(採用基準0.003未達)(`research_state.json` rejected: thin_layers_tide_style_gap)
- 教訓: hit率改善≠ROI改善(市場効率仮説)。**選手固有の条件付き**は未測=E10 で再挑戦(T-3/T-4)
- 付記: Intent の金銭化も現状0点(EV≥1.15 買い目 0/503,640 — 監査§11)

#### R-5. 気温・水温の素値が予測に効く
- 仮説文: 気温・水温はモーター性能に効くから直接入れれば当たる
- 判定: **棄却・再提案禁止** — F=43 で fold間符号反転・permutation で実体の8〜9割が季節の焼き直し(監査§6)
- 教訓: 以後「季節クリマトロジー置換プラセボ」を環境系の標準検査に昇格(E5W に実装済み)
- 生き残り: 差分・変化量系(air_water_gap・pressure_d3h)と Motor×Env slope(U-6)のみ新規性を認める

#### R-6. 当地・地元は無条件で効く
- 仮説文: 当地勝率・当地経験は普遍的に予測へ効く
- 判定: **無条件形は否定** — 既存当地4特徴は ablation で寄与ゼロ〜微マイナスのデッドウェイト(`docs/MODEL_STRATEGY.md` §3。除去も fold1 不再現で見送り=現状維持のまま)
- 構造仮説: ①全国勝率と水準重複 ②難条件でだけ効くなら無条件平均に埋没 ③「当地(経験量)」と「地元(支部)」の混同(監査§8)
- 次のアクション: 条件付き形(Local×難水面)は U-2 = E7+E8 で再挑戦。全滅時は NG-E8SWAP(置換 ablation・起票済み)

---

## 更新ルール

- 実験が決着するたびに該当仮説を移動し、`research_state.json` の `hypotheses` 節と**必ず同期**する(CLAUDE.md §19)
- 棄却された仮説も削除しない(棄却の3類型①効果不在②焼き直し③織り込み済み を明記して Pattern Library と相互参照)
- 事後発見は必ず「再登録→別期間確認」を経てから SUPPORTED に昇格(まくり筋方式)
- 新仮説の追加は G0 事前登録(`artifacts/research/experiment_registry.jsonl`)とセットで行う



# ===== FINDINGS.md =====

# FINDINGS — 研究発見台帳(Canonical Research State)

- 最終更新: 2026-09-04(v2.1 freeze セッション)
- 位置づけ: `research_state.json` / `RESEARCH_STATUS.md` と同期した人間可読の発見集。矛盾したら json 側が正
- 主な出典: `docs/ARCHITECTURE_FREEZE_v2.1.md` / `lane-reports/nextgen_audit_20260903.md` / `lane-reports/hansei_sg_kiryu_20260903.md` / `docs/experiments/structured_order_model/results_summary.md` / `docs/MODEL_STRATEGY.md` / `artifacts/research/experiment_registry.jsonl` / `docs/ANALYSIS_BACKLOG.md`
- 書式: 各発見は必ず3問に答える — **【分かったこと】結局何が分かったか /【予測に効くか】未来の予測に効くか /【市場】市場は既に知っているか**
- 正直ラベルの規約: 小標本は「n=◯逸話」、確定オッズ由来の数値は「diagnostic(診断用・ROI主張不可)」を必ず付ける。無い値は「記録なし」と書く

---

## ① 重要な発見(確定事項)

### 1. 予測 / 市場評価 / 購入判断の3層分離は既に de-facto 実装済み

- 数値・事実: 予測層 = B2 は入力にオッズ由来ゼロ(`dataset.py:16` / class_code 除外済み)。市場は推論後段の表示用ブレンドのみ(`predict_b2_live.py:501` の `0.85*mkt + 0.15*p`)。市場評価層 = 純関数7本(fair_odds → portfolio_ev)が shadow 専用で「記録のみ・本番推奨に影響しない」(`shadow_pipeline.py:33-39` → `predict_live.py:319`)。購入判断層 = select_picks(ev≥0.15)+ NO BET fail-closed(保守係数が欠損・例外なら自動見送り、`raceday_decision_feed.py:64`・EVC_THR=1.15)
- 出典: ARCHITECTURE_FREEZE_v2.1.md §C/§E(2026-09-04 実コード検証で確定)
- だから何?: v2.1 が要求する分離構造は「これから作る」ものではなく「既に守られている」— 破壊ゼロで新研究を積める。
- 【分かったこと】設計思想(オッズに予測を汚染させない)がコードレベルで実現済みだった
- 【予測に効くか】直接は効かない(構造の話)。ただし今後の全実験の安全な土台になる
- 【市場】無関係(内部構造の発見)

### 2. モデル改造12連敗の法則 — 効くのは「情報追加」と「推論工夫」だけ

- 数値: 再学習を伴うモデル改造は12件全滅(racer ID embedding=B2H / 複合損失B3 / 容量増 d192×L3 / 異種混成 / 温度較正 / EMA / 5seed / race_no 特徴 等 — いずれも誤差圏か fold 間不再現)。効いたのは 情報追加(extra7: fold2 NLL 3.785→3.777 / extra2: 全国 Hit@1 9.88→10.21% / extra3: ΔNLL −0.004〜−0.007)と推論工夫(3seed 平均 +0.14pp・exh120 補正層 ΔNLL −0.018・市場ブレンド w=0.85)のみ。唯一のアーキ勝利は B2 構造化そのもの(2fold 全指標で B1/B0/NN 移植を上回った)
- 出典: nextgen_audit_20260903.md §1(実験史の総括)/ results_summary.md(4モデル最終比較・スプリントの教訓)/ MODEL_STRATEGY.md §3
- だから何?: 伸びしろは「モデルをいじる」でなく「モデルが知らない情報を足す」— v2.1 の実行順(情報→構造)の憲法。
- 【分かったこと】ボトルネックは構造でも容量でもなく情報
- 【予測に効くか】効く(研究リソースの配分を決める最重要法則)
- 【市場】無関係(自分たちの実験史の法則)

### 3. favorite-longshot — 市場は本命を系統的に過小評価する

- 数値: implied(オッズ逆算の市場確率)0.5-0.7 帯で実際の勝率が市場評価より −2.9pp、0.7+ で −2.8pp(=本命は見た目より当たる)。中穴 0.1-0.2 帯は +0.9pp 過大。1号艇は全階級で買い得(B2級ですら −4.0pp)。確定オッズ由来 = **diagnostic**
- 出典: ANALYSIS_BACKLOG.md 2-1(lane-reports/favorite_longshot_diag_20260712.md・2026-07-12)/ research_state.json supported
- だから何?: 妙味は穴でなく本命側にある — 「穴を当てて儲ける」戦略は市場の歪みの向きと逆。
- 【分かったこと】市場の歪みは「階級」でなく「本命/穴」の軸に出る(教科書的 favorite-longshot)
- 【予測に効くか】予測精度でなく EV 計算(どこに賭け得があるか)に効く
- 【市場】市場自身の歪みそのもの。ただし締切前オッズ(real)での再確認は未了

### 4. レースの格で走りが変わる(格で ST が締まる)

- 数値: 平均 ST が優勝戦 −0.0065秒 / 準優 −0.0094秒(予選比)、**24/24場で同符号**。1号艇は −0.0203秒。1号艇の逃げ率は予選 46.7% → 準優 71.3%。格カテゴリは F=41 に未収載(未特徴化)
- 出典: nextgen_audit_20260903.md §9 / experiment_registry.jsonl NG-E1(事前登録済み)
- だから何?: 「勝負どころで人は変わる」が全場で定量再現 — 最有望の未特徴化シグナル。
- 【分かったこと】選手の行動は固定能力でなく文脈(レースの格)で系統的に変わる
- 【予測に効くか】効く見込み(NG-E1 で薄層 ΔNLL≥0.003 を判定。プラセボ = race_no 単独版)
- 【市場】未測定(E1 の G5 で判定)。格自体は公知情報なので織り込み済みの可能性は残る

### 5. SG 当日は AI が市場より確率精度で勝った(n=12 逸話)

- 数値: 桐生SG 8/30 最終日12R — 頭的中は AI 9/12 = 市場最人気 9/12(頭選びでは差がつかない)。勝者への確率は AI>市場 11/12、NLL(予測のズレ・小さいほど良い)**AI 0.818 vs 市場 0.981**。展示反映が勝者確率を改善 11/12。単勝100円診断は回収 ¥1,030/¥1,200(ROI 0.86 = 頭当てだけでは控除の壁は越えない)。外した3R は全部まくり/差し系(配当 ¥6,670〜14,800)
- 出典: hansei_sg_kiryu_20260903.md / experiment_registry.jsonl NG-E19SG
- だから何?: エッジは「頭選び」でなく「確率の厚み」に出る — かつ SG は市場が甘くなる仮説の初証拠。
- 【分かったこと】AI の強みは的中の選択でなく確率の見積もり精度(n=12・1日ぶん・能力断定禁止)
- 【予測に効くか】SG/G1 segment のエッジ実在なら賭け所の選別に直結(NG-E19SG で two-sided 検証中)
- 【市場】SG 当日は市場の織り込みが甘かった可能性(観光マネー仮説)— まだ逸話の域

### 6. モーター交換月は年次で移動する

- 数値: Web 情報の矛盾の真因が「交換月は毎年固定でない」こと。K データの2連率リセット検出で**全24場の交換月を確定**(静的資産 motor_exchange_months)
- 出典: research_state.json supported_findings / docs/research_board.html(UNEXPECTED FINDINGS)
- だから何?: モーター識別キー (jcd, motor_no, cycle_year) の前提が固まり、Motor State 研究(W2)が着手可能になった。
- 【分かったこと】外部情報の矛盾はデータから直接解ける(2連率リセット=交換の指紋)
- 【予測に効くか】直接でなく前提整備(motor 系特徴の年度混同バグを防ぐ)
- 【市場】不明(市場が交換月をどこまで意識するかは未測定)

---

## ② Unexpected Findings(意外な発見)

| # | 発見 | 実測 | 出典 |
|---|---|---|---|
| U1 | **風向が6.5年まるごと未使用** | wind_dir_code は学習・本番とも実質全行 −1 の死に特徴。充足している 8.1% も16方位テキスト vs 8方位変換表の欠陥で −1 落ち。さらにスカラー投入で円環性を破壊 | audit §5 |
| U2 | **live 予測の気象入力がゼロ** | 実戦キャプチャ 96/96 件すべて気象 None → fillna(0) で常に「無風・波ゼロ」で予想。学習は実値 98.7% = train/serve skew が残存(P0)。SG もこの状態で戦っていた | audit §5 / research_state P0 |
| U3 | **気温・水温は「季節の焼き直し」** | F=43 実験で fold 間符号反転・permutation で実体の 8-9 割が季節情報の重複 → 素値追加は棄却・再提案禁止。以後「季節クリマトロジー置換プラセボ」を標準検査化 | audit §6 / research_state rejected |
| U4 | **市場は階級を正確に織り込む** | 「A1 は人気しすぎ」説は全級 ±0.7pp で否定。歪みは階級軸に無い(本命/穴軸にある → ①-3) | backlog 2-1(2026-07-12 diag) |
| U5 | **モーター交換月は年次で移動する** | Web の矛盾情報の真因。K 2連率リセット検出で全24場確定(①-6 参照) | research_board / research_state |
| U6 | **展示補正は方向ほぼ完璧・量が保守的** | SG桐生で 11/12 正方向、だが荒れを買える水準まで動かせない(例: 1R 4号の展示ST −0.02 の攻め気配に +0.2pp しか反応せず)。研究窓 ΔNLL −0.018・24/24場改善の実績と両立 | hansei 仮説B / audit §2 |
| U7 | **満潮の定説は逆** | 「満潮=まくり有利」の定説に対し実測は逆方向 | research_state rejected / audit §11 |
| U8 | **風向アイコンはコース図基準だった** | beforeinfo アイコン vs K 風向の素朴一致率 13.7%(ランダム同然)だが、場別角度オフセットが鋭い単一モード(24場中20場で占有率 0.62-0.90・風速≥3m・n=15,660)。= アイコンは方角でなくコース図基準。副産物として**24場コース方位テーブルが半自動で完成**(high19/mid5・venue_course_azimuth.json)。弱モード4場 = 尼崎0.43 / 住之江0.48 / 多摩川0.51 / 徳山0.54 | audit §7 |

各項目の3問:

- **U1/U2(風向未使用・live気象ゼロ)**:【分かったこと】6.5年分の情報空白と P0 運用欠陥が同居していた。【予測に効くか】修復すれば効く可能性大(風コース成分 = NG-E5W 登録済み。live 修復パッチは Owner 判断待ち)。【市場】市場(現地の客)は風を見ている = AI だけが見えていなかった、が仮説
- **U3(気温水温)**:【分かったこと】「効いて見える特徴」の実体が季節 proxy でありうる。【予測に効くか】素値は効かない。残る新規性は差分系(air_water_gap 等)のみ。【市場】不明
- **U4(階級織り込み)**:【分かったこと】市場は階級を見誤らない。【予測に効くか】階級ラベルはモデル入力からも市場歪み説明からも退場。【市場】完全に知っている
- **U5(交換月)**: ①-6 参照
- **U6(展示補正)**:【分かったこと】方向検出と増幅は別問題。【予測に効くか】増幅の穴 = Intent 層(v2.1)の存在理由そのもの。【市場】市場は展示を同時に見ている(展示情報単独のエッジは限定的)
- **U7(満潮)**:【分かったこと】人間メカニズム仮説(物理の向き)を事前に固定してはいけない → E5W が two-sided 設計になった根拠。【予測に効くか】潮汐薄層は棄却済・交互作用は未検証。【市場】不明
- **U8(風向アイコン)**:【分かったこと】データの「仕様の癖」から不変資産(24場コース方位)が採れた。【予測に効くか】NG-E5W(wind_along/wind_cross)の前提資産。【市場】現地客はコース基準で風を見ている = 市場は使っている情報

---

## ③ Pattern Library(再現性のある条件付き発見の台帳)

棄却されたパターンも削除しない(棄却3類型: 効果不在 / 実在するが焼き直し / 実在するが織り込み済み)。

### P1. まくり筋の組を AI が系統的に過小評価

- 条件: まくり・まくり差しで決まる筋の3連単組
- 効果: 平均残差 **+0.001416・z≈8.4・AI 相対 +29% 見落とし**(どの補正でも生き残った唯一の歪み)
- n: 全期間(具体件数は記録なし)/ 検証期間: 全期間(事後発見のため未採用)
- 確信度: **中(再検証中)** — 事後発見なので NG-E10 で事前登録再検証(前半抽出→後半+P2 符号再現)にかけている
- 最終確認日: 2026-09-03(NG-E10 事前登録)
- 出典: audit §13 / experiment_registry.jsonl NG-E10 / ARCHITECTURE_FREEZE §G
- 3問:【分かったこと】AI の負けパターンは「荒れ全般」でなく「まくり筋」に偏る(SG で外した3Rが全部まくり/差し系と現場一致)。【予測に効くか】再検証 PASS なら最短の +EV 候補・GAT 系研究の go/no-go を兼ねる。【市場】SG の3R は市場も外していた = 市場も完全には知らない可能性(E10/E19SG で判定)

### P2. 乖離0.23 を境に損益が反転する(用量反応)

- 条件: 乖離(AI 確率 × オッズ)が 0.23 以上の単勝
- 効果: 的中率は5帯単調増加・ROI は 0.23 を境に損益割れ→プラス圏(0.23+ で n=268・ROI≈1.53)
- n: 268(0.23+ 帯)/ 検証期間: **6年**・独立証拠3本(用量反応 + シャドウ2期間 + 第2アーム)
- 確信度: **中〜高** — 方向は3証拠一致。ただし確定オッズ由来 = **diagnostic** であり、外側検証(EXP-002)の cluster CI 下限 0.943 < 1.0 = **収益証明は未達**。実弾主張不可
- 最終確認日: 2026-07-23(lane-reports/edge_dose_response_20260723.md)
- 出典: MODEL_STRATEGY.md §3 / experiment_registry.jsonl EXP-002
- 3問:【分かったこと】乖離は連続量として効く(閾値0.23 はデータが選んだ境界)。【予測に効くか】シャドウ発火閾値 0.20→0.23 の根拠。【市場】乖離の存在自体が「市場がまだ知らない差分」の候補 — ただし締切前オッズでの本測が残る

### P3. F明け1号艇の勝率低下

- 条件: フライング休み明け直後の1号艇
- 効果: 勝率 **−10pp**
- n: 「大」とのみ記録(具体値は記録なし)/ 検証期間: 記録なし
- 確信度: **高(現象実在)/ ただし特徴化は無効** — F動態の特徴化(extra4)は 2fold 改善なしで不採用
- 最終確認日: 2026-09-03(nextgen_audit で生存例として言及)
- 出典: audit §15 / audit §3A(flying_events.parquet + extra4 builder)
- 3問:【分かったこと】現象は実在するが、モデルは既存特徴(直近成績等)経由で実質吸収済みらしい。【予測に効くか】特徴としては効かない(織り込み済み=①-2 の法則どおり)。【市場】市場も概ね知っている(F持ちの汎用タグは「織り込み済み」で棄却歴)。選手個別の F 後 ST 変化(f_dynamics)だけが未検証の残り火

### P4. 安定板 + 風5m = イン受難(荒天ほど地力差)

- 条件: 安定板使用 + 風速5m前後の荒天
- 効果: イン(1号艇)受難方向に3レース連続で一貫(尼崎 8R 的中・10R 回避判断正解)
- n: **3(逸話)** / 検証期間: 2026-08-26〜27(尼崎実弾)のみ
- 確信度: **低(未検証)** — 作業仮説の段階
- 最終確認日: 2026-09-03(hansei §5 で台帳転記)
- 出典: hansei_sg_kiryu_20260903.md §5(bet_ledger_20260827.md より転記)
- 3問:【分かったこと】AI は風・波は見るが「安定板使用」自体を特徴に持たない = 荒天効果の織り込み不足の候補。【予測に効くか】未知(E5 環境系に引き継ぎ済み。stabilizer は beforeinfo に収録あり)。【市場】不明

---

## ④ 人間向け解説 — 結局この研究で何が分かっているのか

前提の用語(1行ずつ):
- **NLL** = 予測のズレの大きさ(小さいほど良い)。デタラメ(3連単なら log120=4.79)より小さければ「分かっている」
- **implied 確率** = オッズを逆算して出す「市場が思っている確率」。**de-vig** = そこから控除率25%分を取り除く補正
- **fold / walk-forward** = 過去で学習し未来で試す時系列の検証区切り。カンニング(未来情報リーク)を防ぐ仕組み
- **ΔNLL 0.003** = 「採用してよい改善」の最低ライン(これ未満は誤差扱い)
- **diagnostic** = 確定オッズ(締切後の最終形)で測った参考値。実際に買える瞬間のオッズではないので ROI の根拠にしない
- **shadow** = 実際には賭けず記録だけ取る運用。**fail-closed** = 判断材料が欠けたら「買わない」に倒れる安全設計

### 話を3行にすると

1. **AI は市場の95%地点まで来た**(NLL 差 +0.06〜0.07)。オッズを一切見ずに、番組表と過去成績だけで市場の持つ情報のほぼ全てを再構成できている。
2. **残りの差の正体が絞れてきた**。市場が知っていて AI が知らないもの = 風(6.5年未使用)・当日の気象(live はゼロだった)・レースの格(勝負どころで ST が締まる)・攻める意図(展示補正は方向は当たるが量が控えめ)。
3. **市場側にも穴がある**。本命の過小評価(favorite-longshot)と、まくり筋の見落とし(こちらは AI も市場も怪しい)。SG の1日だけなら AI が市場より確率精度で勝った(n=12 なので断定禁止)。

### 「未来の予測に効くか」で仕分けると

- **もう効いている**: B2 構造化・情報追加3弾・3seed 平均・展示補正・市場ブレンド(①-2 の採用リスト)
- **効く見込みで検証待ち**: レースの格(NG-E1)・まくり筋(NG-E10)・風コース成分(NG-E5W)・勝負駆け utility(NG-E23)・SG 市場効率(NG-E19SG)— 全て事前登録済み・Owner の適用判断5点が前提
- **効かないと確定**: 階級ラベル・気温水温の素値・racer ID embedding・容量増・複合損失・race_no・明示積項(いずれも再投入禁止)

### 「市場は既に知っているか」で仕分けると

- **市場が正確に知っている**: 階級(全級 ±0.7pp)・汎用の攻撃タグ / 番組格差 / 1-4-5筋(実在するが織り込み済みで棄却)
- **市場が間違えている**: 本命の価値(−2.9pp 過小・1号艇は全階級で買い得)— ここが AI の賭け得候補
- **市場も AI も見落としの可能性**: まくり筋(P1)・SG 当日の本命(①-5)— 今まさに E10 / E19SG で検証中
- **AI だけが見えていなかった**: 風向・当日気象・安定板(U1/U2/P4)— 修復と特徴化はこれから

### 一番大事な教訓(1行)

**勝ち筋は「賢いモデル」ではなく「モデルがまだ知らない情報」**。12連敗の実験史がそれを証明しており、v2.1 のロードマップ(情報→構造の順)はこの法則の上に立っている。



# ===== research_state.json =====

```json
{
  "updated_at": "2026-09-04",
  "updated_by": "claude/v2.1-freeze-session",
  "canonical_note": "本ファイルが機械可読の正本。人間可読の詳細は同ディレクトリの md 群。Artifact 494f0be1-a091-4cc3-b90f-72df7dc0b01d は view であり正本ではない",
  "architecture_version": "v2.1",
  "architecture_doc": "docs/ARCHITECTURE_FREEZE_v2.1.md",
  "current_phase": "W1直前 (土台W0完了。実験登録簿 = registered 5本 + filed 1本、うち第1波の実行対象は4本。適用パッケージ5点のOwner判断待ち)",
  "baseline_model": {
    "id": "b2f41_prod2026_prod3",
    "description": "B2構造化着順NN (41特徴・6艇self-attention・120通り直接softmax・3seed平均) + exh120展示補正層(θ9) + 市場ブレンド(w=0.85・推論後段)",
    "odds_as_input": false,
    "params": 464817
  },
  "best_model": {
    "id": "b2f41_prod2026_prod3",
    "note": "現状 Baseline と同一 (v2.1 新アーキ未着工のため最新=最良)"
  },
  "current_experiment": null,
  "current_experiment_note": "実行中なし。次 = NG-E10。前提 = 適用パッケージ5点の Owner 判断",
  "experiments": {
    "registry_path": "artifacts/research/experiment_registry.jsonl",
    "adopted": [
      {"id": "B2", "change": "120通り直接スコアリング+6艇attention", "effect": "全指標でB0/B1超え (唯一のアーキ勝利)"},
      {"id": "extra7", "change": "当地収縮+節内フォーム7特徴", "effect": "fold2 NLL 3.785→3.777"},
      {"id": "extra2", "change": "場×コース歴史率+直近5走", "effect": "extra2単独で全国Hit@1 9.88→10.07%、3seed併用で10.21%"},
      {"id": "extra3", "change": "ST分布+節内得点 (F=41完成)", "effect": "ΔNLL -0.004〜-0.007"},
      {"id": "seed3", "change": "3seed確率平均", "effect": "+0.14pp (3で飽和)"},
      {"id": "exh120", "change": "展示タイム/ST/F の後段補正層", "effect": "ΔNLL -0.018 研究窓・24/24場改善"},
      {"id": "mkt_blend", "change": "市場ブレンド w=0.85 (推論後段)", "effect": "住之江で市場単独NLL超え"},
      {"id": "f41_skew_fix", "change": "学習気象を beforeinfo 由来へ統一", "effect": "GATE PASS (2026-08-06切替)"}
    ],
    "rejected": [
      {"id": "b2h_embedding", "reason": "racer ID embedding 改善ゼロ"},
      {"id": "composite_loss/capacity/mixture/race_no/5seed/temp_calib", "reason": "モデル改造系6件 全て誤差圏"},
      {"id": "f43_temp_water", "reason": "気温水温素値 = fold間符号反転・季節の焼き直し"},
      {"id": "thin_layers_tide_style_gap", "reason": "潮汐/戦型/番組ギャップ薄層 -0.0006〜0.0011 (基準0.003未達)"},
      {"id": "class_code", "reason": "階級ラベル全棄却 (2026-06確定・再投入禁止)"},
      {"id": "explicit_interactions", "reason": "明示積項は桐生で過学習方向"}
    ],
    "frozen": [
      {"id": "lambdarank_portfolio", "reason": "GATE FAIL・コード残存・Baseline扱い"}
    ],
    "registered_waiting": [
      {"id": "NG-E10", "theme": "選手externality統計PoC+まくり筋再検証", "gate": "分散成分検定+前後半符号再現"},
      {"id": "NG-E1", "theme": "レース格カテゴリ", "gate": "薄層ΔNLL≥0.003+race_noプラセボ"},
      {"id": "NG-E23", "theme": "勝負駆けutility curve", "gate": "NLL/市場edge 2軸事前分離"},
      {"id": "NG-E5W", "theme": "風コース成分", "gate": "季節クリマトロジー置換プラセボ"},
      {"id": "NG-E19SG", "theme": "SG/G1祭り市場効率", "gate": "two-sided・締切前オッズ=real"},
      {"id": "NG-E8SWAP", "theme": "当地デッドウェイト置換 (起票のみ)", "gate": "E8全滅時のみ着手"}
    ]
  },
  "hypotheses": {
    "note": "本節は要約サブセット。全仮説(29件)の悉皆台帳は HYPOTHESES.md — 収載範囲は台帳側が上位互換",
    "supported": [
      "市場は本命を過小評価する (favorite-longshot。implied0.5+で-2.9pp)",
      "1号艇は全階級で買い得 (イン利は階級を超える)",
      "レースの格で走りが変わる (準優ST-0.0094・24/24場同符号・逃げ率46.7→71.3%。未特徴化)"
    ],
    "testing": [
      "AIはまくり筋の荒れを系統的に見落とす (+29%・z≈8.4) → NG-E10",
      "SG/G1は観光マネーで市場が甘くなる (SG当日 AI NLL 0.818 vs 0.981・n=12) → NG-E19SG",
      "4カド攻撃型は5・6に展開を作る (選手固有の条件付き) → NG-E10"
    ],
    "partially_supported": [
      "勝負駆けで走りが変わる (バイナリ圏内/圏外は統制後消滅 → utility curve形式でE23再挑戦)"
    ],
    "rejected": [
      "階級が予測に効く (全棄却)",
      "高階級は市場で人気過剰 (全級±0.7pp=正確に織り込み)",
      "満潮=まくり有利 (実測は逆方向)",
      "汎用の攻撃タグ/番組格差/1-4-5筋にエッジ (実在するが市場織り込み済み)"
    ],
    "untested": [
      "安定板+強風=イン受難 (尼崎3R連続一貫・n=3逸話)",
      "地元経験は難水面でこそ効く (無条件当地はゼロ効果済) → E8",
      "部品交換は選手の潜在診断信号",
      "師弟・先輩後輩で行動が変わる",
      "ルーキー急成長を市場が遅れて評価する"
    ]
  },
  "supported_findings": [
    "予測/市場評価/購入判断の3層分離は既に de-facto 実装済み (B2オッズ非入力・ev層shadow専用純関数・NO BET fail-closed。2026-09-04実コード検証)",
    "展示補正は方向11/12正・増幅が保守的 (Intent層の存在理由)",
    "実験史: モデル改造12連敗・情報追加と推論工夫のみ有効",
    "風向アイコン=コース図基準の発見 → 24場コース方位テーブル half-auto 完成 (high19/mid5)",
    "モーター交換月は年次で移動する (K 2連率リセット検出で全24場確定)"
  ],
  "rejected_findings": [
    "気温・水温の素値は予測に効く (実体の8-9割が季節の焼き直し)",
    "『A1は人気しすぎ』(市場は階級を正確に織り込む)"
  ],
  "metrics": {
    "national_fold2_3seed": {"nll": 3.7565, "hit1": 0.1020, "tansho_acc": 0.5746},
    "market_gap_nll": "+0.06〜0.07 (確定オッズde-vig比・diagnostic)",
    "sg_kiryu_20260830": {"head_hits": "9/12", "trifecta_top1": "4/12", "ai_nll": 0.818, "market_nll": 0.981, "n": 12, "label": "逸話・断定禁止"},
    "adoption_line_thin_layer_dnll": 0.003
  },
  "data_status": {
    "official_bk": "2020〜全国・ほぼ完全 (K結果はレース後公開=ラベル専用)",
    "beforeinfo": "2020〜 (2023-01〜04欠落=素データ自体なし)。7/28-9/2の5,880R回収済(2026-09-03)。風向は復活作業中・部品交換はパーサ修理待ち",
    "era5": "2020〜2026-09 毎時24場 140万行 (気圧/湿度/突風/空気密度)。事後再解析=本番は予報アーカイブ要",
    "odds_preclose": "全国 2026-07-10〜蓄積中 (real EV評価はこれのみ)",
    "setsu_master": "全期間5,311節 (artifacts/research/nextgen/setsu_master.parquet)",
    "static_assets": "venue_course_azimuth.json (high19/mid5) / venue_branch_map / motor_exchange_months / venue_latlon",
    "missing_wishlist": ["選手コメント時系列(HIGH)", "プロペラ形状(HIGH・困難)", "1M映像展開(MED・打ち切り済)", "人間関係(MED)", "ピット常時(LOW-MED)"]
  },
  "overfitting_status": {
    "fold_contamination": "fold1/fold2は開発汚染済み=採否の最終根拠にしない",
    "gates": "G0事前登録→G1 2fold一貫+bootstrap CI95→G2 3seed→G3 prod2026窓→G4 ECE→G5 市場(diag/real分離)→G6 8segment",
    "danger_zones": ["Player×Course×Stage×Wind等の細分サンプル枯渇 (積項でなく共有表現)", "万舟数本集中の利益 (検知をハーネスに組込予定)"]
  },
  "leakage_status": {
    "defense": "5層 (列名ガード/日付split/集計方向shift(1)/入力由来許可リスト/replay時刻)。本番経路に既知の直接リークなし",
    "known_risks": ["同日クロス会場ソート (パッチ済・本番見送り中・新研究は新ソート必須)", "Stage/節内集計の同日後レース混入 (day-start規約)", "気象の確定観測vs締切前 (§51)", "選手コメントのレース後混入 (前向き収集のみ可)"],
    "unusable_scripts": ["real_backtest.py / walk_forward_eval.py (未来漏れ未修正・新研究で流用禁止)"]
  },
  "pending_owner_decisions": [
    {"n": 1, "item": "live気象修復パッチ (P0)", "recommend": "適用"},
    {"n": 2, "item": "7/27劣化153件修復", "recommend": "適用"},
    {"n": 3, "item": "風向16方位パーサ", "recommend": "適用"},
    {"n": 4, "item": "openapi日次取り込みを夜間ジョブへ", "recommend": "追加"},
    {"n": 5, "item": "同日ソートキー修正の本番適用", "recommend": "見送り (研究ビルドのみ)"}
  ],
  "next_actions": [
    "適用パッケージ5点のOwner判断 (全実験の前提)",
    "NG-E10: まくり筋再検証+externality実在判定 (情報利得最大・GAT系のgo/no-go)",
    "NG-E1+NG-E23: レース格+勝負駆けutility",
    "NG-E5W: 風コース成分",
    "常時: NG-E19SG (SG/G1市場効率)"
  ]
}

```
