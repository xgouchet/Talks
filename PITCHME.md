
# Zen Code Reviews

#### The way towards painless code reviews

_Droidcon Berlin 2017_ 

---


## About… Xavier F. Gouchet 

<h4 class="fragment">Android Architect at <img src="logos/deezer.png" class="logo-inline"/></h4>
#### ‘Mr Tools’ / CI Admin / UT Advocate<!-- .element: class="fragment" -->

###### <span class="fragment"><a>@xgouchet</a> on <i class="fa fa-github" aria-hidden="true"></i>, <i class="fa fa-stack-overflow" aria-hidden="true"></i>, <i class="fa fa-linkedin" aria-hidden="true"></i>, <i class="fa fa-twitter" aria-hidden="true"></i>, …</span>

---

> ♫ Put your hands in the air ♪
> 
> — Placebo

### Who uses code review here ? 

+++

### Code reviews @ Deezer

 - 18 Android developers
 - 3 main repositories
 - Varied experiences and skills

---

## Why ? 

#### The purposes of code reviews

+++

### Find defects early

 - Logic fallacies <!-- .element: class="fragment" -->
 - Typos, spelling <!-- .element: class="fragment" -->
 - Edge cases <!-- .element: class="fragment" -->
 - Potential technical debt  <!-- .element: class="fragment" -->

+++

### Harmonize the code base

 - Code style <!-- .element: class="fragment" -->
 - Naming conventions <!-- .element: class="fragment" -->
 - Architecture <!-- .element: class="fragment" -->
 - Libraries <!-- .element: class="fragment" -->

+++

### Generate discussion around…

 - Choices  <!-- .element: class="fragment" -->
     - Algorithm  <!-- .element: class="fragment" -->
     - Data Structure  <!-- .element: class="fragment" -->
     - Architecture <!-- .element: class="fragment" -->
     - Libraries <!-- .element: class="fragment" -->
 - Features <!-- .element: class="fragment" -->
 - Best practices <!-- .element: class="fragment" -->

+++

### Team Building

 - Cohesion <!-- .element: class="fragment" -->
 - Trust <!-- .element: class="fragment" -->
 - Lower “Linkedin factor” <!-- .element: class="fragment" -->
 - Asynchronous Pair Programming <!-- .element: class="fragment" -->

+++

### Share knowledge

 - Onboard junior / new developers <!-- .element: class="fragment" -->
 - Everyone has something to teach <!-- .element: class="fragment" -->
 - Everyone has something to learn <!-- .element: class="fragment" -->

+++

### Downsides of code review

 - More time spent per ticket / less time spent delivering feature <!-- .element: class="fragment" -->
 - Senior developer frustration <!-- .element: class="fragment" -->

---

## What ?

#### The different types of code reviews

+++

### “Automatic” code review

 - Static Analysis  <!-- .element: class="fragment" -->
     - Android Lints <!-- .element: class="fragment" -->
     - Findbugs, Checkstyle, PMD <!-- .element: class="fragment" -->
     - Detekt, ktlint <!-- .element: class="fragment" -->
 - Tests (Unit, Integrated, Functionnal) <!-- .element: class="fragment" -->

+++

### Pre-commit

 - Pro <!-- .element: class="fragment" -->
     - Quality ensured before merge <!-- .element: class="fragment" -->
     - All code must be reviewed <!-- .element: class="fragment" -->
 - Cons <!-- .element: class="fragment" -->
     - Productivity impact <!-- .element: class="fragment" -->
     - Back & forth Hell ™ <!-- .element: class="fragment" -->

+++

### Post-commit

 - Pro <!-- .element: class="fragment" -->
     - Continuous development <!-- .element: class="fragment" -->
     - Limit git conflicts <!-- .element: class="fragment" -->
 - Cons <!-- .element: class="fragment" -->
     - Bug can ship to production <!-- .element: class="fragment" -->
     - Resolution can become non trivial afterwards <!-- .element: class="fragment" -->

+++

### Optional code reviews

 - by commit author <!-- .element: class="fragment" -->
 - by commit length <!-- .element: class="fragment" -->
 - by files modified <!-- .element: class="fragment" -->
 - random checks <!-- .element: class="fragment" -->
 - … ? <!-- .element: class="fragment" -->

