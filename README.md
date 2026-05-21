# パートナー対応所感

外注デザイナー（パートナー）の対応所感をパートナー別にまとめるサイトです。
週次で追記更新します。

公開URL: <https://nakagawa-prog.github.io/partner-reviews/>

## 構成

```
partner-reviews/
├── index.html        # タブ切替UI（GitHub Pages で公開）
├── partners/
│   ├── hiraoka.md    # 平岡さん（先頭に <!-- 平岡さん --> コメント）
│   ├── nishijima.md  # 西嶋さん
│   └── shimizu.md    # 清水さん
└── README.md
```

タブの並びは **ファイル名のアルファベット順**。表示名は各 .md 先頭の HTMLコメント `<!-- ◯◯さん -->` から自動取得します。

## メンバー向け編集マニュアル（aoki-yukihiro 等）

### 既存パートナーに追記する

1. 対象パートナーの .md を開く
   - 平岡さん: <https://github.com/nakagawa-prog/partner-reviews/blob/main/partners/hiraoka.md>
   - 西嶋さん: <https://github.com/nakagawa-prog/partner-reviews/blob/main/partners/nishijima.md>
   - 清水さん: <https://github.com/nakagawa-prog/partner-reviews/blob/main/partners/shimizu.md>
2. 右上の鉛筆アイコン（Edit）をクリック
3. ファイルの末尾に以下のテンプレを貼って書き換える
   ```
   ## 2026/MM/DD ライター名

   ### 6月末までのTier1,2確度

   <p class="tier-mark"><span class="tier-icon tier-yes"></span></p>

   ### 成果物のクオリティについて
   （本文）

   ### 対応スピードについて
   （本文）

   ### 意思疎通のしやすさについて
   （本文）

   ### そのほか自由になんでも
   （本文）

   ### パートナー担当記事リリースURL
   - 記事URL: ...
   ```
4. 下にスクロール → 緑の「Commit changes…」→「Commit changes」
5. 30秒〜1分でサイトに反映

### 新しいパートナーを追加する

1. 👉 <https://github.com/nakagawa-prog/partner-reviews/new/main/partners> を開く
2. 「Name your file」に `tanaka.md`（苗字をローマ字小文字で、半角英字のみ）
3. 「Edit new file」エリアに以下を貼り付け、内容を書き換え
   ```
   <!-- 田中さん -->

   ## 2026/MM/DD ライター名

   ### 6月末までのTier1,2確度

   <p class="tier-mark"><span class="tier-icon tier-yes"></span></p>

   ### 成果物のクオリティについて
   （本文）

   ### 対応スピードについて
   （本文）

   ### 意思疎通のしやすさについて
   （本文）

   ### そのほか自由になんでも
   （本文）

   ### パートナー担当記事リリースURL
   - 記事URL: ...
   ```
4. 下にスクロール →「Commit new file」
5. 30秒〜1分でタブが追加される

**重要**: 1行目の `<!-- 田中さん -->` がタブ名になります。これを忘れるとファイル名（`tanaka`）が表示されます。

### Tier確度アイコン記法

| 値 | コピペ用 |
| --- | --- |
| ◯（ピンク） | `<p class="tier-mark"><span class="tier-icon tier-yes"></span></p>` |
| △（黄色） | `<p class="tier-mark"><span class="tier-icon tier-maybe"></span></p>` |
| ×（ブルー） | `<p class="tier-mark"><span class="tier-icon tier-no"></span></p>` |
| △〜◯ | `<p class="tier-mark"><span class="tier-icon tier-maybe"></span><span class="tier-tilde">〜</span><span class="tier-icon tier-yes"></span></p>` |

## ホスティング

- GitHub: Public リポジトリ（Free プランのため Private + Pages 不可）
- 公開ページは `<meta name="robots" content="noindex, nofollow">` を入れて検索エンジンに載らないようにしている
- URL は部署内（Chatwork）のみで共有すること

## 技術メモ

- タブ一覧は GitHub Contents API（`/repos/.../contents/partners`）で動的に取得
- 未認証なので IP 単位 60req/h のレートリミットあり。小規模チームなら問題なし
- ローカル確認時は `python3 -m http.server` で立ち上げてブラウザで http://localhost:8000/ を開く
