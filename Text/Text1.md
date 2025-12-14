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