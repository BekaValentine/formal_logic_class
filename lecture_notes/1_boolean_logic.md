# Boolean Logic

Most computery types know something of Boolean Logic, even if they don't know it under that name. Lots of folks have heard about logic gates, many programmers use logical operators and boolean expressions[^0]. The gist of it is very widely know. The specifics slightly less so, and so we'll go over it in depth to have common ground.

[^0]: In Boolean Logic, we call these things expressions as well as propositions, formulas, sentences, statements, sometimes terms. In more interesting logics, the terminology will shift around, and we'll only use some of these words.

## Boolean Values

Boolean Logic can be described as a value-oriented logic. This isn't really a term of art, it's just a way to say that Boolean Logic is a logic that focuses very heavily on the values. Not values in the moral sense, but in the programming sense -- the value of expressions in a language. For Boolean Logic, those values are true and false, or if you're very computery, you might say 1 and 0, or if you like electronics, on and off. I'll use true and false, or T and F, but you can pick your favorite.

Boolean Logic is about those two values, usually called The Booleans, and on operations on them. One of the simplest interesting operations is the "not" operation, which takes a single boolean and gives you back a single boolean. Seen as a mathematical function, it is defined as

```haskell
not(true) = false
not(false) = true
```

The usual notation for this in formal logic is different, and we'll have a table of common notations below, but for now we'll use this mathematical function notation.

Some other operators are "and" and "or" and "implies" aka "if ... then ...". In computer science, "xor", "nor", and "nand" are also pretty popular, as is "if and only if" (aka "iff" aka "equals").

## Expressions of Boolean Logic

If the purpose of a logic is to reason about things, it seems pretty difficult to use this to reason. I mean, what are we reasoning about? Some abstract symbols? What use is that!

To actually make use of Boolean Logic as a tool of reasoning, we have to develop a sense of what the expressions of Boolean Logic are, as a language, and how to make use of them. While the logic is oriented towards values and operators, we need a little more than just that. So what else? Well, expressions! Or really, sentences. Really, really, we need atomic sentences. Boolean Logic gives us a vocabulary and grammar for expressing certain things, by way of symbolic representations of booleans and operators on them, but also a vocabulary for talking about things outsid the scope of the logic itself.

Consider for instance the sentence "Picard drinks Earl Grey". There might be some sense in which we want to analyze this from a logical perspective, but we can also say that this is just an atomic sentence that we're not going to analyze at all, we're merely going to use it. Another similar sentence might be "Worf drinks prune juice", which we similarly might analyze, or not and simply use. Now consider the compound sentence "Picard drinks Earl Grey and Worf drinks prune juice". Clearly this sentence is related to the previous two. For one, its got a lot of the same words in the same relative orders and proximity to one another, and the meanings feel related somehow. And moreover, we can ascribe a property of truth or falsity to thes three sentences, and the truth or falsity of them seems to be related.

Boolean Logic gives us a means to do this. In Boolean Logic, both sentnces "Picard drinks Earl Grey" and "Worf drinks prune juice" can be treated as atomic sentences -- atomic because we don't break them down further, like the atoms of Heraclitus (but not the atoms of modern physics which turn out to not be physical atoms at all). And we can combine these two sentences to make a bigger *compound* sentence by using a logical operator, conveniently named after a word of English: the "and" operator:

```haskell
and("Picard drinks Earl Grey", "Worf drinks prune juice")
```

When we say that we ascribe truth or falsity to these sentences, what we mean is that these sentences can be assigned a "truth value" or a boolean value: to say "Picard drinks Earl Grey" is a true sentence is just to say that it's boolean value is true (or 1, or on). And so that's why we also then can use the logical operator "and" on them: they have boolean values, and so an operator that works on boolean values should be usable on them.

I want to be precise here about what it means for something to have a boolean value, because to some degree it's not obvious what that means. And actually the subtleties here can arise later as interesting subjects of study. When I say that something has a boolean value, I mean both that we have agreed for the purposes of the reasoning to say that they have some value or other, and also that when we use the sentence in an expression/formula of Boolan Logic, we can treat the sentence as if it *was* the value. For instance, if the two sentences above both have the value true, then in som sense we want to say that the compound sentence is "the same as" the compound sentence `and(true, true)`.

We do this usually because we'd like to actually use the *logic* to help us learn things about the sentences in the quotes. We might have some complicated sentence of English, and if we can translate it into some expression of Boolean Logic that is built out of logical operators, together with simpler English sentences that we *don't* consider complicated enough to warrant confusion, then we ought to be able to learn what the more complicated sentence means. Obviously this presupposes we have a way of doing that translation, and that's sort of an art more than a science (unless you study linguistic semantics), but we'll see how far we can get.

The sorts of things we'd like to learn about these sentences are also somewhat varied. For instance, we might have a compound sentence and want to know if the compound sentence is true or not, based on whether or not the atomic sentences are true or not. Or we might want to know what assignments of truth or falsity to the atomic sentences suffice to make the compound sentence false. Or we might want to know whether two compound sentences are equivalent and can be considered paraphrases because the truth values always match. There are any number of things we might want to do with these compound sentences.

But as stated so far, all we have are these two atomic sentences in English about Picard and Worf and not much else. The general framework of Boolean Logic gives us a slightly more general tool: rather than using quoted sentences in English, we can use letters -- usually capital latin letters like `A`, `B`, `C` or `P`, `Q`, `R` -- to stand in for specific choices of sentences that we actually care about. After all, while we might eventually care most about the specific sentences, we'd much rather make use of general tools. So in this setting, we tend to use these abstract letters to signify sentences. These are usually called logical variables, on the grounds that when we use them to develop some knowledge about how truths of sentences relate to one another, we can replace the logical variable sentences with various actual sentences we care about, and the relationships should still hold.

So for instance, if we were to prove that the truth values of `and(A,B)` and `and(B,A)` are always the same regardless of what the truth values of `A` and `B` are, then we can specify the real sentences that correspond to the logical variables `A` and `B` and learn that the truth values of `and("Picard drinks Earl Grey", "Worf drinks prune juice")` and `and("Worf drinks prune juice", "Picard drinks Earl Grey")` are also always the same regardless of the atomic sentences' values. Mapping this back through the translation to English, we now have learned that "Picard drinks Earl Grey and Worf drinks prune juice" is a paraphrase of "Worf drinks prune juice and Picard drinks Earl Grey", and vice versa. That might be useful to know! I mean, maybe not -- it depends on your goals. Maybe you're arguing over a legal contract and the other guy is being a dope claiming that these actually are different and so he doesn't have to pay you $100. Then you probably care and want to show that they're equivalent.

For the rest of this note, we'll use only logical variables, and you can fill in your own choice of atomic sentences as you want.

### Formal Expressions

So, let's define the formal language of Boolean Logic. Or really, the languages, because we often see different notations. In BNF syntax, they are

```bnf
<expression> ::= <variable>
               | <boolean>
               | <unary-operator> <expression>
               | <expression> <binary-operator> <expression>

<variable> ::= "A" | "B" | "C" | ...etc

<boolean> ::= "t" | "f"

<unary-operator> ::= "!"

<binary-operator> ::= "&" | "|" | "->"
```

