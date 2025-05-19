# Gitの使い方

## 1. 初期設定（最初の1回のみ）

```sh
git config --global user.name "あなたの名前"
git config --global user.email "あなたのメールアドレス"
```

## 2. 変更内容の確認

```sh
git status
```

## 3. 変更をステージング（追加）

```sh
git add ファイル名
# 例:
git add index.html
```

## 4. コミット（変更履歴を記録）

```sh
git commit -m "変更内容の説明"
```

## 5. リモートリポジトリへプッシュ

```sh
git push origin ブランチ名
# 例:
git push origin main
```

## 6. VSCodeでの操作

- 左側の「ソース管理」メニューから変更内容を確認・コミットできます。
- コミットメッセージを入力し、「✔」ボタンでコミット。
- 「…」メニューや「プッシュ」ボタンでリモートに反映。

## 補足

- 「M」マークはファイルが変更（Modified）されたことを示します。
- コミットできない場合は、user.nameやuser.emailの設定を確認してください。
- コミット後は必ずプッシュしてリモートリポジトリに反映しましょう。
