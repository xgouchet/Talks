
# Unit Tests

_Workwell_

---

## About… Xavier F. Gouchet

#### Lead Android Engineer at WorkWell 

#### Fluent in Android since Cupcake


###### <a>@xgouchet</a> on <i class="fa fa-github" aria-hidden="true"></i>, <i class="fa fa-stack-overflow" aria-hidden="true"></i>, <i class="fa fa-linkedin" aria-hidden="true"></i>, <i class="fa fa-twitter" aria-hidden="true"></i>, …

+++?image=assets/Slides_WW_EN.png&size=cover

---

## Back to the basics

+++

### The different kinds of tests


+++?image=assets/unit.jpg&size=cover

> Unit tests

+++?image=assets/integration.jpg&size=cover

> Integration tests

+++?image=assets/functional.jpg&size=cover

> Functional tests

+++?image=assets/tdd.jpg&size=cover

> TDD

+++?image=assets/codecoverage.jpg&size=cover

> Code Coverage

---

### Why unit tests

 - Prevent regression <!-- .element: class="fragment" -->
 - Create an explicit self-updating contract <!-- .element: class="fragment" -->
 - Shape the code <!-- .element: class="fragment" -->
 - Ease maintenance <!-- .element: class="fragment" -->
 - Increase our trust in the code <!-- .element: class="fragment" -->

+++

### Why unit tests

#### Use the code !

---

### What to unit test

 - Decision logic (if, switch, …) <!-- .element: class="fragment" -->
 - Input → Output <!-- .element: class="fragment" -->
 - De-Serialization (parcelable, json, …) <!-- .element: class="fragment" -->
 - Callbacks, events <!-- .element: class="fragment" -->
 - Code that will be changed often <!-- .element: class="fragment" -->
 - Code that will be changed by other devs <!-- .element: class="fragment" -->

+++

### What to unit test

 - All cases that come to mind : <!-- .element: class="fragment" -->
    - Ideal case (good inputs / states) <!-- .element: class="fragment" -->
    - Bad case (Empty string / array / list, null, …) <!-- .element: class="fragment" -->
    - Edge cases (non alpha characters, negative numbers, …) <!-- .element: class="fragment" -->

+++

### What not to unit test

 - 3rd party Libraries <!-- .element: class="fragment" -->
 - Framework (Android, Angular, …) <!-- .element: class="fragment" -->
 - Network / API <!-- .element: class="fragment" -->
 - Language (Javascript, Swift, Kotlin, …) <!-- .element: class="fragment" -->
 - Trivial code (getters, setters, …) <!-- .element: class="fragment" -->

---

### How to write unit tests

 - What (unit) feature am I testing ? <!-- .element: class="fragment" -->
 - What is the feature supposed to do ? <!-- .element: class="fragment" -->
 - Given an input / state, what’s the expected output / state ? <!-- .element: class="fragment" -->
 - Can the test be reproduced <!-- .element: class="fragment" -->

+++

### How to write unit tests first

 1. Write the minimal failing test <!-- .element: class="fragment" -->
 2. Check that the test fails ✗ <!-- .element: class="fragment" -->
 3. Write a minimal implementation  <!-- .element: class="fragment" -->
 4. Check that the test passes ✓ <!-- .element: class="fragment" -->
 5. Refactor, Enhance, Comment <!-- .element: class="fragment" -->
 6. GOTO 1 <!-- .element: class="fragment" -->

+++

### How to write unit tests (details)

```kotlin
class FeatureTest {

  // …

  @Test
  fun doesSomething() {
    val fakeValue = 42
    val expectedResult = "foo"

    val result = objectUnderTest.doSomething(fakeValue)

    assertEquals(result, expectedResult);
  }
}
```

@[1]
@[5-6]
@[7-8]
@[10]
@[12]

+++

### How to write unit tests (details)

 - Fake Data <!-- .element: class="fragment" -->
 - Mocks / Stubs <!-- .element: class="fragment" -->


---

## Thanks for your attention

#### Any Question ? 
