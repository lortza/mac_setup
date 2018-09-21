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

May get `Error: Already signed in`

```shell
mas signin [my_apple_id]
```

### Set up Brewfile

```shell
touch Brewfile
```

```shell
tap 'caskroom/cask'

brew 'git'
brew 'npm'

cask 'visual-studio-code'
cask 'firefox'
cask 'gimp'
cask 'google-chrome'
cask 'opera'
cask 'spectacle'
cask 'sequel-pro'
cask 'utorrent'
cask 'vlc'
cask 'macdown'

mas 'Slack', id: 803453959
mas 'Sip', id: 507257563
mas 'Simplenote', id: 692867256
mas 'Todoist', id: 585829637
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





