# 静的ページの作成
- 参考
  - Webホスティング入門: GitHub Pagesで静的ページ作成からデプロイまで
  - https://zenn.dev/bellstone/articles/096114016c3ac6
- レポジトリの作成
- index.htmlの準備
- レポジトリの「settings」→ 「Pages」→ 「Branch」でどこをRootにするかせってする
- 少し時間をおいて再度見ると上の方法「visit site」のボタンが出てくる

# VueでBuildしたファイルをDocs下にコピーするとき
- 以下のようなところが、/assets/になっているとエラーになるので/tenipura/assets/とする
```
<script type="module" crossorigin src="/tenipura/assets/index-D2DNfB8q.js"></script>
<link rel="stylesheet" crossorigin href="/tenipura/assets/index-RqBkh1U7.css" />
```
