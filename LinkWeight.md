# Introduction #

The weight of a link, or the _influence_ of the incoming node to the outgoing one, is computed depending on the incoming node's occurrence and on the co-occurrence of the two nodes (co-occurrence is an attribute of the link).


# Details #

When the link is not labeled, the formula is simple:

_weight<sub>ij</sub>_ = _co-occ<sub>ij</sub>_ / _occ<sub>i</sub>_

When the link is labeled (say, by node _l_):

_weight<sub>ij</sub>_ = ( 1 - _co-occ<sub>ij</sub>_ / _occ<sub>i</sub>_ ) x _AV<sub>l</sub>_ / 100