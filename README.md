
# Klubi
## _Tech setup_


Apps para baixar.

- [MySQLWorkbench]() ou [Beekeeper]()
- [Notion]()
- [Slack]()

## Terminal
Execute o seguinte comando no terminal:
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/lewagon/setup/master/utils/macos_list_processor_type.sh)"
```

☝️ O resultado do comando deve indicar se o seu computador usa Apple Silicon.

If your computer uses Apple Silicon, expand the paragraph below and go through it. Otherwise ignore it.

<details>
  <summary>👉&nbsp;&nbsp;Setup for Apple Silicon 👈</summary>

### Desinstalar Homebrew

Precisamos desinstalar o Homebrew  caso uma versão nativa esteja instalada.

Execute o seguinte comando no terminal:

``` bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"
```

Se o brew não foi instalado, você receberá a mensagem `brew: command not found!`

</details>


## Command Line Tools

Abra um novo terminal, copie e cole o seguinte comando e pressione `ENTER`:

```bash
xcode-select --install
```

Se você receber a mensagem a seguir, pode simplesmente pular esta etapa e ir para a próxima.
```bash
# command line tools are already installed, use "Software Update" to install updates
```

Caso contrário, abrirá uma janela perguntando se você deseja instalar algum software: clique em "Instalar" e aguarde.


:heavy_check_mark: Se você ver a mensagem "The software was installed" then all good :+1:

:x: Se o comando `xcode-select --install` falhar, tente novamente: às vezes os servidores Apple ficam sobrecarregados.

:x: If you see the message "Xcode is not currently available from the Software Update server", you need to update the software update catalog:

```bash
softwareupdate --clear-catalog
```

Once this is done, you can try to install again.


## Homebrew

[Homebrew](http://brew.sh/) is a package manager: it's a software used to install other software from the command line. Let's install it!

Open a terminal and run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

This will ask for your confirmation (hit `ENTER`) and your **macOS user account password** (the one you use to [log in](https://support.apple.com/en-gb/HT202860) when you reboot your Macbook).

:warning: When you type your password, nothing will show up on the screen, **that's normal**. This is a security feature to mask not only your password as a whole but also its length. Just type your password and when you're done, press `ENTER`.

If you already have Homebrew, it will tell you so, that's fine, go on.

Then install some useful software:

```bash
brew update
```

If you get a `/usr/local must be writable` error, just run this:

```bash
sudo chown -R $USER:admin /usr/local
brew update
```

Error message or not, proceed running the following in the terminal (you can copy / paste all the lines at once).

```bash
brew upgrade git         || brew install git
brew upgrade gh          || brew install gh
```


## Visual Studio Code

### Installation

Let's install [Visual Studio Code](https://code.visualstudio.com) text editor.

Copy (`Cmd` + `C`) the command below then paste it in your terminal (`Cmd` + `V`):

```bash
brew install --cask visual-studio-code
```

Then launch VS Code by running the following command in your terminal:

```bash
code
```

:heavy_check_mark: If a VS Code window has just opened, you're good to go :+1:


## Oh-my-zsh

Let's install the `zsh` plugin [Oh My Zsh](https://ohmyz.sh/).

In a terminal execute the following command:

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

If asked "Do you want to change your default shell to zsh?", press `Y`

At the end your terminal should look like this:

![Ubuntu terminal with OhMyZsh](images/oh_my_zsh.png)

:heavy_check_mark: If it does, you can continue :+1:



## GitHub CLI

CLI is the acronym of [Command-line Interface](https://en.wikipedia.org/wiki/Command-line_interface).

In this section, we will use [GitHub CLI](https://cli.github.com/) to interact with GitHub directly from the terminal.

It should already be installed on your computer from the previous commands.

First in order to **login**, copy-paste the following command in your terminal:

:warning: **DO NOT edit the `email`**

```bash
gh auth login -s 'user:email' -w
```

You will get the following output:

```bash
! First copy your one-time code: 0EF9-D015
- Press Enter to open github.com in your browser...
```

Select and copy the code (`0EF9-D015` in the example), then press `ENTER`.

Your browser will open and ask you to authorize GitHub CLI to use your GitHub account. Accept and wait a bit.

Come back to the terminal, press `ENTER` again, and that's it.

To check that you are properly connected, type:

```bash
gh auth status
```

:heavy_check_mark: If you get `Logged in to github.com as <YOUR USERNAME> `, then all good :+1:

Then run the following configuration line:

```bash
gh config set git_protocol ssh
```


## SSH Key

### Generation

We need to generate SSH keys which are going to be used by GitHub to authenticate you. You can think of it as a way to log in, but different from the well known username/password pair.

:warning: If you already generated keys that you already use with other services, you can skip this step.

Open a terminal and copy-paste this command, replacing the email with **yours** (the same one you used to create your GitHub account).

```bash
mkdir -p ~/.ssh && ssh-keygen -t ed25519 -o -a 100 -f ~/.ssh/id_ed25519 -C "TYPE_YOUR_EMAIL@HERE.com"
```

It will prompt for information. Just press enter until it asks for a **passphrase**.

:warning: When asked for a passphrase, put something you want and that you'll remember. It's a password to protect your private key stored on your hard drive.

:warning: When you type your passphrase, nothing will show up on the screen, **that's normal**. This is a security feature to mask not only your passphrase as a whole but also its length. Just type your passphrase and when you're done, press `ENTER`.

### Giving your public key to GitHub

Now, you will give your **public** key to GitHub.

In your terminal copy-paste the following command:

```bash
gh auth refresh -s write:public_key
```

It will prompt a one time code (####-####) on the screen. Copy it and press `ENTER`, then paste the code in your browser and follow the instructions to **Authorize GitHub**.

Back in the terminal, press `ENTER` and run this:

```bash
gh ssh-key add ~/.ssh/id_ed25519.pub
```

This should return `✓ Public key added to your account`. 

## Node.js

[Node.js](https://nodejs.org/en/) is a JavaScript runtime to execute JavaScript code in the terminal. Let's install it with [nvm](https://github.com/nvm-sh/nvm), a version manager for Node.js.

In a terminal, execute the following command:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.0/install.sh | zsh
```

Restart your terminal and run the following:

```bash
nvm -v
```

You should see a version.

Now let's install node:

```bash
nvm install 14.15
```

When the installation is finished, run:

```bash
node -v
```

:heavy_check_mark: If you see `v14.15`, the installation succeeded :+1:

:x: If not, **contact a teacher**


## yarn

[`yarn`](https://yarnpkg.com/) is a package manager to install JavaScript libraries. Let's install it:

In a terminal, run the following command:

```bash
npm install --global yarn
```

Restart your terminal and run the following command:

```bash
yarn -v
```

:heavy_check_mark: If you see a version, you're good :+1:
