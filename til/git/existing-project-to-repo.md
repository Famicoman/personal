# Turn an existing project into a git repo

We have an existing project in some directory and want to turn it into a git project and push it to a remote.

```
cd <localdir>
git init
git add .
git commit -m 'message'
git remote add origin <url>
git push -u origin master
```

## Sources
* https://stackoverflow.com/questions/3311774/how-to-convert-existing-non-empty-directory-into-a-git-working-directory-and-pus