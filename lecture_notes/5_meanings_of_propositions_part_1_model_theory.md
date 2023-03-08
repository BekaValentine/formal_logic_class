# Meanings of Propositions, Part 1: Model Theory

At this point, we've been working a lot in proof systems, and making lots of reference and appeal to Boolean evaluation of propositions into truth values. Everything we've done could be seen as just notation for Boolean logic and that's not entirely wrong. It could've all be invented in the 1800s and some of it probably was. But some time in the early 20th century, some interesting ideas emerged.

We saw in the note on Boolean Logic that one way to think about evaluating a proposition of that logic was by rewriting a proposition until we end up with either `t` or `f`. This rewriting approach can be traced back to, among other people, Emil Post. Post's rewriting systems are applicable to lots of things, not just logic but also grammars, games, computation, you name it. But in saying that, I'm presupposing that grammars, games, computation, etc. aren't logic. But why not? What demarcates the "logic" rewriting rules from the "game" rewriting rules? Another intimately related quandry is when can we prove a proposition? Another is *how* do we prove and how does calculation/computation relate to this?

The investigation of those questions are all incredibly interesting and we'll get to them in time, but before we do, we're going to tackle a deeper question, one that all of the above can be linked to and which, by looking at it first, helps to set the stage for those other questions. The question we will now turn to is this: What do propositions *mean*?

There are two main approaches to answering this question, model theoretic and proof theoretic. Roughly speaking, model theoretic approaches to meaning say that the meaning of a propositon is understood in relation to a mathematical model of some sort. Proof theoretic approaches, on the other hand, say that the meaning of a proposition is understood by the proofs that it participates in. This first note on the meaning of propositons will look at model theoretic approaches to meaning.

## Model Theory from 10,000 Feet

The high altitude view on model theory is this: we can understand the meanings of propositions by explaining how to translate them into some mathematical domain. Usually this is mathematical in the usual sense, but sometimes we also think about translating things into pure functional programs, because those are known to then translate into mathematical domains nicely.

But what is a mathematical domain? Well, if you're a Platonist, you think it's Plato's realm of forms or something, and if you're not a Platonist, you probably don't think that Model Theory is really much of an explanation of meaning anyway, just a tool for translating from one unexplained logic to another unexplained logic. Never the less, sometimes translations translations can be insightful even if they're not the end all be all of explaining meaning.

## Some Simple Model Theories for Propositional Logic WITHOUT Propositional Variables

To explain how model theory works, we shall look at constructing one for Propositional Logic. In fact, we've sort of already seen one when looking at how to evaluate Boolean Logic. So let's see how we talked about evaluation for Boolean Logic, and in particular, for the connectinve `&`. Repeating what we said previously:

> 4. Given an expression of the form `?X & ?Y`, if the value of `?X` is true and also the value of `?Y` is true, then the value of `?X & ?Y` is true, otherwise its value is false.

This contains within it enough to see what a very simple model theory looks like for Propositional Logic. We have some notion of value of a proposition, which in model theory would be called the "denotation" of the proposition, and some set of values that constitute valid values, in this case the values `{true, false}`. In particular, we can view this as a mechanism for translating a proposition into the domain of mathematics on those sets of values using functions into those values. Let's be explicit about this translation, and define define a function `I` which stands for "interpretation", which maps propositions to truth values.

The above clause corresponds to saying

```
I(?X & ?Y) = { true    if I(?X) = true and I(?Y) = true
             { false   otherwise
```

A very common alternative to writing `I(A)` and so on is to write `[[A]]`, or `〚A〛` in unicode. These so called "semantic brackets", which originated with Dana Scott (and are therefore sometimes called "Scott brackets"), are especially promenant in computer science and linguistic semantics. Sometimes one also sees `V(A)` or `V[A]` or variables like that, standing for "value". Here is the full definition of `I`, translating our previous meaning explanations into math:

```
       I(t) = true
       I(f) = false
   I(!(?X)) = { true    if I(?X) = false
              { false   otherwise
 I(?X & ?Y) = { true    if I(?X) = true and I(?Y) = true
              { false   otherwise
 I(?X | ?Y) = { false   if I(?X) = false and I(?Y) = false
              { true    otherwise
I(?X -> ?Y) = { false   if I(?X) = true and I(?Y) = false
              { true    otherwise
```

This particular model theory for Propositional Logic therefore consists of a set that is the "model" of propositions, and a function `I` that maps from the syntax into the model. This is a denotational model theory. If we wish to make a deeper connection to the truth tables, we can now do so as follows: observe that a truth table written using actual truth values, rather than using the conflated `t` and `f` notation, defines a binary function on the set `{true, false}`. For instance, consider this truth table:

