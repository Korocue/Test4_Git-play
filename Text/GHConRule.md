メモリ更新案（コネクター前提・修正版）
# 【GitHubコネクター運用ルール】
- 「最新を読んで」だけは禁止。必ず repo と branch を指定する（例: Korocue/Test4_Git-play の Play）。
- ChatGPTはコネクターで branch の HEAD を取得し、回答の冒頭に「読んだ ref と commit SHA」を必ず明記する（例: Play @ d5a888b…）。
- もしユーザーが GitHubサイトで見えている SHA と一致しない／取得が古い場合は、
  1) branch HEAD を取り直す（同一refで再取得）
  2) それでもズレるなら「ユーザー提示SHAを優先して、そのSHAのdiff/patchを読む」
  の順で切り替える。
- 「存在しない」「フォルダが無い」系の断言は、(a)該当branchでのファイル取得、(b)コミット差分、の両方を試してからにする。


ポイントは「コネクターを主系に置いたまま、ズレた時だけSHA固定に落とす」ってこと。全否定じゃなくて フェイルセーフ。

# 君側の対策（コネクターを活かしたまま、事故を潰す）
## 1) 指示テンプレ（これだけで良い）
repo: Korocue/Test4_Git-play
branch: Play
やること: branch HEAD のdiffから Text/Text1.md を読んで。読んだcommit SHAも書いて。

## 2) 「反映遅い/ズレた」時だけ追加する一文（最小）
GitHubサイトで見えてる最新SHAは <ここにSHA>。もしbranch HEADが違うSHAなら、このSHAのdiffを優先して読んで。


これなら普段はコネクターでスムーズ、ズレた時だけ一段ギアを上げられる。