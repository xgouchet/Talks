
# Team Work

#### Because you can't always build an app all by yourself

_Wild Code School_ 

---

## About… Xavier F. Gouchet 

<h4>Lead Android Software Engineer at Workwell</h4>

###### <span><a>@xgouchet</a> on <i class="fa fa-github" aria-hidden="true"></i>, <i class="fa fa-stack-overflow" aria-hidden="true"></i>, <i class="fa fa-linkedin" aria-hidden="true"></i>, <i class="fa fa-twitter" aria-hidden="true"></i>, …</span>

+++

## What we do at Workwell
# <img src="logos/workwell.png" class="logo-inline"/>


---

# Pair Programming

+++

## What is Pair Programming

![](img/pair_programming.jpg)   <!-- .element: class="photo" -->

+++

 - Driver / Navigator
 - Projector Programming
 - Buddy Programming

---

## Why ? 

#### The purposes of pair programming   

+++

### Find the best solution on a problem

 - Discussion before typing
     - on the problem
     - on the context
     - on the possible solutions

+++

### Improve the code quality

 - Avoid easy mistakes
 - More probability to find edge cases

+++

### Generate discussion around…

 - Choices  
     - Algorithm  
     - Data Structure  
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

+++

### Downsides of Pair Programming

 - More time spent per ticket / less time spent delivering feature 
 - More intense than working alone 
 - Human conflicts 

---

## When ?

#### The right time to do pair programming

+++

### Complex programming tasks

 - Combine different skills / expertise 
 - Tackle the complexity by having two minds holding the big picture 

+++

### Urgent long tasks*

 - Bring juniors up to speed 
     - *if it actually speeds things 
 - Makes sure that urgent ≠ botched 

+++

### Training / Knowledge sharing

 - Give a tour of complex/old parts 
 - Explain advanced patterns / libraries 

---

## How ?

#### The <em>Do</em>s and <em>Dont</em>s of pair programming

+++

### No silent driver

 - Always explain what you're doing, and why

+++

### Pair Carefully

 - Avoid large disparity
 - Avoid affinity issues

+++

### Switch often

 - Share with everyone
 - Mix the team

+++

### Take breaks

 - Relax
 - Clear your mind
 - Take a step back

---

# Code Reviews

+++

## What is Code Review

![](img/code_review.png)   <!-- .element: class="photo" -->

---

## Why ? 

#### The purposes of code reviews

+++

### Find defects early

 - Logic fallacies 
 - Typos, spelling 
 - Edge cases 
 - Potential technical debt  

+++

### Harmonize the code base

 - Code style 
 - Naming conventions 
 - Architecture 
 - Libraries 

+++

### Generate discussion around…

 - Choices  
     - Algorithm  
     - Data Structure  
     - Architecture 
     - Libraries 
 - Features 
 - Best practices 

+++

### Team Building

 - Cohesion 
 - Trust 
 - Lower “Linkedin factor” 
 - Asynchronous Pair Programming 

+++

### Share knowledge

 - Onboard junior / new developers 
 - Everyone has something to teach 
 - Everyone has something to learn 

+++

### Downsides of code review

 - More time spent per ticket / less time spent delivering feature 
 - Senior developer frustration 

---

## When ?

#### The right time to do code reviews

+++

### “Automatic” code review

 - Static Analysis  
 - Tests (Unit, Integrated, Functionnal) 

+++

### Pre-commit

#### Pro 

 - Quality ensured before merge 
 - All code must be reviewed 

#### Cons 

 - Productivity impact 
 - Back & forth Hell ™ 

+++

### Post-commit

#### Pro 

 - Continuous development 
 - Limit git conflicts 

#### Cons 

 - Bug can ship to production 
 - Resolution can become non trivial afterwards 

+++

### Optional code reviews

 - by commit author 
 - by commit length 
 - by files modified 
 - random checks 
 - … ? 

---

## Who ?

#### Let the right people do the review

+++

### Remote code review

 - Anyone with access to GitHub / … 
 - Team lead 
 - Modified files watchers 

+++

### Pair review with another developer

 - Provide a single feedack 
 - Compare different viewpoints 
 - Tone down negative feedbacks 

+++

### Code Review Meeting with the author

 - 3 to 7 attendees 
 - Only for non trivial reviews 
 - Mentor the author 
 - Get in depth view 
 - Discuss alternatives 
 - Immediate feedback 

---

## How ?

#### The <em>Do</em>s and <em>Dont</em>s of code review

+++

### Writing reviewable code

 - Keep the commits short 
     - `git add --patch` / `git add -p`
 - Comment the code 
 - Use a proper commit message 
     - CR Brief for non trivial commits 
 - Link to the ticket 

+++

### Before submitting, review your own code

 - Find easy to spot issues 
     - Typos 
     - Commented code 
     - Duplicates / possible refactoring 
     - Copy / Paste errors 
 - Take a step back on your code 


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

---

# Overall behavior

+++

 - Stay open minded 
 - Make it about the code, not the people 
 - Don't start the flame war 
 - Share your knowledge 
 - Give as much as you receive 


---

## Thanks for your attention

### Any Question ? 

#### See also [codereview.stackexchange.com](https://codereview.stackexchange.com)


