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
リポジトリ運用で「地味に効く」Tips教えて
## テンプレと自動化
- `.github/ISSUE_TEMPLATE` と `PULL_REQUEST_TEMPLATE.md` を置く（聞きたい情報を先に書かせる）
- `CODEOWNERS` でレビュー担当を自動アサイン
- `CONTRIBUTING.md` に「ブランチ命名/コミット規約/テスト手順」を1ページで
- リリースはタグ + `CHANGELOG.md`（または GitHub Releases）で“何が変わったか”を残す
- 依存更新は `dependabot` か Renovate、CIで `npm audit` / `pip-audit` なども回す

# A6
作業ツリーを汚さずに確認したい
## `git show` と `git range-diff`
- 1コミットだけ眺める: `git show <sha>`
- ブランチの差分を要点だけ: `git log main..feature --oneline`
- リベース前後の変化を見る: `git range-diff origin/main...before origin/main...after`
※ range-diff は “同じ変更が形を変えただけか” を見るのに便利

# A7
雑談：レビュー待ち時間の過ごし方
## 5分でできるやつ
レビュー待ちで手を止めると戻るのが大変なので、「次の1手」をメモしてから席を立つ派。
あとは肩回しと、目を遠くに向けるのだけで体感かなり違う。

# A8
詰まったときの“調査”コマンド集
## まずは証拠集め
- その変更誰が入れた？: `git blame -w <file>`
- その単語どこにある？: `git grep -n "<pattern>"`
- ある時点の状態で動かす: `git switch --detach <sha>`
- いらない生成物を確認: `git clean -ndx`（消すなら `-fdx` は慎重に）
- 設定の差を見る: `git config --show-origin -l`

# A9
レビューを通しやすい差分の作り方
## “読みやすさ”の工夫
- 変更を「機能」と「整形」で混ぜない（整形は別コミット/別PR）
- 先にリネーム、後で中身修正（diffが追いやすい）
- 大きいファイル追加は `git lfs` 検討、もしくは生成手順をREADMEに
- PR説明に「なぜこうしたか」だけ1段落入れる（コードは読めば分かるので）

# A10
間違えたときの戻し方、何を選ぶ？
## reset / revert / restore の使い分け
- 共有ブランチで“なかったことに”したい: 基本 `git revert`（履歴を残して打ち消す）
- ローカルのやり直し: `git reset --soft` / `--mixed` / `--hard`（用途で）
- ファイルだけ戻す: `git restore <file>`（ステージも戻すなら `--staged`）
「誰が使ってる枝か」で選ぶのが一番事故らない。

# A11
PR本文の“別パターン”テンプレ
## そのまま貼れる（チェック式）
- 目的: 
- 変更概要: 
- 影響範囲: 
- リスク/ロールバック: 
- 確認項目:
  - [ ] 単体テスト
  - [ ] 手動確認（手順: ）
  - [ ] 監視/ログ追加（必要なら）

# A12
雑談：集中が切れたときの復帰テク
## 私の小技
「いま触ってる関数名」と「次にやること」を1行だけ残してから別作業に移ると、戻るのが速い。
タイマーを25分で区切るより、私は“45分+5分散歩”の方が合うことが多い。
