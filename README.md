# macOS High Sierra v. 10.13 Setup

This is a simple list of instructions to make setting up my MacBook Pro as fast and efficient as possible for web development.

I followed [this gist by mikevallano](https://gist.github.com/mikevallano/d0964aeff471453060cf5c096859adac) and forked [this repo by taniarascia](https://www.taniarascia.com/setting-up-a-brand-new-mac-for-development/) as guides to made this version.

NOTE: I just created a `dotfiles` repo [here](https://github.com/lortza/dotfiles)

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
- Install Magnet
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

Tap the Support Services
```
brew tap caskroom/cask
brew tap homebrew/services
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

#### Option 1: Install Manually -- I did this

```shell
brew install git
brew install graphviz
brew cask install spectacle
brew cask install sublime-text
brew cask install atom
brew cask install harvest
brew cask install slack
brew cask install dropbox
brew cask install firefox
brew cask install gimp
brew cask install spotify
mas install 803453959        # Slack
```

- Check App Store for Updates & run them
- Restart Mac & check Console for errors

#### Option 2: Set up Brewfile -- I have not done this
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
cask 'spotify'

mas 'Slack', id: 803453959
```

```shell
brew bundle
```
Restart Mac & check Console for errors

## Install Node.js

```
brew install node
```

- Copy terminal output into [Evernote file](https://www.evernote.com/Home.action?_sourcePage=jpcfeMMHivriMUD9T65RG_YvRLZ-1eYO3fqfqRu0fynRL_1nukNa4gH1t86pc1SP&__fp=sw-znwOvMVg3yWPvuidLz-TPR6I9Jhx8&hpts=1537402481839&showSwitchService=true&usernameImmutable=false&rememberMe=true&login=&login=Sign+in&login=true&username=richardson.ae%40gmail.com&hptsh=uOH2K8MR8aY694GUXFCd468%2FbJQ%3D#n=12e4acd2-a9a1-41a7-aabc-5ceab533de79&s=s266&ses=4&sh=2&sds=5&)
- Check that Node works
  ```
  node
  ```
- Exit node


## Install NVM

- Install [Node Version Manager](https://github.com/creationix/nvm/blob/master/README.md)
```
brew install nvm
source $(brew --prefix nvm)/nvm.sh
```
- Copy terminal output into [Evernote file](https://www.evernote.com/Home.action?_sourcePage=jpcfeMMHivriMUD9T65RG_YvRLZ-1eYO3fqfqRu0fynRL_1nukNa4gH1t86pc1SP&__fp=sw-znwOvMVg3yWPvuidLz-TPR6I9Jhx8&hpts=1537402481839&showSwitchService=true&usernameImmutable=false&rememberMe=true&login=&login=Sign+in&login=true&username=richardson.ae%40gmail.com&hptsh=uOH2K8MR8aY694GUXFCd468%2FbJQ%3D#n=aa55a413-32c8-40a7-8956-ee1da7d7fbca&s=s266&ses=1&sh=5&sds=5&x=nvm%2520installation&)
- Run nvm
  ```
  nvm
  ```
- You should see a list of options. If you don't, see [this StackOverflow post](http://stackoverflow.com/questions/27651892/homebrew-installs-nvm-but-nvm-cant-be-found-afterwards)
- Restart computer & check console for errors


## Install RVM

- Install [Ruby Version Manager](https://rvm.io/rvm/install)
  ```
  \curl -sSL https://get.rvm.io | bash -s stable
  ```
- Copy terminal output into [Evernote file](https://www.evernote.com/Home.action?_sourcePage=jpcfeMMHivriMUD9T65RG_YvRLZ-1eYO3fqfqRu0fynRL_1nukNa4gH1t86pc1SP&__fp=sw-znwOvMVg3yWPvuidLz-TPR6I9Jhx8&hpts=1537402481839&showSwitchService=true&usernameImmutable=false&rememberMe=true&login=&login=Sign+in&login=true&username=richardson.ae%40gmail.com&hptsh=uOH2K8MR8aY694GUXFCd468%2FbJQ%3D#n=87807eea-365f-494e-a8d0-74ca5a097209&s=s266&ses=1&sh=5&sds=5&x=rvm%2520installation&)
- Add the path:
  ```
  source /Users/annerichardson/.rvm/scripts/rvm
  ```
- Run rvm to make sure it worked
  ```
  rvm
  ```
- Add [autolibs](https://rvm.io/rvm/autolibs) to automatically install dependencies
  ```
  rvm autolibs homebrew
  ```
- Install latest version of ruby
  ```shell
  rvm install ruby-head
  ```
- Set default ruby version
  ```shell
  rvm install "ruby-2.5.1"
  rvm --default use 2.5.1
  ```
- Install bundler
  ```shell
  gem install bundler
  ```

## Install PostgreSQL
A [useful guide](https://launchschool.com/blog/how-to-install-postgresql-on-a-mac)

```
brew install postgresql
```
- Copy terminal output into [Evernote file](https://www.evernote.com/Home.action?_sourcePage=jpcfeMMHivriMUD9T65RG_YvRLZ-1eYO3fqfqRu0fynRL_1nukNa4gH1t86pc1SP&__fp=sw-znwOvMVg3yWPvuidLz-TPR6I9Jhx8&hpts=1537402481839&showSwitchService=true&usernameImmutable=false&rememberMe=true&login=&login=Sign+in&login=true&username=richardson.ae%40gmail.com&hptsh=uOH2K8MR8aY694GUXFCd468%2FbJQ%3D#n=e2876634-af73-42ab-9454-b248e68fe942&s=s266&ses=1&sh=5&sds=5&x=postgres%2520installation&)
- Check that postgresql can be started and stopped
  ```
  brew services start postgresql

  # and shut it down again for now
  brew services start postgresql
  ```
- Enable auto-startup
  ```
  ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgents
  launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
  ```
- Install the `pg` gem
  ```
  gem install pg -- --with-pg-config=/usr/local/bin/pg_config
  ```
- Pin `postgres` in homebrew so it does not get updated automatically
  ```
  brew pin postgresql
  ```

## Install MySQL
TBD

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

- Create `git-completion` file
  ```
  touch ~/git-completion.bash
  subl ~/git-completion.bash
  ```
- Add copy all contents from the [master file](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash) into it and save
- Create `git-prompt` file
  ```
  touch ~/git-prompt.sh
  subl ~/git-prompt.sh
  ```
- Add copy all contents from the [master file](https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh) into it and save


## SSH Keys
Create SSH keys and connect them to GitHub and Bitbucket accounts.

- [Follow GitHub Guide](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) OR...
- Generate Keys
  ```
  ssh-keygen -t rsa -b 4096 -C "my_github_email@example.com"
  ```
- Press `Enter` to accept the default location
- Enter a passphrase
- Create new Secure Note in Lastpass & Save
  - Store passphrase
  - Store fingerprint
  - Store private key (filename: `id_rsa`)
  - Store public key (filename: `id_rsa.pub`)
- Add the SSH key to the local agent
  ```
  eval "$(ssh-agent -s)"
  ```
- For macOS Sierra 10.12.12 and later:
  - Create a ssh/config file:
    ```
    cd ~/.ssh ; touch config ; subl .
    ```
  - Add this info to `.ssh/config` and save:
    ```
    Host *
     AddKeysToAgent yes
     UseKeychain yes
     IdentityFile ~/.ssh/id_rsa
    ```
- Add the key to the agent
  ```
  ssh-add -K ~/.ssh/id_rsa
  ```
- [Add SSH key to GitHub](https://github.com/settings/keys) (Helpful [guide](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/))
- [Add SSH key to Bitbucket](https://bitbucket.org/account/user/annerichardson/ssh-keys/)


## Set up Terminal Preferences

- Open **Terminal > Preferences**
- **Terminal > Preferences > General:** Open new window with "Pro"
- **Terminal > Preferences > Profiles:** Set "Pro" as default
- **Terminal > Preferences > Profiles > Colors & Backgrounds:**
  - Change opacity to 100%
  - Change background color to softer gray

### Configure `~/.bash_profile`
Note: there is a dotfiles repo that has this information in it. See Dotfiles section below.
```
subl ~/.bash_profile
```

```shell
# Update and clean homebrow in one command
alias brewup='brew update; brew upgrade; brew prune; brew cleanup; brew doctor'
# note: psql is 'pinned' by using brew pin postgresql so that it's not updated automatically
# to upgrade psql, first do brew unpin postgresql

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
# export PS1="\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\$(parse_git_branch)\[\033[m\]\$ "
export PS1="$purple\u$green\$(parse_git_branch)$LIGHTBLUE \W $ $reset"

# Enable tab completion
source ~/git-completion.bash

# Change command prompt
source ~/git-prompt.sh
export GIT_PS1_SHOWDIRTYSTATE=1

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

## Set up file structure in `/Users/annerichardson/`
```
mkdir software_development && cd $_
mkdir contract_work
mkdir learning_academies
mkdir open_source
mkdir personal_projects
```

## Configure dotfiles
- My 2012 Mac dotfiles gist https://gist.github.com/lortza/32a0a39733200d6ef2b158ccb7364ffc
- My 2017 Mac dotfiles repo https://github.com/lortza/dotfiles

## Configure Atom

- Install Packages from: https://gist.github.com/lortza/ab0c5c9b436c9104a942370cb7e85186#file-atom_packages-txt
- Load Snippets from: https://gist.github.com/lortza/ab0c5c9b436c9104a942370cb7e85186#file-atom_snippets-cson
- Restart computer & check for console errors

## Configure Sublime
https://packagecontrol.io/installation

## Configure Magnet
- Start at login
- Allow it to control computer
- Shortcuts:
![alt](/screenshots/magnet.png)

## Install Ruby and Rails versions for Priority Projects

- tmdb:
  ```
  rvm install "ruby-2.2.2"
  rvm 2.2.2
  gem install rails -v 4.2.3
  ```
- tarot:
  ```
  rvm install "ruby-2.4.2"
  rvm 2.4.2
  gem install rails -v 5.1.4
  ```
- ftpg:
  ```
  rvm install "ruby-2.3.7"
  rvm 2.3.7
  gem install rails -v 4.1.2
  ```
- pp:
  ```
  rvm install "ruby-2.5.1"
  rvm 2.5.1
  gem install rails -v 5.2.0
  ```


## Mac Preferences (Round 2)
- **Desktop & Screen Saver > Desktop:** Set background image to something from Dropbox/\_PHOTOS/desktop_pictures
- **Printers & Scanners >** Add Printer
- **Users & Groups >** Change login photo to something better
- Statup applications: TBD

## Sign In to all Slack Teams
Use Magic links because it is way easier when doing so many at a time.
```
localflavor
yoloteamslack
wwc-atx
austinrb
austinonrails
refreshaustin
vikingcodeschool
nola
productmatchr
denver-devs
womenintech
rubyonrails-link
rubydevelopers
```

## Install Backblaze
TBD

## Set up TimeMachine
TBD

## Open & Sync Dropbox
- Sign in & choose "select folders"
- Deselect `iTunes Music` so it is not synced onto this computer

## Put Computer Details in Google Doc
- Create a file in [this folder](https://drive.google.com/drive/folders/0B2alZr-hRu53Ulh2dkhhOEEyNVU) with the stats for the computer. This will be useful later when I need to access that information remotely.

<!--

## npm

### Gulp

```shell
npm install --global gulp-cli
```

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
 -->


