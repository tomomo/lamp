# LAMP

LAMP環境（Linux,Apache,MariaDB,PHP with NodeJS）を構築するためのDockerコンテナイメージを作成する。

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
    lamp-mariadb    10.7                af0ab28b16dc   5 minutes ago       482MB
    lamp-mysql      5.5                 e0a1b648aa56   17 minutes ago      250MB
    lamp-php        7.3-nodejs-apache   fcca4ece37c0   40 minutes ago      907MB
    lamp-php        7.4-nodejs-apache   bf8954307e05   58 minutes ago      954MB
    lamp-php        8.0-nodejs-apache   1f1cdfd37a39   About an hour ago   956MB
    lamp-php        8.1-nodejs-apache   7e116ca4bd25   2 hours ago         960MB
    ```
## 使い方
該当プロジェクトの`docker-compose.yml`内の`image`に指定する。
（`example`フォルダを参照。）
