# A1
やっほールシフォン元気？
# A2
じゃあ今日の日付を教えて？
# A3
amendのやり方をもう一度まとめて教えて欲しいな？
## amendまとめ（メッセージ変えないなら）
git add ... → git commit --amend --no-edit → 既にpush済みなら git push --force-with-lease
# A4
ハードリセットまとめについての以下の内容をレビューしてください
## gitの更新を元に戻して、やり直したい場合
git reset --hard <コミットID>
git push --force-with-lease origin <ブランチ名>
## 流れは合ってる。ただ“事故防止の1行”を足すと完成度上がる。
おすすめ版（最小で安全寄り）：
git switch <ブランチ名>
git branch backup/<ブランチ名>-before-rewrite
git reset --hard <コミットID>
git push --force-with-lease origin <ブランチ名>
ポイントは、これは 履歴を書き換えるので --force-with-lease が必要、ってことだけは明記しとくと初心者向けに優しい。

# A5
リポジトリに関するTipsをもう少し教えて！
## 運用のコツ（軽め）
- READMEは「目的 / セットアップ / 動かし方 / よくある詰まり」を最短で辿れる構成にする
- 変更の単位は小さめにして、コミットメッセージは “何をしたか” が一行で分かるようにする（例：`fix: ...` / `docs: ...`）
- PRには「変更点 / 影響範囲 / 確認手順（コマンドや画面操作）」を必ず書く
- 破壊的になりがちな操作（`reset --hard` / `rebase` / `push --force-with-lease`）は、実行前に `git status` と `git branch backup/...` を挟む
- `.gitignore` は「生成物・秘密・環境依存」を最初に固めておく（`node_modules`、`.env`、`dist` など）

# A6
「このブランチだけ別フォルダで同時に開きたい」って時、どうする？
## `git worktree` 小ワザ
同じリポジトリを別ディレクトリに“もう1個チェックアウト”できるやつ。
例えば main を触りつつ、別作業のブランチも同時に開きたい時に便利。

例：
- `git worktree add ../myrepo-feature feature/something`
- 作業が終わったら `git worktree remove ../myrepo-feature`

# A7
適当な雑談でもいい？
## 雑談
作業中のBGMって何派？
歌詞ありだと集中できない人もいるけど、私は「慣れてるアルバムを小さめ音量で流す」か「雨音（環境音）」が一番ミスらない気がする。

# A8
困ったときの “最初に見る” コマンド集、置いとくね
## まずはここから
- いま何が起きてる？：`git status`
- 直近の履歴確認：`git log --oneline --decorate -n 15`
- 差分確認：`git diff`（ステージ済みは `git diff --staged`）
- どのブランチ？：`git branch --show-current`
- 直前の操作を取り消したい：`git reflog`（困ったらここ、だいたい助かる）
