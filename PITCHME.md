# Rock the Gradle

## Rule the world

## <img src="logos/gradle.png" class="logo-inline"/>

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

## Dependencies Management

<small>Credits to [Sam Edwards‏](https://handstandsam.com/2018/02/11/kotlin-buildsrc-for-better-gradle-dependency-management/) (<i class="fa fa-twitter"></i> @HandstandSam)</small>

+++

##### Create `buildSrc/src/main/…/Dependencies.kt`

```kotlin
object Dependencies {
  object Versions {
    const val SupportLib = "26.1.0"
    const val RxJava = "2.1.9"
  }
  object Libraries {
    @JvmField
    val SupportLib = listOf(
  "com.android.support:cardview-v7:${Versions.SupportLib}",
  "com.android.support:appcompat-v7:${Versions.SupportLib}")
    const val RxJava 
      = "io.reactivex.rxjava2:rxjava:${Versions.RxJava}"
  }
}
```

+++

##### Edit your `app/build.gradle`

```gradle
import com.sample.Dependencies

dependencies {
  implementation Dependencies.Libraries.AndroidSupport
  api Dependencies.Libraries.RxJava
}
```

+++

### Pros & Cons

 - Pros
    - Autocomplete when editing your gradle
    - Single definition for multi-module-project
    - Readability & Separation of concerns
 - Cons
    - Incompatible with Android Studio dependency management

---

## Create a Plugin

#### Case study : Localisation Plugin

+++

##### Create `buildSrc/src/main/…/L10nPlugin.kt`

```kotlin
class L10nPlugin : Plugin<Project> {

    override fun apply(project: Project) {
        // TODO Add DSL extensions 

        // TODO Add Task(s)

    }
}
```

+++

##### Edit your `app/build.gradle`

```gradle
import com.sample.L10nPlugin

apply plugin : L10nPlugin
```


---

## Thanks for your attention

#### Any Question ? 

