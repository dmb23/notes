# Make bash the default shell in OS X

> **NOTE:** this might require a lot of configuration to work...

The goal is to have uniform config. Step one towards that goal is to use the GNU utils
wherever possible; step two is now a switch to bash. Let's see if this works...

The required steps are:

- install a current version of bash via brew: `brew install bash` (macOS ships with Bash 3.2,
  since this is the last version with GPLv2 apparently)
- whitelist the shell to allow use as a login shell
  - `which -a bash` shows also the path to the new shell
  - add the path (`/opt/homebrew/bin/bash` currently) to the file `/etc/shells`
- set the default shell via `chsh -s /opt/homebrew/bin/bash` (or rollback via `chsh -s /bin/zsh`)
