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