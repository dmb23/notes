# Rollback changes to git repositories

One of the most-praised advantages of git repositories: you can roll back any changes, when it turns out they fail in production. But how?

## `git revert`

create a new commit that undoes all changes of a previous commit. 

- really good to rollback a rollback
- possible to collect multiple commits via `git revert --no-commit B; git revert --no-commit A; git commit -m 'rollback of A and B'`
- **Leads to wierd issues when reverting a merge commit!**

## `git checkout`

It is possible to `git checkout -f old_commit` (stackoverflow recommends `git checkout -f old_commit -- .`) to overwrite local files with
the state of an older reference.

- nice way to revert multiple commits at once
- works with merge commits
- **added files will not be deleted!**

## `git reset`

re-writes history, which is why I don't want to look into it. Good for local repositories or feature branches.

### `git reset` magic:

To revert from D to A, stackoverflow recommends: `git reset --hard A; git reset --soft D; git commit;`

- apparently that works for everything
- apparently it is time that I understand `git reset`

