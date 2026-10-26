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

TakeMeter is a text classification project that uses posts from Reddit's `r/learnprogramming` community to categorize programming-related discussions. The classifier sorts posts into four categories: `technical_help` for debugging and implementation problems, `learning_guidance` for learning resources and study advice, `development_decision` for technology, project, and career choices, and `experience_sharing` (my fourth, stretch label) for posts that share an experience or achievement without asking for anything. I fine-tuned a DistilBERT model using manually reviewed Reddit posts to see whether it could distinguish these categories based on their content.

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

**Stretch label — what this captures that the other three miss:**

> **Declaration note:** `experience_sharing` was designed alongside the other three labels in Milestone 2 (commit `74acff4`), but I did not declare it as a stretch item at the time. I am declaring it after the fact, with my TF's approval.

The other three labels all describe a _request_: fix my code (`technical_help`), help me learn (`learning_guidance`), or help me choose (`development_decision`). But `r/learnprogramming` also has posts that ask for nothing: someone celebrating a 100% on their first Java exam, sharing a LeetCode solution they're proud of, or posting an open-source learning tool they built. Without this label, those posts would have to be forced into a request label they don't actually make. It traces back to the "Learning Struggles and Experiences" distinction I noticed while reading in Milestone 1, and it holds 19 of my 210 posts (9%).

**What it changed:** adding it is why my multiple-request rule needed a final step: if neither the title nor the body contains a specific request, the post is `experience_sharing`. It also became the fallback for posts that fit no label, which is how I found the four I excluded and replaced (see `data/excluded_posts.csv`).

It is also my weakest label. It was involved in most of the failures when I stress-tested my definitions, the first trained model never predicted it, and with only 3 examples in the test split its scores will be the least stable of the four.

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

**Base model:** distilbert-base-uncased

**Settings:** 3 epochs, learning rate 2e-5, batch size 16, seed 42, max length 128. No changes from the defaults.

**Device:** mps, Apple Silicon GPU, torch 2.14.1

**Anything I changed from the defaults, and why:** I kept the default training settings to establish an initial baseline before experimenting with different configurations in Unit 6. The only changes were configuring the notebook with my four custom labels and personal information.

**Split sizes:** about 147 train / 31 val / 32 test. In the test split: learning_guidance 16, development_decision 10, technical_help 3 and experience_sharing 3. Note that the last two are under 8 examples each.

**Initial Results:** The model achieved 50% test accuracy and a macro F1 score of 0.167 on 32 held-out posts. `learning_guidance` achieved an F1 score of 0.667, while `technical_help`, `development_decision`, and `experience_sharing` each scored 0.000.

The confusion matrix showed that the model predicted `learning_guidance` for all 32 test posts. This suggests that the initial model did not successfully distinguish the four categories. Possible contributing factors include class imbalance, the small dataset, and truncation of longer posts at 128 tokens. I will investigate these issues in Unit 6 while preserving the original results for comparison.

---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1** Stress-testing my label definitions (Milestone 2)

- _What I asked for:_ I asked Claude to generate eight borderline programming posts that could reasonably fit more than one of my four labels. I wanted to test whether my definitions and decision rules were clear enough to classify ambiguous posts consistently.
- _What came back:_ Claude generated eight examples, including posts involving decisions about which programming languages to learn, projects to build, and career directions. While independently labeling them, I found inconsistencies between my `learning_guidance` and `development_decision` definitions. Some posts with similar structures received different labels.
- _What I changed:_ I revised my definitions to distinguish learning decisions from implementation and career decisions. I also added a rule for posts containing multiple requests: use an explicit request in the title first, otherwise use the final explicit question in the body. For requests matching multiple categories, I established a priority order of `technical_help` > `learning_guidance` > `development_decision`.

**Moment 2** AI-assisted pre-labeling and manual corrections (Milestone 4)

- _What I asked for:_ After independently labeling my first 20 Reddit posts, I asked Claude Code to pre-label the remaining 190 posts using the definitions and decision rules in my README.
- _What came back:_ Claude Code assigned labels to all 190 posts and flagged 51 as uncertain because they could reasonably fit multiple categories. Initially, `learning_guidance` accounted for approximately 61% of the dataset.
- _What I changed:_ I manually read and checked every AI-labeled post. I corrected 22 labels based on my own interpretation and written decision rules. For example, I classified the Rust plugin-system post as `development_decision` because the author was asking which architectural approach to take rather than reporting an existing error. I also excluded four posts that did not fit my taxonomy and reviewed their replacements. My final dataset contains 210 labeled posts.

**Pre-labelling disclosure:**

