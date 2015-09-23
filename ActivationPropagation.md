# Introduction #

In the ConceptNetwork, activation value is propagated from one node to another, through the links.


# Example #

Let's start from the example shown in the ConceptNetwork explanation.
```
/--------------\                             /------------\
| S: birthday  |                             |  S: cake   |
+--------------+                             +------------+
| Ty: token    |          /--------\         | Ty: token  |
| AV: 100 %    +----------+ W: 95% +---------+ AV:  0%    |
\--------------/          \--------/         \------------/
```

Propagating the activation value of `birthday` through the link (which could be called `eat`) to the node `cake` will give the following Concept Network:
```
/--------------\                             /------------\
| S: birthday  |                             |  S: cake   |
+--------------+                             +------------+
| Ty: token    |          /--------\         | Ty: token  |
| AV:  60 %    +----------+ W: 95% +---------+ AV:  75 %  |
\--------------/          \--------/         \------------/
```

The **activation value** _AV<sup>t+1</sup><sub>i</sub>_ of a node _i_ at the instant _t + 1_, after propagation, is expressed as the sum of its old activation value _AV<sup>t</sup><sub>i</sub>_ and the other nodes' influence _I<sub>i</sub>_, minus a decay _D<sub>i</sub>_, depending on its decay rate _DR<sub>i</sub>_.

The **decay rate** of a node depends on its NodeType. For a token, it is 40.

_AV<sup>t+1</sup><sub>i</sub>_ = _AV<sup>t</sup><sub>i</sub>_ + _I<sub>i</sub>_ - _D<sub>i</sub>_

The **influence** of other nodes could be given by this classical formula:

_I<sub>i</sub>_ = (Σj≠i _AV<sub>j</sub>_ x _W<sub>ji</sub>_) / 100

but it lets an unbalanced influence between nodes with many neighbors (influencing them) and nodes with almost none.

That's the reason why the ConceptNetwork uses a little more complicated influence, with a logarithmic behavior.

As the `birthday` node has no incoming link, _I<sub>birthday</sub>_ is null.

_D<sub>birthday</sub>_ = _DR<sub>birthday</sub>_ x _AV<sub>birthday</sub>_ / 100 = 40 x 100 / 100 = 40

So, its new activation value _AV<sub>1</sub>_ = _AV<sub>0</sub>_ + _I_ - _D_ = 100 + 0 - 40 = 60.

As far as the `cake` node is concerned, it is different: its activation value is null, and so is its decay. However, it is influenced by `birthday`:

_I<sub>cake</sub>_ = (_AV<sup>0</sup><sub>birthday</sub>_ x _W<sub>birthday,cake</sub>_) / ( 100 x _Div<sub>cake</sub>_ ) = 100 x 95 / ( 100 x _Div<sub>cake</sub>_ ) = 95 / _Div<sub>cake</sub>_

_Div<sub>cake</sub>_ = ln 4 / ln 3 ~ 1.26, so _I<sub>cake</sub>_ ~ 75.

Then, _A<sup>1</sup><sub>birthday</sub>_ = 0 + 60 - 0 = 60

In this example, one could add a `candle` node, that would be associated to the `cake` and `birthday` symbols. One could add a link from `cake` to `candle` **labeled** by `birthday`; so, when `birthday` and `cake` are both activated, this link activate `candle`.