# macOS High Sierra v. 10.13 Setup

[View a more detailed explanation of these steps here.](https://www.taniarascia.com/setting-up-a-brand-new-mac-for-development/)

This is a simple list of instructions to make setting up your Apple computer as fast and efficient as possible for web development.

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

#### Option 1: Set up Brewfile

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

#### Option 2: Install Manually

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
mas install 803453959
```

## GitHub

### Config - `~/.gitconfig`


```shell
[user]
  name   = Firstname Lastname
  email  = you@example.com
[github]
  user   = hunter2
[alias]
  a      = add
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
```


## SSH

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

# Add colors to Terminal
export CLICOLOR=1
export LSCOLORS=ExFxBxDxCxegedabagacad

# Get Git branch
parse_git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

# Format to user@host:/path/to/directory (branch-name)
export PS1="\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\$(parse_git_branch)\[\033[m\]\$ "
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




