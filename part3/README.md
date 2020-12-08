# Part 3： PHPとオブジェクト指向

## 目的

* 開発現場で必要とされるPHPの知識を習得する
* オブジェクト指向を理解しプログラムを書ける
* 自信を持ってコードを読み書きできる

## 環境構築

```bash
# Docker イメージのビルド
docker-compose build

# Docker コンテナの起動
docker-compose up -d

# Docker コンテナ内でコマンドを実行する
docker-compose exec app php -v

# Docker コンテナの停止・削除
docker-compose down
```

## 環境構築 (Remote Development編)

Docker イメージをビルドする。

```bash
docker-compose build
```

VSCode の Remote-Containers: Open Folder in Container からコンテナを開く。

コマンドは VSCode のターミナルから実行する。

終了するときはコンテナを停止・削除する。

```bash
docker-compose down
```

### デバッグ (Xdebug)

デバッグしたい時は下記の順に実施する。

1. コードにブレークポイントを設定する
2. デバッグビューを開く
3. 「Listen for Xdebug」を選択してデバッグを開始する
4. コードを実行する

ブレークポイントで止まらない場合、 `.vscode/launch.json` の port が 9003 であることを確認する。
