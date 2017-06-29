
# What's new in our test libraries

_Deezer_

---

# Writing tests with kotlin

_Deezer_

---

## Writing tests the old way

> ♫ You're thinking of me, the same old way.  ♪
> 
> — The Beatles

+++

### ⇧⌘A ¹ + Convert Java File to Kotlin File

_or_ 

### ⌥⇧⌘J ²

##### <small></small>

<small>¹ Ctrl+Shift+A on real OSes</small>

<small>² Ctrl+Alt+Shift+K on real OSes</small>

+++

```kotlin
@RunWith(RobolectricTestRunner::class)
class FooTest {
    @Test
    fun returns_bar() {
        val foo = Foo("hi")
        val result = foo.bar()
        assertThat(result).isEqualTo(expectedBar)
    }
}
```
---

## Writing tests the new way

> ♫ I'm always testing the sh** around me. ♪
> 
> — Korn


+++

### Spek

 - Specification framework for Kotlin
     - “Tests are specifications”
 - Created and maintained by Jetbrains
     - (in reality folks from JB)
 - Still young

+++

### A Simple case

```kotlin
class MessageQueueContract: SimpleContract({
    describe("a message queue") {
        val queue = MessageQueue()
        context("empty") {
            it("allows adding items") {
                queue.add("")
                assertThat(queue.size).isEqualTo(1)
            }
        }
    }
})
```

+++

### Definitions

 - **describe** : creates a _Group_ for a feature
 - **context** : creates a _Group_ for a context in which the feature is tested
 - **it** : creates a test for a specific part of the feature, within the parent context

+++

### `describe` and `context` can be nested

```kotlin
class MessageQueueContract: SimpleContract({
    describe("a message queue") {
        val queue = MessageQueue()
        context("empty") {
            describe("locked") {
                queue.lock()
                context("released") {
                    queue.release()
                }
            }
        }
    }
})
```

+++

### `describe` and `context` are optional

```kotlin
class FooContract: SimpleContract({
    it("just works") {
        // ..
    }
})
```

---

## Fixtures

> ♫ You can be a permanent fixture in my lyrical mixture. ♪
> 
> — Eminem

+++

### Per group

```kotlin
class FooContract: SimpleContract({
    describe("foo") {
        context("bar") {
            beforeGroup {
                // …
            }
            afterGroup {
                // …
            }
        }
    }
}
```

+++

### Per group fixtures are combined

```kotlin
class FooContract: SimpleContract({
    describe("foo") {
        beforeGroup { println("before 1") }
        afterGroup { println("after 1") }
        context("bar") {
            beforeGroup { println("before 2") }
            afterGroup { println("after 2") }
        }
        context("baz") {
            beforeGroup { println("before 3") }
            afterGroup { println("after 3") }
        }
    }
}
```

```plain
before 1
before 2
after 2
before 3
after 3
after 1
```

+++

### Per group fixtures are combined

```kotlin
class FooContract: SimpleContract({
    describe("foo") {
        beforeGroup { println("before 1") }
        beforeGroup { println("before 1 again") }
        afterGroup { println("after 1") }
        afterGroup { println("after 1 again") }
        // …
    }
}
``` 

```plain
before 1
before 1 again
…
after 1
after 1 again
```

+++

### Per test

```kotlin
class FooContract: SimpleContract({
    describe("foo") {
        beforeEachTest {
            // …
        }
        afterEachTest {
            // …
        }
    }
}
```

+++

### Per test fixtures are combined

<small>(left as an exercise for the reader)</small>

---

## Ignoring tests

> ♫ The number one question is how could you ignore it ♪
> 
> — Linkin Park

+++

```kotlin
class FooContract: SimpleContract({
    describe("foo") {
        context("bar") {
            xit ("ignored because reasons" { 
                // …
            }
        }
    }
}
```

+++

 - **xdescribe** / **xcontext** : all tests within those will be ignored
 - **xit** : ignores a single test

---

## Parameterized Testing 

> ♫ Insufficient data coming through. ♪
> 
> — Electric Light Orchestra


+++
```kotlin
class FooContract: SimpleContract({
    describe("foo") {
        val data = arrayOf(
                data("a", expected = 223),
                data("foo", expected = 1097))
        contextWithData("input %s → %d", *data) {
            input: String, expected: Int ->
            it("returns something") {
                // …
            }
        }
    }
}
```
+++

 - can still be nested within a `describe` / `context` hierarchy
 - can have `describe` / `context` as children
 - `xcontextWithData` to ignore
 - can have as much as 7 input values, and one expected output (each with their own type)



---

## Mocks

> ♫ First you mock it, rock it and then you stock it. ♪
> 
> — Beastie Boys

+++

### As input

```kotlin
class FooContract: SimpleContract({
    describe("foo") {
        context("bar") {
            val mock : Bacon = mock {
                on { getBacon() } doReturn "with eggs"
            }
            // …
        }
    }
}
```

+++

### As callback

```kotlin
class FooContract: SimpleContract({
    describe("foo") {
        context("bar") {
            val mock : Listener = mock()
            it("baz") {
                // …
                verify(mock).onEvent(any())
                verify(mock).spam = 42
            }
        }
    }
}
```

+++

### In order

```kotlin
inOrder(a,b) {
  verify(a).doSomething()
  verify(b).doSomething()
}
```


### Argument matcher

```
    verify(mock).bar(argThat { property == 42 } )
    verify(mock).bar(argForWhich { property == 42 } )
    verify(mock).bar(argWhere { property == 42 } )
    verify(mock).bar(check { 
      assertThat(it.property).isEqualTo(42)
      assertThat(it.other).hasLength(69);
    })
```

+++

### Caveats

 - Kotlin classes are final by default
 - Can only mock `open class` or `interface`
 - Meaning you should code properly !


---

## And with Robolectric ? 

>♫ Rolling out motherf***ers it's the Robots in Disguise. ♪
> 
> — Starbomb

+++

### Spek is not compatible with Robolectric

 - [JetBrains/spek#65](https://github.com/JetBrains/spek/issues/65) Robolectric integration
 - [Robolectric/robolectric#2996](https://github.com/Robolectric/robolectric/issues/2996) Integration with other test frameworks
 - [JetBrains/spek#115](https://github.com/JetBrains/spek/issues/115) Spek Extensions

+++

# But …

<small>Because i love big buts</small>

+++

```kotlin
class FooContract: RoboContract({
    // …
}
```

<small>ⓘ Just a DSL to mimick Spek within Robolectric</small>

---

## Thanks for your attention

#### Any Question ?

---

## Appendix

#### Setting up Gradle

> ♫ All I need you've already done. ♪
> 
> — Natalie Grant

+++

### App

```gradle
dependencies {
    testCompile libraries.kotlin_tests
    testCompile libraries.core_tests
}
```

+++

### Core library

```gradle
dependencies {
    testCompile project(':test-commons')
    testCompile libraries.kotlin_tests
}
```
