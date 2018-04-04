
# Did your mocks read the Terms of Service ?

#### Contracts for your mocks and fakes

_CodeMobile UK 2018_ 

---


## About… Xavier F. Gouchet

#### Lead Android Engineer at WorkWell 

#### Fluent in Android since Cupcake


###### <a>@xgouchet</a> on <i class="fa fa-github" aria-hidden="true"></i>, <i class="fa fa-stack-overflow" aria-hidden="true"></i>, <i class="fa fa-linkedin" aria-hidden="true"></i>, <i class="fa fa-twitter" aria-hidden="true"></i>, …

+++?image=assets/Slides_WW_EN.png&size=cover

---

> Previously, in CodeMobileUk 2017 …

+++?image=assets/previously_2.png&size=contain

+++?image=assets/previously_1.png&size=contain

+++

### Objective 

##### Making sure the tools we use enhance our tests

> You must be as confident in the test you code as you are in the code you test.


---

### Put your hands in the air

 - Unit tests ? <!-- .element: class="fragment" -->
 - Mocks <!-- .element: class="fragment" -->
    - Mockito / KotlinMockito? 
    - Easymock ? <!-- .element: class="fragment" -->
    - JMockit ? <!-- .element: class="fragment" -->
    - Mockk ? <!-- .element: class="fragment" -->


---

## What are we talking about here

#### Mocks ? Stubs ? Fakes ? Dummies ? 

+++

#### Fakes (aka Dummies)

<small>Dumb POJO / Data Class, actual value is not relevant</small>


```kotlin
  @Test(expected = IndexOutOfBoundsException::class)
  fun testThrowsException() {
    val dummyUser = User(name = "Bob", id = 42)
    testedList.put(-666, dummy)
  }
```

+++

#### Stubs / Mocks

<small>Objects with scripted answers</small>

```kotlin
  @Test(expected = IllegalArgumentException::class)
  fun testReturnsNull() {
    whenever(mockProvider.getData()) doReturn null
    testedObject.addDataFrom(mockProvider)
  }
```

+++

#### Spies

<small>Can be mock or real objects, just tracking each call</small>

```kotlin
  @Test fun testCallsListener() {
    val spiedListener = spy(realListener)

    testedObject.addListener(spiedListener)
    testedObject.doSomething()

    verify(spiedListener).somethingDone()
  }
```

---

## Fakes

#### What's the problem with fakes

+++

#### All my tests involved users named Alice and Bob. 

#### Aged 42. <!-- .element: class="fragment" -->

#### Working at FooBar Inc. <!-- .element: class="fragment" -->


+++

#### When all your fake data are `“foo”` and `42`,
####  how can you be sure that your tests are valid ?

<ul>
 <li class="fragment">Where does the `42` come from ?</li>
 <li class="fragment">Lots of hardcoded values !</li>
 <li class="fragment">Only one value is tested. Ever.</li>
</ul>

+++

### Solution ? 

#### Use random data… <!-- .element: class="fragment" -->

+++

```kotlin
  @Test fun invalidateDataAfterTimeout() {
    testedObject.setLastCallTimestamp(0)
    testedObject.setDataTTL(42)

    long ts = 666
    boolean result = testedObject.isDataValid(ts)

    assertFalse(result)
  }
```

+++

```kotlin
  @Test fun invalidateDataAfterTimeout() {
    val fakeTS = rand.nextLong()
    val fakeTTL = rand.nextLong()
    val fakeDelay = rand.nextLong()

    testedObject.setLastCallTimestamp(fakeTS)
    testedObject.setDataTTL(fakeTTL)

    val ts = fakeTS + fakeTTL + fakeDelay
    val result = testedObject.isDataValid(ts)

    assertFalse(result)
  }
```

+++

### … but not _too_ random

#### (Long overflow, negative TTL, …)

+++

#### Introducing [Elmyr <i class="fa fa-github" aria-hidden="true"></i>](https://github.com/xgouchet/Elmyr/) 

```kotlin
class FooTest {
  @JvmField @Rule val forger = new JUnitForger()

  // …
}
```

+++

#### Elmyr features : forging numbers

```kotlin
// works with ints longs, floats and doubles

forger.anInt(min = 0, max =100)
forger.aPositiveLong()
forger.aGaussianFloat(mean = 42.0f, standardDeviation = 100.0f)
forger.aDoubleArray(DoubleConstraint.NEGATIVE_STRICT)
```

+++

#### Elmyr features : forging strings

```kotlin
forger.anHexadecimalString()
forger.aWord()
forger.aSentence()

forger.anEmail()
forger.aUrl()

forger.aStringArray(StringConstraint.WORD)
forger.aStringMatching("(0|+44)\\d{10}")
```

+++

#### Elmyr features : forging from collections, enum

```kotlin
forger.anElementFrom(myCollection)
forger.anElementFrom(value1, value2, value3, …)

forger.aValueFrom(MyEnum::class)

forger.aNullableFrom(nonNullValue)
```

+++

#### Elmyr features : failing tests

```ini
‘testSomething’ failed with fake seed = 0x4815162342
```

```kotlin
  @Before fun forceSeed() {
    forger.reset(4815162342L)
  }
```

+++

```kotlin
  @Test fun invalidateDataAfterTimeout(){
    val fakeTS = forger.aTimestamp()
    val fakeTTL = forger.aLong(1, 86400000)
    val fakeDelay = forger.aLong(1, 86400000)

    testedObject.setLastCallTimestamp(fakeTS)
    testedObject.setDataTTL(fakeTTL)

    val ts = fakeTS + fakeTTL + fakeDelay
    val result = testedObject.isDataValid(ts)

    assertFalse(result)
}
```

---

