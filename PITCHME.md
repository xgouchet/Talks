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

## A brief Gradle introduction


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

##### Default `build.gradle`

```gradle
apply plugin: 'groovy'

dependencies {
    compile gradleApi()
    compile localGroovy()
}
```
@[1]
@[4]
@[5]

---

## Dependency Management

+++

### Before 
#### `app/build.gradle`

```groovy
dependencies {
 implementation"org.jetbrains.kotlin:kotlin-stdlib-jre7:1.2.30"

 implementation "com.android.support:appcompat-v7:27.1.1"
 implementation "com.android.support:design:27.1.1"
 implementation "com.android.support:support-annotations:27.1.1"
}
```

+++

### After 
#### `buildSrc/src/main/kotlin/Dependencies.kt`

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
@[2-5]
@[6-12]
@[7]
@[8-11]
@[8]

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

## Custom Task

#### A concrete example : 

Shared translations between <i class="fa fa-apple" aria-hidden="true"></i>, <i class="fa fa-android" aria-hidden="true"></i> and <i class="fa fa-windows" aria-hidden="true"></i>

+++

#### `buildSrc/src/main/kotlin/DownloadStrings.kt`

```kotlin
open class DownloadStrings : DefaultTask() {
 var languages : Array<String> = arrayOf()
 var path = ""

 @TaskAction
 fun performTask() {
  for (l in languages) {
   Fuel.download("http://192.168.1.42/$l/strings.xml")
    .destination { _, _ -> File("$path/src/main/res/values-$l/strings.xml") }
    .response { _, res, _ -> println("$l → ${res.statusCode}") }
  }
 }
}
```

@[1,13]
@[5,6,12]
@[2,3]
@[7,11]
@[8]
@[9]
@[10]

+++

#### `app/build.gradle`

```groovy
import DownloadStrings

task downloadStrings(type: DownloadStrings) {
    languages = ["en", "fr"]
    projectBasePath = projectDir
}
```

---

## Going Further

@ul
- Add an extension
- Task dependency
@ulend

+++

#### `buildSrc/src/main/kotlin/RemoteExt.kt`

```kotlin
open class RemoteExt(var languages: Array<String> = arrayOf(),
                     var remoteHost: String = "127.0.0.1")
```

+++

#### `buildSrc/src/main/kotlin/RemotePlugin.kt`

```kotlin
class RemoteL10n : Plugin<Project> {
  override fun apply(project: Project) {
    val ext = project.extensions
               .create("remoteStrings", RemoteExt::class.java)
    val task = project.tasks
               .create("downloadStrings", DownloadStrings::class.java)
               .apply {
        projectBasePath = project.projectDir.path
        configuration = ext
    }
    project.afterEvaluate { p -> p.tasks
        .withType(GenerateResValues::class.java){ it.dependsOn(task) }
    }
  }
}
```

@[1,15]
@[2,14]
@[3,4]
@[5,6]
@[5-10]
@[11-13]


+++

#### `app/build.gradle`

```groovy
// […]
import RemoteL10n
apply plugin: RemoteL10n

remoteStrings {
    languages = ["en", "fr"]
    remoteHost = "192.168.1.42"
}
```

+++


### Sidenote on task management

```kotlin
    project.afterEvaluate { p ->
      p.tasks
        .withType(GenerateResValues::class.java){ it.dependsOn(task) }
    }
```

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

## Going even further


@ul
- Create a DSL to configure flavors separately
@ulend


+++

#### `buildSrc/src/main/kotlin/RemoteExt.kt`

```kotlin
open class RemoteExt {
    var remoteHost: String = "127.0.0.1"
    var variants: NamedDomainObjectContainer<VariantL10n>? = null

    fun variants(configureClosure: Closure<VariantL10n>) {
        variants?.configure(configureClosure)
    }
}

open class VariantL10n(val name: String) {
    var languages: Array<String> = arrayOf()
}
```

@[10-12]
@[3]
@[5-7]

+++

#### `buildSrc/src/main/kotlin/RemotePlugin.kt`

```kotlin
class RemoteL10n : Plugin<Project> {
  override fun apply(project: Project) {
    val ext = project.extensions
               .create("remoteStrings", RemoteExt::class.java)
    ext.variants =  project.container(VariantL10n::class.java)

    // …
  }
}
```

@[3-4]
@[5]

+++

#### `app/build.gradle`

```groovy
remoteL10n {
    remoteHost = "192.168.1.42"
    variants {
        debug {
            languages = ["en"]
        }
        freeRelease  {
            languages = ["fr", "en"]
        }
        fullRelease  {
            languages = ["fr", "en", "es", "de"]
        }
    }
}
```
@[3-13]
@[4-6]
@[7-12]

---

## Testing your code

### #TestMatters

+++

```kotlin
class RemoteL10nTest {

    lateinit var fakeProject: Project

    @Before
    fun setUp() {
        fakeProject = ProjectBuilder.builder().build()

        fakeProject.plugins.apply(AppPlugin::class.java)
        fakeProject.plugins.apply(RemoteL10n::class.java)
        fakeProject.evaluate() // using a reflection UglyHack™
    }
}```

@[1,13]
@[3]
@[5-7,12]
@[9]
@[10]
@[11]

+++

```kotlin
class RemoteL10nTest {
  // …
  @Test fun addsExtension() {
    val extension = fakeProject.extensions
                           .getByName(RemoteL10n.EXTENSION_NAME)
    assert(extension is RemoteL10nExtension)
  }

  @Test fun addsTask() {
    val task = fakeProject.tasks.getByName(RemoteL10n.TASK_NAME)
    assert(task is DownloadStrings)
  }
}```

@[3-7]
@[4,5]
@[6]
@[9-12]
@[10]
@[11]

+++

### Unit Testing the task itself

@ul
- Harder to do directly 
- Delegate all business logic to a dedicated class
@ulend

+++

#### `buildSrc/src/main/kotlin/DownloadStrings.kt`

```kotlin
open class DownloadStrings : DefaultTask() {

    var projectBasePath = "."
    var configuration: RemoteExt = RemoteExt()

    @TaskAction
    fun doIt() {
        RemoteL10nFetcher(
                FuelDownloader(), 
                projectBasePath, 
                configuration
            ).fetchStrings()
    }
}
```

@[8-12]
@[9]
@[10]
@[11]
@[12]

---

## Tips and Tricks

+++

### Aliasing the plugin

#### `buildSrc/build.gradle`

```groovy
apply plugin: 'java-gradle-plugin'

gradlePlugin {
  plugins {
    remoteL10n {
      id = "remoteL10n"
      implementationClass = "com.packagename.RemoteL10n"
    }
  }
}```

@[1]
@[3-10]
@[5-8]

+++

### Aliasing the plugin

#### `app/build.gradle`

```groovy
apply plugin: "remoteL10n"
```

+++

### Add task category

#### `buildSrc/src/main/kotlin/DownloadStrings.kt`

```kotlin
open class DownloadStrings : DefaultTask() {

    init {
        group = "makers"
        description = "Downloads strings.xml from a remote server"
    }

    // …
}
```

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

