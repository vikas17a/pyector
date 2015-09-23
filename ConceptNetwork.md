# Introduction #

A Concept Network is a net made of nodes and weighted links between them. It can be wholly connected.

# A concept #

A concept is a set of nodes in the Concept Network, strongly bound together and simultaneously activated. Thus, when nodes named `network`, `neural`, `Widrow`, `Kohonen`, and `Hoff` are in a Concept Network, one can assume that they constitute one concept, different from the one constituted by `Markov`, `hidden`, though the `network` node could belong to the _hidden Markov network_ concept.

```
                   ###########                  ######
                  ## Kohonen ###                ######  Neural Network concept
~~~~~~~~~~  ############|################       ######
~ Markov------network ##|####### Widrow ###
 ~~|~~~~~~   ##|###\####|#######/######\#####   ~~~~~~
~~~|~~~~~~~~~~~|~~##\###|##/---+ ##### Hoff #   ~~~~~~  Markov Network concept
~ HMM-------hidden # neural-----------/#####    ~~~~~~
~~~~~~~~~~~~~~~~~~ #######################
                                                ------  Links
```

This is true, only if the Concept Network was designed in order to associate conceptually near symbols.


# Node #

Each node has these fields:

> - symbol (S):
> > it contains the symbolic information.

> - occurrence (occ):
> > number of times it occurred (in ECTOR case, how many times it appeared in user's utterance).

> - type (Ty):
> > what type of node it is (depends on the application). For ECTOR, they can be "token", "sentence", "sentiment", "expression", "utterer", "label", "file", .... See NodeType.

> - state (AV):
> > the ActivationValue of the node, within a whole ConceptNetworkState.

# Link #

Each ConceptNetwork link comes from node. Its is directed to another node, and has following fields:


> - node
> > the node pointed by this link

> - weight
> > the influence that the departure node has on the arrival node, that one can also see as a conceptual proximity of the two related nodes. This LinkWeight is computed, according to the incoming node's occurrence and the co-occurrence of the two nodes.

> - label
> > optional label node, turning the link into a labeled link

The next figure shows an a minimal Concept Network sample, where the birthday node is completely activated (100%). This node is linked to cake, whose activation value is zero. This link's type is eat, and is weight 95%. This network is an abstract representation of the fact that for an anniversary, one often eats a cake.
```
/----------------\                             /--------------\
|   S: birthday  |                             |    S: cake   |
+----------------+                             +--------------+
| Ty: token      |     /-----------------\     | Ty: token    |
| AV: 100 %      +-----+ T: eat | W: 95% +---->+ AV:  0%      |
\----------------/     \-----------------/     \--------------/
```
Like in neural networks, the activation value from birthday will be propagated to cake, thanks to the ActivationPropagation mechanism.