## Dealing with Mocks

#### What's the problem with mocks

+++

### Foreword

> “There are two types of mocks:
> inputs and outputs”

+++

#### Input

```kotlin
  @Test fun testSomething() {
    val fakeData = forger.anInt()
    val inputMock = mock()
    whenever (inputMock.getData()) doReturn fakeData

    // Call to getData is not verified directly
  }
```

+++

#### Output

```kotlin
  @Test fun testSomething() {
    val outputMock = mock()
    // mock is not stubbed

    verify(outputMock).onSomethingDone()
  }
```

+++

### The problem:

#### Mocks are designed to make the tests pass

+++

### Are your mocks consistent…
#### … between two test methods ? <!-- .element: class="fragment" -->

+++

```kotlin
  @Test fun testFoo() {
    whenever(mockQueue.isEmpty()) doReturn(true)
    whenever(mockQueue.getFirst() doThrow(new Exception())
    // …
  }

  @Test fun testBar() {
    whenever(mockQueue.isEmpty()) doReturn(true)
    whenever(mockQueue.getFirst() doReturn(null)
    // …
  }
```

+++

### Solution ? 

#### Prepare all the mocks in the setup method… <!-- .element: class="fragment" -->

 - Mocks have single configuration <!-- .element: class="fragment" -->
 - All stubbing is done in one place <!-- .element: class="fragment" -->

+++

### Are your mocks consistent…
#### … between two test classes ? <!-- .element: class="fragment" -->

+++

```kotlin
class FooTest {
  @Before fun setupMock() {
    whenever(mockQueue.isEmpty()) doReturn(true)
    whenever(mockQueue.getFirst() doThrow(new Exception())
  }
}

class FizTest {
  @Before fun setupMock() {
    whenever(mockQueue.isEmpty()) doReturn(true)
    whenever(mockQueue.getFirst() doReturn(null)
    // …
  }
}
```

+++

### Solution ? 

#### Use a separate class to setup the mocks <!-- .element: class="fragment" -->

##### _Introducing Contract based mocking_ <!-- .element: class="fragment" -->

+++

#### Defining the contract

```kotlin
class QueueContract {
  val mockedQueue : Queue = mock()

  fun prepareEmpty() {
    whenever(mockedQueue.isEmpty()).thenReturn(true)
    whenever(mockedQueue.getFirst().thenThrow(new Exception())
  }
}
```

+++

#### Using the contract

```kotlin
class FooTest {
  lateinit var queueContract : QueueContract

  @Before fun setUpQueue() {
    queueContract = new QueueContract()
  }

  @Test fun testWithEmptyQueue() {
    queueContract.prepareEmpty()
    val mock = queueContract.mockedQueue
    // …
  }
}

```

+++

### Are your mocks consistent…
#### … with the concrete implementations ? <!-- .element: class="fragment" -->

 - Fuzzy specs <!-- .element: class="fragment" -->
 - 3rd party implementation <!-- .element: class="fragment" -->
 - Undocumented behavior <!-- .element: class="fragment" -->

+++

### Solution ?

#### Use the contract as test definition <!-- .element: class="fragment" -->

+++

#### Introducing [Mesmaeker <i class="fa fa-github" aria-hidden="true"></i>](https://github.com/xgouchet/Mesmaeker/)

_(Still in αlphα)_

+++

#### Defining the contract

```kotlin
open class QueueContract 
  : MockitoContract<Queue>(Queue::class.java) {

  @Clause
  fun prepareEmpty() {
    whenever { it.isEmpty() }.thenReturn(true)
    whenever { it.getFirst() }.thenThrow(new Exception())
  }
}
```

+++

#### Using the contract

```kotlin
class FooTest {

  @Rule public BaseContractRule contracts = new BaseContractRule();
  @Contract lateinit var queueContract: QueueContract

  @Test fun testWithEmptyQueue() {
    queueContract.prepareEmpty()
    val mock = queueContract.getMock()
    // …
  }
}

```

+++

#### Testing the contract

```kotlin
class BarTest (clause : String)
  : ContractValidator<Queue, QueueContract> (clause) {

  override fun instantiateContract()
    : QueueContract = QueueContract()
  override fun instantiateSubject()
    : Queue = Queue()

  companion object {
    @JvmStatic @Parameterized.Parameters()
    fun data(): Collection<Array<Any?>> {
      return generateTestParameters(QueueContract::class.java)
    }
  }
}
```

+++

#### Writing the Clauses of the Contract

```kotlin
  @Clause
  fun prepareWithSize(size: Int) {
    applyIfImplementation { it.resize(size) }

    whenever { it.size() }.thenReturn(size)
    whenever { it.get(-1) }.thenThrow(IooBException())
    whenever { it.get(size) }.thenThrow(IooBException())
  }
```

+++

#### Detail's in the fine print

```kotlin
override fun getClauseParams(clause: String): Array<Any?>? {
  when (contractClause) {
    "prepareWithSize" -> return arrayOf(forger.aSmallInt())
    else -> return emptyArray()
  }
}
```

---

## Conclusion

 - Remember, tests can have bugs and code smells too <!-- .element: class="fragment" -->
 - Try to think of what could go wrong <!-- .element: class="fragment" -->
 - Look for the edge cases <!-- .element: class="fragment" -->

+++

> “You need to be as confident in the code you test as you are in the test you code ”

---

## Thanks for your attention

### Any Question ? 

#### <i class="fa fa-github" aria-hidden="true"></i>

[https://github.com/xgouchet/Elmyr](https://github.com/xgouchet/Elmyr)

[https://github.com/xgouchet/Mesmaeker](https://github.com/xgouchet/Mesmaeker)
 _(αlphα)_

