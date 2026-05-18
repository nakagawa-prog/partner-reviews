# パートナー対応所感

外注デザイナー（パートナー）の対応所感をパートナー別にまとめるサイトです。
週次で追記更新します。

## 構成

```
partner-reviews/
├── index.html        # タブ切替UI（ブラウザで開くか GitHub Pages で公開）
├── partners.json     # パートナー一覧（タブの並び順を管理）
├── partners/
│   ├── hiraoka.md    # 平岡さん
│   ├── nishijima.md  # 西嶋さん
│   └── shimizu.md    # 清水さん
└── README.md
```

## 閲覧方法

- GitHub Pages 公開後: `https://<user>.github.io/partner-reviews/`
- ローカル: `index.html` をブラウザで開く（パートナーのMarkdownは `fetch` で読み込むため、ファイルプロトコルだと CORS でエラーになる可能性があります。その場合は `python3 -m http.server` などで簡易サーバを立てて閲覧してください）

## 更新方法（Claude に依頼するとき）

各パートナーの所感は、`## YYYY/MM/DD ライター名` 見出しで時系列に区切られます。
新しい所感は **下に追記** されていきます（最新が一番下、ではなく時系列の下に積む形）。

### 既存パートナーに追記する

> 平岡さんに 5/25 寒竹で追記して。
> （以下、追記内容）

→ `partners/hiraoka.md` の末尾に
```
## 2026/05/25 寒竹

### 6月末までのTier1,2確度

<p class="tier-mark"><span class="tier-icon tier-yes"></span></p>

### 成果物のクオリティについて
...
```
の形で追加されます。

**Tier確度のアイコン記法（参考）**

| 値 | クラス | 図形 | 色 |
| --- | --- | --- | --- |
| ◯ | `tier-icon tier-yes` | 円 | ピンク |
| △ | `tier-icon tier-maybe` | 三角 | 黄色 |
| × | `tier-icon tier-no` | バツ | ブルー |

複数値（例: △〜◯）は `<span class="tier-tilde">〜</span>` で繋ぐ。

### 新しいパートナーを追加する

> 新しく田中さん追加して、初回は 5/20 青木で。
> （以下、所感内容）

→ `partners/tanaka.md` が作成され、`partners.json` のタブ一覧にも自動追加されます。

### URL を伏せる / 表現を変える

> 平岡さんの記事URL部分を伏せて

→ 該当 Markdown を直接編集します。元データはこのリポジトリのみに残るため、表示を変えても情報は失われません。

## ホスティング

- GitHub: Public リポジトリ（Free プランのため Private + Pages 不可）
- 公開ページは `<meta name="robots" content="noindex, nofollow">` を入れて検索エンジンに載らないようにしています
- URL を不用意に共有しないこと
