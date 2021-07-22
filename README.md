# LAMP

LAMP環境（Linux,Apache,MariaDB,PHP）を構築するためのDockerコンテナイメージを作成する。

## 必須環境
[Docker Desktop on Mac, Docker Desktop on Winows](https://docs.docker.com/compose/install/)などがインストールされ、`docker-compose`が使える状態であること。
## 作り方
1. 当プロジェクトをチェックアウトする。
1. `docker-compose.example.yml`を参考に、自身の環境にあった`docker-compose.yml`を作成する。
2. `env`を参考に、自身の環境にあった`.env`を作成する。
3. `docker compose build`を実行し、コンテナイメージを作成する。
    ```bash
    # 例）下記のような感じで作成されているはず。
    $ docker images
      :
    lamp_apache-php80    latest    a2bba121937f   47 minutes ago      754MB
    lamp_apache-php73    latest    9c5315f8ed1b   47 minutes ago      751MB
    lamp_apache-php74    latest    0967f6e67873   47 minutes ago      754MB
    lamp_phpmyadmin      latest    5e7fa3b7c9a4   About an hour ago   469MB
    lamp_mariadb55       latest    ff7046da5474   About an hour ago   352MB
    ```
## 使い方
該当プロジェクトの`docker-compose.yml`内の`image`に指定する。
（`example`フォルダを参照。）

## 各コンテナイメージに関して
### apache24-php73
PHP7.3を有効化した[Apache2.4](https://httpd.apache.org/docs/2.4/ja/)のウェブサーバー。
### apache24-php74
PHP7.4を有効化した[Apache2.4](https://httpd.apache.org/docs/2.4/ja/)のウェブサーバー。
### apache24-php80
PHP8.0を有効化した[Apache2.4](https://httpd.apache.org/docs/2.4/ja/)のウェブサーバー。<br>
`Imagick`は[不具合](https://github.com/Imagick/imagick/issues/358)のため有効化出来ていない。
→イレギュラーなやり方で対応した。
### mariadb55
[MariaDB](https://mariadb.org/)5.5。<br>
日本時間の設定や文字コードを`utf8mb4`に設定。