The choice of operators, boolean syntax, etc. is actually somewhat incidental, but I'm choosing a few here that are familiar. The syntax on the whole is also incidental, we could have used only prefix operators like Python functions, or LISP or Haskell syntax, or whatever. This kind of infix syntax is closest to what's used in the logic literature, without being too obscure with symbols. We will also throw in parenthesis to disambiguate, in ways that hopefully are familiar to readers. 

Some examples of expressions fitting this grammar are

```haskell
!A
A & !A
!A | B
A -> t
f -> C
(A & B) -> A
A -> (B -> A)
(A -> B) -> B
((A | B) & ((A -> C) & (A -> C))) -> C
```

These expressions have some conventional ways of being spoken in English, which are as follows:

```haskell
A = "A", "it is the case that A"
!A = "not A", "it is not the case that A"
A & B = "A and B"
A | B = "A or B"
A -> B = "A implies B", "A entails B", "if A, B", "if A, then B", "whenever A, then B", "whenever A, B"
t = "true", "truth"
f = "false", "falsity"
```

There are also a variety of other symbols you'll see used in the literature, sometimes with different names. Here are some very common ones:

| Symbol | Alternatives (names in parens) |
| ------ | ------------------------------ |
| t      | T, ⊤ (top), 1, on             |
| f      | F, ⊥ (bottom), 0, off         |
| !      | -, ~, ¬                        |
| &      | &&, ∧ (wedge), · (dot)         |
| \|     | \|\|, ∥, ∨ (vee), +            |
| ->     | →, ⇒, ⊃                      |

Another notation for negation is a line that goes over the whole negated expression. This is not an exhaustive list, just enough to hopefully let you pick up a random book on formal logic and not get lost in symbology.

These operators also have some conventional names, as distinct from the names of the *symbols*. For instance, `&` as a symbol is the ampersand, while `∧` is wedge, but both represent the same logical operator, which is usually called "and" or "conjunction". The operator indicated by `|` is usually called "or" or "disjunction". The operator indicated by `->` is usually called "implication" or "entailment". The operator indicated by `!` is usually called "negation".

One final note on notation. Sometimes we'll want to talk about sentences in the abstract. For instance `A & B` and `C & D` are distinct expressions in the grammar above, but they both have the same shape, at least in that they are both conjunctions. When we want to talk about such general shapes, we need a way of indicating the parts where the details are irrelevant. Some logic texts will abuse notation and re-use the syntax of logical variables for this purpose. I find this confusing, so we'll instead use the same names but prefix them with a question mark. For example, `?A`, which means *some* expression or other, but I don't care which. So we could now refer to both `A & B` and `C & D`, and also `(A | B) & (C -> D)`, and all other conjunctions, by using `?A & ?B`. In fact, I'll try to stick to using names from the end of the alphabet, preferring `?X & ?Y`. This kind of variable is called a *meta-syntactic* or *schematic* variable, because they are not variables that ought to be thought of as existing in the logic itself, but rather are what we use to *refer to* the expressions of the logic. Some logic texts will also use Greek symbols like phi (φ) and psi (ψ), others will use syntax highlighting and special letter forms (eg italic), and while this is nice and pretty, and might be useful on a blackboard, it's a nightmare to type in Markdown, so I've chosen to go with a SICP-inspired notation.

## Evaluating

Now that we've given a precise definition of *what* the expressions of Boolean Logic are, we might well ask how we can use them. As mentioned above, there are many things one might want to do with these expressions, so let's start with the one kind that is most directly related to the fact that Boolean Logic is value-oriented, and that is evaluation. Since every expression is built up out of atomic sentences/logical variables which can be assigned truth values, and out of operators which can sort of combine truth values, we can assign to every expression its own truth value defined in terms of the truth values of the parts inside of it. This process is called evaluation, or evaluating an expression, or calculating and computing its value.

We typically do this by explaining first what the values of the atomic sentences or logical variables are that we're starting with -- an assignment of truth values to logical variables. We also explain how the values of each individual syntactic form is computed -- usually by reference to the values of its parts. And then we calculate, in a bottom up fashion, the values of the various (sub)expressions that are relevant, until we've calculated the one we care about. The first part here -- assignments of values to variables -- is usually contingent on the specific macro-level problem we're interested in, while the second -- how the expressions build up values from parts -- is a fixed aspect of Boolean Logic. Because of this fixed-ness, we usually will specify those once, and then treat them as common knowledge and we never re-specify them. So, let's specify those now.

1. The boolean value of the expression `t` is true, which for the sake of notational simplicity will also be written `t`.
2. The boolean value of the expression `f` is false, which likewise will be written just `f`.
3. Given the expression `!(?X)`, if the value of `?X` is `t`, then the value of `!(?X)` is `f`, and if `?X` is `f` then `!(?X)` is `t`.
4. Given the expression `?X & ?Y`, if the value of `?X` is `t`, and also the value of `?Y` is `t`, then the value of `?X & ?Y` is `t`, otherwise its value is `f`.
5. Given the expression `?X | ?Y`, if the value of `?X` is `f`, and also the value of `?Y` is `f`, then the value of `?X | ?X` is `f`, otherwise its value is `t`.
6. Given the expression `?X -> ?Y`, if the value of `?X` is `t`, and the value of `?Y` is `f`, then the value of `?X -> ?Y` is `f`, otherwise its value is `t`.

There are a few things to observe here. One is the curious fact that the definitions for (3) and (4) look very similar but with some things swapped around. This is an intentional presentation choice, to highlight a phenomenon called duality, which we'll cover later in depth (!! OBLIGATIONs). But another thing to observe is that, gosh is this verbose! I mean it's fine, but its a lot of words. Usually what we'd do to make this easier to present is to give this information in the form of a table.

### Tabular Definitions

One such tabular form has a single column labeled by each schematic variable of interest, and then another column for the whole operator expression. Each row below that represents choices for the values of the schematic variables (that is to say, possible values that the expressions represented by the schematic variable might have), together with the value of the whole expression given those values. For instance, here are the tables for negation and conjunction:

| ?X | !(?X) |
| -- | ----- |
| f  |   t   |
| t  |   f   |

| ?X | ?Y | ?X & ?Y |
| -- | -- | ------- |
| f  | f  |    f    |
| f  | t  |    f    |
| t  | f  |    f    |
| t  | t  |    t    |

We can read these as "when the value of `?X` is `f`, the value of `!(?X)` is `t`", which is the first row for negation, or "when the value of `?X` is `t` and the value of `?Y` is `f`, the value of `?X & ?Y` is `f`", which is the third row of conjunction.

Another somewhat common tabular notation is to compress this into a single column, and to align the values of schematic variables with the schematic variables they belong to, and to align the values of the compound expressions with the operators that form those compound expressions. In this notation, the tables would be written

```
| !(?X) |
| ----- |
| t  f  |
| f  t  |
```

```
| ?X & ?Y |
| ------- |
|  f f  f |
|  f f  f |
|  t f  f |
|  t t  t |
```

These different notations can be more or less useful when we come to calculating, depending on your preference. I will use only the first kind, simply for clarity, but I'll give some examples of the second kind in footnotes where appropriate.

Since we gave the truth tables for negation and conjunction, lets also give truth, falsity, disjunction, and implication. Truth and falsity are obvious and boring, since they have no subexpressions:

| t |
| - |
| t |

| f |
| - |
| f |

Disjunction is just

