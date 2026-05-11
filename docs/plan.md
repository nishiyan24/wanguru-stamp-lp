# わんグル スタンプ特典 LP 実施プラン

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** わんグルへの口コミ投稿を促す、かわいくてシンプルなランディングページを `index.html` 1ファイルで完成させる

**Architecture:** HTML + CSS + JavaScript をすべて `index.html` 1ファイルに収める。外部依存は Google Fonts（Noto Sans JP）のみ。`assets/` フォルダに後からスタンプ画像を追加できる設計にする。

**Tech Stack:** HTML5, CSS3（CSS変数・Flexbox・Grid）, Vanilla JavaScript, Google Fonts

---

## ファイル構成

```
wanguru-stamp-lp/
├── index.html        ← 全コード（HTML + <style> + <script>）
├── assets/           ← スタンプ画像を後から追加（stamp-1.png〜）
├── docs/
│   ├── design.md
│   └── plan.md
├── CLAUDE.md
└── README.md
```

---

## Task 1: HTMLの骨格作成 + assetsフォルダ

**Files:**
- Create: `index.html`
- Create: `assets/` フォルダ（空のまま）

- [ ] **Step 1: `assets/` フォルダを作成する**

  エクスプローラーまたは以下コマンドで作成：
  ```
  mkdir assets
  ```

- [ ] **Step 2: `index.html` を作成する**

  ```html
  <!DOCTYPE html>
  <html lang="ja">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>愛犬のオリジナルスタンプをプレゼント！ | わんグル</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;700;900&display=swap" rel="stylesheet">
    <style>
      /* CSSはTask 2で追加 */
    </style>
  </head>
  <body>

    <!-- ① ヒーロー -->
    <section id="hero"></section>

    <!-- ② 特典の説明 -->
    <section id="benefits"></section>

    <!-- ③ スタンプギャラリー -->
    <section id="gallery"></section>

    <!-- ④ 受け取り方（3ステップ） -->
    <section id="steps"></section>

    <!-- ⑤ 安心ポイント（FAQ） -->
    <section id="safety"></section>

    <!-- ⑥ 最終CTA -->
    <section id="final-cta"></section>

    <!-- ⑦ フッター -->
    <footer id="footer"></footer>

    <script>
      /* JSはTask 8で追加 */
    </script>
  </body>
  </html>
  ```

- [ ] **Step 3: ブラウザで確認する**

  `index.html` をブラウザで開く（ダブルクリックでOK）。
  真っ白なページが表示されれば成功。

---

## Task 2: CSSベース設定

**Files:**
- Modify: `index.html` の `<style>` タグ内

- [ ] **Step 1: `<style>` タグ内に以下を追加する**

  ```css
  /* ===== CSS変数（カラーパレット） ===== */
  :root {
    --color-main:      #FF8C69;
    --color-main-dark: #E87055;
    --color-bg:        #FFF8F0;
    --color-accent:    #A8D5A2;
    --color-text:      #4A3728;
    --color-white:     #FFFFFF;
    --radius:          16px;
    --shadow:          0 4px 16px rgba(74, 55, 40, 0.10);
    --font:            'Noto Sans JP', sans-serif;
  }

  /* ===== リセット ===== */
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: var(--font);
    background-color: var(--color-bg);
    color: var(--color-text);
    line-height: 1.7;
  }

  img { max-width: 100%; height: auto; display: block; }

  /* ===== 共通レイアウト ===== */
  .container {
    max-width: 720px;
    margin: 0 auto;
    padding: 0 20px;
  }

  .section { padding: 64px 0; }

  .section-title {
    font-size: 1.5rem;
    font-weight: 900;
    text-align: center;
    margin-bottom: 32px;
  }

  .section-title span { color: var(--color-main); }

  /* ===== 共通ボタン ===== */
  .btn {
    display: inline-block;
    background-color: var(--color-main);
    color: var(--color-white);
    font-family: var(--font);
    font-size: 1.05rem;
    font-weight: 700;
    padding: 16px 40px;
    border-radius: 50px;
    border: none;
    cursor: pointer;
    text-decoration: none;
    box-shadow: 0 4px 12px rgba(255, 140, 105, 0.40);
    transition: background-color 0.2s, transform 0.15s;
  }

  .btn:hover {
    background-color: var(--color-main-dark);
    transform: translateY(-2px);
  }

  /* ===== 共通カード ===== */
  .card {
    background: var(--color-white);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    padding: 24px;
  }
  ```

