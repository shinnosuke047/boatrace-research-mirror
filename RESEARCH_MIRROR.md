# KYOTEI-AI RESEARCH MIRROR(外部AI共有用・読み取り専用)
生成日: 2026-09-10 / 正本: kyotei-ai リポジトリ /research/ 配下(本ファイルはその連結コピー)
注意: 数値の正直ルール(小標本=断定禁止・確定オッズ由来=diagnostic)を前提に読むこと。本文書には市場の歪みの所在(研究エッジ)が含まれる — 取り扱いは Owner(shin)の指示に従う。
---
# OWNER VIEW — 5 分で分かる研究の現在地(人間向け・日本語)

- 更新: 2026-09-10 16:10(Owner 研究指令 第 2 弾「AI と市場の意見差を較正し、本当に買えるエッジが現実的な頻度で残るか決着させる」の実行後)
- 位置づけ: 正本(NEXT_ACTIONS / DECISION_LOG / DATA_STATUS / FINDINGS / registry)の人間向け要約。内部 ID は括弧で添えるだけ。数値の細部は各正本と lane-reports/t3d3_market_shrinkage_20260910.md へ
- 最終ゴール: 未来の未見レースで、締切前に固定したルールだけを使って、実際に取得可能なオッズで BET / NO BET を決め、資金を増やせるかを判定すること

## 1. 今何が分かったか(今回)

- **AI の確率を市場の確率へ 3〜6 割寄せるだけ(調整つまみ 1〜2 個・新しい AI は作らない)で、予測そのものは良くなった**。3連複・2連単・2連複では「AI 単独」「市場単独」のどちらより当たりの見立てが正確になり、3連単は市場と同じ精度まで、単勝だけは AI 単独のままが最も良い。寄せ幅は市場の丸写しにはなっていない(NG-T3D3)
- **「EV がある」と選んだ後の過信も、的中率で見ればほぼ直った**。2連単は完全に(言った確率どおり当たる)、2連複・3連複もほぼ。3連単だけは直り切らない(実際の的中は言った確率の 6 割)
- **買える候補は大量に残る。頻度はまったく問題にならない**。EV 1.15 以上が 1 レースに 0.6〜1.5 組、全国換算で年 2〜8 万点。1 レース 1 点に絞っても 1 日 100 点前後。真偽の判定は数か月〜1 年でつく(20 年かかる戦略は 1 つも無かった)
- **ところが、実際に受け取る額(確定配当)で見ると 4 券種とも 1 を割る(0.64〜0.85)**。理由は 2 段: ①選んだ組の配当は締切までに 8〜15% 下がる(1〜3 分で。3 分前なら 3〜4 割、単勝は 6 割)②的中率では較正できていても、金額を支配する「高配当の組」ではまだ AI の確率が高すぎる。つまり残った過信は「オッズの高さ」に沿って偏っている
- 事前に固めた機械判定は**ケース1(3連複・2連単・2連複が Market Gate 候補・3連単は却下)**。しかし実際の受取額まで見ると**ケース3 寄り(AI と市場の食い違いは主に AI の誤差で、買える歪みはまだ証明できていない)**。判定ルールに「実際の受取額」を入れていなかったのは私の設計漏れで、ルールは事後に変えていない(別掲で示した)
- 唯一の例外候補: 桐生・住之江の 2連複を締切 3 分前の板で選んだとき、実際の受取額が 1.07〜1.24(300〜600 点・偶然の範囲かどうかまだ言えない)= もっとデータが要る
- 3連単を主商品にする理由は残っていない。1 分前の板では却下、8 分前の板の「合格」は締切までに消え、収束も一番遅い
- 知人(競艇 AI 研究者)の研究ノート 161 項目と照合: 一致 28 / 食い違い 9(測り方の差で説明可)/ 未検証 7。「問題は選び方」「EV で選ぶと誤差を拾う」「2連複が相対的に有望」「単勝は締切までに半減」は一致。知人が唯一残した候補は「市場と市場の食い違い」で今回の AI ブレンドとは別物。今回の「食い違いに応じて縮める」は知人が試していない分岐

## 2. それで何が変わったか

- 「AI vs 市場」の勝負は、**予測精度では AI+市場のブレンドが勝つのに、財布では負けている**という形で決着しつつある。負け方が「頻度」でも「的中率」でもなく「価格」と「高配当側の過信」に絞れた
- 直すべき箇所は 1 つ: **配当の高さに応じて AI の確率をさらに縮める**(つまみ +1〜2 個)。それで実際の受取額が 1 を超えるかを、次は最初から「受取額」で判定する
- 締切直前〜締切後のオッズは今日 15:45 から自前で貯まり始めた(24 場・5 券種・1 日約 3,000 リクエスト)。11/1 まで値は見ない
- 仮想運用(shadow)の単勝は、今夜から「3連単から逆算した単勝価格」で EV を判定する(本番の買い方は不変)
- 本番モデルと 11/1 の holdout 判定ルールは変更なし

## 3. 儲けるまで何が足りないか

- **高配当側の過信を直しても、実際の受取額で +EV が残るか**(次の 1 手)。残らなければ「現 AI では市場に勝てていない」を認め、11/1 の開封と自前の締切直前価格を待つ
- 締切直前(10 秒前〜締切後)の実価格の自前データ(今日から蓄積・11/1 まで封印)
- 実弾の資金管理設計は未着手のまま(候補が出てから)

## 4. 今動いているもの

- 部品交換履歴のバックフィル: 約 5 万ページのうち 8,453(9/16 完走目安)
- 締切直前オッズの自動収集(3連単 = 7/10〜・単勝 = 7/16〜・**5 券種の締切直前〜締切後 = 9/10〜**)と holdout の封印
- 仮想運用の単勝(方式 A 判定・毎晩 23:30)
- 実行中の実験: なし(T3D3 完了)

## 5. 次の 1 手

- **「配当の高さに応じて縮める」較正を 1 本だけ事前登録して実行し、判定を「実際に受け取る額」に置く(Owner GO)**。合格した券種だけ Market Gate へ。全滅なら Market Gate を閉じる

## 6. Backlog に送った面白い仮説(実験はしない・次の 1 手より先に着手しない)

- コース構造 × 攻め手の型 × 受け手の型(H-A)/ 特定水面への習熟 × 調整能力(H-B)/ レース形成の感度マップ(H-C)/ 上手い予想家の逆解析(H-D)
- 次点で回収するもの(設計済み・実行は Owner GO): SOB1 の将来窓再現 / 小さい SC2(優先度低)/ Historical Replay の最小試作(8 時間・設計済み)

## 7. 棄却済みで再研究しないもの(同じ形では再提案しない)

- 階級(A1/B1)は予測に無関係 / 満潮=まくり有利は逆 / 気温・水温の素値は季節の焼き直し / 当地・地元は無条件では効かない / 純粋 externality は信号ゼロ
- モデル改造で強くする(12 連敗)。効くのは情報追加と推論工夫だけ
- レースの格の後付け / 風の線形 2 パラメータ / 勝負駆けの utility / 行動 proxy 薄層 / まくり筋の固定 λ・rolling λ
- 受け手側の「圧力への対応力」の個人差(検出不能)→ GAT は棚上げ / モーター状態の入力昇格 / 当日展示の入力側化(clean 窓でも FAIL)/ 読める=儲かる
- 「3連単の選択後の過信は着順順序付けの問題」→ 否定 / 「全券種で 60〜150 倍を見る」は禁止のまま
- **今回追加: 「表示オッズで EV を判定する」は運用前提として棄却済みだったが、「ブレンドで的中率を較正すれば表示 EV が実現する」も否定(実現値は全券種 <1)** / 「3連単を主商品にする理由」は消えた
- Owner 禁止(作らない): 大型 Scenario Generator / Race Simulator / Portfolio Optimizer 本番化 / GAT 再起票 / 券種専用 NN・券種専用特徴・巨大 calibration network / 拡連複・複勝への拡張 / バックフィルの停止・再起動・35 万拡張 / holdout の閲覧

(棄却理由の全文と内部 ID = HYPOTHESES.md §5 / 今回の詳細 = lane-reports/t3d3_market_shrinkage_20260910.md)

---
# §16 サマリ層(機械生成 — 編集しない・正本は下部の連結全文)
生成日: 2026-09-10 / 生成元: research_state.json + experiment_registry.jsonl + NEXT_ACTIONS.md + DECISION_LOG.md + DATA_STATUS.md + FINDINGS.md

## 1. Current Production(現在の本番)
- Best = Baseline = **`b2f41_prod2026_prod3`**(オッズ入力なし)
- 実体: B2構造化着順NN (41特徴・6艇self-attention・120通り直接softmax・3seed平均) + exh120展示補正層(θ9) + 市場ブレンド(w=0.85・推論後段)
- 主要指標: 全国 fold2 NLL **3.7565** / Hit@1 **10.20%** / 単勝Acc **57.46%**。市場との残距離 NLL +0.06〜0.07 (確定オッズde-vig比・diagnostic)
- 採用ライン(薄層): ΔNLL ≥ 0.003

## 2. Active Research(実行中・待機中)
- 実行中の実験: なし(Owner 指令 第 2 弾 完走 (2026-09-10 16:10)。実行中の実験なし。自走 = 部品バックフィル PID 12667 + forward collector 試験 (NG-FC1・9/11〜9/24 メタデータ評価)…)
- 自走ジョブ: 部品層化バックフィル PID 12667(status=running・8953/49968 ページ・残り目安 5.6 日)
- NG-E19SG(registered): SG/G1 festival-day market-efficiency segment (charter §52/§55, backlog 2-5)
- NG-E8SWAP(filed): dead-weight local features replacement ablation (filed only)
- NG-FC1(registered): forward collector (締切直前〜締切後オッズ前向き収集・close_window) の 2 週間試験運用 — Owner 研究指令 2026-09-10 第 2 弾 §9 GO で launchd 登録…