| ?X | ?Y | ?X \| ?Y |
| -- | -- | -------- |
|  f |  f |     f    |
|  f |  t |     t    |
|  t |  f |     t    |
|  t |  t |     t    |

And implication is

| ?X | ?Y | ?X -> ?Y |
| -- | -- | -------- |
|  f |  f |     t    |
|  f |  t |     t    |
|  t |  f |     f    |
|  t |  t |     t    |

There are many more logical operators, and you can fill out tables like this all sorts of ways, but these are the ones we're going to focus on.

One note on conventions here: you might observe that the value rows of these tables are always sorted as if `f < t`. This isn't necessary, but it's common convention[^1].

[^1]: It also means that when we think in binary terms, with 0s and 1s, the schematic variables end up counting out binary numbers -- 00, 01, 10, 11, etc. -- which is pleasing, but also pragmatic, because they therefore indicate also the row number. 00 is not just the values of `?X` and `?Y` in the first row of the table, that row's 0-based index is also 00 as a binary number! That fact, combined with the fact that the output of these tables is itself a single boolean value, means we can actually be clever and represent the entire table by a bit sequence where the i-th row's output is the i-th bit. If we used little-endian bytes, then the table for `&` is just `0001` which is binary for the number 1, and `|` is `0111` which is binary 7. These kinds of relationships turn out to be useful for implementations, and relating different aspects of logic to one another, and also are great fun to play with. It also lets is observe quite easily that for any n = 0, 1, 2, etc., there are precisely 2^n boolean logical operators with n inputs.

Having now explained the way we evaluate a particular logical expression in terms of the values of its parts, let's talk about how to evaluate a whole compound expression. Specifically, to methods: rewriting and table completion.

### Evaluation by Rewriting

Let's assume we have three logical variables we care about, `A`, `B`, and `C`, and their respective values are `A = t`, `B = f`, and `C = f`. If we want to evaluate the expression `(A & B) | !C`, we can apply the following process:

1. If replace each of the logical variables with their respective values. This would produce `(t & f) | !f`.
2. Find a subexpression that has only boolean-valued subexpressions of its own. For instance, here we can pick either `t & f` or `!f`. Let's pick the former.
3. Use the truth table to determine what the value of that subexpression is, in this case `t & f = f`, and replace the subexpression with that value, giving us `f | !f`.
4. Rinse, repeat.
5. When there's no more subexpressions to replace in this way, and you're left only with a single `t` or `f`, you're done.

You can do this literally by erasing things and replacing them, or you can re-write the entire expression at each step. Take your pick. Here's the full rewriting-based evaluation of `(A & B) | !C`, with each step on a separate line:

```
(A & B) | !C
(t & f) | !f
f | !f
f | t
t
```

So we've discovered that the value of `(A & B) | !C` is `t`, assuming that `A = t`, `B = f`, and `C = f`.

### Table Composition

The above technique works for a single assignment of values for variables. Sometimes, it's more useful to know the value of an expression for *any* assignment of values to variables. In that case, what we can do is build a table that includes all of the subexpressions. Rather than using logical variables `A`, `B`, and `C` here, we instead ought to use schematic variables `?X`, `?Y`, an `?Z`, so that this table constitutes a genralized definition that we can reuse with arbitrary choices for those schematic variables.

To build up this compound table, we'll start by giving the column headers, and then we can compose the information in th definitional tables for the logical operators given above. Our table headers should be each subexpression, so:

| ?X | ?Y | ?Z | ?X & ?Y | !(?Z) | (?X & ?Y) \| !(?Z) |
| -- | -- | -- | ------- | ----- | ------------------ |
| ... |

Now lets put in the values for the schematic variable columns. There's 3 variables, so we'll ultimately have 8 rows:

| ?X | ?Y | ?Z | ?X & ?Y | !(?Z) | (?X & ?Y) \| !(?Z) |
| -- | -- | -- | ------- | ----- | ------------------ |
| f  | f  | f  |
| f  | f  | t  |
| f  | t  | f  |
| f  | t  | t  |
| t  | f  | f  |
| t  | f  | t  |
| t  | t  | f  |
| t  | t  | t  |

And now we can build up the column for the conjunction by referencing the other columns and the tables above. Notice that because the conjunction doesn't use `?Z`, we have redundancy in this column. That's ok, it's just a little extra writing.

| ?X | ?Y | ?Z | ?X & ?Y | !(?Z) | (?X & ?Y) \| !(?Z) |
| -- | -- | -- | ------- | ----- | ------------------ |
| f  | f  | f  |    f    |
| f  | f  | t  |    f    |
| f  | t  | f  |    f    |
| f  | t  | t  |    f    |
| t  | f  | f  |    f    |
| t  | f  | t  |    f    |
| t  | t  | f  |    t    |
| t  | t  | t  |    t    |

Now we can fill in the negation column, again by referencing other columns in the table:

| ?X | ?Y | ?Z | ?X & ?Y | !(?Z) | (?X & ?Y) \| !(?Z) |
| -- | -- | -- | ------- | ----- | ------------------ |
| f  | f  | f  |    f    |   t   |
| f  | f  | t  |    f    |   f   |
| f  | t  | f  |    f    |   t   |
| f  | t  | t  |    f    |   f   |
| t  | f  | f  |    f    |   t   |
| t  | f  | t  |    f    |   f   |
| t  | t  | f  |    t    |   t   |
| t  | t  | t  |    t    |   f   |

And finally, we can complete the table by filling in the disjunction column. But now notice: the disjunction has as its parts, the two columns to the left of it! That means we only need to look at those columns, which are the sub-results of the evaluation.

| ?X | ?Y | ?Z | ?X & ?Y | !(?Z) | (?X & ?Y) \| !(?Z) |
| -- | -- | -- | ------- | ----- | ------------------ |
| f  | f  | f  |    f    |   t   |         t          |
| f  | f  | t  |    f    |   f   |         f          |
| f  | t  | f  |    f    |   t   |         t          |
| f  | t  | t  |    f    |   f   |         f          |
| t  | f  | f  |    f    |   t   |         t          |
| t  | f  | t  |    f    |   f   |         f          |
| t  | t  | f  |    t    |   t   |         t          |
| t  | t  | t  |    t    |   f   |         t          |

And now we have the completed table. To find the value of `(A & B) | !C`, we can now use this table as a reference, a kind of non-primitiv logical operator, and treat the values `A = t`, `B = f`, and `C = f`, as choices for the three inputs `?X`, `?Y`, and `?Z`. We walk down the table to find the row that starts `t f f` and look at the last column to find that its `t`, which is the same answer we got before.

Computing these compound tables is obviously more tedious but they can be useful for certain expressions of Boolean Logic that are interesting. This technique can also be used for answering more complex questions. For example, if we know that `(A & B) | !C` is true, what values can `A`, `B`, and `C` have? Well, we can look at the table to see. In this case, it's clearly, `f f f`, `f t f`, `t f f`, `t t f`, and `t t t`.

## Logical Equivalences

We could also use tables to ask when two expressions are equivalent. Rather than building a table for just a single compound expression, we can build it for two simultaneously, in the same way as before, with the columns corresponding to all the relevant subexpressions. Consider the schematic expressions `!(?X & ?Y)` and `!(?X) | !(?Y)`. Are these equivalent? Are they paraphrases of each other? Here's a table for both of them, putting the full expressions in the right-most columns:

