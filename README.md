# devcontainer-template

devcontainerで開発を始めてみよう！

## Windowsの設定

https://code.visualstudio.com/docs/devcontainers/containers

vscodeとdockerが必要です。`Win+R`から`powershell`と入力し`Ctrl+Shift+Enter`を押します。powershellが管理者で開きます。

wslをインストールします。

```sh
wsl --install
```

端末を再起動します。またpowershellを開きます。

dockerとvscodeをインストールします。

```sh
winget install Docker.DockerDesktop
winget install Microsoft.VisualStudioCode
```

vscodeのdevcontainer拡張機能をインストールします。

```sh
code --install-extension ms-vscode-remote.remote-containers
```

sshの設定をします。秘密鍵を持っていない人は作ります。なんのことか分からない人も作ります。色々聞かれますがすべてEnterで問題ないです。

```sh
# もしかしたら鍵長とアルゴリズムの変更が必要かも
ssh-keygen
```

ssh-agentの設定をします。devcontainer上でsshを使用したgitの使用が可能になります。

https://code.visualstudio.com/docs/remote/troubleshooting#_setting-up-the-ssh-agent

```sh
Set-Service ssh-agent -StartupType Automatic
Start-Service ssh-agent
Get-Service ssh-agent
```

自分の作成した秘密鍵を登録します。登録終わったら秘密鍵を消した方がいいらしいです。私はなんかこわいので持ってます。

```sh
ssh-add
```

端末を再起動します。`Win+R`から`code`と入力し実行します。vscodeが開くのでここからvscodeで作業します。

ターミナルを起動します。``Ctrl+Shift+` ``でターミナルを開くことができます。powershellが開きます。

gitconfigの設定をします。

```sh
# gitコンテナの作成
docker run --rm 
```

コマンドパレットを開きます。`Ctrl+Shit+P`です。

`Dev Containers: Clone Repository in Container Volume...`を選びます。

このgithubのurlを入力して`Enter`。

https://github.com/s-uei/devcontainer-exercise.git

なんか立ち上がったら成功です。``Ctrl+Shift+` ``でコンテナのターミナルを開くことができます。zshが開きます。Debianのターミナルなのでaptとか使うことができます。

```sh
apt -h
```

この仮想コンテナ上でも同じ鍵でsshが可能なことを確認してください。

```sh
ssh-add -l
```

あとはgithubに公開鍵とか登録すると便利です。

## 注意

devcontainerのbaseイメージすべてでgitが使える訳ではないみたい。ssh-agentの連携に難がある。Debianイメージを使うと動作した。

mcr.microsoft.com/devcontainers/base:bullseye
