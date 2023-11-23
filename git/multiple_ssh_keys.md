# How to manage multiple git identities

Sometimes I need to manage multiple identities to authenticate for repositories:
E.g. I have my personal account for github, but work in a Project where the customer
also uses github and provides an account for me (authorized on the project repos).

A workflow that works for me is:

- create two ssh keys (`github_id.rsa` and `project_id.rsa`)
    - and add them for the different identities
- update the `~/.ssh/config` to define multiple hosts for github (see example below)
- clone the project repositories with an updated command, updateing the hostname accordingly
    - e.g. `git clone git@github.com-project:project/repo-name.git`
- run `git config --local ...` for the different repos to match the expected identities

```yaml
Host github.com
  IdentityFile ~/.ssh/github_id_rsa

Host github.com-project
  HostName github.com
  IdentityFile ~/.ssh/project_id_rsa
```
