# Gitコマンドチートシート

## 📋 目次
- [初期設定](#初期設定)
- [リポジトリの作成](#リポジトリの作成)
- [基本操作](#基本操作)
- [ブランチ操作](#ブランチ操作)
- [リモートリポジトリ](#リモートリポジトリ)
- [履歴の確認](#履歴の確認)
- [変更の取り消し](#変更の取り消し)
- [一時退避](#一時退避)
- [便利なコマンド](#便利なコマンド)
- [トラブルシューティング](#トラブルシューティング)

---

## 初期設定

### ユーザー情報の設定
```bash
# 名前を設定
git config --global user.name "あなたの名前"

# メールアドレスを設定
git config --global user.email "your.email@example.com"

# 設定を確認
git config --list
```

### エディタの設定
```bash
# VS Codeを使用する場合
git config --global core.editor "code --wait"

# Vimを使用する場合
git config --global core.editor "vim"
```

### 改行コードの設定
```bash
# Windows
git config --global core.autocrlf true

# Mac/Linux
git config --global core.autocrlf input
```

---

## リポジトリの作成

### 新規リポジトリの作成
```bash
# 現在のディレクトリをGitリポジトリにする
git init

# 指定したディレクトリに新規リポジトリを作成
git init プロジェクト名
```

### 既存リポジトリのクローン
```bash
# リモートリポジトリを複製
git clone https://github.com/ユーザー名/リポジトリ名.git

# 別の名前でクローン
git clone https://github.com/ユーザー名/リポジトリ名.git 新しい名前
```

---

## 基本操作

### 状態の確認
```bash
# 変更されたファイルを確認
git status

# 簡潔な表示
git status -s
```

### ステージングエリアへの追加
```bash
# 特定のファイルを追加
git add ファイル名

# すべての変更を追加
git add .

# すべての変更を追加（削除も含む）
git add -A

# 対話的に追加
git add -p
```

### コミット
```bash
# ステージングエリアの変更をコミット
git commit -m "コミットメッセージ"

# addとcommitを同時に実行（追跡済みファイルのみ）
git commit -am "コミットメッセージ"

# エディタでコミットメッセージを編集
git commit

# 直前のコミットを修正
git commit --amend
```

### 差分の確認
```bash
# ワーキングディレクトリとステージングエリアの差分
git diff

# ステージングエリアと最新コミットの差分
git diff --staged

# 特定のファイルの差分
git diff ファイル名

# ブランチ間の差分
git diff ブランチ1 ブランチ2
```

### ファイルの削除・移動
```bash
# ファイルを削除（Gitと実ファイルの両方）
git rm ファイル名

# Gitの追跡のみ削除（実ファイルは残す）
git rm --cached ファイル名

# ファイルの移動・リネーム
git mv 元のファイル名 新しいファイル名
```

---

## ブランチ操作

### ブランチの作成・切り替え
```bash
# ブランチの一覧表示（*が現在のブランチ）
git branch

# すべてのブランチを表示（リモートも含む）
git branch -a

# 新しいブランチを作成
git branch ブランチ名

# ブランチを作成して切り替え
git checkout -b ブランチ名
# または
git switch -c ブランチ名

# ブランチを切り替え
git checkout ブランチ名
# または
git switch ブランチ名
```

### ブランチの削除
```bash
# マージ済みブランチを削除
git branch -d ブランチ名

# 強制削除（マージされていなくても削除）
git branch -D ブランチ名

# リモートブランチを削除
git push origin --delete ブランチ名
```

### マージ
```bash
# 現在のブランチに指定ブランチをマージ
git merge ブランチ名

# Fast-forwardマージを禁止（必ずマージコミットを作成）
git merge --no-ff ブランチ名

# マージを中止
git merge --abort
```

### リベース
```bash
# 現在のブランチを指定ブランチにリベース
git rebase ブランチ名

# 対話的リベース（コミットを整理）
git rebase -i HEAD~3

# リベースを中止
git rebase --abort

# リベース続行
git rebase --continue
```

---

## リモートリポジトリ

### リモートの管理
```bash
# リモートリポジトリの一覧表示
git remote -v

# リモートリポジトリを追加
git remote add origin https://github.com/ユーザー名/リポジトリ名.git

# リモートリポジトリの情報を表示
git remote show origin

# リモートリポジトリのURLを変更
git remote set-url origin https://github.com/ユーザー名/リポジトリ名.git

# リモートリポジトリを削除
git remote remove origin
```

### プッシュ
```bash
# リモートブランチにプッシュ
git push origin ブランチ名

# 初回プッシュ時（上流ブランチを設定）
git push -u origin ブランチ名

# すべてのブランチをプッシュ
git push --all

# タグをプッシュ
git push --tags

# 強制プッシュ（危険！）
git push -f origin ブランチ名
```

### プル・フェッチ
```bash
# リモートの変更を取得してマージ
git pull origin ブランチ名

# リモートの変更を取得してリベース
git pull --rebase origin ブランチ名

# リモートの変更を取得のみ（マージしない）
git fetch origin

# すべてのリモートブランチを取得
git fetch --all
```

---

## 履歴の確認

### コミット履歴
```bash
# コミット履歴を表示
git log

# 1行で表示
git log --oneline

# グラフ表示
git log --graph --oneline --all

# 詳細な差分付きで表示
git log -p

# 最新のn件のみ表示
git log -n 5

# 特定期間のコミット
git log --since="2025-01-01" --until="2025-01-31"

# 特定ユーザーのコミット
git log --author="ユーザー名"

# ファイルの履歴
git log -- ファイル名
```

### 特定コミットの確認
```bash
# コミットの詳細を表示
git show コミットハッシュ

# 特定ファイルの特定コミットを表示
git show コミットハッシュ:ファイル名
```

### 誰が変更したか確認
```bash
# ファイルの各行の最終更新者を表示
git blame ファイル名

# 特定の行範囲のみ表示
git blame -L 10,20 ファイル名
```

---

## 変更の取り消し

### ワーキングディレクトリの変更を取り消し
```bash
# 特定ファイルの変更を取り消し
git checkout -- ファイル名
# または
git restore ファイル名

# すべての変更を取り消し
git checkout -- .
# または
git restore .
```

### ステージングエリアから取り消し
```bash
# ステージングを取り消し（変更は保持）
git reset HEAD ファイル名
# または
git restore --staged ファイル名

# すべてのステージングを取り消し
git reset HEAD
```

### コミットの取り消し
```bash
# 直前のコミットを取り消し（変更は保持）
git reset --soft HEAD^

# 直前のコミットを取り消し（ステージングも取り消し、変更は保持）
git reset --mixed HEAD^
# または
git reset HEAD^

# 直前のコミットを完全に取り消し（変更も削除）
git reset --hard HEAD^

# 特定のコミットまで戻る
git reset --hard コミットハッシュ

# コミットを打ち消す新しいコミットを作成（安全）
git revert コミットハッシュ
```

### 特定のコミットを適用
```bash
# 他のブランチの特定コミットを現在のブランチに適用
git cherry-pick コミットハッシュ

# 複数のコミットを適用
git cherry-pick コミットハッシュ1 コミットハッシュ2
```

---

## 一時退避

### 変更の一時保存
```bash
# 変更を一時退避
git stash

# メッセージ付きで退避
git stash save "作業中の機能"

# 追跡されていないファイルも含めて退避
git stash -u
```

### 退避した変更の管理
```bash
# 退避リストを表示
git stash list

# 最新の退避を適用（退避は残る）
git stash apply

# 特定の退避を適用
git stash apply stash@{2}

# 最新の退避を適用して削除
git stash pop

# 退避の内容を表示
git stash show

# 退避を削除
git stash drop stash@{0}

# すべての退避を削除
git stash clear
```

---

## 便利なコマンド

### タグ
```bash
# タグの一覧表示
git tag

# 軽量タグを作成
git tag v1.0.0

# 注釈付きタグを作成
git tag -a v1.0.0 -m "バージョン1.0.0リリース"

# 特定のコミットにタグを付ける
git tag v1.0.0 コミットハッシュ

# タグを削除
git tag -d v1.0.0

# タグをプッシュ
git push origin v1.0.0

# すべてのタグをプッシュ
git push origin --tags
```

### エイリアス
```bash
# よく使うコマンドに短縮名を設定
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.graph 'log --graph --oneline --all'
```

### その他の便利コマンド
```bash
# 変更があるファイルの一覧
git diff --name-only

# コミットされていない変更をすべて削除
git clean -fd

# マージ済みのブランチを一覧表示
git branch --merged

# マージされていないブランチを一覧表示
git branch --no-merged

# ファイルの検索
git grep "検索文字列"

# リポジトリのサイズを最適化
git gc
```

---

## トラブルシューティング

### よくある問題と解決法

#### コンフリクトの解決
```bash
# 1. コンフリクトしているファイルを確認
git status

# 2. ファイルを編集してコンフリクトマーカーを削除

# 3. 解決したファイルをステージング
git add ファイル名

# 4. マージを完了
git commit
```

#### 間違ったブランチで作業してしまった
```bash
# 変更を退避
git stash

# 正しいブランチに移動
git checkout 正しいブランチ名

# 変更を戻す
git stash pop
```

#### コミットメッセージを間違えた
```bash
# 直前のコミットメッセージを修正
git commit --amend -m "正しいメッセージ"
```

#### プッシュ済みのコミットを取り消したい
```bash
# revertで打ち消しコミットを作成（安全）
git revert コミットハッシュ
git push origin ブランチ名
```

#### 間違えてファイルを削除した
```bash
# 最新のコミットから復元
git checkout HEAD ファイル名

# 特定のコミットから復元
git checkout コミットハッシュ ファイル名
```

#### リモートブランチを誤って削除した
```bash
# reflogで削除前のコミットを確認
git reflog

# ブランチを復元
git checkout -b ブランチ名 コミットハッシュ
git push origin ブランチ名
```

---

## 🔥 危険なコマンド（使用注意）

```bash
# すべての変更を強制的に破棄
git reset --hard HEAD

# 強制プッシュ（他の人の作業を上書き）
git push -f origin ブランチ名

# 追跡されていないファイルを強制削除
git clean -fd

# リモートの状態に強制的に合わせる
git fetch origin
git reset --hard origin/main
```

⚠️ これらのコマンドは取り消しができないため、実行前に必ず確認してください。

---

## 📚 参考資料

- [Git公式ドキュメント](https://git-scm.com/doc)
- [Pro Git Book（日本語版）](https://git-scm.com/book/ja/v2)
- [GitHub Docs](https://docs.github.com/ja)

---

## 💡 ベストプラクティス

1. **こまめにコミット** - 小さな単位で頻繁にコミット
2. **分かりやすいコミットメッセージ** - 何をしたか明確に記述
3. **ブランチを活用** - 機能ごとにブランチを作成
4. **プッシュ前にプル** - リモートの最新状態を取得してから作業
5. **定期的にマージ** - 長期間ブランチを放置しない
6. **.gitignoreを活用** - 不要なファイルをコミットしない
7. **force pushは慎重に** - チーム開発では特に注意

---

**最終更新**: 2025年1月