---
name: lp-builder
description: 固まったLP仕様(lp-spec.md)から、GPT Image 2.0(gpt-image-2/OpenAI API)で縦長スライスを生成し、HTMLでCTA/動画/フォーム/LINE導線を機能化して、3体以上のサブエージェントで各観点100点までQA、最後にGitHub/Vercelを選んでデプロイする。スマホファースト。
---

# lp-builder — スマホLPビルダー（GPT Image 2.0 → HTML → 100点QA → デプロイ）

> 「**画像で見た目・HTML で機能**」の 2 段方式（Image2 スタイル）を本キット向けに再構成。画像生成は **GPT Image 2.0（OpenAI API）**。謝辞は [CREDITS.md](../../../CREDITS.md)。

## 前提

`lp-grilling` の壁打ちで `lp-spec.md`（LP 仕様）が固まっていること。固まっていなければ先に `lp-grilling` に戻る。
コピー・構成・CTA は `lp-spec.md` が正。ここで創作しない。

## 流れ（4 フェーズ）

```
Phase 1 GPT Image 2.0で縦長スライス生成 → Phase 2 HTMLで機能化 → Phase 3 各観点100点までQA → Phase 4 デプロイ(GitHub/Vercelを選択)
```

### Phase 1 — GPT Image 2.0 で縦長スライスを生成する
**画像生成エンジンは GPT Image 2.0（`gpt-image-2`）。Claude Code は画像生成を内蔵しないので OpenAI API を呼ぶ**（`OPENAI_API_KEY` 必要）。同梱の `scripts/gen_image.py` を使う:

```bash
python3 scripts/gen_image.py --prompt "スマホLPのファーストビュー。..." --size 1024x1536 --out assets/slice1.png
```

- `lp-spec.md` の各セクションを、スマホ用の縦長スライス **4〜8 枚**に分けて生成する。
- **サイズ**: ポートレート `1024x1536` を基本に、より縦長は `1024x2048` 等（16 の倍数・アスペクト 1:3〜3:1）。
- **1 スライス＝1 プロンプト。** 全スライスで同じデザインシステム（色／余白／見出しの強さ）を保つ。参考デザインは**トンマナの参考**で、レイアウトのコピーではない。
- **GPT Image 2.0 は日本語を含む文字描画が高精度**（公称 約 99%）なので焼き込みも実用的。ただし**生成後に誤字・崩れを目視**し、後から変わる要素（価格・日付・特典）や長文は HTML テキストに回す（[`reference/ai-lp-notes.md`](../../../reference/ai-lp-notes.md)）。
- 接続・代替（Runway／HiggsField MCP）は [`reference/connections.md`](../../../reference/connections.md)。

### Phase 2 — HTML で機能化する
- `index.html` を作り、生成画像を `assets/` から読み込んで縦に隙間なく接続する（**画像は再生成しない**）。
- LP 幅は `min(100%, 430px)`、スマホは画面幅いっぱい、PC は中央。
- 画像内の CTA／動画／フォーム／リンク位置に **HTML の `<a>` / `<button>`** を重ねる（計測・A/B・タップ領域・アクセシビリティで有利）。
- URL 未確定は**仮モーダル**（閉じる／背景クリック／Esc）。コンバージョン目的なら**画面下に固定 CTA**。重要テキストは `sr-only` も。
- 計測タグ（GA4／GTM）、フォーム／LINE 導線（UTM 付き）を配線する。

### Phase 3 — QA（3 体以上のサブエージェントで各観点 100 点まで）
**自己採点しない。** `/lp-goal` のループで、**3 体以上のサブエージェント**（機能／デザイン／モバイル&速度／（任意）コピー&法規制）が各観点を 0〜100 点で採点し、**全観点が 100 点になるまで**実行 → 検証 → 修正を繰り返す。
基準は [`references/qa-checklist.md`](references/qa-checklist.md)。デザイン採点が曖昧なら**参考 LP の URL を求めてよい**。

### Phase 4 — デプロイ（GitHub / Vercel を選ばせて公開）
全観点 100 点になったら、**`AskUserQuestion` で「GitHub Pages か Vercel か」を質問**し、選ばれた先へデプロイする。
**完成して終わりにしない。** 接続は [`reference/connections.md`](../../../reference/connections.md)。

- **Vercel**: `vercel` CLI（`vercel deploy`）または Vercel MCP の「create a deployment」。
- **GitHub Pages**: リポジトリに push → Pages を有効化。
- 公開後に**本番 URL が HTTP 200** を返すこと、計測タグの発火を確認。独自ドメイン・決済・フォーム実連携は別途人間確認。

## 出力モードの選び方
- **既定: ハイブリッド**（GPT Image 2.0 のスライス＋HTML 機能化）。
- **HTML テキスト寄り**: 編集頻度・SEO・レスポンシブが最優先のとき。背景／装飾は画像、テキストは HTML。

## やってはいけない
- 仕様が固まる前に作り始める／壁打ちを飛ばす
- Phase 2 で画像を再生成してやり直す
- 自己採点で「完成」と言う（採点はサブエージェント。全観点 100 点まで回す）
- QA・公開先の選択を飛ばして「完成」で止まる（必ず GitHub/Vercel を選ばせて公開まで）
