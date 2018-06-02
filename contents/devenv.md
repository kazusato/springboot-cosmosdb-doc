# 開発環境構築

本章では、Windows 10（64bit）端末に、開発ツールを導入し、開発環境を構築します。
記載以外のツールでも同等の作業は実施可能かと思いますが、想定外の
問題発生を回避するため、一度は同じツールで試してみることをおすすめします。

# 7zip

OpenJDKはtar.gz形式で配布されているため、これを展開できるツールを導入します。
ここでは7zipを使用します。

Webブラウザーで[7zipのページ](https://www.7-zip.org/)を開き、64bit版の
インストーラーをダウンロードしてください。

インストーラーのexeファイルをダウロード後、実行してインストールします。
インストール時の設定はデフォルトのままで問題ありません。

# OpenJDK

[OpenJDK 10のダウンロードページ](http://jdk.java.net/10/)から、Windows
64bit向けのtar ballをダウンロードします。

ダウンロード後、Windowsのエクスプローラーで当該ファイルを開き、
「右クリック＞7-zip＞ここに展開」と操作して展開します。

展開されたファイル（拡張子.tar）を再度「右クリック＞7-zip＞ここに展開」と
操作して展開します。

## ツール配置用フォルダの作成

本書で使用するツールを配置するフォルダとしてCドライブ直下に「java」
フォルダを作成しておきます。

## OpenJDKの配置

展開されたフォルダ「jdk-10.0.1」（最新版ではバージョンは変わっている
可能性あり）を、上で作成したフォルダ（C:\java）に配置します。

## 環境変数の設定

環境変数JAVA_HOMEとPATHを設定します。

1. エクスプローラーの左ペインの「PC」を右クリックし、「プロパティ」を開く。
1. 上で開いた「システム」コントロールパネルの左ペインから、
「システムの詳細設定」を開く。
1. 上で開いた「システムのプロパティ」画面で、「環境変数」ボタンを押し、
「環境変数」設定画面を開く。
1. 以下の手順で「JAVA_HOME」環境変数を設定する。
   1. 「環境変数」設定画面の上段「xxxxxのユーザー環境変数」（xxxxxはユーザー名）で、
   「新規」ボタンを押し。
   1. 「新しいユーザー変数」画面で以下の通り設定する
   （変数値の値は実際のOpenJDKのフォルダ名に合わせること）。
      - 変数名: JAVA_HOME
      - 変数値: C:\java\jdk-10.0.1
   1. 「OK」ボタンを押す。
1. 次に、「Path」環境変数にOpenJDKのパスを追加する。
   1. 「xxxxxのユーザー環境変数」の「Path」を選択して「変数」ボタンを押す。
   1. 「環境変数名の編集」画面で「新規」ボタンを押す。
   1. 追加された入力フィールドに「%JAVA_HOME%\bin」と入力する。
   1. 「OK」ボタンを押す。

### OpenJDKの導入・設定が完了していることの確認

コマンドプロンプトからjavaコマンド、javacコマンドを実行し、導入・設定が
正しく完了していることを確認します。

上の操作（環境変数の設定）を行う前に開いていたコマンドプロンプトでは、
設定した環境変数が反映されていないため、別のコマンドプロンプトを
新たに開いて実施してください。

1. 「スタート＞Windows システム ツール＞コマンドプロンプト」を開く。

    ※今後も使用するので、コマンドプロンプトのアイコンを右クリックし、
    「スタートにピン留めする」を選んでピン留めしておくと便利です。

1. 「java -version」と入力し、以下の通り出力されることを確認する。

    ```
    C:\Users\xxxxx>java -version
    openjdk version "10.0.1" 2018-04-17
    OpenJDK Runtime Environment (build 10.0.1+10)
    OpenJDK 64-Bit Server VM (build 10.0.1+10, mixed mode)
    ```

1. 続いて、「javac -version」と入力し、以下の通り出力されることを確認する。

    ```
    C:\Users\xxxxx>javac -version
    javac 10.0.1
    ```

### 正しく導入・設定が完了していない場合
正しく導入・設定が完了していないと、以下のように表示されます。
手順を再確認してください。

    ```
    C:\Users\xxxxx>java -version
    'java' は、内部コマンドまたは外部コマンド、
    操作可能なプログラムまたはバッチ ファイルとして認識されていません。
    ```

# Azure CLI

本チューリアルでは、Azureを使用するため、Azure CLI（コマンドライン
インターフェース）を導入しておきます。

導入手順は、[WindowsでのAzure CLI 2.0のインストール](https://docs.microsoft.com/ja-jp/cli/azure/install-azure-cli-windows?view=azure-cli-latest)に
記載されている通りです。MSIインストーラーをダウンロードしてインストールします。

導入後、正しく導入されているか、以下の通り確認します。

1. 新たにコマンドプロンプトを開く。
1. 「az --version」コマンドを実行する。正しく導入が完了していると、以下のように表示される。

    ```
    C:\Users\xxxxx>az --version
    azure-cli (2.0.33)
    
    acr (2.0.25)
    acs (2.0.33)
    （中略）
    storage (2.0.33)
    vm (2.0.32)
    
    Python location 'C:\Program Files (x86)\Microsoft SDKs\Azure\CLI2\python.exe'
    Extensions directory 'C:\Users\xxxxx\.azure\cliextensions'
    
    Python (Windows) 3.6.5 (v3.6.5:f59c0932b4, Mar 28 2018, 16:07:46) [MSC v.1900 32 bit (Intel)]
    
    Legal docs and information: aka.ms/AzureCliLegal
    ```

    ※表示されるバージョンは、導入タイミングにより変わります。

# Git for Windows

1. [Git forWindows](https://gitforwindows.org/)からインストーラーをダウンロードする。
1. ダウンロードしたインストーラーを起動する。
1. 「Configuring the ending conversions」画面（8画面目）まで、デフォルト設定のまま「Next」ボタンを押して進む。
1. 「Configuring the ending conversions」画面で、「checkout as-is, commit as-is」（一番下の選択肢）を選び、「Next」ボタンを押す。
1. 引き続き、デフォルト設定のまま「Next」ボタンを押してインストールを完了させる。
1. 「Completing the Git Setup Wizard」画面（最後の画面）で、「View Release Notes」のチェックを外し、「Finish」ボタンを押す。

※リリースノートを読みたければ、チェックを外さなくてもよい。

# IntelliJ IDEA Community Edition

Java IDEとして「IntelliJ IDE Community Edition」を導入します。

1. ブラウザーで[JetBrains](https://www.jetbrains.com/)を開く。
1. 画面上部のナビゲーションバーから「Tools＞IntelliJ IDEA」を選ぶ。
1. 「Download」ボタンを押す。
1. Communityの「Download」ボタンを押す。
1. ダウンロードしたインストーラーを実行してインストールする。設定はデフォルト値のままでよい。

## 日本語化

PleiadesによるIntelliJ IDEAの日本語化を行います。

1. ブラウザーで[日本語化マニュアル](https://www.willbrains.jp/page/4)を開く。
1. 「方法1：Pleiades インストーラーで簡単日本語化 (おすすめ)」の
「Pleiadesプラグイン・ダウンロード」から、「Windows」をクリックする。
1. 新たに開いた「MergeDoc Project」画面の「Pleiades プラグイン・ダウンロード」で、
「Windows」をクリックして「pleiades-win.zip」をダウンロードする。
1. ダウンロードしたZIPファイルを展開する。
1. 展開したフォルダ内の「setup.exe」を実行する。「Pleiades日本語化プラグインのセットアップ」画面が表示される。
1. 表示された画面の「日本語化するアプリケーション」で「選択」ボタンを押す。
1. 「日本語化するアプリケーションの選択(exe)」ダイアログボックスで、
「"C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2018.1.4\bin\idea64.exe"」
を選択する。
これにより、「Pleiadesが配置されるディレクトリ」「Pleiadesの設定が追加されるファイル」欄は
自動的に設定される。
1. 「日本語化する」ボタンを押す。
1. 「日本語化が完了しました。」から始まるメッセージが表示されたら、「OK＞終了」と押して終了する。

## 動作確認と初期設定

1. スタートメニューから「JetBrains＞IntelliJ IDEA Community Edition 2018.1.4」を開く。
1. 「IntelliJ IDEAユーザー使用許諾契約」画面が開くので、利用規約を読み、問題なければ「受諾」ボタンを押す。
1. 「データ共用」画面が表示されるので、「使用統計情報を送信する」か「Don't send」のいずれかを押す。
1. 「IntelliJ IDEAへようこそ」画面が表示される。この後の設定は別途行うので、こおｋでは右上の「×」ボタンを押して終了する。




