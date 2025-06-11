A Hamiltonian cycle is a fundamental concept in graph theory. It's a path in an undirected or directed graph that visits each vertex exactly once and returns to the starting vertex. In other words, it's a cycle that passes through every vertex in the graph exactly once, with the exception of the starting vertex, which is also the ending vertex.

## Key Properties

- A Hamiltonian cycle must visit every vertex in the graph exactly once
- It must return to the starting vertex, forming a complete cycle
- The graph must be connected for a Hamiltonian cycle to exist
- Unlike Eulerian cycles (which visit every edge once), Hamiltonian cycles focus on visiting every vertex once

## Example with Step-by-Step Explanation

Let's work through a concrete example to understand this better.

Consider a graph with 5 vertices labeled A, B, C, D, and E with the following edges:

- A connects to B, C, and E
- B connects to A, C, and D
- C connects to A, B, and D
- D connects to B, C, and E
- E connects to A and D

We can visualize this as a pentagon with some additional connections across it.

Now, let's find a Hamiltonian cycle in this graph:

1. Start at vertex A
2. Move to vertex B
3. Move to vertex D
4. Move to vertex C
5. Move to vertex E
6. Return to vertex A (our starting point)

The complete cycle is A → B → D → C → E → A. This is a Hamiltonian cycle because:

- It visits every vertex exactly once (A, B, C, D, and E)
- It returns to the starting vertex (A)
- It forms a valid path (each consecutive pair of vertices in our sequence is connected by an edge in the graph)

## Contrast with Non-Hamiltonian Graphs

Not all graphs contain Hamiltonian cycles. For example, consider a simple "star" graph with vertex A in the center, connected to vertices B, C, D, and E, but with no connections between B, C, D, and E. In this graph, it's impossible to create a path that visits each vertex exactly once and returns to the start.

## Computational Complexity

Determining whether a Hamiltonian cycle exists in a given graph is an NP-complete problem, which means there's no known efficient algorithm that can solve it for all graphs in polynomial time. This complexity is one reason why the Traveling Salesman Problem (which seeks the shortest Hamiltonian cycle) is so challenging.

## Applications

Hamiltonian cycles have numerous applications:

- Circuit design in electronics
- Operations research for scheduling and routing
- Network design and analysis
- Game theory (such as the Knight's Tour problem in chess)

## Another Practical Example

Imagine planning a road trip through five cities where you want to visit each city exactly once and return to your starting point. If we represent each city as a vertex and the roads between them as edges, finding a valid route for your trip is equivalent to finding a Hamiltonian cycle in the graph.

For instance, if the cities are New York (NY), Boston (BO), Chicago (CH), Denver (DE), and Los Angeles (LA), and there are direct routes between certain pairs of cities, a valid Hamiltonian cycle might be: NY → BO → CH → DE → LA → NY

This means you can travel from New York to Boston, then to Chicago, Denver, Los Angeles, and finally back to New York, visiting each city exactly once.

Understanding Hamiltonian cycles helps us solve many practical problems involving visiting locations exactly once in a connected sequence.