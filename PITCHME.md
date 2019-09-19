
## Team Work, Code Quality & Ethics

##### _Wild Code School_ 

---

## About… Xavier F. Gouchet 

<h4>Lead Android Software Engineer at Workwell</h4>

###### <span><a>@xgouchet</a> on <i class="fa fa-github" aria-hidden="true"></i>, <i class="fa fa-stack-overflow" aria-hidden="true"></i>, <i class="fa fa-linkedin" aria-hidden="true"></i>, <i class="fa fa-twitter" aria-hidden="true"></i>, …</span>

+++

### What we do at Workwell

@img[large photo](img/workwell.jpg)

+++

### And before that ? 

#### 2001, my first line of code…

```java
public class Main{

    public static void main(String[] args) {

        System.out.println("Hello World");

    }

}
```

+++

### … and much more

@img[tiny ghost](logos/dassault_systemes.png)
@img[tiny ghost](logos/isart_digital.png)

@img[tiny ghost](logos/oodrive.png)
@img[tiny ghost](logos/deezer.png)

---

## Team Work

@img[large photo](img/teamwork.jpg)

+++

### Find the best solution on a problem

 - Generate discussions
     - on the problem
     - on the context
     - on the possible solutions
 - Tackle the complexity by having two minds holding the big picture 

+++

### Improve the code quality

 - Avoid easy mistakes
 - More probability to find edge cases
 - Makes sure that urgent ≠ botched

+++

### Cost of fixing bugs

@img[large photo](img/cost_bugs.jpg)

+++

### Generate discussion around…

 - Choices  
     - Algorithm / Data Structure  
     - Architecture 
     - Libraries 
 - Features 
 - Best practices 

+++

### Team Building

 - Cohesion 
 - Trust 
 - Lower “Linkedin factor” 

+++

### Share knowledge

 - Onboard junior / new developers 
 - Get a tour of changes after a break 
 - Combine different skills / expertise 

---

## Team Work: Pair Programming

@img[large photo](img/pair_programming.png)

+++

### The forms of “pair” programming

 - Driver / Navigator
 - Projector Programming
 - Buddy Programming

+++

### Downsides of Pair Programming

 - More time spent per ticket / less time spent delivering feature 
 - More intense than working alone 
 - Human conflicts 

+++

### When ?

 - Complex programming tasks
 - Urgent long tasks*
 - Training / Knowledge sharing

+++

### The <em>Do</em>s and <em>Dont</em>s

 - No silent driver
 - Pair Carefully
     - Avoid large disparity
     - Avoid affinity issues  
 - Switch often
 - Take breaks: Relax, Clear your mind, Take a step back
    
---

## Team Work: Code Reviews

@img[large photo](img/code_review.png)

+++

### The forms of Code Review

 - Remote 
 - Pair Review
 - Review Meeting

+++

### Pre-commit

 - Pro 
     - Quality ensured before merge 
     - All code must be reviewed  
 - Cons 
     - Productivity impact 
     - Back & forth Hell ™ 
 
+++

### Post-commit

 - Pro 
     - Continuous development 
     - Limit git conflicts 
 - Cons 
     - Bug can ship to production 
     - Resolution can become non trivial afterwards 

+++

### Optional code reviews

 - by commit author 
 - by commit length 
 - by files modified 
 - random checks 
 - … ? 

+++

### Let the right people do the review

 - Anyone with access to GitHub / … 
 - Team lead 
 - Modified files watchers 

+++

### The <em>Do</em>s and <em>Dont</em>s

 - Writing reviewable code
     - Keep the commits short :  
`git add --patch` / `git add -p`
     - Comment the code
     - Use a proper commit message
     - Individual commits don't need to compile, the PR does
 - Before submitting, review your own code

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

 - “The name of this variable is ambiguous. You could rename it as …” 
 - “I don’t think this method should be in this class because it’s outside of the class’s responsibility.” 
 - “This rule has many edge cases, you should add more unit tests.” 

