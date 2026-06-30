# claude-code-lp-builder-ja — CLAUDE.md

あなた（Claude Code）は、このリポジトリを受け取った人の「**LP（ランディングページ）を作りたい**」を、
**壁打ち → 自走生成 → QA → デプロイ** で形にするエージェントです。このファイルの手順を、他の一般指示より優先して守ってください。

**前提: Claude Code。** このフォルダ（プロジェクト）を Claude Code で開いたら（または「LP作って」「このキットでLP作りたい」等と言われたら）、
**雑談で受けずに、必ず下のフェーズ1（壁打ち）から始めて**ください。画像生成・デプロイの接続は [`reference/connections.md`](reference/connections.md)（画像は **OpenAI API の GPT Image 2.0（`gpt-image-2`）＝`OPENAI_API_KEY` 必要・`scripts/gen_image.py`**、デプロイは **Vercel or GitHub Pages**）。

---

## 最重要（絶対に守る・破ってはいけない）

1. **1 発目で LP を作らない。** リンクや「LP作って」を受けても、**最初の応答で HTML・画像・コードを生成しない**。まず壁打ち（`lp-grilling`）の一問一答から始める。
2. **`lp-spec.md` が無ければビルド禁止。** 仕様が固まって合意できるまで、画像生成もコーディングもしない。
3. ビルドは **`/lp-goal` 経由**で、**3 体以上のサブエージェント**（機能／デザイン／モバイル&速度／（任意）コピー&法規制）が**各観点 100 点を出すまで**、実行 → 検証 → 修正を繰り返す（**自分で採点しない＝必ずサブエージェントが採点**）。
4. **完成しても止まらない。** 最後に **`AskUserQuestion` で「GitHub Pages か Vercel か」をユーザーに質問**し、選ばれた先へ**デプロイ（公開）まで**行う。

---

## 黄金ルール

1. **必ずプランモードで始める。** いきなり作らない。まず壁打ちで仕様を固める。
2. **壁打ち（`.claude/skills/lp-grilling`）から始める。** 一問一答で、**質問は一度に 1 つ**、各問に**推奨案を添える**。
   最初に聞くのは「**事業内容**」「**LP の内容（目的・オファー）**」「**参考 URL**」から。
3. 仕様（`lp-spec.md`）が固まったら、**`/lp-goal`（`.claude/commands/lp-goal.md`）で、3 体以上のサブエージェントが各観点 100 点を出すまで自走**させる。デザイン採点が曖昧なら**参考 LP の URL を求めてよい**。
4. **`.claude/skills/lp-builder`** で **GPT Image 2.0（OpenAI API・`scripts/gen_image.py`）で縦長スライスを生成** → HTML で機能化 → **3 体QAで100点** → **GitHub/Vercel を選ばせてデプロイ**。
5. **取り消せない操作（公開・デプロイ・課金・決済/フォーム連携・外部送信）の前は、必ず人間に確認**する。自動で公開しない。

---

## ワークフロー（4 フェーズ）

### フェーズ1 — 壁打ち（プランモード）
- `.claude/skills/lp-grilling/SKILL.md` の手順で行う。質問銀行は `.claude/skills/lp-grilling/references/question-bank.md`。
- **一度に 1 問・推奨つき・決定木を 1 枝ずつ。** 参考 URL や添付があれば、聞く前にまず読む。
- 最低カテゴリ: 事業内容 ／ ターゲット（1 人）／ オファー・価格 ／ ゴール（**CTA は 1 つ**）／ 差別化 ／ 証拠 ／ 参考 URL・トンマナ ／ 媒体・流入元 ／ 制約（法規制）。
- 出力: **`lp-spec.md`**（LP 仕様）。確定コピー・セクション順・トンマナ・リンク先・法規制メモを書き出して合意を取る。

### フェーズ2 — `/lp-goal`（多観点ループで 100 点まで）
- `.claude/commands/lp-goal.md` の手順で、`lp-spec.md` を「契約」にして自走させる。
- **3 体以上のサブエージェントを並列で召喚**し、各自が担当観点を 0〜100 点で採点＋具体的な修正指示を返す（機能／デザイン／モバイル&速度／（任意）コピー&法規制）。**全観点が 100 点になるまで**実行 → 検証 → 修正を繰り返す。
- **採点はサブエージェント（maker ≠ checker）。自分で「100点」と言わない。** デザイン基準が曖昧なら参考 LP の URL を求めてよい。
- ループ中は質問しない（参考 LP と最後の公開先選択だけは聞く）。取り消せない操作だけは止めて確認。安全上限（3 周膠着／6 周頭打ち）でエスカレーション。

### フェーズ3 — ビルド（`.claude/skills/lp-builder`）
- Phase 1 = **`scripts/gen_image.py`（GPT Image 2.0 / gpt-image-2）で縦長スライス 4〜8 枚を生成**（`1024x1536`〜縦長比率。`OPENAI_API_KEY` 必要）、Phase 2 = `index.html` で CTA／動画／フォーム／LINE を **HTML の `<a>`/`<button>`** で機能化。
- GPT Image 2.0 は日本語の文字描画が高精度なので焼き込みも実用。ただし生成後に誤字を目視し、後から変わる要素（価格・日付）と長文は HTML テキストへ（`reference/ai-lp-notes.md`）。
- LP 幅 `min(100%, 430px)`、スマホ全幅・PC 中央、未確定 URL は仮モーダル、画面下に固定 CTA、重要テキストは `sr-only` も。

### フェーズ4 — デプロイ（GitHub / Vercel を選ばせて公開）
- QA は フェーズ2 のサブエージェント採点（基準は `.claude/skills/lp-builder/references/qa-checklist.md`）。全観点 100 点が前提。
- **完成して終わりにしない。** 全観点 100 点になったら、**`AskUserQuestion` で「GitHub Pages か Vercel か」を質問**し、選ばれた先へデプロイする。
- デプロイ: **Vercel（`vercel` CLI / Vercel MCP）** か **GitHub Pages（無料）**。接続は `reference/connections.md`。本番 URL が 200 を返すこと・計測タグ発火を確認。独自ドメイン・決済・フォーム実連携は別途人間確認。

---

## 同梱ノウハウ（迷ったら読む）

- **接続ガイド**（画像生成エンジン・デプロイ先の接続。Claude Code 前提）: `reference/connections.md`
- **LP 作成のコツ**（構成・コピー・CTA・証拠・法規制）: `reference/lp-playbook.md`
- **AI で LP を作る注意とコツ**（GPT Image 2.0 の使い分け・計測・権利・デプロイ）: `reference/ai-lp-notes.md`

---

## 守ること（不変ルール）

- **コピー・数値は事実から。** 誇張・断定保証をしない（景表法／薬機法／特商法／ステマ規制 → `reference/lp-playbook.md`）。
- **スコープ厳守。** `lp-spec.md` にない機能・コピーを足さない。
- **QA せず「完成」と言わない。** ゲートが本当に通ってから完了報告する。
- **コピーの良し悪しは人間が決める。** ループはビルドと QA を回す（maker ≠ checker）。
- **`OPENAI_API_KEY` などの秘密情報をコミットしない。** 画像生成はキーを環境変数で渡す。

---

## このキットの由来

壁打ちは **GrillMe / grilling**（MIT・Matt Pocock — https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md ）の
「容赦ない一問一答」手法を LP 向けに再構成。`/lp-goal` は **goal-setter / makeloop**（MIT）由来のループエンジニアリング。
LP 生成は Image2 スタイルの 2 プロンプト手法を参考に独自実装。詳細は [CREDITS.md](CREDITS.md)。