## 3. Latest Findings(直近の判定 5 件)
- **NG-T3D1**(2026-09-09・done_primary・PASS): H1 PASS: fire 41本の drift 中央値 phase1 2場全艇 0.526 [0.43,0.65] / 24場勝者 0.417 [0.39,0.45] / phase2 (先方 final 全艇 910R) T-3 0.667 [0.48,0.81]・T-3再判定 0.569 [0.36,0.75]・T-5 0.474 [0.39,0.74]、placebo p=0.000。先方申告 0.446 は CI 内。H2 INCONCLUSI…
- **NG-T3D2**(2026-09-10・done_primary・PASS): 方式 A (3連単含意単勝 0.75/p3t) PASS・優位: T-3 判定 EV≥1.15 の締切価格 EV>1 survival 58% [52,66] (n_sel 200) vs naive (AI×表示単勝) 32% [29,36] (n=678)・FPR 42% vs 68%・closing price error 0.28 vs 0.46。方式 B (drift 補正 EB 9帯×7ビン×選択) FAIL 33% [27,38]・OOS …
- **NG-EXIN1**(2026-09-10・done_primary・FAIL): FAIL_STACKED (凍結窓 holdout S n=4,530・B=2000): B−A +0.00711 [+0.00154,+0.01292] / C−A +0.00781 [+0.00230,+0.01357] / C−B +0.00070 [−0.00007,+0.00150] = RESIDUAL_ZERO。raw B−A0 (θ なし) −0.0144 だが θ_A の便益 −0.0213 が上回る。パネル fold2: B−base…
- **NG-TS1**(2026-09-10・done_primary・—): ケース D (選択そのもの)。AI-only 選択 (S1/S2/S3) は 4 券種すべて CALIBRATED (replica 59,923R: CR 0.99〜1.01・ECE ≤0.0023・傾き 0.99〜1.01)。EV≥1.15 上位 3 組 (S5) は T-1 (24 場) で 3連単 0.61 [0.52,0.71] / 3連複 0.73 [0.67,0.78] / 2連単 0.74 [0.68,0.80] / 2連複 0.76 […
- **NG-T3D3**(2026-09-10・done_primary・—): 機械判定 (凍結 t3d3_frozen.json・test = prod3 2026-07-01〜08-31・B=2000): 選ばれた λ は全券種で内点 (3連単 T-1 B_abs λ̄0.59 / 3連複 A 0.50 / 2連単 A 0.41 / 2連複 B_signed 0.31+0.047z / 単勝 ≈0.09)。NLL: 3連複・2連単・2連複はブレンドが AI・市場の両方より良い (NLL_BETTER)、3連単は市場と同等 (TI…

## 4. Research Queue(優先順位付き — 正本 = NEXT_ACTIONS.md)
# NEXT_ACTIONS — 現在優先すべき研究(3〜5件だけ) 最新更新: 2026-09-10 16:10(**Owner 指令 第 2 弾「AI と市場の意見差を較正し、本当に買えるエッジが現実的な頻度で残るか決着させる」完走: NG-T3D3 = 凍結判定ケース1(3連複・2連単・2連複 = MARKET GATE CANDIDATE・3連単 = REJECT・CORE なし)/ 実質ケース3 寄り(hit 較正は回復・表示価格の EV は残る・確定配当ベースの実現値は全券種 <1)/ Frontier・Time-to-Evidence(頻度は制約でない)/ 知人 Crosswalk / forward collector 稼働 / shadow 方式 A 稼働 / Replay 設計**。Owner 表示 = research/OWNER_VIEW.md)。実行中の自走 = 部品バックフィル(PID 12667・ETA 9/16)+ forward collector 試験運用(NG-FC1・9/11〜9/24)+ shadow 方式 A(nightly 23:30) …

## 5. Passed(ゲート通過・採用済み)
本番採用済み(ADOPT):
- **B2**: 120通り直接スコアリング+6艇attention — 全指標でB0/B1超え (唯一のアーキ勝利)
- **extra7**: 当地収縮+節内フォーム7特徴 — fold2 NLL 3.785→3.777
- **extra2**: 場×コース歴史率+直近5走 — extra2単独で全国Hit@1 9.88→10.07%、3seed併用で10.21%
- **extra3**: ST分布+節内得点 (F=41完成) — ΔNLL -0.004〜-0.007
- **seed3**: 3seed確率平均 — +0.14pp (3で飽和)
- **exh120**: 展示タイム/ST/F の後段補正層 — ΔNLL -0.018 研究窓・24/24場改善
- **mkt_blend**: 市場ブレンド w=0.85 (推論後段) — 住之江で市場単独NLL超え
- **f41_skew_fix**: 学習気象を beforeinfo 由来へ統一 — GATE PASS (2026-08-06切替)

事前登録ゲート PASS(本番昇格は別途 Owner GO):
- **NG-E10**(done_primary): 層1 externality分散成分 PASS (T=10970.5 vs 帰無8703.5±62.3, p=0.001, permutation1000回。場層別頑健性もp=0.001)。まくり筋OOS PASS確定 (2025-07..2026-06の44,357R: gap+0.001298 CI95[+0.0…
- **NG-E5NR**(done_phaseA): Phase A PASS=強風regime変化あり (18セル全てBH q<0.05+前後半18/18符号一致 → プラセボ棄却後16/18生存・効果は風速に単調)。1号艇逃げ勝率 5-7m/s帯 −7.4pp CI[−8.0,−6.6] / 7+帯 −10.0pp CI[−11.2,−8.7]。まくり率 +2.1〜…
- **NG-MS1**(done_primary): PASS=状態変化シグナルあり。①展示タイム系が最強: 全3枠帯でBH通過・前後半符号一致 (ex_slope 枠1 −0.0071 CI[−0.0101,−0.0040] / 枠2-3 −0.0084 / 枠4-6 −0.0054、1SDあたりTop2確率0.5-1.1pp) ②展示ST系は枠4-6のみ ③スタ展進…
- **NG-ADJ1**(done_primary): PASS=あり。①分散成分: σ²b=0.0549・ICC=0.160・permutation p=0.0010 (1000回・seed42・場×初日z帯120層の層内置換)。モーター個体側ICC=0.048=選手差は機体差の約3倍 ②前後半再現: EB shrunkのSpearman ρ=0.752・選手クラスタb…
- **NG-PARTS-POC**(done_primary): パーサ実ページ検証PASS (9ページ・部品名正常・旧バグのR番号混入ゼロ・部品セルbr連結バグを実ページで発見し即修正)。PoC 480/480ページ完走 (sleep2.5s直列・500cap内): ①正常取得率100% (2020-2026全年度) = 過去35万ページは現存・再取得可能 (監査時の「生HTML…
- **NG-MS2**(done_primary): **PASS** — 凍結2条件 (ΔNLL point≤−0.003 かつ CI95上端<0) を両fold通過・符号反転なし。Δ=(F41+MS6)−同一窓再学習F41 (3seed・cluster bootstrap B=2000): fold1 (test 2025-07〜12, n=25,367) **ΔN…
- **NG-SOB1**(done_primary): **PASS** (凍結基準の機械判定: 宣言14検定中8本成立・うちtop1結果スケール4本≥1・n=280,783)。成立8本= top2残差: 4→5(+0.617)/2→1(+1.043側の3→1含む: 2→1 +0.546・3→1 +1.043)/4→2(−0.625)、top1結果: 4→5(+0.345…
- **NG-T3D1**(done_primary): H1 PASS: fire 41本の drift 中央値 phase1 2場全艇 0.526 [0.43,0.65] / 24場勝者 0.417 [0.39,0.45] / phase2 (先方 final 全艇 910R) T-3 0.667 [0.48,0.81]・T-3再判定 0.569 [0.36,0.75]…
- **NG-T3D2**(done_primary): 方式 A (3連単含意単勝 0.75/p3t) PASS・優位: T-3 判定 EV≥1.15 の締切価格 EV>1 survival 58% [52,66] (n_sel 200) vs naive (AI×表示単勝) 32% [29,36] (n=678)・FPR 42% vs 68%・closing price…

## 6. Failed-Do-Not-Repeat(FAIL 確定 — 同一形の再提案禁止・判定の書き換え禁止)
棄却済み(REJECT):
- **b2h_embedding**: racer ID embedding 改善ゼロ
- **composite_loss/capacity/mixture/race_no/5seed/temp_calib**: モデル改造系6件 全て誤差圏
- **f43_temp_water**: 気温水温素値 = fold間符号反転・季節の焼き直し
- **thin_layers_tide_style_gap**: 潮汐/戦型/番組ギャップ薄層 -0.0006〜0.0011 (基準0.003未達)
- **class_code**: 階級ラベル全棄却 (2026-06確定・再投入禁止)
- **explicit_interactions**: 明示積項は桐生で過学習方向

事前登録ゲート FAIL(登録ルールの機械適用・詳細は registry / EXPERIMENTS.md):
- **NG-E1**(done_primary): FAIL(凍結ルール機械適用・棄却類型=③織り込み済が主+①効果不在併記)。薄層ΔNLL fold1 −0.00055 CI95[−0.00104,−0.00001]/ fold2 −0.00064 CI95[−0.00117,−0.00008]=符号から逆(薄層はbaseを微悪化)。プラセボ(race_no単独)は…
- **NG-E23**(done_primary): FAIL(①効果不在)。選定K=24(fold1点推定で選定・判定はfold2=事前登録どおり)。薄層ΔNLL fold1 −0.000506 CI95[−0.000825,−0.000186]/ fold2 −0.000481 CI95[−0.000697,−0.000249]=薄層はbaseを微悪化・K=12/1…
- **NG-E5W**(done_primary): FAIL(①効果不在・閾値未達)。薄層ΔNLL fold1 +0.000184 CI95[−0.000622,+0.001000]/ fold2 +0.000230 CI95[−0.000267,+0.000723]=符号反転なしだが閾値0.003未達・両foldCI 0跨ぎ。プラセボ①場×月内permutation…
- **NG-I1**(done_primary): FAIL=特徴昇格見送り。薄層ΔNLL fold1アーム −0.000205 CI95[−0.000932,+0.000472](0跨ぎ)/ fold2アーム +0.001078 CI95[+0.000686,+0.001471](0非跨ぎだが閾値0.003の約1/3)。fold間符号反転。改善はattack_pro…
- **NG-N1**(done_primary): FAIL(事前登録ルール厳格適用・符号反転なし)。薄層ΔNLL fold1 +0.000531 CI95[−0.000029,+0.001123](下端僅か0跨ぎ)/ fold2 +0.001306 CI95[+0.000629,+0.002030](有意)— 閾値0.003両fold未達。一方P2完全OOSでλ_m…
- **NG-N1C**(done_primary): FAIL (①②⑤成立 / ③④不成立 → 凍結decision_ruleどおり不採用のまま原因報告)。①対象セル: P2完全OOSでgap +0.001298→+0.000166 CI95[−0.000076,+0.000419] z=+1.32=成立 ②全体NLL非劣性: 6集合すべてCI下端>−0.0005・Δ…
- **NG-PXR1**(done_primary): Step1 FAIL / Step2 FAIL (凍結基準の機械判定・n=280,783)。Step1: 攻撃チャネル6中PASS1のみ (4→5 +0.617 [+0.480,+0.751]。2→1/3→1は宣言と逆符号で有意=攻め手在席時にAIは1号艇top2を**過小**評価) — 基準≥3/6未達。別枠1→2…
- **NG-N1R**(done_primary): FAIL (①②③⑤成立・④のみ2/3で不成立→凍結decision_ruleどおり不採用。N1/N1CのFAIL不変)。①P2全窓 gap_after −0.000013 (z=−0.10・CI 0跨ぎ) = N1C固定λ (z=+1.32) から1桁改善 ②全体NLL非劣性4集合成立 ③BH族補正 (3期×11帯…
- **NG-G3**(done_primary): FAIL_STACKED — MS6の本番昇格なし (凍結2条件の機械判定)。本番相当窓 (train 2020-01..2026-07・base=本番バンドル再利用・mu/sd一致assertで窓不変証明): 生ΔNLL=−0.0146 (方向一致・副判定PASS) だが exh120併用スタックのholdout …
- **NG-EXIN1**(done_primary): FAIL_STACKED (凍結窓 holdout S n=4,530・B=2000): B−A +0.00711 [+0.00154,+0.01292] / C−A +0.00781 [+0.00230,+0.01357] / C−B +0.00070 [−0.00007,+0.00150] = RESIDUAL_…

## 7. Data Collection Status(正本 = DATA_STATUS.md・全文は下部に連結)
- 部品交換 層化バックフィル(B 案)
- T-3 締切前オッズ(national_v2)
- 締切直前〜締切後オッズ forward collector(close_window・NG-FC1)
- beforeinfo(展示・チルト・安定板・気象)
- 研究用特徴 features_v2(B2 経路)の as-of 17 列欠損 → 復旧済み
- 市場アノマリー holdout(3 テーマ)
- 部品交換 日次前向き収集
- 風コレクタ 2 本(直前風変化 U-26)
- ERA5 環境パネル
- (各行の場所・進捗・次のマイルストーンは下部 DATA_STATUS.md 全文を参照)

## 8. Open Questions(未裁定の Owner 判断)
- #1 live気象修復パッチ (P0)(推奨: 適用)
- #2 7/27劣化153件修復(推奨: 適用)
- #3 風向16方位パーサ(推奨: 適用)
- #4 openapi日次取り込みを夜間ジョブへ(推奨: 追加)
- #5 同日ソートキー修正の本番適用(推奨: 見送り (研究ビルドのみ))
- #12 強風regime Phase B (最小regimeモデル・生存16セル対象) の起票可否 — Phase A PASS (逃げ率−10pp/まくり+3.8pp/展示予言力低下が7m/s+で確定)。重要制約: K風=事後観測のため予測特徴化にはT1時点の風ソ…(推奨: T1風の可用性を先に固めてから起票 (風向パーサ適用済み日次取り込み #4 の蓄積 or bi 2026+のみで小規模検証)。焦って事後風でモデル化しない)
- #14 単勝 T-3 蓄積の強化 (national_tan の収集窓を締切 4〜2 分へ寄せる launchd 変更)(推奨: 適用 (T3D2 の将来窓・11/1 判定の母数を増やす。boatrace.jp への追加リクエストは同数で窓移動のみ))
- #15 2023-01-01〜04-24 全場欠落の再取得 (公式 LZH からの可否確認→取得)(推奨: 可否確認まで GO 推奨・取得は別途)
- #16 公開 mirror の git 履歴 / gist 版履歴に残る先方実名の扱い (force push + gist 作り直し)(推奨: Owner 判断 (危険操作))
- #17 crontab 3 行 (風コレクタ 2 + 部品日次 1)(推奨: 設置)
- #18 NG-T3D3 起票 (gap 条件付きブレンド・design_t3d3_20260910.md)(推奨: GO (事前登録→実行。新 NN なし・本番不変))
- #19 forward collector 実装・launchd 登録 (design v2 + draft + plist draft 完成)(推奨: GO (2 週間試験。3連複/2連単/2連複ページの追加有無を同時裁定))
- #20 shadow EV 判定を方式 A (3連単含意単勝) へ差し替え (daily_signal_notify.py・本番隣接)(推奨: GO (持ち越し))
- #21 研究成果の commit + research mirror push (Q-007 e の扱い)(推奨: GO)
- #22 NG-T3D4 起票 = オッズ帯条件付き λ + 判定を『確定配当ベースの実現値 CI 下端 > 1』に置く (実現値が 1 を超えなければケース3 確定・Market Gate 閉鎖)(推奨: GO (Q-022))
- #23 forward collector 試験後 (9/24) の checkpoint 確定 (D-0:30/D-0:10 存廃・3f/2tf 継続) と raw HTML gz の削除(推奨: 試験結果を見て裁定 (メタデータのみ))
- 市場アノマリー holdout 封印(captured 2026-09-01〜10-31 は閲覧禁止・2026-11-01 開封)は未決事項ではなく**遵守事項**

## 9. Decision Log(直近 10 裁定 — 正本 = DECISION_LOG.md・全文は下部に連結)
- 2026-09-10 | NG-T3D3 の設計 | **設計確定 = gap 条件付きブレンド(順序較正ではない)**・起票は Owner GO — log p' = (1−λ)log p + λ log q・λ = λ0 + λ1·z_gap・券種 × lead 別。判定 = S5 後の CR 回復 ∧ EV≥1.15 が残…
- 2026-09-10 | 市場データ可用性監査(Lane M) | 分類確定 — 5 券種とも D なし。全国の締切前「複数時点」があるのは 3連単のみ(nv2 T-8 / 先方 snapshot)。3連複・2連単・2連複の全国締切前は先方直前板 T-1(6.…
- 2026-09-10 | forward collector(締切直前〜締切後の前向き収集) | 実装可能状態(登録は Owner GO) — 7 項目再確認(負荷 +7%・1R 12 req・≈1,950 req/日・polite 1.5 s + 同一秒キュー・失敗処理・保存 2.9 KB/checkpoint・送受信…
- 2026-09-10 | 研究成果の GitHub 同期(commit + push + mirror) | **恒久 GO(shin 2026-09-10「毎回更新されるようにして go」)** — 研究サイクルの closure で `sync_all.sh` を必ず実行(再 GO 不要)。Q-007 e / Q-021 d は本裁定で CLOSED。allowlist 方…
- 2026-09-10 | Owner 研究指令 (第 2 弾)「AI と市場の意見差を較正し、本当に買えるエッジが現実的な頻度で残るか決着させる」 | GO(Owner 2026-09-10 15:20)= Q-019 次サイクル OPEN / Q-021 a・b・c GO — NG-T3D3 正式登録・実行 / Edge–Frequency Frontier + Time-to-Evidence / 知人研究 Crosswalk / forward c…
- 2026-09-10 | NG-T3D3 gap 条件付き市場ブレンド | **凍結判定 = ケース1 (3連複・2連単・2連複 = MARKET GATE CANDIDATE / 3連単 = REJECT / CORE なし)。実質 = ケース3 寄り** — λ は内点 (0.31〜0.59)。3連複・2連単・2連複はブレンドが AI・市場の両方より NLL 良化、3連単は市場と同等、単勝は AI 単独が最良。S5 hit-CR 0.…
- 2026-09-10 | forward collector (close_window) | **launchd 登録・稼働開始 (15:45 JST・Owner 指令 §9 GO)** — robots.txt Disallow 空・時計差 9 s。ページ = oddstf + odds3t (全 checkpoint) + odds3f + odds2tf (D-…
- 2026-09-10 | shadow 第 2 アーム (単勝) の EV 判定 | **方式 A (3連単含意単勝 0.75/p3t × AI ≥ 1.15) に差し替え (shadow only・本番購入ロジック不変)** — 旧判定 (乖離 ≥0.20) は列名を変えずに比較列として残す。新列 p3t/price_A/ev_A/fire_A/stake_A/payout_A/judge。8/31 dr…
- 2026-09-10 | Historical Replay Engine | 設計のみ (実装なし・T3D3 の後に最小試作 8 h・Owner GO) — 5 入力の as-of 定義・model-as-of ladder・leakage checklist 21 項目 (旧 Engine で満たされる 6 / 不足 15)・pre…
- 2026-09-10 | 知人研究 Crosswalk | 整理完了 (判定に不使用・independent reference) — 44 行照合: 一致 28 / 不一致 9 / 未検証 7。知人の生存候補 (2連複 edge002) は市場 vs 市場の歪みで AI ブレンドとは別物。gap ブレンドは知人…

## 10. User-readable Summary(人間向け解説 — FINDINGS.md ④ より抽出)
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

---


# ===== RESEARCH_STATUS.md =====

# RESEARCH_STATUS — 研究状態の正本

- 最新更新: **2026-09-10 16:10**(更新者: Claude / Owner 研究指令 第 2 弾「AI と市場の意見差を較正し、本当に買えるエッジが現実的な頻度で残るか決着させる」完走。NG-T3D3 = 凍結判定ケース1(3連複・2連単・2連複 MARKET GATE CANDIDATE・3連単 REJECT)/ 実質ケース3 寄り(hit 較正は回復・表示価格 EV は残る・確定配当ベースの実現値は全券種 <1)/ Edge–Frequency Frontier・Time-to-Evidence(頻度は制約でない)/ 知人 Crosswalk 44 行 / forward collector 登録・稼働 / shadow 方式 A 稼働 / Historical Replay 設計。人間向け 5 分表示 = research/OWNER_VIEW.md。次 = NG-T3D4(オッズ帯条件付き λ + 実現値 CI gate)の Owner GO)
- 前回更新: 2026-09-10 11:50(Ticket-Space 完走・P0 復旧・T3D3 設計)
- 本ファイルは Canonical Research State の入口。機械可読版 = `research_state.json`。人間向け表示 = 研究コンソール(Artifact 494f0be1… — 本ファイル群から生成される view であり正本ではない)

## 現在の研究フェーズ

**第1波(W1)の登録実験を全消化(2026-09-04)**。done 6本 = NG-E10(両ゲートPASS)+ **NG-I1 / NG-N1 / NG-E1 / NG-E5W / NG-E23(5本とも主ゲートFAIL・全て事前登録ルールの機械適用)**。残 = NG-E19SG(常時・締切前オッズ蓄積待ち)+ NG-E8SWAP(filed)。全実験で「事前登録→操作的定義の凍結→機械判定」を完走、判定ルールの事後変更ゼロ。**Owner 裁定受領 (2026-09-04): #6 GO → NG-N1C (Calibration-specific Gate) 事前登録済 / #7 GO → NG-E5NR (Nonlinear Environmental Regime) 事前登録済 / #8 DEFER (格 = 現象 SUPPORTED・入力側再学習は保留)**。W2 方針 = 後付け薄層の枯渇を受け「真の新情報 / regime / Calibration / Market / Current State 推定」へ重心移動 (最重要候補 = Motor Current State / Maintenance 系)。W2 Candidate Audit 完了 (2026-09-04・beforeinfo 356,476 ファイル実測)。**決定的発見: 部品交換データは 6.5 年間パーサ取り違えで実質未収集だった**。**W2 正式 GO (Owner 2026-09-05)**: 実行順確定 = 並行【①まくり筋較正最終検証 (NG-N1C) ②部品交換修理+前向き収集+層化バックフィル PoC】→ ③現在モーター状態 PoC → ④強風 regime ⑤調整能力。全バックフィルは未承認 (PoC 後に再判断)。並行で「展開圧力×対応力 (Generalized Pressure×Resistance)」の設計+データ監査。新研究思想 8 テーマ (シナリオ分散買い・known-but-underweighted 市場情報 等) を仮説として正式保存。

## Current Best Model / Baseline

- **Best = Baseline = `b2f41_prod2026_prod3`**(現状同一。v2.1 新アーキは未着工のため「最新=最良」)
- 実体: B2構造化着順NN(41特徴・6艇self-attention・120通り直接softmax・3seed平均)+ exh120展示補正層(θ9本)+ 市場ブレンド(w=0.85・推論後段/表示用)
- 主要指標: 全国 fold2 NLL 3.7565 / Hit@1 10.20% / 単勝Acc 57.46%。市場(確定オッズde-vig)との残距離 NLL +0.06〜0.07

## 現在実行中の Experiment

**なし(2026-09-10 16:10・NG-T3D3 完了・自走 = 部品バックフィル + forward collector 試験運用 + shadow 方式 A)**。以下は 2026-09-04 時点の記録: **なし — 第1波5本(NG-I1 / NG-N1 / NG-E1 / NG-E5W / NG-E23)は 2026-09-04 に並列レーンで実行し全て done_primary**。5本とも主ゲート(薄層ΔNLL≥0.003)FAIL。ただし収穫が3つ: ①**N1 はまくり筋の較正歪みを1パラメータ(λ=+0.228)でほぼ完全回収**(完全OOSで相対見落とし +26.3%→+2.7%・副作用ゼロ。閾値0.003が単一セル補正の理論上限より高く原理的に到達不能だった=Owner判断 #6)②E1 で「格は実在するが B2 は既に織り込み済み」が確定・グレード表(E19SG用)を副産物化 ③E5W で強風 7m/s+ の符号逆転(線形仮定の破綻)を発見。詳細 = `lane-reports/{i1_proxy,n1_reweight,e1_stage,e5w_wind,e23_utility}_20260904.md` + registry 各 done_primary 行。残り = registered 1本(NG-E19SG・常時)+ filed 1本(NG-E8SWAP)

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

`NEXT_ACTIONS.md` 参照。1行版(2026-09-10 16:10): **NG-T3D4(オッズ帯条件付き λ + 確定配当ベースの実現値 CI を gate に)の起票 = Owner GO → 1 を超えなければケース3 確定 = Market Gate を閉じて 11/1 holdout 開封と forward collector の締切直前価格を待つ**(常時: forward collector 試験 9/11〜9/24 メタデータ評価・部品バックフィル自走・NG-E19SG 蓄積・holdout 封印)。

## 更新ルール(2026-09-04 Owner 指示で制定)

コード・実験・研究状態を更新したら、**Artifact だけでなく /research/ 配下の本ファイル群と research_state.json を必ず同期する**。他のAI・人間はまずここを読む。



# ===== NEXT_ACTIONS.md =====

# NEXT_ACTIONS — 現在優先すべき研究(3〜5件だけ)

最新更新: 2026-09-10 16:10(**Owner 指令 第 2 弾「AI と市場の意見差を較正し、本当に買えるエッジが現実的な頻度で残るか決着させる」完走: NG-T3D3 = 凍結判定ケース1(3連複・2連単・2連複 = MARKET GATE CANDIDATE・3連単 = REJECT・CORE なし)/ 実質ケース3 寄り(hit 較正は回復・表示価格の EV は残る・確定配当ベースの実現値は全券種 <1)/ Frontier・Time-to-Evidence(頻度は制約でない)/ 知人 Crosswalk / forward collector 稼働 / shadow 方式 A 稼働 / Replay 設計**。Owner 表示 = research/OWNER_VIEW.md)。実行中の自走 = 部品バックフィル(PID 12667・ETA 9/16)+ forward collector 試験運用(NG-FC1・9/11〜9/24)+ shadow 方式 A(nightly 23:30)
**production 変更ゼロ(b2f41 不変)。11/1 holdout ルール不変(forward collector の値も 11/1 まで見ない)。**

## 現在の優先順位(Owner 指令 第 2 弾 完走後)

1. **NG-T3D4 起票(Owner GO 事項・次の 1 手)**: 残った過信は「オッズ帯」に偏在する(hit-CR ≈1 でも実現 ÷ 締切期待 = 0.5〜0.8・FINDINGS P9)。λ をオッズ帯(favorite-longshot 軸)条件付きにした最小モデル(パラメータ +1〜2・新 NN なし)を事前登録し、**判定を「確定配当ベースの実現値 CI 下端 > 1」(実際に受け取る額)に置く**。PASS した券種だけ Market Gate へ。全滅なら「現 AI では実価格で市場に勝てていない(ケース3)」を確定し、Market Gate を閉じて 11/1 開封と forward collector の締切直前価格を待つ。同時に知人地雷②「残る組数 = 剪定 artifact」の同数ランダム剪定比較を入れる
2. **forward collector 試験(自律・メタデータのみ)**: 9/11〜9/24 の 14 日で D-0:30 / D-0:10 の存廃(lead_sec_recv の誤差 p95 ≤ 5 s・1 分刻み更新との関係)/ odds3f・odds2tf の parse 成功率 / 失敗処理の実地 / **応答 8〜10 秒/ページの原因(IPv6 フォールバック疑い = 仮説)** を確認 → checkpoint 確定は Owner。オッズ値は 11/1 まで見ない
3. **自律(読み取り・設計のみ)**: 部品バックフィル完走(9/16 目安)後の Maintenance 最小イベントスタディ設計 / 11/1 holdout 開封手順の事前整理(凍結ルール一覧・開封 script の read-only 化・T3D3 λ の適用有無を開封前に固定)/ Historical Replay 最小試作(3連単 × T-1 × 2026-08・8 h)は T3D4 の後・Owner GO
4. P3(設計済み・実行は Owner GO): SOB1 将来窓再現 / 小さい SC2(優先度低: 過信の原因ではない)。H-A〜H-D は BACKLOG ONLY
5. 禁止維持: 大型 Scenario Generator / GAT / Race Simulator / 券種専用 NN・券種専用特徴・巨大 calibration network / 拡連複・複勝 / 展示入力側化の再提案 / 部品バックフィルの停止・再起動・35 万拡張 / holdout 9/1〜10/31 閲覧 / **test 窓を見てからの τ・候補・窓の変更(T3D3 は凍結どおり・addendum は別掲)**
6. shin 手作業待ち: crontab 3 行(部品日次・風コレクタ)/ 2023-01〜04 再取得可否 / 公開履歴の先方実名(Q-007)

## 完了(2026-09-10 午後・Owner 指令 第 2 弾)

NG-T3D3(λ 内点 0.31〜0.59・3連複/2連単/2連複はブレンドが AI・市場の両方より NLL 良化・S5 hit-CR 0.52〜0.73 → 0.62〜0.905・2連単 PASS・EV≥1.15 は 0.6〜1.5 組/R・年 2〜8 万 BET・実現値は全券種 0.64〜0.85・2連複 T-3 のみ ≥1 で NEEDS MORE DATA)/ Edge–Frequency Frontier(τ 6 × rule 3 × 券種 × anchor 全セル)/ Time-to-Evidence(σ 10〜33・検出 0.2〜0.6 年・頻度は制約でない)/ 凍結後 addendum(締切価格 EV vs 実現 = 高オッズ側の金額重み過信が残留)/ 知人 Crosswalk 44 行(一致 28・不一致 9・未検証 7・地雷 10)/ forward collector 5 券種で登録・稼働(NG-FC1)/ shadow 第 2 アーム 方式 A 稼働 / Historical Replay 設計(leakage 21 項目・試作 8 h)。lane-reports/t3d3_market_shrinkage_20260910.md

## 完了(2026-09-10 午前・Owner 指令「Ticket-Space」)

P0 features_v2 復旧 + G3/EXIN1 clean 再評価(判定不変)/ NG-TS1 = ケース D(順序ではなく選択そのもの・真値は AI と市場の間)/ 市場可用性監査 / T3D3 設計 / forward collector 設計 v2。

## 完了(2026-09-10 早朝・Owner 指令 2026-09-09)

NG-T3D2(A PASS 58% vs naive 32%)/ NG-EXIN1(FAIL_STACKED)/ P3 SC2・SOB1 設計 / backlog U-34〜U-37。

## 完了(2026-09-09)

バンドル突合ゲート G1-G5(NG-GIFTG 5/5 PASS)/ T-3 ドリフト追試(NG-T3D1 H1・H3 PASS)/ 部品バックフィル再開 / 公開 mirror の実名匿名化。**以下の旧リスト(9/5〜9/6)は歴史記録として残すが、優先順位は上の節が正**。

## 旧 Owner 判断リストとの対応(2026-09-06 完走時点)

#1 G3 = **完走 FAIL_STACKED**(MS6 昇格なし・clean 再評価でも不変)/ #5 R1 気象 = **汚染確定・解決**(恒久規律 R1 除外)/ #6 風 = コレクタ実装検証済(crontab 待ち)/ #4 ADJMS1 = MS_NET_ZERO を受けて設計見直し推奨 / #2・#3・#7・#8 = 未裁定のまま

## 常時 / 保存のみ

- 部品バックフィル自走中(進捗= `cat ~/kyotei-ai/artifacts/research/nextgen/parts_bf/parts_bf_state.json`)。完了後に Maintenance 仮説→全量A案の再判断
- forward collector 稼働中(健全性 = `tail data/odds_snapshots/close_window/<YYYYMMDD>/_health.jsonl`・停止 = `launchctl bootout gui/$(id -u)/com.kyotei-ai.collect-close-window`・一時停止 = `touch data/odds_snapshots/close_window/STOP`)
- NG-E19SG 蓄積継続 / 市場アノマリー holdout 封印(閲覧 2026-11-01 以降)
- 保存のみ: シナリオ Generator 大型 / GAT(2重の否定で棚上げ)/ Race Simulator / Portfolio Optimizer 本番化 / 穴シナリオ Gate 数値化



# ===== DECISION_LOG.md =====

# DECISION_LOG — GO/NO-GO 裁定台帳(正本)

- 制定: 2026-09-06(Owner 指令 §16「Decision Log 常設」を受け、過去裁定を遡って構造化)
- 位置づけ: Canonical Research State の一部。**追記のみ(既存行の書き換え禁止・FAIL を成功扱いに変更しない)**
- 収載基準: ①Owner(shin)の GO / NO-GO / DEFER 裁定 ②事前登録ルールの機械適用による実験判定(PASS / FAIL)③本番・データ収集に関わる不可逆な決定。1 行 = 1 裁定
- 出典の正本: `artifacts/research/experiment_registry.jsonl` / `research_state.json`(pending_owner_decisions・w2_directives)/ `RESEARCH_STATUS.md` / `docs/ARCHITECTURE_FREEZE_v2.1.md` Changelog / `lane-reports/nextgen_audit_20260903.md`。矛盾したら各出典が正
- 凡例: **GO**=着手承認 / **PASS・FAIL**=事前登録ゲートの機械判定 / **ADOPT**=本番採用 / **DEFER**=保留 / **REJECT**=棄却(同一形再提案禁止)

| 日付 | 対象 | 裁定 | 何を・なぜ(1行) | 出典 |
|---|---|---|---|---|
| 2026-07-23 | EXP-001(オッズ執行パネル) | 採用(知見) | 3連単30分前判定は median EV 0.916=楽観バイアス確定 → conservative EV 移行を勧告 | registry EXP-001 |
| 2026-07-23 | EXP-004(購入領域の局所較正) | 探索採用 | 購入領域は全帯で約2倍過信。α fit は in-sample=探索扱い、walk-forward 確認を EXP-002 へ統合 | registry EXP-004 |
| 2026-07-23 | EXP-002(nested threshold 検証) | R023 採用 / RCAL 棄却 | R023 が 5/5 期間で安定 → ライブ凍結候補。ただし cluster CI 下限 0.943<1.0=収益証明未達を明記。RCAL(EXP-004 選別)は全敗で棄却 | registry EXP-002 |
| 2026-08-06 | 市場アノマリー3テーマ | 事前登録+holdout 封印 | 登録書以後変更禁止。holdout 2026-09-01〜10-31 は集計・閲覧禁止、開封 2026-11-01 以降 | artifacts/research/mkt/preregistration_20260806.md |
| 2026-08-06 | f41_skew_fix(学習気象の beforeinfo 統一) | ADOPT(本番切替) | train/serve skew 是正。2026-08-04 GATE PASS → 08-06 本番切替 = 現行バンドル `b2f41_prod2026_prod3` | EXPERIMENTS.md §1-8 |
| 2026-09-03 | 監査後の意思決定 10 点 | 一括 GO | ①W1 着手 ②live 気象=案A(openapi)③beforeinfo バックフィル再開 ④風向アイコン前向き蓄積 ⑤コース方位人手較正 ⑥ERA5 取得 ⑦日程・交換月等の小粒手作業 ⑧まくり筋を E10 主仮説として事前登録 ⑨E8SWAP 起票のみ ⑩同日ソートキー修正 — 23項目監査の推奨案を shin が承認 | lane-reports/nextgen_audit_20260903.md 意思決定ポイント |
| 2026-09-03 | W1 第1波 6 本(NG-E10/E1/E23/E5W/E19SG/E8SWAP) | 事前登録 | 判定ルール・閾値を結果計算前に凍結(git a759dac)。以後の事後変更ゼロ | registry 各 registered 行 |
| 2026-09-04 | ARCHITECTURE v2.1 | freeze 制定 | 「6艇の能力ランキング」→「Context-Aware Multi-Agent Dynamic System」へ。予測/市場評価/購入判断の3層分離を明文化。破壊ゼロ・現 B2 は Baseline 保持 | docs/ARCHITECTURE_FREEZE_v2.1.md Changelog |
| 2026-09-04 | 適用パッケージ(監査残 #1-#5) | #1-#4 適用 / #5 見送り | ①live 気象修復パッチ ②7/27 劣化153件修復 ③風向16方位パーサ ④openapi 日次取り込み=適用・追加 / ⑤同日ソートキー修正は本番見送り(研究ビルドのみ) | research_state.json pending #1-5 / RESEARCH_STATUS(P0 パッチ適用済 2026-09-04) |
| 2026-09-04 | NG-I1 / NG-N1 | 事前登録(shin GO「全部go」) | E10 両ゲート PASS を受けた追撃 2 本。操作的定義の凍結 JSON を結果計算前に作成 | registry NG-I1 / NG-N1 registered 行 |
| 2026-09-04 | NG-E10(externality+まくり筋) | **PASS(両ゲート)** | 分散成分 p=0.001 / まくり筋 OOS 1年 gap +0.001298・z=10.2・相対+26.3%見落とし確定。帰結: N1 GO・I-1 前倒し・GAT 起票不支持 | registry NG-E10 done_primary |
| 2026-09-04 | NG-I1(as-of 行動 proxy 特徴) | **FAIL** | fold 間符号反転・閾値 0.003 未達 → 特徴昇格見送り。i1_features.parquet は資産保存 | registry NG-I1 done_primary |
| 2026-09-04 | NG-N1(まくり筋薄層) | **FAIL(較正回収は実証)** | 主ゲート未達。ただし λ=+0.228 で gap +26.3%→+2.7%・副作用ゼロを完全 OOS 実証 → 再ゲート可否は Owner #6 へ | registry NG-N1 done_primary |
| 2026-09-04 | NG-E1(レース格薄層) | **FAIL(③織り込み済)** | B2 は setsu_day/pts 系で格由来シフトを学習済み。現象(ST 変化 24/24 場)の否定ではない → 入力側追加は Owner #8 へ | registry NG-E1 done_primary |
| 2026-09-04 | NG-E5W(風コース成分・線形) | **FAIL(①効果不在)** | 閾値の 1/15・CI 0 跨ぎ。副産物: 風速 7m/s+ で符号逆転=線形仮定の破綻 → 非線形方向は Owner #7 へ | registry NG-E5W done_primary |
| 2026-09-04 | NG-E23(勝負駆け utility) | **FAIL(①効果不在)** | 二値(null 済)→連続の 2 形式で null 確定 = 同路線の再々提案は非推奨 | registry NG-E23 done_primary |
| 2026-09-04 | Owner 判断 #6(N1 較正層の扱い) | GO | Calibration-specific Gate を NG-N1C として新規事前登録(閾値は理論 SE から事前設定)。旧 N1 の FAIL 判定は不変 | research_state.json pending #6 |
| 2026-09-04 | Owner 判断 #7(風の再挑戦方向) | GO | 線形 2 パラメータ形は FAIL 固定。NG-E5NR(強風 regime の最小統計 PoC)を事前登録。巨大 interaction モデル一括実装は禁止 | research_state.json pending #7 |
| 2026-09-04 | Owner 判断 #8(格特徴の入力側追加+再学習) | DEFER | 現象は SUPPORTED 維持。再学習コスト大・モデル改造 12 連敗の実験史を踏まえ、他の新規入力とまとめる時期に再検討 | research_state.json pending #8 |
| 2026-09-05 | W2 実行順 | 正式 GO | 並行【①NG-N1C ②部品パーサ修理+前向き+層化 PoC】→③Motor Current State PoC→④E5NR→⑤Adjustment Skill。35万ページ全バックフィルは未承認のまま。P×R は設計+データ監査まで。新研究思想 8 テーマは仮説として保存(U-18〜U-25) | research_state.json w2_directives_owner_20260905 |
| 2026-09-05 | NG-N1C(まくり筋 Calibration Gate) | **FAIL(①②⑤成立・③④不成立)** | 主因= λ の時間非定常+再正規化の巻き添え。改善効果自体は全窓で正。rolling λ は新規事前登録が必要な別実験として Owner #9 へ | registry NG-N1C done_primary |
| 2026-09-05 | NG-MS1(現在モーター状態 存在確認 PoC) | **PASS** | 展示タイム系推移が B2 残差を予測(全 3 枠帯 BH 通過・当日 z 統制でも独立情報)。W1 以降初のポジティブ → 最小特徴化ゲートへ | registry NG-MS1 done_primary |
| 2026-09-05 | NG-E5NR Phase A(強風 regime) | **PASS(16/18 セル生存)** | 逃げ率 −10pp(7m/s+)・まくり率+・展示予言力低下が単調再現。Phase B は生存セル限定で別途凍結+Owner GO 待ち(pending #12) | registry NG-E5NR done_phaseA |
| 2026-09-05 | NG-ADJ1(選手の調整能力 存在確認 PoC) | **PASS** | ICC=0.160・permutation p=0.001・前後半 ρ=0.752。選手差は機体差の約 3 倍。特徴化は Owner #11 の再学習ゲートと合流 | registry NG-ADJ1 done_primary |
| 2026-09-05 | NG-PARTS-POC(部品パーサ修理+層化 PoC) | 完了(取得体制確立) | 480/480 ページ成功率 100%・過去 35 万ページは現存=再取得可能。A 案(全量 48 日)/ B 案(層化 5 万・7 日)を提示 → Owner #13 へ | registry NG-PARTS-POC done_primary |
| 2026-09-06 | Owner 判断 #11 = P1(NG-MS2) | GO(最優先) | 現在モーター状態の最小特徴化+OOS 実モデルゲート。巨大 Motor Expert 禁止・K 由来展示列の誤使用禁止 | research_state.json pending #11 |
| 2026-09-06 | Owner 判断 #10 = P2(NG-PXR1) | GO | 展開圧力×対応力 Step1-2 ミニ PoC。固有選手ルール禁止・受益艇まで 3 段追跡 | research_state.json pending #10 |
| 2026-09-06 | Owner 判断 #13 = P3(部品バックフィル形態) | B 案 GO | 層化 5 万ページ(≈7 日・節単位)。Maintenance 仮説の増分確認後のみ全量 A 案(48 日)を再判断。日次 crontab は shin 手動のまま | research_state.json pending #13 |
| 2026-09-06 | Owner 判断 #9(rolling λ) | GO(side・優先度 P1 未満) | NG-N1R として事前登録。興味の核=まくり筋歪みそのものの時間変化。旧 N1/N1C の FAIL は不変 | research_state.json pending #9 |
| 2026-09-06 | 部品交換 層化バックフィル B 案 | 起動 | 49,968 ページ・PID 50737・polite sleep≥2.5s・日次 8,000 上限・ETA ≈7 日。全量 35 万は未承認のまま | lane-reports/parts_backfill_start_20260906.md |
| 2026-09-06 | NG-MS2(現在モーター状態 特徴ゲート) | **PASS** | ΔNLL −0.0136/−0.0160(両 fold CI クリーン・12 ヶ月連続負)= extra3 以来の入力側特徴勝利・exh120 級。本番昇格は G3(本番相当窓再検証)+Owner GO が別途必要 | registry NG-MS2 done_primary |
| 2026-09-06 | NG-PXR1(展開圧力×対応力 Step1-2) | **FAIL** | B 側個人差は検出不能(p=0.992)・A 側 slope は宣言と逆符号あり → **GAT・pairwise は棚上げ確定(2 重の否定)**。副産物=攻め手在席時の条件付き較正歪み候補 | registry NG-PXR1 done_primary |
| 2026-09-06 | NG-N1R(rolling/as-of λ) | **FAIL(④のみ不成立)** | 不採用のまま。主成果= λ 軌跡 +0.172→+0.281(約 1.6 倍上昇)=歪みの時間変化を確定記述。縮小局面の過補正が本番接続時の最重要リスク | registry NG-N1R done_primary |
| 2026-09-06 | NG-RC1(読めるレース診断) | done_exploratory | 「読めるレース」は実在しレース前に entropy/自信で識別可能(上位 10% で 3 点 42%/6 点 60.8%)。読める≠儲かる(オッズ未評価)。運用化は事前固定閾値+複数窓が次段階 | registry NG-RC1 done_exploratory |
| 2026-09-06 | W3 方向の Owner 指令(vision+P1-P5+side) | 指令受領 | 「読めるレースを識別し、価値のある世界線だけを少数点で買う AI」。大型実装 5 種(Scenario Generator 大型/GAT/Race Simulator/Environment Expert/Portfolio Optimizer 本番化)は研究設計・最小 PoC まで | research_state.json w2_directives_owner_20260906 |
| 2026-09-06 | NG-SC1 / NG-RC2 / NG-SOB1 / NG-WPOC1 | 事前登録 | Owner 指令(§4-6 ほか)を受けた次段 4 本。SC1=Scenario 分解診断 / RC2=Compressibility Score 試作 / SOB1=二次受益艇の正式 as-of 検定 / WPOC1=ΔW×展示予言力(蓄積不要) | registry 各 registered 行 |
| 2026-09-06 | NG-SC1(Scenario 分解診断) | done_exploratory | 分解は「説明」として成立(同一3連単の多起源を強く支持)。ただし P(S) の事前予測が律速(AUC≤0.57 では不足)・Meaningful Tail はこの粒度で不在 | registry NG-SC1 done_exploratory |
| 2026-09-06 | NG-RC2(Compressibility Score v1) | **判定確定(v1=C2_top6mass)** | 単独指標が学習型合成と同着 → 凍結 tie_break で単純側採用。用途は確実性メーター(選別・点数圧縮)でありエッジ検出器ではない。読める≒儲かるは No(T-3 オッズ・2 ヶ月窓) | registry NG-RC2 done_primary |
| 2026-09-06 | NG-SOB1(二次受益艇 as-of 検定) | **PASS(留保付き)** | 宣言 14 検定中 8 本成立・スケール反転仮説を初の正式検定で確認。ただし宣言符号は PXR1 記述由来 in-sample → 将来窓での再確認まで仮説昇格に使わない | registry NG-SOB1 done_primary |

## 未裁定(open)— 裁定が出たら上表へ追記する

- **#12 強風 regime Phase B の起票可否**: 推奨=T1 時点の風ソース可用性を先に固めてから起票(K 風=事後観測のため)。焦って事後風でモデル化しない
- **#1〜#5 のうち残作業の確認**: #5 同日ソートキー修正は「見送り(研究ビルドのみ)」の裁定で確定済みだが、#2 7/27 劣化 153 件修復の完了確認は未記録
- G3(NG-MS2 の本番相当窓再検証)の起票 = NEXT_ACTIONS.md Owner 判断リスト 1(AI 推奨=最優先)
- T-3 ドリフト追試 / バンドル突合ゲート G1-G5 / NG-ADJMS1 起票 ほか = NEXT_ACTIONS.md Owner 判断リスト 2〜9
| 2026-09-06 | NG-MS3 | 判定 MS_NET_ZERO | 当日展示z併用下でMS6純増分なし (Δ(exms−ex)=+0.0023 CI[+0.0001,+0.0045])・placebo健全 | 機械判定 (凍結プラン) |
| 2026-09-06 | NG-G3 | 判定 FAIL_STACKED → MS6本番昇格なし | stacked Δ=+0.0058 CI[+0.0002,+0.0112] (凍結2条件)。生−0.0146は方向一致。b2f41不変 | 機械判定 (凍結プラン) |
| 2026-09-09 | 知り合いバンドル 突合ゲート G1-G5(NG-GIFTG) | 判定 PASS(5/5) | 構造化データ・締切前時系列ともうちと同値(G3 は先方 7/23〜24 の 3連単回転バグ補正が条件)。「突合前」ラベル解除。モデル入力への採用は別途ゲート | 機械判定 / gift_gates_ga_20260909 / gift_gate_g3_20260909 |
| 2026-09-09 | 部品バックフィル 再開 | GO(shin「推奨でまとめて」2026-09-09) | 9/6 15:09 IPv4 断で自動停止(3,543p)→ 9/9 22:15 PID 12667 で続きから再開 | parts_bf_state.json |
| 2026-09-09 | NG-T3D1 T-3 ドリフト追試 | 判定 H1 PASS / H2 INCONCLUSIVE / H3 PASS / H4 不支持 | fire 単勝の drift 中央値 0.47〜0.67(先方 0.446 は CI 内)・見かけ EV 2.83 vs 実現 0.82 → 選択時オッズは最終まで持たない。EV 判定の実効化(NG-T3D2)を Owner 判断へ | 機械判定(凍結 JSON)/ gift_t3_drift_phase1/phase2_20260909 |
| 2026-09-09 | 公開 mirror の先方実名 | 匿名化(shin 裁定 2026-09-09「実名なし」) | research_state.json のバンドル説明 1 箇所を「知人(競艇AI研究者)」に置換。git 履歴・gist 版履歴の削除は shin 判断 | research_state.json / gift_investigation_20260909 §6 |
| 2026-09-09 | Owner 研究指令「予測できる→実際に買える」 | GO(Owner 2026-09-09) | P1 NG-T3D2(Executable EV: 含意単勝 A / drift 補正 B / late execution C)・P2 NG-EXIN1(展示入力側化・B2 固定)を事前登録して実行。P3 SC2 / SOB1 将来窓は設計のみ。H-A〜H-D は BACKLOG ONLY。大型 Scenario Generator 禁止維持・Readability は利益シグナルにしない・部品バックフィルは停止/再起動/35万拡張しない | Owner 指令本文(research/OWNER_DIRECTIVE_20260909.md)|
| 2026-09-09 | 市場 holdout 2026-09-01〜10-31 | 封印維持(再確認) | 集計・グラフ・fire 数確認・閾値調整・参考閲覧すべて禁止。T3D2 開発窓は 2026-08-31 以前のみ。11/1 に凍結ルールをそのまま適用 | Owner 指令 §10 |
| 2026-09-10 | P3 設計(SC2 小型較正ゲート / SOB1 将来窓再現)+ Backlog U-34〜U-37(H-A〜H-D) | 設計完了・BACKLOG 登録(実験なし) | SC2 = S 3 群(IN/ATT/NEU)×温度 3 パラメータ・oracle 上限診断先行・primary = S 条件付き ΔNLL。SOB1 = 2026-07〜08 未接触窓で成立 8 本の族判定・市場側は 11/1 開封後。H-A 起票条件 = SOB1 REPRODUCED ∧ SC2 PASS | designs/design_sc2_20260909 / design_sob1_future_20260909 / backlog_hypotheses_20260909 |
| 2026-09-10 | NG-T3D2 Executable EV | 判定 A PASS(優位)/ B FAIL / C FAIL(naive より優位)| T-3 表示単勝で EV≥1.15 と判定 → 締切でも EV>1 は 32% [29,36]。3連単含意単勝 (0.75/p3t) で 58% [52,66]・選択 678→200。見かけ EV が高いほど潰れる (ρ −0.69)。3連単は価格が持つ (96%) が realized 0.51 = 選択後較正が次課題。shadow 判定の A 差し替え・forward collector は Owner 判断 | 機械判定(t3d2_frozen.json)/ t3d2_executable_ev_20260909 |
| 2026-09-10 | NG-EXIN1 当日展示の入力側化 | 判定 FAIL_STACKED → 本番不変 | B−A +0.0071 [+0.0015,+0.0129]・C−B ≈0 (RESIDUAL_ZERO)・clean 窓で差なし・展開診断 NOT_ABSORBED。当日展示は exh120 で取り切っている (MS3/G3/EXIN1 一致)。展示の主戦線は閉じる。GAT 再起票根拠なし | 機械判定(exin1_frozen.json)/ exin1_results_20260909 |
| 2026-09-10 | 研究基盤: features_v2 as-of 17 列の 2026-07-22 以降欠損 | 復旧を研究基盤 P0 に(自律・読み取り調査から) | G3 の untouched サブ窓・EXIN1 holdout の 1/3 が劣化窓。live 単勝シグナル経路は L1 確認で無傷 (NaN 0.2%)。原因特定→復旧→G3/EXIN1 の clean 再評価は復旧後 | exin1_addendum2_cleanwindow.json |
| 2026-09-10 | 研究基盤 P0: features_v2 as-of 17 列欠損 | **原因特定・復旧完了 (leakage-safe)** | 原因 = 08-03 の build が 07-21 で止まった features_extra3_structured を left-join (計算式・取得の問題ではない)。復旧 = 同一 builder の rc2 延長 extras + beforeinfo 再スキャン、学習窓 (≤07-21) はバイト同一・復元窓 as-of 独立再計算 300/300 一致。旧ファイルは .bak 保全。09-01 以降は封印のため未収載 | lane-reports/features_v2_gap_20260910.md / artifacts/research/v2/features_v2_restore_20260910.json |
| 2026-09-10 | NG-G3 / NG-EXIN1 clean 窓再評価 (復元特徴・同一バンドル・同一 race set 4,681R・同一凍結条件) | **判定不変 (両方 FAIL_STACKED)** → 展示入力研究は完全に閉じる | G3 stacked +0.0058 → +0.0025 [−0.0022,+0.0074] / EXIN1 B−A +0.0071 → +0.0001 [−0.0047,+0.0046]・C−B RESIDUAL_ZERO・NOT_ABSORBED。劣化窓のバイアス (入力側に不利) は消えたが入力側 = 後段補正と同精度。判定条件は変更していない。production 不変 | artifacts/research/nextgen/fv2_restore/reeval/clean_reeval_summary.json |
| 2026-09-10 | Owner 研究指令「Ticket-Space Calibration Decomposition」 | GO(Owner 2026-09-10) | P0 features_v2 復旧 → NG-TS1(4 券種射影・overall / selection-conditioned / chain / 市場可用性 / 市場診断)→ T3D3・SC2 の次設計 → forward collector 実装可能状態 → 正本更新。新 NN・再学習・拡連複/複勝・券種専用 NN は禁止 | research/OWNER_DIRECTIVE_20260910.md |
| 2026-09-10 | NG-TS1 Ticket-Space Calibration Decomposition | **判定 ケース D(順序ではなく選択そのもの)** | AI-only 選択は 4 券種すべて較正(CR 0.99〜1.01)。EV≥1.15 選択は 4 券種すべて過信(T-1: 0.61 / 0.73 / 0.74 / 0.76)。chain 主因 = 顔ぶれ段(0.72〜0.76)、順序段 0.85〜0.99。真値は AI と市場の間(p−q 五分位で単調)。実現値 全券種 <1(診断)。ケース A/B/C/E 不成立。凍結後の基準変更なし(T-3cp は補助 anchor) | 機械判定(ts1_frozen.json)/ ticket_space_20260910 |
| 2026-09-10 | NG-T3D3 の設計 | **設計確定 = gap 条件付きブレンド(順序較正ではない)**・起票は Owner GO | log p' = (1−λ)log p + λ log q・λ = λ0 + λ1·z_gap・券種 × lead 別。判定 = S5 後の CR 回復 ∧ EV≥1.15 が残る ∧ NLL 非劣化。**SC2 とは統合しない**(NG-TS1 で順序は原因でないと判明・SC2 は別課題として backlog 維持・優先度低下) | designs/design_t3d3_20260910.md |
| 2026-09-10 | 市場データ可用性監査(Lane M) | 分類確定 | 5 券種とも D なし。全国の締切前「複数時点」があるのは 3連単のみ(nv2 T-8 / 先方 snapshot)。3連複・2連単・2連複の全国締切前は先方直前板 T-1(6.6k R)と先方 checkpoint(7/25〜8/1・0.7k R)のみ = 自前収集なし。うちの final は住之江のみ。補間・推定はしない | artifacts/research/nextgen/ts/panels/market_availability_audit.md |
| 2026-09-10 | forward collector(締切直前〜締切後の前向き収集) | 実装可能状態(登録は Owner GO) | 7 項目再確認(負荷 +7%・1R 12 req・≈1,950 req/日・polite 1.5 s + 同一秒キュー・失敗処理・保存 2.9 KB/checkpoint・送受信+ページ内更新時刻の 3 時刻保存・重複マトリクス)。boatrace.jp の robots/規約はローカル未記載 = 未確認(GO 後に取得)。2 週間試験で D−0:30/0:10 の存廃判定 | t3d2/forward_collector_design_v2.md / collect_close_window_draft.py / cron/drafts |
| 2026-09-10 | 研究成果の GitHub 同期(commit + push + mirror) | **恒久 GO(shin 2026-09-10「毎回更新されるようにして go」)** | 研究サイクルの closure で `sync_all.sh` を必ず実行(再 GO 不要)。Q-007 e / Q-021 d は本裁定で CLOSED。allowlist 方式・secret ガード付き | CLAUDE.md §19 / scripts/research/nextgen/sync_all.sh |
| 2026-09-10 | Owner 研究指令 (第 2 弾)「AI と市場の意見差を較正し、本当に買えるエッジが現実的な頻度で残るか決着させる」 | GO(Owner 2026-09-10 15:20)= Q-019 次サイクル OPEN / Q-021 a・b・c GO | NG-T3D3 正式登録・実行 / Edge–Frequency Frontier + Time-to-Evidence / 知人研究 Crosswalk / forward collector 登録 (5 券種) / shadow 方式 A / Historical Replay 設計。新 NN 禁止・production 不変・holdout 封印・既存 FAIL の判定条件不変 | research/OWNER_DIRECTIVE_20260910b.md |
| 2026-09-10 | NG-T3D3 gap 条件付き市場ブレンド | **凍結判定 = ケース1 (3連複・2連単・2連複 = MARKET GATE CANDIDATE / 3連単 = REJECT / CORE なし)。実質 = ケース3 寄り** | λ は内点 (0.31〜0.59)。3連複・2連単・2連複はブレンドが AI・市場の両方より NLL 良化、3連単は市場と同等、単勝は AI 単独が最良。S5 hit-CR 0.52〜0.73 → 0.62〜0.905 (2連単 CALIBRATED = PASS)。表示価格 EV≥1.15 は 0.6〜1.5 組/R 残り年 2〜8 万 BET (頻度は制約でない)。**確定配当ベースの実現値は全券種 <1 (0.64〜0.85)** = 締切価格 8〜15% 減 + 高オッズ側の金額重み過信 (実現/締切期待 0.5〜0.8)。凍結 gate に実現値 CI を入れていなかった (設計漏れ・凍結後の基準変更はせず addendum 別掲)。2連複 T-3 (2 場) のみ実現 ≥1 の点推定 = NEEDS MORE DATA。3連単 T-8 は PASS だが T-1 で REJECT = 締切までに消える | 機械判定 (t3d3_frozen.json) / lane-reports/t3d3_market_shrinkage_20260910.md / registry 行 54 |
| 2026-09-10 | forward collector (close_window) | **launchd 登録・稼働開始 (15:45 JST・Owner 指令 §9 GO)** | robots.txt Disallow 空・時計差 9 s。ページ = oddstf + odds3t (全 checkpoint) + odds3f + odds2tf (D-3:00/D-1:00/D+3:00/D+6:00) = 既存比 +11% (≈3,100 req/日 max)。2連単 1000 倍以上の整数表示を先方 raw HTML で発見し draft 側で対応 (src/scrape.py は同じ取りこぼしあり・無改変)。raw HTML gz を 9/24 まで保持。試験窓 9/11〜9/24 はメタデータのみで評価 (NG-FC1)。初回 fire ok 8/8・4 ページとも parse 数一致。**応答 8〜10 秒/ページが観測 (要監視)** | registry NG-FC1 / ~/Library/LaunchAgents/com.kyotei-ai.collect-close-window.plist / data/odds_snapshots/close_window/ |
| 2026-09-10 | shadow 第 2 アーム (単勝) の EV 判定 | **方式 A (3連単含意単勝 0.75/p3t × AI ≥ 1.15) に差し替え (shadow only・本番購入ロジック不変)** | 旧判定 (乖離 ≥0.20) は列名を変えずに比較列として残す。新列 p3t/price_A/ev_A/fire_A/stake_A/payout_A/judge。8/31 dry-run: 方式 A 99 本 vs 旧 10 本。今夜 23:30 nightly から稼働。daily_signal_notify.py は EV 判定を持たないため対象外 | scripts/shadow_report_national_tan.py |
| 2026-09-10 | Historical Replay Engine | 設計のみ (実装なし・T3D3 の後に最小試作 8 h・Owner GO) | 5 入力の as-of 定義・model-as-of ladder・leakage checklist 21 項目 (旧 Engine で満たされる 6 / 不足 15)・predict.py agg=None の全期間 aggregates と _resolve_train_window の meta 欠落合格を実コードで指摘 | designs/design_historical_replay_20260910.md |
| 2026-09-10 | 知人研究 Crosswalk | 整理完了 (判定に不使用・independent reference) | 44 行照合: 一致 28 / 不一致 9 / 未検証 7。知人の生存候補 (2連複 edge002) は市場 vs 市場の歪みで AI ブレンドとは別物。gap ブレンドは知人未踏。地雷 10 (多重評価・剪定 artifact・λ 退化 ほか) | artifacts/research/nextgen/t3d3/external_crosswalk_20260910.md |



# ===== DATA_STATUS.md =====

# DATA_STATUS — データ収集の現在地(正本)

- 制定: 2026-09-06(Owner 指令 §16「Data Collection Status 常設」を受け新設)
- 位置づけ: Canonical Research State の一部。機械可読の詳細 = `research_state.json` の `data_status` 節(矛盾したらそちらが正)
- 書式: 各行は「何を / どこに / いつから / 現在地 / 次のマイルストーン」に答える。進捗が動く行(バックフィル等)は更新日を必ず添える

## 1. 収集中・自走中

| 何を | どこに | いつから | 現在地(2026-09-09 時点) | 次のマイルストーン |
|---|---|---|---|---|
| **部品交換 層化バックフィル(B 案)** | 出力 `data/beforeinfo_parts/backfill/parts_bf_YYYY.parquet` / 進捗 state `artifacts/research/nextgen/parts_bf/parts_bf_state.json` / ログ `artifacts/research/nextgen/parts_bf/bf_run.log` | 2026-09-06 00:32 JST 起動 | **9/6 15:09 JST に自動停止(boatrace.jp の DNS 解決失敗 = iMac の IPv4 断・3,543 ページで停止)→ 9/9 22:15 JST に PID 12667 で続きから再開(行ロスなし)**。計画 49,968 ページ(756 節・cluster×年×季節の 84 セル層化・seed=20260906)。polite sleep≥2.5s・日次上限 8,000・実測 ≈5 p/min → 再開後 ETA 約 7 日(〜9/16 目安)。kill -9 でも行ロスなし(sidecar flush) | 完走 → Maintenance 仮説の増分確認(イベントスタディ)→ 増分が出た場合のみ全量 A 案(35 万ページ・48 日)を Owner 再判断 |
| **T-3 締切前オッズ(national_v2)** | `data/odds_snapshots/national_v2/` | 2026-07-10〜 | 全国・継続蓄積中(**3連単のみ。単勝は `data/odds_snapshots/national_tan/` 2026-07-16〜 に別収集**)。**欠損: 2026-09-07(2 ファイル)・09-09(0 ファイル)= iMac IPv4 断の影響(9/9 19:11 再起動で復旧)**。**real EV 評価はこのデータのみで主張可**(確定オッズは diagnostic)。知り合いバンドルとの相互検証 G3 = PASS(2026-09-09)・T-3 ドリフト追試の母材(NG-T3D1) | NG-E19SG(SG/G1 市場効率)の判定に足る蓄積 /(T-3 ドリフト追試・バンドル突合 G1-G5 は 2026-09-09 完了)|
| **締切直前〜締切後オッズ forward collector(close_window・NG-FC1)** | `data/odds_snapshots/close_window/YYYYMMDD/JJ/RR_<label>_<HHMMSS>.json`(+ `raw/*.html.gz` は 9/24 まで)/ 健全性 `_health.jsonl` / 締切上書き `deadlines_override_*.json` | **2026-09-10 15:45 JST 稼働開始**(launchd `com.kyotei-ai.collect-close-window`・60 s 発火・KYOTEI_FC_LIVE=1) | 取得点 D-3:00 / D-1:00 / D-0:30 / D-0:10 / D+3:00 / D+10:00(+D+6:00 条件付き)。ページ = 単勝複勝 + 3連単(全点)+ 3連複 + 2連単/2連複(D-3:00 / D-1:00 / D+3:00 / D+6:00)= 24 場 5 券種の自前収集。設計 ≈3,100 req/日 max(既存比 +11%)。初回 fire ok 8/8・parse 数一致(3t 120 / tf 6 / 2tf 30 / 3f 20)・**応答 8〜10 秒/ページを観測(要監視)**。**値は holdout 封印中(11/1 まで集計・閲覧禁止)・メタデータのみで試験評価** | 試験窓 2026-09-11〜09-24(メタデータ): D-0:30/D-0:10 の存廃・3f/2tf 継続・failure handling 実地 → Owner 確認で checkpoint 確定。11/1 以降に締切直前価格での executable EV 判定(T3D2/T3D3 の後継)|
| **beforeinfo(展示・チルト・安定板・気象)** | `data/beforeinfo/`(nightly 収集稼働中) | 2020〜(**2023-01-01〜04-24 は素データ自体が欠落。2026-09-09 追記: 同窓は beforeinfo だけでなく national/races_program・payouts・results も全場ゼロ。先方バンドルも同期間は空で補完不可(江戸川のみ先方 boats 約 722 レース分あり)**) | 全 356,476 ファイル実測済み: チルト充足 94-97%(未特徴化)・安定板 true 率 4.5-9.8%/年・気温 98.7%/水温 95%。**部品交換列は 6.5 年間パーサ取り違えで実質未収集**(正解実装は fetch_beforeinfo_ext.py 系の新 path のみ使用・誤パース旧列は再利用禁止)。注意: R1 の気象は「当日終値」汚染疑い(wind_delta 設計 §0-4・解析では R1 除外) | 2023-01〜04 と 2026-07-28〜 のバックフィル再開(2026-09-03 GO 済・実行待ち)/ 部品交換は上記バックフィル+日次収集で埋める |
| **研究用特徴 features_v2(B2 経路)の as-of 17 列欠損 → 復旧済み** | `artifacts/research/v2/features_v2.parquet`(2020-01-01〜2026-08-31・旧 = `*.gap0722_20260803build.bak`) | 2026-07-22 以降 100% NaN だった | **2026-09-10 復旧完了**: 原因 = 08-03 の build が末尾 07-21 の `features_extra3_structured.parquet` を left-join(builder の as-of 計算に問題なし)+ 気象スキャンが 07-27 で停止。復旧 = 同一 builder の延長版 `rc2/features_extra3_ext.parquet`(2026-06 全行 max|diff|=0)+ beforeinfo 再スキャン。学習窓 (≤07-21) はバイト同一、復元窓 as-of 独立再計算 300/300 一致、NaN 率平常。**G3 / EXIN1 の clean 再評価 = 両方 FAIL 不変**。副次: beforeinfo JSON は遡及で書き換わる(2026 年 60,398 行で wind_dir_code が後から入った・判定には無関係) | 09-01 以降は封印のため未収載 → 11/1 以降に再構築。旧 gate script(g3/exin1)の「末尾 = 08-03」assert は復元後に止まる(再実行時は fv2_clean_reeval.py) |
| **市場アノマリー holdout(3 テーマ)** | 登録書 `artifacts/research/mkt/preregistration_20260806.md`(2026-08-06 登録・以後変更禁止) | holdout 窓 = 2026-09-01〜10-31 | **封印中 — captured ≥2026-09-01 のオッズ集計・閲覧は禁止**。in-sample 窓 = 収集開始〜2026-08-31。W1/W2 実験の評価窓は封印保護のため 2026-07-27 以前で切る運用を継続 | **2026-11-01 開封** → 登録書の閾値のみで判定(in-sample での閾値調整は holdout に波及させない) |

## 2. 実装済み・設置待ち(crontab = shin 手動)

| 何を | どこに | 状態 | 次のマイルストーン |
|---|---|---|---|
| **部品交換 日次前向き収集** | `scripts/collect_parts_daily.py`(実装済み・実ページ検証 PASS 2026-09-05) | **crontab 待ち**。shin が貼る 1 行: `40 22 * * * /Users/saekishinnosuke/kyotei-ai/.venv/bin/python /Users/saekishinnosuke/kyotei-ai/scripts/collect_parts_daily.py >> /tmp/kyotei_parts_daily.log 2>&1` | crontab 設置(MORNING_BRIEF_20260905 記載・Owner 判断リスト 9)。夜間分は fetched_before_deadline=False=研究用(live T1 化には日中締切前ジョブが別途必要) |
| **風コレクタ 2 本(直前風変化 U-26)** | 設計正本 `artifacts/research/nextgen/wind_delta/wind_delta_design_20260906.md`。実装予定 `scripts/research/nextgen/wind_collect_openapi.py` / `wind_collect_amedas.py`・保存先案 `data/research/wind_delta/{source}/{YYYYMMDD}.jsonl` | **設計済み・未実装**(次レーンの最初のタスク・各 30-60 分規模)。boatrace.jp への追加リクエストはゼロ設計(openapi 156 req/日 + アメダス ≤144 req/日) | 実装 → crontab 設置(shin)→ 蓄積 2-4 週で PoC-2(アメダス・プロキシ妥当性)。歴史 PoC-1(ΔW×展示予言力)は蓄積不要・即実行可 |

## 3. 取得済み・静的資産(更新は必要時のみ)

| 何を | どこに | 範囲 | 備考・次 |
|---|---|---|---|
| **ERA5 環境パネル** | `artifacts/research/nextgen/env/era5_hourly_{01..24}.parquet` + `era5_meta.json`。取得スクリプト `scripts/research/nextgen/fetch_era5_env.py` | 2020-01-01〜2026-09-01・毎時・24 場・約 140 万行(気温/気圧/湿度/風/gust/降水/日射 + **air_density を物理式で導出済み**) | **事後再解析 = 予測特徴化は不可・研究窓の記述診断のみ**。本番接続時は Historical Forecast API へ差し替え(era5_meta.json 注記)。延長取得は必要時に fetch_era5_env.py 再実行 |
| 公式 K データ(結果・払戻) | `data/`(既存パイプライン) | 2020〜全国ほぼ完全(**例外: 2023-01-01〜04-24 は全場ゼロ / 住之江 payouts に 2026-04-25・05-06・07-05 の 3 日欠落 — 2026-09-09 G1 突合で発覚**)| レース後公開=ラベル専用(§16-O: market_odds の代用にしない) |
| 節マスタ / standing_panel | `artifacts/research/nextgen/setsu_master.parquet` ほか | 全期間 5,311 節 / 206 万行 | W2 系実験の共通基盤 |
| 静的資産群 | `configs/venue_course_azimuth.json`(high19/mid5)/ venue_branch_map / motor_exchange_months / venue_latlon / `venue_date_grade.parquet`(E1 副産物・29,715 行) | — | grade 表は NG-E19SG で使用可(caveat: 上流欠落 2023-01〜04 中旬) |
| W1 研究資産 | `i1_features.parquet`(206 万行・leak test PASS)/ e1_stage_decision_table.csv / e5w_features.parquet / e23 utility.parquet | — | FAIL 実験の副産物も削除しない(Pattern Library 方針) |
| 知り合いバンドル(external gift) | `data/external/gift_20260906/`(666MB/1,878 ファイル+バンドル2 11GB 生 HTML) | 2025-09〜2026-09 ほか | **突合済み(2026-09-09・NG-GIFTG): G1 払戻 / G2 締切時オッズ / G4 出走表 / G5 展示・チルト = 1,000 件一致率 100%、G3 締切前時系列 = 単勝 0.0%・3連単 0.30%(先方 7/23〜24 の 3連単ラベル回転バグを補正後)→ 構造化データは「うちと同値」ラベル**。直前板 parquet = `data/external/gift_20260906/_parsed/live_board_odds.parquet`(live 6,657R・2026-04-26〜08-31・単勝ページは先方収集に皆無)。secret 様ファイル(名前照合 8 本)は未開封隔離。current_race_with_odds.json は合成サンプル疑い=使用禁止。統合報告 = research/GIFT_INVESTIGATION_20260909.md(GitHub)/ 原本 lane-reports/gift_investigation_20260909.md |
| 市場パネル(NG-TS1・Lane M) | `artifacts/research/nextgen/ts/panels/`(odds_pre 528 万行 / odds_close 193 万行 / payouts_win / deadlines / `market_availability_audit.md`)。builder = `scripts/research/nextgen/ts_build_market_panels.py` | 2025-07-01〜2026-08-31(09-01〜 は封印・列挙段階で除外) | **5 券種の A/B/C 分類済み(D なし)**。3連複・2連単・2連複の全国締切前は先方直前板(T-1・6.6k R)と先方 checkpoint(7/25〜8/1・0.7k R)のみ = 自前収集ゼロ。うちの final は住之江のみ(桐生 final 無し)。旧形式 timeseries JSON(〜2026-06 上旬・snapshot_time 無し・ファイル名 HHMM)は captured_at で補完(4,163 件)。timeseries の締切未解決 451 レース(07-09 以前の一部)は lead を作れず除外 |

## 4. 未取得(Wish List・research_state.json より)

選手コメント時系列(HIGH)/ プロペラ形状(HIGH・困難)/ 1M 映像展開(MED・打ち切り済)/ 人間関係(MED)/ ピット常時(LOW-MED)



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
| U-34 | コース構造×攻め手/受け手の戦術特性(H-A) | ⬜未検証(BACKLOG) | SOB1 8 チャネル成立(in-sample)・PXR1 は受け手個人差 FAIL | SOB1 将来窓 ∧ SC2 の両 PASS 後に起票 |
| U-35 | 特定水面への習熟×調整能力×難条件×コース(H-B) | ⬜未検証(BACKLOG) | 無条件当地は R-6 で否定済み・ADJ1 で調整能力は実在 | E7/E8(U-2)の結果を見てから設計確定 |
| U-36 | レース形成の感度マップ(H-C) | ⬜未検証(BACKLOG・設計候補) | SC1 分解成立・RC2 top6_mass 確定・WPOC1 副産物(ΔW→ST) | EXIN1 の結果(展示入力側)が前提 |
| U-37 | 専門家の判断材料の逆解析(H-D) | ⬜未検証(BACKLOG) | 記録なし(repo 内に専門家の判断記録は無し) | Expert Feature Gap Matrix を最初の成果物に |
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

### 1-f. Owner 研究指令 2026-09-09 由来の Hypothesis / Design Backlog(BACKLOG ONLY・T3D2/EXIN1 より先に実験しない)

- 出典は全て `research/OWNER_DIRECTIVE_20260909.md` §6(原文)。指令 §12 に従い、各仮説に改善軸(Probability accuracy / Race selection・readability / Market mispricing discovery / Executable profit・risk)を明記する
- 扱い順は 1-e と同じ: 観察 → 一般仮説 → 最小統計 PoC → OOS 再現 → 予測価値 → 市場価値 → 必要なら Architecture 投資(ゲート混同禁止)

#### U-34. Course Interaction × Tactical Profile(H-A: コース構造×攻め手の戦術特性×受け手/受益艇の戦術特性)
- 仮説文: 展開の系統的な歪み(誰が 1 着を奪い、誰が 2 着に残り、誰が連れるか)は「Racer A × Racer B」の個人ペアではなく、**コース構造 × 攻め手のコース別戦術特性 × 受け手/受益艇の戦術特性**の組合せで説明できる。例: 3 コースに攻撃型がいる時の 1/2/4/5 コースへの影響、4 コース攻撃型 → 5 コースの受益、攻撃で 1 着率は落ちるが 2 着には残るスケール反転
- なぜ有望か: NG-SOB1 で「攻め手プロファイル在席 → 受益候補艇の系統シフト」が 14 検定中 8 本・6 年間符号割れゼロで成立(in-sample・将来窓待ち)。NG-E10 の確認済み signature 7 件も「選手×コースの静的プロファイル」で表現できる型だった(P-4)。研究単位をコース×型に置けば個人ペアのサンプル枯渇(ペア再戦 n 中央値 1)を避けられる
- **何と違うか(再提案禁止との区別)**: ①**個人ペア固有効果の再研究ではない**(NG-PXR1 Step2 = 受け手側の個人差は検出不能で FAIL・GAT/pairwise は 2 重否定で棚上げ → 本仮説は受け手側も「型」で持つ)②R-7(純粋 externality)は前提として維持(自艇と隣が同時に動く型のみ)③NG-I1(薄層 6 係数)の同一形は作らない(型は特徴でなく研究単位)④R-4(汎用の攻撃タグ)とは違い**コース条件付き**の型
- 改善軸: **Probability accuracy**(攻め手在席時の 1 号艇・受益艇の条件付き較正)/ **Market mispricing discovery**(U-23 の市場側は SOB1 将来窓設計 §6 = holdout 開封後)
- 必要データと可用性(ls・行数): `results.parquet` 2,101,565 行(2020-01〜2026-09-08・approach / st / kimarite 列 → 受け手側プロファイル「攻められた時の 2 着残し率」「連れ率」は as-of で導出可能・未構築)/ `i1_features.parquet` 2,061,406 行(attack_propensity@course・approach_deviation・〜2026-07-27)/ `e10/p1_residual_panel.parquet` 1,710,414 行 / `e10/p2_dump_p120.parquet` 50,926R / `rc2/rc2_dump_p120_w.parquet` 8,997R(2026-07〜08)/ `sob1/` 成果物一式 / `sc1/sc1_race_labels.parquet` 341,174R
- 現在の証拠: SOB1 PASS(in-sample・将来窓で未確認)。受け手側の「型」は記録なし
- サンプル規模: 検証未実施(コース×型セルなら 1 セル数万レース級の見込み・凍結時に実数確認)
- 確信度: 低〜中(攻め手側は SOB1 で足場あり。受け手側の型が個人差 FAIL(PXR1)を超えて出るかは未知)
- 最初の成果物: **コース×型 の 6×6 影響行列**(攻め手のコース a × 型 → 各コース c の top1 / top2 残差シフト・as-of・placebo 付き)。最初は 4→1 / 4→5 / 3→1 の 3 セルに限定
- 進む条件: **SOB1 将来窓 REPRODUCED ∧ SC2 PASS の両方**(指令 §7)。片方でも未達なら起票しない
- 次のアクション: **BACKLOG ONLY・T3D2/EXIN1 より先に実験しない**。設計正本 = `artifacts/research/nextgen/designs/design_sob1_future_20260909.md` §8

#### U-35. Venue-Specific Adjustment Advantage(H-B: 特定水面への習熟×調整能力×環境難度×コース)
- 仮説文: 「地元だから強い」ではない。**特定水面への習熟が、特定の難条件(強風・波・特殊水面)での調整・操縦能力を高める** = Venue familiarity × Player adjustment skill × Environment difficulty × Course の条件付き効果。候補変数: 過去 N 年の当該場出走数 / 直近の当該場出走 / 場×コースの residual / 強風・波・特殊水面時の residual / 調整能力(ADJ1 s_i)/ 当日展示への改善速度
- なぜ有望か: 無条件の当地特徴は ablation でデッドウェイト(R-6)だが、憲章の分解(水面への慣れ / 風への適応 / 調整知識)は「難条件でだけ効くなら平均に埋没する」構造。NG-ADJ1 で調整能力の選手差は実在(ICC=0.160・前後半 ρ=0.752)。細分によるサンプル枯渇は **hierarchical shrinkage**(ADJ1 の EB 機構流用)で避ける
- **何と違うか**: ①**単純当地勝率ではない**(R-6 = 無条件当地の FAIL は維持・local_win / local_2rate の再投入はしない)②U-2(地元×難水面・E7/E8)の**上位形** — U-2 が「難条件 × 地元」の交互作用 3 本なら、本仮説は「習熟(連続量)× 調整能力 × 難度 × コース」の階層モデル。U-2 の結果が出るまで設計を確定しない ③「調整能力が高いから強い」の主効果特徴は作らない(adj_ms 統合設計の禁止事項を継承)④気温・水温の素値は使わない(R-5)
- 改善軸: **Probability accuracy**(難条件レースの条件付き較正)/ 副: **Race selection**(習熟差が出る難条件レースの選別)
- 必要データと可用性(ls・行数): `racers_program.parquet`(branch = 支部 列あり・行数未確認)/ `results.parquet` 2,101,565 行(racer_id × 場 の出走履歴 → 当該場出走数 as-of は導出可能)/ `features.parquet` 2,142,699 行(local_win / local_2rate・wind_speed / wave — ただし気象は R1 汚染 = 当日終値スタンプのため予測特徴化不可)/ `data/beforeinfo/` 2,328 日分(2020-01-01〜・2026-07 = 31 日 / 08 = 31 日・T1 の風・安定板)/ `motor_state/ms_panel.parquet` 682,094 行(stabilizer / wind_speed / z_ex 列・2024-06〜2026-06)/ `adj_skill/adj_series_table.parquet` 74,271 行(選手×節・s_i)/ **支部→県マップは repo に無し(24 行手作業・U-2 既知)** / 難場の客観化 = 22 場 KMeans 3 タイプ(既存資産・ファイル所在は要確認)
- 現在の証拠: 無条件形はゼロ効果済み(R-6)。条件付き形は記録なし。U-2(E7/E8)は未実行
- サンプル規模: 検証未実施。難条件(強風 ≥6m / 波 ≥5cm)は開催日の約 1 割(adj_ms 設計の実測 9.7%)→ 場×選手セルは薄く、shrinkage が生命線
- 確信度: 低(構造仮説として筋は良いが、当地系は 2 度否定の前例。E7/E8 全滅なら本仮説の優先度も下げる)
- 最初の成果物: **習熟 × 難度の 2×2 residual 表**(当該場出走数 上位/下位 × 難条件 有/無 の B2 残差・場 × コース層別・季節クリマトロジー置換プラセボ付き)。効果が「難条件 × 習熟あり」のセルにだけ出るかを見る存在確認まで
- 進む条件: U-2(E7/E8)の判定が出ていること。存在確認 PASS → 特徴化ゲートは exh120 併用 stacked を第一関門に置く(MORNING_BRIEF 新仮説 2「状態系特徴の共通罠」)
- 次のアクション: **BACKLOG ONLY・T3D2/EXIN1 より先に実験しない**。U-2 の受け皿 NG-E8SWAP(filed)とは別物

#### U-36. Race Formation Factor Map(H-C: レース形成の感度マップ)
- 仮説文: 1M のレース形成は 天候 × モーター/現在艇状態 × 選手 × 水面/会場 × コース + 6 艇配置 で決まる。**巨大モデルは作らず**、ST・展示・風 regime・戦術プロファイル配置を現実的な範囲で ± 変化させたときの 120 通り分布の動き(ΔP(120) / own shift / neighbor shift / downstream beneficiary shift / entropy / top6 mass)を測る **Race Formation Sensitivity Map** として設計候補を残す
- なぜ有望か: SC1 で分解 P(T)=ΣP(S)P(T|S) は成立(ΔH は null の 75 倍・同一 3 連単は複数展開の混合)。RC2 で top6_mass が確実性メーターとして確定。WPOC1 副産物で「風の変化は ST 遅延+分散を通じてレースに入る」(半期完全再現)。つまり「入力の摂動 → 分布の動き」を測る材料は揃いつつある。EXIN1 §5(指令)の「展開が読めるようになったか」の診断そのものが本マップの第 1 版
- **何と違うか**: ①大型 Scenario Generator / Race Simulator ではない(Owner 禁止維持)— 既存 B2 の推論に摂動を入れて感度を測るだけ・学習なし ②Meaningful Tail(U-31・SC1 で不在)を探す道具ではない ③Readability を利益シグナルにしない(指令 §8・RC2 で「読める≠儲かる」確定)— 用途は展開診断・race selection・点数圧縮に限定 ④明示積項の特徴化はしない
- 改善軸: **Race selection・readability**(主)/ **Probability accuracy**(EXIN1 の展開診断=どの入力が分布を動かすかの可視化)/ 副: Executable profit・risk(betting interface の scenario coverage 入力候補・実装は別)
- 必要データと可用性(ls・行数): 120 通り分布 = `e10/p2_dump_p120.parquet` 50,926R / `rc2/rc2_dump_p120_w.parquet` 8,997R / `readability/rc_race_metrics.parquet` 50,926R(entropy・top6_mass 等)/ 摂動対象の T1 入力 = `data/beforeinfo/` 2,328 日分(展示タイム・展示 ST・チルト・風)/ `ms_panel.parquet` 682,094 行(z_ex / z_st / tilt)/ `i1_features.parquet`(戦術プロファイル配置)/ 風 regime = `data/research/wind_delta/{amedas, openapi_t1}`(コレクタ実装済み・**蓄積は開始直後・crontab 待ち**)+ ERA5 24 場(`nextgen/env/era5_hourly_01..24.parquet`・事後再解析のため研究窓の記述のみ)
- **重要な依存**: 現行 B2 は当日展示を後段 exh120 でしか見ないため、展示 ST・展示タイムの摂動が「分布の動き」として意味を持つのは **NG-EXIN1 の B/C アーム(展示入力側)が成立した場合**。EXIN1 FAIL なら摂動できる入力は事前 ST 系 prior・風・戦術プロファイルに限られる(その範囲で第 1 版を作るかは Owner 判断)
- 現在の証拠: 記録なし(構成要素の SC1 / RC2 / WPOC1 は各々判定済み・マップ自体は未着手)
- サンプル規模: 検証未実施(摂動は推論のみ・レース数は dump 窓の 50,926 + 8,997)
- 確信度: 低〜中(道具としての成立は堅い・「読める」以上の価値は EXIN1 次第)
- 最初の成果物: **感度表(入力 × 指標)**: 摂動 8 種(1 号艇展示 ST ±1SD / センター艇展示タイム ±1SD / 風速 ±3m/s / 4 コース attack_propensity 上位⇄下位 など)× 指標 6 種(ΔP(120) の TVD / own / neighbor / downstream shift / Δentropy / Δtop6_mass)を p2 窓で 1 枚。全て推論のみ・学習なし
- 進む条件: NG-EXIN1 の判定が出ていること(B/C PASS なら展示摂動を含む版・A のみなら事前情報版)。マップが「4→5 受益」「1 号艇状態悪化時の他艇 shift」を再現して初めて SC2 / betting interface の入力に接続
- 次のアクション: **BACKLOG ONLY・T3D2/EXIN1 より先に実験しない**(設計候補として保存。EXIN1 §5 の展開診断が事実上の第 0 版)

#### U-37. Expert Forecaster Reverse Engineering(H-D: 上手い人間の判断材料の逆解析)
- 仮説文: 長期実績を確認できる専門家(元レーサー / 場専属解説者 / 実績追跡可能な予想者)は、一般客と**異なる観測対象・異なる判断分岐**を持っており、それは買い目ではなく「何を観測し、どこで判断を分けているか」として抽出できる。特に「事前予想 → 展示後に予想を変更した理由」に AI が持たない判断材料が集中する
- なぜ有望か: モデル改造 12 連敗・「効くのは情報追加だけ」の実験史(FINDINGS ①-2)に照らすと、次の情報源の候補を**人間の専門家の観測項目**から逆算するのは合理的。SG 桐生の hansei で shin 自身が「ピット速報・整備コメント」を読みに使えた実例(U-3 の起点)。SNS 予想屋を無条件に上手いと仮定しない(実績確認できる対象のみ)
- **何と違うか**: ①**買い目のコピー・予想の集約ではない**(市場は既に人間の予想を織り込んでいる = R-4 型の結末になるだけ)②U-15(元トップの名前人気)・T-2(SG 市場効率)のような市場心理仮説ではなく、**特徴量研究のフィルター**(何を次に特徴化するかを決める道具)③U-8(攻め気配検知)とは重なるが、本仮説は「専門家が見ているのに AI に無い項目」を網羅的に棚卸しする側
- 改善軸: **Probability accuracy**(新特徴量研究の優先順位付け)/ **Market mispricing discovery**(専門家が一般客と判断を分ける場面 = 市場が重み付けし切れていない情報の候補・U-21 と接続)
- 必要データと可用性(ls・行数): **repo 内に専門家の判断記録は無い**(私が確認した範囲: `data/sns/` = `sample_packyao.txt`(買い目サンプル 1 本)+ `evaluations/sample_packyao_eval.csv`(1 本)= いずれも「買い目」型で判断材料の記録ではない / `data/external/` は知人バンドルのみ / docs・lane-reports の grep で該当なし)→ **新規取得が必要**(公式サイトの場専属解説者コメント・元レーサー解説の事前/展示後コメント・取得方法と権利関係は要調査。本レーンはネットワーク禁止のため未確認)。AI 側の「既に持つ材料」は `features.parquet` 45 列(F41)+ exh120 入力 + i1 / MS6 定義から機械的に列挙可能
- 現在の証拠: 記録なし
- サンプル規模: 検証未実施(取得設計が先)
- 確信度: 低(道具としての価値は高いが、判断記録の取得可能性が未確認)
- 最初の成果物: **Expert Feature Gap Matrix** — 専門家の各判断材料を ①AI が既に持つ ②データはあるが未特徴化 ③既存データから導出可能 ④新規取得が必要 ⑤定量化困難 の 5 分類に振り分けた表(対象 3 名以上・各 20 項目以上を目標)。「事前予想 → 展示後変更」の理由は別列で採取
- 進む条件: 対象専門家の実績が確認できること(SNS の自称実績は不可)+ 判断記録の取得手段が確定していること。Matrix の ②③ が新特徴量研究の候補リストになり、④は取得設計、⑤は Intent 層の課題として記録
- 次のアクション: **BACKLOG ONLY・T3D2/EXIN1 より先に実験しない**。取得手段の調査(ネットワークを伴う)は Owner GO 後に別レーンで

---

## 2. TESTING(事前登録済みで検証枠にある — 実行中の実験は現在なし・2026-09-10。直近完了 = NG-T3D2 / NG-EXIN1)

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


### 2-x. 2026-09-09 Owner 指令で登録 → 2026-09-10 完了(判定は registry / DECISION_LOG)

- **NG-T3D2 Executable EV / Closing Price Proxy** — 仮説: 締切前に固定したルール(3連単含意単勝 / drift 補正 / late execution)で「実際に買える価格」の EV を判定できる。改善軸 = Executable profit / risk(+ Market mispricing discovery)。registry NG-T3D2
- **NG-EXIN1 当日展示の入力側化** — 仮説: 当日展示を B2 の 6 艇 attention に入れる方が exh120 後段補正より強く、他艇との相対状態(展開)まで学習できる。改善軸 = Probability accuracy(secondary: 展開診断)。registry NG-EXIN1

### 2-y. 2026-09-10 Owner 指令で登録 → 同日完了: NG-TS1 Ticket-Space Calibration Decomposition(判定 = ケース D「選択そのもの」。registry / DECISION_LOG)

- **2026-09-10 15:40 登録 → 同日完了: NG-T3D3 = gap 条件付きブレンド**(凍結判定 = ケース1: 3連複・2連単・2連複 MARKET GATE CANDIDATE / 3連単 REJECT。実質 = ケース3 寄り: hit 較正は回復・表示価格 EV は残るが確定配当ベースの実現値は全券種 <1 = 高オッズ側の金額重み過信が残留。FINDINGS ①12・P9・lane-reports/t3d3_market_shrinkage_20260910.md)。次の TESTING 候補(未登録・Owner GO 待ち): **NG-T3D4 = オッズ帯条件付き λ + 実現値 CI gate**。以下は登録前の記述(歴史記録): 旧候補 **NG-T3D3 = gap 条件付きブレンド**(log p' = (1−λ)log p + λ log q・λ = λ0 + λ1·z_gap・券種 × lead 別)。仮説「乖離に応じて AI を市場側へ縮めれば EV 選択後の CR が 1 に戻り、かつ EV≥1.15 の組が残る券種がある」。全滅なら「食い違いは価格に織り込み済み」。designs/design_t3d3_20260910.md
- 商品候補の仮説(検証前): 2連複 / 2連単は情報優位(直前板でも AI ≥ 市場)が締切まで残り価格が中程度に持つ → T3D3 PASS なら最初の Market Gate 候補。3連単に固執する根拠は無いが乗り換える証拠も無い
  - **2026-09-10 T3D3 後の判定**: 2連単は凍結 primary で唯一 PASS(hit-CR 0.905・survival 0.70)、2連複は top1 で CALIBRATED、桐生・住之江の 2連複 T-3 だけ実現 ≥1(n 小・NEEDS MORE DATA)。3連単は REJECT(1 分前で robust EV<1・8 分前の PASS は締切で消える)→ **3連単に固執する理由は消えた**。ただし「乗り換えれば勝てる」証拠もまだ無い(実現値は 4 券種とも <1)

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

- **「3連単の選択後の過信は着順順序付け(集合→順序 / 3 着条件付き)の問題」→ 否定(2026-09-10・NG-TS1)**: 3連複・2連複でも同じ過信(CR 0.73 / 0.76)、順序段は較正済み(0.85〜0.99)。順序較正層(SC2 型)で EV 選択後の過信を直す提案は同一形で再提案しない
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

- 最終更新: 2026-09-10(… → NG-T3D2 / NG-EXIN1 → features_v2 復旧 → NG-TS1 Ticket-Space 反映)
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

### 9. 「EV あり」と判定した単勝の 3 分の 2 は締切価格では EV なし — 含意単勝で判定すれば 6 割が残る(NG-T3D2・2026-09-10)

- 数値: T-3(先方 3.4 分前)で AI×表示単勝 ≥1.15 と判定した 678 本のうち、締切価格でも EV>1 だったのは **32% [29, 36]**。3連単 120 通りから逆算した含意単勝価格(0.75/p3t)で判定すると **58% [52, 66]**(選択 200 本・凍結 PASS 線 = CI 下限 50% を通過)。表示オッズの drift 補正(帯×時間×選択の shrunk model)は 33% で効かず、締切 2 秒前の板まで待っても 44% [40, 48]。見かけ EV と drift の Spearman **−0.69 [−0.72, −0.66]**(n=2,316): 見かけ EV 十分位 2.93 の艇は締切までに 0.24 倍へ
- 出典: lane-reports/t3d2_executable_ev_20260909.md / registry NG-T3D2 / 凍結 artifacts/research/nextgen/t3d2/t3d2_frozen.json
- だから何?: 「割安に見える」の大半は薄い単勝板と AI のズレで、締切の大口が埋める(AI 較正は良好・ECE 0.0065)。EV 判定の価格入力を深い市場(3連単)の含意に替えるのが今ある最良の代理。それでも 4 割は締切で EV<1 なので、締切直前の実価格を自前で継続収集しないと執行可能 EV は確定できない(表示は 1 分刻み・T-30 秒は歴史に無い)
- 【分かったこと】締切前の EV 判定は「確率」より「価格の代理」で決まる【予測に効くか】確率モデルは不変・判定ルールの入力を替える話【市場】3連単は価格が持つ(survival 96%)が realized 0.51 [0.19, 0.94] = 選ばれた組の確率が過大 → 次の壁は選択後較正(価格ではない)

### 10. 当日展示は後段補正(exh120)で取り切っている — NN の入力側に入れても同じ(NG-EXIN1・2026-09-10)

- 数値: holdout(n=4,530)で 展示入力側 B − 現行 A = **+0.0071 [+0.0015, +0.0129]**(悪化)、B に exh120 を重ねた C − B = +0.0007 [−0.0001, +0.0015](残余ゼロ)。上流特徴が健全な clean 窓(n=2,921)では B − A = −0.0015 [−0.0073, +0.0042] = 差なし。パネル fold2 では B − base −0.0204(MS3 の当日展示 z 単独 −0.0209 を再現)
- 出典: lane-reports/exin1_results_20260909.md / registry NG-EXIN1 / 凍結 artifacts/research/nextgen/exin1/exin1_frozen.json
- だから何?: MS3・G3・EXIN1 の 3 実験で「当日展示の情報は exh120 が既に全部使っている」が一致。6 艇 attention に展示を与えても展開(1 号艇悪化時の再配分・センター艇上昇時の隣接・二次受益)は A 以上に読めない(NOT_ABSORBED)。後段の薄い補正層は上流特徴が壊れた期間でも効く(劣化窓で B − A +0.0227)= 現行設計を維持する積極理由。展示の主戦線は閉じる。GAT を作り直す根拠にもならない
- 【分かったこと】展示情報の取り込み方は現行が上限【予測に効くか】効かない(本番不変)【市場】未評価(オッズ不使用)

### 11. EV で選んだ舟券の過信は「順序」ではなく「AI と市場の食い違い」で生まれる — 3連複・2連単・2連複でも同じ(NG-TS1・2026-09-10)

- 数値: AI 確率だけで上位 3 組を選ぶと 4 券種すべて CR(実際 ÷ 言った確率)0.99〜1.01(replica 59,923R・ECE ≤ 0.0023)。EV≥1.15 上位 3 組で選ぶと締切 1 分前の板で 3連単 0.61 [0.52,0.71] / 3連複 0.73 / 2連単 0.74 / 2連複 0.76(全部過信・本番モデルも同符号)。chain 分解: 顔ぶれ段(3連複 0.76・2連単 0.72・2連複 0.74)が主因で順序段は 0.85〜0.99。p−q 五分位で AI の CR 1.3→0.8、市場の CR 0.8→1.3 = 真値は間
- 予測に効くか: **効く方向が確定** — 直すのは順序ではなく「乖離に応じて AI を市場側へ縮める」1 つ(T3D3 設計)。【市場】直前板では 3連単は市場が上(NLL +0.030)、2連複は AI が上(−0.033)、3 分前は全券種 AI が上。価格安定 3連単 97% > 3連複 83% > 2連単 82% > 2連複 73% ≫ 単勝 28%。実現値は全券種 <1(診断・ROI 根拠にしない)
- 確信度: **高**(2 モデル × 4 anchor × 4 券種で同符号・凍結ケース規則の機械適用)。出典 = lane-reports/ticket_space_20260910.md

### 12. AI と市場を混ぜると予測は良くなり、的中率の過信も直る — しかし「実際に受け取る額」では +EV が残らない(NG-T3D3・2026-09-10)

- **事実**: AI 確率を市場 de-vig 確率へ 3〜6 割縮める対数線形ブレンド(パラメータ 1〜2 個・券種 × lead 別)で、3連複・2連単・2連複は AI 単独・市場単独の両方より NLL が良化(test = 本番モデル 2026-07〜08・CI で有意)。3連単は市場と同等、単勝は AI 単独が最良。EV≥1.15 で選んだ後の hit-CR は 0.52〜0.73 → 0.62〜0.905(2連単 CALIBRATED)。表示価格の EV≥1.15 は 1 レース 0.6〜1.5 組残り、年 2〜8 万 BET(頻度は制約でない・数か月で真偽が判る)。
- **しかし**: 確定配当ベースの実現値は T-1 で全券種 0.64〜0.85。締切価格は選んだ組で 8〜15% 下がり(3 分前なら 3〜4 割・単勝 6 割)、さらに締切価格で見た期待(1.15〜1.3)に対し実現は 0.5〜0.8 倍 = **的中回数では較正されていても、金額を支配する高オッズの組で p' がまだ高すぎる**(favorite-longshot 形の残留過信)。
- **含意**: 凍結ルールの機械判定はケース1(3 券種 MARKET GATE CANDIDATE・3連単 REJECT)だが、実質はケース3 寄り「乖離は主に AI 誤差で、買える歪みは未証明」。次の gate は「確定配当ベースの実現値 CI 下端 > 1」を含めるべき。唯一の例外候補 = 桐生・住之江 2連複 T-3(実現 1.07〜1.24・n 300〜600・CI は 1 を跨ぐ)。3連単を主商品にする理由は残っていない。
- 出典: lane-reports/t3d3_market_shrinkage_20260910.md / artifacts/research/nextgen/t3d3/

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

### 1. 「締切時オッズ×100 ≠ 確定払戻」は両側で再現、ただし極端値は返還由来(NG-GIFTG・2026-09-09)

- 数値: 勝ち組の締切時 3連単オッズ×100 が確定払戻より大きいレース = うち 133/7,078(1.88%)・先方バンドル 211/10,175(2.07%)、逆方向は両側 0。先方申告「最大 +5.7 倍」は再現せず(うち 5.7 倍超 29 件・最大 346 倍)。乖離 133 件のうち勝ち艇の決まり手「恵まれ」が 51 件(38%・全体では 0.8%)
- 出典: lane-reports/gift_gates_ga_20260909.md(G2 追加)/ registry NG-GIFTG
- だから何?: 「締切時オッズ」はバッチ集計の表示値で、精算は必ず確定払戻で行う(既存規律の再確認)。極端値の主因は返還レース(仮説)であり parser 不良ではない

### 2. うちの歴史データに 2023-01-01〜04-24 の全場欠落(beforeinfo だけではなかった)(2026-09-09)

- 数値: national/races_program・payouts・results・beforeinfo が同窓で全場ゼロ(参考: 2022 年同窓は桐生 732 / 江戸川 672 / 住之江 816 レース)。加えて住之江 payouts に 2026-04-25・05-06・07-05 の 3 日欠落(G1 の未一致 35 レースの正体)。知り合いバンドルも同期間は空で補完不可(江戸川のみ先方 boats 約 722 レース分)
- 出典: lane-reports/gift_gates_ga_20260909.md(G6)
- だから何?: 過去の実験の学習窓・grade 表(venue_date_grade)の「上流欠落 2023-01〜04 中旬」はこの穴が原因。再取得は boatrace.jp の公式 LZH(data/raw/B, K)から可能か要確認(shin GO 事項)

### 3. 研究用特徴(features_v2)の as-of 17 列が 2026-07-22 以降 100% 欠損していた(2026-09-10)

- **復旧済み 2026-09-10**: 原因 = 08-03 の build が 07-21 で止まった features_extra3_structured を left-join(計算式・取得の問題ではない)。leakage-safe に復旧(学習窓バイト同一・as-of 独立再計算 300/300)。G3 / EXIN1 の clean 再評価でも判定不変(両方 FAIL)。lane-reports/features_v2_gap_20260910.md

- 数値: artifacts/research/v2/features_v2.parquet の setsu_*・venue_lane_*_prior・racer_recent5_*・st_q10/std_prior・local 系・wind/wave が 07-22 以降 NaN。この窓では全モデルが 1 号艇を 34% と予測(実際 55.7%)。G3 の「untouched」サブ窓と EXIN1 holdout の 1/3 がこの劣化窓に当たる。live 単勝シグナル経路(LightGBM + data/processed/<venue>/features.parquet)は同種列の NaN 0.2% で無傷(L1 確認・私が確認した範囲では)
- 出典: artifacts/research/nextgen/exin1/exin1_addendum2_cleanwindow.json / lane-reports/exin1_results_20260909.md
- だから何?: 07-22 以降の研究 holdout は劣化窓を除いて読む。原因特定と復旧が研究基盤の P0(復旧後に G3 / EXIN1 の clean 再評価)

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

### P6. 選んだ単勝は締切までに約半分に縮む(T-3 ドリフト)【**再現・PASS**(2026-09-09・NG-T3D1)】

- 条件: 本番シグナル(AI − 市場 ≥ 0.20・単勝帯 0.0375〜0.25)が fire した単勝を、選択時(締切 6.3 分前中央値)/ T-5 / T-3 の表示オッズで見たとき
- 効果: 締切時オッズ ÷ 選択時オッズ の中央値 **0.47〜0.67**(設計別・同オッズ帯の対照は 0.98〜1.0・placebo p=0.000)。見かけ EV 2.83 に対し実現値 0.819 [0.70, 0.95](gap 3.46)。外部研究者の独立申告 0.446 と整合
- n: fire 41 本(先方 final 全艇 910R)/ 534 本(実現値)/ 検証期間: 2026-07-13〜08-31(holdout 未接触)
- 確信度: **中〜高**(2 phase・3 設計で符号一致・外部申告と整合)。ただし fire∧T-3∧final は 41 本と薄い
- 最終確認日: 2026-09-09
- 出典: lane-reports/gift_t3_drift_phase1_20260909.md / phase2 / registry NG-T3D1
- 3問:【分かったこと】fire は「薄い単勝プールが一時的に過小評価した艇」を拾い、締切間際の大量投票で AI 側に寄る。3連単からの含意単勝(深いプール)では締切 1 分前に縮みが完了(0.445 vs 対照 0.889)。AI 確率の誤りではなく「選択時オッズが最終まで持たない」【予測に効くか】確率そのものは不変。**EV 判定の入力を「締切時に持つオッズ」に替える必要**(NG-T3D2 候補: 含意単勝判定 / drift 係数 / 執行時点)【市場】買える歪みの確定ではない。ROI 主張なし

### P7. 見かけ EV が高いほど締切までに潰れる(selection-induced drift)【**確定**(2026-09-10・NG-T3D2)】

- 条件: T-3 前後の表示単勝で計算した見かけ EV(AI 確率 × 表示オッズ)を十分位に切る
- 効果: 見かけ EV と締切までの log drift の Spearman −0.69 [−0.72, −0.66]。十分位 0.19→drift 1.90 / 0.80→1.00 / 1.23→0.60 / 2.93→0.24。選択艇 0.42 vs 非選択 1.16。締切後の EV は全十分位で中央値 <1(0.27〜0.85)
- n: 2,316(先方 T-3 → final・7/23〜8/1・24 場)/ 検証期間: 開発窓 2026-07-10〜08-31(holdout 未接触)
- 確信度: **高**(T3D1 の fire 0.47〜0.67・外部申告 0.446・3 anchor で方向一致)
- 最終確認日: 2026-09-10
- 出典: lane-reports/t3d2_executable_ev_20260909.md / registry NG-T3D2
- 3問:【分かったこと】「割安」の大半は薄い単勝板の一時的ズレ【予測に効くか】確率は不変。EV 判定の価格入力を 3連単含意に替える(方式 A)と survival 32%→58%【市場】買える歪みの確定ではない。realized は CI が 1 を跨ぐか下回る(ROI 主張なし)

### P8. EV 選択後の過信は全券種共通・AI と市場の乖離に比例(winner's curse)【**確定**(2026-09-10・NG-TS1)】

- 条件: p × 表示オッズ ≥ 1.15 の上位 3 組(3連単・3連複・2連単・2連複)。効果: CR 0.61〜0.76(T-1・24 場)、T-3 / T-3cp / T-8 / 本番モデルでも同符号。乖離(p−q)最上位五分位で AI CR 0.79〜0.90 / 市場 CR 1.16〜1.34。predicted EV 五分位で単調(最上位 0.71〜0.82)。順序段(集合→順序・1・2 着→3 着)は無傷。3連単の 60〜150 倍帯が最も強い(CR 0.43)
- 出典: lane-reports/ticket_space_20260910.md §4 / ts1_market_results.json

### P9. 残った過信は「オッズ帯」に沿って偏在する — 的中率の較正比が 1 でも金額の較正比は 0.5〜0.8【**確定(診断)**(2026-09-10・NG-T3D3 addendum)】

- 条件: AI × 市場のブレンド後に表示価格 EV≥1.15 で選んだ組(T-1・4 券種)。hit-CR 0.84〜1.03 に対し「実現 ÷ 締切価格での期待」= 0.48〜0.67。単勝・2連複 T-3(2 場)は 0.77 / 1.30。
- 意味: 的中回数は当たりやすい組が、金額は高オッズの組が支配する。ブレンドは前者を直し後者を直し切れていない → 次の較正はオッズ帯条件付き(λ を favorite-longshot 軸で持つ)。
- 出典: tables/addendum_close_ev.csv(凍結後・判定に不使用)

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
 "updated_at": "2026-09-10",
 "updated_by": "claude/t3d3-session (Owner研究指令 2026-09-10 第 2 弾 完走 16:10)",
 "canonical_note": "本ファイルが機械可読の正本。人間可読の詳細は同ディレクトリの md 群。Artifact 494f0be1-a091-4cc3-b90f-72df7dc0b01d は view であり正本ではない",
 "architecture_version": "v2.1",
 "architecture_doc": "docs/ARCHITECTURE_FREEZE_v2.1.md",
 "current_phase": "2026-09-10 16:10: Owner 指令 第 2 弾「AI と市場の意見差を較正し、本当に買えるエッジが現実的な頻度で残るか決着させる」完走 — NG-T3D3 (gap 条件付き市場ブレンド): λ 内点 0.31〜0.59・3連複/2連単/2連複はブレンドが AI・市場の両方より NLL 良化・S5 hit-CR 0.52〜0.73 → 0.62〜0.905 (2連単 CALIBRATED = PASS)・表示価格 EV≥1.15 は 0.6〜1.5 組/R 残り年 2〜8 万 BET (頻度は制約でない・検出 0.2〜0.6 年)・**凍結判定 = ケース1 (3連複・2連単・2連複 MARKET_GATE_CANDIDATE / 3連単 REJECT / CORE なし)・実質 = ケース3 寄り (確定配当ベースの実現値は全券種 0.64〜0.85 = 締切価格 8〜15% 減 + 高オッズ側の金額重み過信 0.5〜0.8)**。2連複 T-3 (桐生/住之江) のみ実現 ≥1 = NEEDS_MORE_DATA。forward collector 5 券種 稼働 (NG-FC1・15:45〜)・shadow 第 2 アーム 方式 A・Historical Replay 設計 (leakage 21)・知人 Crosswalk 44 行。次 = NG-T3D4 (オッズ帯条件付き λ + 実現値 CI gate) の Owner GO。 | 前段: 2026-09-10: Owner 指令「予測できる→実際に買える」完走 — NG-T3D2 (Executable EV): 方式 A 3連単含意単勝 PASS・優位 (T-3 判定 EV≥1.15 の締切 survival 58% [52,66] vs naive 32% [29,36])・B drift 補正 FAIL・C 締切 2 秒前 44%・selection-induced drift ρ −0.69・3連単は価格が持つ (96%) が realized 0.51 = 選択後較正が次課題 / NG-EXIN1 (展示入力側化): FAIL_STACKED (B−A +0.0071 [+0.0015,+0.0129]・C−B ZERO・clean 窓差なし・NOT_ABSORBED) = 当日展示は exh120 で取り切っている・本番 b2f41 不変 / 副産物: features_v2 as-of 17 列 2026-07-22 以降欠損 (研究基盤 P0)。 | 前段: 2026-09-09: 知り合いバンドル調査 完走 — NG-GIFTG 突合 5/5 PASS (先方構造化データはうちと同値・G3 は先方 7/23-24 の 3連単回転バグ補正が条件) / NG-T3D1 T-3 ドリフト追試 H1 PASS (fire 単勝 drift 0.47〜0.67・先方 0.446 は CI 内)・H3 PASS (見かけ EV 2.83 vs 実現 0.82)・H2 INCONCLUSIVE・H4 不支持。次 = Owner 裁定 (NG-T3D2 EV 判定の実効化 / NG-EXIN1)。 | 前段: W3 (Owner研究指令 2026-09-06) 完走。9件の判定: NG-MS3 MS_NET_ZERO (当日展示z単独−0.0209がMS6−0.0160より強く、当日展示併用下でMS6純増分は+0.0023=無し。MS2 PASSの実体=当日展示の冗長エンコード) / NG-G3 FAIL_STACKED (本番相当窓で生−0.0146だがexh120併用スタック+0.0058 CI[+0.0002,+0.0112]=MS6本番昇格なし・b2f41不変) / NG-SOB1 PASS (2着スケール反転=まくりは1着を奪うが2着は残す・in-sample caveat付き・4→1攻め時勝率低下はB2でも残存=織り込み不足候補) / NG-SC1 done_exploratory (scenario 10クラス分解成立・Meaningful Tail不在=集中はbodyに住む・S実現条件付きでB2に系統較正ズレ→SC2起票候補) / NG-RC2 done_primary (RC Score v1=top6_mass・OOS上位10%でhit6 62.4%=+21.8pp・24/24場・utility相関ゼロ=読める≠儲かる) / NG-WPOC1 不支持 (副産物=風変化でST+3.7ms遅延+SD増・半期完全再現) / W-2 R1気象汚染確定 (6.5年×24場・恒久規律=beforeinfo気象解析はR1除外・E5NR主検定とB2本番特徴は無傷) / W-1 風コレクタ2本実装検証済 (crontab 2行=shin設置待ち) / docs §16 mirror再構成済 (DECISION_LOG/DATA_STATUS/designs新設)。次の主戦線 = NG-EXIN1 (当日展示の入力側特徴化 vs exh120後段のstacked直接対決・MS3でex raw−0.0209実測) + SC2 (S条件付き較正ゲート) + SOB1将来窓再確認。production変更ゼロ (b2f41_prod2026_prod3不変)",
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
 "current_experiment_note": "Owner 指令 第 2 弾 完走 (2026-09-10 16:10)。実行中の実験なし。自走 = 部品バックフィル PID 12667 + forward collector 試験 (NG-FC1・9/11〜9/24 メタデータ評価) + shadow 方式 A (nightly)。次 = NG-T3D4 起票 (Owner GO)",
 "experiments": {
  "registry_path": "artifacts/research/experiment_registry.jsonl",
  "adopted": [
   {
    "id": "B2",
    "change": "120通り直接スコアリング+6艇attention",
    "effect": "全指標でB0/B1超え (唯一のアーキ勝利)"
   },
   {
    "id": "extra7",
    "change": "当地収縮+節内フォーム7特徴",
    "effect": "fold2 NLL 3.785→3.777"
   },
   {
    "id": "extra2",
    "change": "場×コース歴史率+直近5走",
    "effect": "extra2単独で全国Hit@1 9.88→10.07%、3seed併用で10.21%"
   },
   {
    "id": "extra3",
    "change": "ST分布+節内得点 (F=41完成)",
    "effect": "ΔNLL -0.004〜-0.007"
   },
   {
    "id": "seed3",
    "change": "3seed確率平均",
    "effect": "+0.14pp (3で飽和)"
   },
   {
    "id": "exh120",
    "change": "展示タイム/ST/F の後段補正層",
    "effect": "ΔNLL -0.018 研究窓・24/24場改善"
   },
   {
    "id": "mkt_blend",
    "change": "市場ブレンド w=0.85 (推論後段)",
    "effect": "住之江で市場単独NLL超え"
   },
   {
    "id": "f41_skew_fix",
    "change": "学習気象を beforeinfo 由来へ統一",
    "effect": "GATE PASS (2026-08-06切替)"
   }
  ],
  "rejected": [
   {
    "id": "b2h_embedding",
    "reason": "racer ID embedding 改善ゼロ"
   },
   {
    "id": "composite_loss/capacity/mixture/race_no/5seed/temp_calib",
    "reason": "モデル改造系6件 全て誤差圏"
   },
   {
    "id": "f43_temp_water",
    "reason": "気温水温素値 = fold間符号反転・季節の焼き直し"
   },
   {
    "id": "thin_layers_tide_style_gap",
    "reason": "潮汐/戦型/番組ギャップ薄層 -0.0006〜0.0011 (基準0.003未達)"
   },
   {
    "id": "class_code",
    "reason": "階級ラベル全棄却 (2026-06確定・再投入禁止)"
   },
   {
    "id": "explicit_interactions",
    "reason": "明示積項は桐生で過学習方向"
   }
  ],
  "frozen": [
   {
    "id": "lambdarank_portfolio",
    "reason": "GATE FAIL・コード残存・Baseline扱い"
   }
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
   {
    "id": "NG-E19SG",
    "theme": "SG/G1祭り市場効率",
    "gate": "two-sided・締切前オッズ=real。蓄積待ち (2026-07-10〜)。grade表は E1 副産物 venue_date_grade.parquet が利用可"
   },
   {
    "id": "NG-E8SWAP",
    "theme": "当地デッドウェイト置換 (起票のみ)",
    "gate": "E8全滅時のみ着手"
   },
   {
    "id": "NG-FC1",
    "theme": "forward collector 2 週間試験 (close_window・5 券種・メタデータのみ評価)",
    "gate": "評価窓 2026-09-11〜09-24。D-0:30/D-0:10 存廃・3f/2tf 継続・failure handling 実地。オッズ値は 11/1 まで見ない"
   }
  ],
  "done_20260910": [
   {
    "id": "NG-TS1",
    "theme": "Ticket-Space Calibration Decomposition",
    "verdict": "ケース D (選択そのもの)。AI-only 較正・EV 選択後 4 券種すべて過信 (T-1 0.61/0.73/0.74/0.76)・順序段は無傷",
    "report": "lane-reports/ticket_space_20260910.md"
   },
   {
    "id": "NG-T3D3",
    "theme": "gap 条件付き市場ブレンド (log-linear pool・λ0+λ1·g(z_gap)・券種×lead・候補選択は fit 窓内 split)",
    "verdict": "凍結 = case1_market_gate (3連複・2連単・2連複 MGC / 3連単 REJECT / CORE なし)。実質 = ケース3 寄り (実現値 全券種 <1・高オッズ側の金額重み過信残留)",
    "report": "lane-reports/t3d3_market_shrinkage_20260910.md",
    "artifacts": "artifacts/research/nextgen/t3d3/"
   }
  ],
  "designed_not_registered": [
   {
    "id": "NG-T3D4",
    "theme": "オッズ帯 (favorite-longshot) 条件付き λ + 判定 = 確定配当ベースの実現値 CI 下端 > 1 + 同数ランダム剪定比較",
    "design": "未作成 (lane-reports/t3d3_market_shrinkage_20260910.md §6・§10-10 が根拠)",
    "gate": "Owner GO 後に設計 → 事前登録"
   }
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
   "SG/G1は観光マネーで市場が甘くなる (SG当日 AI NLL 0.818 vs 0.981・n=12) → NG-E19SG",
   "残った過信はオッズ帯に偏在する (hit-CR ≈1 でも実現 ÷ 締切期待 = 0.5〜0.8・FINDINGS P9) → オッズ帯条件付き λ で実現値が 1 を超えるか = NG-T3D4 (未登録)"
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
   "U-18 展開圧力×対応力 — **Step1-2ミニPoC完了 (NG-PXR1 2026-09-06): B側対応力は検出不能 (p=0.99)・A側slopeも宣言と逆符号が主 → GAT棚上げ確定 (E10と2重の否定)**。「圧力が無い」ではなく「対応力の個人差が現データで検出不能」。副産物=攻め手在席時の1号艇過小評価/外隣過大評価の条件付き較正パターン (別起票候補)",
   "U-19 コース条件付き相性 (Course-conditioned Matchup Skill)",
   "U-20 波及と受益艇 (Interaction propagation / beneficiary effect)",
   "U-21 市場の重み付け不足情報 (Known-but-underweighted market information)",
   "U-22 条件付き相互作用の誤価格 (Conditional interaction mispricing。S-5=まくり筋はAI側較正歪みのみ確定、の判定は上書きしない)",
   "U-23 二次・三次受益艇の誤価格 (Second-order beneficiary mispricing)",
   "U-24 シナリオ分散買い (Scenario-aware betting portfolio・購入層の概念。実装は市場レイヤ成熟後)",
   "U-25 頑健EV+下振れ最適化 (Robust EV + downside-aware optimization)",
   "U-26 直前風変化 (Current Wind Delta) — 展示時→本番直前の風変化がST・展示予測力を変える (Owner 2026-09-06。E5NRの「強風で展示予言力低下」が傍証)",
   "U-27 風の不安定性 (Wind Volatility) — 平均風速でなく変動 (SD/max-min/gust/風向変化/regime transition) がST分散・荒れやすさに影響。平均5m安定日と2-9m往復日を同一扱いしない",
   "U-28 選手の風適応力 (Player Wind Adaptation) — 風変化への適応能力に選手差。まず風変化に対するST誤差・分散の再現可能な選手差をas-of+shrinkageで確認 (即特徴量化しない)",
   "U-29 環境×モーター状態 (Environment × Motor) — 空気密度/水温/気温−水温差等の「変化」がCurrent Motor Stateと交互作用 (素値の単純投入は再試行しない・季節proxy混同に厳重注意)",
   "U-30 シナリオ条件付き分布 (Conditional Scenario Distribution) — P(Scenario)×P(Order|Scenario)の2段構造。全体数%でもScenario内中心舟券の情報を捨てない",
   "U-31 意味のある穴 vs 薄い穴 (Meaningful Tail vs Diffuse Tail) — レアScenario内の確率集中で「買える穴」と「ノイズ穴」を区別",
   "U-32 読めるレース (Race Compressibility) — 少数点に真の確率質量を圧縮できるレースが存在する (entropy系指標で識別)",
   "U-33 価値加重シナリオカバレッジ (Value-weighted Scenario Coverage) — 全世界線でなく価値のある世界線だけを複数カバー (NO COVERも正式な選択)",
   "U-34: Course Interaction × Tactical Profile (H-A) — BACKLOG ONLY・SOB1将来窓∧SC2 PASS 後に起票 (Owner 指令 2026-09-09 §6)",
   "U-35: Venue-Specific Adjustment Advantage (H-B) — BACKLOG ONLY・無条件当地特徴は R-6 否定維持 (Owner 指令 2026-09-09 §6)",
   "U-36: Race Formation Sensitivity Map (H-C) — BACKLOG ONLY・設計候補のみ・EXIN1 結果が前提 (Owner 指令 2026-09-09 §6)",
   "U-37: Expert Forecaster Reverse Engineering (H-D) — BACKLOG ONLY・最初の成果物 = Expert Feature Gap Matrix (Owner 指令 2026-09-09 §6)"
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
  "national_fold2_3seed": {
   "nll": 3.7565,
   "hit1": 0.102,
   "tansho_acc": 0.5746
  },
  "market_gap_nll": "+0.06〜0.07 (確定オッズde-vig比・diagnostic)",
  "sg_kiryu_20260830": {
   "head_hits": "9/12",
   "trifecta_top1": "4/12",
   "ai_nll": 0.818,
   "market_nll": 0.981,
   "n": 12,
   "label": "逸話・断定禁止"
  },
  "adoption_line_thin_layer_dnll": 0.003,
  "e10": {
   "externality_variance_T": 10970.5,
   "externality_null_mean": 8703.5,
   "externality_null_sd": 62.3,
   "externality_p": 0.001,
   "pure_externality_p": 0.894,
   "own_diag_sd_pp": "2.9-4.5 (LGB代理の選手スキル取り残し・caveat)",
   "makuri_oos_window": "2025-07-01..2026-06-30",
   "makuri_n_races": 44357,
   "makuri_n_tickets": 354856,
   "makuri_gap": 0.001298,
   "makuri_ci95": [
    0.001053,
    0.001551
   ],
   "makuri_z": 10.22,
   "makuri_relative_miss": "+26.3%",
   "makuri_venues_positive": "22/24",
   "confirmed_signatures": 7,
   "label": "確定は較正の歪み。P2に締切前オッズ無し=買える歪みは未確定",
   "source": "lane-reports/e10_externality_20260904.md"
  },
  "w1_batch_20260904": {
   "n1_lambda_makuri": 0.228,
   "n1_p2_gap_before": 0.001298,
   "n1_p2_gap_after": 0.000166,
   "n1_p2_z_after": 1.3,
   "n1_thin_dnll_fold1": 0.000531,
   "n1_thin_dnll_fold2": 0.001306,
   "i1_thin_dnll_fold2": 0.001078,
   "i1_signature_capture": "7/7 (分布の端)",
   "e1_agreement_rate": 0.992,
   "e1_thin_dnll": "fold1 −0.00055 / fold2 −0.00064 (負=悪化)",
   "e5w_thin_dnll": "fold1 +0.000184 / fold2 +0.000230",
   "e5w_strong_wind_dnll": -0.002174,
   "e23_thin_dnll": "fold1 −0.000506 / fold2 −0.000481 (K=24)",
   "label": "5本とも主ゲートFAIL (採用ライン0.003)。数値の出典は各 lane-report",
   "source": "lane-reports/{i1_proxy,n1_reweight,e1_stage,e5w_wind,e23_utility}_20260904.md"
  },
  "t3d3_20260910": {
   "test": "prod3 2026-07-01〜08-31",
   "lambda": {
    "sanrentan_T1": 0.59,
    "sanrenpuku_T1": 0.5,
    "nirentan_T1": 0.41,
    "nirenpuku_T1": 0.31,
    "tansho_T3": 0.09
   },
   "nll_ai_mkt_blend": {
    "sanrentan": [
     3.739,
     3.688,
     3.684
    ],
    "sanrenpuku": [
     2.298,
     2.293,
     2.276
    ],
    "nirentan": [
     2.515,
     2.512,
     2.489
    ],
    "nirenpuku": [
     1.969,
     1.994,
     1.957
    ],
    "tansho": [
     1.1315,
     1.2914,
     1.1355
    ]
   },
   "S5_hitCR_ai_to_blend": {
    "sanrentan": [
     0.52,
     0.62
    ],
    "sanrenpuku": [
     0.61,
     0.84
    ],
    "nirentan": [
     0.73,
     0.905
    ],
    "nirenpuku": [
     0.72,
     0.86
    ]
   },
   "realized_return_tau115_top3_T1": {
    "sanrentan": 0.64,
    "sanrenpuku": 0.71,
    "nirentan": 0.69,
    "nirenpuku": 0.67
   },
   "bets_per_year_est_tau115_top1": {
    "nirentan": 39750,
    "nirenpuku": 35759
   },
   "case_frozen": "case1_market_gate",
   "case_substantive": "case3-leaning"
  }
 },
 "data_status": {
  "official_bk": "2020〜全国・ほぼ完全 (K結果はレース後公開=ラベル専用)",
  "beforeinfo": "2020〜 (2023-01〜04欠落=素データ自体なし)。全356,476ファイルのフルスキャン実測 (2026-09-04 W2監査・エラー0): チルト充足94-97% (F41未収載=未利用100%)・安定板true率4.5-9.8%/年 (場別分布は物理と整合・2026はopenapi由来で構造的欠測0.6%)・気温98.7%/水温95%。**部品交換列は6.5年間パーサ取り違えで前走成績(同日前走のレース番号)を保存していた=部品交換データは実質未収集** (選手ID照合119/119で確定。正解実装は fetch_beforeinfo_ext.py に既在。前向き修理≈0.5日・過去分は生HTML未保存のため再スクレイプ35万ページ≒12日=Owner GO必須・openapiでは取れない)",
  "era5": "2020〜2026-09 毎時24場 140万行 (気圧/湿度/突風/空気密度)。事後再解析=本番は予報アーカイブ要",
  "odds_preclose": "全国 3連単 2026-07-10〜 (national_v2)・単勝 2026-07-16〜 (national_tan) 蓄積中 (real EV評価はこれのみ)。**2026-09-10 15:45〜 forward collector close_window (24 場・5 券種・D-3:00〜D+10:00・NG-FC1 試験運用) 稼働** = 3連複/2連単/2連複の全国締切前オッズの自前収集開始 (値は 11/1 まで封印)",
  "setsu_master": "全期間5,311節 (artifacts/research/nextgen/setsu_master.parquet)",
  "static_assets": "venue_course_azimuth.json (high19/mid5) / venue_branch_map / motor_exchange_months / venue_latlon / venue_date_grade.parquet (E1副産物・29,715行)",
  "research_assets_w1": "i1_features.parquet (選手×コースas-of行動プロファイル206万行・leak test PASS) / e1_stage_decision_table.csv (8カテゴリ・一致率99.2%) / e5w_features.parquet (風コース成分) / e23 utility.parquet",
  "missing_wishlist": [
   "選手コメント時系列(HIGH)",
   "プロペラ形状(HIGH・困難)",
   "1M映像展開(MED・打ち切り済)",
   "人間関係(MED)",
   "ピット常時(LOW-MED)"
  ],
  "external_gift_20260906": "知人(競艇AI研究者)の研究全量バンドル (data/external/gift_20260906/・gitignore)。2026-09-09 突合済み: G1/G2/G4/G5 一致率 100%・G3 単勝 0.0%/3連単 0.30% (先方 7/23-24 回転バグ補正後) = 突合前ラベル解除。直前板 parquet = _parsed/live_board_odds.parquet (live 6,657R・単勝ページ皆無)。secret 様 8 本未開封。統合報告 lane-reports/gift_investigation_20260909.md",
  "features_v2_research": "2026-09-10 復旧済み: 2026-07-22 以降の as-of 17 列欠損は 08-03 build が 07-21 止まりの extras を left-join したのが原因。rc2 延長 extras + beforeinfo 再スキャンで leakage-safe 復旧 (学習窓バイト同一)。窓 2020-01-01〜2026-08-31 (09-01〜 は封印・11/1 以降に再構築)。旧 = *.gap0722_20260803build.bak",
  "market_panels_ts": "artifacts/research/nextgen/ts/panels/ (2025-07-01〜2026-08-31)。5 券種 A/B/C 分類済み・D なし。3連複/2連単/2連複の全国締切前は先方直前板 T-1 + checkpoint (7/25〜8/1) のみ (自前ゼロ)",
  "close_window_forward_collector": {
   "path": "data/odds_snapshots/close_window/",
   "since": "2026-09-10 15:45 JST",
   "launchd": "com.kyotei-ai.collect-close-window (60 s・KYOTEI_FC_LIVE=1)",
   "pages": "oddstf + odds3t (全 checkpoint) / odds3f + odds2tf (D-3:00, D-1:00, D+3:00, D+6:00 条件付き)",
   "load": "≈3,100 req/日 max (既存比 +11%)",
   "trial": "NG-FC1 2026-09-11〜09-24 メタデータのみ",
   "sealed": "オッズ値は 2026-11-01 まで集計・閲覧禁止",
   "watch": "応答 8〜10 秒/ページ (初回 fire 実測)"
  },
  "shadow_tan_method_A": {
   "script": "scripts/shadow_report_national_tan.py",
   "since": "2026-09-10 (nightly 23:30)",
   "judge": "方式 A: EV_A = AI × 0.75/p3t ≥ 1.15 (監視 ≥1.05)。旧判定 (乖離 ≥0.20) は比較列として維持",
   "log": "data/processed/national/shadow_log_tan.parquet (+7 列)"
  }
 },
 "overfitting_status": {
  "fold_contamination": "fold1/fold2は開発汚染済み=採否の最終根拠にしない",
  "gates": "G0事前登録→G1 2fold一貫+bootstrap CI95→G2 3seed→G3 prod2026窓→G4 ECE→G5 市場(diag/real分離)→G6 8segment",
  "danger_zones": [
   "Player×Course×Stage×Wind等の細分サンプル枯渇 (積項でなく共有表現)",
   "万舟数本集中の利益 (検知をハーネスに組込予定)"
  ],
  "w1_note": "第1波5実験は全て事前登録→凍結→機械判定を完走。バグは全件addendum開示+初回数値破棄で再実行 (I1×1件・N1×2件・E1×1件)。判定ルールの事後変更ゼロ"
 },
 "leakage_status": {
  "defense": "5層 (列名ガード/日付split/集計方向shift(1)/入力由来許可リスト/replay時刻)。本番経路に既知の直接リークなし",
  "known_risks": [
   "同日クロス会場ソート (パッチ済・本番見送り中・新研究は新ソート必須)",
   "Stage/節内集計の同日後レース混入 (day-start規約。E23はT1-T5機械検証で違反ゼロを確認)",
   "気象の確定観測vs締切前 (§51)",
   "選手コメントのレース後混入 (前向き収集のみ可)",
   "**R1気象の終値上書き疑い (2026-09-06 P4設計レーン発見・n=1観察)**: beforeinfoのR1気象だけ「HH:MM現在」=当日終値で上書きされる挙動を実測 — 事実ならR1行の気象特徴は6.5年分look-ahead汚染。R1 vs R2系統差検定で要確認・確認まで新研究のR1気象は要注意扱い",
   "beforeinfoの風はレース単位スタンプで前レース発走時点 (展示より約15分古い) — 「直前風」の実観測はアメダス10分値が上限 (T-1分ラベルは実観測でない)"
  ],
  "unusable_scripts": [
   "real_backtest.py / walk_forward_eval.py (未来漏れ未修正・新研究で流用禁止)"
  ]
 },
 "pending_owner_decisions": [
  {
   "n": 1,
   "item": "live気象修復パッチ (P0)",
   "recommend": "適用",
   "status_20260909": "未裁定のまま持ち越し (Owner 指令 2026-09-09 では言及なし)"
  },
  {
   "n": 2,
   "item": "7/27劣化153件修復",
   "recommend": "適用",
   "status_20260909": "未裁定のまま持ち越し (Owner 指令 2026-09-09 では言及なし)"
  },
  {
   "n": 3,
   "item": "風向16方位パーサ",
   "recommend": "適用",
   "status_20260909": "未裁定のまま持ち越し (Owner 指令 2026-09-09 では言及なし)"
  },
  {
   "n": 4,
   "item": "openapi日次取り込みを夜間ジョブへ",
   "recommend": "追加",
   "status_20260909": "未裁定のまま持ち越し (Owner 指令 2026-09-09 では言及なし)"
  },
  {
   "n": 5,
   "item": "同日ソートキー修正の本番適用",
   "recommend": "見送り (研究ビルドのみ)",
   "status_20260909": "未裁定のまま持ち越し (Owner 指令 2026-09-09 では言及なし)"
  },
  {
   "n": 6,
   "item": "N1 まくり筋較正層の扱い",
   "decision": "GO (Owner 2026-09-04)。Calibration-specific Gate を NG-N1C として新規事前登録済み (①対象セル|z|<2+CI 0跨ぎ ②全体NLL非劣性 ③非対象セル非悪化 ④walk-forward 3期再現 ⑤場別致命的過補正ゼロ ⑥福岡・唐津の主因診断)。NG-N1 の旧判定は変更しない (旧ゲートではFAILのまま保持)。場別λは診断のみ・本番採用せず過学習リスク評価"
  },
  {
   "n": 7,
   "item": "E5W 風の再挑戦方向",
   "decision": "GO (Owner 2026-09-04)。線形2パラメータ形はFAIL固定・同一形再提案禁止。NG-E5NR (Nonlinear Environmental Regime) を事前登録済み — まず「強風でレース生成過程が変わるか」の最小統計PoC (逃げ率/ST/決まり手/まくり率/外艇Top3/展示→本番の分布変化)。巨大interactionモデルの一括実装は禁止。安定板はn小逸話を真実扱いせず新規仮説として扱う"
  },
  {
   "n": 8,
   "item": "E1 格特徴のB2入力側追加+再学習",
   "decision": "DEFER (Owner 2026-09-04)。「レース格は無意味」とは扱わない — 現象 (ST・逃げ率変化) はSUPPORTED・追加予測価値は現B2では薄い (F41から65%再構成可・新情報量薄・再学習コスト大・モデル改造12連敗)。他の新規入力とまとめて再学習するタイミング / architecture revision / Stage Expert の明確な追加証拠が出た場合に再検討"
  },
  {
   "n": 9,
   "item": "rolling/as-of λ によるまくり筋較正の再挑戦",
   "decision": "GO (Owner 2026-09-06・side lane)。NG-N1R として事前登録済み。興味の核=まくり筋歪みそのものの時間変化。旧N1/N1CのFAILは不変。優先度はNG-MS2より下"
  },
  {
   "n": 10,
   "item": "P×R (展開圧力×対応力) Step1-2 ミニPoC",
   "decision": "GO (Owner 2026-09-06)。NG-PXR1 として事前登録済み。固有選手ルール禁止・巨大GAT禁止。受益艇 (Attacker→Affected→Beneficiary) まで3段追跡に拡張。A×B interactionがOOSで残った場合のみpairwise/GAT再評価"
  },
  {
   "n": 11,
   "item": "現在モーター状態の最小特徴化+OOSゲート",
   "decision": "GO (Owner 2026-09-06・Priority 1)。NG-MS2 として事前登録済み。巨大Motor Expertは作らない。特徴候補=節初日状態/当日状態/trend/improvement/volatility/convergence/tilt change/exhibition progression のas-of構成。K由来展示列の誤使用禁止"
  },
  {
   "n": 12,
   "item": "強風regime Phase B (最小regimeモデル・生存16セル対象) の起票可否 — Phase A PASS (逃げ率−10pp/まくり+3.8pp/展示予言力低下が7m/s+で確定)。重要制約: K風=事後観測のため予測特徴化にはT1時点の風ソースが必要 (biは2026のみ)",
   "recommend": "T1風の可用性を先に固めてから起票 (風向パーサ適用済み日次取り込み #4 の蓄積 or bi 2026+のみで小規模検証)。焦って事後風でモデル化しない",
   "status_20260909": "未裁定のまま持ち越し (Owner 指令 2026-09-09 では言及なし)"
  },
  {
   "n": 13,
   "item": "部品交換バックフィルの実施形態",
   "decision": "B案 GO (Owner 2026-09-06)。層化5万ページ (≈7日・節単位サンプリングで交換前後の接続を保証)。目的=部品交換/新ペラ/交換種類/交換前状態/交換後展示・本番/Current Motor State接続の標本確保。Maintenance仮説に実際の増分が確認できた場合のみ全量 (A案48日) を再判断。日次前向き収集のcrontab設置はshin手動のまま"
  },
  {
   "n": 14,
   "item": "単勝 T-3 蓄積の強化 (national_tan の収集窓を締切 4〜2 分へ寄せる launchd 変更)",
   "recommend": "適用 (T3D2 の将来窓・11/1 判定の母数を増やす。boatrace.jp への追加リクエストは同数で窓移動のみ)"
  },
  {
   "n": 15,
   "item": "2023-01-01〜04-24 全場欠落の再取得 (公式 LZH からの可否確認→取得)",
   "recommend": "可否確認まで GO 推奨・取得は別途"
  },
  {
   "n": 16,
   "item": "公開 mirror の git 履歴 / gist 版履歴に残る先方実名の扱い (force push + gist 作り直し)",
   "recommend": "Owner 判断 (危険操作)"
  },
  {
   "n": 17,
   "item": "crontab 3 行 (風コレクタ 2 + 部品日次 1)",
   "recommend": "設置"
  },
  {
   "n": 18,
   "item": "NG-T3D3 起票 (gap 条件付きブレンド・design_t3d3_20260910.md)",
   "recommend": "GO (事前登録→実行。新 NN なし・本番不変)"
  },
  {
   "n": 19,
   "item": "forward collector 実装・launchd 登録 (design v2 + draft + plist draft 完成)",
   "recommend": "GO (2 週間試験。3連複/2連単/2連複ページの追加有無を同時裁定)",
   "status": "裁定済 GO (Owner 指令 2026-09-10 第 2 弾) → 実施済"
  },
  {
   "n": 20,
   "item": "shadow EV 判定を方式 A (3連単含意単勝) へ差し替え (daily_signal_notify.py・本番隣接)",
   "recommend": "GO (持ち越し)",
   "status": "裁定済 GO (Owner 指令 2026-09-10 第 2 弾) → 実施済"
  },
  {
   "n": 21,
   "item": "研究成果の commit + research mirror push (Q-007 e の扱い)",
   "recommend": "GO",
   "status": "裁定済 GO (Owner 指令 2026-09-10 第 2 弾) → 実施済"
  },
  {
   "n": 22,
   "item": "NG-T3D4 起票 = オッズ帯条件付き λ + 判定を『確定配当ベースの実現値 CI 下端 > 1』に置く (実現値が 1 を超えなければケース3 確定・Market Gate 閉鎖)",
   "recommend": "GO (Q-022)"
  },
  {
   "n": 23,
   "item": "forward collector 試験後 (9/24) の checkpoint 確定 (D-0:30/D-0:10 存廃・3f/2tf 継続) と raw HTML gz の削除",
   "recommend": "試験結果を見て裁定 (メタデータのみ)"
  }
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
  "ready_now": [
   "チルト (24場2020-26・充足94-97%・節内変更追跡可・未利用100%)",
   "安定板 (true率4.5-9.8%/年・場別分布が物理と整合・2026年openapi欠測caveat)",
   "展示の未利用粒度 (節内日次推移・スタ展進入変化13.06%=スタブ疑い検証済みシロ)",
   "モーター識別 (場,motor_no,交換年度キー成立・物理11,669機・中央値202走/機)",
   "節マスタ/standing_panel (356,580行/2,059,541行)",
   "気象 ERA5 1,403,136行"
  ],
  "repair_needed": [
   "部品交換: パーサ修正+前向き収集=小(≈0.5日・fetch_beforeinfo_ext.pyの正解実装を移植)。過去分バックフィル=大(再スクレイプ35万ページ≒12日・Owner GO必須)"
  ],
  "acquisition_needed": [
   "新ペラフラグ (beforeinfoページに列は実在→部品交換修理に相乗り可)",
   "選手・調整コメント (手元に無し・前向きのみ・fetched_at付きingest guard設計)"
  ],
  "leakage_top3": [
   "features.parquetの展示/進入/ST/気象はK(レース後)由来 — 新規Motor研究が素で読むと即事故。beforeinfo由来へ張替え必須",
   "national buildの同日ソート順欠陥 — 節内Motor State等の同日集計の前に研究ビルドのソートキー修正が前提",
   "2026年のソース断層 (openapi: 部品/安定板欠測) — 年×ソース交絡につき_sourceフラグ伝搬必須"
  ],
  "w2_priority_proposal": [
   {
    "rank": 1,
    "id": "NG-N1C",
    "why": "登録済・実装ゼロに近い・唯一のOOS確定歪みの回収。即実行可",
    "eig": "高/コスト極小"
   },
   {
    "rank": 2,
    "id": "W2-A Motor Current State PoC",
    "why": "未利用100%のチルト+展示節内推移+安定板+モーター識別が全部「今すぐ使える」。as-ofはbeforeinfo由来で清潔。B2重複は成績3本+展示z9本のみ",
    "eig": "高"
   },
   {
    "rank": 3,
    "id": "W2-B 部品交換パーサ修理+前向き収集開始",
    "why": "≈0.5日で資産が毎日積み上がり始める (待つほど損)。分析自体は蓄積後orバックフィルGO後",
    "eig": "高(遅延回収)/コスト極小"
   },
   {
    "rank": 4,
    "id": "NG-E5NR Phase A",
    "why": "登録済・統計PoCのみでコスト小。安定板データ準備完了",
    "eig": "中〜高"
   },
   {
    "rank": 5,
    "id": "W2-C Player Adjustment Skill",
    "why": "W2-Aの産物 (motor state panel) に依存するため後続。partial pooling前提",
    "eig": "中〜高"
   }
  ],
  "deferred_candidates": {
   "D": "Setup Confidence — コメント前向き収集の蓄積待ち (チルト変更・展示volatility部分は W2-A に内包)",
   "F": "Local×難水面 — E8SWAP着手条件のまま",
   "G": "Dynamic Player Trajectory — I1教訓によりsegment評価設計を先に固めてから",
   "H": "Market Recognition Lag — 締切前オッズ蓄積+holdout解封 (11/1) 後"
  }
 },
 "w2_directives_owner_20260905": {
  "status": "W2正式GO + 次期研究思想の統合 (Owner全文指示 2026-09-05)。全テーマは 観察→一般仮説→最小統計PoC→OOS再現→予測価値→市場価値→必要ならArchitecture投資 の順で扱う",
  "confirmed_order": [
   "並行: NG-N1C (まくり筋較正最終検証・旧N1のFAIL判定は不変)",
   "並行: 部品交換パーサ修理+前向き収集 (分析でなくデータ資産・即実施。誤パース列の再利用は絶対禁止。取得=部品交換/新ペラ/交換種類/fetched_at/source/race_id/racer_id/motor identity/as-of保証metadata)",
   "次: Current Motor State PoC (「元々強いモーターか」でなく「この選手がこの節で調整した結果、今この時点でどういう状態か」のas-of推定。features.parquetのK由来列は直接流用禁止=beforeinfo由来as-ofへ張替え必須)",
   "その後: NG-E5NR Phase A (強風regime)",
   "その後: Player Adjustment Skill"
  ],
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
  "new_themes_registered_as_hypotheses": [
   "1. Generalized Pressure×Resistance (展開圧力×対応力)",
   "2. Course-conditioned Matchup Skill (コース条件付き相性)",
   "3. Interaction propagation / beneficiary effect (波及と受益艇)",
   "4. Known-but-underweighted market information",
   "5. Conditional interaction mispricing",
   "6. Second-order beneficiary mispricing",
   "7. Scenario-aware betting portfolio (シナリオ分散買い)",
   "8. Robust EV + downside-aware optimization"
  ],
  "console_rule": "Research Mirror/Artifactは内部IDだけで説明しない。各研究に日本語一言名+何を調べる/なぜ重要/今何が分かった/次に何を/市場エッジとの関係 をスマホで読める形で。内部IDは括弧内の補助",
  "discipline": "post-hoc閾値変更禁止 / holdout汚染禁止 / leakage禁止 / small-n断定禁止 / closing oddsをreal EV扱いしない / fundamental predictionにオッズ非入力 / FAIL書き換え禁止 / PoC前の巨大Architecture禁止 / Model improvementとMarket edgeの混同禁止 / NO BET=first-class decision"
 },
 "w2_directives_owner_20260906": {
  "vision": "読めるレースを識別し、複数の展開世界を条件付きで理解し、市場価格に対して価値のある世界線だけを少数点で買うAI (Current State → Interaction → Scenario → Market → Portfolio)",
  "priorities": [
   "P1: 現在モーター状態の最小特徴化+OOS実モデル試験 (NG-MS2。巨大Motor Expert禁止。K由来展示列の誤使用禁止)",
   "P2: 展開圧力×対応力ミニPoC (NG-PXR1。固有選手ルール禁止・受益艇まで3段追跡)",
   "P3: 部品交換 層化5万ページバックフィル (Maintenance仮説の増分確認後のみ全量再判断)",
   "P4: リアルタイム風取得基盤+展示→締切の風変化PoC設計 (展示時/締切15/10/5/3/1分前のtimestamp付き収集設計)",
   "P5: 調整能力×現在モーター状態の統合設計 (Initial State×Adjustment Skill×Interventions×Meet Progression→Current State。「調整能力が高いから強い」の単純特徴は禁止)",
   "side: rolling λ (NG-N1R・優先度はP1より下)"
  ],
  "no_big_build": [
   "Scenario Generator大型モデル",
   "GAT",
   "Learned Race Simulator",
   "Environment Expert",
   "Portfolio Optimizer本番化 — いずれも研究設計・データ準備・最小PoCまで"
  ],
  "wind_state": "風は「強さ」でなく「変動」も: 平均/風向/成分/展示時からの差/直近trend/SD/max-min/gust/風向変化量/regime transition/安定性。核仮説=展示時と本番直前の風が異なるほど展示ST・展示性能の本番予測力が低下する。平均5m安定日と2-9m往復日を同一扱いしない。Player Wind Adaptation (風変化への適応の選手差) は仮説保存→ST誤差・分散の再現可能な選手差をas-of+shrinkageで確認してから",
  "environment_x_motor": "気温/気圧/湿度/空気密度/水温/気温−水温差/前日差/節初日差/展示時差。主眼は絶対値でなく「環境が変化した時にどのモーター状態がどう反応するか」(Environment×Motor交互作用)。素値の単純投入は再試行しない (棄却済み)。季節・場proxyとの混同に厳重注意 (季節クリマトロジープラセボ標準)",
  "scenario_structure": "将来的にP(Scenario)×P(Trifecta|Scenario)の2段構造を研究 (例: 1逃げ安定55%/3攻め1凌ぎ22%/3攻め2抵抗内崩れ12%/3攻め完全成功7%)。全体では数%の舟券でも特定Scenario内では中心舟券という情報を捨てない。120通りsoftmaxは捨てない — 当面は併存 (decomposition/explanation)。Scenario ModelがOOSで予測改善を示した場合のみRace Simulator/mixture検討",
  "meaningful_vs_diffuse_tail": "Meaningful Tail=レアScenario内で少数舟券に確率集中 / Diffuse Tail=Scenario内でも分散。区別の表現候補=Scenario Probability/Conditional Concentration/Scenario Entropy/contingent events数",
  "readability": "Race Readability/Compressibility を研究: 1着確率集中度/Head entropy/Conditional 2nd・3rd entropy/Scenario entropy/Epistemic uncertainty/Required ticket count から「少数世界線に圧縮できるレース」を識別",
  "new_metrics": "NLL/Hit@1に追加: Head Accuracy by Confidence Bucket (50-60/60-70/70-80/80%+) / Conditional 2nd Coverage (頭固定で上位1-2艇の2着カバー率) / Conditional 3rd Coverage / Minimum Ticket Set (確率質量50/70/80/90%に要る点数) / Realized Hit Rate of Minimum Set",
  "hit_rate_policy": "「読めるレース限定で3連単ポートフォリオを3回に1回」はOwnerの作業仮説であってハード目標ではない。33%達成のためにモデルを歪めることは禁止。研究するのは「確信度の高いサブセット+3-6点で的中率がどこまで上がるか」のconfidence bucket別評価。当てることと儲かることは必ず分離 (Predictability→Compressibility→Market Price→Robust EV→Portfolioの順)",
  "portfolio_principles": "Sparse必須 (同等のEV/リスクなら9点より3点)。追加舟券には十分なRobust EV or 有意なScenario Diversification Benefitを要求。「万が一のため100円追加」の常態化禁止。全Scenario保険買い禁止。目標=Value-weighted Scenario Coverage (買う価値のある世界線だけカバー・価値が無ければNO COVER)",
  "tail_scenario_gate_7": "穴世界線をPortfolioへ追加する事前Gate候補: ①Scenario Probabilityが極端に小さくない ②Scenario内で少数舟券に集中 ③市場に対するEdge ④Robust EVでも成立 ⑤既存Portfolioと異なるScenario exposure ⑥追加資金に対するDownside改善 ⑦Portfolio全体のEVを壊さない — バックテスト前に定義を凍結",
  "market_focus": "Known-but-underweighted / Conditional interaction mispricing / Beneficiary mispricing / **Rare Scenario mispricing** (市場も「3が攻める」は知っているが、その場合に5が浮上する条件付き確率まで正確に価格化していない歪み)。締切前オッズholdoutの封印は絶対に破らない",
  "architecture_vision_20260906": "Historical Player/Motor → Current Motor State → Current Environment State → Player Adjustment/Environmental Adaptation → 6艇Current State → Pressure×Resistance → Scenario Generator → P(Scenario)+P(Order|Scenario) → 120通りFundamental Probability → Calibration/Uncertainty → Market Evaluation → Scenario×Ticket Payoff → Sparse Value-weighted Portfolio → BET/NO BET。概念であり一括実装禁止",
  "human_facing": "日本語名称を主表示 (現在モーター状態/選手の調整能力/直前風変化/展開圧力×対応力/穴シナリオ/読めるレース/シナリオ分散買い)。内部IDは括弧の補助"
 },
 "next_actions": [
  "Owner GO 事項 (次の 1 手): NG-T3D4 起票 = オッズ帯条件付き λ (+1〜2 パラメータ・新 NN なし) を事前登録し、判定を『確定配当ベースの実現値 CI 下端 > 1』に置く。全滅ならケース3 確定 = Market Gate を閉じて 11/1 開封と forward collector の締切直前価格を待つ",
  "自律 (メタデータのみ): forward collector 試験 9/11〜9/24 — D-0:30/D-0:10 存廃・odds3f/odds2tf parse 成功率・失敗処理実地・応答 8〜10 秒/ページの原因 (IPv6 フォールバック疑い = 仮説)。checkpoint 確定は Owner",
  "自律 (読み取り・設計のみ): 部品バックフィル完走 (9/16 目安) 後の Maintenance 最小イベントスタディ設計 / 11/1 holdout 開封手順の事前整理 / Historical Replay 最小試作 (8 h) は T3D4 の後・Owner GO",
  "P3 (Owner GO): SOB1 将来窓再現 / 小さい SC2 (優先度低)。BACKLOG ONLY: H-A〜H-D",
  "禁止維持: 大型 Scenario Generator / GAT / Race Simulator / 券種専用 NN・券種専用特徴・巨大 calibration network / 拡連複・複勝 / 展示入力側化 / バックフィル停止・再起動・35 万拡張 / holdout 9/1〜10/31 閲覧 (forward collector の値も) / test 窓を見てからの τ・候補・窓の変更"
 ]
}
```


# ===== OWNER_DIRECTIVE_20260909.md =====

# Owner 研究指令 2026-09-09 — 「予測できる」から「実際に買える」へ

- 受領: 2026-09-09 23:10 JST(Discord / claude code 経由・shin)
- 位置づけ: DECISION_LOG の GO 根拠。実行記録 = NEXT_ACTIONS.md / registry NG-T3D2・NG-EXIN1 / lane-reports/t3d2_*・exin1_*・p3_designs_*
- 本文(原文どおり・要約なし)

---

目的: 研究を「予測できる」から「実際に買える」に進める。

まず canonical research state、NEXT_ACTIONS、DECISION_LOG、DATA_STATUS、FINDINGS、experiment registry を読み、現状を自分で再確認。RESEARCH_MIRROR.md は表示用であり、正本との食い違いがあれば正本を優先。

今回の最重要目的 = 締切前に利用可能な情報だけで確率と実際に執行可能な価格を評価し、BET / NO BET を決められる状態へ近づけること。新しいモデルを無制限に作ることではない。

## 0. 最初に状態整合性を修正
mirror の機械生成サマリの Research Queue と最新 NEXT_ACTIONS に古い記述が混在している可能性。完了済み実験 / current experiment / 自走中ジョブ / Owner 判断待ち / 次の優先順位を整合させる。現時点の認識: ①知人バンドル突合 G1-G5 = 完了・PASS ②T-3 drift 追試 = 完了 ③Current Motor State の本番昇格 = FAIL_STACKED ④production = b2f41_prod2026_prod3 のまま ⑤部品層化バックフィル = 自走中 ⑥次の主戦線 = EV 判定実効化 → 当日展示入力側化 ⑦market holdout 2026-09-01〜10-31 は絶対に開封しない。正本と違う場合は正本に従い差を報告。

## 1. 最優先: EV 判定を「実際に買える価格」に変える(NG-T3D2 = Executable EV / Closing Price Proxy)
NG-T3D1: fire 単勝の選択時→締切時 odds ratio ≈0.47〜0.67(対照 ≈1.0)、見かけ EV ≈2.83、実現値 ≈0.82。「選択時に割安」と「その価格で買える」は別問題。比較する基本 3 案:
- A. 3連単市場から作る含意単勝価格(120 通りから艇ごとの 1 着含意確率。de-vig を明示)
- B. Drift-adjusted price(time-to-close / 現在オッズ帯 / fire・non-fire / 必要なら pool・venue の少数変数 shrunk/simple model。巨大 ML 禁止・過学習防止優先)
- C. Late execution(締切直前まで待つ。候補 T-30 秒。歴史データに無ければ捏造・補間せず historical test 可能範囲と forward collector / shadow 運用に分離)

## 2. T3D2 で本当に知りたい指標
「T-3 時点で EV ありと判定したものが締切価格でも本当に EV ありだったか」を primary の一つに。closing price prediction error / EV sign survival / EV>1.05・1.10・1.15 survival / false-positive rate / predicted EV vs executable EV / selection count / calibration / realized return(条件を満たす場合のみ)/ bootstrap CI。閾値は事前登録。「EV が高く見えるものほど締切までに潰れる」selection-induced drift の有無を確認。

## 3. 最終商品は 3連単
知人バンドルの 3連単締切前系列が突合 PASS なので、モデルが選んだ 3連単舟券の T-3 価格 → pre-close/final 価格の drift も調べる。区分は事前固定: 通常帯 / 60〜150 倍 / 150〜300 倍。薄い区分は断定禁止。1000 倍等の Extreme Tail を細分しない。

## 4. 次点: 当日展示を NN の入力側へ(NG-EXIN1)
問い: 当日展示を後段の薄い補正として使う現在方式より、6 艇 self-attention に入れて「他艇との相対状態」まで学習させる方が強いか。arm: A 現 production 相当(F41 NN + exh120)/ B 展示入力側(F41 + 当日展示特徴 → B2)/ C 展示入力側 + exh120。巨大アーキテクチャ変更禁止・B2 固定。入力候補は展示タイム・展示 ST・F・安全確認済みの相対/z 表現から。

## 5. EXIN1 で確認したい本質
NLL だけでなく「展開」が読めるようになったか(1 号艇状態悪化時の他艇 probability shift / センター艇展示上昇時の隣接艇 shift / 4→5 等の二次受益 / entropy・top6 mass 変化)。既存 B2 attention が展示を与えれば相互作用を吸収できるかのテスト。吸収できるなら GAT 等を再び作る理由はない。

## 6. 新仮説の正式保存(Hypothesis / Design Backlog・T3D2/EXIN1 より先に実験しない)
- H-A Course Interaction × Tactical Profile(研究単位を Racer A × Racer B から コース構造 × 攻め手の戦術特性 × 受け手/受益艇の戦術特性 へ。個人ペア固有効果の再研究ではない。SOB1 将来窓と接続)
- H-B Venue-Specific Adjustment Advantage(「地元だから強い」ではない。無条件の当地特徴はデッドウェイトを維持。特定水面への習熟が特定条件での調整・操縦能力を高めるか = Venue familiarity × Player adjustment skill × Environment difficulty × Course。hierarchical shrinkage)
- H-C Race Formation Factor Map(天候 × モーター/現在艇状態 × 選手 × 水面/会場 × コース + 6 艇配置。巨大モデルは作らず Race Formation Sensitivity Map として設計候補)
- H-D Expert Forecaster Reverse Engineering(上手い人間の買い目コピーではなく、何を観測しどこで一般客と判断を分けているかの逆解析。事前予想→展示後の変更理由。最初の成果物 = Expert Feature Gap Matrix)

## 7. SC2 / SOB1
大型 Scenario Generator は禁止維持。T3D2 / EXIN1 の後に「小さい SC2」と「SOB1 future-window reproduction」として回収。両方再現して初めて Course Interaction × Tactical Profile へ。

## 8. Readability
読める ≠ 儲かる は確定。利益シグナルとして扱わない。使い道は race selection / probability compression / portfolio size / confidence 表示に限定。holdout ルールを破らない。

## 9. 部品バックフィル
そのまま自走継続。停止・再起動・全量 35 万ページへ拡張しない。5 万ページ PoC 完走後、Maintenance/parts が当日展示を超えて増分を持つか最小イベントスタディ。増分が無ければ全量取得しない。

## 10. 市場 holdout 絶対規律
2026-09-01〜10-31 は封印維持。集計しない・グラフを見ない・fire 数を確認しない・閾値調整に使わない・「参考だけ見る」も禁止。T3D2 の開発窓は 2026-08-31 以前だけ。11/1 に凍結した判定ルールをそのまま適用。

## 11. 実行順
P0 canonical state / mirror 整合 → P1 NG-T3D2 → P2 NG-EXIN1(P1/P2 独立なら並行可)→ P3 SC2 / SOB1 future validation の具体設計 → BACKLOG ONLY(H-A〜H-D)。部品バックフィルは別レーンで継続。

## 12. 研究を無限化しないルール
新仮説を発見しても今の実験を中断して即実装しない。まず backlog へ。各候補は Probability accuracy / Race selection・readability / Market mispricing discovery / Executable profit・risk のどれを改善する仮説か明記。どれにも該当しない研究は優先しない。

## 13. 人間向け表示
研究終了時、Owner が 5 分で状況を理解できる最新表示: 今何が分かったか / それで何が変わったか / 儲けるまで何が足りないか / 今動いているもの / 次の 1 手 / Backlog に送った面白い仮説 / 棄却済みで再研究しないもの。内部 experiment ID だけを並べない(例: 「NG-T3D1 PASS」ではなく「T-3 で割安に見えた艇は締切までに価格が約半分へ縮むことが再現した。したがって現在表示オッズによる EV 判定はそのままでは使えない」)。

## 14. Owner へ返す内容
①今回何を実行したか ②PASS / FAIL ③予測 AI 自体は強くなったか ④実際に買える EV へ近づいたか ⑤production 変更の有無 ⑥次にやるべきことを 1 つ ⑦Owner の手作業が必要なら具体的なコマンド/操作。

最終ゴール: 未来の未見レースで、締切前に固定したルールだけを使って、実際に取得可能なオッズで BET / NO BET を決め、資金を増やせるかを判定すること。



# ===== GIFT_INVESTIGATION_20260909.md =====

# 知り合いバンドル 調査統合報告 — 2026-09-09

> GitHub 用コピー(原本 = ローカル `lane-reports/gift_investigation_20260909.md`・同一内容)。lane-reports/ は機微情報を含み得るため git 不管理の方針(.gitignore)なので、統合報告のみ research/ 直下に置く(research/reports/ も ignore 対象だったため)。詳細レーン報告 6 本はローカル参照。


- 依頼: shin「もらった研究データをしっかり調査して GitHub に報告」(2026-09-09)。裁定 = 範囲 C(突合 G1-G5 + T-3 ドリフト追試)/ private 全文 + 公開 mirror は匿名要約 / 実名なし / 完了時 commit+push
- 対象: `data/external/gift_20260906/`(バンドル1 = 構造化データ+研究ノート 666MB・1,878 ファイル / バンドル2 = 生 HTML 11GB・348,822 ファイル)。9/6 の棚卸し 2 本(gift_bundle_audit / gift2_bundle_audit)の続き
- 体制: L1 + background agent 5 レーン並列(GA 突合 G1/2/4/5+G6 / GB 突合 G3 / P 直前板 parse / K 知見カタログ / D T-3 追試)。session_clock tag `gift_20260909`
- 遵守: バンドル read-only(書込は `_parsed/` と artifacts のみ)/ secret 様ファイル(名前照合 8 本)未開封 / 2026-09-01 以降のオッズ(holdout 封印)不使用 / 本番(models・bet_log 4 本・cron・既存 script)不変 / ネットワーク不使用 / 先方の実名は新規成果物に書かない
- 用語: **突合ゲート** = 先方の値とうちの値を同キーで突き合わせた一致率 / **T-3** = 締切 3 分前 / **ドリフト比** = 締切時オッズ ÷ 選択時オッズ(1 未満 = 縮んだ)

## 1. 結論 3 行

1. **先方の構造化データは「うちと同じ値」**。突合 5 ゲート全 PASS(G1/G2/G4/G5 = 1,000 件一致率 100%、G3 締切前時系列 = 単勝 0.0%・3連単 0.30%)。ただし G3 は先方 7/23〜24 の 3連単ラベル回転バグ(先方の罠集にある「row-major 反転」の実物)を補正することが条件。「突合前」ラベルは解除。
2. **過去データとしての新規性は低い**(レース結果・出走表・展示はうちの全国 24 場 2020〜 と同値・同範囲。2023-01〜04 の穴は先方も空)。**価値は「締切前オッズ」と「研究ノート」に集中**: 締切前オッズ 3 系統(10 日分の多時点 / 締切 1 分前の板 6,657 レース / 住之江 当日 2 時点)はうちに無い時点。
3. **T-3 ドリフト追試(NG-T3D1)**: 「選んだ単勝は締切までに約半分に縮む」は**うちのデータで再現(H1 PASS)**: fire 買い目 41 本のドリフト比中央値 0.47〜0.67(設計別)で、先方申告 0.446 は CI 内。見かけの EV 2.83 に対し実現値 0.82(H3 PASS)。**EV+15% 運用の「選択時オッズ」は最終まで持たない**。時間単調性(H2)は検出力不足で判定不能、「締切時オッズは常に払戻より高い」(H4)は不支持。

## 2. 突合ゲート結果(NG-GIFTG・全 PASS)

| Gate | 突合ペア | 共通キー | 抽出 n | 一致率 | 判定 |
|---|---|---|---|---|---|
| G1 | 払戻(住之江・4 券種)× うちの確定払戻 | 19,631 | 1,000 | 100%(人気順も 100%) | PASS |
| G2 | 締切時 3連単オッズ(住之江 36R)× うちの歴史オッズ | 4,260 | 1,000 | 100% | PASS(母数小) |
| G3 | 締切前時系列(23 場・7/23〜8/1)× うちの national_v2 / timeseries(±120 秒最近傍) | 3連単 195,960 組 / 単勝 1,502 艇 | 全件 | 単勝 中央値 0.0% / 3連単 全日 2.97% → 7/23〜24 回転補正で 0.30% | PASS(条件付き) |
| G4 | 出走艇(登録番号・全国勝率・モーター)× うちの racers_program | 125,221 | 1,000 | 3 項目とも 100% | PASS |
| G5 | 展示タイム・チルト(住之江)× うちの beforeinfo | 28,345 / 13,445 | 各 1,000 | 100% / 100% | PASS |

- G3 の FAIL 原因は先方側に限定: 7/23〜24 は先方 (1着,2着,3着) → うち (3着,1着,2着) の読み替えで一致(うちの確定払戻を審判にした払戻アンカー診断で先方側と特定・仮説: 先方が 7/25 にパーサ修正)。補正は `scripts/research/nextgen/gift_gate_g3.py` に実装済み。
- 締切時刻の一致率 98.8%(1,254/1,269)。系統的な時間ラグは両側なし。
- 副産物(両側で再現): 「勝ち組の締切時 3連単オッズ×100 > 確定払戻」がうち 1.88%(133/7,078)・先方 2.07%・逆方向 0。先方申告の「最大 +5.7 倍」は再現せず(極端値は返還レース由来の仮説)。
- caveat: G2 は住之江 36 レース分のみ(先方オッズの 9 割は江戸川で、うちに江戸川オッズが無く未検証)。G5 チルトは 2024-04 以降のみ。単勝 G3 は 65 レースと薄い。

## 3. 「過去データは拾えたか / 使えるか」の判定

| 資産 | 判定 | 根拠 |
|---|---|---|
| レース結果・払戻・出走表・展示(住之江 5 年 / 江戸川 5 年 / 桐生) | **うちと同値・同範囲 = 取り込み不要** | G1/G4/G5 100%。江戸川もうちの national に既存 |
| 2023-01〜04 の欠落補完 | **不可** | バンドル2 raw/parsed の同窓 62 日は全て空ディレクトリ(G6)。江戸川のみ先方 boats 約 722 レース分が候補 |
| 締切前オッズ ① 10 日分の多時点(23 場・単勝あり) | **使える(G3 PASS)** | T-3 追試の phase 2 で使用。24 場全艇の締切時単勝(final_win_odds)はうちに無い資産 |
| 締切前オッズ ② 締切 1 分前の板(24 場・2026-04-26〜08-31・live 6,657R) | **使える(parquet 化済み)** | 先方パーサと 3連単 120 組 100% 一致。**単勝ページは先方収集に皆無(0/17,450)** → 単勝は 3連単からの含意で代用。うちの national_v2 と同一レース 3,458R(7/10〜8/31) |
| 締切前オッズ ③ 住之江 当日 2 時点(6.4 万行) | 参考(未使用) | 52% がレース後バックフィルで、当日行のみ可 |
| 部品交換(住之江 5 年) | 薄い | 非空 1,475/28,393。うちのバックフィル(再開済み)が本命 |
| 研究ノート 134 本 + verdict | **使える(コスト 0)** | §5 |
| 予想評価ログ・特徴量・ポインタ JSON・合成疑いのオッズ | 使わない | 9/6 棚卸しどおり |

## 4. T-3 ドリフト追試(NG-T3D1)

### 4.1 結論

先方の主張「EV ルールで選んだ単勝は締切までに約半分に縮む」は**再現(H1 PASS)**。見かけ EV と実現値の差も先方の方向(H3 PASS)。「残り時間に単調」(H2)は検出力不足で判定不能、「締切時オッズは常に払戻より高い」(H4)は不支持(取得時刻の定義差で説明でき、締切前の表示値は払戻と上下対称)。事前登録→凍結→機械判定(phase 1 = `t3_drift_frozen.json`、phase 2 = `t3_drift_phase2_frozen.json`)。凍結後の基準変更ゼロ(H4 の addendum 1 件は元判定を維持)。

### 4.2 判定表

| 仮説 | 判定 | 主要数値(n・CI95) |
|---|---|---|
| H1 選択バイアス(fire の drift < 同オッズ帯の対照) | **PASS** | phase 1(2 場全艇): fire 41 本 中央値 **0.526** [0.43, 0.65](対照 3,134・placebo p=0.000)/ 24 場勝者 0.417 [0.39, 0.45](182)。phase 2(先方 final 全艇 910R): T-3 0.667 [0.48, 0.81](fire 41 / 対照 2,335・対照全体 0.984)/ T-3 で再判定 0.569 [0.36, 0.75](28)/ T-5 0.474 [0.39, 0.74](41) |
| H2 時間単調性 | **INCONCLUSIVE** | 各時点で fire 再判定した drift 比(その時点÷final)の帯別中央値 1.76(締切 0〜0.5 分前)〜2.34(4〜6.5 分前)・ρ +0.09 [−0.06, +0.25](271 観測 / 59R)。fire 艇の軌跡(選択 = 6 分前)は締切直前 1.16 → 4〜6.5 分前 2.11 で単調 ρ +0.27 [0.12, 0.40] だが選択時点条件付き |
| H3 実効 EV(見かけ vs 実現) | **PASS** | fire 534 本: 見かけ EV 2.83 vs 実現 0.819 [0.70, 0.95] → gap 3.46 [2.97, 4.10]。勝者の VR(選択時÷締切時)中央値 2.40・縮んだ割合 92.9% |
| H4 「締切時オッズ ≠ 払戻」 | 先方定式は**不支持**・事実関係は整合 | 締切後に凍結した表示値 = 払戻 99.3%(575)/ 先方 final(締切 17.4 分後取得)= 払戻 100%(910)。締切前の表示値は払戻と不一致だが上下対称(page>payout 41〜45% / page<payout 46〜48%) |

### 4.3 先方申告との対応

| 先方申告(突合前) | うちの追試 |
|---|---|
| drift 比 0.446(22/22 レース) | T-5 0.474 / T-3 再判定 0.569 / 2 場全艇 0.526 / 勝者 0.417 → いずれも CI が 0.446 を含む(整合)。T-3 logged 0.667 は選択(6.3 分前)〜T-3 で既に一部縮んでいるため大きめ |
| 締切 2 分前 1.14 / 20 分超 1.81 の単調性 | 先方定式化では 1.92 / 1.84 で単調でない。fire 艇を締切直前に見ると 1.16(先方の 1.14 に相当・仮説: 先方の数字は「先に選んだ買い目を締切間際に見た比」) |
| 実効損益分岐 VR ≥ 2.2 | 方向一致。T-3 anchor 3.31 [2.17, 5.37](77) |
| 締切時オッズは常にページ値 > 払戻 | 不支持(対称)。先方自身の final は締切 17.4 分後の取得で払戻と 100% 一致 |

### 4.4 含意(事後診断・判定には未使用)

- 表示単勝は締切直前に激しく振れる(例: 1.8 倍の本命が 2 分前に 14.1 倍表示 → 確定 2.1 倍。overround 正常・別 parser 同値 = 実表示)。fire は「薄い単勝プールが一時的に過小評価した艇」を拾い、締切間際の大量投票で AI 側に寄る。スパイク以外の fire 勝者も 0.437 に縮むので、選択バイアスはスパイクだけでは説明できない
- 3連単から作った含意単勝(深いプール)では、締切 1 分前に fire の縮みが既に完了(T-1 含意 ÷ 選択時表示 = 0.445 [0.40, 0.47] vs 対照 0.889。払戻 ÷ T-1 含意は 1.056 で対照と差なし)。**仮説: fire 乖離の大半は「薄い単勝板 vs 深い 3連単プール」の差**。AI 確率が間違っているのではなく(的中率 34% は AI 確率 0.41 と大きく矛盾しない)、「選択時オッズが最終まで持たない」ことが問題
- したがって EV 判定は「選択時の表示単勝」でなく「締切時に持つオッズ」で行う必要がある(§7 #1)

### 4.5 caveat

- fire∧T-3∧final は 41 本(先方期間 10 日・final 910/1,596R)。うちの単勝 T-3 帯(national_tan)は 607R と薄い。H2 主集合は検出力不足
- 含意単勝の代理は FAIL(先方実単勝との相対差中央値 0.376)なので P2-4 の 3 点系列は参考値
- **ROI の良否は主張しない**(実効 EV の「比較」のみ)。holdout 封印(9/1 以降)未接触
- 出典: `lane-reports/gift_t3_drift_phase1_20260909.md` / `gift_t3_drift_phase2_20260909.md` / registry NG-T3D1

## 5. 研究ノートのカタログ(Lane K)

- 全 161 行(memory 128 + suminoe_docs 21 + bwev_docs 11)。種別: finding 105 / ops 46 / doctrine 6 / data_trap 4。先方の判定: 該当なし 60 / 未判定 54 / PASS 27(ほぼ手法 PASS、edge PASS は実質 1 件)/ NO_EDGE 17 / FAIL 3
- 上位 10 件(うちに効く順): ① T-3 ドリフト 0.446(本報告 §4 で追試)② 締切時オッズ≠実払戻(§2 で両側再現)③ 過去アーカイブに締切前オッズなし(うちの national_v2 が独自資産である裏付け)④ 単勝 cross-market エッジ(先方唯一の maxT 通過候補・ただし T-3 実行は先方自身が未確認)⑤ データ罠集 ⑥ 研究 doctrine(maxT 必須・パリミュチュエル 33% 縮約)⑦ 2連複の生存候補(未完成凍結)⑧ venue path 混入バグの発見経緯 ⑨ 研究アーク統合サマリ ⑩ 本番シグナル UI の運用仕様
- **データ罠集 11 件をうちのパーサに当てた結果**: 5 件は構造的に防御済み。**「entry_course の枠番コピー」と同一症状を、うちも `approach` フィールドで 2026-07-26 まで踏んでいた**(約 4,000 レース収集後に発覚・修正済み・再発防止テスト未整備)。no-data シェル検知と「締切時オッズ≠払戻」は部分的緩和で要フォロー
- 矛盾リスト: 明確な矛盾なし(favorite-longshot 方向は一致)。要確認 2 件(先方の「1 号艇買い得説」が ROI 主張を含むか / 階級棄却の趣旨)
- 成果物: `artifacts/research/nextgen/gift_audit/knowledge/catalog.csv` / `data_traps.md` / `lane-reports/gift_knowledge_catalog_20260909.md`

## 6. うち側の発見(バンドル調査の副産物)

1. **2023-01-01〜04-24 の欠落は beforeinfo だけでなく national/races_program・payouts・results も全場ゼロ**(参考: 2022 年同窓は桐生 732 / 江戸川 672 / 住之江 816 レース)。過去実験の学習窓・grade 表の「上流欠落」はこれが原因。再取得は公式 LZH から可能か要確認(shin GO 事項)
2. 住之江 payouts に 2026-04-25・05-06・07-05 の 3 日欠落(G1 未一致 35 レースの正体)
3. 単勝の締切前オッズは `data/odds_snapshots/national_tan/`(2026-07-16〜)に別収集されている(national_v2 は 3連単のみ)。T-3 帯(2.5〜4 分前)のスナップショットがあるのは 607 レースと薄く、T-3 と T-2 の両方があるレースは 0
4. national_v2 の欠損: 9/7(2 ファイル)・9/9(0 ファイル)= iMac の IPv4 断(9/9 19:11 再起動で復旧)。部品バックフィルも同原因で 9/6 15:09 に停止していた → 9/9 22:15 に再開(PID 12667)
5. 公開 mirror(GitHub + gist)に 9/6 01:17 以降、先方の実名が 1 箇所含まれていた(research_state.json のバンドル説明が機械生成で流れていた)。正本側を匿名化済み・本報告の同期で公開側から消える。**git 履歴と gist の版履歴には残る**(消すには公開 repo の履歴書き換え = force push・gist は削除再作成。実施は shin 判断)

## 7. 次のアクション候補(Owner 判断・番号で返せる形)

| # | 内容 | AI 推奨 |
|---|---|---|
| 1 | **EV 判定の実効化(NG-T3D2 起票)**: 選択時の表示単勝でなく「締切時に持つオッズ」で判定する。案 A = 3連単含意単勝(深いプール)で判定 / 案 B = 表示単勝に drift 係数(fire 帯 0.45〜0.67)を掛ける / 案 C = 執行を締切 30 秒前へ(それでも 16% 縮む)。事前登録ゲートで A/B/C を比較 | **Yes・最優先**(EV+15% 運用の実効性を直撃) |
| 2 | NG-EXIN1 起票(当日展示の入力側化・W3 からの継続) | Yes |
| 3 | 単勝 T-3 蓄積の強化: national_tan の T-3 帯は 607R しかない。収集窓を締切 4〜2 分に寄せる(launchd 変更 = shin) | Yes |
| 4 | 2023-01-01〜04-24 全場欠落の再取得(公式 LZH からの可否確認 → 実行は boatrace.jp アクセス = shin GO) | Yes(小) |
| 5 | approach(進入)の枠番コピー再発防止テスト追加 | Yes(小) |
| 6 | 公開 mirror の git 履歴・gist 版履歴に残った先方実名の扱い(force push + gist 作り直し) | shin 判断(危険操作) |
| 7 | crontab 3 行(風 2 + 部品日次 1・継続) | Yes |
| 8 | 江戸川 2023-01〜04 の穴埋め(先方 boats 約 722R) | 低優先 |

## 8. 成果物一覧

| 種別 | パス |
|---|---|
| 統合報告 | `lane-reports/gift_investigation_20260909.md`(本書) |
| レーン報告 | `lane-reports/gift_gates_ga_20260909.md` / `gift_gate_g3_20260909.md` / `gift_parse_live_20260909.md` / `gift_knowledge_catalog_20260909.md` / `gift_t3_drift_phase1_20260909.md` / `gift_t3_drift_phase2_20260909.md` |
| script(再実行可) | `scripts/research/nextgen/gift_gates_ga.py` / `gift_gate_g3.py` / `gift_parse_live_board.py` / `gift_t3_drift.py` |
| 結果 JSON | `artifacts/research/nextgen/gift_audit/{gates,g3,parse,knowledge,drift}/` |
| parquet(gitignore・ローカルのみ) | `data/external/gift_20260906/_parsed/live_board_odds.parquet` / `closing_board_odds.parquet` / `board_file_meta.parquet` |
| 正本更新 | `research/DATA_STATUS.md` / `DECISION_LOG.md` / `FINDINGS.md` / `NEXT_ACTIONS.md` / `research_state.json` / `artifacts/research/experiment_registry.jsonl`(NG-GIFTG / NG-T3D1) |

## 9. 実測時間(session_clock tag gift_20260909)

- 開始 22:17:37 → 統合・正本更新完了 22:57(壁時計 約 40 分・5 レーン並列)。レーン単体の実測: GA 14 分 / GB 12 分 / P 17 分 / K 約 23 分 / D 34 分(phase 1 20 + phase 2 12)
- 手戻り: 4 レーンが背景実行の完了待ちで一旦停止し、L1 からの再開指示が必要だった(ハーネス仕様。成果物は全て完成)


