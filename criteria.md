# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. _"The model is accurate"_ is an
opinion. _"Every label has an F1 of at least 0.60 on the held-out set"_ is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — _"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"_. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area                  | A question it could answer                                            |
| --------------------- | --------------------------------------------------------------------- |
| Overall accuracy      | How often does it need to be right to be worth using?                 |
| Per-label performance | Is one label allowed to be much worse than the others?                |
| Balance               | How lopsided can your label counts get before it's a problem?         |
| Consistency           | If someone else labelled the same posts, how often should you agree?  |
| Confidence            | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1.

The model achieves at least 60% accuracy on the held-out test set.

**Why this target:**

> The dataset contains four categories of programming discussions. Some posts overlap between categories, especially `learning_guidance` and `development_decision`. I expect the model to classify most posts correctly despite these similarities and overlaps.

---

## 2.

Each of the four labels achieves an F1 score of at least 0.5 on the held-out test set.

**Why this target:**

Overall accuracy alone could hide poor performance on a smaller category. I want the model to recognize all four types of posts rather than perform well only on the most common labels.

---

## 3.

The `learning_guidance` label achieves an F1 score of at least 0.65 on the held-out test set for each of the three evaluation seeds.

**Why this target:**

During the taxonomy stress test, I found that learning questions frequently overlap with development decisions and personal experiences. I chose a higher target for this label because I want the model to distinguish learning-related requests reliably despite these overlaps.

---

## 4.

No single label accounts for more than 50% of the final labelled dataset.

**Why this target:**

My initial exploration found different types of programming discussions, but I have not yet measured their distribution. I want to avoid a dataset dominated by one category. This way, the model has a reasonable opportunity to learn each label.

---

## 5.

At least 75% agreement on the 30 staff-labeled posts evaluated by the course's agreement.py script.

**Why this target:**

Applying written labeling rules consistently is important for building a reliable text classifier. The staff agreement exercise provides a reproducible way to check whether I can apply a predefined taxonomy consistently, including on ambiguous posts.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
