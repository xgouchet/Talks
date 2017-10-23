
## Jenkins Workshop


---

## Jenkins ???

+++

### What's Jenkins

 - Put simply, just a `cron` on steroids with a UI
    - Run task periodically (nightly, checks every *n* minutes)
    - Monitor SCM changes (do something for new branches, commits, PRs)
    - Run task on demand

+++

### What can a task do

 - Put simply ? Anything !
     - Build the app
     - Run tests / static analysis
     - Call APIs (Jira, GitHub, …)
     - Trigger other tasks
     - …

---

## Jenkins at Deezer

+++

## Hephaistos vs Artemis ?

 - Hephaistos : Dev oriented
 - Artemis : non dev (Q&A, PO, PM, …), betas, releases 
     - Warning ! No debug version are allowed to be build on Artemis

+++

## Managing Jenkins

 - Make sure the servers are up and running
     - A little bit of sysadmin required
 - Troubleshooting whenever a task goes red
 - Manage users permissions and forgotten passwords


---

## Jenkins servers sysadmin

+++

# Hands on ! 

## Let's get you some accounts

## Make sure that you have a decent terminal

#### (You might want to install Linux for this)

+++

```bash
sudo useradd michel
sudo passwd michel
sudo adduser michel sudo
```

+++

# Hands on !

## Where is Jenkins installed ? 
## The various symlinks and folders in play

```bash
sudo su jenkins
```

+++

# Hands on ! 

## Upgrading the OS

```bash
# Update the package list
sudo apt update
# List upgradable packages
sudo apt list --upgradable
# Upgrade the packages
sudo apt upgrade [packages]
```

+++

### Clean the APT cache

```
$sudo apt-get clean
```

+++

# Hands on ! 

## Troubleshooting the size issue

```bash
# disk space usage per partition
df -h
# disk space usage current folder
du -a --max-depth=1 . | sort -nr
```

---

# Jenkins Admin

+++

# Hands on ! 

## Upgrading the plugins

+++

# Hands on ! 

## Users (new accounts, passwords)

+++

# Hands on ! 

## User permissions

---

# Jenkins Jobs

+++

## Pipeline

 - Groovy based script language
 - Nodes
 - Steps

---

## Thanks for your attention

#### Any Question ? 

