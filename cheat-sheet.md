# ブランチ作成と切り替えを同時に行う
git checkout -b ブランチ名

# ブランチ確認
git branch

# ブランチ切り替え
git checkout ブランチ名

# マージ（mainに戻ってから）＊コマンドで行う場合、TOMAPでは通常merge作業はgit Hubで行います。
git checkout main
git merge ブランチ名

# コンフリクト解決後
git add .
git commit -m "コンフリクトを解決"

# 困ったときの状況確認
git status
git log --oneline --graph --all