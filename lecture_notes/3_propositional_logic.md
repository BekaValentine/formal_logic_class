# Propositional Logic

The remainder of these notes will cover modern logic, discussing things that started to be researched in the late 1800s and which continue to this day. The main focus of this note is Propositional Logic, which will allow us to look at a variety of proof systems that are used to various degrees within then field of logic. Propositional Logic is the modern way of thinking about the kinds of logic that are Boolean-ish. Boole's logic was based on truth values and that historically gave rise to interesting questions, such as how to cope with the complexities of using just truth values and truth tables to determine relationships between propositions. Another is how to extend the logic to hand more complex propositions that involve predication, quantification, and so on. Still further are questions that arose from both ancient philosophy and modern mathematical logic, questions like "are propositions always strictly either true or false? can they be a mix of the two, or maybe neither true nor false?"

The developments that happened as a result of these questions often involved going well beyond Boole's own logic and techniques, forcing the development of whole new ways of thinking about Logic and logics. When those techniques are then turned back onto the matter of Boole's logic, we get the subject that is Propositional Logic, or more specifically *Classical* Propositional Logic. What we'll do now is explore some of these questions and techniques as they apply specifically Propositional Logic.

## Classical Proofs via Truth Tables

We saw before in Note 1 that we could look at the relationships between propositions using truth tables, and then also by some simple calculational methods. But there are other ways we can reason as well, derived from truth tables but not relying on them.

Let's observe again the truth table for conjunction as a reference point:

| ?X | ?Y | ?X & ?Y |
| -- | -- | ------- |
| f  | f  |    f    |
| f  | t  |    f    |
| t  | f  |    f    |
| t  | t  |    t    |


Supposing we know that the value of a proposition `?X` is true, and also that the value of a proposition `?Y` is true, this truth table lets is conclude that the value of the compound proposition `?X & ?Y` is also true. If we know only that `?X` is true, we cannot say anything about `?Y` or `?X & ?Y`. But suppose that instead we know only that `?X & ?Y` is true? Can we say anything about `?X` or `?Y`? Yes! Because the compound proposition is true, it must be the case that `?X` is true and so is `?Y`. In fact, we saw this previously when looking at how to see if a proposition was satisfiable, but instead of assuming that we knew the conjunction was true, we were asking how it might be true.

These kinds of patterns of inference can in fact be used with a more convenient notation, the one we saw for Aristotelian arguments:

```
  ?X             ?X & ?Y        ?X & ?Y
  ?Y           ∴ ?X           ∴ ?Y
∴ ?X & ?Y
```

This same game can be played with a whole variety of propositions. There are a number of very common ones that people like to use, however. For example, this one, called the Disjunctive Syllogism (names again, ey?):

```
  ?X | ?Y
  !(?X)
∴ ?Y
```

Why is this pattern of reasoning ok? Because if we built the truth table containing metavariables `?X`, `?Y`, and the propositions `?X | ?Y` and `!(?X)`, we would find that, indeed, when those two are true, it's always the case that `?Y` is also true. It's precisely the second row here:

| ?X | ?Y | !(?X) | ?X \| ?Y |
| -- | -- | ----- | -------- |
| f  | f  |   t   |    f     |
| f  | t  |   t   |    t     |
| t  | f  |   f   |    t     |
| t  | t  |   f   |    t     |

Here are some more common propsitional syllogisms and their names:

```
(Pure) Hypothetical Syllogism

    ?X -> ?Y
    ?Y -> ?Z
  ∴ ?X -> ?Z

Modus Ponens

    ?X -> ?Y
    ?X
  ∴ ?Y

Modus Tollens

    ?X -> ?Y
    !(?Y)
  ∴ !(?X)

Constructive Dilemma

    (?X -> ?Y) & (?Z -> ?W)
    ?X | ?Z
  ∴ ?Y | ?W

Destructive Dilemma

    (?X -> ?Y) & (?Z -> ?W)
    !(?Y) | !(?W)
  ∴ !(?X) | !(?Z)

Addition (on the left, similarly for on the right)

    ?X
  ∴ ?X | ?Y

Simplification (on the left, seen before, similarly for on the right)

    ?X & ?Y
  ∴ ?X

Conjunction (seen before)

    ?X
    ?Y
  ∴ ?X & ?Y
```

Obviously any number of inference patterns can be found. Let's take a look at how these patterns can be used to form a larger argument. We saw with Aristotelian arguments that we start from a bunch of premises and derive conclusions from them one after another, sometimes relying on some conclusions to be premises of subsequent inference steps. So let's see an example of this, where we'll use these propositional syllogisms to prove that `A & (B & C)` entails `(A & B) & C`:

