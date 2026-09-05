# KYOTEI-AI RESEARCH MIRROR(外部AI共有用・読み取り専用)
生成日: 2026-09-05 / 正本: kyotei-ai リポジトリ /research/ 配下(本ファイルはその連結コピー)
注意: 数値の正直ルール(小標本=断定禁止・確定オッズ由来=diagnostic)を前提に読むこと。本文書には市場の歪みの所在(研究エッジ)が含まれる — 取り扱いは Owner(shin)の指示に従う。
---


# ===== RESEARCH_STATUS.md =====

# RESEARCH_STATUS — 研究状態の正本

- 最新更新: **2026-09-05**(更新者: Claude / セッション: W2 正式 GO + 次期研究思想の統合)
- 本ファイルは Canonical Research State の入口。機械可読版 = `research_state.json`。人間向け表示 = 研究コンソール(Artifact 494f0be1… — 本ファイル群から生成される view であり正本ではない)

## 現在の研究フェーズ

**第1波(W1)の登録実験を全消化(2026-09-04)**。done 6本 = NG-E10(両ゲートPASS)+ **NG-I1 / NG-N1 / NG-E1 / NG-E5W / NG-E23(5本とも主ゲートFAIL・全て事前登録ルールの機械適用)**。残 = NG-E19SG(常時・締切前オッズ蓄積待ち)+ NG-E8SWAP(filed)。全実験で「事前登録→操作的定義の凍結→機械判定」を完走、判定ルールの事後変更ゼロ。**Owner 裁定受領 (2026-09-04): #6 GO → NG-N1C (Calibration-specific Gate) 事前登録済 / #7 GO → NG-E5NR (Nonlinear Environmental Regime) 事前登録済 / #8 DEFER (格 = 現象 SUPPORTED・入力側再学習は保留)**。W2 方針 = 後付け薄層の枯渇を受け「真の新情報 / regime / Calibration / Market / Current State 推定」へ重心移動 (最重要候補 = Motor Current State / Maintenance 系)。W2 Candidate Audit 完了 (2026-09-04・beforeinfo 356,476 ファイル実測)。**決定的発見: 部品交換データは 6.5 年間パーサ取り違えで実質未収集だった**。**W2 正式 GO (Owner 2026-09-05)**: 実行順確定 = 並行【①まくり筋較正最終検証 (NG-N1C) ②部品交換修理+前向き収集+層化バックフィル PoC】→ ③現在モーター状態 PoC → ④強風 regime ⑤調整能力。全バックフィルは未承認 (PoC 後に再判断)。並行で「展開圧力×対応力 (Generalized Pressure×Resistance)」の設計+データ監査。新研究思想 8 テーマ (シナリオ分散買い・known-but-underweighted 市場情報 等) を仮説として正式保存。

## Current Best Model / Baseline

- **Best = Baseline = `b2f41_prod2026_prod3`**(現状同一。v2.1 新アーキは未着工のため「最新=最良」)
- 実体: B2構造化着順NN(41特徴・6艇self-attention・120通り直接softmax・3seed平均)+ exh120展示補正層(θ9本)+ 市場ブレンド(w=0.85・推論後段/表示用)
- 主要指標: 全国 fold2 NLL 3.7565 / Hit@1 10.20% / 単勝Acc 57.46%。市場(確定オッズde-vig)との残距離 NLL +0.06〜0.07

## 現在実行中の Experiment

