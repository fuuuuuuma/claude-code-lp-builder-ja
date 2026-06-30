# LP作成のコツ — lp-playbook

このキットが LP を作るときに従う、**構成・コピー・コンバージョン・法規制**の指針。
数値の多くは業界ベンチマークや経験則であり、**自分の LP では必ず A/B テストで再検証**する。出典は末尾。

---

## 1. 構成の鉄則

- **ファーストビュー（FV）に 4 要素**を必ず入れる: キャッチコピー／アイキャッチ画像／CTA ボタン／信頼要素（実績・権威）。
- FV で「**誰のための・何の・どんな得が得られるページか**」を即答できる状態に。詰め込まず「伝わる順」を優先。
- **広告／流入元の訴求文と FV 見出しを一致させる（メッセージマッチ）。** 離脱改善の最優先施策。
- 証拠（実績・声・データ）は**オファーの前**に積む。**FAQ は申込ボタンの直上**に置く。
- **ゴール（CTA）は 1 つに絞る。** 出口を 1 つにして離脱を防ぐのが高 CV の最重要原則。

### 推奨セクション順（心理変化に沿う）
1. FV（誰に・何を・どんな得か ＋ 信頼要素）
2. 共感・問題提起（悩みの自分ごと化）
3. ベネフィット（得られる未来 ＋ 根拠）
4. 権威・実績（受賞／メディア／専門家推薦）
5. お客様の声（実名・顔写真、可能なら動画）
6. 比較表／ストーリー（選ぶ理由・開発背景）
7. オファー・緊急性（今行動する理由）
8. FAQ（申込をためらう不安をピンポイント解消）
9. クロージング CTA

---

## 2. コピーの型（用途で選ぶ）

| 型 | 流れ | 向いている用途 |
|---|---|---|
| **新 PASONA** | Problem → Affinity(共感) → Solution → Offer → Narrow down → Action | 悩み解決型。旧 PASONA の Agitation(煽り)を Affinity に置換。脅すように煽らない |
| **QUEST** | Qualify → Understand → Educate → Stimulate → Transition | 特定の悩みを持つ読者向け |
| **PASBECONA** | 新 PASONA の Solution→Offer の間に Benefit / Evidence / Contents を挿入 | オファー前に証拠を厚くする Web 時代型 |
| **PREP** | 結論 → 理由 → 具体例 → 結論 | 各セクション内・FAQ 回答の型 |
| **AIDA** | Attention → Interest → Desire → Action | 認知重視・新商品 |

---

## 3. コンバージョンを上げる要点

- **フォーム項目を削る** — 項目数と CVR はほぼ逆相関。**目安は 8 項目以下、可能なら 5 項目以下**。
  - 事例: Imagescape の問い合わせフォームで 11→4 項目にした同一テストで、送信 +160%・CVR +120%（単発事例）。
  - Baymard のチェックアウト平均は約 11.3 項目だが、大半は 8 項目で足りる。
- **1 ページ＝1 ゴール＝1 主要 CTA** — Unbounce の 18,639 LP 分析で、単一 CTA の LP は平均 CVR **13.5%**、3 つ以上は **10.5%**。
  - 回遊リンク・グローバルナビ・無関係な外部リンクを LP から外す。
- **表示速度** — Think with Google / SOASTA で、読込 1→3 秒で直帰確率 **+32%**、1→5 秒で **+90%**、1→10 秒で **+123%**。モバイルは **3 秒超で 53% 離脱**。速度は FV 表示より前の前提条件。
- **信頼シグナル（社会的証明）** — 実名・顔写真・数値入りの声、導入実績、保証／返金、プライバシー記載を **CTA の近く**に。
- **ベンチマーク** — Unbounce 2024（41,000 ページ）で全業種 CVR 中央値 **6.6%**。良し悪しは**必ず同業種と比較**（SaaS 低め・イベント/エンタメ高めなど業種差が大きい）。

> ⚠️ **数値の扱い**: 「単一 CTA で +32%」「項目 1 つで 20〜30% 減」「1 秒遅延で 7% 減」などの派生数値は、出典が辿れないものが多い（**未確認**）。断定で使わない。「フォーム離脱 約 7 割」は実体が Baymard の**カート放棄率 70.22%**（EC チェックアウト）で、汎用フォーム離脱率ではない。

---

## 4. チャネル別の要点

