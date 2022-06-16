# Move recent commits from one branch to another

*The situation:* I just happily coded and three commits in I realise I am still on master / develop instead of the feature branch I want to be.

*The solution:* 

```bash
git checkout -b newbranch HEAD~3
git branch --set-upstream-to=oldbranch
git cherry-pick ..oldbranch
git branch --force oldbranch oldbranch~3
git branch --unset-upstream
```

for a detailed discussion see [this SO answer](https://stackoverflow.com/a/36463546)
