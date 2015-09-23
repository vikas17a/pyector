# Warning #
This page comes from an [ancient note](http://francois.parmentier.free.fr/ector/note_concept_creation.html). I need to rethink this aspect for version 0.5

# Introduction #

Words often have several semantics, that's why a concept is a combination of several words. Actually, an expression gives a particular sense to all the words it contains.


Moreover, some words are often related, and have a particular sense when associated (like "neural" and "network"). That's why we can create a new semantic node in the concept Network when a sequence of words co-occurs equally.

```
                                                 +---(2)---> many(4)
                                                 |
                                                 v
there (5) <----(4)---> has (10) <----(4)---> been (6)
                                                 ^
                         |                       |
                         |                       +---(1)--> several(1)
                         |
                         | CREATION OF "there as been"
                         v

                   there has been(4)
                    ^      ^      ^
                    |      |      |
           +--(4)---+     (4)     +--(4)---+   +--(2)--> many(4)
           |               |               |   |
           v               |               v   v
      there(5) <--(4)--> has(10) <--(4)--> been(6)
                                               ^
                                               |
                                               +--(1)--> several(1)
```

When a phrase is added, the higher level concepts (higher than words) are also considered. Example: addition of the phrase there has been something.

```
              there has been(5)
              ^      ^      ^
              |      |      |
     +--(5)---+     (5)     +--(5)---+   +--(2)--> many(4)
     |               |               |   |
     v               |               v   v
there(6) <--(5)--> has(11) <--(5)--> been(7) <--(1)--> something(1)
                                         ^
                                         |
                                         +--(1)--> several(1)
```


In order to create a concept, all the nodes to be integrated must have an equivalent (95%) co-occurrence.

The created node then has a number of occurrences equal to the minimum of the co-occurrences considered.

"Creating" nodes influence the new one, but this one influences only the first and last constituents of the string.

A created node can be a sub-concept of another existing one (for example a sentence, or another created concept).

```
      s e n t e n c e
      |   |   |   |
    +-+   |   |   +--+
    |     |   |      |
word1--word2--word3--word4

 NEW CONCEPT WITH WORDS 1 TO 3

       s e n t e n c e
             |      |
         created    +--- word4 -+
           node                 |
          | | |                 |
 word1 ---+ | +---- word3 ------+
            |
          word2
```