- [ ] **Step 2: ブラウザで確認する**

  `index.html` をリロード。背景が薄いクリーム色（`#FFF8F0`）になっていれば成功。

---

## Task 3: ヒーローセクション

**Files:**
- Modify: `index.html` の `<section id="hero">` と `<style>`

- [ ] **Step 1: `<section id="hero">` の中身を追加する**

  ```html
  <section id="hero" class="hero">
    <div class="container">
      <div class="hero__inner">
        <div class="hero__badge">🐾 期間限定特典</div>
        <h1 class="hero__title">
          あなたの愛犬が、<br>
          <span>スタンプになる！</span>
        </h1>
        <p class="hero__sub">
          わんグルに口コミを書くだけで<br>
          オリジナルスタンプが<strong>無料</strong>でもらえる！
        </p>
        <a href="#" class="btn hero__btn">
          🐶 口コミを書いてスタンプをもらう
        </a>
        <p class="hero__note">※ 口コミ投稿後にスタンプ申請フォームをご案内します</p>
      </div>
    </div>
  </section>
  ```

  > **注意:** `href="#"` は仮のリンクです。わんグルの口コミページURLが決まったら差し替えてください。

- [ ] **Step 2: `<style>` にヒーロー用CSSを追加する**

  ```css
  /* ===== ヒーロー ===== */
  .hero {
    background: linear-gradient(160deg, #FFF8F0 0%, #FFE8D6 100%);
    padding: 80px 0 64px;
    text-align: center;
  }

  .hero__badge {
    display: inline-block;
    background: var(--color-accent);
    color: var(--color-text);
    font-size: 0.85rem;
    font-weight: 700;
    padding: 6px 18px;
    border-radius: 50px;
    margin-bottom: 20px;
  }

  .hero__title {
    font-size: 2.4rem;
    font-weight: 900;
    line-height: 1.3;
    margin-bottom: 20px;
  }

  .hero__title span { color: var(--color-main); }

  .hero__sub {
    font-size: 1.1rem;
    margin-bottom: 36px;
    line-height: 1.9;
  }

  .hero__sub strong {
    color: var(--color-main);
    font-weight: 900;
  }

  .hero__btn { font-size: 1.15rem; padding: 18px 48px; }

  .hero__note {
    margin-top: 16px;
    font-size: 0.78rem;
    color: #aaa;
  }
  ```

- [ ] **Step 3: ブラウザで確認する**

  - ページを開いたときにグラデーション背景があるか
  - タイトル「あなたの愛犬が、スタンプになる！」がオレンジ色で表示されるか
  - ボタンがオレンジ色で表示されるか

---

## Task 4: 特典説明 + 3ステップフロー

**Files:**
- Modify: `index.html` の `<section id="benefits">`・`<section id="steps">` と `<style>`

- [ ] **Step 1: `<section id="benefits">` の中身を追加する**

  ```html
  <section id="benefits" class="section benefits">
    <div class="container">
      <h2 class="section-title">🎁 もらえる<span>特典</span></h2>
      <div class="benefit-card card">
        <div class="benefit-card__icon">🐶</div>
        <div class="benefit-card__body">
          <h3 class="benefit-card__title">愛犬のオリジナルスタンプ</h3>
          <p class="benefit-card__text">
            あなたの愛犬の写真をもとに、LINEで使えるかわいいオリジナルスタンプを
            <strong>完全無料</strong>でプレゼント！お友達にシェアしてじまんしちゃおう🎉
          </p>
          <ul class="benefit-list">
            <li>✅ 完全無料（制作費・送料 一切なし）</li>
            <li>✅ LINEスタンプとして受け取り可能</li>
            <li>✅ 愛犬の写真1枚から作成</li>
          </ul>
        </div>
      </div>
    </div>
  </section>
  ```