I used Claude to write the script that collected public Reddit posts through Reddit's RSS feed. I initially explored `r/soccer`, but the posts were dominated by video highlights and had insufficient written content for my classification task. A few days after downloading those data, some of the posts were blocked/deleted by the community guidelines. I therefore switched to `r/learnprogramming`.

I labeled the first 20 posts independently without any AI assistance and marked them `cold` in `labels.csv`. Claude Code pre-labeled the remaining 190 posts, after which I personally reviewed every suggested label and corrected 22 of them. I also reviewed four replacement posts suggested by AI after excluding posts that did not fit my definitions.

Claude Code helped with data collection, stress-testing, and initial classification suggestions, but I made the final decisions about the taxonomy, label corrections, and acceptance criteria.

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure                     | Baseline | Trained | Difference |
| --------------------------- | -------- | ------- | ---------- |
| Overall accuracy            | 0.500    | 0.500   | +0.000     |
| Macro F1                    | 0.349    | 0.167   | -0.183     |
| F1 — `development_decision` | 0.000    | 0.000   | +0.000     |
| F1 — `experience_sharing`   | 0.250    | 0.000   | -0.250     |
| F1 — `learning_guidance`    | 0.703    | 0.667   | -0.036     |
| F1 — `technical_help`       | 0.444    | 0.000   | -0.444     |

**What I predicted before I looked:** I expect the zero-shot baseline to outperform my fine-tuned model in overall accuracy and macro F1 because my first training run predicted only `learning_guidance`. The baseline may recognize distinctions among all four labels using their definitions without depending on my small training dataset.

**What the gap actually means:**

My prediction was partially correct. I expected the zero-shot baseline to outperform my fine-tuned model in both accuracy and macro F1. However, both models achieved 50% accuracy on the same 32 held-out posts, while the baseline achieved a higher macro F1 score of 0.349 compared with 0.167 for the trained model.

Fine-tuning did not improve overall accuracy and reduced macro F1 by approximately 0.183. The trained model predicted `learning_guidance` for all 32 posts, correctly classifying the 16 posts belonging to that category. The baseline correctly classified 16 posts as well, but recognized examples across multiple categories, including `technical_help` and `experience_sharing`.

Neither model correctly identified any `development_decision` posts. This suggests that distinguishing development decisions from learning guidance may be particularly difficult for the models. I will investigate whether this pattern continues across three training seeds and examine the confusion matrix to identify which labels are being confused.

The small dataset, class imbalance, and limited training may also have contributed to the fine-tuned model's performance, but further evaluation is needed to determine the cause.

---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion                           | Target                    | Seed 42 | Seed 7 | Seed 2024 | Verdict                       |
| ----------------------------------- | ------------------------- | ------- | ------ | --------- | ----------------------------- |
| 1. Overall accuracy                 | ≥ 0.60                    | 0.500   | 0.500  | 0.500     | Missed                        |
| 2. Every label's F1 (lowest shown)  | ≥ 0.50                    | 0.000   | 0.000  | 0.000     | Missed                        |
| 3. `learning_guidance` F1           | ≥ 0.65 on all three seeds | 0.667   | 0.667  | 0.667     | Met                           |
| 4. Largest label's share of dataset | ≤ 50%                     | 50.0%   | 50.0%  | 50.0%     | Met (at the limit)            |
| 5. Agreement with staff set         | ≥ 75%                     | —       | —      | —         | Met (agreement scored at 93%) |

**Device:** all three seeds ran on `mps` (Apple Silicon GPU), torch 2.14.1, 3 epochs, learning rate 2e-5, batch size 16. Matrix shown is from seed 42.

**Three-seed interpretation:**

The accuracy spread across seeds 42, 7, and 2024 was 0.000 because all three runs achieved the same accuracy of 50%. The model predicted `learning_guidance` for every test post, and each stratified test split contained 16 `learning_guidance` posts out of 32. As a result, the model correctly classified exactly half of the posts in every run.

Although the zero spread shows consistent results across the three seeds, it does not mean the model learned to classify all four categories successfully. Instead, it consistently relied on predicting the majority label.

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted         | technical_help | learning_guidance | development_decision | experience_sharing |
| ------------------------ | -------------- | ----------------- | -------------------- | ------------------ |
| **technical_help**       | 0              | 3                 | 0                    | 0                  |
| **learning_guidance**    | 0              | 16                | 0                    | 0                  |
| **development_decision** | 0              | 10                | 0                    | 0                  |
| **experience_sharing**   | 0              | 3                 | 0                    | 0                  |

