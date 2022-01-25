# Part 7： データベースとSQL

## 目的

* データベースの基本概念を学ぶ
* データベースの設計ができるようになる
* SQLを使いこなせるようになる

## 環境構築

```bash
# Docker イメージのビルド
docker-compose build

# Docker コンテナの起動
docker-compose up -d

# データベースに接続する（パスワードは pass を入力）
docker-compose exec db mysql -u test_user -D test_database -p
docker-compose exec db bash -c 'mysql -u${MYSQL_USER} -p${MYSQL_PASSWORD} ${MYSQL_DATABASE}'

# Docker コンテナの停止・削除
docker-compose down
```

## Docker で困ったら

### dbコンテナが起動しない場合

下記のエラーでdbコンテナが起動しない場合

```bash
2017-11-20 02:56:52 1 [ERROR] InnoDB: auto-extending data file ./ibdata1 is of a different size 0 pages
 MB) than specified in the .cnf file: initial 768 pages, max 0 (relevant if non-zero) pages!
2017-11-20 02:56:52 1 [ERROR] InnoDB: Could not open or create the system tablespace. If you tried to a
 to the system tablespace, and it failed here, you should now edit innodb_data_file_path in my.cnf back
and remove the new ibdata files InnoDB created in this failed attempt. InnoDB only wrote those files fu
did not yet use them in any way. But be careful: do not remove old data files which contain your precio
2017-11-20 02:56:52 1 [ERROR] Plugin 'InnoDB' init function returned error.
2017-11-20 02:56:52 1 [ERROR] Plugin 'InnoDB' registration as a STORAGE ENGINE failed.
2017-11-20 02:56:52 1 [ERROR] Unknown/unsupported storage engine: InnoDB
2017-11-20 02:56:52 1 [ERROR] Aborting
```

MySQLの古いデータを削除します。

```bash
# MySQLの以前のデータを削除する
rm -rf docker/db/mysql_data
```

Dockerの不要なイメージ、コンテナ、ネットワーク、ボリュームを削除します。

```bash
# Docker コンテナの停止・削除
docker-compose down

# Docker の不要なイメージ、コンテナ、ネットワーク、ボリュームを削除する
docker system prune --volumes
```

MySQLのデータの同期をやめるために、 `docker-compose.yml` の下記3行目を削除します

```bash
db:
  volumes:
    - ./docker/db/mysql_data:/var/lib/mysql # ← この行を削除します
```

イメージから作成し直します。

```bash
# Docker イメージのビルド
docker-compose build

# Docker コンテナの起動
docker-compose up -d

# コンテナの起動状態を確認する
docker-compose ps
```