- [ ] **Step 2: `<section id="steps">` の中身を追加する**

  ```html
  <section id="steps" class="section steps">
    <div class="container">
      <h2 class="section-title">📋 <span>3ステップ</span>で受け取れる！</h2>
      <div class="steps__list">

        <div class="step-item">
          <div class="step-item__num">1</div>
          <div class="step-item__body">
            <h3 class="step-item__title">わんグルで口コミを書く</h3>
            <p class="step-item__text">
              利用したペット関連のお店・サービスについて、正直な感想を投稿してください。
            </p>
          </div>
        </div>

        <div class="step-item">
          <div class="step-item__num">2</div>
          <div class="step-item__body">
            <h3 class="step-item__title">申請フォームに必要事項を入力</h3>
            <p class="step-item__text">
              口コミ投稿後に表示されるフォームから、愛犬のお写真と一緒に申請します。
            </p>
          </div>
        </div>

        <div class="step-item">
          <div class="step-item__num">3</div>
          <div class="step-item__body">
            <h3 class="step-item__title">スタンプが届く！</h3>
            <p class="step-item__text">
              数営業日以内にLINEスタンプのURLをお送りします。ダウンロードしてお使いください🎉
            </p>
          </div>
        </div>

      </div>
    </div>
  </section>
  ```

- [ ] **Step 3: `<style>` に特典・ステップ用CSSを追加する**

  ```css
  /* ===== 特典カード ===== */
  .benefit-card {
    display: flex;
    gap: 20px;
    align-items: flex-start;
  }

  .benefit-card__icon {
    font-size: 3rem;
    flex-shrink: 0;
  }

  .benefit-card__title {
    font-size: 1.2rem;
    font-weight: 700;
    margin-bottom: 8px;
    color: var(--color-main);
  }

  .benefit-card__text {
    margin-bottom: 16px;
    font-size: 0.95rem;
  }

  .benefit-list {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 6px;
    font-size: 0.95rem;
  }

  /* ===== ステップ ===== */
  .steps__list {
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .step-item {
    display: flex;
    gap: 20px;
    align-items: flex-start;
    background: var(--color-white);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    padding: 20px 24px;
  }

  .step-item__num {
    flex-shrink: 0;
    width: 44px;
    height: 44px;
    border-radius: 50%;
    background: var(--color-accent);
    color: var(--color-text);
    font-size: 1.3rem;
    font-weight: 900;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .step-item__title {
    font-size: 1rem;
    font-weight: 700;
    margin-bottom: 4px;
  }

  .step-item__text { font-size: 0.9rem; }
  ```

- [ ] **Step 4: ブラウザで確認する**

  - 特典カードが白いカードとして表示されるか
  - ステップが1・2・3と緑の丸数字付きで並ぶか

---

## Task 5: スタンプギャラリー（プレースホルダー対応）

**Files:**
- Modify: `index.html` の `<section id="gallery">` と `<style>`

- [ ] **Step 1: `<section id="gallery">` の中身を追加する**

  ```html
  <section id="gallery" class="section gallery">
    <div class="container">
      <h2 class="section-title">🖼️ スタンプ<span>サンプル</span></h2>
      <p class="gallery__sub">こんなスタンプが作れます！</p>
      <div class="gallery__grid">

        <!-- 画像を追加するときは <div class="gallery__item"> を
             <div class="gallery__item"><img src="assets/stamp-1.png" alt="スタンプサンプル1"></div>
             に差し替えてください -->

        <div class="gallery__item gallery__item--placeholder">🐾</div>
        <div class="gallery__item gallery__item--placeholder">🐶</div>
        <div class="gallery__item gallery__item--placeholder">🐱</div>
        <div class="gallery__item gallery__item--placeholder">🐾</div>
        <div class="gallery__item gallery__item--placeholder">🐶</div>
        <div class="gallery__item gallery__item--placeholder">🐱</div>
      </div>
      <p class="gallery__note">※ 実際のスタンプ画像に順次差し替えます</p>
    </div>
  </section>
  ```