```
    A & (B & C)
  ∴ A

    A & (B & C)
  ∴ B & C

    B & C
  ∴ B

    B & C
  ∴ C

    A
    B
  ∴ A & B

    A & B
    C
  ∴ (A & B) & C
```

## Fitch Style

If we number the propositions in our proofs, we can put the justifications into the proofs, and make it less noisy by removing repeated occurences of propositions and also the now redundant therefore sign:

```
1.  A & (B & C)
2.  A            (simplification on 1)
3.  B & C        (simp. on 1)
4.  B            (simp. on 3)
5.  C            (simp. on 3)
6.  A & B        (conjunction on 2 and 4)
7.  (A & B) & C  (conj. on 6 and 5)
```

Another common notation for the information in the parentheses is to list the relevant lines and then the rule name or some abbreviation thereof. For instance, instead of `conjunction on 2 and 4` one might find `2, 4, conj`. There are many such notations, and you'll get used to working with them flexibly.

Using this kind of proof system can be more or less difficult depending on your choice of what syllogisms you choose to rely on. The above ones are somewhat traditional and also awful for reasoning. Some of them are good, but there are games that are just unbearable.

Additionally, there are some questions which are not easily answered in this system. For instance, supposing we know that some proposition, such as `A & B`, entails some other, such as `A`, what then does this say about the proposition `(A & B) -> A`? Well, maybe nothing, maybe something. But it would be nice to say that if we can somehow construct a proof that starts at `A & B` and leads to `A`, then that proof itself allows us to conclude `(A & B) -> A`. Or in general, if `?X` lets us proof `?Y`, then we ought to be able to conclude `?X -> ?Y`. This motivates the introduction of another kind of proof to be added called a conditional proof.

### Conditional Proofs

The usual notation for this is to indent the lines that are the "helper" proof, often placing a single big vertical line in front of them all to group them, and then to reference the helper proof by the range of lines that go into it. For instance, to prove `(A & B) -> A`, we would write

```
1.   | A & B
2.   | A          (1, simp)
3.  (A & B) -> A  (1-2, conditional proof i.e. cp)
```

Sometimes the vertical lines go to the left of the numbers:

```
     | 1. A & B
     | 2. A       (1, simp)
3.  (A & B) -> A  (1-2, cp)
```

These notes will stick with the first format.

Let's use conditional proofs to prove `(A & B) -> C` entails `A -> (B -> C)`:

```
1.  (A & B) -> C
2.    | A
3.    |  | B
4.    |  | A & B   (2, 3, conj)
5.    |  | C       (1, 4, modus ponens i.e. mp)
6.    | B -> C     (3-5, cp)
7.  A -> (B -> C)  (2-6, cp)
```

Notice here we're using a nested condition proof too!

One might well wonder then what are the criteria for which a conditional proof is acceptable and the answer is this: A conditional proof can have only one unjustified proposition within it, and that is the proposition that becomes the left side of the implication (not counting the unjustified propositions in nested conditional proofs). That proposition is called the hypothesis, and the use of the conditional proof technique is said to "discharge" that hypothesis because the c onclusion of the conditional proof is an implication, and that hypothesis is no longer in need of justification -- it's not considered an unjustified proposition of the whole proof, just the internal helper proof.

There is a convenient notation we can use for distinguishing the hypothesis of a conditional proof from the conclusions drawn from it: we put a big horizontal line between them and the conclusions that follow from them. Here's the proof of `(A & B) -> A` again with this notation:

```
1.   | A & B
     |----------
2.   | A          (1, simp)
3.  (A & B) -> A  (1-2, conditional proof i.e. cp)
```

Indeed, this notation can be used in general to distinguish between any unjustified propositions (hypotheses or general assumptions or whatever), and so since the above proof has no overall assumptions, then consistent use of the horizontal divider line gives us

```
    |-----
1.  |  | A & B
    |  |----------
2.  |  | A          (1, simp)
3.  | (A & B) -> A  (1-2, conditional proof i.e. cp)
```

Notice that the *whole* proof has this horizontal division (and a vertical line on the left), and above the horizontal division is nothing at all, because the proof as a whole relies on no assumptions! This will often be omitted, tho, because it's a bit noisy.

Sometimes assumptions/hypotheses will be labeled by `hypothesis` as if this was a rule itself, but these notes leave that out for a few reasons, not the least of which is that you know they're hypotheses by the position above the horizontal dividing line.