Biggest confusion: 10 real `development_decision` posts called `learning_guidance`.
The other direction: 0 real `learning_guidance` posts called `development_decision`.

**My biggest off-diagonal number, and what it means:**

The largest misclassification was 10 actual `development_decision` posts incorrectly predicted as `learning_guidance`, while no `learning_guidance` posts were predicted as `development_decision`.

This indicates a strong directional bias toward `learning_guidance`. The model failed to recognize requests about implementation choices, project directions, and career decisions as a separate category. However, since all 32 posts were classified as `learning_guidance`, the problem extends beyond this single label boundary.

The identical results across seeds 42, 7, and 2024 suggest that this behavior is consistent across the evaluated splits rather than being caused by one unfavorable random seed. I will use the staff-agreement exercise to investigate whether inconsistent labeling contributed to the problem.

---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| #   | Criterion              | Target                    | Verdict | How I decided                                                                                                                                                                                                                                                 |
| --- | ---------------------- | ------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Overall accuracy       | ≥ 0.60 on all three seeds | Missed  | All three seeds achieved 0.500 accuracy, below the 0.60 target.                                                                                                                                                                                               |
| 2   | Every label's F1       | ≥ 0.50 on all three seeds | Missed  | `technical_help`, `development_decision`, and `experience_sharing` each scored 0.000 on all three seeds.                                                                                                                                                      |
| 3   | `learning_guidance` F1 | ≥ 0.65 on all three seeds | Met     | All three seeds achieved an F1 score of 0.667, meeting the 0.65 target. However, this was achieved by predicting `learning_guidance` for every test post (100% recall, 50% precision), not by successfully distinguishing the category from the other labels. |
| 4   | Largest label's share  | ≤ 50%                     | Met     | `learning_guidance` accounts for 105 of 210 posts (50%).                                                                                                                                                                                                      |
| 5   | Staff agreement        | ≥ 75%                     | Met     | 28 of 30 labels agreed with staff (93.3%).                                                                                                                                                                                                                    |

**Diagnoses**

### Criterion 1 — Overall Accuracy (Missed)

**Target:** At least 60% accuracy on each of the three seeds.

**Observed:** All three seeds achieved 50% accuracy, with a spread of 0.000.

**Diagnosis — Majority-class collapse**

The direct cause of the accuracy failure was majority-class collapse. The trained model predicted `learning_guidance` for every test post across all three seeds. Because each stratified test split contained 16 `learning_guidance` posts out of 32, predicting this label exclusively resulted in exactly 50% accuracy for every run.

The training dataset was imbalanced: `learning_guidance` represented 105 of 210 posts (50%), while `technical_help` and `experience_sharing` represented only 21 and 19 posts, respectively. With approximately 147 training posts and only three training epochs, the model had limited opportunities to learn the distinctions between the four categories. The class imbalance and limited training may have contributed to the model's collapse into predicting the majority label.

The zero-shot baseline achieved the same 50% accuracy but a higher macro F1 score of 0.349, compared with 0.167 for my fine-tuned model. It also correctly identified some `technical_help` and `experience_sharing` posts, while my trained model never predicted either category. This suggests that useful classification signals exist in the text, but my fine-tuned model failed to learn them effectively under the current training configuration.

My staff-agreement exercise produced 93.3% agreement (28 out of 30 posts), suggesting that I can generally apply written labeling rules consistently. However, my two disagreements revealed a tendency to assign labels based on resemblance without fully checking whether their definitions were satisfied. Since the staff exercise used a different three-label taxonomy, these results do not prove that my own four-label dataset was consistently labeled. Instead, they provide additional reason to examine my labeling decisions.

Overall, the model's majority-class collapse directly explains why Criterion 1 failed. The dataset imbalance, limited training examples, and potential labeling inconsistencies provide possible explanations for why the model developed this behavior.

### Criterion 2 — Every Label's F1 (Missed)

**Target:** At least 0.50 F1 for every label on each of the three seeds.

**Observed:** `technical_help`, `development_decision`, and `experience_sharing` each achieved an F1 score of 0.000 across all three seeds. Only `learning_guidance` achieved 0.667.

**Diagnosis — Limited training examples and inconsistent label application**

The model failed to recognize three of the four categories across all three seeds. The confusion matrix shows that it classified every test post as `learning_guidance`, resulting in F1 scores of 0.000 for `technical_help`, `development_decision`, and `experience_sharing`.

**Limited examples for `technical_help` and `experience_sharing`**

These two categories contained only 21 and 19 posts in the full dataset, leaving approximately 15 and 13 training examples, respectively. Each category had only three test examples in every evaluated seed.

