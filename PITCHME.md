# Rock the Gradle

### ![](assets/gradle.png) <!-- .element class="logo" -->

## Rule the world

_Android Makers, 2018_ 


---


## About… Xavier F. Gouchet

#### Lead Android Engineer at WorkWell 

#### Fluent in Android since Cupcake


###### <a>@xgouchet</a> on <i class="fa fa-github" aria-hidden="true"></i>, <i class="fa fa-stack-overflow" aria-hidden="true"></i>, <i class="fa fa-linkedin" aria-hidden="true"></i>, <i class="fa fa-twitter" aria-hidden="true"></i>, …

+++?image=assets/Slides_WW_EN.png&size=cover

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

- Works like any module in your project <!-- .element class="fragment" -->
- Compiled and tested before any gradle task <!-- .element class="fragment" -->
- Groovy, Java, Kotlin, … <!-- .element class="fragment" -->

+++

### What can it do for me ?

- Better dependency management <!-- .element class="fragment" -->
- Helper classes / methods <!-- .element class="fragment" -->
- Custom tasks in dedicated classes <!-- .element class="fragment" -->
- Custom plugin <!-- .element class="fragment" -->

All of this local && versionned with the project <!-- .element class="fragment" -->

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

 - Tasks & Extensions classes **must be** open
 - `buildSrc` is always built and tested
 - Your build code should be as clean and maintained as your production code
     - SOLID, KISS, DRY

---

## Thanks for your attention

#### Any Question ? 

[github.com/xgouchet/RockTheGradle](https://github.com/xgouchet/RockTheGradle)

