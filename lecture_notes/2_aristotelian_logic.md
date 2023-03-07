# Aristotelian Logic

As mentioned in the introduction, Aristotle's project was probably the first attempt to formally study logic and reasoning. The field of study that he gave rise to had aspects which look quite similar to modern logic, and some of the questions he asked are still asked of logic today. But in other respects, Aristotelian logic is quite peculiar and odd, with aspects that feel almost mystical in nature. There was inference, of course, but also an abundance of classification, naming patterns, making visual representations. Rather than feeling like a coherent and grounded study of logic, it feels very much like what it is: the first major step away from the informal argument of the time, influenced in no small part by Pythagorean mathematical mysticism.

The particular nature of the logic is peculiar relative to Boolean Logic. Rather than connectives like "and" and "or", Aristotelian Logic is more concerned with the relationships between categories or kinds of things, which is why it often uses the word "categorical". This difference emerges from the historical context that the logic grew out of. As mentioned previously, there were a lot of pundits and know-it-alls roaming around the Greek world at the time, especially Athens, claiming to have explanations for all the things. But which "all the things"? They weren't making claims about physical phenomena like the pre-Socratics, no. They were making grand claims about politics and society and morality. You see, Athens had just recently suffered a major defeat at the hands of the Spartans, then the Persian Wars took their toll, and Athenian society was thrown into doubt. They became quite pre-occupied with questions like, what makes a good society, what about the Spartans let them win, what is justice, why should people behave one way or another, etc. And so the Sophists were answering *these* questions, which are fundamentally questions about the relationships between sorts of things, relationships between categories -- societies vs. good societies, ways you should behave and ways you shouldn't, justices vs. injustice, and so forth. Boolean Logic can tell you about "and" and "or" but cannot tell you anything about how sorts of things relate to one another, and that's just the kind of question Athenians were most interested in.

## Argument, Validity, Soundness

The object of study in Aristotelian logic is, well, logic. But specifically, it's about logical arguments. That doesn't mean spats or disputes, at least not quite. In some sense, of course, it does, because the origin of this is genuinely in heated argument, but in this context, it means something very specific: a logical argument is a step by step process of reasoning that starts from some premises and draws a conclusion. Argument in this sense is not something that has to involve anyone other than the reasoner -- it's called an argument in the same way that one might say "my argument for XYZ". Indeed, one often makes use of logical argumentation for checking one's *own* thoughts rather than the thoughts of others or to convince others.

But what do we want to know about arguments? In the Aristotelian context, there are two major ideas that are of interest: validity and soundness. An argument is said to be valid just in case the truth of all the premises guarantees the truth of the conclusion. The guaranteeing part here is not some kind of causality, but rather just an observational thing. Validity is about what we know to be true and how we can expand our knowledge on the basis of prior knowldge, rather than about how truth is made.

The second part is soundness. Soundness is like validity in that it is a property of an argument. In fact, it's a subcase of validity: an argument is said to be sound just in case it is valid *and also* the premises are true. This is a subtle distinction, here. Validity does not mean anything is in fact true, nor does it assume it. An argument can be valid even if the premises are false and the conclusion is false. Soundness, on the other hand, requires more: it requires that the premises must be *true*, and therefore the conclusion must also be true.

Now, what good is this distinction? Why not just have one or the other? Well on the one hand, soundness matters because of course the point of an argument is often to determine or convince oneself of truths and it's no good reasoning all day if what you get out is that something *might* but true but it depends on things we don't know about. I want to know that I can make coffee because I'm sleepy, it makes no difference whether I *could* make coffee if this and that and the other thing but actually I can't make coffee, I want to know *that* I can.

But on the other hand, we also can make quite a lot of use of validity because it lets us reveal false assumptions or erroneous thinking. You might think that you've reasoned soundly about your coffee maker and you've done all the things to make the premises true and so now they are, and yet the coffee just isn't getting made, what's wrong? Well if you know that the premises were true and you had the ground coffee in the basket and the water in the tank and so on, then it must be that the reasoning about what was relevant to making coffee that was the problem! The argument must not have been valid, so now you can go and figure out what the missing premise was so you can make your coffee. Validity lets you *debug*.

