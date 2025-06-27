---
html:
  toc: true
---
# 勉強会　事前準備

Svelte + GitHub Copilot Hands-on 勉強会では、以下のソフトウェアを使用します。

- Git
- VSCode
  - Extensions
    - dbaeumer.vscode-eslint
    - esbenp.prettier-vscode
    - github.copilot
    - github.copilot-chat
    - svelte.svelte-vscode
- Node.js v22 (LTS)
- pnpm

勉強会の前までに、後述の手順に従いインストール・設定を行ってください。

## Windows PCを使用される方

WindowsではChocolateyを使用してソフトウェアをインストールします。

管理者権限でPowershellを起動します。(起動操作は下記参照)

1. ショートカットキー `Windows` + `R` を実行します。
2. 表示されたダイアログで `powershell` と入力します。
3. ショートカットキー `Ctrl` + `Shift` + `Enter` を実行します。

表示されたPowershellウィンドウで以下のコマンドを実行します。

```ps1
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

続けて以下のコマンドを実行し、必要なソフトウェアをインストールします。

```ps1
choco install -y nodejs-lts
choco install -y pnpm
choco install -y git
choco install -y vscode
```

## Macを使用される方

MacではHomebrewを使用してソフトウェアをインストールします。

ターミナルで以下のコマンドを実行し、Homebrewをインストールします。

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

続けて以下のコマンドを実行し、必要なソフトウェアをインストールします。

```sh
brew install node@22
brew install pnpm
brew install git
brew install --cask visual-studio-code
```


## Widnows / Mac 共通

1. 以下のコマンドを実行し、必要なVSCode Extensionsをインストールします。

```sh
code --install-extension dbaeumer.vscode-eslint
code --install-extension github.copilot
code --install-extension github.copilot-chat
code --install-extension svelte.svelte-vscode
code --install-extension esbenp.prettier-vscode
```

2. 以下の手順に従いVSCodeからGitHub Copilotが使用できるように設定します。
  https://code.visualstudio.com/docs/copilot/setup

3. VSCodeでウィンドウ上部のCopilotのアイコンから`Open Chat`を選択し、GitHub CopilotのChat Viewが表示できることを確認します。
  ![](https://code.visualstudio.com/assets/docs/copilot/chat/copilot-chat/copilot-chat-menu-command-center.png)
4. Chat View下部で、Chatのモード(Ask、Edit、Agent)が選択できることを確認します。  
  ![](https://code.visualstudio.com/assets/docs/copilot/chat/chat-modes/chat-mode-dropdown.png)

