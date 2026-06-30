# claude-code-lp-builder-ja

**Claude Code に渡すと、いきなり作らず「壁打ち」から始まる — スマホ LP 自動生成キット。**

**前提は Claude Code。** このフォルダを Claude Code で開くと、AI がまず **事業内容・LP の内容・参考 URL** などを
一問ずつ聞く壁打ちを始め、答えるだけで設計図（`lp-spec.md`）が固まります。
そこから **`/lp-goal`** で、**GPT Image 2.0（OpenAI API・`gpt-image-2`）** による画像生成 → HTML 化 →
**3 体以上のサブエージェントが各観点 100 点を出すまで**作り込み → **GitHub / Vercel を選んで公開**まで自走します。
接続は [`reference/connections.md`](reference/connections.md)。

> 🎁 これは配布用のギフト版です。壁打ちは [GrillMe / grilling](https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md)（MIT・Matt Pocock）、
> `/lp-goal` は goal-setter / makeloop（MIT）の考え方を土台に、LP 制作向けへ再構成しています。謝辞とライセンスは [CREDITS.md](CREDITS.md)。

- 📊 中身の解説スライド: [`./slides.html`](slides.html)
- 📄 中身の 1 枚資料（縦スクロール）: [`./onepager.html`](onepager.html)

---

## このキットの「3 つの効き目」

1. **1 発目で作らせない。** リンク＋「LP作って」でも、**必ず壁打ちから**。`lp-spec.md` が固まるまでビルドしない。
2. **本当にループする。** 壁打ち後、**3 体以上のサブエージェント**（機能／デザイン／モバイル&速度／コピー&法規制）が
   各観点を採点し、**全部 100 点になるまで**実行 → 検証 → 修正を繰り返す（自己採点しない）。
3. **完成で止めない。** 仕上がったら **GitHub Pages か Vercel か**を質問し、選ばれた先へ**公開まで**。

---

## 収録物

| 収録物 | 役割 | 場所 |
|---|---|---|
| **オーケストレーター** | 壁打ち→/lp-goal→ビルド→QA→デプロイ を強制する CLAUDE.md | [`CLAUDE.md`](CLAUDE.md) |
| **壁打ち `lp-grilling`** | 一問一答で仕様を固めるスキル（GrillMe を LP 向けに再構成） | [`.claude/skills/lp-grilling/`](.claude/skills/lp-grilling/SKILL.md) |
| **`/lp-goal`** | 3 体以上のサブエージェントで各観点 100 点まで自走 → 公開先を選んでデプロイ | [`.claude/commands/lp-goal.md`](.claude/commands/lp-goal.md) |
| **LP ビルダー `lp-builder`** | GPT Image 2.0 で画像生成 → HTML 機能化 → QA → デプロイ | [`.claude/skills/lp-builder/`](.claude/skills/lp-builder/SKILL.md) |
| **画像生成スクリプト** | OpenAI API（gpt-image-2）で縦長スライスを生成 | [`scripts/gen_image.py`](scripts/gen_image.py) |
| **同梱ノウハウ** | 接続ガイド／LP 作成のコツ／AI で LP を作る注意（出典つき） | [`reference/`](reference/) |

Claude Code はプロジェクト直下の `CLAUDE.md` を自動で読み、この順番で動きます。

---

## 使い方（Claude Code・5 ステップ）

1. **Claude Code でこのフォルダを開く**（`CLAUDE.md` が自動で読み込まれます）。画像生成用に `export OPENAI_API_KEY=...` を設定。
2. **「LP 作って」** と話しかける → **必ずプランモードで壁打ち**が始まる（いきなり作りません）。
3. 事業内容・LP の内容・参考 URL… の質問に答えていく → `lp-spec.md` が固まる。
4. **`/lp-goal`** → GPT Image 2.0 で画像生成 → HTML 化 → **3 体以上のサブエージェントが各観点 100 点を出すまで**自走。
5. **GitHub Pages か Vercel かを聞かれたら選ぶ** → その先へ**公開（デプロイ）**まで。

---

## ワークフロー（4 フェーズ）

```
 ① 開く → ② 壁打ち(プランモード強制) → ③ /lp-goal(画像生成→HTML→3体QAで100点) → ④ デプロイ(GitHub/Vercelを選択)
              lp-grilling                  lp-builder ＋ gen_image.py                    connections
                  ↓
              lp-spec.md（LP仕様＝以降の入力）
```

- **フェーズ1 壁打ち** — `.claude/skills/lp-grilling/`（質問銀行つき）。出力は `lp-spec.md`。**仕様が無ければビルド禁止。**
- **フェーズ2 /lp-goal** — `.claude/commands/lp-goal.md`。3 体以上のサブエージェントで各観点 100 点まで実行→検証→修正。
- **フェーズ3 ビルド** — `.claude/skills/lp-builder/`。Phase 1 `scripts/gen_image.py`（gpt-image-2）→ Phase 2 HTML 機能化。
- **フェーズ4 デプロイ** — 100 点になったら **GitHub Pages or Vercel を質問**して公開（人間が選択＝承認）。

---

## 同梱ノウハウ

- **接続ガイド**（Claude Code 前提。画像＝OpenAI API gpt-image-2／Runway・HiggsField、デプロイ＝Vercel/GitHub）: [`reference/connections.md`](reference/connections.md)
- **LP 作成のコツ**（FV の 4 要素・新 PASONA 等の型・1 ページ 1 CTA・フォーム削減・速度・法規制）: [`reference/lp-playbook.md`](reference/lp-playbook.md)
- **AI で LP を作る注意**（GPT Image 2.0 の文字精度と残る弱点・ハイブリッド・計測・権利・デプロイ）: [`reference/ai-lp-notes.md`](reference/ai-lp-notes.md)

数値は業界ベンチマーク・経験則を含みます。**自分の LP では必ず A/B テストで再検証**してください。出典は各ファイル末尾。

---

## 安全（キットに組み込んだ歯止め）

- **1 発目で LP を作らない・壁打ち必須**（`lp-spec.md` が無ければビルド禁止）。
- 取り消せない操作（公開・デプロイ・課金・決済/フォーム連携・外部送信）の前は**必ず人間に確認**。自動公開しない。
- コピー・数値は事実から。**誇張・断定保証をしない**（景表法／薬機法／特商法／ステマ規制）。
- 仕様（`lp-spec.md`）にない機能・コピーを足さない（スコープ厳守）。
- **各観点 100 点（サブエージェント採点）まで「完成」と言わない**。
- **`OPENAI_API_KEY` などの秘密情報をコミットしない**。

---

## ライセンス / クレジット

- 本キット: MIT（[LICENSE](LICENSE)）— © 2026 河村風真 (fuuuuuuma)
- 土台にした原典（GrillMe / goal-setter / makeloop — いずれも MIT）への謝辞とライセンス全文: [CREDITS.md](CREDITS.md)
- 壁打ちの原典 GrillMe: https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md

自由に使って、改変して、配ってかまいません。原典の著作権表示（CREDITS.md）だけ一緒に残してください。