| ?X    | ?Y    | ?X & ?Y |
| ----- | ----- | ------- |
| false | false | false   |
| false | true  | false   |
| true  | false | false   |
| true  | true  | true    |

This is very definitiely a function, mapping `{true, false}⨯{true, false}` to `{true, false}`. As such, we can name it, so let's call it `c`, mnemonic for conjunction. Similarly for `d` that is the truth table for disjunction, `i` for implication, `n` for negation. Then:

```
       I(t) = true
       I(f) = false
   I(!(?X)) = n(I(?X))
 I(?X & ?Y) = c(I(?X), I(?Y))
 I(?X | ?Y) = d(I(?X), I(?Y))
I(?X -> ?Y) = i(I(?X), I(?Y))
```

This particular flavor, sometimes called an algebraic semantics, is especially appealing at times, because, as we'll see later, we can often characterize a collection of *logical* connectives by relating them to collections of *mathematical functions*, and such collections are normally called *abstract algebras*.

Another flavor of model theory, more like what Tarski would have given when he invented model theory, is to define a metalinguistic judgment of propositions, which we'll write `!= A` and which in unicode would be written `⊨ A`. This can be read as "it's true that `A`", or things to that effect. We also generally will have its negation `!/= A` (`⊭ A`), which might be read as "it's not true that `A`" or "it is false that `A`", and so on. In this setting, we do not have "values" per say, but rather we just say that a proposition "is true" or "is false". The equivalent statement of the meanings of propositions in this form would be

```
1. != t.
2. !/= f.
3. != ?X & ?Y  iff != ?X and != ?Y.
4. != ?X | ?Y  iff != ?X or != ?Y.
5. != ?X -> ?Y iff !/= ?X or != ?Y.
```

As noted in the title of this section, these little model theoretic semanticses all give meanings for propositions that lack propositional variables. That is to say, we had nothing to say about propositions like `Worf drinks prune juice`, or more abstractly, `A`. Instead we only had the atomic propositions `t` and `f`, and compound propositions built out of those. These are also only a few of the options for how we might translate from logic into mathematics, any number of other options exist.

## Some Simple Model Theories for Propositional Logic WITH Propositional Variables

To handle propositional variables, we'll add extra stuff to our models. For the first kind of model, a denotational semantics, we will augment our function `I` with explanations for the value of atomic variables. For instance, if `A` is true, then our definition of `I` now needs to have a clause `I(A) = true`, and so forth. This can be tedious, so an alternative to doing this is to parameterize `I` by a set of propositional variables `V`, written as a superscript, and a general all-encompassing rule for propositional variables:

```
I^V(?P) = { true   if ?P in V
          { false  otherwise
```

with the caveat that this is only usable precisely when `?P` is an a propositional variable.

For an algebraic semantics, the same would hold, or we could instead add another function specifically for assigning values to propositional variables, call it `v` for variable, and add

```
I(?P) = v(?P) (assuming ?P is a propositional variable)
```

Finally, for the Tarski-style model theory, we would write `V != A` instead of just `!= A`, and likewise `V !/= A` instead of just `!/= A`. We would augment our rules by placing `V` uniformly into the position before the turnstile-like symbol, and then add a new clause:

```
V != ?P iff ?P is in V (assuming ?P is a propositional variable)
```


## Models as Objects of Inquiry

In the first kind of model theory, for variable-less propositional logic, the semantic domain `{true,false}` is sometimes called the model. In the augmented kind of model theory that can treat propositional variables too, one sometimes finds `V` called the model, or `V` together with the semantic domain `{true,false}` is the model. For the algebraic varieties, usually the functions are also considered part of the model.

This then lets us describe the models abstractly. Let's consider the algebraic sort only, because it's especially interesting here:

An algebraic model `M` is a tuple consisting of...

- A set of values `D = {true, false}`
- An element `tt` in `D` (`true`)
- An element `ff` in `D` (`false`)
- A function `n : D → D` (the negation truth table)
- A function `c : D⨯D → D` (the conjunction truth table)
- A function `d : D⨯D → D` (the disjunction truth table)
- A function `i : D⨯D → D` (the implication truth table)
- A function `v : PropositionalVariable → D` (if we have propositional variables) 

We can now abstract over `D`, and say instead that an algebraic model `M` is a tuple of...

- A set of values `D`
- An element `tt` in `D`
- An element `ff` in `D`
- A function `n : D → D`
- A function `c : D⨯D → D`
- A function `d : D⨯D → D`
- A function `i : D⨯D → D`
- A function `v : PropositionalVariable → D` (if we have propositional variables)
- 
We might then wish to place some constraints on these models, or not. If not, then these are then "models" of Propositional Logic in only the most rudimentary of senses: they have the right "shapes" for the syntax translation but that's all.

