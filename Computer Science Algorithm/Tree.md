# Definition
In [computer science](https://en.wikipedia.org/wiki/Computer_science "Computer science"), a **tree** is a widely used [abstract data type](https://en.wikipedia.org/wiki/Abstract_data_type "Abstract data type") that simulates a hierarchical [tree structure](https://en.wikipedia.org/wiki/Tree_structure "Tree structure"), with a root value and subtrees of children with a [parent node](https://en.wikipedia.org/wiki/Tree_(data_structure)#Terminology), represented as a set of linked [nodes](https://en.wikipedia.org/wiki/Node_(computer_science) "Node (computer science)"). In constrast to [linear data structures](https://en.wikipedia.org/wiki/Linear_data_structure "Linear data structure"), trees cannot be represented by relationships between neighboring nodes in a single straight line.

A tree data structure can be defined [recursively](https://en.wikipedia.org/wiki/Recursion "Recursion") as a collection of nodes, where each node is a data structure consisting of a value and a list of references to nodes. The start of the tree is the "root node" and the reference nodes are the "children". No reference is duplicated and none points to the root.

Alternatively, a tree can be defined abstractly as a whole (globally) as an [ordered tree](https://en.wikipedia.org/wiki/Ordered_tree "Ordered tree"), with a value assigned to each node. Both these perspectives are useful: while a tree can be analyzed mathematically as a whole, when actually represented as a data structure it is usually represented and worked with separately by node (rather than as a set of nodes and an [adjacency list](https://en.wikipedia.org/wiki/Adjacency_list "Adjacency list") of edges between nodes, as one may represent a [digraph](https://en.wikipedia.org/wiki/Tree_(data_structure)#Digraphs), for instance). For example, looking at a tree as a whole, one can talk about "the parent node" of a given node, but in general, as a data structure, a given node only contains the list of its children but does not contain a reference to its parent (if any).
![[Pasted image 20220402093003.png]]
## Node
Nodes are often arranged into tree structures. A node represents the information contained in a single data structure. These nodes may contain a value or condition, or possibly serve as another independent data structure. Nodes are represented by a single parent node. The highest point on a tree structure is called a root node, which does not have a parent node, but serves as the parent or 'grandparent' of all of the nodes below it in the tree. The height of a node is determined by the total number of edges on the path from that node to the furthest leaf node, and the height of the tree is equal to the height of the root node. Node depth is determined by the distance between that particular node and the root node. The root node is said to have a depth of zero. Data can be discovered along these network paths. An IP address uses this kind of system of nodes to define its location in a network.

### Definitions
-   **Child**: A child node is a node extending from another node. For example, a computer with internet access could be considered a child node of a node representing the internet. The inverse relationship is that of a **parent node**. If node _C_ is a child of node _A_, then _A_ is the parent node of _C_.
-   **Degree**: the degree of a node is the number of children of the node.
-   **Depth**: the depth of node _A_ is the length of the path from _A_ to the root node. The root node is said to have depth 0.
-   **Edge**: the connection between nodes.
-   **Forest**: a set of trees.
-   **Height**: the height of node _A_ is the length of the longest path through children to a leaf node.
-   **Internal node**: a node with at least one child.
-   **Leaf node**: a node with no children.
-   **Root node**: a node distinguished from the rest of the tree nodes. Usually, it is depicted as the highest node of the tree.
-   **Sibling nodes**: these are nodes connected to the same parent node.
