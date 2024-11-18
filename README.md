# macOS High Sierra v. 10.13 Setup

This is a simple list of instructions to make setting up my MacBook Pro as fast and efficient as possible for web development.

This guide is based on:
- [this gist by mikevallano](https://gist.github.com/mikevallano/d0964aeff471453060cf5c096859adac)
- [this repo](https://github.com/taniarascia/mac),
- [and this post by taniarascia](https://www.taniarascia.com/setting-up-a-brand-new-mac-for-development/)


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

### Install Apps Purchased from AppStore

- CopyClip

## Clean up Dock

- Remove all unused icons from dock

## Configure dotfiles
Cloning a dotfiles repo into your root folder will handle the setup of a lot of basic settings.
- My 2017 Mac dotfiles repo https://github.com/lortza/dotfiles
- My 2012 Mac dotfiles gist https://gist.github.com/lortza/32a0a39733200d6ef2b158ccb7364ffc

### What's Configured by dotfiles repo
- .bash_profile
- .bashrc
- .gemrc
- .gitconfig
- .gitignore
- .gitignore_global
- .irbrc
- .my_scripts.sh
- .profile
- .rvmrc
- .zlogin
- .zshrc
- git-completion.bash _you may want to copy a fresh version from the [master file](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash) in here_
- git-prompt.sh _you may want to copy a fresh version of the [master file](https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh) in here_

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

There is a file in this repo called `homebrew_apps.txt`. This file contains the list of all of the homebrew apps I like to install. Install them all at once with: 

```shell
xargs brew install < my/path/to/homebrew_apps.txt
```

## Install Node.js
- Install node
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

## Install Yarn
See [docs](https://yarnpkg.com/lang/en/docs/install/#mac-stable). Exclude installing Node.js so that nvm’s version of Node.js is used.
```
brew install yarn --without-node
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

## Install MySQL -- If needed
Decide whether MySQL or MariaDB is needed. Install only 1, as they conflict.

```
brew install mysql
```
- Copy terminal output into [Evernote file](https://www.evernote.com/Home.action?_sourcePage=jpcfeMMHivriMUD9T65RG_YvRLZ-1eYO3fqfqRu0fynRL_1nukNa4gH1t86pc1SP&__fp=sw-znwOvMVg3yWPvuidLz-TPR6I9Jhx8&hpts=1537402481839&showSwitchService=true&usernameImmutable=false&rememberMe=true&login=&login=Sign+in&login=true&username=richardson.ae%40gmail.com&hptsh=uOH2K8MR8aY694GUXFCd468%2FbJQ%3D#n=3dfb2610-b838-4047-8147-5ca0e0055311&s=s266&ses=1&sh=5&sds=5&x=mysql%2520instal&)
- Start agent for current version
  ```
  ln -sfv /usr/local/opt/mysql/*.plist ~/Library/LaunchAgents
  launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
  ```
- Pin `mysql` in homebrew so it does not get updated automatically
  ```
  brew pin mysql
  ```


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

## Install Heroku CLI
- Go to Heroku's [Dev Center](https://devcenter.heroku.com/articles/heroku-cli) for reference
- Install the cli tools
  ```
  brew install heroku/brew/heroku
  ```
- Set up autocomplete (instructions [here](https://docs.brew.sh/Shell-Completion)) by adding this to the `.bashrc` file.
  ```
  if type brew 2&>/dev/null; then
    for completion_file in $(brew --prefix)/etc/bash_completion.d/*; do
      source "$completion_file"
    done
  fi
  ```
- Then run:
  ```
  heroku autocomplete --refresh-cache
  ```

## Set up Terminal Preferences

- Open **Terminal > Preferences**
- **Terminal > Preferences > General:** Open new window with "Pro"
- **Terminal > Preferences > Profiles:** Set "Pro" as default
- **Terminal > Preferences > Profiles > Colors & Backgrounds:**
  - Change opacity to 100%
  - Change background color to softer gray


## Set up file structure in `/Users/annerichardson/`
```
mkdir software_development && cd $_
mkdir contract_work
mkdir learning_academies
mkdir open_source
mkdir personal_projects
```

## Show Library folder
```shell
chflags nohidden ~/Library
```

## Configure Atom
- **Settings > Packages > Autosave:** Check "Enabled"
- **Settings > Core > Exclude VCS Ignored Paths:** false
- Install Packages from this list: https://github.com/lortza/mac_setup/blob/master/atom_setup/list_of_packages.txt
- Paste settings into all of the config files in this folder:
- Atom Folder: https://github.com/lortza/mac_setup/tree/master/atom_setup
  - config.cson
  - keymap.cson
  - snippets.cson
  - styles.less
- Restart computer & check for console errors

## Configure Sublime
- Install package control: https://packagecontrol.io/installation
- Install Packages:
  - GitGutter
- Set up Preferences
- Add folder of snippets
- Add purchase key

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

## Install awesome_print
- [Globally install awesome_print](https://pennyforyourcode.com/installing-a-ruby-gem-globally-in-rvm-ffa7222f7e7)
  ```
  rvm @global do gem install awesome_print end
  ```
- Add awesome_print to irb
  ```
  subl ~/.irbrc
  ```
  Add these lines to `.irbrc`
  ```
  require 'awesome_print'
  AwesomePrint.irb!
  ```
- There may be a little more to this process...

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