## Catgorical Propositions and Terms

Before we can talk about arguments, we have to know what constitutes a part of an argument. That is to say, we mentioned premises and conclusions, but what sorts of things are these? We saw one kind of proposition when we looked at Boolean logic, the Boolean expression, but this isn't actually the kind of proposition that Aristotelian logic is concerned with. Instead, propositions called "categorical propositions" are the main interest. A categorical proposition is a proposition that is "about" categories, that is to say, kinds of things. The classic example of a category used in these propositions is "men" and "mortal", in the categorical proposition "all men are mortal". The words for categories in a categorical proposition are called terms. Unlike propositions, terms are neither true nor false.

The general shape of a categorical proposition is

```bnf
<categorical-proposition> ::= <quantifier> <term> <copula> <term>
<quantifier> ::= "all" | "every" | "each" | ...etc | "some" | "a" | "any" | ...etc
<copula> ::= "is" | "are" | "is not" | "are not"
<term> ::= "man" | "dog" | "tree" | "thing that is good" | "time when John goes to the store" | ...etc
```

The specific choice of quantifiers depends, but typically one finds use of just "all" and "some", which is how this note will phrase things, and similarly one typically finds just the copula "are", and this note will likewise only use that. The terms are exclusive nominal forms, which can lead to interesting paraphrases when translating from normal English into a categorical proposition. Sentences like "whenever John goes to the store, he buys cheese" have to become sentences like "all times when John goes to the store are times when he buys cheese". The benefit of this constraint, however, is that it makes it far easier to reason about things since the number of shapes a proposition can take is drastically reduced.

Within a proposition, you'll find two terms, one between the quantifier and the copula, and another after the copula. To distinguish them, they're given two distinct names. The term between the quantifier and copula is called the subject, while the term after the copula is the predicate.

There are therefore four specific categorical propositions we will concern ourselves with:

```
A: all <subject> are <predicate>
E: all <subject> are not <predicate>
I: some <subject> are <predicate>
O: some <subject> are not <predicate>
```

The letters before the propositions are their names[^1]. A sentence of the form `all <subject> are <predicate>` (or more conveniently, `all <S> are <P>`) is called an "A" type sentence. Naming things was very important to Aristotelian logicians.

[^1]: The names `A`, `E`, `I`, and `O` come from Latin, and were assigned to these forms of proposition by Roman and Medieval logicians working long after Aristotle was dead. `A` and `I` come from the first two vowels of the word "affirmo", meaning "I affirm", because they are sentences that affirm a truth. On the other hand, `E` and `O` come from the vowels of "nego", meaning "I deny", because they are sentences that deny or negate a truth.

## Squares of Opposition

At this point, one usually discusses what's called the Square of Opposition, or the Traditional Square of Opposition to distinguish it from the Modern Square of Opposition. The Square of Opposition, both in traditional and modern forms, is a diagram used to show the relationship between the four types of categorical proposition. It's arranged with one proposition type at each corner, and lines drawn between each pair, labelled with relationships, like so:

```
       A                                     E
all <S> are <P>  -----contrary-----  all <S> are not <P>
       |        \                  /         |
       |           \            /            |
       |              \      /               |
subalternation     contradiction       subalternation
       |              /      \               |
       |           /            \            |
       |        /                  \         |
some <S> are <P>  --subcontrary --  some <S> are not <P>
       I                                     O
```

The opposing corners of the square are joined by lines labeled "contradiction", which indicates that the pairs `A-O` and `E-I` have opposite truths. That is to say, if `all <S> are <P>` is true, then `some <S> are not <P>` is false, and vice versa, and also the same holds of `some <S> are <P>` and `all <S> are not <P>`.

The pairs joined by lines labeled "subalternation" are such that if the top proposition (`A` or `E`) is true, the bottom (`I` or `O`, respectively) is also true, and if the bottom one is false, the top is false. So if `all <S> are <P>` is true, then so is `some <S> are <P>`, and if `some <S> are <P>` is false, then so is `all <S> are <P>` Likewise for the E and O pair.

The pair `A-E` is linked by a line labeled contrary, which indicates that both cannot be true (but both might be false). Similarly, the pair `I-O` is linked by a line labeled subcontrary, which indicates that both cannot be false (but both might be true).

