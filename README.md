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

**Where the posts came from:**

**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. -->

**Counts per label:**

| Label | Count | Share |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
| **Total** |  | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:*
>
> *Could have been:*
>
> *I chose, because:*

**2.**
> *The post:*
>
> *Could have been:*
>
> *I chose, because:*

**3.**
> *The post:*
>
> *Could have been:*
>
> *I chose, because:*

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
