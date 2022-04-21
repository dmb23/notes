# Configuring git

## reasonable global config

Config globally with `git config --global [setting]`. Check where config is stored with `git config --list --show-origin`.

- `pager.branch false` git pipes output of e.g. branch into a pager (less by default). Turn it off to see the output still for the next command.
- `user.name "My Name"`
- `user.email myemail@example.com`
- `alias.tnylog=log --oneline --graph --decorate` to quickly see what is happening (if `tig` is not installed)


## update local config

You can override project-wide settings with `git config --local`. This is then stored in the local `.git/config`.

