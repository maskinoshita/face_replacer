# Serverless Frameworkによるハンズオン

このリポジトリは下記の2つのハンズオンのためのリポジトリです。

* Serverless FremeworkによるデモアプリのX-Ray設定
* Serverless FrameworkによるサーバーレスなE2Eテストの実行

ディレクトリ構成は下記のとおりです。子プロジェクトはGit Submoduleで導入されており、それぞれ別のリポジトリで管理されています。
```plain
/                           親プロジェクト
├── face_replacer_e2e           E2Eテストの子プロジェクト
├── face_replacer_example       デモアプリの子プロジェクト
└── serverless-compose.yml      各プロジェクトの設定
```

![#7構成図](docs/imgs/%237.drawio.png)

## ハンズオン1 (X-Ray)

### AWSのX-Rayの有効化まで (先週のp4まで)

1. このリポジトリをクローンする (--recursive)
   ```bash
   git clone https://github.com/maskinoshita/face_replacer.git --recursive

   # --recursive 忘れた場合
   git clone https://github.com/maskinoshita/face_replacer.git
   git submodule update --init --recursive
   ```
2. ライブラリをインストールする
    ```bash
    npm install                       # 親プロジェクト
    git submodule foreach npm install # 子プロジェクトすべて
    ```
3. `face_replacer_example/serverless.yml`の65行目の`suffix`を一意の値になるように編集
    https://github.com/maskinoshita/face_replacer_example/blob/59c7ea4c86aa257d107ca73490ff7be082b97b78/serverless.yml#L65
4. `face_replacer_example`をデプロイする
    ```bash
    # 親ディレクトリにいる場合 (face_replacer)
    # e2eのプロジェクトもデプロイするが、e2eは失敗する。あとで修正するのでそのままでOk.
    sls deploy

    # 子ディレクトリにいる場合 (face_replacer_example)
    sls deploy
    ```