---

theme: "black"
transition: "default"

---

# Django 環境の構築と開発

---

## Anacondaを利用した開発環境の構築

---

### WindowsにAnacondaを導入する

--

#### Ancondaのインストール

[Anaconda](http://www.anaconda.com/) から最新のanacondaをインストールする。

---

### Windowsにgitを導入する

--

#### Scoopのインストール

##### PowerShellの起動

スタートからWindows PowerShellを起動する

##### PowerShellの設定変更

```powershell
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
```

##### PowerShellからのScoopのインストール

```powershell
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
```

--

#### Scoopによるgitのインストール

##### gitのインストール

```cmd
scoop install git
```

##### gitの更新

```cmd
scoop update git
```

---

### 仮想環境の構築

--

#### 開発用仮想環境の作成

スタートからAnaconda Promptを起動する

```cmd
conda create -n django2_env python=3.*
```

--

#### 必要なパッケージのインストール

```cmd
conda activate django2_env
conda install -y django==2.*
conda install -y -c conda-forge cookiecutter
```

---

### condaコマンドの使い方

--

#### condaによるパッケージの管理

##### パッケージのインストール

```cmd
conda install <パッケージ名>
```

##### パッケージの削除

```cmd
conda remove <パッケージ名>
```

--

#### condaによる仮想環境の管理

##### 仮想環境の作成

```cmd
conda create -n <仮想環境名>
```

##### 仮想環境の削除

```cmd
conda env remove -n <仮想環境名>
```

##### 仮想環境のリスト

```cmd
conda env list
```

--

#### 仮想環境の利用と終了

##### 仮想環境の利用

```cmd
conda activate <仮想環境名>
```

##### 仮想環境の終了

```cmd
conda deactivate
```

--

#### condaとpip

Anacondaでパッケージを管理するにはAnacondaのcondaコマンドとPythonのpipコマンドがある。ただし、お互いに独立しているため併用には注意する必要がある。condaもpipもお互いの存在を意識しないためバージョンが競合した場合には問答無用の上書きが発生しパッケージの動作に不具合が生じる可能性がある。最悪、Anacondaの環境全体が破壊されるリスクもある。

--

#### condaでパッケージが見つからないときの推奨手順

1. condaパッケージの検索
    condaパッケージを配布しているチャンネルを検索する。

    ```bash
    anaconda search <package>
    ```

2. pipから入れる、手順は後述

--

#### Anaconda環境下でのpipパッケージの利用

1. pipから入れたい場合、まずPyPIのサイトから該当するパッケージを探し、依存関係を調べておく。依存するパッケージのうち、condaからインストール可能なものは予めインストールしておく。

2. 依存関係を満たしたらインストールし、動作確認する。

```bash
pip install --no-deps <package>
```

--

#### condaでパッケージが見つからないときの別法

* pipからしか入れられないパッケージを入れたい場合、新しいcondaの環境を作る(conda create -n env python)。その環境内ではconda installは一切用いない。

---

## djangoでの最初のプロジェクトのスタート

--

### djangoでの最初のプロジェクトの作成

```cmd
django-admin startproject djexample
```

この操作でカレントディレクトリの下にdjexampleというプロジェクトフォルダが作られ、その中にdjexampleというフォルダが作成される。

--

### 作成したdjangoのプロジェクトのフォルダの構成

djexample (プロジェクトのベース)  
|-djexample (プロジェクトの設定)  
|-manage.py

--

### 最初のWebアプリケーションの作成

```cmd
manage.py startapp app
```

プロジェクトフォルダの中でこの操作を実行すると、appというフォルダが作られその中にアプリケーションの数個のファイルが作成される。

--

### 最初のプロジェクトの起動

```cmd
manage.py runserver
```

プロジェクトフォルダの中でこの操作を実行すると、開発用のサーバが起動する。
