# Rock the Gradle

## Rule the world

## <img src="logos/gradle.png" class="logo-inline"/> + <img src="logos/kotlin.png" class="logo-inline"/>

_Android Makers, 2018_ 

---

## About… Xavier F. Gouchet

#### Lead Android Engineer at WorkWell <img src="logos/workwell.png" class="logo-inline"/>

#### Fluent in Android since Cupcake


###### <a>@xgouchet</a> on <i class="fa fa-github"></i>, <i class="fa fa-stack-overflow"></i>, <i class="fa fa-linkedin"></i>, <i class="fa fa-twitter" aria-hidden="false"></i>, …

+++

### What we do at WorkWell <img src="logos/workwell.png" class="logo-inline"/>

`TODO  w/ marketing`

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

+++

- Works like _any_ module in your project
- Compiled **and tested** for any gradle task
- Groovy, Java, Kotlin

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

## Let's see some code

### <img src="logos/gradle.png" class="logo-inline"/> + <img src="logos/kotlin.png" class="logo-inline"/>

---

## Reminders 

 - Task & Extension classes **must be** open
 - `buildSrc` is always built and tested

---

## Thanks for your attention

#### Any Question ? 

[github.com/xgouchet/RockTheGradle](https://github.com/xgouchet/RockTheGradle)

