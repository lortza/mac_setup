# Weekly Maintenance

## Run brewup
- Be sure all delicate apps are pinned
  - postgres
  - elasticsearch
- run `brewup`
  This is an alias for
  ```
  alias brewup='brew update; brew upgrade; brew prune; brew cleanup; brew doctor;'
  ```

## Updates Casks
- Check to see what's outdated
  ```
  brew cask outdated
  ```
- Update individual programs as you see fit
  ```
  brew cask reinstall name_of_cask
  ```
- Another options is to do them all at once, but you run the risk of upgrading one you didn't intend.
  ```
  brew cask outdated | xargs brew cask reinstall
  ```


## Shut Down
