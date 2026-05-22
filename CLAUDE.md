# partner-reviews プロジェクト

外注デザイナー（パートナー）の対応所感をまとめた社内向けサイト（GitHub Pages）。
このファイルは Claude Code 向けのプロジェクト記憶。誰がclone してもClaude Code が同じ動作をするための設計書。

## 公開URL

<https://nakagawa-prog.github.io/partner-reviews/>

## あなた（Claude）の役割

ユーザーが以下のような依頼をしてきたら、規約に従って Markdown を編集し、commit & push してください。

- 「平岡さんに 5/22 青木で追記して。〜内容〜」
- 「新しく田中さん追加して。初回は 5/22 寒竹で〜内容〜」
- 「西嶋さんのタブ消して」
- 「平岡さんの 5/18 のTier確度を ◯ に変更して」

実行フローは常に: **Markdown編集 → git add → git commit → git push**

push まで完了したら、反映タイミング（30秒〜1分後）を伝える。

## プロジェクト構成

```
partner-reviews/
├── index.html        # タブ切替UI + Markdownレンダラ + GitHub API自動列挙
├── CLAUDE.md         # このファイル
├── README.md         # メンバー向けブラウザ編集マニュアル
└── partners/
    ├── hiraoka.md    # 平岡さん（先頭に <!-- 平岡さん --> コメント）
    ├── nishijima.md  # 西嶋さん
    └── shimizu.md    # 清水さん
```

**重要**: `partners.json` は存在しない。タブ一覧は `index.html` 内の JS が GitHub Contents API で `partners/` 配下の .md を自動列挙する。タブ名は各 .md 先頭の `<!-- 表示名 -->` から自動抽出される。

## 既存パートナーへの追記フォーマット

各 .md は `## YYYY/MM/DD ライター名` 見出しで時系列に区切る。新しい所感は **ファイル先頭（`<!-- 表示名 -->` コメントの直後）に追加**する（最新が上になるよう降順）。

```markdown
## 2026/MM/DD ライター名

### 6月末までのTier1,2確度

<p class="tier-mark"><span class="tier-icon tier-yes"></span></p>

### 成果物のクオリティについて
（本文）

### 対応スピードについて
...

### 意思疎通のしやすさについて
...

### そのほか自由になんでも
...

### パートナー担当記事リリースURL
- ...
```

「6月末までのTier1,2確度」の直下、アイコンの後にユーザーがTier判断の補足を述べる場合は、`### 成果物のクオリティについて` の前に普通の段落として記述する。

## Tier 確度アイコン記法

| 値 | クラス | 図形・色 |
| --- | --- | --- |
| ◯ | `tier-icon tier-yes` | 円・ピンク |
| △ | `tier-icon tier-maybe` | 三角・黄色 |
| × | `tier-icon tier-no` | バツ・ブルー |

複数値（例: △〜◯）は `<span class="tier-tilde">〜</span>` で繋ぐ：

```html
<p class="tier-mark"><span class="tier-icon tier-maybe"></span><span class="tier-tilde">〜</span><span class="tier-icon tier-yes"></span></p>
```

## 新規パートナー追加時

1. `partners/{id}.md` を新規作成（id はローマ字小文字。例: `tanaka.md`）
2. **必ず1行目に `<!-- 田中さん -->` のコメントを書く**（これがタブ名になる）
3. その後、通常の追記フォーマットで初回所感を記述
4. JSON 編集は不要（自動列挙のため）

タブの並び順はファイル名のアルファベット順。

## 反映フロー

ローカルで編集 → `git add` → `git commit -m "..."` → `git push` → GitHub Pages が30秒〜1分で再ビルドして反映。

コミットメッセージは「平岡さん 2026/5/22 にTier確度の補足を追記」のように、誰の・いつの・何の更新かわかる形にする。

## ローカル動作確認方法

index.html は GitHub Contents API でリモートのファイル一覧を取得するため、未push分はローカルでも一覧に出ない。push 後に GitHub Pages で確認する。

ローカルで一応動かしたい場合：

```bash
python3 -m http.server 8765
```

→ http://localhost:8765/ （ただし表示されるのはリモートの最新 push の内容）

## 注意

- Publicリポジトリだが `<meta name="robots" content="noindex, nofollow">` で検索エンジン除外
- パートナー個人名・社内Tier評価・記事プレビューURL等を掲載しているため機密扱い
- URL は部署内（Chatwork）のみで共有
- GitHub Contents API は未認証で IP 単位 60req/h のレートリミット。小規模チームなら問題なし

## Collaborators（編集権限あり）

- nakagawa-prog（admin）
- aoki-yukihiro（write、2026/5/21招待承諾済み）

新しいメンバーを追加する場合は admin が `gh api repos/nakagawa-prog/partner-reviews/collaborators/{username} -X PUT -f permission=push` で招待する。
