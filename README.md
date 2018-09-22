# macOS High Sierra v. 10.13 Setup

This is a simple list of instructions to make setting up your Apple computer as fast and efficient as possible for web development.

I followed [this gist by mikevallano](https://gist.github.com/mikevallano/d0964aeff471453060cf5c096859adac) and forked [this repo by taniarascia](https://www.taniarascia.com/setting-up-a-brand-new-mac-for-development/) as guides to made this version.

## Set System Preferences (Round 1)

- **Track Pad:** Speed, Click, Secondary Click
- **Dock:** Size
- **Security and Privacy > General >** App Store and identified developers
- **Security and Privacy > Firewall >** On
- **Displays > Display >** Uncheck "Show mirroring options in menu bar"
- **Displays > Night Shift >** Set schedule and temperature
- **App Store >** Check: "Install app updates"
- **App Store Password Settings >** Free Downloads: Save Password
- **Sharing >** Off
- **Date & Time >** Show date


## In the App Store

### Run Updates

- Do all OS updates
- Do all system default software updates
- Restart computer again after all updates
- Check Console for errors

### Install Purchased

- Install CopyClip
- Install Evernote, sign in
- Restart computer again after all updates
- Check Console for errors

## Clean up Dock

- Remove all unused icons from dock

## Homebrew

Install Homebrew
```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Tap Cask
```
brew tap caskroom/cask
```

Install Google Chrome
```
brew cask install google-chrome
```
Open, Sign In, and load these instructions.

### Install Mac App Store Interface

```shell
brew install mas
```

#### Sign in to App Store

```shell
mas signin [my_apple_id]
```
May get `Error: Already signed in`

### Install Apps

#### Option 1: Set up Brewfile -- I have not done this
Brew bundle's uild is currently failing, so I chose to do the manual install on 9/21/18.

```shell
touch Brewfile
```

```shell
brew 'git'

cask 'spectacle'
cask 'sublime-text'
cask 'atom'
cask 'harvest'
cask 'slack'
cask 'dropbox'
cask 'firefox'
cask 'spectacle'
cask 'gimp'

mas 'Slack', id: 803453959
```

```shell
brew bundle
```
Restart Mac & check Console for errors

#### Option 2: Install Manually -- I did this

```shell
brew install git
brew cask install spectacle
brew cask install sublime-text
brew cask install atom
brew cask install harvest
brew cask install slack
brew cask install dropbox
brew cask install firefox
brew cask install gimp
mas install 803453959        # Slack
```

- Check App Store for Updates & run them
- Restart Mac & check Console for errors


## Configure Git

This sets up the defaults for how you interact with Git.

Set up the github config file
```
subl ~/.gitconfig
```

In the `.gitconfig` file:
```shell
[user]
  name   = Firstname Lastname
  email  = you@example.com
[github]
  user   = my_github_username
[alias]
  a      = add
  c      = commit
  ca     = commit -a
  cam    = commit -am
  cm     = commit -m
  s      = status
  pom    = push origin master
  pog    = push origin gh-pages
  puom   = pull origin master
  puog   = pull origin gh-pages
  cob    = checkout -b
  co     = checkout
  l      = log --oneline --decorate --graph
  lall   = log --oneline --decorate --graph --all
  ls     = log --oneline --decorate --graph --stat
  lt     = log --graph --decorate --pretty=format:'%C(yellow)%h%Creset%C(auto)%d%Creset %s %Cgreen(%cr) %C(bold blue)%an%Creset'
[credential]
  helper = osxkeychain
[core]
  editor = subl -n -w
[color]
  diff = auto
  status = auto
  branch = auto
  ui = auto
[merge]
  conflictstyle = diff3
```

## SSH

SSH Keys
- [Follow GitHub Guide](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) OR...
- Generate Keys `ssh-keygen -t rsa -b 4096 -C "my_github_email@example.com"`
- Press `Enter` to accept the default location
- Enter a passphrase
- Create new Secure Note in Lastpass & Save
  - Store passphrase
  - Store fingerprint
  - Store private key (`id_rsa`)
  - Store public key (`id_rsa.pub`)
- Add the SSH key to the local agent `eval "$(ssh-agent -s)"`
- For macOS Sierra 10.12.12 and later:
  - Create a ssh/config file: `cd ~/.ssh ; touch config`
  - Add this info to it and save:
  ```
  Host *
   AddKeysToAgent yes
   UseKeychain yes
   IdentityFile ~/.ssh/id_rsa
  ```
- Add the key to the agent `ssh-add -K ~/.ssh/id_rsa`
- [Add SSH key to GitHub](https://github.com/settings/keys) (Helpful [guide](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/))
- [Add SSH key to Bitbucket](https://bitbucket.org/account/user/annerichardson/ssh-keys/)

### Config - `~./ssh/config`

```shell
Host example
    HostName example.com
    User example-user
    IdentityFile key.pem
```

### Generate SSH key

```shell
ssh-keygen -t rsa -b 4096 -C "you@example.com"
eval "$(ssh-agent -s)"
ssh-add -K ~/.ssh/id_rsa
```

## Bash

### Config - `~/.bash_profile`

```shell
# Update and clean homebrow in one command
alias brewup='brew update; brew upgrade; brew prune; brew cleanup; brew doctor'

# prompt colors!
RED='\[\e[1;31m\]'
YELLOW='\[\e[0;33m\]'
BOLDYELLOW='\[\e[1;33m\]'
GREEN='\[\e[0;32m\]'
BLUE='\[\e[1;34m\]'
DARKBROWN='\[\e[1;33m\]'
DARKGRAY='\[\e[1;30m\]'
CUSTOMCOLORMIX='\[\e[1;30m\]'
DARKCUSTOMCOLORMIX='\[\e[1;32m\]'
LIGHTBLUE="\[\033[0;36m\]"
BOLDLIGHTBLUE="\[\033[1;36m\]"
BOLDPURPLE='\[\e[1;35m\]'

green="\[\033[0;32m\]"
blue="\[\033[0;34m\]"
purple="\[\033[0;35m\]"
reset="\[\033[0m\]"

# Add colors to Terminal
export CLICOLOR=1
export LSCOLORS=ExFxBxDxCxegedabagacad

# Get Git branch
parse_git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

# Format to user@host:/path/to/directory (branch-name)
export PS1="\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\$(parse_git_branch)\[\033[m\]\$ "

# Git Aliases
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'
alias gco='git checkout'
alias gb='git branch'
alias gl='git log'
alias glp="git log --pretty=format:'%h - %an, %ar: %s'"
alias glo='git log --oneline'
```



set up file structure in `/Users/annerichardson/`
```
mkdir software_development
cd software_development
mkdir contract_work
mkdir learning_academies
mkdir open_source
mkdir personal_projects
```

## Configure dotfiles
from https://gist.github.com/lortza/32a0a39733200d6ef2b158ccb7364ffc


## Configure Atom

### Install Packages
from https://gist.github.com/lortza/ab0c5c9b436c9104a942370cb7e85186#file-atom_packages-txt
### Load Snippets
from https://gist.github.com/lortza/ab0c5c9b436c9104a942370cb7e85186#file-atom_snippets-cson

<!--
## Node.js

### Download Node

```shell
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash
```

```shell
nvm install node
```

```shell
nvm use node
```

#### Update Node.js

```shell
nvm install node --reinstall-packages-from=node
```

## npm

### Gulp

```shell
npm install --global gulp-cli
```

## Ruby Version Manager

### Download rvm

```shell
\curl -sSL https://get.rvm.io | bash -s stable
```

### Install Ruby version

```shell
rvm install ruby-head
```

```shell
rvm --default use 2.4.0
```

```shell
gem install bundler
```

## Install Composer

```shell
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```


## Mac Preferences (Round 2)

- **Printers & Scanners >** TBD
- **Users & Groups >** TBD
- Statup applications


### Show Library folder

```shell
chflags nohidden ~/Library
```

### Show hidden files

This can also be done by pressing `command` + `shift` + `.`.

```shell
defaults write com.apple.finder AppleShowAllFiles YES
```

### Show path bar

```shell
defaults write com.apple.finder ShowPathbar -bool true
```

### Show status bar

```shell
defaults write com.apple.finder ShowStatusBar -bool true
```

### Disable unidentified developer warnings

```shell
sudo spctl --master-disable
```
 -->


## Put Computer details in Google Doc

- Create a file in [this folder](https://drive.google.com/drive/folders/0B2alZr-hRu53Ulh2dkhhOEEyNVU) with the stats for the computer. This will be useful later when I need to access that information remotely.




