# LAMP

LAMP環境（Linux,Apache,MariaDB,PHP with NodeJS）を構築するためのDockerコンテナイメージを作成する。

## 必須環境
[Docker Desktop on Mac, Docker Desktop on Winows](https://docs.docker.com/compose/install/)などがインストールされ **docker-compose** が使える状態であること。
## 作り方
1. 当プロジェクトをチェックアウトする。
1. **docker-compose.example.yml**を参考に、自身の環境にあった**docker-compose.yml**を作成する。
1. **env**を参考に、自身の環境にあった**.env**を作成する。
1. "**docker compose build**"を実行し、コンテナイメージを作成する。
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
該当プロジェクトの**docker-compose.yml**内の**image**に指定する。
（exampleフォルダを参照。）

## VSCodeによるリモート開発設定例
設定はexampleフォルダの**docker-compose.yml**や **.devcontainer.json**を参照。
+ VSCodeに**extensition**を導入する。
    ```bash
    # VSCode
    code --install-extension mrmlnc.vscode-apache
    code --install-extension formulahendry.auto-close-tag
    code --install-extension streetsidesoftware.code-spell-checker
    code --install-extension ms-azuretools.vscode-docker
    code --install-extension EditorConfig.EditorConfig
    code --install-extension dbaeumer.vscode-eslint
    code --install-extension mhutchie.git-graph
    code --install-extension donjayamanne.githistory
    code --install-extension codezombiech.gitignore
    code --install-extension eamodio.gitlens
    code --install-extension oderwat.indent-rainbow
    code --install-extension MS-CEINTL.vscode-language-pack-ja
    code --install-extension yzhang.markdown-all-in-one
    code --install-extension bierner.markdown-preview-github-styles
    code --install-extension bierner.markdown-mermaid
    code --install-extension junstyle.php-cs-fixer
    code --install-extension neilbrayfield.php-docblocker
    code --install-extension bmewburn.vscode-intelephense-client
    code --install-extension esbenp.prettier-vscode
    code --install-extension alexcvzz.vscode-sqlite
    code --install-extension stylelint.vscode-stylelint
    code --install-extension bradlc.vscode-tailwindcss
    code --install-extension VisualStudioExptTeam.vscodeintellicode
    code --install-extension johnsoncodehk.volar
    code --install-extension redhat.vscode-yaml
    ```
+ Win10の時は、**devcontainer.json**の"**remoteUser**"を有効にする。
