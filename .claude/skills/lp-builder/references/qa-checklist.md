# QA チェックリスト — lp-builder

納品／デプロイの前に必ず通す。`/goal` ループ（`prompts/goal-loop.md`）のゲートはこのリストを基準にする。
数値基準は出典つき（末尾）。

## ビジュアル
- [ ] スマホファースト（最小 375px で破綻しない／設計幅 375〜430px）
- [ ] FV で「誰の・何の・どんな得か」と最初の行動が伝わる
- [ ] 画像スライスが 1 つのデザインシステムに見える（色・余白・見出しの強さ）
- [ ] GPT Image 2.0 の焼き込み文字に誤字・崩れがないか目視（小さい／長い日本語は要注意 → HTML テキストへ）
- [ ] ポスターではなく「読める LP」になっている

## 機能
- [ ] CTA が正しい URL、または仮モーダルを開く
- [ ] 動画枠が正しい動画、または仮モーダルを開く
- [ ] フォーム／LINE／プロフィールリンクが、提供されていれば配線済み
- [ ] モーダルが 閉じるボタン・背景クリック・Esc で閉じる
- [ ] 画面下の固定 CTA が本文の必須要素を隠していない（固定バー分の下部余白を確保）
- [ ] 画像内の重要テキストに対応する `sr-only` がある

## レスポンシブ／スマホ UX
- [ ] **390px と 430px で横スクロールが出ない**（`<meta viewport>` 設定、`max-width:100%`／`box-sizing:border-box`）
- [ ] PC でスマホキャンバスが中央表示
- [ ] **タップターゲットが十分**（実装目安 44×44px 以上、ターゲット間 8px 程度。WCAG 2.2 は最小 24px・拡張 44px）
- [ ] 本文 16px 以上、コントラスト比 通常 4.5:1／大きい文字 3:1 以上
- [ ] 重要 CTA・主要操作が**親指で届く下部**にある
- [ ] フォーム入力補助（`type=tel`／`inputmode`／`type=email`／`autocomplete`／郵便番号→住所補完／全角強制なし／エラーは色＋テキスト）

## 表示速度（Core Web Vitals・p75）
- [ ] **LCP ≤ 2.5 秒**（FV 画像の最適化・先読み・WebP/AVIF・lazy-load）
- [ ] **CLS ≤ 0.1**（画像・iframe・動画に width/height か aspect-ratio を指定し領域を確保）
- [ ] **INP ≤ 200ms**（2024 年 3 月に FID を置換した指標）

## 計測・連携
- [ ] GA4（GTM 経由）でフォーム送信／CTA クリックをイベント化し、公開後にリアルタイムで発火確認
- [ ] LINE 誘導 URL に UTM パラメータ
- [ ] フォーム送信先・自動返信・サンクスページを 1 回テスト送信して確認

## 法規制・表記
- [ ] 誇大広告・断定保証がない（景表法：優良誤認・有利誤認）
- [ ] 体験談・推薦に広告である旨の明示（ステマ規制・2023/10/1）
- [ ] 健康・美容で医薬品的な効能効果の断定がない（薬機法）
- [ ] 価格・特典・期間の表示が実態と一致（有利誤認・二重価格に注意）
- [ ] フォームがある場合、プライバシーポリシー／個人情報の取得目的を記載

## デリバリ
- [ ] 生成画像など素材はプロジェクト内（`assets/`）に置いている
- [ ] スマホ／PC のスクショを生成して目視（空白・崩れ・リンク切れがない）
- [ ] **デプロイは人間の確認後**（Vercel or GitHub Pages → `reference/connections.md`）。公開 URL が HTTP 200 を返す

---

## 出典
- Web Vitals（LCP/CLS/INP・p75）｜web.dev — https://web.dev/articles/vitals
- INP becomes a Core Web Vital（2024/3/12）｜web.dev — https://web.dev/blog/inp-cwv-march-12
- Target Size (Minimum) AA・24px｜W3C WAI — https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
- Target Size (Enhanced) AAA・44px｜W3C WAI — https://www.w3.org/WAI/WCAG22/Understanding/target-size-enhanced.html
- Layout（44×44pt）｜Apple HIG — https://developer.apple.com/design/human-interface-guidelines/layout
- ステルスマーケティング規制｜消費者庁 — https://www.caa.go.jp/policies/policy/representation/fair_labeling/stealth_marketing
