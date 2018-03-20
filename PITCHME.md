# Rock the Gradle

## Rule the world

## <img src="logos/gradle.png" class="logo-inline"/>

_Android Makers, 2018_ 

---

## About… Xavier F. Gouchet

#### Lead Android Engineer at WorkWell <img src="logos/workwell.png" class="logo-inline"/>

#### Fluent in Android since Cupcake


###### <a>@xgouchet</a> on <i class="fa fa-github" aria-hidden="true"></i>, <i class="fa fa-stack-overflow" aria-hidden="true"></i>, <i class="fa fa-linkedin" aria-hidden="true"></i>, <i class="fa fa-twitter" aria-hidden="true"></i>, …

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

```
apply plugin: 'groovy'
dependencies {
    compile gradleApi()
    compile localGroovy()
}
```

+++



---

## Thanks for your attention

#### Any Question ? 

