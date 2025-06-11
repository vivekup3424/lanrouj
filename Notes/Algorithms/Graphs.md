---
id: Graphs
aliases: []
tags:
  - introduction
  - graph
---

# Motivation
So graph is the most important topic for a Computer Science student according to me.
I have in my Bachelor's studied so many algorithms and problems related to graphs
Infact most of the problems of mathematics and computer science can be reduced to
graphs

# What does it made up of ?
Graph is a network where two things
1. (nodes)
2. edges

![[graph_intro.png]]

For more information see this [[https://en.wikipedia.org/wiki/Graph_(discrete_mathematics)]]

# Representation of Graph Data Structure

There are multiple ways to store a graph: The following are the most common representations.

- Adjacency Matrix
- Adjacency List

### [Adjacency Matrix Representation of Graph Data Structure:](https://www.geeksforgeeks.org/adjacency-matrix)

In this method, the graph is stored in the form of the 2D matrix where rows and columns denote vertices. Each entry in the matrix represents the weight of the edge between those vertices. 

![adjacency_mat1-(1)-copy](https://media.geeksforgeeks.org/wp-content/uploads/20240502183320/adjacency_mat1-(1)-copy.webp)

Below is the implementation of Graph Data Structure represented using Adjacency Matrix:

```c++
void addEdge(vector<vector<int>> &mat, int i, int j)
{
    mat[i][j] = 1;
    mat[j][i] = 1; // Since the graph is undirected
}

void displayMatrix(vector<vector<int>> &mat)
{
    int V = mat.size();
    for (int i = 0; i < V; i++)
    {
        for (int j = 0; j < V; j++)
            cout << mat[i][j] << " ";
        cout << endl;
    }
}

```

### [Adjacency List Representation of Graph:](https://www.geeksforgeeks.org/adjacency-list-meaning-definition-in-dsa)

This graph is represented as a collection of linked lists. There is an array of pointer which points to the edges connected to that vertex. 

![](https://media.geeksforgeeks.org/wp-content/uploads/20200630125356/adjacency_list.jpg)

Below is the implementation of Graph Data Structure represented using Adjacency List:
```c++
// Function to add an edge between two vertices
void addEdge(vector<vector<int>>& adj, int i, int j) {
    adj[i].push_back(j);
    adj[j].push_back(i); // Undirected
}
```

#### Comparison between Adjacency Matrix and Adjacency List

When the graph contains a large number of edges then it is good to store it as a matrix because only some entries in the matrix will be empty. An algorithm such as [Prim’s](https://www.geeksforgeeks.org/prims-minimum-spanning-tree-mst-greedy-algo-5) and [Dijkstra](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7) adjacency matrix is used to have less complexity.


| Action           | Adjacency Matrix | Adjacency List |
| ---------------- | ---------------- | -------------- |
| Adding Edge      | O(1)             | O(1)           |
| Removing an edge | O(1)             | O(N)           |
| Initializing     | O(N*N)           | O(N)           |

## Real-Life Applications of Graph Data Structure:

Graph Data Structure has numerous real-life applications across various fields. Some of them are listed below:

![](https://media.geeksforgeeks.org/wp-content/uploads/20200630130949/applications_graph.jpg)

- If we recall all the previous data structures that we have studied like array, linked list, tree, etc. All these had some restrictions on structure (mostly linear and tree hierarchical which means no loops). Graph allows random connections between nodes which is useful in many real world problems where do have restrictions of previous data structures.
- Used heavily in social networks. Everyone on the network is a vertex (or node) of the graph and if connected, then there is an edge. Now imagine all the features that you see, mutual friends, people that follow you, etc can seen as graph problems.
- Used to represent the topology of computer networks, such as the connections between routers and switches.
- Used to represent the connections between different places in a transportation network, such as roads and airports.
- ****Neural Networks:**** Vertices represent neurons and edges represent the synapses between them. Neural networks are used to understand how our brain works and how connections change when we learn. The human brain has about 10^11 neurons and close to 10^15 synapses.
- ****Compilers:**** Graph Data Structure is used extensively in compilers. They can be used for type inference, for so-called data flow analysis, register allocation, and many other purposes. They are also used in specialized compilers, such as query optimization in database languages.
- ****Robot planning:**** Vertices represent states the robot can be in and the edges the possible transitions between the states. Such graph plans are used, for example, in planning paths for autonomous vehicles.
- Dependencies in a software project (or any other type of project) can be seen as graph and generating a sequence to solve all tasks before dependents is a standard graph topological sorting algorithm.
- For optimizing the cost of connecting all locations of a network. For example, minimizing wire length in a wired network to make sure all devices are connected is a standard Graph problem called Minimum Spanning Tree.

## Cycles and circuits in the graph
1. [[Hamiltonian Path]]