- **セミナー／ウェビナー**: FV にタイトル・開催日時・オンライン開催の明示・登壇者（顔写真／所属／役職）。中段で経歴・実績。申込フォームは氏名・メール・会社名程度に短縮。
- **LINE 登録**: 商品名／キャッチ → 問題提起と解決法 → ベネフィット → 配信内容の予告 → 友だち追加ボタン。核は「**今、登録する理由**」になる即時特典。
- **資料請求／BtoB**: フォームは会社名・氏名・メールの 3 項目、問い合わせは ＋電話・課題内容の 5 項目が目安。

---

## 5. 日本語 LP の法規制チェック（公開前に必ず）

> 一次情報（消費者庁・文化庁等）で最終確認する。薬機法の具体的な線引き等は専門家確認を推奨。

### 景品表示法（不当景品類及び不当表示防止法）
- **優良誤認表示（第 5 条第 1 号）**: 品質・内容を実際／競合より著しく優良と示す表示。例「3 日で若返る」「飲むだけで −10kg」など根拠なき断定。
- **有利誤認表示（第 5 条第 2 号）**: 価格・取引条件を実際／競合より著しく有利と誤認させる表示。例「今日だけ 50%OFF」が実は通常価格、「先着◯名限定」が実際は一律。
- **第 5 条第 3 号（指定告示）**: おとり広告など。
- **課徴金**: 対象売上額の **3%**（対象期間は原則最長 3 年）。課徴金額が 150 万円未満なら不命令。自主返金で減額・不命令の余地。
- **2024 年（令和 6 年）10 月 1 日施行の改正**: 10 年以内の再違反は課徴金 **1.5 倍（実質 4.5%）**。優良誤認・有利誤認に **直罰（100 万円以下の罰金）**を新設。

### ステマ規制（2023 年 10 月 1 日施行）
- 景表法第 5 条第 3 号の指定告示「**一般消費者が事業者の表示であることを判別することが困難な表示**」。
- **規制対象は事業者（広告主）**。LP の体験談・推薦・インフルエンサー投稿には **広告である旨の明示**が必要。
- 「No.1」「満足度 95%」も、実データの裏付けがなければ優良誤認になりうる。

### 薬機法（医薬品医療機器等法）
- 健康食品・化粧品などで、**医薬品的な効能効果の断定表現は禁止**。具体的な線引きは一次情報・専門家で確認（未確認の線引きは断定しない）。

### Web アクセシビリティ（関連）
- 改正障害者差別解消法は 2024 年 4 月 1 日施行で、民間事業者に**合理的配慮の提供**が義務化。**Web アクセシビリティ自体は義務化されておらず**、向上は「環境の整備」（努力義務）の位置づけ。

---

## 出典

**LP 構成 / コピー**
- LP 構成の作り方｜Web 幹事 — https://web-kanji.com/posts/landing-page-constitution
- 売れる LP 構成の作り方｜トライハッチ — https://lab.tryhatch.co.jp/lp/lp-structure/
- PASONA と PASBECONA｜my-OBC-life — https://obc-life.com/pasona-pasbecona/
- QUEST フォーミュラ｜Data Driven Knowledgebase — https://blog.since2020.jp/glossary/quest/
- セミナー LP の作り方｜ferret One — https://ferret-one.com/blog/seminar-lp

**CRO / ベンチマーク**
- Average landing page conversion rate (Q4 2024)｜Unbounce — https://unbounce.com/average-conversion-rates-landing-pages/
- Minimize Form Fields｜Baymard — https://baymard.com/blog/checkout-flow-average-form-fields
- Imagescape Contact Form Case Study (PDF) — https://www.imagescape.com/media/filer_public/06/94/0694c7f4-8914-4598-8871-b857fbc12737/form_case_study.pdf
- Mobile Page Speed Benchmarks｜Think with Google — https://business.google.com/think/marketing-strategies/mobile-page-speed-new-industry-benchmarks/

**法規制（一次・公式）**
- 優良誤認／有利誤認の解説｜消費者庁 — https://www.caa.go.jp/policies/policy/representation/fair_labeling/representation_regulation/misleading_representation
- ステルスマーケティングは景表法違反に（2023/10/1）｜消費者庁 — https://www.caa.go.jp/policies/policy/representation/fair_labeling/stealth_marketing
- 景品表示法改正（課徴金・罰則拡充）｜契約ウォッチ — https://keiyaku-watch.jp/media/hourei/keihinhyojihou-2024/
- 改正障害者差別解消法と Web アクセシビリティ｜Web 担当者 Forum — https://webtan.impress.co.jp/e/2024/05/10/46759
