# Adding a Git submodule

```
create repos for main and submodule @ github

create Main solution folder
cd main
git init
git remote add origin [git-repo-main]
git add .
gcmsg 'initial commit'
git push origin master

// from the main project dir
git submodule add [git-repo-submodule] [submodule-dir]
// this adds the subfolder

cd [submodule-dir]
touch README.md
echo 'testing' >> README.md

git add .
gcmsg 'initial commmit for submodule'
git remote -v // shows origin repo

git push origin master
```

### TBA Managing repos
[Git-Tools-Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

