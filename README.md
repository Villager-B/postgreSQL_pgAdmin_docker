# PostgreSQL+pgAdmin4 on Docker

Docker上でPostgreSQL14 + pgAdmin4の環境を構築する

## 主な特徴
- PostgreSQL v14
- pgAdmin4 v6
- [10年戦えるデータ分析入門 SQLを武器にデータ活用時代を生き抜く](https://amzn.to/3Pa95U3)のデータのInsertまで説明

## 環境を構築手順
1. `git clone https://github.com/Villager-B/postgreSQL_pgAdmin_docker.git`
2. cloneしたリポジトリに移動する
3. docker volumeの作成
    1. `docker volume create postgres_volume`
    2. `docker volume create pgadmin4_volume`
3. `docker-compose up -d`でコンテナを立ち上げる
4. http://localhost:9999 にアクセス

### Postgres情報
```
Username: shimasan
Password: postgres1234
Port: 15432 -> 5432
```

### pgAdmin4情報
```
Access URL: localhost:9999
UserEmail: sample@sample.com
Password: sample1234
```

## Option
### 10年戦えるデータ分析入門 SQLを武器にデータ活用時代を生き抜く
- 商品ページ
    - [10年戦えるデータ分析入門 SQLを武器にデータ活用時代を生き抜く](https://amzn.to/3Pa95U3)
- データ
    - [『10年戦えるデータ分析入門』サポートページ](https://i.loveruby.net/stdsql/)

### データの挿入

1. 上記サポートページからサンプルデータをダウンロード
    1. 無記名・サイズ大の両方
2. cloneしたリポジトリに移動する
3. `mkdir resource`でディレクトリ作成
4. ダウンロードしたサンプルデータを解凍し，resourceに2つのフォルダを移動
5. 以下のコマンドを実施し，データを挿入する

```bash
docker exec -it postgres bash
```

```bash
cd stdsql-large-20201213
psql -h localhost -p 5432 -U shimasan < load.sql
cd ..
cd stdsql-20201213
psql -h localhost -p 5432 -U shimasan < load.sql
```

6. http://localhost:9999 にアクセスし，ログイン
7. クイックリンクにある「新しいサーバーを追加」を選択
    1. Generalで名前を適当に入力
    2. 接続でホスト名`postgres`，ユーザ名`shimasan`，Passwprdはpostgresのパスワードを入力
8. 自分でつけた名前/データベース/shimasan/スキーマ に挿入したテーブルが確認できる
9. 画面にあるツールオプションからクエリツールを選択すれば完了

## 参考文献
- [Docker for WindowsでPostgres+pgAdminのコンテナをたてる](https://qiita.com/Yukimura127/items/c798cf9c3b19498ab8bf)