The zero-shot baseline achieved F1 scores of 0.444 for `technical_help` and 0.250 for `experience_sharing`, demonstrating that some examples could be identified from their text and label definitions. However, my fine-tuned model never predicted either category.

The limited number of training examples is therefore a likely contributing cause of these failures. The baseline results suggest that the categories are distinguishable in at least some cases, but my current training configuration did not provide sufficient learning for the model to recognize them reliably.

**Inconsistent labeling of `development_decision`**

For `development_decision`, insufficient examples alone is a less convincing explanation because the category contains 65 posts. For `development_decision`, insufficient examples alone is a less convincing explanation because the category contains 65 posts. Despite this, all 10 `development_decision` examples in every seed's test split were incorrectly classified as `learning_guidance`. Even the zero-shot baseline achieved an F1 score of 0.000 for this category. Even the zero-shot baseline achieved an F1 score of 0.000 for this category.

The boundary between `learning_guidance` and `development_decision` is particularly difficult because both categories can involve programming languages, projects, and career development. My taxonomy distinguishes them based on whether the author is asking what or how to learn versus making an implementation, project, or career decision.

However, reviewing my original dataset revealed that I did not always apply this distinction consistently.

For example, I labeled "I wanna ask how to develop logic in coding" as `development_decision`, although it asks how to improve a programming skill and therefore fits `learning_guidance` under my definitions.

Similarly, I labeled "In the age of AI... should I even get back to programming" as `experience_sharing`, even though its career-related question better fits `development_decision`.

Additionally, 18 of my 22 manual labeling corrections moved posts into `development_decision`. This shows that many of my initial classifications differed from my later application of that category's definition, although the correction count alone does not prove those revisions were inconsistent.

My staff-agreement exercise provides supporting context. Both disagreements involved applying the `analysis` label to posts that resembled an argument but lacked the supporting evidence required by the definition. Those mistakes occurred under a different taxonomy, but they revealed a similar risk of applying labels without fully satisfying their decision rules.

Together, the concrete inconsistencies in my dataset and the difficult boundary between learning and career or implementation decisions support a diagnosis of inconsistent label application around `development_decision`. This may have made the distinction harder for the model to learn.

**Overall diagnosis**

Criterion 2 failed because the model collapsed into predicting `learning_guidance` for every post. The evidence identifies two contributing problems: limited training representation for `technical_help` and `experience_sharing`, and inconsistent application of the `development_decision` labeling rules.

These findings provide two possible improvement directions. For Milestone 5, I will choose one targeted change based on this diagnosis, keep the original acceptance criteria unchanged, and compare the results against the three original training seeds.

---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** 28 / 30 = 93%

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

> _The post:_ sp_019 - Nobody actually enjoys the long run. They enjoy having done it, which is a completely different thing, and the sport would be more honest if it said so.

> _Staff said / I said:_ `hot_take` / `analysis`

> _My call, and why:_ The post distinguishes between enjoying a long run and enjoying having completed it. I interpreted this distinction as an argument supporting the author's conclusion. However, the staff taxonomy requires a specific, checkable fact that actively supports the argument. The author provides no such evidence for the sweeping claim that nobody enjoys long runs. I agree that hot_take is the better-supported label. This follows Rule 1 of the staff taxonomy: an `analysis` label requires a specific, checkable fact that supports the argument. Neither post provides that supporting evidence.

> _Which pile:_ (a) the rule covered it and you applied it loosely — a consistency problem

**2.**

> _The post:_ sp_020 - Every injury thread on this forum is the same injury and the same three replies.

> _Staff said / I said:_ `hot_take` / `analysis`

> _My call, and why:_ I interpreted the claim that injury threads contain similar discussions as an analysis of a recurring pattern. The claim is potentially verifiable, but the author provides no actual examples, comparisons, or supporting evidence. The staff rules require evidence to support the conclusion, not merely a claim that could be investigated. Therefore, I agree with the staff's hot_take classification. This follows Rule 1 of the staff taxonomy: an `analysis` label requires a specific, checkable fact that supports the argument. Neither post provides that supporting evidence.

> _Which pile:_ (a) the rule covered it and you applied it loosely — a consistency problem

**What the pattern in my disagreements tells me:**
Both disagreements came from interpreting arguments or potentially verifiable claims as `analysis` without checking whether the author provided supporting evidence. The staff taxonomy helped me distinguish between a statement that could be verified and an argument actually supported by a checkable fact.

The 93% agreement rate suggests that I can generally apply the staff's written definitions consistently. However, this agreement exercise used a different three-label taxonomy from my own four-label TakeMeter classifier, so it does not establish that my training labels were free of inconsistencies.

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
