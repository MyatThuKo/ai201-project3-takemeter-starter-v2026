# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

TakeMeter is a text classification project that uses posts from Reddit's `r/learnprogramming` community to categorize programming-related discussions. The goal is to fine-tune a language model to recognize different types of posts based on their content.

### Community Selection and Observations (Milestone 1)

I selected r/learnprogramming because the community contains a variety of programming-related questions, technical discussions, and personal experiences. The posts generally contain enough written context for text classification.

After reviewing approximately 40 posts from the collected dataset, I noticed four recurring distinctions:

1. **Learning Resources and Guidance:** Users ask for tutorials, courses, books, and advice on how to begin learning programming.

2. **Technical Problems and Debugging:** Users describe programming issues, often including code snippets, error messages, or unexpected behavior.

3. **Learning Struggles and Experiences:** Users discuss difficulties understanding concepts, solving problems independently, or staying motivated.

4. **Technology and Career Decisions:** Users ask for help choosing programming languages, frameworks, career paths, or development technologies.

Some posts overlap between these distinctions. For example, someone struggling to learn Python might also ask for learning resources. This suggests that clear definitions and decision rules will be necessary when designing the final labels.

These observations will guide the label taxonomy developed in Milestone 2.

### Differences in Post Quality

I noticed that some posts provide more detailed context than others. For example, technical questions that include code snippets, error messages, and explanations of what the user has already attempted are generally more substantial because other community members can better understand the problem and provide specific solutions. In contrast, some posts ask broad questions about learning programming without explaining their experience, goals, or challenges, making it harder for others to provide useful advice.

However, a longer post is not necessarily more substantial. A short post with a clear question and relevant details can still be more useful than a lengthy post without a specific purpose.

---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `technical_help`

**Definition:** A post requesting help diagnosing or resolving a specific programming error, unexpected behavior, or implementation problem, even if it also describes a project or learning experience.

**Example 1:**

> "Python code takes 10-20 seconds to start — Hello, I started learning python recently I dowloaded it, also vs code and python extension for it. The poblem is, when I start a programm (even a simple one, whick only takes an input fron the user and prits it) takes 10 or more seconds to start or just dosen't work at all then i clic soething and it kindof crashes itself, but thats my fault for mesinf with it, when I leave it, it just takes really lng dose somone know how to fix it and/or how to make folders proporly and where to keep them (could be the problem)?"

**Example 2:**

> "Why is the program showing invalid when the number is within the range? — int user_year; // input year cout > user_year; while(user_year > 2099 || user_year The user input needs to be greater than 1900 and less than 2099, so 1900 - 2099. Whenever I input a value in between those numbers such as 2010, it gives invalid input. What I want if user_year is outside the specified range indicate ""Invalid input"" but loop back to user input. I used an if statement but the problem was that it did not loop back to cin EDIT: HERE IS MY ORIGINAL CODE while (!(cin >> user_year) || user_year 2099) { cin.clear(); cin.ignore(10000, '\n'); cout FIXED: I had a function in my program and it was causing it to return 0 as the year. but the code above is correct"

### `learning_guidance`

**Definition:** A post requesting advice on learning programming, including study methods, learning resources, understanding concepts, overcoming difficulties, or choosing what and how to learn.

**Example 1:**

> "Starting from Zero in C++ — Hi everyone! I’m pursuing CSE at a Tier-4 college and have zero programming knowledge. I’m entering the tech field for the first time and want to start with C++ from scratch. What’s the best way to learn C++? Which free resources would you recommend, and what common mistakes should I avoid? Also, how should I build my coding and problem-solving skills to become internship- and job-ready?"

**Example 2:**

> Resources to better coding — Hi! Can anyone suggest interactive resources to study DSA and Object Oriented Python like that of deeplearning.ai to learn machine learning and deep learning.

### `development_decision`

**Definition:** A post requesting advice on choosing implementation technologies, project directions, or career paths, excluding decisions primarily about learning.

**Example 1:**

> "It is worth be a Front End Dev? — I'm Starting to be a FrontEnd Dev but I saw lot of jobs that require Full stack or some of Back End, In my Learn I was trying just to be a Only Front End but sometimes you search and all the jobs want a Full stack or want Back End. ¿Do you think can people be a only Front End Dev or have to learn Backend too obligatory?"

**Example 2:**

> "Choosing the Right Tech Stack for My First Full-Stack Project — I have learned the basics of programming and web development, and I want to build my first real-world full-stack project: an e-commerce website for a clothing brand, for which I already have a client. I want to make it professional, from UI/UX design and database architecture to security, testing, and deployment. What tech stack would you recommend? Finally, how important is the tech stack to recruiters? If a company uses different technologies from those I used in my project, could this put me at a disadvantage during a technical interview? What advice would you give me to make this project stand out in my portfolio and prepare for interviews? Thank you in advance for your advice!"

### `experience_sharing`

