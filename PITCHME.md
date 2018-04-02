
# Git Magic Tricks

_CodeMobile UK 2018_ 

---

## About… Xavier F. Gouchet

#### Lead Android Engineer at WorkWell 
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

---

### In the terminal

```shell
$ git config group.property "Foo"
$ git config --global group.property "Bar"
$ git config --system group.property "Baz"
```

---

## Aliases

```ini
[alias]
  lg = log --pretty=format:"%Cyellow%h %ad %Cwhite%s"
```

```shell
$ git lg
```

---

### You're here ↓

```ini
[alias]
  # WTF was I working on earlier… ?
  wtf = "!git status --short --branch; 
          echo -e '\nThe last 3 commits was :'; 
          git lg -3 --numstat"
```

---

### Short term memory loss

```ini
[alias]
  # log only my commits
  mine = lg --author="$(git config user.email)"

  # log my commits since yesterday
  standup = !git mine --since yesterday
```

---

### Take out the trash

```ini
[alias]
  # dmb = delete-merged-branches
  dmb = "!git branch --no-color --merged | 
          egrep -v "(^\*|master|develop)" | 
          xargs -I{} git branch -d {}"
```

---

### What's up, doc ?


```ini
[alias]
  update = "!git pull -r && git dmb && git wtf"

  sync = "!git pull -r && git push"
```

---

### Rewriting history

```ini
[alias]
  # Amend last commit
  amend = commit --amend

  # Amend without prompting for a message update
  comend = commit --amend --no-edit

  # Create a fixup commit (git fixup 35d15a2)
  fixup = commit --fixup
```

---

### Can i have some more, please ?

```ini
[alias]
  # never push force !
  please = push --force-with-lease
```

---

### To err is human, but a real disaster needs a git client

```ini
[alias]
  # undo `git [add|rm] …`
  unstage = reset --mixed

  # undo `git commit …`, keep the changes
  uncommit = reset --soft HEAD^

  # undo `git commit …`, drop the changes ⚠
  rollback = reset --hard HEAD^
```
---

### I have sexdaily...
##### _dislexia..._

```ini
[help]
  # execute the mistyped command after 50 deciseconds (5s)
  autoCorrect = 50

```

### Damn autocorrect!

```ini
[alias]
  cehcout = checkout
  cmomit = commit
```

---

### An accident waiting to happen

```ini
[alias]
  yolo = "!git add -a && 
        commit -m "$(curl -s whatthecommit.com/index.txt)"
```
 - “Some fixes.”
 - “Should work now… I think”
 - “You won't believe what this developer did to fix the bug !”

---

## Want more ?

 - <i class="fa fa-search" aria-hidden="true"></i> `.gitconfig` on <i class="fa fa-github" aria-hidden="true"></i> gists
 - <i class="fa fa-search" aria-hidden="true"></i> `git aliases` on <i class="fa fa-stack-overflow" aria-hidden="true"></i> or just <i class="fa fa-google" aria-hidden="true"></i>

> If you type it more than twice, make an alias of it

---

# Demo time

---

# ~~Demo time~~

---

# Questions

---

# ~~Questions~~

---

# Git Hooks

### &nbsp;

---

# ~~Git Hooks~~

### Next time… maybe ?

#### Thank you for your attention
