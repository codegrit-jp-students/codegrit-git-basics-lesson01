## ローカルリポジトリの作成

### 1. テスト用のフォルダーを作成する

初期設定が完了したらいよいよGitを実際に使っていきましょう。今回はDesktopにgit_testというフォルダーを作ります。

```bash
$ pwd
/Users/user_name
$ cd Desktop
$ pwd
/Users/user_name/Desktop
$ mkdir git_test
$ cd git_test
```

### 2. `git init`でリポジトリの作成

リポジトリの作成には`git init`というコマンドを利用します。

```bash
$ git init
Initialized empty Git repository in /Users/user_name/Desktop/git_test/.git/
```

このコマンドを実行すると、新しく`.git`というサブディレクトリが作成されます。

## ステータスを確認する

### 1.`git status`で状態を確認

Gitでは`git status`というコマンドを利用していつでもリポジトリの状態を確認することが出来ます。

```bash
$ git status
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)
```

現在は、git_testフォルダーは空なので上記のように表示されます。

### 2. ファイルを作成する

試しに`README.md`というファイルを作成してみましょう。

```bash
$ touch README.md
$ ls
README.md
```

### 3. 再度、`git status`で状態を確認

```bash
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.md

nothing added to commit but untracked files present (use "git add" to track)
```

表示が少し変わりました。ここで`Untracked files:`とあり、その下に先ほど作成した`README.md`があります。これはファイルを作成したもののGitはまだそのファイルの変更を記録する準備が出来ていないことを意味します。

## `git add`でファイルをリポジトリに追加する

### 1. `git add`でファイルをリポジトリに追加する

`README.md`への変更を記録する準備を整えるには`git add`コマンドを利用します。

```bash
$ git add README.md
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   README.md
```

いかがでしょうか。先ほどの`Untracked files:`という項目が消え、代わりに`Changes to be committed:`という項目の中に`README.md`が入りました。これでREADME.mdへの変更をGitが記録していく準備が整いました。

### 2. ファイルに変更を加える

準備が整ったのでファイルに変更を加えてみましょう。

1. ファイルをAtomエディターで開く

```bash
$ atom README.md
```

2. 変更を加えて保存する

以下のテキストを入力して、保存しましょう。

```
# Gitのテスト

## 目的

- Gitを実際に使ってみる。
```

3. ステータスを確認する

```bash
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   README.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md
```

いかがでしょう。今度は、`Changes not staged for commit:`という項目が加わってその下に`"modified:   README.md"`とあります。これはファイルへの変更がまだstage状態にないという意味ですね。

4. 再度、`git add`コマンドを使う

```bash
$ git add README.md
$ git staus
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   README.md
```

さて、再度`git add README.md`というコマンドを入力してからステータスを確認してみました。すると`Changes not staged for commit:`という項目がまた無くなりましたね。何が起こったのでしょうか？

## ステージングエリアとは

Git独特の概念としてステージングというものがあります。このステージングエリアは、ファイルに対して比べた変更をリポジトリに保存する前の段階の場所を指します。この場所があることで、例えばたくさんのファイルを一度に編集した時に一度に全部の変更を記録せず、一部のファイルの変更だけを記録する(コミットするといいます。)ことが出来ます。

例を挙げると、新機能の開発途中でバグを別のファイルで見つけてそのファイルを修正したとします。このときそのファイルだけを`git add 修正したファイル`としてステージングに持っていきコミットすることでバグ修正だけの更新記録を作ることができます。

このように、複数の変更内容を一度にコミットすることで、小さく分けてコミットすることで、プロジェクト全体の動きが見えやすくなります。

## コミットする

### `git commit`

さあ、ファイルの変更をステージングエリアに持ってきて、コミットするする準備が整いました。コミットするには`git commit`というコマンドを使います。

```bash
$ git commit
```

すると、初期設定の際に設定したエディタでメッセージ(**コミットメッセージ**)を編集することが出来ます。

試しに`Add README.md to learn git.`と入れて保存しましょう。

### 再度ステータスを確認する。

保存が完了したら、再びstatusを確認してみましょう。

```bash
$ git status
On branch master
nothing to commit, working tree clean
```

これは、コミットが完了したので現在ステージング状態のファイルも、ステージング前のファイルも何もないことを示しています。