The relations above are all relations in the traditional square. The modern square lacks the vertical and horizontal relationships. This is because in the traditional context, `A` and `E` type sentences were expected to be used and make sense only when the subject did in fact apply to something. For instance, "all men are mortal" would not be said at all if there were no men. In a modern context, however, it's fine to use `A` and `E` sentences when the subjects apply to nothing, and because of that, the horizontal and vertical relationships of the square simply don't hold.

You might wonder, quite rightly, how it is that we're supposed to know this square is correct. I mean, I drew it, ok, fine, but I could've drawn anything. What makes it *true*? This is not something that really has a good answer. The only real answer anyone can give, because this is ultimately the truth of the matter, is that you just have to *feel* that they're true. Which is to say, the square of opposition doesn't represent some deep universal truth so much as it represents the intuitions you have about the meanings of these words. If you then go on to wonder what to do if different people have different intuitions, the answer is often go take a hike.

## Categorical Syllogisms

Categorical propositions are all good and well, but the only thing we can say about them from a logical perspective is whether they're true or false. That's not logic at all, not inference, that's just assertion. To infer, we need at least two propositions and to be able to ask about how the truth of one relates to the truth of the other. The Square of Opposition gives us some amount of that, but it's not all that useful. Once you pick a subject and predicate, you have four sentences and relations among them, and what use is that? Well, perhaps some, because you can use the square to decide when you can substitute one sentence for another. But in an Aristotelian context, true *inference* and *reasoning* is done by always relating three or more propositions in an argument.

Now, an argument can in principle have many premises and many conclusions. You'll often find them written like

```
Premise 1
Premise 2
Premise 3
Therefore, Conclusion 1
Therefore, Conclusion 2
Premise 4
Therefore Conclusion 3
etc.
```

The `therefore` part is often written with the symbol `∴`, as in

```
  Premise 1
  Premise 2
  Premise 3
∴ Conclusion 1
∴ Conclusion 2
  Premise 4
∴ Conclusion 3
```

And sometimes you'll find the "reasons" written in parentheses after the conclusions, as in

```
  Premise 1
  Premise 2
  Premise 3
∴ Conclusion 1 (because Premises 1 and 2)
∴ Conclusion 2 (because Premises 1 and 3)
  Premise 4
∴ Conclusion 3 (because Conclusion 1 and Premise 4)
```

Additionally, sometimes one sees all of the premises placed together and all of the conclusions placed together, separated by a line, instead of using symbols or the word "therefore":

```
Premise 1
Premise 2
Premise 3
Premise 4
------------
Conclusion 1
Conclusion 2
Conclusion 3
```

Whenever we're dealing with big arguments, however, it can be confusing to understand how and why the propositions relate to one another. Obviously, using reasons in parentheses is useful, but the visual clutter of it can be hard to cope with. As a result, a more convenient form for verifying arguments is frequently used whereby each inference step is isolated into an independent micro-argument. For instance, the above might be turned into three micro-arguments:

```
  Premise 1             Premise 1             Conclusion 1
  Premise 2             Premise 3             Premise 4
∴ Conclusion 1        ∴ Conclusion 2        ∴ Conclusion 3
```

This form lets us look at each piece in isolation, and check if it's valid, and then if all of the micro-arguments is valid, we know the whole argument is valid.

Such a micro-argument is called a "syllogism" or a categorical syllogism, and always consists of two premises and one conclusion.

## Major Terms and Minor Terms, Major Premises and Minor Premises

Because a syllogism has exactly three propositions in it, it has the shape

```
  <quantifier> <subject> <copula> <premise>
  <quantifier> <subject> <copula> <premise>
∴ <quantifier> <subject> <copula> <premise>
```

There are therefore three quantifiers, three copulas, and six terms. In in general, we can use six distinct terms, but having more than three distinct terms is useless because no inferences can be made at all. Similarly, having just one or two provides no *useful* inferences. So then, in general, exactly three terms are used, each proposition has two distinct terms, and each term is used in a distinct proposition. The subject of the conclusion is used in exactly one of the premises, the predicate of the conclusion is used in the other premise, and a third proposition is used in both premises. For instance,

