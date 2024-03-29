# Gitの仕組みと基本的なコマンド
* gitはスナップショット（差分ではなくファイルの内容を丸ごと）を記録する
* 最新のコミットが直前のコミットを記録しておくことで以前の状態に戻すことができる

## ローカル環境について
ローカルは３つのエリアに分かれている
1. ワークツリー
2. ステージ
3. リポジトリ

### ワークツリー
自分の手元の作業場のこと。<br>
ファイルを変更する作業場

### ステージ
コミット（スナップショットを記録すること）する変更を準備する場所<br>
Gitではワークツリーで行った変更をステージに一旦追加してから、その後にスナップショットを記録していく。<br>
こうすることで、任意の変更箇所のみ（変更箇所のうち、ステージングしたもののみ）をスナップショットに記録することが可能になる。<br>
ステージへの追加は、`git add`コマンドで行うことができる。

### リポジトリ
スナップショットの保管場所のこと。<br>
ローカルのスナップショットはここに記録し、これをリモートリポジトリにアップロードする。<br>
リポジトリには
* *圧縮ファイル*（ファイルの中身を圧縮したもの）
* *ツリーファイル*（構造や名前を持たない圧縮ファイルに構造を与える）
* *コミットファイル*（いつ、誰が、何を、何のために変更したのかの情報を保存する）<br>
が保管される<br>
ローカルリポジトリにスナップショットを記録するには、`git commit`コマンドを使用する。

## リポジトリの作成

### ローカルリポジトリを新規作成する場合
以下のコマンドを実行することで*.gitディレクトリ*が作成される
```
git init
```

.gitディレクトリには
* 圧縮ファイル
* ツリーファイル
* コミットファイル
* インデックスファイル
* 設定ファイル

などgitで必要なファイルが格納されている

### Gitリポジトリをコピーして作成する場合
```
git clone <リポジトリ名>
```

* リモートリポジトリのファイルがワークツリーにコピーされる
* .gitディレクトリがコピーされる

## 変更をステージに追加する
```
// ファイルを指定して追加
git add <ファイル名>
// ディレクトリを指定して追加
git add <ディレクトリ名>
// 変更をすべて追加
git add .
```
git addを実行することで、
1. 圧縮ファイルがリポジトリに記録され、
2. インデックスファイルがステージに追加される


## ステージに追加した変更をリポジトリに記録（コミット）する
```
git commit
// コミットメッセージを追加できる
git commit -m "<メッセージ>"
// 変更内容を確認できる
git commit -v
```
git commitをすることで
1. ツリーファイル
2. コミットファイル
が作成される

## 現在の変更状況を確認する
```
// 前回ステージに追加してから変更したワークツリーのファイルを表示する
// 前回コミットしてからステージに追加されたファイルを表示する
git status
```

## 変更差分（何を変更したか）を確認する
```
// git addする前の変更差分(ワークツリーとステージの差分)
git diff
git diff <ファイル名>

// git addした後の変更分（ステージとリポジトリの差分）
git diff --staged
```

## 変更履歴を確認する
```
git log
// 変更の要点をまとめて1行で表示する
git log --oneline
// ファイルの変更差分を表示する
git log -p <ファイル名>
// 表示するコミット数を制限する
git log -n <コミット数>
```

## ファイルの削除を記録する
```
// ワークツリーのファイルごと削除
git rm <ファイル名>
git rm -r <ディレクトリ名>

// ワークツリーのファイルは残したいとき
git rm --cached
```

## ファイルの移動（ファイル名の変更）を記録する
```
git mv <旧ファイル>　<新ファイル>

// 以下のコマンドも同じ
mv <旧ファイル> <新ファイル>
git rm <旧ファイル>
git add <新ファイル>
```


## GitHubにプッシュする
### リモートリポジトリを新規追加する
```
// originというショートカットでurlのリモートリポジトリを登録する
// →今後はoriginという名前でリモートにpushしたりpullしたりできるようになる
git remote add origin <githubリポジトリのURL>
```

### リモートリポジトリへ送信（push）する
```
// mainブランチを作成する
git branch -M main
// mainブランチにプッシュする
git push <リモート名> <ブランチ名>
git push origin main
```

※ GitHubにプッシュするときに認証が必要になる。認証に必要なトークンを以下で作成する。

[image:74CF28B0-0FE5-41C8-B9E1-35CFD942B783-58729-0000056CE5735FF2/スクリーンショット 2022-10-13 7.41.01.png]


## 管理しないファイルをGitの管理から外す
管理しないファイルは.*gitignoneファイル*に指定する
```
// 指定したファイルを除外
<ファイル名>
// ルートディレクトリを指定
/<ファイル名>
// ディレクトリ以下を除外
dir/
```





