---
sidebar_position: 1
slug: /
---

## Git-Version-Control

- to see all git configuration files.

```
git config --list
```

- to set golbal git profile.

```
git config --global user.name "git user name"
git config --global user.email "git@gmail.com"
```

- clone git repo form github.

```
git clone https://git-repo-link.com
```

- adding files to staging area.

```
git add . // to add all files
git add file1 file2
```

- to see status. you can see all the untracted and staging files.

```
git status
```

- commit the changes on local. its create a local snapshot.

```
git commit -m 'commit msg'
```

- to push local snapshot on remote. use -u if you push your branch first time on github.

```
git push
or
git push origin branch_name
```

- to initilize a git.

```
git init
```

- add new remote to your local project.

```
git remote add origin https://git-repo-link.com
```

- to compare old snapshot to new changes.

```
git diff
```

- to see history. its shows commit msg, date and id.

```
git log
git log --oneline
```

- to see specifc commit changes.

```
git show commit_id
```

- to search in your history log.

```
git log --grep='example'
```

- rename files using git.

```
git mv old_file_name new_file_name
```

- track empty folder on git.

```
just create a .gitkeep file inside a empty folder.
```

- restore files staging area to working area. if we already added that file it will moved from staging to working.
- NOTE: if your file is already on working/untracked area then git restore command can remove all your changes on that file.

```
git restore --staged file_name
git restore .
```

- checkout a specific commit stage.
- NOTE - its not remove the letest code, its just show the preview of prevouse commit state.

```
git checkout commit_id
```

- revert/roll bak to an old state. this can roll back to a previsue commit state.

```
git revert commit_id
```