**Definition:** A post sharing a programming achievement, project, or personal experience without requesting a specific technical solution, learning recommendation, or development decision.

**Example 1:**

> "im kinda proud of this solution i wrote even though it was an ""easy"" i still felt like i grew a lot — the problem: Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid. An input string is valid if: Open brackets must be closed by the same type of brackets. Open brackets must be closed in the correct order. Every close bracket has a corresponding open bracket of the same type. Example 1: Input: s = ""()"" Output: true Example 2: Input: s = ""()[]{}"" Output: true Example 3: Input: s = ""(]"" Output: false Example 4: Input: s = ""([])"" Output: true Example 5: Input: s = ""([)]"" Output: false my solution: (on leetcode) class Solution: def isValid(self, s: str) -> bool: inputs = { ""("":1, "")"":9, ""{"":2, ""}"":8, ""["":3, ""]"":7} prev_bracket=[] if(len(s)%2!=0): return False for a in s: if inputs[a]"

**Example 2:**

> "First job anxiety — ​ I recently got a job from a totally new field I have not worked in before, software development to be exact. My only experience with this is from school, which was very thin and some very small testing I've done myself. They all know I'm new to this, but lack of training and guiding is what gives me anxiety. Everything is huge (codebases, databases, everything) and even the field the company's software is for, is very foreign to me. The HR ""training"" was good and I was told that the other employees will help me out, but in fact they all seem to be very distant and while they do help a bit, I feel like they want to get out of the situation asap. My first days have been going through codebase and db and trying to figure out how everything works. I was given a task to implement a small feature, but no one is aware of that and the answers I get, don't necessarily answer my questions. I feel overwhelmed, anxious and exhausted already. I feel like I'm supposed to do stuff already, but I also feel like I'm a burden. The team is quite small and everyone got their hands full of work already. I know a lot of you have been in this same situation. Did things figure themselves out at a time or how it ended? Cheers!"

### The hardest boundary

**Which two labels:** `learning_guidance` vs `development_decision`

**The decision rule I used every time:**

Some posts involve choosing between programming languages, technologies, or projects, but the reason behind the choice determines the label.

If the author is deciding what or how to learn, including choosing programming languages for study, courses, or learning methods, I classify the post as `learning_guidance`.

If the author is choosing technologies for an actual implementation, deciding which project to build, or selecting a professional career direction, I classify the post as `development_decision`.

For example, someone asking whether to learn C before C++ is seeking `learning_guidance`, while someone deciding whether to build a Linux process-monitoring project is seeking a `development_decision`.

**Handling posts with multiple requests:**

> Added this after having AI stree test my label definitions

When a post contains multiple requests, I first check whether the title contains an explicit question or request that matches one of my four labels. If it does, I use that request to determine the label.

If the title does not contain a request that matches a label, I use the final explicit question or request in the post body.

If neither the title nor the body contains a specific request, I classify the post as `experience_sharing`, provided it describes a programming experience, achievement, or project.

If the selected request contains multiple types of help, I use the following priority order: `technical_help` > `learning_guidance` > `development_decision`.

Mentioning an error, technology, or personal experience does not automatically determine the label. The request must match the label's definition.

---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:** The posts come from subreddit `r/learnprogramming`

**How I labelled them:**

- 20 posts labelled cold
- 190 pre-labelled by Claude, and manually checked
- 22 corrected
- 4 posts that fit no label were excluded and replaced, logged in data/excluded_posts.csv

**Counts per label:**

| Label                | Count | Share |
| -------------------- | ----- | ----- |
| learning_guidance    | 105   | 50%   |
| development_decision | 65    | 31%   |
| technical_help       | 21    | 10%   |
| experience_sharing   | 19    | 9%    |
| **Total**            | 210   | 100%  |

**Three hard cases**

**1.**

> _The post:_
> "Plugin system for multi platform rust application — Hi, I'm building so I'm making a peer to peer reading tracker that has multiple native clients (one for my Linux laptop and one for my android phone) with a Rust core that handles most of the actual logic and the client being in C and GTK4 for my Linux client and Kotlin for my android app. The thing is I want to have cover source logic behind plugins since that's never really stable and I don't want to have to rebuild my app at every new source I want to add either. Is there a tool that helps with that? (Sorry if this is a dumb question or if my explanation isn't very clear.)"
> _Could have been:_ `technical_help` or `development_decision`

> _I chose, because:_ chose `development_decision` because the author is asking for guidance on which tool or architectural approach to use for their plugin system. They are not describing an existing error or unexpected behavior that needs fixing. Instead, they want to determine the appropriate implementation direction for their application, which fits `development_decision` better than `technical_help`.

**2.**