- [ ] **Step 2: `<style>` にギャラリー用CSSを追加する**

  ```css
  /* ===== ギャラリー ===== */
  .gallery { background: #FFF0E6; }

  .gallery__sub {
    text-align: center;
    margin-bottom: 24px;
    font-size: 0.95rem;
    color: #888;
  }

  .gallery__grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
  }

  .gallery__item {
    aspect-ratio: 1;
    border-radius: var(--radius);
    overflow: hidden;
  }

  .gallery__item img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .gallery__item--placeholder {
    background: var(--color-white);
    box-shadow: var(--shadow);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2.5rem;
  }

  .gallery__note {
    text-align: center;
    margin-top: 16px;
    font-size: 0.78rem;
    color: #aaa;
  }
  ```

- [ ] **Step 3: ブラウザで確認する**

  - ギャラリーが3列グリッドで並ぶか
  - 絵文字プレースホルダーが正方形のカードに収まっているか

---

## Task 6: 安心ポイント（FAQ） + 最終CTA

**Files:**
- Modify: `index.html` の `<section id="safety">`・`<section id="final-cta">` と `<style>`

- [ ] **Step 1: `<section id="safety">` の中身を追加する**

  ```html
  <section id="safety" class="section safety">
    <div class="container">
      <h2 class="section-title">💬 よくある<span>ご質問</span></h2>
      <div class="faq-list">

        <div class="faq-item card">
          <p class="faq-item__q">Q. 本当に無料ですか？</p>
          <p class="faq-item__a">A. はい、完全無料です。制作費・送料など一切かかりません。</p>
        </div>

        <div class="faq-item card">
          <p class="faq-item__q">Q. どんな写真でも大丈夫ですか？</p>
          <p class="faq-item__a">A. 愛犬の顔がはっきり写っている写真なら基本的にOKです。</p>
        </div>

        <div class="faq-item card">
          <p class="faq-item__q">Q. スタンプはいつ届きますか？</p>
          <p class="faq-item__a">A. 申請から数営業日以内にLINEスタンプのURLをお送りします。</p>
        </div>

        <div class="faq-item card">
          <p class="faq-item__q">Q. 何回でも申請できますか？</p>
          <p class="faq-item__a">A. お一人さま1回限りの特典となります。</p>
        </div>

      </div>
    </div>
  </section>
  ```

- [ ] **Step 2: `<section id="final-cta">` の中身を追加する**

  ```html
  <section id="final-cta" class="section final-cta">
    <div class="container">
      <div class="final-cta__inner card">
        <p class="final-cta__emoji">🐾</p>
        <h2 class="final-cta__title">愛犬のスタンプを<br>作ってみませんか？</h2>
        <p class="final-cta__text">
          わんグルに口コミを書くだけ。<br>
          かんたん3ステップで受け取れます！
        </p>
        <a href="#" class="btn">
          🐶 口コミを書いてスタンプをもらう
        </a>
      </div>
    </div>
  </section>
  ```

- [ ] **Step 3: `<style>` にFAQ・最終CTA用CSSを追加する**

  ```css
  /* ===== FAQ ===== */
  .faq-list {
    display: flex;
    flex-direction: column;
    gap: 12px;
  }

  .faq-item__q {
    font-weight: 700;
    color: var(--color-main);
    margin-bottom: 6px;
  }

  .faq-item__a { font-size: 0.95rem; }

  /* ===== 最終CTA ===== */
  .final-cta { background: linear-gradient(160deg, #FFE8D6 0%, #FFF8F0 100%); }

  .final-cta__inner {
    text-align: center;
    padding: 48px 32px;
  }

  .final-cta__emoji {
    font-size: 3rem;
    margin-bottom: 16px;
  }

  .final-cta__title {
    font-size: 1.6rem;
    font-weight: 900;
    margin-bottom: 12px;
    line-height: 1.4;
  }

  .final-cta__text {
    font-size: 1rem;
    margin-bottom: 28px;
    color: #666;
  }
  ```

