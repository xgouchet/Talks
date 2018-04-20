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

### What is Gradle ?

@ul
 - General purpose
 - Dependency Management System
 - Build management (dependency based)
@ulend

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

### Show of hands

@ul
 - Configured project in gradle
 - Wrote a custom task
 - Wrote a custom plugin
@ulend

---

## Meet the `buildSrc` folder

+++

```plain
┬📂 MyProject
├┬📂 app/
│├──📁 src/
│└──📄 build.gradle
├┬📂 buildSrc/
│├──📁 src/
│├──📄 build.gradle ?
│└──📄 settings.gradle
├─📄 build.gradle
└─📄 settings.gradle
```
@[1]
@[1,9-10]
@[1-4]
@[1,5-8]

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

## Diving in the good stuff

+++

### Step 1 : Create a `buildSrc` folder

+++

### Step 2 : … that's it

Default `build.gradle`

```gradle
apply plugin: 'groovy'
dependencies {
    compile gradleApi()
    compile localGroovy()
}
```

---

## Dependency Management

+++

### Before 
#### `app/build.gradle`

```groovy
dependencies {
 implementation"org.jetbrains.kotlin:kotlin-stdlib-jre7:$kotlin_version"

 implementation "com.android.support:appcompat-v7:$android_support_version"
 implementation "com.android.support:design:$android_support_version"
 implementation "com.android.support:support-annotations:$android_support_version"
}
```

+++

### After 
#### <i class="fa fa-edit" aria-hidden="true"></i> `buildSrc/src/main/kotlin/Dependencies.kt`

```kotlin
object Dependencies {
 object Versions {
  const val Kotlin = "1.2.30"
  const val AndroidSupportLib = "27.1.1"
 }

 object Libraries {
  const val KotlinJre7 = "org.jetbrains.kotlin:kotlin-stdlib-jre7:${Versions.Kotlin}"

  @JvmField
  val SupportLibs = arrayOf("com.android.support:appcompat-v7:${Versions.AndroidSupportLib}",
    "com.android.support:design:${Versions.AndroidSupportLib}",
    "com.android.support:support-annotations:${Versions.AndroidSupportLib}")
 }
}
```

+++

### After 
#### `app/build.gradle`

```groovy
import Dependencies

dependencies {
    implementation Dependencies.Libraries.KotlinJre7
    implementation Dependencies.Libraries.SupportLibs
}
```
---

### Sidenote on task management

+++

#### Dependency

@ul
 - `dependsOn`
 - `finalizedBy`
@ulend

+++

#### Ordering

@ul
 - `mustRunAfter`
 - `shouldRunAfter`
@ulend

---

## Reminders 

@ul
 - Tasks & Extensions classes **must be** open
 - DSL can go as deep as you need
 - `buildSrc` is always built and tested
 - Use `apply from: "$project.rootDir/config/findbugs.gradle"`
 - Your build code should be as clean as your production code
@ulend

---

## Thanks for your attention

#### Any Question ? 

[github.com/xgouchet/RockTheGradle](https://github.com/xgouchet/RockTheGradle)

