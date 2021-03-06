# Spring BootとCosmos DBで簡単なアプリケーションを作ろう

Spring BootとAzure Cosmos DBを使って、簡単なアプリケーションを作成するチュートリアルです。
Windows 10環境に開発ツールをセットアップするところから始めます。

# 前提環境・条件

- Windows 10 Pro 64bit/April 2018 Update (1803)
   - エクスプローラーは「表示」タブの「表示/非表示」で
   「ファイル名拡張子」「隠しファイル」にチェックを入れておく
   （表示設定にしておく）ことをお勧めします。
   - これ以前のバージョン（アップデート）でも、おおむね同様に動作すると
   思いますが、一部画面表示等が異なる可能性があります。
- Azureサブスクリプションを保有し、Azureポータルにログインできること。

# 対象バージョン

- OpenJDK 10
- Spring Boot 2.x
- Spring Data 2.x
- Spring Data Cosmos DB 2.x

# 目次
1. [開発環境構築](contents/devenv.md)
1. [Spring Bootプロジェクトの作成](contents/spring_boot_prj.md)
1. [IntelliJ IDEAへの取り込み](contents/intellij_idea.md)
1. [簡単なWebページを作る](contents/simple_web_page.md)
1. [Azure Cosmos DBの準備](contents/prepare_cosmosdb.md)
1. [JavaプログラムからCosmos DBにアクセスする](contents/java_to_cosmosdb.md)
1. [REST APIを作成する](contents/rest_api.md)
1. [Cosmos DBリソースを削除する](contents/delete_rg.md)