- [ ] **Step 4: ブラウザで確認する**

  - FAQカードが縦に並ぶか
  - 最終CTAカードが中央揃えで大きく表示されるか
  - ボタンが2か所に正しく表示されるか

---

## Task 7: フッター

**Files:**
- Modify: `index.html` の `<footer id="footer">` と `<style>`

- [ ] **Step 1: `<footer id="footer">` の中身を追加する**

  ```html
  <footer id="footer" class="footer">
    <div class="container">
      <p class="footer__logo">🐾 わんグル</p>
      <p class="footer__copy">© 2024 わんグル. All rights reserved.</p>
      <p class="footer__note">
        ※ 本特典はわんグルへの口コミ投稿が条件となります。<br>
        スタンプのデザインは写真の状態により異なる場合があります。
      </p>
    </div>
  </footer>
  ```

- [ ] **Step 2: `<style>` にフッター用CSSを追加する**

  ```css
  /* ===== フッター ===== */
  .footer {
    background: var(--color-text);
    color: rgba(255,255,255,0.85);
    text-align: center;
    padding: 40px 0;
  }

  .footer__logo {
    font-size: 1.2rem;
    font-weight: 700;
    margin-bottom: 8px;
    color: var(--color-white);
  }

  .footer__copy {
    font-size: 0.8rem;
    margin-bottom: 12px;
  }

  .footer__note {
    font-size: 0.75rem;
    line-height: 1.8;
    color: rgba(255,255,255,0.55);
  }
  ```

- [ ] **Step 3: ブラウザで確認する**

  - フッターが濃いブラウン背景で表示されるか
  - 注意書きが薄い文字で表示されるか
  - ページ全体が上から下まで通しで確認できるか

---

## Task 8: レスポンシブ対応 + 全体仕上げ

**Files:**
- Modify: `index.html` の `<style>` と `<script>`

- [ ] **Step 1: `<style>` にスマホ用レスポンシブCSSを追加する**

  ```css
  /* ===== レスポンシブ（スマホ：600px以下） ===== */
  @media (max-width: 600px) {
    .hero__title { font-size: 1.8rem; }
    .hero__btn   { font-size: 1rem; padding: 16px 28px; }

    .benefit-card {
      flex-direction: column;
      align-items: center;
      text-align: center;
    }

    .gallery__grid { grid-template-columns: repeat(2, 1fr); }

    .final-cta__inner { padding: 36px 20px; }
    .final-cta__title { font-size: 1.3rem; }

    .btn { font-size: 0.95rem; padding: 14px 28px; }
  }
  ```

- [ ] **Step 2: `<script>` タグ内にスムーススクロールを追加する**

  ```js
  document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
      const target = document.querySelector(this.getAttribute('href'));
      if (target) {
        e.preventDefault();
        target.scrollIntoView({ behavior: 'smooth' });
      }
    });
  });
  ```

- [ ] **Step 3: ブラウザの幅を狭くしてスマホ表示を確認する**

  ブラウザの開発者ツール（F12）→ スマホアイコンをクリック → iPhone SE（375px幅）で確認：
  - テキストが見切れていないか
  - ボタンが押しやすい大きさか
  - ギャラリーが2列になっているか

- [ ] **Step 4: 全セクションを通しで確認する**

  - ページ上部から下部までスクロールして崩れがないか
  - 全ボタンのhoverエフェクト（浮き上がり）が動くか
  - フォントが Noto Sans JP（丸みのある日本語フォント）になっているか

---

## 完成後のチェックリスト

- [ ] `assets/` にスタンプ画像を追加したら、ギャラリーの `gallery__item--placeholder` を `<img>` タグに差し替える
- [ ] わんグルの口コミページURLが決まったら `href="#"` を正しいURLに更新する
- [ ] スマホ・PC両方で最終確認する