+++

### Pair review with another developer

 - Provide a single feedack <!-- .element: class="fragment" -->
 - Compare different viewpoints <!-- .element: class="fragment" -->
 - Tone down negative feedbacks <!-- .element: class="fragment" -->

+++

### Code Review Meeting with the author

 - 3 to 7 attendees <!-- .element: class="fragment" -->
 - Only for non trivial reviews <!-- .element: class="fragment" -->
 - Mentor the author <!-- .element: class="fragment" -->
 - Get in depth view <!-- .element: class="fragment" -->
 - Discuss alternatives <!-- .element: class="fragment" -->
 - Immediate feedback <!-- .element: class="fragment" -->

---

## How ?

#### The <em>Do</em>s and <em>Dont</em>s of code review

+++

### Writing reviewable code

 - Keep the commits short <!-- .element: class="fragment" -->
     - `git add --patch` / `git add -p`
 - Comment the code <!-- .element: class="fragment" -->
 - Use a proper commit message <!-- .element: class="fragment" -->
     - CR Brief for non trivial commits <!-- .element: class="fragment" -->
 - Link to the ticket <!-- .element: class="fragment" -->

+++

### Before submitting, review your own code

 - Find easy to spot issues <!-- .element: class="fragment" -->
     - Typos <!-- .element: class="fragment" -->
     - Commented code <!-- .element: class="fragment" -->
     - Duplicates / possible refactoring <!-- .element: class="fragment" -->
     - Copy / Paste errors <!-- .element: class="fragment" -->
 - Take a step back on your code <!-- .element: class="fragment" -->


+++

### Commenting on issues

> “If you can't understand that, then yes, you're crazy. Or just terminally stupid.”
> 
> — Linus

+++

### Be precise : what is the problem ?

##### “This code is bad !” <span style="color:#c0392b;font-size:150%;">✗</span>

##### “This line could cause a memory leak…” <span style="color:#16a085;font-size:150%;">✔</span>

+++

### Argument : why is it a problem ?

##### “Obviously!”  <span style="color:#c0392b;font-size:150%;">✗</span>

##### “… because the activity reference is retained…” <span style="color:#16a085;font-size:150%;">✔</span>

+++

### Be helpful : how to fix the problem ?

##### “Deal with it!”  <span style="color:#c0392b;font-size:150%;">✗</span>

##### “… you could instead use a WeakReference.” <span style="color:#16a085;font-size:150%;">✔</span>

+++

### Define criticity : How important is the issue ?

##### “…”  <span style="color:#c0392b;font-size:150%;">✗</span>

##### “It’s not critical, but must be fixed in a later commit before the release candidate next week.” <span style="color:#16a085;font-size:150%;">✔</span>

+++

### Examples

 - “The name of this variable is ambiguous. You could rename it as …” <!-- .element: class="fragment" -->
 - “I don’t think this method should be in this class because it’s outside of the class’s responsibility.” <!-- .element: class="fragment" -->
 - “This rule has many edge cases, you should add more unit tests.” <!-- .element: class="fragment" -->

+++

### Voting down

 - Avoid blocking commits unnecessarily <!-- .element: class="fragment" -->
 - Always make the reasons clear <!-- .element: class="fragment" -->
 - Make a full review <!-- .element: class="fragment" -->
 - If an issue has already been raised, don't comment just to say “+1” <!-- .element: class="fragment" -->

+++

### Receiving critique

 - Take a step back <!-- .element: class="fragment" -->
 - Stay humble <!-- .element: class="fragment" -->
 - Motivate your choices <!-- .element: class="fragment" -->
 - Accept the critique <!-- .element: class="fragment" -->
     - (even if it means more work for you) <!-- .element: class="fragment" -->

+++

### Overall behavior

 - Stay open minded <!-- .element: class="fragment" -->
 - Make it about the code, not the people <!-- .element: class="fragment" -->
 - Don't start the flame war <!-- .element: class="fragment" -->
 - Share your knowledge <!-- .element: class="fragment" -->
 - Give as much as you receive <!-- .element: class="fragment" -->

+++

### Going further ?

#### [codereview.stackexchange.com](https://codereview.stackexchange.com)

---

## Thanks for your attention

### Any Question ? 