Typically, one adds the constraint that `(D,tt,ff,n,c,d,i)` constitutes a Boolean algebra and that there is some ordering relation that therefore obtains which normally would be written `<=` or variations thereof.

We say that a model `M` models/proves a proposition `A`, `M != A` iff `ff < I^M(A) <=  tt`. The model-indexed `I` is just the version of `I` from above, but using the specific oprations from the model rather than the specific Boolean truth functions discussed earlier. We will omit the superscript `M` when it's obvious which model is intended.


Ideally, we would like to constrain ourselves a bit more and talk about the relationship between these model-ish things, and the logic we care about. In particular, model theory asks us to consider the questions

1. If `!- ?X` is provable, is `ff < I(?X) <= tt`? What about `!- ?X` being unprovable? Does that mean `I(?X) = ff`?
2. If `ff < I(?X) <= tt`, is `!- ?X` provable? What about if `I(?X) = ff`, is `!- ?X` unprovable?

When the first question is answered yes -- that is to say, if a proposition is provable, it's meaning is `tt` in the model, and `ff` otherwise -- then we say that the logic is "sound" with respect to the model. When the second question is answered yes -- that all and only `tt`-valued propositions are provable -- the logic is said to be "complete" w.r.t. the model.

In general, Model Theory strives to find models for which a given logic is sound, and completeness is a nice but not necessary benefit. We can often find models for which the logic is not complete, but still we call them models for the logic. On the other hand, when we have a model for which the logic is unsound, we often will not even say it's a model for the logic. We will instead say it's just not a model for it at all and that the models are something else entirely.

It turns out that for Propositional Logic as we have been describing it, the algebraic model we gave above, with `D = {true,false}`, is a special case of a more general structure -- the Boolean Algebra -- for which the Propositional Logic we've been using is sound. Another instance of a Boolean Algebra for which Propositional Logic is sound is powersets of a chosen set. Let's look at that next.

## Powerset Models

Suppose we have a designated set `U`, for "universe". It can be any set you like, take your pick. We can define a model for Propositional logic in terms of `U` as follows:

- `D = P(U)` (the powerset of `U`, i.e. the set of subsets of `U`)
- `tt = U`
- `ff = ∅`
- `n(X) = U\X` (the complement of `X` in `U`)
- `c(X,Y) = X ∩ Y`
- `d(X,Y) = X ∪ Y`
- `i(X,Y) = n(d(n(X),Y)) = U\((U\X) ∪ Y)`
- `V` is some arbitrary function mapping propositional variabls to `D`

This is indeed a Boolean Lattice and the ordering relation is `⊆`. The definition of `M != A` as `ff < I(A) <= tt` becomes `∅ ⊂ I(A) ⊆ U`, which is just to say that `I(A)` is non-empty.

This too is a perfectly coherent model for Propositional Logic. Not only is Propositional Logic as we've described it so far sound w.r.t. the powerset model, it's alsos *complete*: any equation over sets built from a owerset model's functions will be provable with the Classical Propositional Logic that we've been discussing so far. I really should emphasize the "classical" here, because there are variations of Propositional Logic that we will soon look at for which this isn't true.

## Kripke Models

Another kind of model for the Propositional Logic is one which is very similar to the Powerset Model but subtlely different as well. It's a variation of the non-algebraic kinds of models mentioned above, but still using sets in curious ways. Namely, they are Kripke Models, invented by philosopher Saul Kripke for model logics.

A Kripke model for Propositional Logic consists of a set `W`, for "worlds", and a binary relation `S` that relates worlds to propositional variables (that is to say, `S ⊆ W⨯PropositionalVariable`). We define now an auxiliary relation, written `!!-` (unicode `⊩`), that relates worlds to general propositions (`w !!- A` is read "`w` satisfies `A`"), and also implicitly its denial, `!!/-` (unicode `⊮`):

```
?w !!- ?P         iff   S(?w,?P)  (if ?P is a propositional variable)
?w !!- t
?w !!/- f
?w !!- !(?X)      iff   ?w !!/- ?X
?w !!- ?X & ?Y    iff   ?w !!- ?X and ?w !!- ?Y
?w !!- ?X | ?Y    iff   ?w !!- ?X or ?w !!- ?Y
?w !!- ?X -> ?Y   iff   ?w !!/- ?X or ?w !!- ?Y
```

We then say that a model `M` that is to say the pair `(W,S)`, proves `A`, `M != A` iff there is some world `w` in `W` for which `w !!-^M A`, where `!!-^M` is meant to indicate the relation `!!-` for this specific model.

