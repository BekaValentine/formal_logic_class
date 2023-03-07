# Proof Trees for Propositional Logic

We saw in the last, rather long, note that there were a variety of proof methods we can use to do proofs about propositional logic and that they were especially well suited to different sorts of questions about propositions. Fitch style let us draw conclusions very nicely, including ones involving assumptions via conditional proofs. Tableaux let us analyze satisfiability, tautology, and contradiction conveniently. These particular proof methods can be used for all sorts of forms of logic, not just propositional logic, and so it's worth having at least some familiarity with them.

But as we look further into logic, and in particular at proof theory, we'll want to make use of different notations, because those notations are somewhat hard to extend into other logics. Again, not impossible, but some logics, such as modal logics and substructural logics, really require the logician to twist themselves into knots figuring out how to make Fitch or tabeleau proofs work.

So in this note, we'll look at two closely relatd proof systems that employ tree shaped proofs, and from this note onward, all our proofs will be in one of these two styles.

## Basic Proof Trees

Let us look at some arguments/proofs that we can make using our propositional syllogisms. For instane, here is a proof that `A & B` entails `B & A`:

```
    A & B
  ∴ A

    A & B
  ∴ B

    B
    A
  ∴ B & A
```

Or using our more tidy notation:

```
    A & B
  ∴ A
  ∴ B
  ∴ B & A
```

And with numbers and reasons:

```
1. A & B
2. A      (1, simp)
3. B      (2, simp)
4. B & A  (3, 2, conj)
```

This notation is nice for short-ish proofs, but when the proofs get longer, or really, when a single premise has to be used twice in very long sub-proofs, it can be inconvenient, because the inference rules can reference previous propositions that are quite far away spatially. I mean, you could have a proof with a thousand lines and then on line 1001, you need to use proposition 1 and proposition 1000 and that's a lot of paging back and forth you're gonna be doing!

So an alternative approach is to notice that our reasons, which are on the right, contain both the name of a syllogism *and* the lines of the proposition that need to be referenced. In a sense, then, this describes a kind of graph. Our proof above sort of is like this directed graph here, where edges are inferences pointing from conclusion to premise:

```
  A & B
   ^ ^
  /   \
B       A
 ^     ^
  \   /
  B & A
```

Or alternatively we could say this is a tree, and just duplicate the top node:

```
A & B   A & B
  ^       ^
  |       |
  B       A
   ^     ^
    \   /
    B ^ A
```

This is pretty good at conveyig the ways the propsitions relate, but we don't have the reasons, so lets put syllogism names back in, this time on the right of conclusions:

```
A & B          A & B
  ^              ^
  |              |
  B (simp)       A (simp)
   ^             ^
     \         /
        B ^ A (conj)
```

This is a proof tree! Well, ok, the usual notatien is different. Instead of drawing actual arrows from conclusion up to premise, we simply separate a conclusion from premises by a horizontal like, and label the line with the syllogism (often on the right but sometimes on the left):

```
A & B         A & B
----- simp    ----- simp
  B             A
  --------------- conj
       B & A
```

In this kind of proof, the premises are at the leaves, which are at the top of the tree. You can tell they're premises because there's no line above them indicating that they're the conclusions of rules. Another word for these in the context of treating them as having *unknown* truth values is that they're assumptions, or hypotheses.

Let's look at some of the previous named syllogisms in this notation:

```
?X -> ?Y    ?Y -> ?Z
-------------------- (Pure) Hypothetical Syllogism
      ?X -> ?Z

?X -> ?Y    ?X
-------------- Modus Ponens
      ?Y

?X -> ?Y    !(?Y)
----------------- Modus Tollens
     !(?X)

(?X -> ?Y) & (?Z -> ?W)    ?X | ?Z
---------------------------------- Constructive Dilemma
             ?Y | ?W

(?X -> ?Y) & (?Z -> ?W)    !(?Y) | !(?W)
---------------------------------------- Destructive Dilemma
              !(?X) | !(?Z)

  ?X
------- Addition (on the left, similarly for on the right)
?X | ?Y

?X & ?Y
------- Simplification (on the left, seen before, similarly for on the right)
  ?X

?X    ?Y
-------- Conjunction
?X & ?Y
```

This notation also has a means of handling conditional proofs, which in this context are actually called hypothetical proofs. We saw before, with Fitch style, that conditional proofs conclude with an implication. With tree proofs, we are more generous and say that we'll conclude with whatever we like so long as its justified by the truth tables. We'll write these by treating hypotheses in a hypothetical proof as if they are the conclusions of inference rules, but the names of the rules are invented on the spot. For instance, here's a hypothetical proof from `A & B` to `A`:

```
----- 1
A & B
----- simp
  A
```

I named the phony rule here `1`, but we could just as well call it `x` or `foo` or whatever. Now, the conditional proof rule in Fitch would here be a rule that extends the *root* of the tree, and which has a label that *mentions* the hypothesis that's being discharged:

```
   ----- 1
   A & B
   ----- simp
     A
------------ cp(1)
(A & B) -> A
```

Before we used the conditional proof rule on this, discharging hypothesis 1, we would say that the proof tree has a single hypothesis (namely, 1), and after we used th conditional proof, we would say that the tree has zero hypotheses.

Another thing to note is that we can use a single discharging rule to discharge two *occurences* of a proposition. This is a situation where the second notation is ideally suited, because it lets us decide whether we're discharging one, or more, at discharge time rather than when we initially write them.

For example, our proof above that goes from `A & B` to `B & A` can be used to prove both `(A & B) -> (B & A)`and also to prove `(A & B) -> ((A & B) -> (B & A))`. Here are proofs. First, the first:

```
----- 1       ----- 1
A & B         A & B
----- simp    ----- simp
  B             A
  --------------- conj
       B & A
------------------ cp(1)
(A & B) -> (B & A)
```

And second, the second:

```
      ----- 1       ----- 2
      A & B         A & B
      ----- simp    ----- simp
        B             A
        --------------- conj
             B & A
      ------------------ cp(1)
      (A & B) -> (B & A)
------------------------------- cp(2)
(A & B) -> ((A & B) -> (B & A))
```

In fact there are a few alternative routes to this same conclusion, using different hypotheses for different premises of the `conj` rule, and discharging them in different orders. And in fact we can swap out `A` for any other proposition in the hypothesis 1 and still get a valid proof, and similarly for `B` in hypothesis 2, which is not the case for the single-hypothesis proof.

Finally, note that it is fine to also discharge a hypothesis that is not actually explicitly written anywhere and also not used for anything. This is analogous to a Fitch style proof where we simply just have extra hypotheses in a conditional proof that go unused in actual reasoning.

## Weird Hypothesis Discharge

The notation of hypotheses and discharging can lead to some weird situations, and some of them  actually don't correspond to any of our truth-table-based patterns of inference. For instance, if a hypothesis is discharged twice, that's a little fishy, but it's technially not too bad because we could always have discharged a second identical hypothesis. Thats weird and is definitely confusing notation to avoid, but it's inferentially ok. But worse is to discharge hypotheses in strang places. For instance, consider this wonky proof tree:

```
--- 1
  A
------ cp(1)  --- 1
A -> A         A
---------------- mp
        A
```

This proof seemingly lets us conclude `A` with no undischarged hypothesis, right? But `A` could be replaced by anything at all, even false proposition. Somethings fishy here and not in the ultimately-ok way like with multiple discharges of a single hypothesis.

The problem is, the hypothesis is discharged by the conditional proof that concludes `a -> A`, but then in some other part of the tree, we use the hypothesis again! If we allow that kind of proof, we always can prove weird invalid things. If instead we say that a hypothesis can only be used in the tree above its discharging inference, and nowhere else, then we recover only valid inferences.

Put it another way, every time we have a hypothesis that is labeled so as to indicate how it links up with a discharging inference, that inference has to be *below* in on the way to the root of the tree. It cannot be off to the side on some other branch of the proof.

## Hypothesis vs. Premise

This notation requires that we look around the proof tree to find the discharging rule in order to say that the hypothesis has indeed be discharged. A common alternative is to leave the hypothesis unadorned by a label and line, and instead only add it when we discharge it. We would then start with

```
A & B
----- simp
  A
```

and only by discharging mark it:

```
   ----- 1
   A & B
   ----- simp
     A
------------ cp(1)
(A & B) -> A
```

This lets is see the undischarged hypotheses easily. But it also means that we don't have a way of distinguishing between premises which we take to be true for unspecified reasons, and hypotheses which we don't know to be true but which we want to assume are true temporarilly in the course of proving something. That distinction is often made simply by putting some framing text explaining when something is proven elsewhere, but if you *really really really* want notation in the proof itself, then you treat the premise like it's the conclusion of an inference rule and you label it with the reason why you think its true. For instance:

```
----- because John told me so
A & B
----- simpl
  A
```

Actually more commonly, you'll find labels like "lemma 5" which refers to some proof done elsewhere. But sometimes it's indeed the case that you just take some propositions to be true for non-logical reasons and that's that.

## Hypothetical Proofs But Better

The previous proof trees suffer from one big flaw: hypotheses are strewn about everywhere, they can magically appear when discharged, they can be repeated any number of types and treated as copies or not. It's sort of a mess. A convenient mess, to be sure! But still a bit of a mess. It works "fine" if you imagine yourself working top down, as if drawing conclusions from hypotheses and ultimately ending in a single big tree. But otherwise it's kind of bad.

And so there is an improvement on this that one finds: we make the assumptions tag along!

Rather than premises and conclusions being bare propositions, we instead say that a premise or conclusion is a *pair* of one hypothesis, and a list of conlusions. Usually this is written `G !- A` where `G` is the list of hypotheses and `A` is the proposition. With unicode, this would actually be more like `Γ ⊢ A` with profuse use of Greek symbols but these notes will stick with `G !- A` style. This is often read as "`G` entails `A`" or "`G` proves `A`" or "from `G` one an prove `A`". We call the form `G !- A` a "hypothetical judgement", though other names may also be found. The symbol `!-` is called turnstile, presumably because it looks a little like a turnstile.