> _The post:_
> "Feedback on HammingCube: a 3D parity code implemented in C11 — Hi! I've been exploring error-correcting codes through a small C11 project called HammingCube. It implements a three-dimensional product of single-parity-check codes (not the classical Hamming code). It encodes 64 data bits into 125 bits, corrects up to three unknown bit flips, and recovers up to seven erasures when their positions are known. The repo includes a CLI, tests, and a lesson-style README explaining the math. I used AI assistance while developing the code and documentation, and I'd appreciate independent human feedback. In particular: Do you see correctness or edge-case problems in the erasure decoder's GF(2) elimination? Is the C API clear about invalid, ambiguous, and successfully recovered inputs? Is the README's explanation of the distance-8 guarantee understandable? Repo: https://github.com/piecatdev/HammingCube"

> _Could have been:_ `technical_help` or `development_decision`

> _I chose, because:_ I chose `development_decision` because the author has already implemented a project and is requesting feedback about its API design, correctness, and documentation. I classified it as `development_decision` because some questions concern whether the implementation and design choices are appropriate. However, `technical_help` is also reasonable because the author explicitly asks reviewers to identify correctness problems and edge cases in the code

**3.**

> _The post:_
> "Should I stick with Java or switch to JavaScript? Am I struggling because Java is difficult, or am I choosing the wrong path? — I'm transitioning from data analytics to software engineering, and I've been torn between pursuing Java and JavaScript. I've been learning Java through Hyperskill, but lately, I've been questioning whether I made the right choice. One of my main reasons for choosing Java is that it's widely used by large enterprises and big companies. Coming from a developing country, I'd like to eventually work overseas, and I feel that Java might give me a better chance of landing that kind of opportunity. I also wonder whether enterprise Java jobs offer more stability and a clearer career path than JavaScript jobs, although I'm not sure if that's actually true. My impression is that JavaScript has a lower barrier to entry, which makes the field feel more saturated. I imagine I might end up working as a freelancer, joining a consultancy, or working remotely for an overseas company rather than relocating abroad. Of course, I could be completely wrong about these assumptions, so I'd appreciate hearing from people with experience in both ecosystems. I've also heard people say that JavaScript developers have to constantly keep up with new frameworks and changing technologies, which can lead to burnout. In contrast, I've heard that Java's ecosystem is more stable and that its core technologies don't change as rapidly. As I get older, I find myself less willing to spend all my time keeping up with new technologies. I'd rather build a solid set of skills that remain useful for years and use the mental energy I have left to enjoy other aspects of life. Interestingly, I also enjoy Java in a way I didn't quite experience with Python. I feel like I'm actually programming and building things rather than just writing scripts for data analysis. There's something satisfying about it that makes me want to keep going. The problem is that whenever I encounter a particularly challenging assignment, I start questioning my decision. Sometimes, I feel like I could solve the same problem much more easily in Python. With Java, I'm constantly running into concepts, syntax, and unfamiliar ways of doing things that I don't fully understand yet. It feels like trying to survive in a foreign country without speaking the local language. This makes me wonder whether I'm struggling because Java genuinely isn't the right fit for me, or whether I'm simply going through the uncomfortable learning curve that comes with learning a new language and moving into software engineering. Part of me wants to switch to JavaScript because it might be easier to learn and allow me to make progress faster. Another part of me wonders whether I'd just be running away from the difficulty instead of pushing through the stage where everything feels unfamiliar. Since I'm in my mid-20s, I want to break into software engineering as quickly as possible. JavaScript feels like it might help me get there sooner, while Java feels like more of a gamble because of the commitment and steep learning curve involved before I can see the results of my efforts. So, for those of you who have learned Java or transitioned into software engineering from another field: - Did you go through a similar phase where you questioned your choice of programming language? - Is sticking with Java worth it if my long-term goal is to work for a large company, potentially overseas? - If you've worked with both Java and JavaScript, how different are their job markets, career opportunities, and long-term prospects in practice? - How did you know whether you were struggling because of the learning curve or because you were pursuing the wrong path? To be honest, I might be posting this partly because I want someone to tell me that it's normal for Java to feel difficult at first and that things will eventually click. But I'd genuinely appreciate honest advice, even if it means reconsidering my current path. Thank you!"

> _Could have been:_ `learning_guidance` or `development_decision`

> _I chose, because:_ I chose `development_decision` because the author discusses difficulties learning Java but also compares Java and JavaScript based on job opportunities, long-term stability, and a possible transition into software engineering. I classified it as `development_decision` because the choice is closely connected to the author's professional career direction rather than simply understanding a programming concept. However, `learning_guidance` is also reasonable because the author asks whether their struggles are part of the normal learning process.

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**

**Settings:** <!-- epochs, learning rate, batch size, seed -->

**Anything I changed from the defaults, and why:**

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->



---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Moment 2**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Pre-labelling disclosure:**

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy |  |  |  |
| Macro F1 |  |  |  |
| F1 — `label_one` |  |  |  |
| F1 — `label_two` |  |  |  |

**What I predicted before I looked:**

<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->


<!-- Two sentences. Your confusion matrix is the evidence. -->

<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
