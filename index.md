# github Action の使い方

実際に作って動きを確認する

## mkdocs + Material で作る 静的サイト

-1 github の pages で公開できるソース
-1 docker での wwwサーバーで公開するソース
-1 2つを同時に管理できる状態を作る

github で リポジトリを2つ作る
 リポジトリA 更新元のリポジトリ
   メインのリポジトリ となる。
 リポジトリB github pages で公開するリポジトリ
  こちらは リポジトリAの github action で生成・更新される
  こちらのリポジトリは自動更新のため、github からクローンする必要はない

## リポジトリの作成
  -1 リポジトリB を作成
  作成するときに、readme ,gitignore,license などのファイルは作成しない（チェックしない）
  リポジトリは、public で作成しないと、追加料金が発生するので注意する
  
  -1 リポジトリBの所有者の個人用アクセストークンを取得
    * GitHub のページ右上 [プロフィール画像] → [Settings]
    * ページ左側 [Developer settings] をクリック
    * [Personal access tokens] → [Generate new token] をクリック
    * 発行の HMTL フォームで、[note] には文字列を入力
    * [select scopes] で [public_repo] にチェックをつける
    * そして [Generate token] ボタンをクリック
    * 表示された文字列をパスワードマネージャー等に保存しておく

!!! note 
アクセストークンがわかれば、他人のアカウントのリポジトリへのアクセスも可能となる
スコープごとにアクセストークンを作成できる

  -1 個人用アクセストークンをリポジトリAの Secret に登録
     [Settings] → [Secrets] → [New repository secrets]
     新規作成した個人用アクセストークンを Name“PERSONAL_TOKEN” として登録

  -1 リポジトリA にデプロイ用 GitHub Actions ワークフローを追加
    action 内でアクセストークンを呼び出すときに先ほど設定した"PERSONAL_TOKEN"で指定して呼び出すことができる

  -1 GitHub Actions を実行し、デプロイします
     リポジトリBの指定したブランチに対してプッシュされたことを確認します。

  -1 リポジトリAの GitHub Pages を有効にします
     リポジトリA で [Settings] をクリック
      画面を下にスクロールさせ、[GitHub Pages] で [Source] を “master branch” を選択します

  -1 Web ページが実際に表示できるか確認します
     'http(s)://<user>.github.io/<repository>'

     