The simplest rule relating to hypothetical judgments is simply to say that if our list of hypotheses contains a proposition, then that proposition is proven "by hypothesis":

```
------ hyp (A is in G)
G !- A 
```

The stuff in parenthesis is a condition on the use of the rule. We could alternatively complicate things by adding other judgments beyond the hypothetical one tht let us explicitly show that `A` is in fact in `G` but we'll use this notation here. The condition isn't actually written in proofs, its only written in the definition of the method of proof by hypothesis here.

We also might want to discuss rules relating to the list of hypotheses. For instance, it's certainly true just by the hypothesis rule that `A, B !- A` and also `B, A !- A`, so the order doesn't matter for hypotheses. The same is true for duplication, or the addition of more hypotheses. But that's just for the concluding of a hypothesis -- `A` in thi case. What if we concluded a conjunctin? Is it the case that `A, B !- A&B` is th same as `B, A !- A&B`? These are very good questions to be asking, because they motivate some deep insights, but those are things we will look at later.

Let's now annotate some of our syllogisms with hypotheses. Let's start with simplification:

```
?G !- ?X & ?Y
------------- simp
  ?G !- ?X
```

This is nice. If we can prove `?X & ?Y` from the assumptions `?G`, then we can prove `?Y` from those same assumptions. Convenient!

But if we look at the conjunction syllogism, we have an intereting question: we're going to have multiple lists of hypotheses in the premises. Do we write use the sameone everywhere like this:

```
?G !- ?X    ?G !- ?Y
-------------------- conj
   ?G !- ?X & ?Y
```

Or maybe we write two different ones and fuse them togther somehow?

```
?G1 !- ?X    ?G2 !- ?B
---------------------- conj
  ?G1,?G2 !- ?X & ?Y
```

Or maybe some third thing? Well it turns out that these are all very interesting questions later on, but in the version of Propositional Logic that we're looking at here, the one that captures Boolean Logic and truth tables, the choice doesn't matter either way. So we'll just pick the first one since it's less to keep track of. We'll repeat this pattern for other rules too.

Here's addition:

```
?G !- ?X
------------- addition
?G !- ?X | ?Y
```

And modus ponens:

```
?G !- ?X -> ?Y    ?G !- ?X
-------------------------- mp
         ?G !- ?Y
```

And now lets tackle conditional proof, since this will really show off the beauty of the hypothetical judgment:

```
 ?G, ?X !- ?Y
-------------- cp
?G !- ?X -> ?Y
```

Loo at that! all the hypothese relevant are to the left of the turnstile and so we can see at once what hypotheses are able to be discharged, and also we can see *that* we're disharging it because it vanishe from the list of hypothesis.

One final note: the problem of weird use of hypotheses becomes trivial to deal with when using hypothetical judgments: because the hypotheses are only usable when they're in the list of hypotheses, then all uses of a hypothesis will be ok. Any time the list of hypotheses and loses one or more hypotheses in the downward direction, it's because a specific rule of inference manipulates the list of hypotheses and *discharges* the now absent ones. Lets look at the wonky proof in this setting to see this in action:

```
 ------ hyp
 A !- A
--------- cp
!- A -> A     G1 !- A
--------------------- mp
        G2 !- A
```

What could `G1` and `G2` actually be? What list of propositions? Well if they're both the empty list, we would get

```
 ------ hyp
 A !- A
--------- cp
!- A -> A     !- A
------------------ mp
       !- A
```

The tree is incompletee, we still have to prove `!- A` on the right, but that's obviously a problem because we don't *have* a proof of `!- A`. In fact, it's the *conclusion* of this whole thing!

Alternatively, we could say that `G1` and `G2` were something else, maybe both are the list consisting of just `A`. That's fine, we can then use hypothesis to prove the right branch:

```
 ------ hyp
 A !- A
--------- cp   ------ hyp
!- A -> A      A !- A
--------------------- mp
        A !- A
```

But now we're not using modus ponens correctly becaus the hypotheses on the premises differ. We ould make them the same, but then we have a different conclusion:

```
 --------- hyp
 A, A !- A
----------- cp   ------ hyp
A !- A -> A      A !- A
----------------------- mp
          A !- A
```

We proved that `A` holds, but only if we have the hypothesis `A` to begin with, which isn't what we were trying to prove. So it looks like we just can't make the wonky proof with strange hypothesis discharges correspond to any valid proofs using hypothetical judgements. At best we can construct some vaguely similar looking proofs, but they all prove rather boring entailments that need hypotheses, rather than than being able to just prove anything with no assumptions. And in the special case where `A` is actually the false proposition `F`, which should not be provable at all, well the only way to prove it is to assume it, so we don't actually have a real proof of `F`. We're safe from weirdness!