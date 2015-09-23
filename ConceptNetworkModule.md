# Introduction #

Version 0.1 of pyECTOR has only one module usable: ConceptNetwork.py.
Let's see what it can do.


# Run it #

src/ConceptNetwork.py is a import module, and is aimed to be used by Ector.py, but it can also be run as a autonomous program. If you are in a shell, in the root directory of the project, you can type:
```
python src/ConceptNetwork.py
```

# Use it #

When started, it loads an optional concept network from a file named `conceptnetwork.pkl`.
But the first time you run it, the ConceptNetwork is empty.

## Add node ##
You can add a basic node using the `@addnode` command, like that:
```
@addnode from
Node "from" added
```
All the text after the command becomes the symbol of the new node.

## Add link ##
To create a link, you need at least two nodes. So, let's create another one:
```
@addnode to
Node "to" added
```

**Note:** you could add a node which symbol contains a space, but you would not be able to link it to another node, as the separator of the `@addlink`'s parameters is _space_.

```
@addlink from to
<__main__.Link instance at 0x01356440>
```
This command creates a link from the "from" node to the "to" node. The command displays the representation of the python object created, so you can know it has succeeded.

## Display nodes ##
You can always display all nodes in the ConceptNetwork:
```
@shownodes
from (basic): 1
to (basic): 1
```
The `@shownodes` command displays one node per line:
  * the symbol of the node
  * the type of the node (`basic` for all nodes added thanks to `@addnode`command)
  * the occurrence of the node (the number of times the symbol has been added in the ConceptNetwork).

## Activate a node ##
In order to enable the ActivationPropagation, one needs to activate at least one node (setting its ActivationValue to 100 or less):
```
@activate from
```
In version 0.1, this command does not yield any output.

## Display the activation values of the nodes ##
To see the state of the ConceptNetwork, use `@showstate`:
```
@showstate
oldav	av	age	Node
100	13	1	from(basic)
0	63	0	to(basic)
```
This command displays only the state of the nodes which have been active in less than 50 ActivationPropagations:
  * old activation: the activation of the node at the beginning of the last activation propagation
  * activation value: the ActivationValue of the node at the end of the last activation propagation
  * age: number of activation propagations since the first activation of the node
  * node: symbol (type) of the node, which is the id of the node.

## Online help ##
Except this page, you can use the `@help` command, which displays a list of the available commands:
```
@help
@help give this help
@addnode name: add the node given
@addlink node1 node2 [label]: add a link from node1 to node2
@activate name [activation value]: activate a node from its name
@propagate [nb]: propagate the activation nb times
@shownodes: show the nodes in the ConceptNetwork
@showlinks: show the links in the ConceptNetwork
@showstate: show the state of the nodes
@save: save the Concept Network and its state
@quit: quit without saving
```