```
  <quantifier> <A> <copula> <B>
  <quantifier> <B> <copula> <C>
∴ <quantifier> <A> <copula> <C>
```

Just as before when we named the terms in a proposition because of multiplicity, there are multiplicities here that we will name. The term which is the subject of the conclusion is called the "minor term", and the term that is the predicate of the conclusion is the "major term". The remaining term, which is only in the premises, is called the "middle term". Similarly, the premise that contains the major term is the "major premise", and the premise that contains the minor term is the "minor premise". A syllogism is in standard form when the major premise precedes the minor premise. Again, naming things was very important for Aristotelian logicians.

## Moods, Figures, and Inference

Because syllogisms have three propositions, and can be placed into standard form, we can say that any standard form syllogism can be uniquely identified structurally, that is to say, by its shape ignoring the choice of terms. By labelling each proposition with its type, a syllogism can be given a name. For instance, a syllogism of the form

```
  all <middle> are <major>
  some <minor> are not <middle>
∴ some <minor> are <middle>
```

is a syllogism of the shape `EOI`, because the major premise is type `E`, the minor premise is type `O`, and the conclusion is type `I`. The shape of a syllogism is called its "mood", so this is mood `EOI`. There are 4^3 = 64 moods.

Similarly, the middle term of the syllogism can be in one of two places for each premise:

```
  <quantifier> <middle> <copula> <major>
  <quantifier> <minor> <copula> <middle>
∴ <quantifier> <minor> <copula> <major>

  <quantifier> <major> <copula> <middle>
  <quantifier> <minor> <copula> <middle>
∴ <quantifier> <minor> <copula> <major>

  <quantifier> <middle> <copula> <major>
  <quantifier> <middle> <copula> <minor>
∴ <quantifier> <minor> <copula> <major>

  <quantifier> <major> <copula> <middle>
  <quantifier> <middle> <copula> <minor>
∴ <quantifier> <minor> <copula> <major>
```

These for choices are called figures, and from top to bottom they are figure 1, figure 2, figure 3, and figure 4.

Therefore, any proposition's shape can be uniquely determined by its mood and its figure together. The mood `EOI` syllogism from before is figure 1, and so we would call it `EOI-1`. There are, then, a total of 64*4 = 256 different unique shapes of syllogisms. Again, lots of interest in names.

We can categorize all 256 syllogisms by whether or not they are valid. For example, consider the form `AAA-1`, as exemplified by this famous syllogism:

```
  all men are mortal
  all people who are the famous Ancient Greek philosopher Socrates are men[^2]
∴ all people who are the famous Ancient Greek philosopher Socrates are mortal
```

[^2]: The usual form of this syllogism uses `Socrates is a man` for the minor premise, but to reason formally using Aristotle's techniques, we must put this sentence into correct form of a categorical proposition, hence the peculiarity.

This form of syllogism, `AAA-1`, is going to be valid no matter what the choice of terms.

```
  all <B> are <C>
  all <A> are <B>
∴ all <A> are <C>
```

Because of this, the traditional perspective on this is to say that this is a valid syllogism.

I say traditional, because it depends on the same assumptions about `all` sentences as the traditional square of opposition, in comparison to the modern square. In a modern setting, we make a finer distinction between validity: some syllogisms are *conditionally* valid, and some are *unconditionally* valid, and we say that only the unconditionally valid forms are "valid" with no modifier. Modern syllogisms are conditionally valid when certain of their terms hold of a non-zero number of things, just as how with the modern square of opposition some of the links between propositions didn't hold because they pre-supposed things about the terms in question.

There are 256 forms of syllogism, but very few of them are valid, either traditionally or modernly, so we can just list them.

The unconditionally valid forms, which are valid in both traditional and modern Aristotelian logic, number just 15, and they are

| Figure 1 | Figure 2 | Figure 3 | Figure 4 |
| -------- | -------- | -------- | -------- |
| AAA      | AEE      | AII      | AEE      |
| AII      | AOO      | EIO      | EIO      |
| EAE      | EAE      | IAI      | IAI      |
| EIO      | EIO      | OAO      |          |

