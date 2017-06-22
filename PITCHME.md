
# Legacy code

#### How to deal with code you didn't write

_Wild Code School_ 

---

![Deezer](assets/md/logos/deezer.png) <!-- .element: class="logo white" -->

## About…  Xavier F. Gouchet 

#### Android Architect <!-- .element: class="fragment" -->
#### ‘Mr Tools’ / CI / UT <!-- .element: class="fragment" -->
#### Fluent in Android since Cupcake <!-- .element: class="fragment" -->

###### <span class="fragment"><a>@xgouchet</a> on <i class="fa fa-github" aria-hidden="true"></i>, <i class="fa fa-stack-overflow" aria-hidden="true"></i>, <i class="fa fa-linkedin" aria-hidden="true"></i>, <i class="fa fa-twitter" aria-hidden="true"></i>, …</span>

+++

### And before that … ?

![Orleans](assets/md/logos/orleans.jpg) <!-- .element: class="fragment logo white" -->
![Paris8](assets/md/logos/paris8.jpg) <!-- .element: class="fragment logo white" -->
![Dassault](assets/md/logos/dassault.png) <!-- .element: class="fragment logo white" -->
![Isart](assets/md/logos/isart.png) <!-- .element: class="fragment logo white" -->

---

## What is legacy code ? 

> ♫ It's a chronicling of our rise… ♪
> 
> — Tenacious D

+++

