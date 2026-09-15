# パチスロ実データ解析ラボ

パチスロ機種横断の実データ解析記事シリーズの紹介サイト。各記事の要約・紹介をここに掲載し、
検証内容の詳細・本文はnote記事へ誘導する「ハブ型」構成の静的サイト。

## サイト構成

- `index.html` — トップページ(導入文 → 記事紹介カード → ホブゴブリンのプロフィール/About → フッター)
- `notice.html` — コンプライアンス表記の詳細ページ(年齢制限・ギャンブル依存症への注意・実店舗名非掲載・特定商取引法表示等)
- `assets/css/style.css` — 共通スタイルシート(フレームワーク不使用)
- `assets/images/` — 画像アセット(記事見出し画像・favicon元画像等)
- `robots.txt` / `sitemap.xml` — 検索エンジン向け設定

フレームワーク・ビルドツールは使用していない素のHTML/CSSのみの静的サイト。ページ数が少ないため、ビルドスクリプトは持たせていない。

## 記事の追加方法(今後、他機種の記事が増えた場合)

`index.html` の `<div class="article-list">` 内にある `<article class="article-card">...</article>` ブロックを
まるごとコピーし、以下を差し替えて追加するだけでよい(JSON化やテンプレートエンジンの追加実装は不要)。

- `.article-card-media img` の `src`(見出し画像)・`alt`
- `.article-tag`(データ規模等の一言タグ)
- `<h3>`(記事タイトル)
- `.article-summary`(一言サマリー)
- `.article-points` 内の `<li>`(読みどころの箇条書き)
- `.btn-primary` の `href`(該当note記事のURL)

記事本文(有料部分・無料部分とも)はnote側を正とし、サイト側には要約・紹介のみを持たせる(二重管理しない)。

## デザイン方針

見出し画像(`assets/images/title-banner.png`、note記事の見出し画像を流用)のトーンに合わせた
トロピカル・沖縄モチーフ(ティール×ゴールドのグラデーション、波形の区切り、ハイビスカスを想起させる差し色)。

## ローカルでの確認方法

ビルド不要の静的ファイルのため、リポジトリ直下で簡易サーバーを立てて確認できる。

```bash
python3 -m http.server 8080
# http://localhost:8080/ にアクセス
```

## GitHub Pages

- 公開方法: GitHub Actions(`.github/workflows/deploy.yml`)が `main` へのpushをトリガーに
  リポジトリ直下をそのままPagesアーティファクトとしてアップロード・デプロイする(ビルド手順なし)。
- 独自ドメイン: `https://slotrealdata.com/`(取得・移行済み。リポジトリ直下の `CNAME` ファイルとGitHub Pages設定〔`cname`〕で紐付け)
- 旧URL(GitHub Pages・ドメイン未設定時代): `https://nattuuuzamiurai.github.io/slot-realdata-lab-site/`(現在は使用していない)

### 独自ドメイン移行の実施状況

- `index.html` / `notice.html` / `glossary.html` / `how-to-read.html` / `trust.html` / `faq.html` の `<link rel="canonical">`、`og:url`、`og:image` を新ドメインに更新済み
- `robots.txt` の `Sitemap:` 行、`sitemap.xml` の各 `<loc>` を新ドメインに更新済み
- DNS設定(レジストラ側でのAレコード/CNAME設定)は別途完了が必要(運営者側の作業)

## ブランド・コンプライアンス制約

- 断定的な的中率・回収率の保証表現、必勝法を思わせる煽り文句は使わない
- 実店舗名・台番号は掲載しない
- 年齢制限・ギャンブル依存症への配慮を欠かさない(`notice.html` に詳細掲載)