The conditionally valid forms, which are valid only in traditional Aristotelian logic, number just 9, and they are

| Figure 1 | Figure 2 | Figure 3 | Figure 4 | Condition that makes them valid  |
| -------- | -------- | -------- | -------- | -------------------------------- |
| AAI      | AEO      |          | AEO      | Minor term applies to something  |
| EAO      | EAO      |          |          | ditto                            |
|          |          | AAI      | EAO      | Middle term applies to something |
|          |          | EAO      |          | ditto                            |
|          |          |          | AAI      | Major term applies to something  |

Any argument whatsoever, which is formed from only valid syllogisms, is a valid argument. You can have a million syllogisms, and as long as they each are one of these forms, the whole argument is guaranteed to be valid.

## Relation to Naive Set Theory

Categorical propositions and syllogisms may look to the astute reader like set theory, and indeed, they do have a nice relationship to naive set theory. Each term corresponds to the name of a set, and each categorical proposition corresponds to a proposition in naive set theory. The relationship is as follows:

| Categorical Proposition | Set Theoretic Proposition |
| ----------------------- | ------------------------- |
| `all ?S are ?P`         | `?S ⊆ ?P` or `?S∩?Pᶜ = ∅` |
| `all ?S are not ?P`     | `?S ⊆ ?Pᶜ` or `?S∩?P = ∅` |
| `some ?S are ?P`        | `?S∩?P != ∅`             |
| `some ?S are not ?P`    | `?S∩?Pᶜ != ∅`             |

It is sometimes useful to have a notation that means the same as `?S∩?P != ∅` but doesn't use equality or use the empty said. We shall instead write `?S ∩∩ ?P` with a double intersection symbol to mean this. Then, using only purely binary relations, our table simplifies to

| Categorical Proposition | Set Theoretic Proposition |
| ----------------------- | ------------------------- |
| `all ?S are ?P`         | `?S ⊆ ?P`                 |
| `all ?S are not ?P`     | `?S ⊆ ?Pᶜ`                |
| `some ?S are ?P`        | `?S ∩∩ ?P`                |
| `some ?S are not ?P`    | `?S ∩∩ ?Pᶜ`               |

We can restate any syllogism in these terms. For instance, the form `AAA-1` can be translated as follows:

```
  all ?M are ?P                 ?M ⊆ ?P
  all ?S are ?M    becomes      ?S ⊆ ?M
∴ all ?S are ?P               ∴ ?S ⊆ ?P
```

Similarly, `EIO-3` is translated as:

```
  all ?M are not ?P                  ?M ⊆ ?Pᶜ
  some ?M are ?S        becomes      ?M ∩∩ ?S
∴ some ?S are not ?P               ∴ ?S ∩∩ ?Pᶜ
````

## Conclusions for Aristotelian Logic

We've seen now the grammars of sentences and syllogisms, and the methods of reasoning with them. We've seen plenty of mysterious names that are perhaps useful but peculiar in their abundance. More can be said about all of this, looking at invalid forms, naming and classifying them, engaging in a kind of butterfly collecting of logical things. But we get no closer to really understanding logic.

One major reason is the secret subjectivity of it all. You may be wondering how we know that the valid syllogisms are indeed valid and the others are not. Again, this is a case where the whole logic is leaning very heavily on *intuition*, and if you have different intuitions, too bad. This is a little harsh, of course -- the standard way to evoke intuitions is to find an example of the syllogism in question where the premises are judged to be true and the conclusion is nevertheless judged to be false. So it's not as if the way you determine validity or invalidity is to sit around and feel your way towards that, you find counterexamples. But that still ultimately is reducing the validity to a judgment made by people, not by logic itself, and people *can and do* disagree about those judgments. The long history of logic in Europe has consisted predominantly of people insisting that only one set of judgments is "correct" and the others should be ignored as weird, wrong, insane, and so on, and it wasn't until much more recently that pluralism in logic began to emerge.

Aristotelian logic was fairly unchanged for literal millenia because of all of thise. In the end, it's more a historical curiosity than anything else. These days, we have better questions, and better methods of exploring answers. And we certainly have less blinders on about what kinds of questions.