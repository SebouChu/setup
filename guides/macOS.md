# macOS

## GitHub

If you don't have a GitHub account, sign up here: https://github.com/join


## Command Line Tools

Open a new terminal, copy-paste the following command and hit `ENTER`:

```bash
xcode-select --install
```

If you receive the following message, you can just skip this step and go to next step.

```bash
# command line tools are already installed, use "Software Update" to install updates
```

Otherwise, it will open a window asking you if you want to install some software: click on "Install" and wait.


## Homebrew

[Homebrew](http://brew.sh/) is a package manager: it's a software used to install other software from the command line. Let's install it!

Open a terminal and run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

This will ask for your confirmation (hit `ENTER`) and your **macOS user account password** (the one you use to [log in](https://support.apple.com/en-gb/HT202860) when you reboot your MacBook).

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
brew install git wget imagemagick jq openssl
```


## Atom

### Installation

Let's install Atom text editor.

Go to https://atom.io, download and install it.

Then you can launch it from your Applications or by running the following command in your terminal:

```bash
atom
```


## Atom Packages

### Installation

Let's install some useful packages to Atom.

Copy-paste the following commands in your terminal:

```bash
apm install atom-beautify
apm install emmet
apm install file-icons
apm install highlight-selected
```

Here is a list of the packages you are installing:
- [Atom Beautify](https://atom.io/packages/atom-beautify)
- [Emmet](https://atom.io/packages/emmet)
- [File Icons](https://atom.io/packages/file-icons)
- [Highlight Selected](https://atom.io/packages/highlight-selected)


## macOS Terminal Theme

Launch a terminal, click on `Terminal > Preferences` and set the "Pro" theme as default profile.

**Quit and restart** your terminal: it should now have a nice black background, easier on the eyes.


## Oh My Zsh

Let's install the `zsh` plugin [Oh My Zsh](https://ohmyz.sh/).

In a terminal execute the following command:

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

If asked "Do you want to change your default shell to zsh?", press `Y`

At the end your terminal should look like this:


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

Go to [this page](https://github.com/settings/keys), click on the green button "New SSH key".

Write "My Computer" in the title, and for the key, copy-paste the result of the following command:

```bash
cat ~/.ssh/id_ed25519.pub
```

It should begins with `ssh-ed25519` and ends with your email.


## rbenv

Let's install [`rbenv`](https://github.com/rbenv/rbenv), a software to install and manage `ruby` environments.

First, we need to clean up any previous Ruby installation you might have:

```bash
rvm implode && sudo rm -rf ~/.rvm
# If you got "zsh: command not found: rvm", carry on. It means `rvm` is not
# on your computer, that's what we want!

sudo rm -rf $HOME/.rbenv /usr/local/rbenv /opt/rbenv /usr/local/opt/rbenv
```

:warning: This command may prompt for your password.

:warning: When you type your password, nothing will show up on the screen, **that's normal**. This is a security feature to mask not only your password as a whole but also its length. Just type your password and when you're done, press `ENTER`.

Then in the terminal, run:

```bash
brew install rbenv
```

When it's done, run:

```bash
echo 'eval "$(rbenv init - zsh)"' >> ~/.zshrc
```

Then quit **all your opened terminal windows** (`Cmd` + `Q`) and restart one.


## Ruby

### Installation

Now, you are ready to install the latest [ruby](https://www.ruby-lang.org/en/) version and set it as the default version.

Run this command, it will **take a while (5-10 minutes)**

```bash
rbenv install 3.0.3
```

Once the ruby installation is done, run this command to tell the system to use the 3.0.3 version by default.

```bash
rbenv global 3.0.3
```

Then **restart** your terminal again (close it and reopen it).

```bash
ruby -v
```

**NOTE**: If you have an Apple Silicon chip (M1, M1 Pro, M1 Max) and you try to install legacy Ruby versions, it might fail. You need a little trick on the `rbenv install` command, for example, to install Ruby 2.5.5:

```bash
RUBY_CFLAGS="-Wno-error=implicit-function-declaration" rbenv install 2.5.5
```

### Installing some gems

In the ruby world, we call external libraries `gems`: they are pieces of ruby code that you can download and execute on your computer. Let's install some!

In your terminal, copy-paste the following command:

```bash
gem install bundler jekyll 'rails:~>6.1'
```

Rerun the command to install the gems.

:warning: **NEVER** install a gem with `sudo gem install`! Even if you stumble upon a Stack Overflow answer (or the terminal) telling you to do so.


## Node.js

[Node.js](https://nodejs.org/en/) is a JavaScript runtime to execute JavaScript code in the terminal. Let's install it with [nvm](https://github.com/nvm-sh/nvm), a version manager for Node.js.

In a terminal, execute the following command:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | zsh
```

Restart your terminal and run the following:

```bash
nvm -v
```

You should see a version. If not, ask a teacher.

Now let's install node:

```bash
nvm install --lts
```

When the installation is finished, run:

```bash
nvm alias default node
```


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


## PostgreSQL

For storing data in your Rails applications, you'll need something called [PostgreSQL](https://www.postgresql.org/), an open-source robust and production-ready database system.

Let's install it now.

Run the following commands:

```bash
brew install postgresql
brew services start postgresql
```

Once you've done that, let's check that it worked:

```bash
psql -d postgres
```

If you enter a new prompt like this one, you're good!

```bash
psql (13.3)
Type "help" for help.

postgres=#
```

To quit it, type `\q` then `Enter`.

## ActiveStorage Preview libraries

In Rails applications, we use ActiveStorage to upload files to services like Amazon S3, GCS, etc. To display video and PDF previews, we need FFmpeg and Poppler.

```bash
brew install ffmpeg poppler
```