The proof for that `(A & B) -> C` entails `A -> (B -> C)`:

```
1.  | (A & B) -> C
    |--------------
2.  |   | A
    |   |-----
3.  |   |  | B
    |   |  |------
4.  |   |  | A & B   (2, 3, conj)
5.  |   |  | C       (1, 4, modus ponens i.e. mp)
6.  |   | B -> C     (3-5, cp)
7.  | A -> (B -> C)  (2-6, cp)
```

With this notation in mind, we can actually make hypothetical proofs simpler by allowing multiple hypotheses, and multiple discharges. For instance, suppose we wish to derive the rule of (Pure) Hypothetical Syllogism:

```
1.  | A -> B
2.  | B -> C
    |--------
3.  |  | A
    |  |-----
4.  |  | B     (1, 3, mp)
5.  |  | C     (2, 4, mp)
6.  | A -> C   (3-5, cp)
```

Again, in general, the shape of a conditional proof is

```
 | ?X
 |-----
 | ...some stuff
 | ?Y
?X -> Y
```

By the way, since we like naming things, this proof notation with the vertical and horizontal lines, etc. is called Fitch Style, after the logician Frederic Benton Fitch who invented it.

### Indirect Proof

Now, let's look at another important kind of proof rule that uses the same hypothetical and indented syntax: the indirect proof. This kind of proof involves assuming some proposition, and then from that assumption concluding a contradiction (that is to say, concluding both a proposition and it's negation), and then discharging the hypothesis by concluding outside of the internal proof that the hypothesis is false. The shape of this proof is roughly like so:

```
 | ?X
 |-----
 | ...some stuff
 | ?Y
 | !(?Y)
!(?X)
```

So let's prove `A -> B` and `!B` entail `!A` using an indirect proof:

```
1.  | A -> B
2.  | !B
    |--------
3.  |  | A
    |  |------
4.  |  | B      (1, 3, mp)
5.  |  | !B     (repeating 2)
6.  | !A        (3-5, indirect proof)
```

Effectively, we've proven that Modus Tolens is a theorem in a system with Modus Ponens and indirect proofs.

One may wonder at this point what justifies us having conditional and indirect proofs. In the setting of Boole-style logics, they're just inline notations for a bunch of truth table manipulation. In particular, we're setting up truth tables for the hypothesis and conclusions, filling out the table to the point where we can see the truth values of the hypotheses, and then proceeding only to fill out rows where those hypotheses' values are true.

### Tautologies and Contradictions

Proving tautologies in Fitch style means proving something with no top-level hypotheses. Proving contradictions, as previously mentioned, means proving a proposition and its negation at the same time as conclusions.

### Conditional Proofs as Primitive Idea

One might observe that the following is provable: if `?X | ?Y` and `?X -> ?Z` and `?Y -> ?Z` then `?Z`. And indeed various versions of this built out of these with implication and conjunction, for instance the clean little propositional schema `((?X | ?Y) & (?X -> ?Z) & (?X -> ?Z)) -> ?Z`.

We might even go further and observe that, in general, we can prove `?X -> ?Z` and `?Y -> ?Z` by use of conditional proofs, such that, where we wanted to use `?X -> ?Z` or `?Y -> ?Z`, we could instead have said that `?X` (resp. `?Y`) conditionally entails `?Z`.

Given this, we might then say, we can use conditional proofs for more than just concluding `->`. We might, for instance, say that this kind of proof is also valid:

```
1.  ?X | ?Y

2.  | ?X
    |----
3.  | ?Z

4.  | ?Y
    |----
5.  | ?Z

6. ?Z (1, 2-3, 4-5, conditional proof for disjunction)
```

This kind of proof -- where instead of proving an implication and then using it for some other stuff, is actually quite nice, because after all, the implication wasn't really all that necessary, it was the entailment that it corresponded to that mattered. This will motivate a later notational development that treats conditional proofs as fundamental -- involving something called a "hypothetical judgment" -- and will ultimately let us ask very interesting questions about the nature of our logic at a macroscopic level. 

## Tableau Proofs

Another popular kind of proof notation is the Tableau Proof, or the Method of Tableaux (French plural of Tableau). This method has some similarities to the proofs we've seen so far, but also has some interesting differences.

We start by looking exclusively at the syllogisms, or inference rules, that don't involve conditional proofs above. That is to say, those such as Conjunction or Simplification or Addition:

```
   ?X             ?X & ?Y        ?X
   ?Y           ∴ ?X           ∴ ?X | ?Y
 ∴ ?X & ?Y
```

