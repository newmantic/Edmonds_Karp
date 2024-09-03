# Edmonds_Karp


The Edmonds-Karp algorithm is an implementation of the Ford-Fulkerson method for computing the maximum flow in a flow network. It uses a breadth-first search (BFS) to find the shortest augmenting path in terms of the number of edges. This algorithm ensures that each augmenting path has the minimum possible number of edges from the source to the sink.


A flow network is a directed graph G = (V, E) where:
V is a set of vertices.
E is a set of directed edges.
Each edge (u, v) in E has a capacity c(u, v), which represents the maximum amount of flow that can pass through the edge.
The flow f(u, v) along an edge (u, v) must satisfy:
Capacity constraint: 0 <= f(u, v) <= c(u, v)
Flow conservation: For every vertex u (except for the source s and the sink t), the total flow into u equals the total flow out of u.

The goal of the maximum flow problem is to find the maximum possible flow from a source vertex s to a sink vertex t in a flow network.

An augmenting path is a path from the source s to the sink t in the residual graph where the residual capacity c_f(u, v) = c(u, v) - f(u, v) is positive for every edge (u, v) on the path.

The residual graph G_f of a flow network G is a graph that represents the remaining capacities after considering the flow f.
If there is a flow f(u, v) from u to v:
The edge (u, v) in the residual graph has a capacity c_f(u, v) = c(u, v) - f(u, v).
There is also a backward edge (v, u) in the residual graph with a capacity c_f(v, u) = f(u, v).



Initialization:
Start with an initial flow f(u, v) = 0 for all edges (u, v) in G.
Construct the initial residual graph G_f.

Breadth-First Search (BFS):
Use BFS to find the shortest augmenting path P from the source s to the sink t in the residual graph G_f.
The bottleneck capacity of the path P is bottleneck(P) = min(c_f(u, v)) for all edges (u, v) on the path.

Augment Flow:
Increase the flow along the path P by bottleneck(P).
Update the residual graph G_f by subtracting bottleneck(P) from the forward edges and adding it to the backward edges.

Repeat:
Repeat the BFS and augmenting steps until no more augmenting paths can be found (i.e., BFS fails to find a path from s to t).

Termination:
The algorithm terminates when no more augmenting paths are found, and the current flow f is the maximum flow from s to t.


Let:
G = (V, E) be the flow network.
c(u, v) be the capacity of edge (u, v).
f(u, v) be the flow through edge (u, v).
G_f be the residual graph.
s be the source vertex.
t be the sink vertex.

Initialization:
For each edge (u, v) in E:
    f(u, v) = 0
    f(v, u) = 0
    
Residual Capacity:
c_f(u, v) = c(u, v) - f(u, v)
c_f(v, u) = f(u, v)

BFS to Find Augmenting Path:
Perform BFS from s to t in G_f.
If an augmenting path P is found, find the bottleneck capacity:
    bottleneck(P) = min(c_f(u, v)) for all (u, v) in P
    
Augment Flow:
For each edge (u, v) in P:
    f(u, v) = f(u, v) + bottleneck(P)
    f(v, u) = f(v, u) - bottleneck(P)
    
Repeat:
Repeat BFS and augment flow until no augmenting path can be found.


The time complexity of the Edmonds-Karp algorithm is O(V * E^2), where V is the number of vertices and E is the number of edges. This is because each BFS runs in O(E) time, and the maximum number of augmenting paths found is O(E * V).
