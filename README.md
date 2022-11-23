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

### [VisualStudioCode](https://code.visualstudio.com/)
> 最新のWebおよびクラウドアプリケーションの構築とデバッグのために再定義され最適化されたコードエディタです。

setting.json
