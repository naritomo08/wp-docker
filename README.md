# wp-docker

wordpress実行コンテナになります。

## 参考URL

[Docker ComposeでWordPress開発環境を構築する方法](https://weblabo.oscasierra.net/wordpress-docker-compose/)

## なぜ、あえてDockerなのか？

インフラエンジニアとしてDockerから触れたほうが扱いやすく、
以下の利点を感じられたため、開発環境構築ではDockerを使用することを
推しています。

* OS問わず同じ開発環境での開発が可能
* インフラ/アプリエンジニアでのコラボがしやすい。
　 (具体的にはインフラ屋でOS/開発環境のベース環境を構築し、
　　アプリエンジニアで本来行うべき開発業務に集中できる。)
* 本番Web環境で多く使用されているAWS/AzureなどのIaaSサービス
　に対し、Docker資産を使用できる。

一応、本番環境展開にPaaSを使用する手はありますが、
AWS/Azureを絡めたほうが業務につながるとみています。

## 事前準備

windows11+wsl2+Ubuntu22+DockerCompose+vscode+gitでの環境を構築してること。

## 環境構築手順

### ベースリポジトリをクローンする。

```bash
$ git clone https://github.com/naritomo08/wp-docker.git
$ cd wp-docker
*フォルダ名は任意のものに変更できる。
```

後にファイル編集などをして、git通知が煩わしいときは
作成したフォルダで以下のコマンドを入れる。

```bash
 rm -rf .git
```

### dockerコンテナを立ち上げる。

```bash
$ docker-compose up -d
```

### 各種サイト確認する。

## サイトURL

### laravel

http://127.0.0.1:8080

### adminer(DB管理ツール)

http://127.0.0.1:8081

* ログイン情報
  - サーバ: mysql
  - ユーザ名: wordpress
  - パスワード: wordpress
  - データベース: wordpress

### mailhog(メールサーバ)

http://127.0.0.1:8025

本メールサーバを使用するときは以下の設定を行うこと。
メールサーバ:mailhog
ポート:1025
送信元アドレス:info@example.com

## コンテナ起動する方法

`docker-compose.yml`が存在するフォルダーで以下のコマンドを実行する。

```bash
$ docker-compose up -d
```

## コンテナ停止する方法

`docker-compose.yml`が存在するフォルダーで以下のコマンドを実行する。

```bash
$ docker-compose stop
```

## コンテナ削除する方法

`docker-compose.yml`が存在するフォルダーで以下のコマンドを実行する。

```bash
$ docker-compose down
```

## 起動中のコンテナに入る

### wordpressコンテナ

```bash
$ docker-compose exec wordpress /bin/bash
```

### DBコンテナ

```bash
$ docker-compose exec mysql /bin/bash
```

## その他

## 本作成したソースを流用したい場合

今回のソースについて、コンテナ作成時に以下の
wordpressソースをローカルに保管するようにしています。

以下のローカルフォルダをコンテナ停止状態でgitに保管して
他の開発環境に持っていくことで流用することが出来ます。

本Dockerに再度展開するときはコンテナファイル展開先のローカルにして、
他のすでに立ち上げている環境ではコンテナ内のフォルダへオフライン
状態で展開してください。

| ローカル | コンテナ内のフォルダ | 概要 |
| ---- | ---- | ---- |
| ./docker-data/mysql/ | /var/lib/mysql	| MySQLのデータベース |
| ./docker-data/wordpress/themes | /var/www/html/wp-content/themes | WordPressのテーマが保存されるフォルダ |
| ./docker-data/wordpress/plugins | /var/www/html/wp-content/plugins	| WordPressのプラグインが保存されるフォルダ |
| ./docker-data/wordpress/uploads | /var/www/html/wp-content/uploads	| WordPressにアップロードしたメディアが保存されるフォルダ |

# おわりに

本記事以外にもElixir/rubyについても同様のものを上げていますので、
参照していただいてこちらにも挑戦していただければと思います。

https://qiita.com/naritomo08/items/fecf4ace7b9ca9078102

https://qiita.com/naritomo08/items/b39d4ee6987fb052ca79