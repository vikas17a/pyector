# Introduction #

Each ConceptNetwork Node has a _type_, which determines its decay rate.


# Details #

Here are the different types (they are chatterbot-oriented, but one could add others):

  * sentence : a node containing a sentence, which decay rate is 50
  * token : a part of a sentence, used to represent an atomic symbol (typically a word). Decay rate: 40
  * expression : a part of sentence, containing at least two tokens. Decay rate: 40
  * sentiment : a sentiment, that maybe active or not. Decay rate: 10
  * utterer : someone that can talk. Decay rate: 70
  * label : a node specially created to be a link's label (`part-of` between a sentence and its tokens or expressions, for exemple). Decay rate: 10
  * file : like an utterer, but for a file (even taken on the web). Decay rate : 50