+++

### Voting down

 - Avoid blocking commits unnecessarily 
 - Always make the reasons clear 
 - Make a full review 
 - If an issue has already been raised, don't comment just to say “+1” 

+++

### Receiving critique

 - Take a step back 
 - Stay humble 
 - Motivate your choices 
 - Accept the critique 
     - (even if it means more work for you) 

+++

### Going Further

[codereview.stackexchange.com](https://codereview.stackexchange.com)

---

## Code Quality: Tests

@img[large photo](img/dummy.jpg)

+++

### What are the goals of tests ?

 - Verify that the code works
 - Make the contract explicit
 - Guide the development (TDD)
 - Prevent regressions
 - Ensure retrocompatibility & ease maintenance
 - Increase our confidence in the code

+++

> “Your code is meant to be executed. Testing is the best way to make sure it actually is executed.”

+++

### The forms of tests

 - Unit tests
 - Integration tests 
 - Functionnal tests (aka end to end tests)
 - Test Driven Development

+++

### Reasons not to write tests

 - I don't need tests (“Testing is Doubting”)
 - I don't have time
 - I don't know how to write tests

+++

### What not to test ?

 - 3ʳᵈ party libraries (npm modules, …)
 - Framework (Vue, Angular, …)
 - Network / API
 - Language (JS, Typescript, toolchain, …)
 - Trivial code (getter/setters, …)

+++

### What to test ?

 - Decision logic (if, switch, when, …)
 - Input → Output
 - (De)serialization / transformation (manual only)
 - Callbacks events
 - Critical code

+++

### How to write Tests

 - Isolate the Unit
 - Write down the Unit’s purpose
 - Write down known (and unknown) use cases

+++

### Test golden rules

- fast to execute
- reproducible
- reliable


+++

### The TDD recipe

@img[large ghost](img/tdd_loop.png)

+++

### Going further

 - Read the best practice for your language / framework
 - Explore other patterns
     - BDD
     - Mutation testing
     - Fuzzy testing

---

## Code Quality: Static Analysis

@img[large photo](img/analysis.jpg)

+++

### The forms of static analysis (aka lint)

 - Style conventions
 - Bad practices
 - Programming errors
 - Potential bugs

---

## Ethics in programming

@img[large photo](img/chidi.jpg)

+++

### Definitions

 - Legal / Illegal / Unlawful

> Ethics and morality are subjective. 
> For the first time, the answer is not `true` or `false`

+++

### Why talk about ethics ?

> In this world, with great power there must also come…  
> great responsibility!
> 
> Stan Lee

+++

### Don't code the features blindly

> What would your users say if they were listening to your meeting? Would you make the same choice? 

+++

### To ship or not to ship

> Should we ship a Minimum Viable Product ? Should we fix every single bug ? 

+++

### Take ownership of the codebase

> If you see an issue in someone else’s code, it becomes your responsibility too.

+++

### Anticipate Misuse

> Deep Learning is a armless technology, right ?

+++

### Going Further

 - `The Programmer's Oath` (Bob Martin)
 - `The IEEE & ACM manifesto`
 - [Dark Patterns](https://darkpatterns.org/)

---

## The proper mindset

@img[large photo](img/brain.jpg)

+++

### The proper mindset… Team work

 - Stay open minded 
 - Accept imperfection
 - Make it about the code, not the people 
 - Don't start the flame war 
 - Share your knowledge 
 - Give as much as you receive 

+++

### The proper mindset… Tests

 - Bugs are not failure but insights
 - When you fix a bug, write a test for it
 - Grow your code and tests hand in hand…
    - … one step at a time
 - Always try to think about what can go wrong
 - Test is code


+++

### The proper mindset… Ethics 
 - Don't take anything for granted
 - Think before you code anything
 - Take ownership of the code / the product / the company

---

## Thanks for your attention

### Any Question ? 



