# LunAPI: Lunaのためのpythonインターフェース

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/remnrem/luna-api-notebooks/HEAD?urlpath=%2Fdoc%2Ftree%2F00_overview.ipynb)

このリポジトリには、LunAPI（_luna-py_と発音）のチュートリアルとリファレンスノートブックが含まれています。
LunAPIは、睡眠信号データの分析のための[Luna](http://zzz.bwh.harvard.edu/luna/) C/C++ツールセットのPythonベースのインターフェースです。

## はじめに

macOS（IntelとSiliconチップ）とLinux（Intel x86_64）向けのバイナリホイールが[PyPI](https://pypi.org/project/lunapi/)で利用可能ですが、`lunapi` Pythonパッケージの開発中は、主にDockerベースのインストールをサポートしています。
これにより、すべてのプラットフォーム（Windows、macOS、Linux）で同じ機能が利用可能になり、`lunapi`をJupyter Lab対話型ノートブック環境に組み込まれた関連モデルとリソース（チュートリアルデータ、ステージングモデルなど）とともにバンドルすることができます。

> [!NOTE]
> 経験豊富なユーザーは、ローカルでプロジェクトをコンパイルすることができます
>（つまり、[Luna](http://github.com/remnrem/luna-base)と[LunaAPI](http://github.com/remnrem/luna-api)を事前にインストールし、
> scikit-build-core/CMakeビルドシステムを呼び出す）。インストールに関する注意事項は、
> 時期を見て`luna-api`リポジトリに追加される予定です。

### pipによるインストール

`pip`を使用してインストールするには（macOS、Windows、またはLinuxディストリビューションで）、以下を試してください：

```
pip install lunapi
```

これが成功した場合、この現在のリポジトリの内容をダウンロードし、ダウンロードのルートディレクトリで`jupyter lab`を実行してノートブックを起動してください（もちろん、まだインストールしていない場合は[JupyterLab](https://jupyter.org/)をインストールする必要があります）。

これが現在のプラットフォーム/Pythonインストールをサポートしていない場合は、Dockerイメージ（以下）を使用する必要があります。現在、ソースホイールは配布されていません：今後、Linuxのためのソースホイールを追加することを検討します。

### Dockerによるインストール

簡単な4つのステップがあります：

 - [Docker Desktop](http://www.docker.com)をインストール

 - `lunapi` Dockerイメージをプル：
   ```
   docker pull remnrem/lunapi
   ```

 - このリポジトリのノートブックを取得：
   ```
   git clone https://github.com/remnrem/luna-api-notebooks.git
   ```

 - コンテナ内の`/lunapi/`フォルダに現在のフォルダをマッピングして、Lunaやその他のリソースがバンドルされたJupyter Labでコンテナを起動：

     - macOSまたはLinuxの場合：
     ```
     docker run --rm -p 8888:8888 -v ${PWD}:/lunapi/ remnrem/lunapi
     ```

     - Windowsの場合：
     ```
     docker run --rm -p 8888:8888 -v %cd%:/lunapi/ remnrem/lunapi
     ```

詳細については以下の注意事項を参照してください。

### 1) Docker Desktopのインストール

まず、お使いのマシン用の[Docker Desktop](http://www.docker.com)の無料コピーをダウンロードしてください。
Macを使用している場合は、正しいチップタイプ（AppleまたはIntel）を選択してください。

<p align="center" width="100%">
 <img src="img/docker1.png" width="70%" height="70%">
</p>

問題が発生した場合は、Dockerのページに多くのヘルプがあります。

### 2) 最新のLunAPIイメージをプル

Dockerをインストールした後、コマンドラインを使用して最新バージョンの`lunapi`を_プル_します：

```
docker pull remnrem/lunapi
```

<p align="center" width="100%">
 <img src="img/pull.png" width="100%" height="100%">
</p>

> [!TIP]
> このコマンドを後で使用して、使用しているバージョンが最新であることを確認することができます。

### 3) チュートリアルとリファレンスノートブックの取得

次に、このリポジトリからチュートリアルとリファレンスノートブックを取得します。これらは必須ではありませんが、
始めるのに役立ちます。例えば、コマンドラインから`git clone`を使用するか、
このページ上部のリンクからZipファイルを単にダウンロードすることができます：

<p align="center" width="100%">
 <img src="img/download.png" width="50%" height="50%" align="center">
</p>

### 4) LunAPIの起動

ノートブックをダウンロードしたフォルダ（`luna-api-notebooks/`）に移動し、
以下のDockerコマンドを実行して_LunAPI_を起動します（これは上記をすでにダウンロードした後、
つまり新しいセッションを開始する際の開始点です）：

```
docker run --rm -p 8888:8888 -v ${PWD}:/lunapi/ remnrem/lunapi
```

<p align="center" width="100%">
 <img src="img/run.png" width="100%" height="100%" align="center">
</p>

> [!NOTE]
> Dockerの使用に関する詳細については、Dockerのドキュメントを参照してください。
> 上記のコマンドは、イメージ`remnrem/lunapi`を`run`します
>（つまり、[DockerHub](http://hub.docker.com)リポジトリからダウンロードしたものを）。
> 追加オプションは、1）終了時にコンテナを停止し（`--rm`）、2）コンテナのポート8888を
> ローカルマシンのポート8888にマッピングして、ローカルウェブブラウザからJupyter Labに
> アクセスできるようにし、3）ローカルマシンの現在のフォルダ（`${PWD}`）をコンテナ内の
> `/lunapi/`フォルダにマッピングして、コンテナからマシンにファイルの読み書きができるように
> します。より多くの機能については、Dockerオプションを参照してください。例えば、複数の
> フォルダをマッピングしたり（または作業ディレクトリ以外のフォルダを指定したり、
> 例：`-v /home/john/data/:/lunapi/`を`local:container`の形式で使用）することは簡単です。
> 一つのヒントとして、パフォーマンスの理由からホームフォルダ全体をマッピングしない方が
> 良いでしょう。

上記を実行すると、ウィンドウにJupyter Labの起動ログからのテキストが表示されるはずです
（その大部分は安全に無視できます。これには、その後そのターミナルウィンドウにJupyterLabから
表示される可能性のある様々な警告も含まれます）。後でこれを合理化するように努めますが、
現時点では：Jupyter Labにアクセスするには、`http://127.0.0.1`で始まる行（2回表示される
かもしれません）を探してください（これはローカルマシンです）：

<p align="center" width="100%">
 <img src="img/start.png" width="100%" height="100%" align="center">
</p>

例えば、この特定の例では、コピーするリンクは以下のようになります：
```
http://127.0.0.1:8888/lab?token=df46b121be42d19f70d647af90b569b1240c668f41bf1b57
```
> [!TIP]
> トークンは毎回異なることに注意してください。上記の正確なリンクは使用しないでください。

行全体（トークンを含む）をコピーしてウェブブラウザに貼り付けると、Jupyter Labのインスタンスが
すでに実行されており、分析を開始する準備ができているはずです！例えば、ここでは最初に
`import lunapi as lp`を実行し、次にNSRRチュートリアルEDFでPOPS自動ステージャーを実行します：

<p align="center" width="100%">
 <img src="img/nb.png" width="100%" height="100%">
</p>

詳細については、ノートブック（`.ipynb`ファイル）を開いて、`lunapi`のチュートリアルと
リファレンス資料をご覧ください。

Jupyter Labインスタンスをローカルマシンで実行し続けるために、ターミナルウィンドウを開いたままに
してください（バックグラウンドにすることができます）。Jupyter Labインスタンスは、起動した
ターミナルでCtrl-Cを押すことで閉じることができるはずです。（Windowsでは、これが機能しない
かもしれません：その場合は、Docker Desktopを使用してコンテナを閉じることができます。）

> [!CAUTION]
> 設定ファイルを変更しない限り、一度に実行できるJupyter LabとLunAPIコンテナのインスタンスは
> 1つだけです。

## 詳細情報

メインのLunaドキュメントページは[http://zzz.bwh.harvard.edu/luna](http://zzz.bwh.harvard.edu/luna)
にあり、Lunaの使用方法、そのコマンドスクリプト言語、および利用可能な分析の範囲について説明しています。

現在、Pythonインターフェース（つまり_LunAPI_、同様にPythonパッケージ`lunapi`とも呼ばれる）に
関連するすべてのドキュメントは、このリポジトリのJupyterノートブックにあります。