All of these rules are additive, that is to say, when we used these rules, we're always gaining information. The tableau proof notation starts from this perspective. We initially start with a set of premises, let's say `A`, `B`, and `C`. We arrange this into a box like so:

```
   ---
  | A |
  | B |
  | C |
   ---
```

Each inference we want to make from a tableau is drawn by extnding a line down from the bottom-most box. to a new box with the conclusion. So for instance to use the Conjunction rule on `A` and `B`, we would write

```
     ---
    | A |
    | B |
    | C |
     ---
      |
   -------
  | A & B |
   ------- 
```

If we wish to indicate how we arrived at the conclusion, we can put numbers on the left, aligned with propositions, and then reasons on the right:

```
        ---
1.     | A |
2.     | B |
3.     | C |
        ---
         |
      -------
4.   | A & B |   (1, 2, conj)
      ------- 
```

We continue to extend this downward from the bottom, even if we're using only propositions from boxes further up, for instance:

```
        ---
1.     | A |
2.     | B |
3.     | C |
        ---
         |
      -------
4.   | A & B |   (1, 2, conj)
      ------- 
         |
      -------
5.   | A & C |   (1, 3, conj)
      ------- 
```

At this point, we've only extnded the bottom-most box with a single line each time, and in those cases, we typically avoid lines and boxes entirely, just writing

```
1.  A
2.  B
3.  C
4.  A & B  (1, 2, conj)
5.  A & B  (1, 3, conj)
```

This of course looks very much like how we simplified our proofs earlier, but in the context of tableaux, we understand this to be amenable to the box operations.

It is at this point that we now can see something new with tableau proofs: branching. In our syllogisms above, we do not have a rule such as 

```
    ?X | ?Y
  ∴ ?X
```

Indeed, this rule is not valid. But the truth table that defines disjuntion lets us observe the following fact: every row where `?X | ?Y` is true is one either *either* `?X` is true, *or* `?Y` is true. We import this fact into the method of tableaux by *branching* the tableau:

```
     -------
    | A | B |
     -------
       / \
     /     \
   ---     ---
  | A |   | B |
   ---     ---
```

But what does this *mean*? Like, it's clearly not the case that `A` is true just because it's in a box coming off of the upper box, so what does it mean? In some sense, a tableau like this is saying that *at least one of* the paths from the root to a leaf box is in some sense "true". I put true in quotes here because even that's kind of wibbly in terms of what its supposed to mean when said of a tableau.

Relating this to the truth table makes it clearer what we're doing: each leaf box/path from the root to the leaf box corresponds to a row in a compound truth table with the designated propositions as true. Each "inference", each expansion of a leaf box into one or more sub-boxes, involves filling out more of the rows and columns. A single additional line down may involve adding a new column, as with conjunction.

Going from this:

```
   ---
  | A |
  | B |
   ---
```

to this:

```
     ---
    | A |
    | B |
     ---
      |
   -------
  | A & B |
   -------
```

corresponds to going from this partial compound truth table:

| A | B |
| - | - |
| t | t |

to this one:

| A | B | A & B |
| - | - | ----- |
| t | t |   t   |

We expand a single path to a leaf box, which contains two propositions (i.e. a row in a truth table with those two columns labeled as true) into a single path to a leaf box, which contains those propositions but also a new proposition that is true (i.e. we add to that row a new column that is also true).

Similarly, going from this:

```
   -------
  | A | B |
   -------
```

to this:

```
     -------
    | A | B |
     -------
       / \
     /     \
   ---     ---
  | A |   | B |
   ---     ---
```

corresponds to expanding this truth table:

| A \| B |
| ------ |
|   t    |

to this one:

| A \| B | A | B |
| ------ | - | - |
|   t    | f | t |
|   t    | t | f |
|   t    | t | t |

Or, perhaps more accurately, to this one that leaves cells blank when the value doesn't matter:

| A \| B | A | B |
| ------ | - | - |
|   t    |   | t |
|   t    | t |   |

We take the one path with one proposition, which corresponds to the single row with a only true propositions, and split it into two paths with two propositions on each path, which corresponds to two rows where all of the propositions that are mentioned are true.

We might be inclined to actually represent the truth table, in which case we would do a three-way expansion in the tableau instead. But to do this, we need to have a way of distiguishing between the true propositions and false ones, since after all we want to be explicit. So instad of only writing a propsition, we'll write it's value next to it too:

```
   -------------
  |  A | B   t  |
   -------------
```

Now it's clear how to do a full three-way split:

```
         -------------
        |  A | B   t  |
         -------------
            /  |  \
          /    |    \
        /      |      \
   -----     -----     -----
  | A t |   | A t |   | A f |
  | B f |   | B f |   | B t |
   -----     -----     -----
```

A not uncommon shorthand to avoid annotating with truth values is instead to just add negation instead of the negative values, which we will use here as well, but with the caveat that technically, a negated proposition is a distinct proposition from the  original one, and saying that it's true is *technically not the same* as saying that the negated proposition is false.

Now then, whether we use the true-only tableaux or the tableaux with truth value annotations depends on what we're trying to do with our tableau proofs. If we're proving that a set of propositions is consistent/satisfiable, or that it's a tautology, then we can get away with the true-only version. If we want to check for contradictions, we can use annotated version as well.

So how might we use tableaux for these tasks? So far, tableaux are just fun little ways to ake use of syllogisms, which are themselves representations of reasoning patterns from truth tables.

The actual way to *use* a tableau for one of those tasks involves using *specific* transformations of the tableau, not just arbitrary syllogisms. The transformations we use for consistency/satisfiability and tautology are (related to) some of the ones we've seen already. Namely, we have the following:

1. If a path to a leaf node has a conjunction that has not been used yet in that path, extend that path with a box for each conjunct. The conjunction is now used in that path and cannot be reused in it.
2. If a path to a leaf node has a disjunction that has not been used yet in that path, extend the path with two boxes, one with each disjunct. The disjunction is now used in both those paths and cannot be reused in either of them.

We also need to explain how to handle negation, since we're making use of it in place of truth value assignments, and also negation is itself also a proposition we care about.

If we had truth value assignments, then how we'd handle negation is obvious: we simply add the negated proposition with the opposite truth value. E.g., if we have a tableau with `!A t` then we would add `A f` and if we had `!A f` we'd add `A t`. But instad we have to expand in other ways. For negated atomic propositions, we do nothing, but for compound propositions, we do the following:

1. If a path to a leaf node has a negated conjunction that has not been used yet in that path, extend that path with two boxes, one with each conjunct negated. The negated conjunction is now used in both those paths and cannot be reused in either of them.
2. If a path to a leaf node has a negated disjunction that has not been used yet in that path, extend that path with a box with both disjuncts negated. The negated disjunction is now used in that path and cannot be used again.
3. If a path to a leaf node has a negated negation that has not been used yet in that path, extend the path with a box containing the inner proposition. The double negation is now used in that path and cannot be used again.

Lets see how this looks. Consider the tableau

```
   -------------
  |  !(A & B )  |
   -------------
```

Since this is negated conjunction, we branch with negated conjuncts:

```
   -------------
  |  !(A & B )  |
   -------------
       /   \
   ----     -----
  | !A |   | !B  |
   ----     -----
```

In some sense, this is implicitly a proof relying on De Morgan's law that `!(A & B) = !A | !B`, and just omitting that disjunction.

Now similarly for negated disjunction:

```
   -------------
  |  !(A | B )  |
   -------------
```

becomes

```
   -------------
  |  !(A | B )  |
   -------------
         |
       ----
      | !A |
      | !B |
       ----
```

Again, this is as if we implicitly were doing a proof using De Morgan's other law `!(A | B) = !A & !B` and just omitting the intermediate conjunction.

Finally, double negation such as

```
   -------
  | !(!A) |
   -------
```

would become

```
   -------
  | !(!A) |
   -------
      |
     ---
    | A |
     ---
```

While proving stuff, we might come across a path to a leaf box that has both a proposition and its negation. If we do, we put a big X under that box and never work on it again. We treat that path as if it doesn't exist.

We now ought to talk about implication, but we'll sidestep it entirely by saying we'll treat it like syntactic sugar: `?X -> ?Y` is the same as `!(?X) | ?Y`, or at least it has the same inference patterns, and so whenever we see implication we can just swap it out and move on.

Now how do we know if a proposition is consistent/satisfiable? If we use the above four rules to use every proposition possible on every path, until each path is either X'ed out or has only (possibly-negated) atoms and used compound propositions. If at the end of this, any of the paths has no X, then it's satisfiable/consistent, and we can read the satisfying conditions off it by looking at the possibly-negated atom. A bare atom must be true, and a negated one false, and together that ives us the assignment of truth values to the atomic proposition that make that path true.

On the other hand, if there are no paths that were X'ed out, then all assignments of values to atomic propositions make the proposition true and it's a tautology. To check whether a set of propositions is contradictory (or if a proposition is a contradiction), simply apply these rules, and at the end if *all* paths are X'ed out, then it's a contradiction.