# AIでLPを作る注意とコツ — ai-lp-notes

このキットは **Claude Code から OpenAI API の GPT Image 2.0（`gpt-image-2`）** で LP の見た目を作る前提
（`scripts/gen_image.py` で呼ぶ・`OPENAI_API_KEY` 必要）。GPT Image 2.0 でも残る弱点と回避策をまとめる。
接続は [`connections.md`](connections.md)、出典は末尾。

---

## 1. GPT Image 2.0 の要点

- モデル: **GPT Image 2.0（`gpt-image-2`）**。OpenAI が 2026/4/21 公開した画像モデル（それ以前は `gpt-image-1.5`）。
- **接続**: Claude Code は画像生成を内蔵しないため **OpenAI API**（`OPENAI_API_KEY`）経由で呼ぶ（`scripts/gen_image.py`）。別モデルは Runway / HiggsField MCP も可（[`connections.md`](connections.md)）。
- **文字描画が高精度**: 日本語を含む多言語の文字を高精度（公称 約 99%）で描く。だから**キャッチや見出しの焼き込みも実用的**になった（旧世代の「日本語が崩れる」前提は大きく改善）。
- **サイズ**: ポートレート `1024x1536` を基本に、`gpt-image-2` は 幅・高さが 16 の倍数／アスペクト 1:3〜3:1 の任意解像度に対応（縦長スライス向き）。生成前に構造を推論（reasoning）する。
- **コスト目安**: 1 枚あたり概ね $0.04〜$0.35（解像度・複雑さによる）。API 課金。

---

## 2. それでも残る「画像である」弱点

文字精度は上がったが、**画像である以上の構造的な弱点は残る**。ここを HTML で補う:

- **後から直しにくい** — 価格改定・文言変更・誤字修正のたびに、その画像を**再生成**することになる。A/B やコピー改善を回す LP ほど不利。
- **SEO／検索が弱い** — ページ内テキストが無いと内容が認識されにくく、広告の品質評価が下がって CPC が上がりうる。
- **重い** — 高解像度画像の積み上げで LCP が悪化し、離脱が増える。
- **アクセシビリティ** — 画像化したテキストはスクリーンリーダーで読めない。
- **小さい／長い日本語はなお崩れうる** — 焼き込んだ文字は**生成後に誤字・崩れを必ず目視**する。

---

## 3. 定石はハイブリッド

- **FV・世界観パートは GPT Image 2.0 の画像、見出し・本文・CTA・フォームは HTML テキスト。**
- **CTA は透明ボタンを重ねず、HTML の `<a>` / `<button>` で実装。** 計測・色変更・A/B・タップ領域・アクセシビリティのすべてで有利。
- **後で必ず変わる要素（価格・日付・特典・会社名）はテキスト化**する。長文も HTML へ。

---

## 4. 計測・連携

- **GA4 は GTM 経由**で設置し、フォーム送信／CTA クリックをイベント化。公開後に**リアルタイムで発火確認**まで。
- **LINE 誘導 URL に UTM パラメータ**を付け、GA4 で流入・CV を判別。
- フォームの**送信先・自動返信・サンクスページ**（CV 計測トリガー）を 1 回テスト送信して確認する。

---

## 5. 生成画像の権利

- 文化庁『AI と著作権に関する考え方について』は **2024 年 3 月 15 日**、『チェックリスト＆ガイダンス』は **2024 年 7 月 31 日**公表（いずれも法的拘束力のない整理）。
- 生成・利用段階では**通常の著作権法が適用**され、既存著作物への**類似性＋依拠**があれば侵害になりうる。既存キャラ・ブランドロゴ・著名人に似た生成画像は避ける。
- OpenAI / 各 MCP の**利用規約**を確認・保存。商標・肖像権も確認。**プロンプトと生成物のログを保管**する。
- 参考: 2025 年 11 月 20 日、千葉県警が生成 AI 画像の無断複製を著作権法違反容疑で書類送検（報道）。

---

## 6. デプロイと運用

- デプロイ先と接続は [`connections.md`](connections.md)（**Vercel（`vercel` CLI / MCP）** ／ **GitHub Pages**）。**完成して終わりにせず、GitHub/Vercel を選ばせて公開まで**。**公開＝外部送信は人間が確認**してから。
- **QA は 3 体以上のサブエージェントで各観点 100 点まで**（機能・デザイン・モバイル&速度・コピー&法規制）。人が担うのは導線設計・ブランド表現・**モバイル実機確認・計測タグ検証・法的表記・ファクトチェック**。
- AI の癖: 指定の未実装／セクション間の品質ムラ／デスクトップ偏重でモバイル確認が後回し。

---

## 出典

- GPT Image 2 Model（gpt-image-2・サイズ）｜OpenAI API — https://developers.openai.com/api/docs/models/gpt-image-2
- Image generation｜OpenAI API — https://developers.openai.com/api/docs/guides/image-generation
- AI と画像生成の日本語テキスト精度（参考）｜ネットインパクト — https://www.netimpact.co.jp/technique/28075/
- AI と著作権について（公式）｜文化庁 — https://www.bunka.go.jp/seisaku/chosakuken/aiandcopyright.html
- AI 生成画像を無断複製、初の摘発か｜日本経済新聞 — https://www.nikkei.com/article/DGXZQOUD2067T0Q5A121C2000000/
- 主要デプロイ先比較（Vercel/Netlify/Cloudflare Pages）｜Qiita — https://qiita.com/YushiYamamoto/items/e648bdc866dd2bbe3482