| ?X | !(?X) | ?Y | !(?Y) | ?X & ?Y | !(?X & ?Y) | !(?X) \| !(?Y) |
| -- | ----- | -- | ----- | ------- | ---------- | -------------- |
| f  |   t   | f  |   t   |    f    |     t      |       t        |
| f  |   t   | t  |   f   |    f    |     t      |       t        |
| t  |   f   | f  |   t   |    f    |     t      |       t        |
| t  |   f   | t  |   f   |    t    |     f      |       f        |

And hey, presto, the last two columns are identical, so for every assignment of values to variables, these two expressions have the same value. They're equivalent! This particular equivalence, in fact, is a well known distributive law, one of the two De Morgan laws[^2]. The other is the equivalence of `!(?X | ?Y)` and `!(?X) & !(?Y)`[^3].

[^2]: De Morgan was a contemporary of Boole's, who used the newly invented Boolean Logic to prove a variety of interesting logical theorems.

[^3]: You'll notice that the equivalences look very similar. In fact, they're exactly the same, except they have the `&` and `|` swapped. This is another example of a duality, and is the one that inspired a lot of people to become very interested in the notion of duality.

Determining th equivalence of expressions can be a very important thing in the context of applied logic. For instance, it might be cheaper to build a logic circuit that represents one expression over another. Another way that equivalences can be useful is in making the writing of logical expressions more convenient. For example, if `A & (B & C)` is equivalent to `(A & B) & C`, then it really doesnt matter which you write, and in fact we could just drop the parenthesis to avoid wasting ink. Indeed, they are equivalent and so we do usually drop parens. The same is true of `(A | B) | C` and `A | (B | C)`.

Another question one might be interested in is what expressions of Boolean Logic are always true or always false, no matter what assignment of values to variables you pick. An expression thats always true is called a "tautology", and one that is always false is a "contradiction"[^4].

[^4] Contradiction is also used to describe two or more expressions that cannot all be true, or to describe th situation where one sentence always the opposite value of another sentence, as in "`A` contradicts `!A`". These relate to the idea of an always false expression in that if you conjoined all of them, you would get an expression that is always false.

An example of a tautology in Boolean Logic is the schema expression `?X | !(?X)`, which will always be true no matter choice of `?X` is, even if it's a big complicated expression. That tautology is called the Law of the Excluded Middle (LEM), where the "middle" here is a middle ground between truth and falsity. An example of a contradiction is `?X & !(?X)`, which is always false no matter the choice of `?X`[^5]. This is sometimes called the Law of Non-Contradiction (LNC), at least when its given as something that must not be provable (i.e., you might find people saying that a logic should not prove a contradiction, by which they mean this or any equivalent expression).

[^5]: Keen observers will notice that the expression in LEM and the expression in LNC are similar but with `&`  and `|` swapped. These two also form a duality. You will also probably notice, with some thinking, that the one is equivalent to the negation of the other. It is true in general that if `?X` is a tautology, `!(?X)` is a contradiction, and vice versa.

Another interesting variation on the theme of equivalence is operator equivalence. We saw already that there are relationships between `&` and `|` under negation. It turns out that because of this equivalence, and also the equivalence `!(!(?X)) = ?X`, we can prove both that `?X & ?Y` is equivalent to `!(!(?X) | !(?Y))`, and also `?X | ?Y` is equivalent to `!(!(?X) & !(?Y))`. This means that we could, in principle, throw out either of the operators `&` and `|`, and still be able to express the same ideas. We could keep the symbol as syntactic sugar, of course, but we wouldn't need it as a primitive notion of Boolean Logic if we wanted to do without it. The same is true of the expression `?X -> ?Y`, which turns out to be equivalent to `!(?X) | ?Y`.

Indeed, we can take this even further and ask, of all the logical operators we could define, not just the ones we have already defined, which sets suffice to give you all the rest as syntactic sugar via logical equivalences? This question is especially interesting from a practical perspective. One answer to this is that "nand", which is the negation of conjunction (`?X nand ?Y = !(?X & ?Y)`) is sufficient by itself to replace every other logical operator, including all the binary ones, ternary ones, etc. and the unary ones, and also the nullary ones (`t` and `f`). Nand is also easy to implement in silicon and so a lot of modern computers are actually built almost entirely out of nand circuits for cost and simplicity reasons.

## Calculating with Equivalences

Evaluating expressions and computing tables is a useful tool, but they're not the only way to use expressions. Another important way is to calculate with them. One of the most basic kinds of calculations we might care to make is an equivalence calculation, where we combine known equivalences to produce new, previously unknown equivalences. For example, if we know that `?X` is equivalent to `?Y`, then we ought to be able to conclude that `?X -> ?Z` is equivalent to `?Y -> ?Z`.

The basic principle of reasoning about equivalence is that if two expressions `?X` and `?Y` are equivalent -- which we'll write as `?X = ?Y` -- then given any expression containing the one, we can swap out any occurances of it for the other, and get an equivalent expression. It would be nice to make this formal, however, so let's do that. Here are the basic rules of equivalence for Boolean Logic expressions as given above:

1. If `?X = ?Y`, then `!(?X) = !(?Y)`.
2. If `?X1 = ?X2` and `?Y1 = ?Y2`, then `?X1 & ?Y1 = ?X2 & ?Y2`.
3. If `?X1 = ?X2` and `?Y1 = ?Y2`, then `?X1 | ?Y1 = ?X2 | ?Y2`.
4. If `?X1 = ?X2` and `?Y1 = ?Y2`, then `?X1 -> ?Y1 = ?X2 -> ?Y2`.

These four rules allow us to propagate equivalences up from small parts to the larger wholes. They are called the rules of congruence. We also ought to have some rules that aren't related to the operators themselves, namely:

1. `?X = ?X` (reflexivity)
2. If `?X = ?Y`, then `?Y = ?X` (symmetry)
3. If `?X = ?Y` and `?Y = ?Z`, then `?X = ?Z` (transitivity)

The reflexivity rule should be understood as saying that whenever you need to know that two expressions are equivalent, it suffices that they are syntactically identical. So for example, `A & B = A & B` is true by reflexivity because the two sides are manifestly the same just by looking. They are also, of course, equivalent due to congruence and then reflexivity on the atomic sentences, but we're treating reflevity here as applicable to entire expressions if we want to use it that way.

So now, how can we use equivalences for calculation? Well, suppose we want to show that in general, it holds that `?X & (?Y & ?Z) = (?Z & ?Y) & ?X`. How could we do this? Given just the rules above, it's actually not possible, but we *can* construct one tabular proof of equivalence for `?X & ?Y = ?Y & ?X`:

| ?X | ?Y | ?X & ?Y | ?Y & ?X |
| -- | -- | ------- | ------- |
| f  | f  |    f    |    f    |
| f  | t  |    f    |    f    |
| t  | f  |    f    |    f    |
| t  | t  |    t    |    t    |

Let's call this commutativity of `&` (or `&comm` for short). A little helper fact like this is known as a lemma. Armed with this one tabular proof, we can now reason as follows:

1. `?X = ?X` because of reflexivity.
2. `?Y & ?Z = ?Z & ?Y` because of `&comm`.
3. Therefore, using congruence we know that `?X & (?Y & ?Z) = ?X & (?Z & ?Y)`.
4. And also because of `&comm`, we know that `?X & (?Z & ?Y) = (?Z & ?Y) & ?X`.
5. Putting these two things together using transitivity, we know that `?X & (?Y & ?Z) = (?Z & ?Y) & ?X`.

This is a little verbose, however, so there's a cleaner notation we can use:

```
  ?X & (?Y & ?Z)

= { &comm on ?Y and ?Z }

  ?X & (?Z & ?Y)

= { &comm on ?X and ?X & ?Y}

  (?Z & ?Y) & ?X
```

In this style of equational calculation, we omit the congruence parts, because they're usually obvious given the different sides of the `=`'s. We also implicitly make use of transitivity by syntactically chaining the `=`'s (this form of calculation is called transitive/equational/preorder reasoning and othr things in that vein). Finally, inside the braces, we explain which rule we're using, and how we're using it. Here, we only needed to use our above rule/lemma `&comm`, which we proved separately.

It's valid to ask why it is that we can do this kind of calculation. This kind of question is actually deeply interesting but is much more complex than this chapter ccan go into. We'll try to justify it later in these notes, however (!! OBLIGATION).

Another kind of reasoning that is extremely useful maks us not of equivalence but of a weaker notion, entailment. Consider the (lightly abbreviated) compound truth tables for the two expression schemas `(?X & ?Y) & ?Z` and `?X & ?Z`:

| ?X | ?Y | ?Z | (?X & ?Y) & ?Z | ?X & ?Z |
| -- | -- | -- | -------------- | ------- |
|  f |  f |  f |       f        |    f    |
|  f |  f |  t |       f        |    f    |
|  f |  t |  f |       f        |    f    |
|  f |  t |  t |       f        |    f    |
|  t |  f |  f |       f        |    f    |
|  t |  f |  t |       f        |    t    |
|  t |  t |  f |       f        |    f    |
|  t |  t |  t |       t        |    t    |

These two expressions are clearly not equivalent, because they have different rows. In particular, for `?X = t`, `?Y = f`, and `?Z = t` they different. But we can also observe that whenever `(?X & ?Y) & ?Z` is true, `?X & ?Z` is *also* true. This means that if we ever know the former, we're allowed to act as if we have the latter. We can represent this symbolically as `(?X & ?Y) & ?Z !- ?X & ?Y`, using the symbol `!-`. This symbol is also sometimes written `|-` in ASCII, and in unicode is `⊢`. The symbol is called a "turnstile", because it looks vaguely like a turnstile in a train station, etc., and when read allowed is pronounced "entails", as in reading `A !- B` as "`A` entails `B`". We can also read it as "given `A`, we know `B`", or "assuming `A`, then `B`", and similar such phrasings.

We can extend this observation to a form of calculation similar to what we just did above, but with certain limitations. Let's give some rules, but start with the more general rules:

1. `?X !- ?X` (reflexivity)
2. If `?X !- ?Y` and `?Y !- ?Z`, then `?X !- ?Z` (transitivity)

Thats it. We do not have a symmetry rule, because as we saw above, sometimes it's just not true that entailment goes both ways. When it does, we of course call it equivalence -- `A !- B` and `B !- A` means `A = B`, and sometimes we even write this as `A -!!- B` (or `A -||- B` or `A ⟛ B`) to be more evocative of the bidirectional entailment.

If we wish to now look at the entailment-equivalents of the congruence rules described above, we have to be careful. Entailment is directional, and so there are subtleties.

1. If `?X !- ?Y` then `!(?Y) !- !(?X)` (note the direction swap!)
2. If `?X1 !- ?X2` and `?Y1 !- ?Y1`, then `?X1 & ?Y1 !- ?X2 & ?Y2`.
3. If `?X1 !- ?X2` and `?Y1 !- ?Y1`, then `?X1 | ?Y1 !- ?X2 | ?Y2`.
4. If `?X1 !- ?X2` and `?Y1 !- ?Y1`, then `?X2 -> ?Y1 !- ?X1 -> ?Y2` (note the placement of `?X1` and `?X2`!)

Again, we might wonder what justifies these, and we'll get to that much later (!! OBLIGATION). For now, we can take it for granted that this is correct.

