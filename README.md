# Git入門

## 目的

- バージョン管理の重要性を知る
- Gitの基本を知る
- Gitlabのアカウントを作成し、CodeGritでの学習に備える

## 前提知識

このレッスンはコマンドライン入門を完了していることを前提としています。

## バージョン管理とは

バージョン管理とは、ファイルの時間ごとの変更を保存し、後からその変更を確認したり、以前の状態を復元することの出来る仕組みのことです。プログラマーが使うことが多いですが、実際にはビジネスでのドキュメントの管理などでも威力を発揮します。例えば求人サービスを運営するWantedly社では契約書の管理にGitを利用しています。

[GitHubを使って法務コミュニケーションのスピードを2倍にした話](https://www.wantedly.com/companies/wantedly/post_articles/30679)

## バージョン管理の重要性

バージョン管理を利用せずにファイルを編集するのには危険が伴います。例えば、Webサイトに新しい追加をしたい時を考えてみましょう。この時バージョンを行わずにサイトの変更を行ったところ重大なエラーがありサイト自体が動かなくなってしまいました。どう対応するでしょうか？バージョン管理をしていない場合、どうにかして今あるサイトを修正するしかありませんが、時間が経つにつれてサイト利用者からはクレームが入り、経営者からも早く修正するよう圧力が加わります。こんなストレスのかかる環境で仕事すると、エラー原因も中々見つかりません。バージョン管理をきちんとしていれば、一旦ちゃんと動いていたバージョンに戻してから、ゆっくりエラー原因の確認と修正を行うことが出来ます。このようにバージョン管理は、実際的な場面でとても重要になってくるのです。

## リポジトリとは

バージョン管理システムにおいて、変更の情報を保存している場所をリポジトリと呼びます。特に自分のパソコン内にあるリポジトリをローカルリポジトリ、外部にあるリポジトリのことをリモートリポジトリと呼びます。

## Gitとは

Gitは世界で最も普及しているバージョン管理システムです。Gitを利用することで、自分のローカル環境でバージョン管理が簡単に行える他、数人規模のチームから、数百人、数千人という大規模のチームまで一つのプロジェクトの開発に一度に関わることが可能です。

## Gitをインストールする

文章だけ読んでも理解が大変かと思いますのでまずは使ってみましょう。Gitは以下のページからダウンロードすることが出来ます。なおWindowsでPowerShellを使う場合の方法はこの項目の後に出てきます。

1. Gitインストーラーのダウンロード

[Git - Downloads](https://git-scm.com/downloads)

![Gitのインストール1](../images/install_git1.png) 

2. インストール

ファイルのダウンロードが完了したら、ダウンロードしたファイルを解凍して出てきたファイルをクリックします。指示に従って進むとインストール完了です。

**Windowsの場合**
Windowsの場合は途中の画面で"Adjusting your PATH environment"という項目が出てきます。ここでは、"Use Git from Git Bash only"を選んで下さい。

3. 確認する

インストールが完了したらターミナルを起動して確認してみましょう。(結果表示はインストールしたバージョンによって異なります。)

**Windowsの場合**
Windowsの場合は"git bash"というアプリをAdministrator権限で開く必要があります。検索ツールでgitと入れると"git bash"が出てくるはずですので、右クリックで"Run as administrator"を選んで起動します。

```bash
$ git --version
git version 2.12.2
```

### WindowsのPowerShellでGitを使う

WindowsのPowerShellでGitを利用する際にはパッケージマネージャーChocolateyを利用します。(Chocolateyのインストール方法については、準備コースのPowerShellのテキストを参考にしてください。)

```bash
$ choco install 
$ git --version
```

## Gitの初期設定

Gitのインストールが完了したら初期設定を行いましょう。設定にはコマンドラインを利用します。

### 利用者の名前を設定する

```bash
$ git config --global user.name "自分の名前"
```

### 利用者のメールアドレスを設定する

```bash
% git config --global user.name "自分の名前"
```

### デフォルトのエディタを設定する

- nanoを利用する

コマンドライン入門で紹介したエディタnanoを利用するには以下のように入力します。

```bash
$ git config --global core.editor "nano -w"
```

- Atomを利用する

既にAtom入門を完了して、コマンドラインからAtomを使える状態でしたら以下のコマンドでAtomをデフォルトのエディタに設定しましょう。

```bash
$ git config --global core.editor "atom --wait"
```

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

## gitでの開発フローの基本

さて、実はここまでで既にgitでの開発フローを既に一通り実践してきました。gitでの開発フローはこれまで行ったように、

1. ファイルに変更を加える
2. `git add`でステージングエリアに変更されたファイルを移動する
3. `git commit`でステージングエリアのファイルを記録する

という流れを繰り返し行います。

## 再度同じフローを試してみよう

### 1. ファイルに変更を加える

さて、先ほどのファイルに再度変更を加えてみましょう。以下のテキストを追加してから保存して下さい。

```
- Gitでの開発フローを実践する。
- Gitlabのアカウントを作って、CodeGritでの学習に備える。
```

### 2. `git add`でステージングエリアに移動する

`git add`でステージングエリアに再度変更したファイルを移動します。

```bash
$ git add README.md
```

### 3. `git commit`で変更をコミットする

ステージングエリアにあるファイルをコミットします。

```bash
$ git commit -m "Update README.md"
[master d26cca1] Update README.md
 1 file changed, 2 insertions(+)
```

ここで`-m`というオプションの後に"Update README.md"という文章を付けました。このように、コミットメッセージをエディタで編集せずに入力することも出来ます。

## `git log`でgitへのコミットの履歴を見る

さて、ここまでで２回リポジトリへのコミットを行いました。今度はこれらのコミットの歴史を振り返って見ましょう。これには`git log`というコマンドを利用します。

```bash
$ git log
commit d26cca1a7913a69cba66e942aa94e66fed2acfbf
Author: あなたの名前 <あなたのメールアドレス>
Date:   Fri Dec 8 22:38:26 2017 +0800

    Update README.md

commit 13a5782000665111930028612e42195ce32d60dc
Author: あなたの名前 <あなたのメールアドレス>
Date:   Fri Dec 8 22:18:29 2017 +0800

    Add README.md to learn git.
```

このように、`git log`を利用することで、コミットの歴史をコミットメッセージや、コミットした人の名前、メールアドレス、時間と一緒に振り返ることが出来ます

## Sourcetreeアプリケーションを利用しよう

さて、`git log`でコミットの歴史を見ましたが、Sourcetreeというアプリケーションを使うと、こうしたログをより分かりやすくみることが出来ます。

### 1. Sourcetreeをインストールする

以下のURLからSourcetreeをダウンロードし、ダウンロードしたファイルを解凍して、インストールを行って下さい。

https://ja.atlassian.com/software/sourcetree

### 2. Sourcetreeにgit_testディレクトリを紐付ける

インストールが完了したらアプリケーションを開いてみましょう。

![Sourcetree1](../images/sourcetree1.png)

すると上記の画像のような画面が出て来ると思いますので、git_testのフォルダをこの点線部分の中にドラッグしてみましょう。

![Sourcetree2](../images/sourcetree2.png)

これで無事紐付けが完了しました。

### 3.ログを見てみる

紐付けが完了したら、git_testの部分をダブルクリックして見て下さい。すると次のような画面が開きます。

![Sourcetree3](../images/sourcetree3.png)

ここでコミットメッセージが並んだ部分をクリックすると、下のパネルでどのような変更が行われたのかを簡単に見ることが出来ます。

## まとめ

いかがだったでしょか。最初はちょっととっつきにくいかもしれませんが、Gitの開発フローを繰り返し使っていけば慣れていくはずです。また今回紹介したのはGitのコマンドの一部です。これからCodeGritで学習を進めていく上で、マージやブランチなど新しい概念も紹介していきます。

## 更に学ぼう

### 本で学ぶ

- [Pro Git](https://git-scm.com/book/ja/v2)

Git公式サイト内にPro Gitという書籍が無料で公開されています。日本語版なので読みやすいはずです。

### 記事で学ぶ

- [Become a Git Guru](https://www.atlassian.com/git/tutorials)

### インタラクティブに学ぶ

- [tryGit](https://try.github.io/levels/1/challenges/1)
- [Progate](https://prog-8.com/languages/git)

### 動画で学ぶ

- [git入門 - ドットインストール](https://dotinstall.com/lessons/basic_git)