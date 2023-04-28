# dev-setup
開発機セットアップガイド

- SSH鍵作成
- Gitの設定
- Homebrewパッケージインストール
- nvm設定
- VisualStudioCodeの設定

## すぐに始める
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install git

git config --global user.name <name>
git config --global user.email <email>

ssh-keygen -C ""
cat ~/.ssh/id_rsa.pub | pbcopy 
#GitHubのSSHkeysに登録

git clone git@github.com:kmzkr/dev-setup.git
cd dev-setup
cp Brewfile ~/.Brewfile
brew bundle --global
```

## 詳細
### [ssh-keygen]()
> SSH（Secure SHell）の公開鍵と秘密鍵を作成するコマンドです

```sh
#コメントなしで鍵を作成
ssh-keygen -C ""

#公開鍵をGithubなどサービスのSSHkeysに登録する
cat ~/.ssh/id_rsa.pub | pbcopy

#例：クローン
git clone git@github.com:kmzkr/dev-setup.git
```

### [Git](https://git-scm.com/)
> バージョン管理システム

```sh
#Git設定ファイル
git config --global user.name <name>
git config --global user.email <email>
cat ~/.gitconfig
```

### [Homebrew](https://brew.sh/index_ja)
> macOS（またはLinux）用パッケージマネージャー

```sh
#xcodeをインストール(省略可：homebrewインストールの中でもやってくれる)
xcode-select --install

#Homebrewインストール(公式ページから確認推奨)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

#Homebrewインストール確認
brew help 

#パッケージリストをコピーする
cp Brewfile ~/.Brewfile

#パッケージをインストール
brew bundle　--global

#パッケージのインストール確認
brew list

#パッケージ情報を表示
brew info

#Homebrewの更新 インストールしたパッケージは更新されない
brew update

#更新可能なパッケージ一覧を表示
brew outdated

#インストールしたパッケージを更新
brew upgrade
brew upgrade git #パッケージ指定する場合
```

補足
```sh
#リストの更新
brew bundle dump --global --force

#手動インストール CUIアプリ
brew install git

#手動インストール GUIアプリ
brew install --cask visual-studio-code

#手動インストール AppStoreアプリ
#AppStoreへ事前ログインが必要
brew install mas #mas-cli必須
mas install 539883307 #LINE
```

## [nvm](https://github.com/nvm-sh/nvm)
> node.jsのバージョン マネージャー

[nvm - Homebrew Formulae](https://formulae.brew.sh/formula/nvm)を参照

初期設定
```sh
mkdir ~/.nvm

vi ~/.zshrc
#以下を入力-----
#nvm
export NVM_DIR="$HOME/.nvm"
  [ -s "$(brew --prefix)/opt/nvm/nvm.sh" ] && \. "$(brew --prefix)/opt/nvm/nvm.sh" # This loads nvm
  [ -s "$(brew --prefix)/opt/nvm/etc/bash_completion.d/nvm" ] && \. "$(brew --prefix)/opt/nvm/etc/bash_completion.d/nvm" # This loads nvm bash_completion
#-------------

#適用
source ~/.zshrc
```

使い方
```sh
#インストール済み一覧
nvm ls

#インストール
nvm install v18.12.1

#インストール .nvmrc
nvm install

#バージョン切り替え
nvm use v18.12.1

#バージョン切り替え .nvmrc
nvm use
```

参考
- [NPMとpackage.jsonを概念的に理解する](https://qiita.com/righteous/items/e5448cb2e7e11ab7d477)

### Python
以下のパッケージ
- [pyenv](https://github.com/pyenv/pyenv): Pythonバージョン管理ツール
- [pipenv](https://pipenv-ja.readthedocs.io/ja/translate-ja/): Pythonのパッケージマネジャー

#### pyenv
初期設定
```
vi ~/.zshrc
#以下を入力-----
#pyenv
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
#-------------

#適用
source ~/.zshrc
```

使い方
```
#利用可能なすべてのバージョンのリストが表示
pyenv install -l

#Pythonインストール
pyenv install 3.10.4

#Pythonアンインストール
pyenv uninstall 3.10.4

#インストール済みのバージョン一覧
pyenv versions

#バージョン切り替え
pyenv shell 3.10.4 #現在のシェル セッションのみを選択します
pyenv local 3.10.4 #現在のディレクトリ (またはそのサブディレクトリ) にいるときはいつでも自動的に選択します
pyenv global 3.10.4 #ユーザー アカウントに対してグローバルに選択します
```

#### pipenv
使い方
```
#仮想環境の作成
pipenv --python 3.6
# pyenvを使用している場合は，環境に入っていないバージョンを指定したときにはpyenvと連動してPythonのインストールが自動的に行われる

#パッケージインストール
pipenv install numpy

#開発パッケージインストール
pipenv install --dev autopep8 flake8

#pipfileからの環境再現
pipenv install

#pipfile.lockからの環境再現
pipenv sync

#requirements.txtからのインストール
pipenv install -r ./requirements.txt

#仮想環境へログイン
pipenv shell

#仮想環境の場所
pipenv --venv

#仮想環境の削除
pipenv --rm
```

### [VisualStudioCode](https://code.visualstudio.com/)
> 最新のWebおよびクラウドアプリケーションの構築とデバッグのために再定義され最適化されたコードエディタです。

```sh
#設定ファイル
cp vscode/settings.json $HOME/Library/Application\ Support/Code/User/settings.json 

#拡張機能をインストール
sh vscode/extentions.sh
```


補足：設定ファイル

```sh
#ユーザ設定
cat $HOME/Library/Application\ Support/Code/User/settings.json 

#ワークスペース設定
cat <プロジェクトルート>/.vscode/settings.json

#ユーザ設定をエクスポート
cat $HOME/Library/Application\ Support/Code/User/settings.json > vscode/settings.json
```

補足：拡張機能設定ファイル

```sh
#ユーザ設定
ls -al ~/.vscode/extensions

#ワークスペース設定 recommendations
cat <プロジェクトルート>/.vscode/extensions.json

#インストール済みの拡張機能一覧
code --list-extensions

#インストール済みの拡張機能一覧をインストール用ファイルとしてエクスポート
code --list-extensions | xargs -L 1 echo code --install-extension > vscode/extensions.sh
```

### [Docker](https://docs.docker.com/)
Docker Desktopとしてインストールする。

```sh
#インストール
brew install --cask docker

#インストール確認
docker -v

#DockerDesktopを起動させないとdockerコマンドが通らないので注意
open /Applications/Docker.app
```