Now, let's do some entailment reasoning. Let's first observe that `?X & ?Y !- ?X`. If we look at the truth table for `?X & ?Y`, this is clearly the case: all the rows where `?X & ?Y` are true are also rows where `?X` are true (but not necessarily vice versa). This makes sense -- if `?X` AND `?Y` are true, then of course `?X` is true. Call this `&proj1` for `&` projection 1 (there's obviously an `&proj2` that pulls out `?Y`, as well).

So then, here's a little entailment proof of the two expression we looked at before:

1. By `&proj1`, we know `?X & ?Y !- ?X`.
2. By reflecivity, we know `?Z !- ?Z`.
3. By the second rule of the entailment analog of congruence, we therefore know that `(?X & ?Y) & ?Z !- ?X & ?Z`.

Using the convenient transitive reasoning notation from earlier, this becomes the simple proof

```
   (?X & ?Y) & ?Z

!- { &proj1 on ?X & ?Y }

   ?X & ?Z
```

This kind of calculation is less commonly done within Boolean Logic, at least not the kind that most computer folk are used to using, but it does show up quite a bit in certain contexts where we're reasoning about programs. For instance, the calculational reasoning performed in the Squiggolist tradition of functional and relational programming research employees this kind of reasoning. Another, more common form, is subtyping, where instead of expressions that represent propositions in a logic, we use expressions that represent datatypes, and instad of entailment, we use a subtyping relation, usually written `A <: B` and chain subtyping statements.

## Normal Forms

As we've seen above, in Boolean Logic, expressions can be complex, recursively defined things, and the evaluation procedures are similarly recursive in nature. We saw that can make use of this recursive structure to answer questions about things such as the values of particular expressions, or when two expressions are equivalent, or when one entails another. But this can be increasingly tedious as the number of logical variables or schematic variables grows. Each variable can have two possible values, and so the tables grow exponentially, as a power of two. Determining if two expressions are equivalent by hand using tables rapidly becomes infeasible, and computing this in software also becomes quite difficult fairly quickly. Given expressions of Boolean Logic with 100 variables, a computer would take longer than the lifetime of the universe to determine if they're equivalent using the tabular composition method! Trying to use calculational techniques can make it somewhat easier to do, but we end up running into problems of indeterminacy -- which rules do we use? How do we decide? Which lemmas should we prove? We can automate this with a computer, to be sure, but it's still not ideal.

To address this, logicians have developed a variety of techniques to make the problems simpler. One especially useful one is called the Normal Form. For every expression of Boolean Logic, there is a corresponding normal form that it can be transformed into, which is also logically equivalent to it, but which is much easier to use. Indee, there are *many* normal forms an expression can be transformed into, but usually you pick one normalization technique and use only that. Two major kinds of normal form are Conjunctive Normal Form and Disjunctive Normal Form.

### Conjunctive Normal Form

In Conjunctive Normal Form (CNF), all expressions are of built up from atoms at the bottom (specifically, atomic sentences or logical variables), which are optionally negated as desired, and those are then put together with disjunction, and then the disjunctions are conjoined. So then, all expressions in CNF look like `(A | !B | C) & (!A | !C) & D & (E | F)`. CNF has lots of uses in logic, but is somewhat less interesting in its connections to computation, so we'll omit further detailed discussion of it.

### Disjunctive Normal Form

Similarly, we have Disjunctive Normal Form (DNF), which puts disjunctions outside conjunctions. DNF expressions all look like `(A & !B & C) | (!A & !C) | D | (E & F)`[^6]. This form has lots of rich connections to computation, and especially data types. It also has rich connections to the logic tables we described above.

[^6]: Strictly speaking, `f` and `t` are also valid, but we only ever us them in isolate, never as part of a compound DNF expression. Though they might show up in compound expressions during the process of normalization.

But before we get into that, lets look at how we derive the disjunctive normal forms for an arbitrary expression of Boolean Logic.

So, firstly, notice that DNF does not use `->`. We can remove `->` from any expression of Boolean Logic simply by treating it as syntactic sugar, thanks to the equivalence `?X -> ?Y = !(?X) | ?Y`. So that's our first step in normalization: eliminate all uses of `->`.

Next, consider negation: we want all negation to be "at the bottom", so to speak. That is to say, no negation applied to any expression except for logical variables. We can take advantage of the two De Morgan laws we saw earlier to push negation close to the logical variables and make the expressions simpler:

If we have `!(?X | ?Y)`, push the negation under the disjunction to produce `!(?X) & !(?Y)`, and likewise if we have `!(?X & ?Y)`, push the negation under the conjunct to produce `!(?X) | !(?Y)`. We repeatedly apply this whenever possible until the negations are all as far down as possible. It doesn't matter if we do this top-down or bottom-up. Eventually, however, we'll have negations applied directly to logical propositions, or to other negations, as in `!!!(?X)`.

The next thing we can do is take advantage of the logical equivalence `!!(?X) = ?X`, which is usually called Double Negation Elimination (DNE). Through repeated appication, any even numbered stack of negations on top of a logical variable will go away, and an odd numbered stack is reduced to a single negation.

We're almost done. At this point, we have all negations at the logical variables only, with at most one negation. We have no implications, those having been expanded as syntactic sugar. Finally, the expression above the atoms/negations are built out of only conjunction `&` and disjunct `|`. But the structure of the conjunctions and disjunctions aren't yet in DNF. We can still have disjunctions inside of conjunctions.

The final step is to repeatedly make use of the following two equivalences:

1. `?X & (?Y | ?Z) = (?X & ?Y) | (?X & ?Z)`
2. `(?X | ?Y) & ?Z = (?X & ?Z) | (?Y & ?Z)`

These are distributive laws not unlike the mathematical laws relating addition and multiplication: `x * (y + z) = x * y + x * z` and `(x + y) * z = x * z + y * z`[^7]. These two equivalences let you push the conjunction down below a disjunction, further towards the logical variables where they need to be.

[^7]: The reason why these laws look so similar is quite interesting, but well beyond the scope of these lecture notes.

A few more rules pertaining to `t` and `f` can be applied freely at any point, whenever possible[^8]:

1. Replace `?X & t` and `t & ?X` with just `?X`.
2. Replace `?X | t` and `t | ?X` with just `t`.
3. Replace `?X & f` and `f & ?X` with just `f`.
4. Replace `?X | f` and `f | ?X` with just `?X`.

[^8]: We have some more things that look like they should be dualities, and of course they are. Duality is verywhere in logic!

All of these rules are based on equivalences, which you can prove easily enough with the tabular method.

After this process, when no more rules apply, we have an almost-DNF expression. Let's see some examples of this before we go the final step to full and true DNF. First, let's normalize `!(!(A -> B) & (f | (C | D)))`. We'll use a calculational notation to do this:

```
  !(!(A -> B) & (f | (C | D)))

= { replace f | ?X with ?X }

  !(!(A -> B) & (C | D))

= { desugar -> }

  !(!(!A | B) & (C | D))

= { push ! over | }

  !((!!A & !B) & (C | D))

= { push ! over & }

  !(!!A & !B) | !(C | D)

= { push ! over & }

  (!!!A | !!B) | !(C | D) = !!!A | !!B | !(C | D)

= { push ! over | }

  !!!A | !!B | (!C & !D)

= { double negation elimination }

  !A | B | (!C & !D)
```

We didn't get to see any uses of the distributivity laws, so lets look at an expression with some of those. Namely, `(A | B) & (C | D | E)`:

```
  (A | B) & (C | D | E)

= { distribute on the right }

  (A & (C | D | E)) | (B & (C | D | E))

= { distribute on the left }

  (A & C) | (A & D) | (A & E) | (B & C) | (B & D) | (B & E)
```

Now what are some uses of this? Well, the above set of rules doesn't quite suffice to let us make identifying equivalent expressions trivial, but it *does* give us a nice tool for relating arbitrary expressions to their truth tables. Rather than sitting down and calculating all of the possible truth table rows for a complex expression, we can instead calculate a DNF, and read off the truth table from that. How? Let's take a look again at `!(!(A -> B) & (f | (C | D)))`. We saw that this reduces to the expression `!A | B | (!C & !D)`. Each of the disjuncts here -- `!A`, `B`, and `!C & !D` -- can be seen as partially-specified rows of a truth table. Namely, `!A` is rows where `A` is valued as `f`, `B` is rows where `B` is valued `t`, and `!C & !D` is rows where both `C` and `D` are valued as `f`.

Let's fill out the 16 different rows, for the variable only, and ignore the compound expression:

| A | B | C | D | ... |
| - | - | - | - | --- |
| f | f | f | f |
| f | f | f | t |
| f | f | t | f |
| f | f | t | t |
| f | t | f | f |
| f | t | f | t |
| f | t | t | f |
| f | t | t | t |
| t | f | f | f |
| t | f | f | t |
| t | f | t | f |
| t | f | t | t |
| t | t | f | f |
| t | t | f | t |
| t | t | t | f |
| t | t | t | t |

Now lets go through and fill in the last column, according to those row descriptions. First, we will in all the rows where `A` is `f` with the value `t` for the final column. Those rows are the ones indicated by arrows, so they get `t`:

| A | B | C | D | ... |
| - | - | - | - | --- |
| f | f | f | f |  t  | <---
| f | f | f | t |  t  | <---
| f | f | t | f |  t  | <---
| f | f | t | t |  t  | <---  all newly filled cells
| f | t | f | f |  t  | <---
| f | t | f | t |  t  | <---
| f | t | t | f |  t  | <---
| f | t | t | t |  t  | <---
| t | f | f | f |
| t | f | f | t |
| t | f | t | f |
| t | f | t | t |
| t | t | f | f |
| t | t | f | t |
| t | t | t | f |
| t | t | t | t |

Ok, now lets find all the rows where `B` is `t` and fill those final columns in as `t` as well. It's ok if it's already `t`.

| A | B | C | D | ... |
| - | - | - | - | --- |
| f | f | f | f |  t  |
| f | f | f | t |  t  |
| f | f | t | f |  t  |
| f | f | t | t |  t  |
| f | t | f | f |  t  | <---
| f | t | f | t |  t  | <--- these 4 are previously filled
| f | t | t | f |  t  | <---
| f | t | t | t |  t  | <---
| t | f | f | f |
| t | f | f | t |
| t | f | t | f |
| t | f | t | t |
| t | t | f | f |  t  | <---
| t | t | f | t |  t  | <--- these 4 are newly filled
| t | t | t | f |  t  | <---
| t | t | t | t |  t  | <---

And now, finally, let's find the columns where `C` and `D` are both `f`, and fill those final columns in as `t`:

| A | B | C | D | ... |
| - | - | - | - | --- |
| f | f | f | f |  t  | <--- previously filled
| f | f | f | t |  t  |
| f | f | t | f |  t  |
| f | f | t | t |  t  |
| f | t | f | f |  t  | <--- previously filled
| f | t | f | t |  t  |
| f | t | t | f |  t  |
| f | t | t | t |  t  |
| t | f | f | f |  t  | <--- newly filled
| t | f | f | t |
| t | f | t | f |
| t | f | t | t |
| t | t | f | f |  t  | <--- previously filled
| t | t | f | t |  t  |
| t | t | t | f |  t  |
| t | t | t | t |  t  |

Last but not least, we can fill in the remaining rows' final column with `f`:

| A | B | C | D | ... |
| - | - | - | - | --- |
| f | f | f | f |  t  |
| f | f | f | t |  t  |
| f | f | t | f |  t  |
| f | f | t | t |  t  |
| f | t | f | f |  t  |
| f | t | f | t |  t  |
| f | t | t | f |  t  |
| f | t | t | t |  t  |
| t | f | f | f |  t  |
| t | f | f | t |  f  | <---
| t | f | t | f |  f  | <--- these three now get `f`
| t | f | t | t |  f  | <---
| t | t | f | f |  t  |
| t | t | f | t |  t  |
| t | t | t | f |  t  |
| t | t | t | t |  t  |

And indeed, this is the truth table for the complex expression we started with! Or at least it is if we put `!(!(A -> B) & (f | (C | D)))` in place of `...`. Try reconstructing the truth table using the tabular method to see that this is the case. This process of converting to DNF first is dramatically faster in general than manually calculating the truth tables.

Another use for disjunctive normal form is the reverse process. Given any arbitrary truth table, we can construct a logical formula in DNF as follows: ignore the rows where the whole formula is valued `f`. Translate each row as follows: if a variable is given as `t` then write down the variable, if it's `f`, write the negation of the variable, and then conjoin those. Then, after all rows are written like this, combine them all with disjunctin.

For example, consider the random truth table[^9]:

| A | B | C | ??? |
| - | - | - | --- |
| f | f | f |  t  |
| f | f | t |  t  |
| f | t | f |  f  |
| f | t | t |  f  |
| t | f | f |  t  |
| t | f | t |  f  |
| t | t | f |  f  |
| t | t | t |  t  |

[^9]: Ok, it's not so random, if you convert the final column into a binary string you get 11001001, which is the title of Star Trek: The Next Generation's 15th episode, about little cyborg people who talk to each other in binary.

What is the logical expression for this truth table? I don't know. But let's find out!

Step 1 was to ignore all the rows where the last column is `f`. That's these:

| A | B | C | ??? |
| - | - | - | --- |
| f | f | f |  t  |
| f | f | t |  t  |
| f | t | f |  f  | <---
| f | t | t |  f  | <---
| t | f | f |  t  |
| t | f | t |  f  | <---
| t | t | f |  f  | <---
| t | t | t |  t  |

So throw 'em out:

| A | B | C | ??? |
| - | - | - | --- |
| f | f | f |  t  |
| f | f | t |  t  |
| t | f | f |  t  |
| t | t | t |  t  |

Then, for each row, write it as a conjunction, with the variables either negated (if they're valued `f`, or not, if they're valued `t`):

| A | B | C | ??? |
| - | - | - | --- |
| f | f | f |  t  | ---> !A & !B & !C
| f | f | t |  t  | ---> !A & !B & C
| t | f | f |  t  | ---> A & !B & !C
| t | t | t |  t  | ---> A & B & C

And finally, combine those sub-expressions into a disjunction:

```
(!A & !B & !C) | (!A & !B & C) | (A & !B & !C) | (A & B & C)
```

And there we have it, the title of a Star Trek episode translated into an expression of Boolean Logic in disjunctive normal form. I'm sure Lt. Cmdr. Data would approve! Of course, there are simpler, or at least smaller, expressions that are equivalent. For instance, we can represent it as `(!A & !B) | (A & (B == C))`, assume we're allowed to use the `==` operator (boolean equality, also know as iff, if and only iff). Or if we want only the operators from earlier, `(!A & !B) | (A & (B -> C) & (C -> B))`, or `(!A & !B) | (A & ((B & C) | (!B & !C)))`, or any number of other equivalent things that are technically shorter, by characters at least, than the big disjunction. The DNF form has the advantage of being *trivially derived* from the truth table without any thought.

## Satisfaction

The Rolling Stones couldn't get no satisfaction, but logical expressions often can: in logic, we say that an expression with logical variables can be "satisfied" if there are some values for variables which will make the whole expression true. An expression that is unsatisfiable is a contradiction, one that is always satisfiable is a tautology, but what about the space between? Some expressions are neither contradictions nore tautologies, but merely satisfiable expressions. How can we determiine whether an expression is satisfiable, and if so, which assignments of values to variables will do it?

This is a problem that arises a lot in computer science, under the name Satisfaction Problems, or SAT. If you see a number before the SAT, that's how many logical variables are involved. The most common name you'll see is probably 3SAT, which is the problem of whether or not an arbitrary boolean expression with 3 logical variables can be satisfied.

It's extremely easy to answer the question "is the expression `?X` satisfiable?" for any arbitrary boolean expression, so long as you have a lot of time to spend on it. I mean, you can just build up the truth table of the expression and see if any of its final columns has a `t` in it, and if so, the answer is yes, other it's no! But this brute force solution is awful if we're trying to answer the question for expressions with many logical variables. As with the equivalence problem described above, once we get into the realm of 100 or so variables, even our best computers couldn't do it in the lifetime of the univers so far.

So what else can we do? Well, one option is to use our truth tables in the reverse direction. Previously, we determined the truth table for a complex expression by building up to it from sub-expressions, aggregating intermedia columns until we got to the column for the full expression. This time, we'll work in reverse. Let's see an example of this process. Consider the expression `A & !B`. This is definitely satisfiable, and it's not too hard to just built the truth table for it the usual way, but let's work backwards.

Starting with the whole expression, we know it can only have the values `f` and `t`, in unknown arrangments. So, let's start with a single column with just those:

| A & !B |
| ------ |
|   f    |
|   t    |

Now, the whole expression is a conjunction -- the outermost operator is `&` -- so we can look at the truth table for `&` and find out what the corresponding truth values must be, or can be, for the sub-expressions, for each possible truth value for the whole conjunction. In this case, the conjunction is true when `A` and `!B` are both true, and false otherwise. So we'll add columns for these sub-expressions, and split the rows to reflect this:

| A & !B | A | !B |
| ------ | - | -- |
|   f    | f | f  |
|   f    | f | t  |
|   f    | t | f  |
|   t    | t | t  |

The `t` row didn't split at all because only one of the rows for conjunction is valued `t`, but the `f` row split into three, because of the three rows in the conjunction table that are all valued `f`.

Now we have only one remaining non-atomic column, `!B`. The `A` column is atomic, and so we don't need to do anything more with it. Looking at the negation table, now, we do the same thing, and insert a new column for `B`, and make its values the necessary things so that the `!B` column is valued as shown there:

| A & !B | A | !B | B |
| ------ | - | -- | - |
|   f    | f | f  | t |
|   f    | f | t  | f |
|   f    | t | f  | t |
|   t    | t | t  | f |

Every column that could be expanded into new columns has been expanded, so we're done. If we now check the columns for `A` and `B`, we see that they're all the possible combinations of values and variables, but in a funny order. Let's re-arrange the table, by moving the columns to a more normal order, and sorting the rows so that the `A` and `B` columns look like we've been doing above:

| A | B | !B | A & !B |
| - | - | -- | ------ |
| f | f | t  |   f    |
| f | t | f  |   f    |
| t | f | t  |   t    |
| t | t | f  |   f    |

We now know that the values `A = t` and `B = f` together will satisfy this expression. However, not all expressions are satisfiable. For instance, `A & !A`. Let's do the same thing here, and see what goes wrong. By the same reasoning as abov, the whole thing can only have two values, `t` and `f`, so we build that table

| A & !A |
| ------ |
|   f    |
|   t    |

And then we expand the table by working backwards on conjunction:

| A & !A | A | !A |
| ------ | - | -- |
|   f    | f | f  |
|   f    | f | t  |
|   f    | t | f  |
|   t    | t | t  |

So far so good. Finally, we work backwards on negation, adding a second column for `A` this time based on the truth table for the negation column:

| A & !A | A | !A | A |
| ------ | - | -- | - |
|   f    | f | f  | t |
|   f    | f | t  | f |
|   f    | t | f  | t |
|   t    | t | t  | f |

Now we can inspect the columns. We have two columns for the atomic sentence `A`, but they're *distinct* columns. They sometimes have the same value, but sometimes they differ! But a variable like `A` can only have one value, so which is it? Well, the answer is, if we look at only the rows when `A & !A` is true, we see that those specific rows -- all 1 of them -- have conflicting values for `A`, and therefore there's no way to make the whole expression true. It's unsatisfiable!

This is the failure condition -- when we have failed to satisfy the expression. Any time the same variable must be assigned both `t` and `f` in all the rows where the whole expression is valued `t`, we know that the expression is unsatisfiable. Another way to say this is, if we eliminate all of the rows with conflicting definitions for the variables, the remaining rows do not ever assign `t` to the whole expression, like so:

| A & !A | A | !A | A |
| ------ | - | -- | - |
|   f    | f | t  | f |
|   f    | t | f  | t |

Now let's look at a case where the sentence always satisfiable (i.e. is a tautology). For instance, consider the expression `A | (A -> B)`. We start with the table

| A \| (A -> B) |
| ------------- |
|       f       |
|       t       |

and then expand this with the table for `|`:

| A \| (A -> B) | A | A -> B |
| ------------- | - | ------ |
|       f       | f |   f    |
|       t       | f |   t    |
|       t       | t |   f    |
|       t       | t |   t    |

And then expand with the table for `->`:

| A \| (A -> B) | A | A -> B | A | B |
| ------------- | - | ------ | - | - |
|       f       | f |   f    | t | f |
|       t       | f |   t    | f | f |
|       t       | f |   t    | f | t |
|       t       | f |   t    | t | t |
|       t       | t |   f    | t | f |
|       t       | t |   t    | f | f |
|       t       | f |   t    | f | t |
|       t       | f |   t    | t | t |

If we now remove the rows with conflicting values for `A`, we're left with

| A \| (A -> B) | A | A -> B | A | B |
| ------------- | - | ------ | - | - |
|       t       | f |   t    | f | f |
|       t       | f |   t    | f | t |
|       t       | t |   f    | t | f |
|       t       | f |   t    | f | t |

But what about cases where the whole thing is false? Well, we have all possible combinations of values for both `A` and `B`, so there are no such cases! The expression is always true!

This technique so far has involved working backwards to all the assignments of values to variables. This isn't much better than building up the truth table from those same assignments! Wasn't the point to do better than brute force enumeration? Yes! And we can, in two different ways! The first is quite simple: since we're trying to find a means of satisfying the expression, we don't need to consider any cases where the whole expression is false. That immediately eliminates a bunch of work. If we repeat the process for `A & !A`, this time omitting false rows, we get this:

Start with the goal of satisfying the expression.

| A & !A |
| ------ |
|   t    |

Expand with `&`'s truth table:

| A & !A | A | !A |
| ------ | - | -- |
|   t    | t | t  |

Expand with '!'s truth table:

| A & !A | A | !A | A |
| ------ | - | -- | - |
|   t    | t | t  | f |

We only have one row now, and it has a conflict. Eliminating it produces no rows, and so the expression cannot be satisfied.

A second technique we can also use is to make better use of our attention and focus on individual rows and variables. Rather than expanding everything, we can try to narrow in on the potential conflicts by trying to expose multiple occurences of the same logical variable, and eliminating rows as we go. Any time there is a conflict of variable assignments in a row, regardless of what other parts of the row we've looked at, we can immediately remove that row from the table, and not go any further with it. To demonstrate this, let's consider the expression `A & (!A & (B | C))`, which is a contradiction.

Starting with the satisfaction rows only:

| A & (!A & (B \| C)) |
| ------------------- |
|          t          |

Expand now with `&`:

| A & (!A & (B \| C)) | A | !A & (B \| C) |
| ------------------- | - | ------------- |
|          t          | t |       t       |

And again:

| A & (!A & (B \| C)) | A | !A & (B \| C) | !A | B \| C |
| ------------------- | - | ------------- | -- | ------ |
|          t          | t |       t       | t  |   t    |

At this point, we can entirely ignore the disjunction `B | C` and expand only the negation:

| A & (!A & (B \| C)) | A | !A & (B \| C) | !A | B \| C | A |
| ------------------- | - | ------------- | -- | ------ | - |
|          t          | t |       t       | t  |   t    | f |

Immediately we have a conflict, and there's only one row in the table, so we remove it and we've eliminated every possible option for satisfaction, and proven that the expression is unsatisfiable.

Using this technique at works decently well for moderately sized expressions, and simply requires that we focus on the decompositions that will expose multiple decompositions of the same logical variable. We generally *won't* only be working on a single row -- the expressions we looked at above were lucky choices that were well suited to demonstrate the technique -- but the combination of both simplifying techniques *does* eliminate a lot of work. These same techniques can also be used to find the cases when an expression is false, just by focusing on only the `f` rows rather than `t` rows.

Many computery folks are already doing something kind of like this whenever they have to evaluate a logical expression, but very often, they're doing it informally, with not a lot of rigor behind the reason, just rough ideas of what seems right. By applying the table technique, they can get precise, reliable results.

## Conclusions for Boolean Logic

There are many many more things we ould say about Boolean Logic, but we're going to pause here. The stuff we've discussed in this note is a fairly good place to stop, because most, if not all of it, ought to be fairly familiar to you already if you do computery things. This presentation of it all, however, has probably included some new things you didn't know. It also allowed us to look at some of the sorts of questions and phenomena that logicians study. Amongst those are equivalence, entailment, satisfaction, and proof. As we progress through the rest of these notes, we'll look at more ways to reason with Boolean Logic and its close kin. These later techniques will often provide us with more power or convenience when actually constructing proofs and refutations.