### What is legacy code ?

 - Code including anti-patterns<!-- .element: class="fragment" -->
 - Code with (almost) no tests<!-- .element: class="fragment" -->
 - Code written hastily (#deadlines)<!-- .element: class="fragment" -->
 - Temporary code (#quickfix)<!-- .element: class="fragment" -->
 - Code written by someone else<!-- .element: class="fragment" -->
 - Code written before now<!-- .element: class="fragment" -->

#### in one word : Code ! <!-- .element: class="fragment" -->

+++

### Why is it bad ? 

 - Poor performances <!-- .element: class="fragment" -->
 - Buggy <!-- .element: class="fragment" -->
 - Hard to read <!-- .element: class="fragment" -->
 - Hard to understand <!-- .element: class="fragment" -->
 - Hard to maintain <!-- .element: class="fragment" -->

+++

### Why is it still there ? 

 - Too long to change <!-- .element: class="fragment" -->
 - Too hard to change <!-- .element: class="fragment" -->
 - No one knows how it works <!-- .element: class="fragment" -->
 - Why fix it if it ain't broken <!-- .element: class="fragment" -->

---

### My personal experience with

## Legacy Code

+++

```bash
    commit 1e7dfd3e0c6715f3e611975892d8618afb7c33a6
    Author: _alex <_alex@...>
    Date:   Tue Jan 6 14:56:57 2009 +0000
    
        Created folder
```

+++

 - 8 years <!-- .element: class="fragment" -->
 - 12’000+  commits <!-- .element: class="fragment" -->
 - 30+  different committers <!-- .element: class="fragment" -->
 - 750’000+  lines of code* <!-- .element: class="fragment" -->
 - 200’000+  lines of comments* <!-- .element: class="fragment" -->
 - 7’500+  source files* <!-- .element: class="fragment" -->

<small class="fragment">* As of June 2017</small>

+++

#### We had 8 big refactoring in the past 4 years. 

### Let’s look at 3 “post-mortem”

---

## 1 : The ugly

> “The only valid measurement of code quality : WTFs / Minute.”
> 
> — Thom Holwerda

+++

![No code reviews](assets/md/img/1_1_no_code_review.png)<!-- .element: class="photo" -->

### No code reviews

+++

![No vision ahead](assets/md/img/1_2_no_vision_ahead.jpg)<!-- .element: class="photo" -->

### No vision ahead

+++

![Lasagna architecture](assets/md/img/1_3_lasagna.jpg)<!-- .element: class="photo" -->

### Lasagna architecture

+++

![Bad thread strategy](assets/md/img/1_6_java_threads.png)<!-- .element: class="photo" -->

### Bad thread strategy

+++

![Ugly duplicates](assets/md/img/1_4_bogdanovs.jpg)<!-- .element: class="photo" -->

### Many (ugly) duplicates

+++

![No unit tests](assets/md/img/1_5_no_tests.png)<!-- .element: class="photo" -->

### No unit tests

---

## 2 : The bad

> “Programming is like sex. One mistake and you have to support it for the rest of your life.”
> 
> — Michael Sinz

+++

![From scratch](assets/md/img/2_1_from_scratch.png)<!-- .element: class="photo" -->

### From scratch

+++

![No memory](assets/md/img/2_2_no_memory.gif)<!-- .element: class="photo" -->

### No idea what the previous system did

+++

![Architecture](assets/md/img/2_3_architecture.png)<!-- .element: class="photo" -->

### Architecture beforehand

+++

![No code review](assets/md/img/2_4_no_code_review.png)<!-- .element: class="photo" -->

### Still no code review

+++

![Tests… Kinda…](assets/md/img/2_5_tests_kinda.png)<!-- .element: class="photo" -->

### Tests… Kinda…

+++

![Tests not updated](assets/md/img/2_6_tests_not_updated.png)<!-- .element: class="photo" -->

### Tests were not updated

+++

![Urgency → mistaks](assets/md/img/2_7_urgency.png)<!-- .element: class="photo" -->

### Urgency → mistakes 
#### _#deadline_<!-- .element: class="fragment" -->

---

## 3 : The good

> “When debugging: novices insert corrective code; experts remove defective code.”
> 
> — Richard Pattis

+++

![Existing code assessed](assets/md/img/3_1_assessment.png)<!-- .element: class="photo" -->

### Existing code assessed

+++

![Plan ahead](assets/md/img/3_2_battle_plan.png)<!-- .element: class="photo" -->

### We had a plan

+++

![Plan ahead](assets/md/img/3_3_roadmap.png)<!-- .element: class="photo" -->

### We had a plan

+++

![Prepare the fork](assets/md/img/3_4_fork.png)<!-- .element: class="photo" -->

### We prepared the refactoring

+++

![Unit test](assets/md/img/3_5_unit_tests.png)<!-- .element: class="photo" -->

### Each step was (unit) tested

+++

![No deadline](assets/md/img/3_6_no_deadline.png)<!-- .element: class="photo" -->

### No deadline

+++

![Progressive release](assets/md/img/3_7_gatekeep.png)<!-- .element: class="photo" -->

### Progressive release (beta, gatekeep)

---

## Dealing with legacy code

> “There are two ways to refactor legacy code;
> Only the third one works.”
>
> — Alan J. Perlis

+++

### Don't judge; Understand

 - Why is the code written that way ?<!-- .element: class="fragment" -->
    - (old) constraints<!-- .element: class="fragment" -->
    - rushed code<!-- .element: class="fragment" -->
    - bad specs<!-- .element: class="fragment" -->
 - What can be done about it ?<!-- .element: class="fragment" -->

+++

### Trivial changes first

 - Renaming <!-- .element: class="fragment" -->
 - Moving <!-- .element: class="fragment" -->
 - Splitting <!-- .element: class="fragment" -->

+++

### Plan ahead

 - What needs to be done ? <!-- .element: class="fragment" -->
 - In what order ? <!-- .element: class="fragment" -->

+++

### Resist the urge to rewrite everything

+++

### Test first, refactor later

---

## The refactoring algorithm

> ♫ There must be a better way 
> 
> to make the things we want… ♪
> 
> — Paul Mc Cartney

+++


![Know your enemy](assets/md/img/4_1_know_your_enemy.png)<!-- .element: class="photo" -->

### “Know your enemy

#### Identify change points

+++


#### Find test points

+++

![Cut ties](assets/md/img/4_3_cut_ties.jpg)<!-- .element: class="photo" -->

### “Cut ties”

#### Break dependencies

+++

![Protect yourself](assets/md/img/4_4_protect_yourself.png)<!-- .element: class="photo" -->

### “Protect yourself”

### Write tests

+++

### Refactor


---

## Refactoring gone wrong

> ♫ So let this serve as a reminder
> 
> A warning sign ♪
> 
> — Disturbed

---

## Legacy Code is not inevitable

+++

### Follow best practices

 - Standard conventions
 - 

+++

### Reuse exisiting code

+++

### SOLID / DRY / KISS

+++ 

### Document everything

 - Document the feature specs
 - Document the bug fixes and special cases
 - `// TODO Leave instructions for future self`

---

## Thanks for your attention

#### Any Question ? 