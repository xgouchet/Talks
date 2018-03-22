
# Git Magic Tricks

_CodeMobile UK 2018_ 

---

## About… Xavier F. Gouchet

#### Lead Android Engineer at WorkWell <img src="logos/workwell.png" class="logo-inline"/>

#### Fluent in Android since Cupcake


###### <a>@xgouchet</a> on <i class="fa fa-github" aria-hidden="true"></i>, <i class="fa fa-stack-overflow" aria-hidden="true"></i>, <i class="fa fa-linkedin" aria-hidden="true"></i>, <i class="fa fa-twitter" aria-hidden="true"></i>, …

---

## Foreword

### Edit the config files : 

 - Local `/…/repo/.git/config`
 - Global (per user) : `~/.gitconfig`
 - System : `/etc/gitconfig`

```ini
[group]
  property = value
```

+++

### In the terminal

```shell
$ git config group.property "Foo"
$ git config --global group.property "Bar"
$ git config --system group.property "Baz"
```
+++

## Aliases

```ini
[alias]
  lg = log --pretty=format:"%C(yellow)%h %ad %Creset%s"
```

```shell
$ git lg
```

---

## You're here ↓

```ini
[alias]
  # WTF was I working on earlier… ?
  wtf = "!git status --short --branch; 
          echo -e '\nThe last commit was :'; 
          git l -1 --numstat"
```

+++

```ini
[alias]
  # log only my commits
  mine = log --author="$(git config user.email)"
  # log my commits since yesterday
  standup = !git mine --pretty=format:… --since yesterday
  # List most active authors 
  score = shortlog --numbered --summary --no-merges
```

---

## Working with branches

```ini
[alias]
  # dmb = delete-merged-branches
  dmb = "!git branch --no-color --merged | 
          egrep -v "(^\*|master|develop)" | 
          xargs -I{} git branch -d {}"
```

+++

```ini
[alias]
  # Update local branch
  update = "!git pull -r && git dmb && git wtf"
  # Synchronize with the remote repository
  sync = "!git pull -r && git push"
```

---

## Rewriting history

```ini
[alias]
  # Amend last commit
  amend = commit --amend
  # Amend without prompting for a message update
  comend = commit --amend --no-edit
  # Create a fixup commit (git fixup 35d15a2)
  fixup = "!f() { git commit --fixup=$1 }; f"
```

+++

## Rewriting history

```ini
[alias]
  # never push force !
  please = push --force-with-lease
```

+++

## To err is human, but a real disaster needs a git client

```ini
[alias]
  # Remove the changes from the index
  unstage = reset --mixed
  # Remove the last commit, keep the changes
  uncommit = reset --soft HEAD^
  # Delete the last commit with its changes ⚠
  rollback = reset --hard HEAD^
```

+++

![git areas](img/git_areas.png)

---

## I have sexdaily...
### _dislexia... damn_

```ini
[help]
  # execute the mistyped command after 50 deciseconds (5s)
  autoCorrect = 50


[alias]
  cehcout = checkout
  cmomit = commit
```

---

## An accident waiting to happen

```ini
[alias]
  steal = commit --amend --reset-author --no-edit
  yolo = commit -m "$(curl -s whatthecommit.com/index.txt)"
```

---

## Want more ‽

 - Search for `.gitconfig` on <i class="fa fa-github" aria-hidden="true"></i> gists
 - Search for `git aliases` on <i class="fa fa-stack-overflow" aria-hidden="true"></i> or just <i class="fa fa-google" aria-hidden="true"></i>
 - If you type it more than twice, make an alias of it

---

## Thanks for your attention

#### Any Question ? 

