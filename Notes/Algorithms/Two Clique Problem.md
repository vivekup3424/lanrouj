A Clique is a subgraph of graph such that all vertices in subgraph are completely connected with each other. Given a Graph, find if it can be divided into two Cliques.

**Examples:**

Input : G[][] =   {{0, 1, 1, 0, 0},
                  {1, 0, 1, 1, 0},
                  {1, 1, 0, 0, 0},
                  {0, 1, 0, 0, 1},
                  {0, 0, 0, 1, 0}};
Output : Yes

![graph divided in two cliques](https://media.geeksforgeeks.org/wp-content/cdn-uploads/TwoClique1.png)

This problem looks tricky at first, but has a simple and interesting solution. A graph can be divided in two cliques if its complement graph is [Bipartitite](https://www.geeksforgeeks.org/bipartite-graph/). So below are two steps to find if graph can be divided in two Cliques or not. 

- Find the complement of Graph. Below is the complement graph is above shown graph. In complement, all original edges are removed. And the vertices which did not have an edge between them, now have an edge connecting them. 

![twoclique2](https://media.geeksforgeeks.org/wp-content/cdn-uploads/TwoClique2.png)

- Return true if complement is Bipartite, else false. The above shown graph is Bipartite. Checking whether a Graph is Bipartite or no is discussed [here](https://www.geeksforgeeks.org/bipartite-graph/).

**How does this work?**   
If complement is Bipartite, then graph can be divided into two sets U and V such that there is no edge connecting to vertices of same set. This means in original graph, these sets U and V are completely connected. Hence original graph could be divided in two Cliques.

**Implementation:**   
Below is the implementation of above steps. 