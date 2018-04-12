# Rock the Gradle

<img src="assets/gradle.png" class="logo-inline"/>

## Rule the world

_Android Makers, 2018_ 


---


## About… Xavier F. Gouchet

#### Lead Android Engineer at WorkWell 

#### Fluent in Android since Cupcake


###### <a>@xgouchet</a> on <i class="fa fa-github" aria-hidden="true"></i>, <i class="fa fa-stack-overflow" aria-hidden="true"></i>, <i class="fa fa-linkedin" aria-hidden="true"></i>, <i class="fa fa-twitter" aria-hidden="true"></i>, …

+++?image=assets/Slides_WW_EN.png&size=cover


---

## A brief Gradle <img src="assets/gradle.png" class="logo-inline"/> introduction

+++

### The Gradle algorithm

@ul
 - Initialization
 - Configuration
 - Execution
@ulend

Note:
- Initialisation : lists projects; 
- Config : create tasks, resolve dependencies; 
- Execution : select & execute tasks

+++

See it yourself using the command 

```bash
$ gradle build --profile
```

---

## Meet the `buildSrc` folder

+++

```
┬📂 MyProject
├┬📂 app/
│├──📁 src/
│└──📄 build.gradle
├┬📂 buildSrc/
│├──📁 src/
│└──📄 build.gradle
├─📄 build.gradle
└─📄 settings.gradle
```
@[1]
@[1,8-9]
@[1-4]
@[1,5-7]

+++

### How does it work ?

@ul
- Works like any module in your project 
- Compiled and _tested_ before any gradle task 
- Groovy, Java, Kotlin, … 
@ulend

+++

### What can it do for me ?

@ul
- Better dependency management 
- Helper classes / methods 
- Custom tasks in dedicated classes 
- Custom plugin 
- Local a versionned with the project
@ulend

---

## Let's see some code

+++

### Default `build.gradle`

```gradle
apply plugin: 'groovy'
dependencies {
    compile gradleApi()
    compile localGroovy()
}
```

---

## Reminders 

@ul
 - Tasks & Extensions classes **must be** open
 - `buildSrc` is always built and tested
 - Your build code should be as clean and maintained as your production code
     - SOLID, KISS, DRY
@ulend

---

## Thanks for your attention

#### Any Question ? 

[github.com/xgouchet/RockTheGradle](https://github.com/xgouchet/RockTheGradle)