**なし — 第1波5本(NG-I1 / NG-N1 / NG-E1 / NG-E5W / NG-E23)は 2026-09-04 に並列レーンで実行し全て done_primary**。5本とも主ゲート(薄層ΔNLL≥0.003)FAIL。ただし収穫が3つ: ①**N1 はまくり筋の較正歪みを1パラメータ(λ=+0.228)でほぼ完全回収**(完全OOSで相対見落とし +26.3%→+2.7%・副作用ゼロ。閾値0.003が単一セル補正の理論上限より高く原理的に到達不能だった=Owner判断 #6)②E1 で「格は実在するが B2 は既に織り込み済み」が確定・グレード表(E19SG用)を副産物化 ③E5W で強風 7m/s+ の符号逆転(線形仮定の破綻)を発見。詳細 = `lane-reports/{i1_proxy,n1_reweight,e1_stage,e5w_wind,e23_utility}_20260904.md` + registry 各 done_primary 行。残り = registered 1本(NG-E19SG・常時)+ filed 1本(NG-E8SWAP)

## 主要な研究成果(直近)

0. **W1 第1波バッチ完了(2026-09-04)**: 5実験を1日で消化し全て機械判定。核心は NG-N1 — まくり筋の較正歪み(唯一の OOS 確定歪み)は凍結 B2 への後段1パラメータ補正で **gap z=10.2 → 1.3(相対見落とし +26.3%→+2.7%)** まで回収でき、まくり筋以外への悪影響ゼロ、鏡像の過大評価も同時解消することを完全 OOS で実証。ただし主ゲート(レース全体 ΔNLL≥0.003)は閾値が単一セル補正の理論上限(≈0.0013〜0.0015)を超えており原理的に到達不能だった → 判定は FAIL のまま・再ゲートは Owner 判断 #6。他: I-1(proxy 2特徴は signature 7件を全捕捉するも薄層 FAIL)/ E1(格は織り込み済み・③型棄却)/ E5W(効果不在・季節焼き直しではない・強風で符号逆転)/ E23(勝負駆けは2形式で null 確定)
1. **NG-E10 両ゲートPASS(2026-09-04)**: ①選手固有 externality の分散成分は実在(T=10,970.5 vs 帰無8,703.5±62.3・permutation p=0.001・場層別でも不変)②まくり筋の AI 過小評価は完全OOS 1年分(2025-07〜2026-06・44,357R)で確定 — gap +0.001298・CI95[+0.001053,+0.001551]・z=10.2・相対+26.3%見落とし・22/24場プラス。確認済み signature 7件(攻撃スタイル型6・前づけ型1)。純粋externality(自艇無傷で隣だけ動く型)は信号ゼロ(p=0.894)。判定 = N1 GO(主役=まくり筋セル項)+ I-1 proxy前倒し・GAT起票は不支持。**確定は「較正の歪み」であり「買える歪み」は未確定(P2に締切前オッズ無し)**
2. **SG桐生 8/30 実戦**: 頭的中9/12(市場と同着)、勝者確率で AI>市場 11/12(NLL 0.818 vs 0.981・n=12逸話)。展示補正は11/12正方向・量が保守的
3. **23項目監査**: 風向6.5年未使用 / live気象ゼロ(P0→パッチ適用済 2026-09-04) / 未使用データの山(格ラベル・気温水温・チルト・部品交換・決まり手・支部)
4. **分離構造の実証**: 予測(オッズ非入力)/市場評価(純関数7本・shadow専用)/購入判断(NO BET fail-closed)の3層分離が既に de-facto 実装済みと実コード確認
5. 実験史の憲法: **モデル改造12連敗・情報追加と推論工夫のみ有効**

## 現在の問題

- conditional_finish に class_code 残留(再利用前に再GATE必須)
- N1 の閾値設計問題 → **裁定済み (2026-09-04 Owner #6 GO)**: Calibration-specific Gate を NG-N1C として新規事前登録 (閾値は理論SEから事前設定)。NG-N1 の旧判定は「旧ゲートでは FAIL」のまま保持 — FAIL 実験を成功扱いに書き換えない
- **まくり筋の確定は「AIの較正の歪み」であって「買える歪み」ではない**(P2 に締切前オッズが無く市場比較は不可のまま。市場側の判定は NG-E19SG / 締切前オッズ蓄積が受け皿)
- 2026-09-04 バッチ成果物は同日 commit 済み(本セッション)

## 次にやること

`NEXT_ACTIONS.md` 参照。1行版: **W2 順位の Owner 確定 → ①NG-N1C ②Motor Current State PoC ③部品交換修理+前向き収集 ④E5NR Phase A ⑤Player Adjustment Skill の順で実行**(常時: NG-E19SG 蓄積、holdout 封印 11/1 まで)。

## 更新ルール(2026-09-04 Owner 指示で制定)

コード・実験・研究状態を更新したら、**Artifact だけでなく /research/ 配下の本ファイル群と research_state.json を必ず同期する**。他のAI・人間はまずここを読む。



# ===== NEXT_ACTIONS.md =====

# NEXT_ACTIONS — 現在優先すべき研究(3〜5件だけ)

最新更新: 2026-09-05(**W2 正式 GO + 次期研究思想の統合** — Owner 全文指示)。
全テーマの扱い順: **観察 → 一般仮説 → 最小統計PoC → OOS再現 → 予測価値 → 市場価値 → 必要なら Architecture 投資**。

## 並行実行中(Owner 確定順)

### 1. まくり筋補正の最終検証(NG-N1C)— 完了・FAIL(2026-09-05)

- ①対象セル解消(z=1.32)・②全体NLL非劣性・⑤場別安全は成立。**③非対象セル(2/33帯が悪化)・④3期再現(2/3のみ)が不成立** → 凍結ルールどおり不採用。旧 NG-N1 の判定も不変
- 主因 = 補正つまみ λ の時間変化(2024H2 +0.17 → 2026H1 +0.28 で固定値だと効き過ぎ/効き不足が出る)。**rolling λ(直近窓で逐次更新)での再挑戦 = Owner 判断 #9**(新規事前登録が必要な別実験)

### 2. 部品交換の修理+前向き収集(実行中・データ資産)

- 誤パース列(前走成績が入っている)は**正しい部品交換データとして絶対に再利用しない**
- 取得: 部品交換 / 新ペラ / 可能なら交換種類 / fetched_at / source / race_id / racer_id / motor identity / as-of 保証 metadata
- **全バックフィル(35万ページ)は未承認** → まず Stratified Backfill PoC(場・年度・季節・グレードで層化した小規模取得)で 正常取得率・発生率・接続率・追跡率・polite 実測速度 を確認し、全量の EIG/コストを再推定して Owner 再判断

## 次

### 3. 現在モーター状態 PoC(NG-MS1)— 完了・**存在確認 PASS**(2026-09-05・W1以降初のポジティブ)

- 節内の調整推移(特に展示タイムの推移)が B2 の予測残差を予測する。**当日の値だけを見る現行の展示補正では表現できない独立情報**(当日 z を統制しても有意に残存・プラセボで消失・前後半符号一致)
- 「元々のモーターの強さ」(motor_2rate)と直交 = 本当に「今の仕上がり」を測っている。軸同士は無相関 = 単一の点数に潰せない(最低3次元)
- as-of パネル 68.2 万行(2024-06〜2026-06・24場)を資産化 — Player Adjustment Skill(⑤)の土台にそのまま使える
- **次段階 = 最小特徴化 + OOS ゲート(B2 入力側 = 再学習を伴う)→ Owner 判断 #11 として起票提案**

## その後

### 4. 強風 regime PoC(NG-E5NR Phase A・登録済み) / 5. 選手の調整能力(Player Adjustment Skill)

## 並行(設計まで) — 展開圧力×対応力(Generalized Pressure × Resistance)

- 現場観察(強い1コースの隣の2が走りにくい/強3の外の4が崩れて5-6へ波及 等)の**一般化仮説**。個人ルール(峰・毒島・茅原等)としては実装しない — 観察は仮説形成の例であり統計的事実ではない
- いまやるのは**事前研究設計+データ可用性監査まで**(PoC Step1-6 の設計・ペア順 1→2 / 2↔3 / 3→4 / 4→5 / 攻撃艇→外側追走 / 前づけ→周囲・sample size と shrinkage 設計)
- GAT 再評価条件: pair interaction が OOS 再現し単独プロファイルで表現できない追加価値が出た場合のみ。再現しなければ GAT 導入理由に使わない

## 常時 / 市場研究の思想更新(Owner 2026-09-05)

- 狙いは「誰も知らない情報」でなく **known-but-underweighted(市場が知っているが重み付けし切れていない情報)/ 条件付き interaction の誤価格 / 二次・三次の受益艇の誤価格**。「攻める本人は売られるが受益者は売られていない」を重点確認(締切前オッズ蓄積後)
- 予測エッジと購入エッジの4ゲート分離を厳守: 現象実在 → 予測追加価値 → 市場未価格化 → 購入EV
- 購入の最終形は Scenario-aware Betting Portfolio(シナリオ分散買い)— 概念保存済み・一気に実装しない
- NG-E19SG 蓄積継続 / 市場アノマリー holdout 封印(閲覧 2026-11-01 以降)/ 格の再学習 DEFER 継続



# ===== ARCHITECTURE.md =====

# ARCHITECTURE — Canonical Architecture の現在地

- **Architecture Version: v2.1**(制定 2026-09-04・shin freeze 指示)
- 最新更新: 2026-09-05(W2 正式 GO セッション — §2-2 ブロック注記と §6 概念ロードマップを追記。**Architecture Version は v2.1 のまま不変**)
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

### 2-2. ブロック注記 — Owner 思想更新(2026-09-05。**概念であり v2.1 freeze の変更ではない**)

§2 の表の行・分類(KEEP/EXTEND/NEW 等)・Gap 欄は不変。以下は該当ブロックに載せる思想レベルの注記のみ(全て未採択・実装は各 PoC→OOS 再現後)。

**Betting/Portfolio ブロック注記(購入層の思想更新)**

- 最終購入を「**予測確率の高い3連単を上から買う」設計にしない**(Owner 方針 2026-09-05)
- レースを複数シナリオ(例: 1逃げ / 3攻め1凌ぎ / 3攻めで2-3崩れ5浮上 / 3攻め完全成功 / 波乱)として扱い、**Ticket×Scenario exposure** を評価する。1-2-3/1-2-4/1-2-5 の3点は分散に見えて「1逃げ+2残り」シナリオへの集中投資
- optimizer 指標候補(未採択): Expected Return / **Robust EV**(確率が多少ズレても残る EV)/ Scenario Coverage / Concentration(同一シナリオ依存度)/ Probability of Total Loss(全滅確率)/ Downside Risk(CVaR 等・必要なら)/ Epistemic Uncertainty
- **禁止**: 的中率のためだけの低EV舟券の大量追加。追加舟券には十分な Robust EV **または**有意な Scenario diversification benefit を要求。目的は EV を維持したまま主要シナリオ耐性を高め、下側リスクを抑えること
- 凍結原則は不変(§4): EV 閾値 +15% 固定・NO BET = first-class decision
- 対応仮説: `HYPOTHESES.md` U-24 / U-25(いずれも未検証・概念保存のみ)

**Market Evaluation ブロック注記(市場研究の思想更新)**

- 主戦場は「誰も知らない秘密情報」ではなく ①**known-but-underweighted**(市場が知っているが重み付けし切れていない情報)②**conditional interaction mispricing**(条件付き相互作用の誤価格)③**second-order・beneficiary mispricing**(二次=直接影響艇・三次=崩れからの受益艇の誤価格)
- 重点確認: 「**攻める本人は売られるが展開受益者は十分売られていない**」現象
- 評価計画: 締切前オッズ蓄積後、Interaction Pattern ごとに model prob / market implied / pre-close movement / EV / beneficiary ticket EV / 反応速度 / 最終反映量を評価
- ゲート分離(混同禁止): 「現象が存在する → AI 予測に追加価値 → 市場が十分価格化していない → 実際に購入EVがある」は全部別ゲート。Market Layer と Fundamental Prediction の完全分離を継続
- 対応仮説: `HYPOTHESES.md` U-21 / U-22 / U-23(いずれも未検証)

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

---

## 6. 概念ロードマップ(未採択・実装禁止・PoC 先行)— Owner 最終形 concept(2026-09-05)

Owner が W2 正式 GO と同時に示した**最終形の概念フロー**。位置づけを先に固定する:

- これは**概念であり v2.1 freeze の変更ではない**(Architecture Version は上げない。§3 Changelog にも version 行を足さない — version 変更を伴う設計変更時は従来どおり freeze 文書 Changelog → version 更新 → 本ファイル同期)
- **一気に実装しない**。各ブロックの採択には **最小統計PoC → OOS 再現** が必要(扱い順: 観察 → 一般仮説 → 最小統計PoC → OOS再現 → 予測価値 → 市場価値 → 必要なら Architecture 投資)。PoC 前の巨大 Architecture 構築は禁止
- 対応する仮説台帳: `HYPOTHESES.md` U-18〜U-25(全て未検証)

```
Fundamental Race Model
   → Current State(選手・モーターの「今」の as-of 状態推定)
   → Interaction / Scenario Model
   → 120通り Fundamental Probability
   → Calibration / Uncertainty
   → Market Evaluation
   → Scenario × Ticket Payoff Matrix
   → Portfolio Optimization
   → BET / NO BET
```

**GAT 再評価条件(NG-E10 時点の「GAT 起票不支持」は維持)**: Pressure×Resistance の pair interaction が **OOS で再現し、かつ単独プロファイル(選手×コースの静的プロファイル)で表現できない追加価値**が確認された場合のみ、GAT / pairwise / message passing を再評価する。再現しなければ GAT 導入理由に使わない。



# ===== EXPERIMENTS.md =====

# EXPERIMENTS — 実験台帳(正本)

- 最終更新: 2026-09-04(セッション: W1 第1波バッチ完了反映 — I1/N1/E1/E5W/E23 の5本を同日消化)
- 位置づけ: Canonical Research State の実験台帳。機械可読 index = `artifacts/research/experiment_registry.jsonl`。矛盾時は `research_state.json` / `RESEARCH_STATUS.md` を正とする
- 主な出典: `docs/experiments/structured_order_model/results_summary.md` / `docs/MODEL_STRATEGY.md` / `docs/ARCHITECTURE_FREEZE_v2.1.md` / `lane-reports/nextgen_audit_20260903.md` / `lane-reports/hansei_sg_kiryu_20260903.md` / `lane-reports/e10_externality_20260904.md` / `artifacts/research/mkt/preregistration_20260806.md`
- 判定凡例: **ADOPT**(採用・本番/構成に反映)/ **REJECT**(棄却・同一形での再提案禁止)/ **FROZEN**(凍結・コード残存/Baseline扱い)/ **REGISTERED**(事前登録済み・未実行)/ **DONE**(完了・判定確定)
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

## 4. 完了(DONE・第1波 6本)

### 4-1. NG-E10 — 選手 externality 統計PoC + まくり筋事前登録再検証 【**DONE・両ゲートPASS**(2026-09-04)】

- **仮説**: ①選手×コースが隣接艇の結果に与える系統的影響(externality)が実在する(T-4)②AI はまくり筋(攻め艇1着+外の追走艇2/3着の3連単組)を系統的に過小評価している(T-1・唯一の生存歪み +0.001416, z≈8.4, 相対+29%)③4カド攻撃型の外恩恵は選手固有現象として存在する(T-3)
- **事前登録**: 2026-09-03(registry・git a759dac)+ 操作的定義の凍結 `artifacts/research/nextgen/e10/e10_operational_plan_frozen.json`(結果計算前)。**判定ルール・閾値の事後変更ゼロ**。頑健性検定1本のみ結果計算前に追加宣言(addendum1)
- **データ**: P1 = LGB expanding crossfit 残差パネル(285,069レース×6艇・全期間)/ P2 = fold2 replica 推論 dump(2025-07-01〜2026-06-30・50,926R・完全OOS。sanity: mean test NLL 3.764945 = 既存一致 PASS)
- **主判定① externality 分散成分(層1)**: **PASS** — T=10,970.5 vs permutation 帰無 8,703.5±62.3(1,000回・seed42)、p=**0.001**(下限値)。頑健性: (コース,年,場)層別 permutation でも p=0.001 = 場の偏りの偽陽性ではない。→ N1 中止条件に該当せず
- **主判定② まくり筋セル**: **PASS(OOS確定)** — 完全OOS 1年分 44,357レース/354,856買い目/的中2,212。AI 予測 0.4936% → 実績 0.6234%、gap **+0.001298**、CI95 **[+0.001053, +0.001551]**(0非跨ぎ)、z=**10.22**、AI相対見落とし **+26.3%**(発見時 +29%・z≈8.4 と同符号・同水準)。半期4期連続プラス(z 4.8〜8.4)・**24場中22場プラス**(マイナス2場=福岡/唐津は CI が 0 を大きく跨ぐ=サンプル不足で否定材料ではない)・グレード帯(A1人数 proxy)全帯で CI 0非跨ぎ
- **層3 signature**: 前半 2021-2023 の 46,550セル → BH-FDR q<0.05 で26本 → \|shrunk\|≥2pp で20候補 → 後半 2024-2026H1 + P2 の符号再現で**確認済み7件**(藤山翔大 3→1 −12.5pp / 菅章哉 3→1 −10.8pp / 藤山翔大 2→1 −9.3pp / 高田ひか 2→1 −7.3pp / 大神康司 5→6 +4.2pp / 高田ひか 3→4 +4.2pp(P2 +0.1pp=実質弱い)/ 戸塚邦好 4→5 +3.4pp)。型の内訳: **攻撃スタイル型 6/9・前づけ型 1/6・新人外回り型 0/5(後半全滅=新人期限定の非定常シグナル。再現ゲートが正しく排除)**
- **別枠(純粋 externality)**: 自艇残差≈0層(94,770 slot)は T=4,340 vs 帰無 4,389・p=**0.894 = 信号ゼロ**。検出された効果の実体は「攻め・進入イベントで自艇と隣が同時にズレる」型
- **判定**: **DONE(done_primary・両ゲートPASS)** — ①N1 GO(**主役=まくり筋セル項・選手 signature 項は補助**。signature は7件と薄く、まくり筋は35万買い目/年で厚い)②**I-1 proxy 特徴(attack_propensity@course / approach_deviation)の前倒し**(確認済み7件の実体はこの2特徴でほぼ張れる)③**GAT 起票は今回のエビデンスからは不支持** ④まくり筋の用途第一=較正改善+AI艇報。**P2 に締切前オッズ無し=「買える歪み」は未確定**(2026-07-31 の「市場はまくり筋を外していない」含意は上書きしていない)
- **考察(バグ処理の経緯)**: 実行途中で比例配分重みの実装バグを発見(P1 の合計2再正規化で p>1 の行 0.49% → w=p(1-p) が負に発散)→ **クリップ修正のみ行い全層再実行・初回実行の数値は破棄**(addendum2 で全経緯開示)。自艇≈0層・対角・まくり筋は補正不使用のため無影響
- **caveat 主要**: P1 の LGB 代理は選手 ID を持たず、自艇対角 2.9〜4.5pp(選手スキルの取り残し)と externality 推定は数学的に完全分離不可 — 「残差関連」であり因果断定しない。攻め/前づけの機構解釈は事後データ(approach)による記述
- 出典: `lane-reports/e10_externality_20260904.md` / registry NG-E10 done_primary 行 / `artifacts/research/nextgen/e10/`

### 4-2. NG-I1 — as-of 行動プロファイル proxy 特徴 【**DONE・FAIL**(2026-09-04)】

- **仮説**: attack_propensity@course(K=20収縮まくり率)+ approach_deviation(as-of 前づけ癖)は E10 確認済み signature の実体を張れる新情報
- **指標(実測)**: 薄層ΔNLL fold1アーム −0.000205 CI95[−0.000932,+0.000472](0跨ぎ)/ fold2アーム **+0.001078** CI95[+0.000686,+0.001471](0非跨ぎだが閾値 0.003 の約1/3)。fold間符号反転。改善は attack_propensity 単独。placebo 0/20 = 小信号は本物
- **判定**: **FAIL**(特徴昇格見送り・F43 再学習ゲート起票せず)
- **考察**: E10 signature 7件は全員2特徴の分布の端で捕捉 = 特徴設計は妥当。薄層6係数では「少数の特異選手に集中する効果」が平均化され閾値未達。焼き直し検査 最大|r|=0.45。i1_features.parquet(206万行・leak test PASS)は資産保存
- 出典: `lane-reports/i1_proxy_20260904.md` / `artifacts/research/nextgen/i1/`

### 4-3. NG-N1 — 凍結B2への対数線形再重み付け(まくり筋セル項)【**DONE・主ゲートFAIL/較正回収は実証**(2026-09-04)】

- **仮説**: λ_makuri × I(combo∈まくり筋セル)の log-odds 加算で唯一の OOS 確定歪みを回収できる
- **指標(実測)**: 薄層ΔNLL fold1 +0.000531 CI95[−0.000029,+0.001123] / fold2 +0.001306 CI95[+0.000629,+0.002030] = 閾値 0.003 両fold未達。**P2 完全OOS: λ_makuri=+0.228(過去1年fit・固定適用)で gap +0.001298(z=10.2)→ +0.000166(z=1.3・CI 0跨ぎ)= 相対見落とし +26.3%→+2.7%・グレード全帯で残存消滅・副作用ゼロ(鏡像の過大評価 z≈−10 も同時解消)**。signature 補助項は両fold CI 0跨ぎで不採用方向
- **判定**: **FAIL**(凍結ルール機械適用・符号反転なし)。ただし閾値 0.003 は単一セル補正の理論上限(≈0.0013〜0.0015)より高く原理的に到達不能だった(fold2 実測はほぼ上限到達)→ 較正層としての採否は「セル較正ゲート」の新規事前登録で再判定するかの **Owner 判断 #6**
- **考察**: 福岡・唐津は一律λの過補正で軽度逆方向歪み(場別λは登録外・未実施)。ハーネスバグ2件 addendum 開示・全再実行で数値一致を機械確認。市場比較・ROI 主張なし
- 出典: `lane-reports/n1_reweight_20260904.md` / `artifacts/research/nextgen/n1/`

### 4-4. NG-E1 — レース格カテゴリ(Stage)薄層 【**DONE・FAIL=③織り込み済**(2026-09-04)】

- **指標(実測)**: 薄層ΔNLL fold1 **−0.00055** CI95[−0.00104,−0.00001] / fold2 **−0.00064** CI95[−0.00117,−0.00008] = 符号から逆(base 微悪化)。プラセボ(race_no 単独)は両fold点推定で下回る = 格≠レース番号の焼き直し。ex-ante 判定器一致率 **99.20%**(昇格条件 ≥98% クリア)・決定表カバレッジ未分類 0.0067%・焼き直し検査 Cramér's V≈0.26 / setsu_day からの再構成率 65%
- **判定**: **FAIL(③織り込み済が主+①効果不在併記)** — B2(F41)は setsu_day / setsu_pts 系で格由来シフトを学習済み・出力薄層に拾う残差なし
- **考察**: 格の実測効果(ST 変化 24/24場)の否定ではない。残る道は入力側追加+再学習(**Owner 判断 #8**)。副産物 `venue_date_grade.parquet`(29,715行)は NG-E19SG で使用可(caveat: 上流欠落 2023-01〜04中旬)。grade 軸の独立検証なし(ex-ante/事後とも Bヘッダ同一ソース)
- 出典: `lane-reports/e1_stage_20260904.md` / `artifacts/research/nextgen/e1/`

### 4-5. NG-E5W — 風コース成分薄層 【**DONE・FAIL=①効果不在**(2026-09-04)】

- **指標(実測)**: 薄層ΔNLL fold1 +0.000184 CI95[−0.000622,+0.001000] / fold2 +0.000230 CI95[−0.000267,+0.000723] = 符号反転なしだが閾値の1/15・CI 0跨ぎ。プラセボ①場×月内 permutation 20本 max +0.000068 < 実測 = 信号は本物だが微小。プラセボ②季節クリマトロジー置換で効果消失 = **季節の焼き直しではない**。クリーン行(bi)は fold窓 0行(bi 風向は 2026 年のみ実在)のため K行(wx_src=k_rotated)研究判定+クリーン診断(2026Q1→Q2 +0.000265・単一窓)で実行(凍結計画に事前明記)
- **判定**: **FAIL**(特徴昇格なし)。棄却スコープは「勝者艇番への線形傾き2パラメータ構造」— 風が無関係の証明ではない
- **考察**: **風速 7m/s+ で −0.002174 へ符号逆転 = 線形仮定が強風で破綻**(安定板×強風仮説と方向整合・次仮説の種)。8方位量子化+bi↔K一致 67.3% による効果希釈の可能性。再挑戦は非線形/安定板交互作用方向のみ(**Owner 判断 #7**)
- 出典: `lane-reports/e5w_wind_20260904.md` / `artifacts/research/nextgen/e5w/`

### 4-6. NG-E23 — 勝負駆け utility curve 【**DONE・FAIL=①効果不在**(2026-09-04)】

- **指標(実測)**: 選定 K=24(fold1 選定・fold2 判定)。薄層ΔNLL fold1 **−0.000506** CI95[−0.000825,−0.000186] / fold2 **−0.000481** CI95[−0.000697,−0.000249] = base 微悪化・K=12/18 も全負で結論不変。適格レース限定では悪化拡大 = 増分情報ゼロの追い証拠。θ終値 |θ|≤0.033 でほぼ無補正。市場軸(確定オッズ diagnostic・2,051R)は u1 五分位×6帯すべて CI 0跨ぎ = utility 帯由来の市場歪み検出されず(断定せず)。day-start 検証 T1-T5 全PASS・違反ゼロ
- **判定**: **FAIL**。節の立ち位置(勝負駆け)路線は二値(null 済)→連続(本実験)の**2形式で null** = 同路線の再々提案は非推奨
- **考察**: q_k は「世界凍結」近似(登録どおりの操作的定義)。E0/E10 個人プロファイリング路線へ寄せるのが合理的(lane 見解)
- 出典: `lane-reports/e23_utility_20260904.md` / `artifacts/research/nextgen/e23/`

---

## 5. 事前登録済み・未実行(REGISTERED 1本 + filed 1本)

registry(`artifacts/research/experiment_registry.jsonl`)からの転記。NG-E1 / NG-E23 / NG-E5W は 2026-09-04 完了 → §4 へ移動。NG-I1 / NG-N1 は 2026-09-04 に L1 が事前登録し同日完了 → §4。

| ID | テーマ / 仮説 | planned_test(登録内容) | decision_rule(登録内容) | 状態 |
|---|---|---|---|---|
| **NG-E19SG** | SG/G1 祭り日の市場効率 segment。一次証跡 = SG桐生 8/30(AI NLL 0.818 vs 市場 0.981・n=12逸話) | grade segment 別のモデル vs 市場 NLL/Brier 差(two-sided・登録済み1本)。SG/G1 開催日 vs 一般。real=締切前オッズ(national_v2 2026-07-10..)、確定オッズ使用時は diagnostic 明示。副次 = 織り込み済み棄却群(戦型/番組格差/F持ち/1-4-5)の SG 限定再判定(BH)。**グレードラベルは E1 副産物 venue_date_grade.parquet が利用可** | 前後半符号再現なしは探索止まり。ROI/EV 主張は real のみ | registered(常時・蓄積待ち) |
| **NG-E8SWAP** | 当地デッドウェイト3本の置換 ablation(起票のみ) | (実行時定義)当地系3本の除外/置換 2fold NLL。着手条件: Local×難水面3セル(W2-4)が全滅した場合のみ | −(登録上未定義) | filed(実行しない) |

---

## 6. 市場アノマリー3テーマ(事前登録済み・holdout 封印中)

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

## 7. 市場・収益系実験(registry 記載・儲ける力レーン・完了分)

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

## 8. 横断メモ(数値の読み方)

- 採用ライン(薄層): ΔNLL ≥ **0.003**(参考: exh120 −0.018 / extra3 −0.004〜0.007 / 棄却薄層群 −0.0006〜0.0011)
- 市場との残距離: NLL +0.06〜0.07(確定オッズ de-vig 比・**diagnostic**)。SG桐生 8/30 の AI NLL 0.818 vs 市場 0.981 は **n=12 の逸話**(能力断定禁止)
- 棄却の3類型を必ず明記: ①効果不在(CI跨ぎ)②実在するが焼き直し(統制で消滅)③実在するが織り込み済(市場残差ゼロ)。②③は Pattern Library に記録し廃棄しない



# ===== HYPOTHESES.md =====

# HYPOTHESES — 研究仮説台帳(正本)

- 最新更新: **2026-09-05**(更新者: Claude / セッション: W2 正式 GO — Owner 次期研究思想 8 テーマを U-18〜U-25 として追加。既存エントリの判定・本文は不変)
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
| S-5(旧T-1) | AIはまくり筋の荒れを見落とす | ✅支持(OOS確定) | OOS1年 gap+0.001298・z=10.2・+26.3%・22/24場(E10) | N1薄層・E16。買える歪みは未確定 |
| T-2 | SG/G1は市場が甘くなる | 🔄検証中 | AI NLL 0.818 vs 市場0.981(n=12逸話) | NG-E19SG |
| P-4(旧T-3) | 4カド攻撃型は5・6に展開を作る | 🌓部分 | 攻撃スタイル型6/9再現・型は選手固有(7件/1,872人) | I-1 proxy特徴 |
| S-6(旧T-4) | 特定選手が隣の艇を殺す/活かす | ✅支持 | 分散成分 permutation p=0.001(E10) | N1補助項+I-1 |
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
| U-18 | 展開圧力×対応力(P×R) | ⬜未検証 | 現場観察のみ(逸話・n不明) | 事前研究設計+データ可用性監査(W2並行) |
| U-19 | コース条件付き相性 | ⬜未検証 | 記録なし | U-18 PoC Step4 に内包 |
| U-20 | 波及と受益艇 | ⬜未検証 | 具体形は P-4/S-6 判定済・一般形は記録なし | U-18 PoC Step6 |
| U-21 | 市場の重み付け不足情報 | ⬜未検証 | S-1/S-4 が同型の傍証(diagnostic) | 締切前オッズ蓄積後 |
| U-22 | 条件付き相互作用の誤価格 | ⬜未検証 | S-5 は AI 側の歪みのみ確定 | 締切前オッズ蓄積後 |
| U-23 | 二次・三次受益艇の誤価格 | ⬜未検証 | 記録なし | 締切前オッズ蓄積後 |
| U-24 | シナリオ分散買い | ⬜未検証 | 記録なし | 概念保存・実装しない(W3以降) |
| U-25 | 頑健EV+下振れ最適化 | ⬜未検証 | 記録なし | 概念保存・実装しない(U-24とセット) |
| R-1 | 階級が予測に効く | ❌否定 | 全棄却(2026-06確定・再投入禁止) | — |
| R-2 | 高階級は市場で人気過剰 | ❌否定 | 全級±0.7pp=正確に織り込み | — |
| R-3 | 満潮=まくり有利 | ❌否定 | 実測は逆方向 | 再解釈のみ |
| R-4 | 汎用の攻撃タグ/番組格差/1-4-5筋にエッジ | ❌否定 | 実在するが市場織り込み済み | 選手固有はE10 |
| R-5 | 気温・水温の素値が効く | ❌否定 | 8-9割が季節の焼き直し | 差分系のみ(U-6) |
| R-6 | 当地・地元は無条件で効く | ❌否定 | ablationデッドウェイト | 条件付きはU-2 |
| R-7 | 純粋externality(自艇無傷で隣だけ動く) | ❌否定 | 自艇残差≈0層 p=0.894=信号ゼロ(E10) | — |

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

### 1-e. Owner 現場観察+指示由来の次期研究思想 8 テーマ(2026-09-05 W2 正式GO時に登録 — 全て仮説・未検証)

- 出典は全て「**Owner 現場観察+指示 2026-09-05**」(`research_state.json` の `w2_directives_owner_20260905` に構造化全文)
- 注意(正直ラベル): 峰・毒島・茅原等の個人名を伴う現場観察は**仮説形成の例であり統計的事実ではない**。個人ルールとしては実装しない
- 扱い順は全テーマ共通: 観察 → 一般仮説 → 最小統計PoC → OOS再現 → 予測価値 → 市場価値 → 必要なら Architecture 投資(ゲート混同禁止)
- 本節は Owner 指示による仮説登録のみ。G0 実験登録は各 PoC の起票時に個別に行う

#### U-18. 展開圧力×対応力(Generalized Pressure × Resistance)
- 仮説文: コース条件付きの「圧力を作る側」の圧力量 × 「受ける側」の対応力 × 相対位置 が、相手艇の期待着順変化を生み、さらに周囲艇へ展開波及する
- なぜ有望か: Owner 現場観察(強い1コースの隣の2が走りにくい/強い3の外の4が崩れて5-6へ波及する 等)の一般化。隣接する判定済み仮説(S-6・P-4)が同方向の傍証
- 既存判定との接続(上書きしない): S-6(選手externality=支持)・P-4(攻撃スタイル型=部分支持)の一般化。**R-7(純粋externality=否定)は本仮説でも前提として維持** — 「自艇無傷で隣だけ動く」型は信号ゼロ。NG-I1 の薄層 FAIL(全選手一律の薄い補正では特異選手の集中効果が平均化される)も設計制約として引き継ぐ
- 仮の profile 軸(名称付き能力を真実扱いせず、まず観測可能な残差構造を確認する): Pressure側 = Inside/Attack/Sashi/Makuri/Makuri-sashi Pressure・Outside Compression・Neighbor Disruption・Opportunity Creation / Resistance側 = Strong-In Resistance・Attack Resistance・C2 Preservation・C3/C4 Survival・Defensive Turn・Second-place Preservation・Collapse Avoidance・Pressure Absorption
- PoC 手順(設計案・Step1-6): ①艇Aの在席が艇Bの B2 残差に与える影響を as-of 測定 → ②影響量が B 側でも系統的に変わるか → ③Bの圧力耐性を shrinkage 付きで推定 → ④A単独/B単独/A+B/A×B 比較 → ⑤interaction の OOS 追加価値 → ⑥Bの崩れの波及(内隣/外隣/5-6号艇の Top2/Top3 変化)。**全ペア巨大モデル禁止** — ペア順は 1→2 / 2↔3 / 3→4 / 4→5 / 攻撃艇→外側追走艇 / 前づけ艇→周囲艇
- 現在の証拠: 現場観察のみ(逸話・n不明)。統計記録なし
- サンプル規模: 検証未実施
- 確信度: 低〜中(隣接判定は同方向だが、一般形そのものは未検証)
- 次のアクション: **事前研究設計+データ可用性監査まで**(既定 W2 順は止めない。EIG が極めて高いと判断したら理由付きで順位変更案を出す)。GAT 再評価条件は ARCHITECTURE.md §6 参照

#### U-19. コース条件付き相性(Course-conditioned Matchup Skill)
- 仮説文: 選手×選手(または型×型)の相性がコース条件付きで存在し、同じ相手でも並び・コースによって matchup の有利不利が系統的に変わる
- なぜ有望か: P-4 の判定「型は選手固有の静的プロファイルで表現できる」の次の問いとして自然(静的プロファイル同士の条件付き組合せ)。R-1(階級ラベル棄却)とは別物 — 静的ラベルでなく選手固有プロファイル間の関係を見る
- 現在の証拠: 記録なし
- サンプル規模: 検証未実施
- 確信度: 低
- 次のアクション: 単独では未起票。U-18 PoC Step4(A単独/B単独/A+B/A×B 比較)に内包して判定

#### U-20. 波及と受益艇(Interaction propagation / beneficiary effect)
- 仮説文: 攻め・崩れの影響は隣接1艇で止まらず、内隣/外隣/5-6号艇の Top2/Top3 確率変化として波及し、「崩れから利益を受ける受益艇」が系統的に存在する
- なぜ有望か: P-4(4カド攻撃型→5・6の外恩恵=部分支持)の一般化。E10 の確認済み signature 7件は具体例に相当するが、二次・三次の波及量の定量はどの実験でも未測定
- 既存判定との接続: P-4/S-6 の判定は不変。本仮説は「波及の一般形と量」の未検証部分のみを対象とする
- 現在の証拠: 一般形は記録なし
- サンプル規模: 検証未実施
- 確信度: 低〜中
- 次のアクション: U-18 PoC Step6(崩れの波及測定)。市場側の帰結は U-23 で別判定

#### U-21. 市場が知っているが重み付け不足の情報(Known-but-underweighted market information)
- 仮説文: エッジの主戦場は「誰も知らない秘密情報」ではなく、市場参加者も知っているが**重み付けし切れていない**情報にある
- なぜ有望か: S-1/S-2/S-4(本命過小・乖離の用量反応)は既にこの型の実例(いずれも diagnostic)。R-4 の教訓(実在するが織り込み済み)と対 — 問いは「知られているか」でなく「十分に重み付けされているか」
- 現在の証拠: 同型の傍証のみ(確定オッズ diagnostic)。思想としての一般形は記録なし
- サンプル規模: 検証未実施
- 確信度: 低〜中
- 次のアクション: 締切前オッズ蓄積後(NG-E19SG と同じ受け皿)。4ゲート分離(現象実在→予測追加価値→市場未価格化→購入EV)を厳守

#### U-22. 条件付き相互作用の誤価格(Conditional interaction mispricing)
- 仮説文: 条件付き相互作用(特定の並び・型の組合せで生じる展開)を市場が価格化し切れていない
- なぜ有望か: S-5 で確定したのは「**AI 側の較正の歪み**」であり、市場側が同じ筋を外しているかは未確定(2026-07-31 の「市場はまくり筋を外していない」含意は上書きされていない)。本仮説はその市場側の問い
- 逆風の前例: R-4(汎用の筋・タグは実在するが市場織り込み済み)。条件付き形でのみ生き残る可能性を検証する
- 現在の証拠: 記録なし
- サンプル規模: 検証未実施
- 確信度: 低
- 次のアクション: 締切前オッズ蓄積後、Interaction Pattern ごとに model prob / market implied / pre-close movement / EV / 反応速度 / 最終反映量を評価

#### U-23. 二次・三次受益艇の誤価格(Second-order beneficiary mispricing)
- 仮説文: 攻める本人(一次)は市場に売られるが、直接影響を受ける艇(二次)・崩れから利益を受ける艇(三次)は十分に売られない
- なぜ有望か: 重点確認対象 = 「攻める本人は売られるが展開受益者は十分売られていない」現象(Owner 指示の明示重点)。U-20 の市場側の帰結
- 現在の証拠: 記録なし
- サンプル規模: 検証未実施
- 確信度: 低
- 次のアクション: 締切前オッズ蓄積後、beneficiary ticket EV を含めて評価(U-22 と同じ評価枠)

#### U-24. シナリオ分散買い(Scenario-aware betting portfolio)
- 仮説文: 最終購入は「予測確率の高い3連単を上から買う」より、レースを複数シナリオ(例: 1逃げ/3攻め1凌ぎ/3攻めで2-3崩れ5浮上/3攻め完全成功/波乱)として扱い **Ticket×Scenario exposure** を最適化する方が、下側リスク調整後の成績が良い
- なぜ有望か: Owner 方針(2026-09-05)「予測確率の高い3連単を上から買う設計にしない」。例: 1-2-3/1-2-4/1-2-5 の3点買いは分散に見えて「1逃げ+2残り」シナリオへの集中投資
- 既存との接続: U-15(展開クラスタ条件付き着順)/E16 が Scenario Model 側の前提。購入層の詳細注記は ARCHITECTURE.md §2-2
- 現在の証拠: 記録なし
- サンプル規模: 検証未実施
- 確信度: 低(概念段階)
- 次のアクション: **概念保存のみ・実装しない**(W3 以降・予測層成熟後)。EV 閾値 +15% は不変

#### U-25. 下振れ考慮の頑健EV最適化(Robust EV + downside-aware optimization)
- 仮説文: 確率推定が多少ズレても残る **Robust EV** と下側リスク指標(Scenario Coverage / Concentration / 全滅確率 / CVaR 等・必要なら / Epistemic Uncertainty)を組み込んだポートフォリオ最適化が、素の EV 最大化より実運用で頑健
- 禁止則(仮説段階から固定): **的中率のためだけの低EV舟券の大量追加は禁止**。追加舟券には十分な Robust EV または有意な Scenario diversification benefit を要求
- 現在の証拠: 記録なし
- サンプル規模: 検証未実施
- 確信度: 低(概念段階)
- 次のアクション: 概念保存のみ・実装しない(U-24 とセット。指標候補の採否も未決)

---

## 2. TESTING(事前登録済みで検証枠にある — 実行中の実験は現在なし)

※ 旧 T-1(まくり筋)→ **S-5 に昇格**、旧 T-4(選手externality)→ **S-6 に昇格**、旧 T-3(4カド攻撃型)→ **P-4 に移動**(いずれも NG-E10 判定・2026-09-04)

#### T-2. SG/G1 は観光マネーで市場が甘くなる(祭りの市場効率低下)
- 仮説文: 大型開催は場外流入の観光マネーが穴に散り、本命過小(favorite-longshot)が普段より増幅 → AI の相対エッジが拡大する
- なぜ有望か: SG桐生 8/30 実測 — 勝者への確率で AI>市場 11/12、NLL AI 0.818 vs 市場 0.981。AI 74-81% の鉄板を市場は 57-67% でしか売っていなかった(R5/R8/R9)。S-1 の条件付き増幅版(`lane-reports/hansei_sg_kiryu_20260903.md` §3 仮説A)
- 必要データ: 締切前オッズ(national_v2 2026-07-10〜・期間浅い)+ グレードラベル(月間開催日程ページ・取得可能確認済)
- 現在の証拠: **n=12・1日ぶんの逸話(断定禁止)**。単勝診断は AI頭で ROI 0.86 = 頭当てだけでは控除の壁は越えない、も併記
- サンプル規模: n=12 逸話
- 確信度: 低(効果は鮮明だが1日ぶん)
- 次のアクション: **NG-E19SG**(registered・常時)— two-sided・ROI/EV 主張は real(締切前)のみ。副次: 織り込み済み棄却群(戦型/番組格差/F持ち/1-4-5)の SG 限定再判定

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

#### S-5. AIはまくり筋の荒れを系統的に見落とす(旧 T-1 → 2026-09-04 昇格)
- 仮説文: まくり・まくり差しで決まる筋の3連単組(1レース8通り)をモデルが系統的に過小評価している
- 判定: **SUPPORTED(OOS確定)** — NG-E10 主ゲート: 完全 out-of-sample の1年分(2025-07-01〜2026-06-30・44,357レース/354,856買い目/的中2,212)で AI 予測 0.4936% → 実績 0.6234%、gap **+0.001298**・CI95 **[+0.001053, +0.001551]**(0非跨ぎ)・z=**10.22**・AI相対見落とし **+26.3%**(発見時 +29%・z≈8.4 と同符号・同水準)
- 再現性: 半期4期連続プラス(z 4.8〜8.4)・**24場中22場プラス**(マイナス2場は CI 0跨ぎ=サンプル不足)・グレード帯(A1人数 proxy)全帯で CI 0非跨ぎ = 期間や場の偶然でなく**モデルの構造的な癖**
- 統治: 事後発見 → 事前登録(2026-09-03)→ OOS 再現、の「まくり筋方式」を完走した初例。判定ルールの事後変更ゼロ
- 正直ラベル: **確定したのは「AIの較正の歪み」。P2 に締切前オッズが無く「買える歪み」かは未確定**(2026-07-31 の「市場はまくり筋を外していない」含意は上書きされていない)
- 次のアクション: N1薄層(まくり筋セル項が主役)+ 較正改善・AI艇報の定量根拠。E16「歪みセル限定混合」の第一対象
- 出典: `lane-reports/e10_externality_20260904.md` §1-2 / registry NG-E10 done_primary 行

#### S-6. 特定選手が隣接コースを系統的に殺す/活かす(選手 externality・旧 T-4 → 2026-09-04 昇格)
- 仮説文: 選手×コースが隣接艇の結果に与える系統的な影響(externality)が実在する(憲章§62)
- 判定: **SUPPORTED** — NG-E10 層1 分散成分検定: T=10,970.5 vs permutation 帰無 8,703.5±62.3(1,000回・seed42)・p=**0.001**(帰無平均の+36σ)。(コース,年,場)層別の頑健性でも p=0.001。確認済み signature 7件(藤山翔大 3→1 **−12.5pp** 等 — FINDINGS P5 参照)
- 限定(重要): 効果の実体は「攻め・進入イベントで**自艇と隣が同時に動く**型」— 純粋 externality(自艇無傷で隣だけ動く型)は信号ゼロ(R-7)。また 7件/1,872選手 = 全選手に広く分布する性質ではなく、ごく少数の特異プロファイル
- caveat: P1 の LGB 代理は選手 ID を持たず、自艇対角 2.9〜4.5pp の「選手スキル取り残し」と完全分離不可 = 残差関連であり因果断定しない
- 次のアクション: N1(補助項)+ **I-1 proxy 特徴**(attack_propensity@course / approach_deviation)。GAT 起票は今回のエビデンスからは不支持
- 出典: `lane-reports/e10_externality_20260904.md` §1/§3-5 / registry NG-E10 done_primary 行

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

#### P-4. 4カド攻撃型は5・6に展開を作る(外恩恵・旧 T-3 → 2026-09-04 移動)
- 仮説文(当初): 4カドに攻撃型の特定選手がいるとき、5・6コースに展開(外恩恵)が生まれる
- 判定: **PARTIALLY SUPPORTED** — NG-E10 層3 で**攻撃スタイル型 signature は9候補中6件が再現**(層3の再現主力。まくり・まくり差し常習者が2-4枠にいると1号艇が沈む/外隣が浮く。例: 戸塚邦好 4→5 +3.4pp)。ただし限定2点: ①「型」は選手固有の静的プロファイル(まくり率・前づけ率)で表現できる現象で、汎用の展開力学ではない(確認7件/1,872選手)②前づけ型は1/6・新人外回り型は0/5(非定常で全滅)
- 教訓: ペア同士の動的相互作用(GAT が得意な形)が要る証拠は出ていない — 「選手×コースの静的プロファイル」で足りる
- 次のアクション: **I-1 proxy 特徴化**(attack_propensity@course=K=20収縮まくり率 / approach_deviation=as-of 前づけ癖)
- 出典: `lane-reports/e10_externality_20260904.md` §3-4(viz4_confirmed_signatures.csv)

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
- 教訓: hit率改善≠ROI改善(市場効率仮説)。**選手固有の条件付き**は E10 で判定済み(→ P-4 部分支持 / S-6 支持)
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

#### R-7. 純粋 externality — 自艇は想定どおり走りつつ隣だけを変える(2026-09-04 新規)
- 仮説文: 「選手Aが隣にいると、A自身は普通に走りつつ隣Bだけが予測より良く/悪く走る」型の externality が存在する
- 判定: **REJECTED** — NG-E10 別枠検定: 自艇の予測が当たっているレース(自艇残差≈0層・94,770 slot)に限ると T=4,340 vs 帰無 4,389・p=**0.894 = 信号ゼロ**
- 教訓: 検出された externality は全て「攻め・進入イベントで自艇と隣が**同時に**ズレる」型(S-6 の限定条項)。narrative の「Aがいると隣Bが強くなる(Aは普通に走る)」という語りは現データでは支持されない
- 出典: `lane-reports/e10_externality_20260904.md` §1(別枠)/§6

---

## 更新ルール

- 実験が決着するたびに該当仮説を移動し、`research_state.json` の `hypotheses` 節と**必ず同期**する(CLAUDE.md §19)
- 棄却された仮説も削除しない(棄却の3類型①効果不在②焼き直し③織り込み済み を明記して Pattern Library と相互参照)
- 事後発見は必ず「再登録→別期間確認」を経てから SUPPORTED に昇格(まくり筋方式)
- 新仮説の追加は G0 事前登録(`artifacts/research/experiment_registry.jsonl`)とセットで行う



# ===== FINDINGS.md =====

# FINDINGS — 研究発見台帳(Canonical Research State)

- 最終更新: 2026-09-04(v2.1 freeze → NG-E10 判定反映 → W1 第1波バッチ完了反映)
- 位置づけ: `research_state.json` / `RESEARCH_STATUS.md` と同期した人間可読の発見集。矛盾したら json 側が正
- 主な出典: `docs/ARCHITECTURE_FREEZE_v2.1.md` / `lane-reports/nextgen_audit_20260903.md` / `lane-reports/hansei_sg_kiryu_20260903.md` / `lane-reports/e10_externality_20260904.md` / `docs/experiments/structured_order_model/results_summary.md` / `docs/MODEL_STRATEGY.md` / `artifacts/research/experiment_registry.jsonl` / `docs/ANALYSIS_BACKLOG.md`
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
- 【予測に効くか】**効かないと確定(NG-E1・2026-09-04)**: 薄層ΔNLL は両 fold で負(base 微悪化)= B2 は setsu_day / setsu_pts 系から格由来シフトを既に学習済みで、出力への後付けに拾う残差なし。現象実在・予測増分ゼロ。入力側追加+再学習は未検証(Owner 判断 #8)
- 【市場】NG-E1 は③織り込み済(モデル側)を確定。市場側の格 segment 判定は NG-E19SG へ(E1 副産物のグレード表を流用)

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

### 7. まくり筋の AI 過小評価は完全 OOS 1年分で確定(NG-E10・2026-09-04)

- 数値: 完全 out-of-sample の1年分(2025-07-01〜2026-06-30・44,357レース/354,856買い目/的中2,212)で AI 予測 0.4936% → 実績 0.6234%。gap **+0.001298**・CI95 **[+0.001053, +0.001551]**(0非跨ぎ)・z=**10.22**・AI 相対見落とし **+26.3%**(発見時 +29%・z≈8.4 と同水準)。半期4期連続プラス・**24場中22場プラス**・グレード帯(A1人数 proxy)全帯で CI 0非跨ぎ = モデルの構造的な癖
- 出典: e10_externality_20260904.md §1-2 / registry NG-E10 done_primary
- だから何?: 2026-07-31 に「検出力不足(z=1.79)」だった判定が1年分の未接触データで決着 — AI はまくりで決まる筋を今も約26%割り引いて売っている。事後発見→事前登録→OOS 再現の「まくり筋方式」完走の初例。
- 【分かったこと】AI の負けパターン「まくり筋の割引」は偶然でなく構造
- 【予測に効くか】効く(N1薄層のまくり筋セル項=最短の較正改善。E16 歪みセル限定混合の第一対象)
- 【市場】**未確定** — P2 に締切前オッズが無く市場比較は不可。「買える歪み」の確定ではない(2026-07-31 の「市場はまくり筋を外していない」含意は上書きされていない)

### 8. 選手固有 externality は実在する — ただし「イベント型」(NG-E10・2026-09-04)

- 数値: 分散成分検定 T=10,970.5 vs permutation 帰無 8,703.5±62.3(1,000回・seed42)・p=**0.001**(場層別の頑健性でも 0.001)。確認済み signature 7件(2重再現ゲート通過)。コース×コース行列では 2-4枠の「誰か」で1号艇の残差が 2.4〜3.5pp 動く(まくり筋過小評価の選手別の顔)
- 出典: e10_externality_20260904.md §1/§3/§5
- だから何?: 憲章§62「特定の選手が特定コースを殺す」は少数の実名選手について統計的に実在。ただし効果は「自艇と隣が同時に動く攻め/進入イベント型」で、純粋 externality(自艇無傷)は信号ゼロ(p=0.894)— GAT 的な動的相互作用の証拠は出ておらず、選手×コースの静的プロファイル(I-1 proxy 2特徴)でほぼ表現できる。
- 【分かったこと】6艇 interaction の実在は Yes、ただし形は限定的(N1 中止条件に該当せず・GAT 起票は不支持)
- 【予測に効くか】N1(signature は補助項)+ I-1 proxy 特徴(attack_propensity@course / approach_deviation)で回収予定
- 【市場】未測定(P2 にオッズ無し)

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
| U9 | **新人外回り型 signature は後半で全滅(非定常)** | 5→6 の+効果 5候補は登録番号5184以降の若手ばかり = 新人期の大外進入慣行の疑似シグナル。前半(新人期)だけ強く、卒業と共に消滅 → 後半再現ゲートで 0/5。事前登録の再現ゲートが無ければ5件の偽シグナルを掴んでいた | e10 §4/§6 |
| U10 | **externality は「自艇と隣が同時に動く」型だけ** | 自艇残差≈0層(94,770 slot)で p=0.894 = 純粋 externality(自艇無傷で隣だけ動く型)は信号ゼロ。実在するのは前づけ・攻撃スタイル等の進入/攻めイベント由来の系統ズレ | e10 §1/§6 |
| U11 | **風の効きは強風で符号が逆転する** | 風コース成分の薄層効果は通常域で微プラスだが、風速 7m/s+ に限ると −0.002174 へ反転 = 「風は直線的に効く」仮定が強風で破綻。安定板×強風=イン受難仮説(P4・n=3)と方向整合 | e5w_wind_20260904.md |
| U12 | **B2 出力への後付け薄層は枯渇した** | W1 第1波5実験(I1/N1/E1/E5W/E23)が全て主ゲート FAIL。B2 は格も勝負駆けも既に織り込み、残る歪みはまくり筋のような較正セル単位のみ(それも1パラメータで回収可能=N1)。伸びしろは入力側新情報か較正・市場評価側へ | 第1波 lane-reports 5本 |

各項目の3問:

- **U1/U2(風向未使用・live気象ゼロ)**:【分かったこと】6.5年分の情報空白と P0 運用欠陥が同居していた。【予測に効くか】修復すれば効く可能性大(風コース成分 = NG-E5W 登録済み。live 修復パッチは Owner 判断待ち)。【市場】市場(現地の客)は風を見ている = AI だけが見えていなかった、が仮説
- **U3(気温水温)**:【分かったこと】「効いて見える特徴」の実体が季節 proxy でありうる。【予測に効くか】素値は効かない。残る新規性は差分系(air_water_gap 等)のみ。【市場】不明
- **U4(階級織り込み)**:【分かったこと】市場は階級を見誤らない。【予測に効くか】階級ラベルはモデル入力からも市場歪み説明からも退場。【市場】完全に知っている
- **U5(交換月)**: ①-6 参照
- **U6(展示補正)**:【分かったこと】方向検出と増幅は別問題。【予測に効くか】増幅の穴 = Intent 層(v2.1)の存在理由そのもの。【市場】市場は展示を同時に見ている(展示情報単独のエッジは限定的)
- **U7(満潮)**:【分かったこと】人間メカニズム仮説(物理の向き)を事前に固定してはいけない → E5W が two-sided 設計になった根拠。【予測に効くか】潮汐薄層は棄却済・交互作用は未検証。【市場】不明
- **U8(風向アイコン)**:【分かったこと】データの「仕様の癖」から不変資産(24場コース方位)が採れた。【予測に効くか】NG-E5W(wind_along/wind_cross)の前提資産。【市場】現地客はコース基準で風を見ている = 市場は使っている情報
- **U9(新人外回り型の全滅)**:【分かったこと】選手 signature は非定常でありうる(キャリア段階と共に消える)= 選手ID固定の静的テーブルは腐る。前づけ勢も引退で判定不能化(同 §6)。【予測に効くか】特徴化するなら as-of の行動プロファイル(直近まくり率・前づけ率)で追随させる — I-1 設計の直接根拠。【市場】未測定
- **U10(イベント型 externality)**:【分かったこと】「あの選手が横にいると隣が化ける(本人は普通)」という narrative は不支持 — 効果は自艇と隣が同時に動く攻め/進入イベント。【予測に効くか】動的ペア相互作用(GAT)より静的プロファイル2特徴で足りる。【市場】未測定

---

## ③ Pattern Library(再現性のある条件付き発見の台帳)

棄却されたパターンも削除しない(棄却3類型: 効果不在 / 実在するが焼き直し / 実在するが織り込み済み)。

### P1. まくり筋の組を AI が系統的に過小評価 【**OOS確定**(2026-09-04)】

- 条件: まくり・まくり差しで決まる筋の3連単組(攻め艇1着+その外の追走艇2/3着・1レース8通り)
- 効果: 発見時 +0.001416・z≈8.4・相対+29% → **NG-E10 完全OOS(2025-07〜2026-06)で gap +0.001298・CI95[+0.001053, +0.001551]・z=10.22・相対+26.3% を再現・確定**。半期4期連続プラス・22/24場プラス・全グレード帯 CI 0非跨ぎ
- n: OOS 44,357レース/354,856買い目/的中2,212 / 検証期間: 発見 2025H1 → OOS 2024H2+2025H2+2026H1
- 確信度: **高(OOS確定)** — 再検証中→確定へ更新(2026-09-04)。事後発見→事前登録→OOS 再現の完走例
- 最終確認日: 2026-09-04(NG-E10 判定)
- 出典: e10_externality_20260904.md §1-2(makuri_oos_results.csv / viz2)/ registry NG-E10 done_primary / audit §13
- **回収の実証(NG-N1・2026-09-04)**: λ_makuri=+0.228 の後段1パラメータ補正(過去1年 fit・固定適用)で P2 完全 OOS の gap が **+0.000166(z=1.3・CI 0跨ぎ)= 相対見落とし +2.7%** まで縮小・副作用ゼロ・鏡像の過大評価も同時解消。主ゲート(レース全体 ΔNLL≥0.003)は閾値が単一セル補正の理論上限より高く FAIL → 採用可否は Owner 判断 #6
- 3問:【分かったこと】AI の負けパターンは「荒れ全般」でなく「まくり筋」に偏る — 構造的な癖と確定、かつ**1パラメータで消せる**。【予測に効くか】較正改善として実証済み(採用は Owner 判断 #6。AI艇報の定量根拠には即使える)。【市場】**未確定 — P2 にオッズ無し。「買える歪み」の確定ではない**(市場側判定は E19SG/締切前オッズ蓄積へ)

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

### P5. 確認済み 選手×コース signature 7件(NG-E10 層3・2026-09-04 新規)

- 条件: 特定選手が特定コースにいるとき、隣接コースの2着以内残差が系統的に動く(比例配分帰無を引いた後・2重再現ゲート通過のみ)
- 効果(shrunk 効果 / P2 再現値・型):
  - 藤山翔大(4561) 3→1 **−12.5pp**(P2 −37.4pp・攻撃スタイル)/ 同 2→1 −9.3pp(−20.4pp)
  - 菅章哉(4571) 3→1 −10.8pp(−11.4pp・攻撃スタイル/外へ28%)
  - 高田ひか(4804) 2→1 −7.3pp(−20.0pp)/ 同 3→4 +4.2pp(P2 +0.1pp = 凍結ルール上は確認だが実質弱い)
  - 大神康司(3574) 5→6 +4.2pp(+9.6pp・**前づけ 進入89%内へ**)
  - 戸塚邦好(4575) 4→5 +3.4pp(+8.6pp・外回り傾向12%)
- n: 各セル 174〜219(前半 2021-2023)/ 検証: 前半 BH-FDR q<0.05 → \|shrunk\|≥2pp 20候補 → 後半 2024-2026H1 + P2 符号再現で 7件(不再現7・判定不能6=引退等で反証ではない)
- 確信度: **中〜高**(統計は2重再現。ただし 7件/1,872選手 = 希少。選手ID固定テーブルは非定常で腐る → as-of 行動プロファイルで追随)
- 最終確認日: 2026-09-04
- 出典: e10_externality_20260904.md §3-4 / viz4_confirmed_signatures.csv / signature_table.csv
- 3問:【分かったこと】憲章§62「特定の選手が特定コースを殺す」は少数の実名選手で統計的に実在。【予測に効くか】I-1 proxy 2特徴(まくり率・前づけ率)でほぼ張れる = N1 補助項+I-1 へ。【市場】未測定(P2 にオッズ無し)

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
- **確定して回収可能と実証済み(採用は Owner 判断 #6)**: まくり筋の AI 過小評価(E10 で OOS 確定 → N1 の1パラメータ補正で gap +26.3%→+2.7%・副作用ゼロを完全 OOS 実証)
- **検証済み・効かないと確定(2026-09-04 第1波)**: レースの格の出力薄層(NG-E1・織り込み済み)・風コース成分の線形形(NG-E5W)・勝負駆け utility(NG-E23・二値/連続の2形式で null)・行動 proxy の薄層(NG-I1・特徴設計は妥当だが薄層では平均化)
- **検証待ち**: SG 市場効率(NG-E19SG・締切前オッズ蓄積待ち)・風の非線形/安定板交互作用(Owner 判断 #7 で起票可否)
- **効かないと確定(従来分)**: 階級ラベル・気温水温の素値・racer ID embedding・容量増・複合損失・race_no・明示積項(いずれも再投入禁止)

### 「市場は既に知っているか」で仕分けると

- **市場が正確に知っている**: 階級(全級 ±0.7pp)・汎用の攻撃タグ / 番組格差 / 1-4-5筋(実在するが織り込み済みで棄却)
- **市場が間違えている**: 本命の価値(−2.9pp 過小・1号艇は全階級で買い得)— ここが AI の賭け得候補
- **AI が見落とすと確定・市場側は未測定**: まくり筋(P1 — AI 側は E10 で OOS 確定。市場が知っているかは P2 にオッズ無く未測 = E19SG/締切前オッズ蓄積で判定)・SG 当日の本命(①-5・n=12 逸話)
- **AI だけが見えていなかった**: 風向・当日気象・安定板(U1/U2/P4)— 修復と特徴化はこれから

### 一番大事な教訓(1行)

**勝ち筋は「賢いモデル」ではなく「モデルがまだ知らない情報」**。12連敗の実験史がそれを証明しており、v2.1 のロードマップ(情報→構造の順)はこの法則の上に立っている。



# ===== research_state.json =====

```json
{
  "updated_at": "2026-09-04",
  "updated_by": "claude/w1-batch-session (elpsykongroo, shin GO=全部go)",
  "canonical_note": "本ファイルが機械可読の正本。人間可読の詳細は同ディレクトリの md 群。Artifact 494f0be1-a091-4cc3-b90f-72df7dc0b01d は view であり正本ではない",
  "architecture_version": "v2.1",
  "architecture_doc": "docs/ARCHITECTURE_FREEZE_v2.1.md",
  "current_phase": "W2 Owner確定順を完走 (2026-09-05 夜間自走)。①NG-N1C: FAIL (λ時間非定常。rolling λ=判断#9) ②部品交換: コード完成・boatrace.jpメンテ明け待ち ③NG-MS1 現在モーター状態: **存在確認PASS** ④NG-E5NR 強風regime Phase A: **PASS (16/18セル生存・逃げ率7m/s+で−10pp)** ⑤NG-ADJ1 選手の調整能力: **PASS (選手差は機体差の3倍・前後半ρ=0.75)**。**存在確認3連PASS = Owner指示「当日Current State推定への重心移動」の妥当性を初日で確認**。次=判断#11 (MS特徴化+再学習ゲート・ADJ統合設計) を筆頭にOwner裁定待ち5点 (#9/#10/#11/#12/部品バックフィル)。P×R設計監査済み (ミニPoC=判断#10)",
  "baseline_model": {
    "id": "b2f41_prod2026_prod3",
    "description": "B2構造化着順NN (41特徴・6艇self-attention・120通り直接softmax・3seed平均) + exh120展示補正層(θ9) + 市場ブレンド(w=0.85・推論後段)",
    "odds_as_input": false,
    "params": 464817
  },
  "best_model": {
    "id": "b2f41_prod2026_prod3",
    "note": "現状 Baseline と同一 (W1 第1波で Baseline を超える昇格なし。5実験とも主ゲートFAIL)"
  },
  "current_experiment": null,
  "current_experiment_note": "実行中なし。第1波5本 (NG-I1/N1/E1/E5W/E23) は 2026-09-04 に並列レーンで実行し全て done_primary。詳細は registry と lane-reports/{i1_proxy,n1_reweight,e1_stage,e5w_wind,e23_utility}_20260904.md",
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
    "completed_w1": [
      {
        "id": "NG-E10",
        "status": "done_primary",
        "date": "2026-09-04",
        "theme": "選手externality統計PoC+まくり筋事前登録再検証",
        "result": "①externality分散成分 PASS: T=10970.5 vs permutation帰無8703.5±62.3 (1000回・seed42)、p=0.001。(コース,年,場)層別の頑健性でも p=0.001。②まくり筋セル OOS PASS確定: 完全OOS 2025-07..2026-06 の44,357R/354,856買い目で gap +0.001298、CI95[+0.001053,+0.001551] (0非跨ぎ)、z=10.22、AI相対見落とし+26.3% (発見時+29%・z≈8.4と同水準)。半期4期連続プラス・24場中22場プラス・全グレード帯 (A1人数proxy) CI 0非跨ぎ。③確認済みsignature 7件 (攻撃スタイル型6/9・前づけ型1/6・新人外回り型0/5=後半全滅は非定常で正しい挙動)。④自艇残差≈0層は p=0.894 = 純粋externality信号ゼロ (効果の実体は攻め/進入イベントで自艇と隣が同時にズレる型)",
        "decision": "N1 GO (主役=まくり筋セル項・選手signature項は補助) / I-1 proxy特徴 (attack_propensity@course, approach_deviation) の前倒し / GAT起票は今回のエビデンスからは不支持 / まくり筋の用途第一=較正改善+AI艇報 (P2に締切前オッズ無し=「買える歪み」は未確定)",
        "integrity_note": "比例配分重みの実装バグを発見→クリップ修正のみ→全層再実行・初回数値破棄 (addendum2で開示)。判定ルール・閾値の事後変更ゼロ。頑健性検定1本は結果計算前に追加宣言 (addendum1)",
        "source": "lane-reports/e10_externality_20260904.md + registry NG-E10 done_primary行"
      },
      {
        "id": "NG-I1",
        "status": "done_primary",
        "date": "2026-09-04",
        "theme": "as-of行動プロファイル proxy特徴 (attack_propensity@course + approach_deviation)",
        "result": "FAIL=特徴昇格見送り。薄層ΔNLL fold1アーム −0.000205 CI95[−0.000932,+0.000472] (0跨ぎ) / fold2アーム +0.001078 CI95[+0.000686,+0.001471] (0非跨ぎだが閾値0.003の約1/3)。fold間符号反転。改善はattack_propensity単独 (+0.00118)。placebo 0/20=fold2の小信号は本物。E10確認済みsignature 7件は全員2特徴の分布の端で捕捉=特徴設計は妥当、薄層6係数では特異選手集中効果が平均化され閾値未達",
        "decision": "F43再学習ゲートは起票しない。i1_features.parquet (206万行・leak test PASS) は資産保存",
        "source": "lane-reports/i1_proxy_20260904.md"
      },
      {
        "id": "NG-N1",
        "status": "done_primary",
        "date": "2026-09-04",
        "theme": "凍結B2への対数線形再重み付け薄層 (まくり筋セル項主役)",
        "result": "主ゲートFAIL (閾値0.003両fold未達: fold1 +0.000531 CI[−0.000029,+0.001123] / fold2 +0.001306 CI[+0.000629,+0.002030])。ただしP2完全OOSで λ_makuri=+0.228 (過去1年fit・固定適用) によりまくり筋gap +0.001298 (z=10.2) → +0.000166 (z=1.3・CI 0跨ぎ) = 相対見落とし+26.3%→+2.7%・グレード全帯で残存消滅。副作用ゼロ (非まくり筋セル悪化なし・鏡像の過大評価z≈−10も同時解消)。signature補助項は両fold CI 0跨ぎで不採用方向。lane指摘: 閾値0.003は単一セル補正の理論上限 (≈0.0013〜0.0015) より高く原理的に到達不能だった (fold2実測はほぼ上限到達)",
        "decision": "このままの形での昇格なし。較正層としての採否は適正スコープの閾値で再ゲートするかの Owner 判断待ち (pending_owner_decisions #6)。福岡・唐津は一律λの過補正で軽度逆方向歪み (場別λは登録外・未実施)",
        "source": "lane-reports/n1_reweight_20260904.md"
      },
      {
        "id": "NG-E1",
        "status": "done_primary",
        "date": "2026-09-04",
        "theme": "レース格カテゴリ (Stage) 薄層",
        "result": "FAIL (③織り込み済が主+①効果不在)。薄層ΔNLL fold1 −0.00055 / fold2 −0.00064 = 符号から逆 (base微悪化)。B2(F41)はsetsu_day/setsu_pts系で格由来シフトを学習済み=出力薄層に拾う残差なし。プラセボ (race_no) は両fold点推定で下回る=格≠レース番号の焼き直し。ex-ante判定器一致率99.20% (昇格条件≥98%クリア)・決定表カバレッジ未分類0.0067%",
        "decision": "B2出力への薄層経路は閉じる。格の実測効果 (ST変化24/24場) の否定ではなく、残る道はB2入力への格特徴追加+再学習 (起票はOwner判断・pending #8)。副産物 venue_date_grade.parquet (29,715行) は NG-E19SG で使用可 (caveat: 上流欠落2023-01〜04中旬)",
        "source": "lane-reports/e1_stage_20260904.md"
      },
      {
        "id": "NG-E5W",
        "status": "done_primary",
        "date": "2026-09-04",
        "theme": "風コース成分 (wind_along/wind_cross) 薄層",
        "result": "FAIL (①効果不在)。ΔNLL fold1 +0.000184 / fold2 +0.000230 = 符号反転なしだが閾値の1/15・CI 0跨ぎ。プラセボ①場×月内perm 20本のmax未満=信号は本物だが微小。プラセボ②季節クリマトロジー置換で効果消失=季節の焼き直しではない。クリーン行(bi風向)はfold窓0行 (biは2026年のみ実在) のためK行 (wx_src=k_rotated) 研究判定+クリーン診断 (2026Q1→Q2 +0.000265 CI 0非跨ぎ・単一窓) で実行 (凍結計画に事前明記)。副次: 風速7m/s+で−0.002174へ符号逆転=線形仮定が強風で破綻",
        "decision": "特徴昇格なし。棄却スコープは「勝者艇番への線形傾き2パラメータ構造」。再挑戦は非線形/安定板交互作用方向のみ (pending #7)。8方位量子化による効果希釈 (attenuation) の可能性を明記",
        "source": "lane-reports/e5w_wind_20260904.md"
      },
      {
        "id": "NG-E23",
        "status": "done_primary",
        "date": "2026-09-04",
        "theme": "勝負駆け utility curve (q_k連続形式・E2+E3統合)",
        "result": "FAIL (①効果不在)。選定K=24 (fold1選定・fold2判定)。ΔNLL fold1 −0.000506 / fold2 −0.000481 = 薄層はbase微悪化・K=12/18でも全負で結論不変。適格レース限定では悪化拡大=増分情報ゼロの追い証拠。θ終値|θ|≤0.033でほぼ無補正。市場軸 (確定オッズdiagnostic・2,051R) はu1五分位×6帯すべてCI 0跨ぎ=utility帯由来の市場歪み検出されず (断定せず)。day-start検証T1-T5全PASS・違反ゼロ",
        "decision": "節の立ち位置 (勝負駆け) 路線は二値 (null済) → 連続 (本実験) の2形式でnull=同路線の再々提案は非推奨。E0/E10個人プロファイリング路線へ寄せるのが合理的",
        "source": "lane-reports/e23_utility_20260904.md"
      }
    ],
    "registered_waiting": [
      {"id": "NG-E19SG", "theme": "SG/G1祭り市場効率", "gate": "two-sided・締切前オッズ=real。蓄積待ち (2026-07-10〜)。grade表は E1 副産物 venue_date_grade.parquet が利用可"},
      {"id": "NG-E8SWAP", "theme": "当地デッドウェイト置換 (起票のみ)", "gate": "E8全滅時のみ着手"}
    ]
  },
  "hypotheses": {
    "note": "本節は要約サブセット。全仮説(29件)の悉皆台帳は HYPOTHESES.md — 収載範囲は台帳側が上位互換",
    "supported": [
      "市場は本命を過小評価する (favorite-longshot。implied0.5+で-2.9pp)",
      "1号艇は全階級で買い得 (イン利は階級を超える)",
      "レースの格で走りが変わる (準優ST-0.0094・24/24場同符号・逃げ率46.7→71.3%)。ただし NG-E1 (2026-09-04) で「B2は既に織り込み済み=出力薄層に残差なし」と確定。現象は実在・予測増分はゼロ",
      "AIはまくり筋の荒れを系統的に見落とす (NG-E10 OOS確定: gap+0.001298・z=10.2・相対+26.3%・22/24場)。NG-N1 (2026-09-04) で λ_makuri=+0.228 の1パラメータ補正により gap→+2.7% (z=1.3) まで回収可能・副作用ゼロと実証 (採用はOwner判断待ち)。「買える歪み」は未確定=P2にオッズ無し",
      "特定選手が隣接コースを系統的に殺す/活かす=選手externalityは実在 (NG-E10 分散成分 permutation p=0.001・確認済みsignature 7件。実体は攻め/進入イベント由来の系統ズレ)",
      "節内の調整推移 (展示タイム系) はB2残差を予測する独立情報 (NG-MS1 2026-09-05: 当日z統制でも残存・元々の強さと直交・最低3次元。**存在確認レベル=予測価値/ROIは未検証**)",
      "強風でレース生成過程そのものが変わる (NG-E5NR Phase A 2026-09-05: 逃げ率7m/s+で−10pp・まくり率+3.8pp・展示の予言力低下。16/18セル生存・記述的確定。**K風=事後観測のため予測特徴化はT1風ソースが前提**)",
      "モーター調整の上手さに選手固有の系統差が実在 (NG-ADJ1 2026-09-05: ICC=0.16=機体差の3倍・前後半ρ=0.752 CI[0.726,0.776]。**存在確認レベル・中身は未分解**)"
    ],
    "testing": [
      "SG/G1は観光マネーで市場が甘くなる (SG当日 AI NLL 0.818 vs 0.981・n=12) → NG-E19SG"
    ],
    "partially_supported": [
      "4カド攻撃型は展開を作る (NG-E10: 攻撃スタイル型signature 6/9再現。NG-I1 (2026-09-04): proxy 2特徴は7件全員を分布の端で正しく捕捉=設計妥当、ただし薄層ゲートはFAIL=全選手一律の薄い補正では特異選手集中効果が平均化される)"
    ],
    "rejected": [
      "階級が予測に効く (全棄却)",
      "高階級は市場で人気過剰 (全級±0.7pp=正確に織り込み)",
      "満潮=まくり有利 (実測は逆方向)",
      "汎用の攻撃タグ/番組格差/1-4-5筋にエッジ (実在するが市場織り込み済み)",
      "節の立ち位置 (勝負駆け) が予測に効く (バイナリ圏内/圏外=統制後消滅 → 連続utility=NG-E23で両fold負。2形式null・同路線の再々提案は非推奨 2026-09-04)",
      "風のコース成分が線形に効く (NG-E5W: 信号実在だが閾値の1/15・強風7m/s+で符号逆転=線形仮定が破綻。非線形/安定板交互作用方向のみ残す 2026-09-04)"
    ],
    "untested": [
      "安定板+強風=イン受難 (尼崎3R連続一貫・n=3逸話。E5W強風符号逆転が傍証を追加)",
      "地元経験は難水面でこそ効く (無条件当地はゼロ効果済) → E8",
      "部品交換は選手の潜在診断信号",
      "師弟・先輩後輩で行動が変わる",
      "ルーキー急成長を市場が遅れて評価する",
      "U-18 展開圧力×対応力 (Generalized Pressure×Resistance) — コース条件付き圧力×対応力×相対位置→期待着順変化→波及 (Owner現場観察 2026-09-05・個人ルール実装禁止・設計監査まで進行中)",
      "U-19 コース条件付き相性 (Course-conditioned Matchup Skill)",
      "U-20 波及と受益艇 (Interaction propagation / beneficiary effect)",
      "U-21 市場の重み付け不足情報 (Known-but-underweighted market information)",
      "U-22 条件付き相互作用の誤価格 (Conditional interaction mispricing。S-5=まくり筋はAI側較正歪みのみ確定、の判定は上書きしない)",
      "U-23 二次・三次受益艇の誤価格 (Second-order beneficiary mispricing)",
      "U-24 シナリオ分散買い (Scenario-aware betting portfolio・購入層の概念。実装は市場レイヤ成熟後)",
      "U-25 頑健EV+下振れ最適化 (Robust EV + downside-aware optimization)"
    ]
  },
  "supported_findings": [
    "予測/市場評価/購入判断の3層分離は既に de-facto 実装済み (B2オッズ非入力・ev層shadow専用純関数・NO BET fail-closed。2026-09-04実コード検証)",
    "展示補正は方向11/12正・増幅が保守的 (Intent層の存在理由)",
    "実験史: モデル改造12連敗・情報追加と推論工夫のみ有効 — W1第1波5連FAILで「B2出力への後付け薄層」の限界も確定 (取れる残差が既にほぼ無い)",
    "まくり筋の較正歪みは1パラメータ後段補正で回収可能 (NG-N1: gap z=10.2→1.3・副作用ゼロ・完全OOS)",
    "風向アイコン=コース図基準の発見 → 24場コース方位テーブル half-auto 完成 (high19/mid5)",
    "モーター交換月は年次で移動する (K 2連率リセット検出で全24場確定)"
  ],
  "rejected_findings": [
    "気温・水温の素値は予測に効く (実体の8-9割が季節の焼き直し)",
    "『A1は人気しすぎ』(市場は階級を正確に織り込む)",
    "純粋externality (自艇は無傷で隣だけ動く型) は信号ゼロ (NG-E10 自艇残差≈0層: p=0.894)"
  ],
  "metrics": {
    "national_fold2_3seed": {"nll": 3.7565, "hit1": 0.1020, "tansho_acc": 0.5746},
    "market_gap_nll": "+0.06〜0.07 (確定オッズde-vig比・diagnostic)",
    "sg_kiryu_20260830": {"head_hits": "9/12", "trifecta_top1": "4/12", "ai_nll": 0.818, "market_nll": 0.981, "n": 12, "label": "逸話・断定禁止"},
    "adoption_line_thin_layer_dnll": 0.003,
    "e10": {
      "externality_variance_T": 10970.5, "externality_null_mean": 8703.5, "externality_null_sd": 62.3, "externality_p": 0.001,
      "pure_externality_p": 0.894,
      "own_diag_sd_pp": "2.9-4.5 (LGB代理の選手スキル取り残し・caveat)",
      "makuri_oos_window": "2025-07-01..2026-06-30", "makuri_n_races": 44357, "makuri_n_tickets": 354856,
      "makuri_gap": 0.001298, "makuri_ci95": [0.001053, 0.001551], "makuri_z": 10.22, "makuri_relative_miss": "+26.3%",
      "makuri_venues_positive": "22/24", "confirmed_signatures": 7,
      "label": "確定は較正の歪み。P2に締切前オッズ無し=買える歪みは未確定",
      "source": "lane-reports/e10_externality_20260904.md"
    },
    "w1_batch_20260904": {
      "n1_lambda_makuri": 0.228,
      "n1_p2_gap_before": 0.001298, "n1_p2_gap_after": 0.000166, "n1_p2_z_after": 1.3,
      "n1_thin_dnll_fold1": 0.000531, "n1_thin_dnll_fold2": 0.001306,
      "i1_thin_dnll_fold2": 0.001078, "i1_signature_capture": "7/7 (分布の端)",
      "e1_agreement_rate": 0.992, "e1_thin_dnll": "fold1 −0.00055 / fold2 −0.00064 (負=悪化)",
      "e5w_thin_dnll": "fold1 +0.000184 / fold2 +0.000230", "e5w_strong_wind_dnll": -0.002174,
      "e23_thin_dnll": "fold1 −0.000506 / fold2 −0.000481 (K=24)",
      "label": "5本とも主ゲートFAIL (採用ライン0.003)。数値の出典は各 lane-report",
      "source": "lane-reports/{i1_proxy,n1_reweight,e1_stage,e5w_wind,e23_utility}_20260904.md"
    }
  },
  "data_status": {
    "official_bk": "2020〜全国・ほぼ完全 (K結果はレース後公開=ラベル専用)",
    "beforeinfo": "2020〜 (2023-01〜04欠落=素データ自体なし)。全356,476ファイルのフルスキャン実測 (2026-09-04 W2監査・エラー0): チルト充足94-97% (F41未収載=未利用100%)・安定板true率4.5-9.8%/年 (場別分布は物理と整合・2026はopenapi由来で構造的欠測0.6%)・気温98.7%/水温95%。**部品交換列は6.5年間パーサ取り違えで前走成績(同日前走のレース番号)を保存していた=部品交換データは実質未収集** (選手ID照合119/119で確定。正解実装は fetch_beforeinfo_ext.py に既在。前向き修理≈0.5日・過去分は生HTML未保存のため再スクレイプ35万ページ≒12日=Owner GO必須・openapiでは取れない)",
    "era5": "2020〜2026-09 毎時24場 140万行 (気圧/湿度/突風/空気密度)。事後再解析=本番は予報アーカイブ要",
    "odds_preclose": "全国 2026-07-10〜蓄積中 (real EV評価はこれのみ)",
    "setsu_master": "全期間5,311節 (artifacts/research/nextgen/setsu_master.parquet)",
    "static_assets": "venue_course_azimuth.json (high19/mid5) / venue_branch_map / motor_exchange_months / venue_latlon / venue_date_grade.parquet (E1副産物・29,715行)",
    "research_assets_w1": "i1_features.parquet (選手×コースas-of行動プロファイル206万行・leak test PASS) / e1_stage_decision_table.csv (8カテゴリ・一致率99.2%) / e5w_features.parquet (風コース成分) / e23 utility.parquet",
    "missing_wishlist": ["選手コメント時系列(HIGH)", "プロペラ形状(HIGH・困難)", "1M映像展開(MED・打ち切り済)", "人間関係(MED)", "ピット常時(LOW-MED)"]
  },
  "overfitting_status": {
    "fold_contamination": "fold1/fold2は開発汚染済み=採否の最終根拠にしない",
    "gates": "G0事前登録→G1 2fold一貫+bootstrap CI95→G2 3seed→G3 prod2026窓→G4 ECE→G5 市場(diag/real分離)→G6 8segment",
    "danger_zones": ["Player×Course×Stage×Wind等の細分サンプル枯渇 (積項でなく共有表現)", "万舟数本集中の利益 (検知をハーネスに組込予定)"],
    "w1_note": "第1波5実験は全て事前登録→凍結→機械判定を完走。バグは全件addendum開示+初回数値破棄で再実行 (I1×1件・N1×2件・E1×1件)。判定ルールの事後変更ゼロ"
  },
  "leakage_status": {
    "defense": "5層 (列名ガード/日付split/集計方向shift(1)/入力由来許可リスト/replay時刻)。本番経路に既知の直接リークなし",
    "known_risks": ["同日クロス会場ソート (パッチ済・本番見送り中・新研究は新ソート必須)", "Stage/節内集計の同日後レース混入 (day-start規約。E23はT1-T5機械検証で違反ゼロを確認)", "気象の確定観測vs締切前 (§51)", "選手コメントのレース後混入 (前向き収集のみ可)"],
    "unusable_scripts": ["real_backtest.py / walk_forward_eval.py (未来漏れ未修正・新研究で流用禁止)"]
  },
  "pending_owner_decisions": [
    {"n": 1, "item": "live気象修復パッチ (P0)", "recommend": "適用"},
    {"n": 2, "item": "7/27劣化153件修復", "recommend": "適用"},
    {"n": 3, "item": "風向16方位パーサ", "recommend": "適用"},
    {"n": 4, "item": "openapi日次取り込みを夜間ジョブへ", "recommend": "追加"},
    {"n": 5, "item": "同日ソートキー修正の本番適用", "recommend": "見送り (研究ビルドのみ)"},
    {"n": 6, "item": "N1 まくり筋較正層の扱い", "decision": "GO (Owner 2026-09-04)。Calibration-specific Gate を NG-N1C として新規事前登録済み (①対象セル|z|<2+CI 0跨ぎ ②全体NLL非劣性 ③非対象セル非悪化 ④walk-forward 3期再現 ⑤場別致命的過補正ゼロ ⑥福岡・唐津の主因診断)。NG-N1 の旧判定は変更しない (旧ゲートではFAILのまま保持)。場別λは診断のみ・本番採用せず過学習リスク評価"},
    {"n": 7, "item": "E5W 風の再挑戦方向", "decision": "GO (Owner 2026-09-04)。線形2パラメータ形はFAIL固定・同一形再提案禁止。NG-E5NR (Nonlinear Environmental Regime) を事前登録済み — まず「強風でレース生成過程が変わるか」の最小統計PoC (逃げ率/ST/決まり手/まくり率/外艇Top3/展示→本番の分布変化)。巨大interactionモデルの一括実装は禁止。安定板はn小逸話を真実扱いせず新規仮説として扱う"},
    {"n": 8, "item": "E1 格特徴のB2入力側追加+再学習", "decision": "DEFER (Owner 2026-09-04)。「レース格は無意味」とは扱わない — 現象 (ST・逃げ率変化) はSUPPORTED・追加予測価値は現B2では薄い (F41から65%再構成可・新情報量薄・再学習コスト大・モデル改造12連敗)。他の新規入力とまとめて再学習するタイミング / architecture revision / Stage Expert の明確な追加証拠が出た場合に再検討"},
    {"n": 9, "item": "rolling/as-of λ によるまくり筋較正の再挑戦 — NG-N1C FAILの主因はλの時間非定常 (2024H2 +0.17→2026H1 +0.28)。fitを直近窓で逐次更新するas-of設計なら④の主因に直接対処できるが、新規事前登録が必要な別実験", "recommend": "起票 (コスト小・非対象セル副作用③への対処設計も込みで。ただしFAILの繰り返しを避けるため③の多重検定設計を含め慎重に事前設定)"},
    {"n": 10, "item": "P×R (展開圧力×対応力) Step1-2 ミニPoCの並行実行可否 — 設計監査済み・新規データ取得ゼロ・E10/I1資産流用のみ。FAILでもGAT恒久棚上げの決定価値", "recommend": "既定W2の待ち時間に並行1レーンで実行 (順位変更はしない)"},
    {"n": 11, "item": "現在モーター状態の最小特徴化+OOSゲート起票 — NG-MS1で存在確認PASS (展示タイム系の節内推移が当日値で表現できない独立情報・元々の強さと直交・最低3次元)。次段階はB2入力側特徴追加=再学習を伴う", "recommend": "起票 (extra3以来の真の新規as-of情報。実験史「情報追加のみ有効」と整合。設計論点=節初日水準+当日値+推移の合成、2024-06以降しかパネルが無い点の学習窓設計、K由来列の張替え)"},
    {"n": 12, "item": "強風regime Phase B (最小regimeモデル・生存16セル対象) の起票可否 — Phase A PASS (逃げ率−10pp/まくり+3.8pp/展示予言力低下が7m/s+で確定)。重要制約: K風=事後観測のため予測特徴化にはT1時点の風ソースが必要 (biは2026のみ)", "recommend": "T1風の可用性を先に固めてから起票 (風向パーサ適用済み日次取り込み #4 の蓄積 or bi 2026+のみで小規模検証)。焦って事後風でモデル化しない"}
  ],
  "w2_directives_owner_20260904": {
    "design_shift": "B2出力への後付け薄層は枯渇 → ①真に新しい入力情報 ②条件付き/regime-specific情報 ③Calibration ④Market Evaluation ⑤Current State推定へ重心移動。「公開静的情報をもう1個足す」より「レース当日のCurrent State推定」を優先",
    "motor_current_state": "W2最重要候補の1つ。単一スカラー化しない (Stretch/Acceleration/Turn Exit/Turning/Handling/起こし/Stability/Setup Confidence 等の複数軸latent候補)。人間が正解ラベルを固定しすぎない — 観測可能proxyは明示・不明部はlatent表現",
    "maintenance": "部品名フラグで終わらせない。Latent Problem → Intervention → Observed Response の構造 (交換前の不調・交換後の展示/ST/着順残差/コメント変化・翌日以降の改善・選手差)",
    "player_adjustment_skill": "同じ悪モーターからの改善能力の選手差。partial pooling / shrinkage / as-of更新前提。小標本選手を固定評価しない",
    "setup_confidence": "ペラ形状が直接取れなくても調整発言/頻度/チルト変更/展示推移/本番結果から Setup Confidence / Adjustment Volatility / Convergence を推定できないか",
    "discipline": "Expert群/GAT/Master Integratorを一気に実装しない。存在確認→最小PoC→OOS再現→単純特徴で表現できない場合のみアーキ投資 (E10でGATを即起票しなかった規律を維持)",
    "market_separation": "Fundamental→Calibration→Market Evaluation→Betting Decisionの分離を絶対維持。まくり筋補正が較正採用されても「市場Edgeがある」とは扱わない。市場側は締切前オッズ蓄積後に別途検証 (E19SG常時継続)",
    "w2_candidates": "A=Motor Current State / B=Maintenance・Parts / C=Player Adjustment Skill / D=Propeller・Setup Confidence latent / E=Nonlinear Wind・Stabilizer Regime / F=Local×Difficult Conditions / G=Dynamic Player Skill Trajectory / H=Market Evaluation・Recognition Lag — 各候補を期待予測価値/未利用情報量/データ品質/as-of化/leakage/実装コスト/n/B2重複/市場織り込み/EIGで評価して順位提案 (監査実行中)",
    "new_concepts_hypothesis_only": "Daily Race Regime (当日1R〜現在Rの逐次推定) / Player×Motor Compatibility / Attack×Resistance (受け側の抵抗) / Tactical Predictability / Value of Information — 真実として実装せず、適合性とEIGで順位付けして必要なら研究候補化",
    "segment_eval": "Dynamic Player State系は全国平均NLLだけでなく若手/急成長/急低下/特定コース/特定Stageのsegment valueも確認 (I1の教訓: 現象説明できても全国NLLに効かない可能性)"
  },
  "w2_audit_20260904": {
    "source": "lane-reports/w2_data_audit_20260904.md + artifacts/research/nextgen/w2audit/w2_data_audit.json (beforeinfo 356,476ファイル・フルスキャン実測)",
    "ready_now": ["チルト (24場2020-26・充足94-97%・節内変更追跡可・未利用100%)", "安定板 (true率4.5-9.8%/年・場別分布が物理と整合・2026年openapi欠測caveat)", "展示の未利用粒度 (節内日次推移・スタ展進入変化13.06%=スタブ疑い検証済みシロ)", "モーター識別 (場,motor_no,交換年度キー成立・物理11,669機・中央値202走/機)", "節マスタ/standing_panel (356,580行/2,059,541行)", "気象 ERA5 1,403,136行"],
    "repair_needed": ["部品交換: パーサ修正+前向き収集=小(≈0.5日・fetch_beforeinfo_ext.pyの正解実装を移植)。過去分バックフィル=大(再スクレイプ35万ページ≒12日・Owner GO必須)"],
    "acquisition_needed": ["新ペラフラグ (beforeinfoページに列は実在→部品交換修理に相乗り可)", "選手・調整コメント (手元に無し・前向きのみ・fetched_at付きingest guard設計)"],
    "leakage_top3": ["features.parquetの展示/進入/ST/気象はK(レース後)由来 — 新規Motor研究が素で読むと即事故。beforeinfo由来へ張替え必須", "national buildの同日ソート順欠陥 — 節内Motor State等の同日集計の前に研究ビルドのソートキー修正が前提", "2026年のソース断層 (openapi: 部品/安定板欠測) — 年×ソース交絡につき_sourceフラグ伝搬必須"],
    "w2_priority_proposal": [
      {"rank": 1, "id": "NG-N1C", "why": "登録済・実装ゼロに近い・唯一のOOS確定歪みの回収。即実行可", "eig": "高/コスト極小"},
      {"rank": 2, "id": "W2-A Motor Current State PoC", "why": "未利用100%のチルト+展示節内推移+安定板+モーター識別が全部「今すぐ使える」。as-ofはbeforeinfo由来で清潔。B2重複は成績3本+展示z9本のみ", "eig": "高"},
      {"rank": 3, "id": "W2-B 部品交換パーサ修理+前向き収集開始", "why": "≈0.5日で資産が毎日積み上がり始める (待つほど損)。分析自体は蓄積後orバックフィルGO後", "eig": "高(遅延回収)/コスト極小"},
      {"rank": 4, "id": "NG-E5NR Phase A", "why": "登録済・統計PoCのみでコスト小。安定板データ準備完了", "eig": "中〜高"},
      {"rank": 5, "id": "W2-C Player Adjustment Skill", "why": "W2-Aの産物 (motor state panel) に依存するため後続。partial pooling前提", "eig": "中〜高"}
    ],
    "deferred_candidates": {"D": "Setup Confidence — コメント前向き収集の蓄積待ち (チルト変更・展示volatility部分は W2-A に内包)", "F": "Local×難水面 — E8SWAP着手条件のまま", "G": "Dynamic Player Trajectory — I1教訓によりsegment評価設計を先に固めてから", "H": "Market Recognition Lag — 締切前オッズ蓄積+holdout解封 (11/1) 後"}
  },
  "w2_directives_owner_20260905": {
    "status": "W2正式GO + 次期研究思想の統合 (Owner全文指示 2026-09-05)。全テーマは 観察→一般仮説→最小統計PoC→OOS再現→予測価値→市場価値→必要ならArchitecture投資 の順で扱う",
    "confirmed_order": ["並行: NG-N1C (まくり筋較正最終検証・旧N1のFAIL判定は不変)", "並行: 部品交換パーサ修理+前向き収集 (分析でなくデータ資産・即実施。誤パース列の再利用は絶対禁止。取得=部品交換/新ペラ/交換種類/fetched_at/source/race_id/racer_id/motor identity/as-of保証metadata)", "次: Current Motor State PoC (「元々強いモーターか」でなく「この選手がこの節で調整した結果、今この時点でどういう状態か」のas-of推定。features.parquetのK由来列は直接流用禁止=beforeinfo由来as-ofへ張替え必須)", "その後: NG-E5NR Phase A (強風regime)", "その後: Player Adjustment Skill"],
    "backfill_decision": "35万ページ全バックフィルは未承認。まず Stratified Maintenance Backfill PoC (場・年度・季節・グレードで層化した小規模取得) で 正常取得率/部品交換発生率/新ペラ発生率/部品種類分布/前後レース接続率/展示接続率/モーター個体追跡率/交換後追跡走数/仮説検証に必要な標本充足/polite実測速度 を確認 → 全量のEIG/コストを再推定してOwner再判断",
    "pressure_resistance": {
      "scope_now": "事前研究設計+データ可用性監査まで (既定W2は止めない。EIGが極めて高いと判断したら理由付きで順位変更案を出す)",
      "hypothesis": "Course-conditioned Pressure × Course-conditioned Resistance × Relative Position → 相手艇の期待着順変化 → 周囲艇への展開波及 (圧力を作る側×受ける側の対応力)。個人ルール(峰・毒島・茅原等)としては実装しない — 現場観察は仮説形成の例であり統計的事実ではない",
      "profile_axes_hypothetical": "Pressure側: Inside/Attack/Sashi/Makuri/Makuri-sashi Pressure・Outside Compression・Neighbor Disruption・Opportunity Creation / Resistance側: Strong-In Resistance・Attack Resistance・C2 Preservation・C3/C4 Survival・Defensive Turn・Second-place Preservation・Collapse Avoidance・Pressure Absorption — 名称付き能力を真実扱いせず、まず観測可能な残差構造を確認",
      "poc_protocol": "Step1: 艇Aの在席が艇BのB2残差に与える影響をas-ofで測定 → Step2: 影響量がB側でも系統的に変わるか → Step3: Bの圧力耐性をshrinkage付きで推定 → Step4: A単独/B単独/A+B/A×B比較 → Step5: interactionのOOS追加価値 → Step6: Bの崩れの波及 (内隣/外隣/5-6号艇のTop2/Top3変化)",
      "pair_order": "全ペア巨大モデル禁止。サンプル多く意味の強い関係から: 1→2 / 2↔3 / 3→4 / 4→5 / 攻撃艇→外側追走艇 / 前づけ艇→周囲艇",
      "gat_condition": "GAT即実装不支持は維持。pair interactionがOOS再現し単独Profileで表現できない追加価値が確認された場合のみGAT/pairwise/message passingを再評価。再現しなければGAT導入理由に使わない"
    },
    "market_philosophy_update": "「誰も知らない秘密情報」でなく Known-but-underweighted Information / Conditional Interaction Mispricing / Second-order・Beneficiary Mispricing を主戦場に。一次(攻める本人)だけでなく二次(直接影響を受ける艇)・三次(崩れから利益を受ける艇)まで市場価格とのズレを調べる。重点確認=「攻める本人は売られるが展開受益者は十分売られていない」現象。締切前オッズ蓄積後にInteraction Patternごとの model prob/market implied/pre-close movement/EV/beneficiary ticket EV/反応速度/最終反映量を評価",
    "edge_separation_gates": "現象が存在する→AI予測に追加価値→市場が十分価格化していない→実際に購入EVがある は全部別ゲート。混同禁止。Market LayerはFundamental Predictionと完全分離を継続",
    "scenario_portfolio": {
      "principle": "最終購入を「予測確率の高い3連単を上から買う」設計にしない (Owner方針)。レースを複数シナリオ (例: 1逃げ/3攻め1凌ぎ/3攻めで2-3崩れ5浮上/3攻め完全成功/波乱) として扱い、Ticket×Scenario exposure を評価。1-2-3/1-2-4/1-2-5は3点でも「1逃げ+2残り」への集中投資",
      "optimizer_metrics_candidates": "Expected Return / Robust EV (確率が多少ズレても残るEV) / Scenario Coverage / Concentration (同一シナリオ依存度) / Probability of Total Loss / Downside Risk (CVaR等・必要なら) / Epistemic Uncertainty",
      "anti_pattern": "的中率のためだけの低EV舟券大量追加は禁止。追加舟券には十分なRobust EV OR 有意なScenario diversification benefit を要求。目的=EVを維持したまま主要シナリオ耐性を高め下側リスクを抑える"
    },
    "target_architecture_concept": "Fundamental Race Model → Current State → Interaction/Scenario Model → 120通りFundamental Probability → Calibration/Uncertainty → Market Evaluation → Scenario×Ticket Payoff Matrix → Portfolio Optimization → BET/NO BET。現時点では概念のみ・一気に実装しない",
    "new_themes_registered_as_hypotheses": ["1. Generalized Pressure×Resistance (展開圧力×対応力)", "2. Course-conditioned Matchup Skill (コース条件付き相性)", "3. Interaction propagation / beneficiary effect (波及と受益艇)", "4. Known-but-underweighted market information", "5. Conditional interaction mispricing", "6. Second-order beneficiary mispricing", "7. Scenario-aware betting portfolio (シナリオ分散買い)", "8. Robust EV + downside-aware optimization"],
    "console_rule": "Research Mirror/Artifactは内部IDだけで説明しない。各研究に日本語一言名+何を調べる/なぜ重要/今何が分かった/次に何を/市場エッジとの関係 をスマホで読める形で。内部IDは括弧内の補助",
    "discipline": "post-hoc閾値変更禁止 / holdout汚染禁止 / leakage禁止 / small-n断定禁止 / closing oddsをreal EV扱いしない / fundamental predictionにオッズ非入力 / FAIL書き換え禁止 / PoC前の巨大Architecture禁止 / Model improvementとMarket edgeの混同禁止 / NO BET=first-class decision"
  },
  "next_actions": [
    "W2実行順 (Owner確定 2026-09-05): 【並行実行中】①NG-N1C まくり筋較正最終検証 ②部品交換パーサ修理+前向き収集+Stratified Backfill PoC【次】③Current Motor State PoC【その後】④NG-E5NR ⑤Player Adjustment Skill",
    "並行: Generalized Pressure×Resistance (展開圧力×対応力) の事前研究設計+データ可用性監査 (実験はまだ・設計まで)",
    "全バックフィル(35万ページ)は未承認 — 層化PoCの結果でEIG/コスト再推定→Owner再判断",
    "常時: NG-E19SG (締切前オッズ蓄積 2026-07-10〜。grade表=E1副産物が利用可)",
    "市場アノマリー3テーマ holdout 封印中 (2026-09-01〜10-31)。集計・閲覧は 2026-11-01 以降"
  ]
}

```