This class of models -- Kripke models -- are intimately related to powerst models. In particular, the a powerset model `(U,V)` can be turned into a Kripke model by defining `W = D\∅ = P(U)\∅` and `S(w,A) iff w ⊆ V(A)`. It can then be shown that `w !!- A` holds if and only if `w ⊆ I(A)` in the powerset model, and so `(W,S) != A` iff there is some `w in D` such that `w !!- A` ie `w ⊆ I(A)`. We know that `w` cannot be the empty set because of the definition of `W`, so if there is such a `w`, it is a non-empty set such that the powerst definition of satisfation, as `I(A)` is non-empty, necessarily holds, because `w` is non-empty, and is a subset of `I(A)`, so `I(A)` must be non-empty. Therefore the powerset model gives rise to an equivalent powerset model.

## Proving Soundness and Completeness

How might we go about proving that Propositional Logic is sound and complete w.r.t. the above models? Well, first, we really need to pin down precisely what Propositional Logic is. We've seen quite a lot of proof systems, and ways of reasoning that relate to truth tables, but the truth tables have now been revealed to actually be more of a semantic notion than an inferential one. So what defines the *proof system* in isolation of the model theory? A set of axioms! Or more precisely, a set of axiom schemas. Or at least that's one formulation. A more congenial sort is a set of syllogisms/inference rules. This seems perhaps a bit backward -- we previously derived the inference rules from the truth tables. But in reality, what we were secretly doing was defining a set of inference rules that are sound and complete w.r.t. specific parts of a model theory.

So then, in modern logic, what we do is give a set of inference rules for Propositional Logic without reference to truth tables at all, and then prove that they're sound and complete with respect to truth tables/Boolean Algebras/etc, afterwards. The inference system stands on its own terms, and is justified by showing that it can relate to specific models.

How do we do this exactly? We want to prove that the totality of rules is sound and complete with respect to the models we mentioned. To do this, we typically do this in a number of phases. The first phase is to prove that each inference rule is sound and complete w.r.t. the models -- by which we mean that when we have a proof that uses the inference rule, the corresponding model theoretic statement holds, and vice versa. Then we'll see if we can compose these into a large proof of soundness and completeness for the entire logic.

The general shape of a soundness proof for an inference rule is that for a rule that look like

```
   A ...
 ---------- rule
 OP(A, ...)  
```

Where `I(OP(...)) = op(I(...), ...)`, it must also be the case that when there exists actual *proofs* using this rule

```
    :
    : P
    :
    A ...
  ---------- rule
  OP(A, ...)
```

there is a corresponding statement about the model which is true. For the simplest Boolean Algebra model we saw -- Boole's own algebra of truth values -- the statement is that when there exists such proofs using the rule, `I(OP(A,...)) = op(I(A), ...) = true`. That is to say, if we can construct a proof that makes use of this rule, then the proposition that concludes it has the value `true`. How might we go about showing this in practice? For conjunction it looks like this:

Let's look at soundness for the conjunction syllogism. Suppose we have a valid proof that ends with Conjunction, like so:

```
:      :
: P    : Q
:      :
A      B
-------- conj
 A & B
```

We need to show that `I(A & B) = c(I(A), I(B)) = true`. The first part of this equation, `I(A & B) = c(I(A), (I(B)))`, is trivial, because that's part of the definition of `I`, so we're off the hook there. But the second part, `c(I(A), I(B))` is a little harder. The definition of the conjunction truth function returns true only when the arguments are both equal to true, and so if `c(I(A), I(B)) = true`, it must also be the case that `I(A) = true` and `I(B) = true`. Can we convince ourselves of this?

Now, I want to be very clear here with what's going on. I do not mean is it the case *given this specific proof*, can we do this. We may well be able to do so. For instance, here's one proof of this shape that makes this trivial:

```
---   ---
 t     t
 ------- conj
  t & t
```

It's defintely the case that `I(t) = true`, and so the equation that `c(I(t), I(t)) = true` is the same as `c(true, true) = true`. So in this one case, when the proof exists, it's also true that the proposition is interpreted to true in the model. And conversely as well. But What we need to show is that this is going to hold in general, of all such proofs. The question is, given that `A` and `B` above could be *any* propositions, and `P` and `Q` could be *any* proofs of them, can we in general convince ourselves that `I(A) = true` and `I(B) = true`, just from the fact that `P` and `Q` are themselves valid proofs?

And the answer to this is, well, maybe. Assuming that we allow ourselves to be convinced by inductive arguments at this level of meta-logical reasoning. But the details of this are actually not obvious at all. And in fact, coming up with them is hard enough that it took entire PhD dissertations worth of work to figure out how to do. We'll return to this later.